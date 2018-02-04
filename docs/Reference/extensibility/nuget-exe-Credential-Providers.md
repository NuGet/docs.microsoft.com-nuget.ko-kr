---
title: "nuget.exe 자격 증명 공급자 | Microsoft Docs"
author: kraigb
ms.author: kraigb
manager: ghogen
ms.date: 12/12/2017
ms.topic: article
ms.prod: nuget
ms.technology: 
description: "nuget.exe 자격 증명 공급자는 피드를 사용 하 여 인증 하며 특정 규칙을 따르는 명령줄 실행 파일로 구현 됩니다."
keywords: "nuget.exe 자격 증명 공급자, 자격 증명 공급자 API 피드를 사용 하 여 인증, 갤러리를 사용 하 여 인증"
ms.reviewer:
- karann-msft
- unniravindranathan
ms.openlocfilehash: 88ce0106ad4e628ba8120f94b7951c7746ab67f3
ms.sourcegitcommit: 4651b16a3a08f6711669fc4577f5d63b600f8f58
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 02/02/2018
---
# <a name="authenticating-feeds-with-nugetexe-credential-providers"></a>Nuget.exe 자격 증명 공급자를 사용한 피드 인증

*NuGet 3.3 +*

때 `nuget.exe` 피드를 인증 하기 위한 자격 증명이 필요 다음과 같이 찾습니다.

