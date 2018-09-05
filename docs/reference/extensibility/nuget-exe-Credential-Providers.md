---
title: nuget.exe 자격 증명 공급자
description: nuget.exe 자격 증명 공급자는 피드를 사용 하 여 인증 하 고 특정 규칙을 따르는 명령줄 실행 파일로 구현 됩니다.
author: karann-msft
ms.author: karann
ms.date: 12/12/2017
ms.topic: conceptual
ms.openlocfilehash: 97a44c6d561f426fa50fa068a9bbf793f77a3111
ms.sourcegitcommit: 1d1406764c6af5fb7801d462e0c4afc9092fa569
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 09/04/2018
ms.locfileid: "43550191"
---
# <a name="authenticating-feeds-with-nugetexe-credential-providers"></a>Nuget.exe 자격 증명 공급자를 사용 하 여 피드 인증

*NuGet 3.3 이상*

때 `nuget.exe` 피드를 사용 하 여 인증 하려면 자격 증명이 필요에 다음과 같은 방식으로 찾습니다.

1. NuGet에서 자격 증명을 먼저 찾습니다 `Nuget.Config` 파일입니다.
1. NuGet에는 아래에 나와 있는 순서에 따라 플러그 인 자격 증명 공급자를 사용 합니다. (예제 이며 합니다 [Visual Studio Team Services 자격 증명 공급자](https://www.visualstudio.com/docs/package/get-started/nuget/auth#vsts-credential-provider).)
1. NuGet은 명령줄에 자격 증명을 묻는 메시지를 표시 합니다.

여기에 설명 된 자격 증명 공급자 에서만 작동 하는 참고 `nuget.exe` 및 'dotnet restore' 또는 Visual Studio에 없습니다. Visual Studio를 사용 하 여 자격 증명 공급자를 참조 하세요. [nuget.exe Visual Studio에 대 한 자격 증명 공급자](nuget-credential-providers-for-visual-studio.md)

nuget.exe 자격 증명 공급자는 3 가지 방법으로 사용할 수 있습니다.

- **전 세계**: 자격 증명 공급자의 모든 인스턴스를 사용할 수 있도록 `nuget.exe` 현재 사용자의 프로필에서 실행, 추가 `%LocalAppData%\NuGet\CredentialProviders`합니다. 만들어야 할 수 있습니다는 `CredentialProviders` 폴더입니다. 자격 증명 공급자의 루트에 설치할 수는 `CredentialProviders` 폴더 또는 하위 폴더입니다. 자격 증명 공급자를 여러 파일/어셈블리에 있는 경우에 구성 공급자를 유지 하려면 하위 폴더를 사용할 수 있습니다.

- **환경 변수에서**: 자격 증명 공급자를 어디서 나 저장에 액세스할 수 있게 `nuget.exe` 설정 하 여는 `%NUGET_CREDENTIALPROVIDERS_PATH%` 공급자 위치에 환경 변수입니다. 이 변수는 세미콜론으로 구분 된 목록을 사용할 수 있습니다 (예를 들어 `path1;path2`) 여러 위치가 있는 경우.

- **Nuget.exe와 함께**: nuget.exe 자격 증명 공급자와 같은 폴더에 배치할 수 있습니다 `nuget.exe`합니다.

자격 증명 공급자를 로드할 때 `nuget.exe` 위의 위치를 모든 파일에 대 한 순서 대로 검색 `credentialprovider*.exe`, 발견 될 순서에서 해당 파일을 로드 합니다. 여러 자격 증명 공급자 동일한 폴더에 있는 경우 사전순으로 로드 됩니다.

## <a name="creating-a-nugetexe-credential-provider"></a>Nuget.exe 자격 증명 공급자 만들기

자격 증명 공급자는 명령줄 실행 파일을 형태로 `CredentialProvider*.exe`, 입력을 수집 하는, 적절 하 게 자격 증명을 획득 하 고 적절 한 종료 상태 코드 및 표준 출력을 반환 합니다.

공급자는 다음을 수행 해야 합니다.

- 여부를 제공할 수 있습니다 자격 증명을 대상으로 지정 된 URI에 대 한 자격 증명 획득을 시작 하기 전에 확인 합니다. 그렇지 않은 경우 상태 코드 1 자격 증명이 없는 반환 해야 합니다.
- 수정 하지 `Nuget.Config` (예: 자격 증명 설정을).
- 핸들 HTTP 프록시 구성으로 자체 NuGet에서 플러그 인 프록시 정보를 제공 하지 않습니다.
- 자격 증명 또는 오류 세부 정보를 반환 `nuget.exe` stdout으로 utf-8 인코딩을 사용 하 여 JSON 응답 개체 (아래 참조)를 작성 하 여 합니다.
- 필요에 따라 stderr에 로깅을 추가 추적을 내보냅니다. "Normal" 또는 "자세히" 세부 정보 표시 수준에서 추적이 표시 되 면 NuGet에서 콘솔에 있으므로 적이 없습니다 비밀을 stderr에 작성 합니다.
- 예기치 않은 매개 변수를 무시 해야 나중 버전의 NuGet 사용 하 여 이후 버전과 호환성을 제공 합니다.

### <a name="input-parameters"></a>입력된 매개 변수

| 매개 변수/스위치 |설명|
|----------------|-----------|
| Uri {value} | 패키지 원본 URI 필요한 자격 증명입니다.|
| NonInteractive | 있는 경우 공급자는 대화형 프롬프트 발생 하지 않습니다. |
| isRetry | 있는 경우이 시도 재시도는 이전에 실패 한 시도 나타냅니다. 일반적으로 공급자는 모든 기존 캐시 무시 하 고 가능한 경우 새 자격 증명을 요청 하도록이 플래그를 사용 합니다.|
| {Value} 세부 정보 표시 | 있는 경우 다음 값 중 하나: "normal", "quiet" 또는 "자세히"입니다. 변수에 값이 없는 경우 "normal" 기본값은입니다. 공급자를 사용 해야이의 선택적 로깅 수준 확인 하기 위해 표준 오류 스트림에 내보냅니다. |

### <a name="exit-codes"></a>종료 코드

| 코드 |결과 | 설명 |
|----------------|-----------|-----------|
| 0 | 성공 | 자격 증명 성공적으로 획득 된 및 stdout에 기록 되었습니다.|
| 1 | ProviderNotApplicable | 현재 공급자는 지정된 된 URI에 대 한 자격 증명을 제공 하지 않습니다.|
| 2 | 실패 | 공급자는 지정된 된 URI에 대 한 올바른 공급자 하지만 자격 증명을 제공할 수 없습니다. 이 경우 nuget.exe 인증 다시 시도 하지 않습니다 하 고 실패 합니다. 일반적인 예제는 사용자가 대화형 로그인을 취소 하는 경우입니다. |

### <a name="standard-output"></a>표준 출력

| 속성 |노트|
|----------------|-----------|
| 사용자 이름 | 인증 된 요청에 대 한 사용자 이름입니다.|
| 암호 | 인증 된 요청에 대 한 암호입니다.|
| 메시지 | 실패할 경우에서 추가 세부 정보를 표시 하는 데에 사용 하는 응답에 대 한 세부 정보 선택 사항입니다. |

예제에서는 stdout:

    { "Username" : "freddy@example.com",
      "Password" : "bwm3bcx6txhprzmxhl2x63mdsul6grctazoomtdb6kfbof7m3a3z",
      "Message"  : "" }

## <a name="troubleshooting-a-credential-provider"></a>자격 증명 공급자 문제 해결

현재, NuGet 직접 지원 하지 않고 많은 사용자 지정 자격 증명 공급자, 디버깅 [4598 발급](https://github.com/NuGet/Home/issues/4598) 이 작업을 추적 합니다.

다음 작업도 수행할 수 있습니다.

- Nuget.exe 사용 하 여 실행을 `-verbosity` 스위치를 자세한 출력을 검사 합니다.
- 디버그 메시지를 추가 `stdout` 적절 한 위치에 있습니다.
- Nuget.exe 3.3 이상을 사용 해야 합니다.
- 이 코드 조각 사용 하 여 시작 시는 디버거를 연결 합니다.

    ```cs
    while (!Debugger.IsAttached)
    {
        System.Threading.Thread.Sleep(100);
    }
    Debugger.Break();
    ```

추가 도움말을 보려면 [는 nuget.org 지원 요청을 제출](https://www.nuget.org/policies/Contact)합니다.