1. NuGet의 자격 증명에 먼저 찾습니다 `Nuget.Config` 파일입니다.
1. NuGet 아래에 나와 있는 순서에 따라 플러그 인 자격 증명 공급자를 사용 합니다. (및 예제는 [Visual Studio Team Services 자격 증명 공급자](https://www.visualstudio.com/docs/package/get-started/nuget/auth#vsts-credential-provider).)
1. NuGet은 명령줄에 자격 증명을 묻는 메시지를 표시합니다.

여기에서 설명 하는 자격 증명 공급자 에서만 작동 하는 참고 `nuget.exe` 'dotnet 복원' 또는 Visual Studio에서가 아니라 합니다. Visual Studio와 함께 자격 증명 공급자를 참조 하십시오. [nuget.exe Visual Studio에 대 한 자격 증명 공급자](nuget-credential-providers-for-visual-studio.md)

nuget.exe 자격 증명 공급자는 세 가지 방법에서 사용할 수 있습니다.

- **전역으로**: 자격 증명 공급자의 모든 인스턴스를 사용할 수 있도록 하려면 `nuget.exe` 현재 사용자의 프로필에서 실행에 추가 `%LocalAppData%\NuGet\CredentialProviders`합니다. 만들어야 할 수는 `CredentialProviders` 폴더입니다. 루트에 자격 증명 공급자를 설치할 수 있습니다는 `CredentialProviders` 폴더 또는 하위 폴더 내 합니다. 자격 증명 공급자는 여러 파일/어셈블리에 있는 경우에 구성 공급자를 유지 하려면 하위 폴더를 사용할 수 있습니다.

- **환경 변수에서**: 자격 증명 공급자를 어디에 저장 하 고 액세스할 수 `nuget.exe` 설정 하 여는 `%NUGET_CREDENTIALPROVIDERS_PATH%` 환경 변수 공급자 위치를 합니다. 이 변수는 세미콜론으로 구분 된 목록이 될 수 있습니다 (예를 들어 `path1;path2`) 여러 위치에 있는 경우.

- **Nuget.exe 함께**: nuget.exe 자격 증명 공급자와 같은 폴더에 배치할 수 있습니다 `nuget.exe`합니다.

자격 증명 공급자를 로드할 때 `nuget.exe` 위의 위치 이름이 인 모든 파일에 대 한 순서 대로 검색 `credentialprovider*.exe`, 하는 순서로 해당 파일을 로드 합니다. 여러 자격 증명 공급자는 같은 폴더에 있으면 알파벳 순서로 로드 일입니다.

## <a name="creating-a-nugetexe-credential-provider"></a>Nuget.exe 자격 증명 공급자 만들기

자격 증명 공급자는 명령줄 실행 파일은 폴더에서 `CredentialProvider*.exe`, 입력을 수집 하는를 적절 하 게 자격 증명을 획득 하 고 적절 한 종료 상태 코드 및 표준 출력을 반환 합니다.

공급자는 다음을 수행 해야 합니다.

- 있는지 여부를 제공할 수 있습니다 자격 증명의 대상된 URI에 대 한 자격 증명 획득을 시작 하기 전에 확인 합니다. 그렇지 않으면 상태 코드는 자격 증명 없이 1을 반환 해야 합니다.
- 수정 하지 `Nuget.Config` (예: 없는 자격 증명을 설정).
- 핸들 HTTP 프록시 구성을으로 자체 NuGet에 플러그 인 프록시 정보를 제공 하지 않습니다.
- 자격 증명 또는에 오류 정보를 반환 `nuget.exe` utf-8 인코딩을 사용 하 여 stdout으로 JSON 응답 개체 (아래 참조)를 작성 하 여 합니다.
- 필요에 따라 stderr에 대 한 추가 추적 로깅을 내보냅니다. "Normal" 또는 "자세히" 자세한 정도 수준에서 추적이 표시 되 면 NuGet에서 콘솔에 있으므로 적이 없는 비밀을 stderr에 작성 합니다.
- 예기치 않은 매개 변수를 무시 해야 NuGet의 이후 버전과 이후 버전과 호환성을 제공 합니다.

### <a name="input-parameters"></a>입력된 매개 변수

| 매개 변수/스위치 |설명|
|----------------|-----------|
| Uri {value} | 패키지 원본 URI 필요한 자격 증명입니다.|
| NonInteractive | 있는 경우 공급자는 대화형 프롬프트를 발급 하지 않습니다. |
| IsRetry | 있는 경우에이 시도이 대해서는 이전에 실패 한 시도의 다시 시도 임을 나타냅니다. 일반적으로 공급자는 모든 기존 캐시를 무시 하 고 가능한 경우 새 자격 증명을 요청 하도록이 플래그를 사용 합니다.|
| 자세한 정도 {value} | 있는 경우 다음 값 중 하나: "normal", "자동" 또는 "자세히"입니다. 변수에 값이 없는 경우에 "보통" 기본값입니다. 공급자를 사용 해야이의 선택적 로깅 수준 표시로 표준 오류 스트림에 내보냅니다. |

### <a name="exit-codes"></a>종료 코드

| 코드 |결과 | 설명 |
|----------------|-----------|-----------|
| 0 | 성공 | 자격 증명을 성공적으로 인식 한 고 stdout에 기록 되었습니다.|
| 1 | ProviderNotApplicable | 현재 공급자는 지정된 된 URI에 대 한 자격 증명을 제공 하지 않습니다.|
| 2 | 실패 | 공급자는 지정된 된 URI에 대 한 올바른 공급자 하지만 자격 증명을 제공할 수 없습니다. 이 경우 nuget.exe 인증을 시도 하지 않습니다 하 고 실패 합니다. 일반적인 예는 사용자가 대화형 로그인을 취소 하는 경우입니다. |

### <a name="standard-output"></a>표준 출력

| 속성 |노트|
|----------------|-----------|
| 사용자 이름 | 인증 된 요청에 대 한 사용자 이름입니다.|
| 암호 | 인증 된 요청에 대 한 암호입니다.|
| 메시지 | 오류 발생 시에서 추가 세부 정보를 표시 하는 데에 사용 하는 응답에 대 한 선택적 세부 정보입니다. |

예제 stdout:

    { "Username" : "freddy@example.com",
      "Password" : "bwm3bcx6txhprzmxhl2x63mdsul6grctazoomtdb6kfbof7m3a3z",
      "Message"  : "" }

## <a name="troubleshooting-a-credential-provider"></a>자격 증명 공급자 문제 해결

현재, NuGet 직접 지원 하지 않고 많은 사용자 지정 자격 증명 공급자; 디버깅을 위해 [4598 발급](https://github.com/NuGet/Home/issues/4598) 이 작업을 추적 합니다.

다음 작업도 수행할 수 있습니다.

- Nuget.exe와 실행의 `-verbosity` 자세한 출력을 검사 하는 스위치입니다.
- 디버그 메시지 추가 `stdout` 적절 한 위치에 있습니다.
- 3.3 이상 nuget.exe를 사용 하는 확인 해야 합니다.
- 이 코드 조각으로 시작할 때 디버거를 연결 합니다.

    ```cs
    while (!Debugger.IsAttached)
    {
        System.Threading.Thread.Sleep(100);
    }
    Debugger.Break();
    ```

자세한 도움말 [는 nuget.org 지원 요청을 제출](https://www.nuget.org/policies/Contact)합니다.
