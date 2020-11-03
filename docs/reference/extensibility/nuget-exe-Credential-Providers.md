---
title: 자격 증명 공급자 nuget.exe
description: nuget.exe 자격 증명 공급자는 피드를 사용 하 여 인증 하며, 특정 규칙을 따르는 명령줄 실행 파일로 구현 됩니다.
author: karann-msft
ms.author: karann
ms.date: 12/12/2017
ms.topic: conceptual
ms.openlocfilehash: 41e3e63138351bafd5e3a56080268faef10d85a3
ms.sourcegitcommit: b138bc1d49fbf13b63d975c581a53be4283b7ebf
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 11/03/2020
ms.locfileid: "93238116"
---
# <a name="authenticating-feeds-with-nugetexe-credential-providers"></a>nuget.exe 자격 증명 공급자를 사용 하 여 피드 인증

에서 버전 `3.3` 지원은 `nuget.exe` 특정 자격 증명 공급자에 대해 추가 되었습니다. 이후 `4.8` 모든 명령줄 시나리오에서 작동 하는 [자격 증명 공급자에 대 한 버전 지원](NuGet-Cross-Platform-Authentication-Plugin.md) ( `nuget.exe` , `dotnet.exe` , `msbuild.exe` )이 추가 되었습니다.

의 모든 인증 방법에 대 한 자세한 내용은 [인증 된 피드의 패키지](../../consume-packages/consuming-packages-authenticated-feeds.md#nugetexe) 사용을 참조 하세요. `nuget.exe`

## <a name="nugetexe-credential-provider-discovery"></a>자격 증명 공급자 검색 nuget.exe

nuget.exe 자격 증명 공급자는 다음과 같은 세 가지 방법으로 사용할 수 있습니다.

- **전역적** 으로: 모든 인스턴스에서 현재 사용자의 프로필로 자격 증명 공급자를 사용할 수 있도록 하려면 `nuget.exe` 에 추가 `%LocalAppData%\NuGet\CredentialProviders` 합니다. 폴더를 만들어야 할 수도 있습니다 `CredentialProviders` . 자격 증명 공급자는 폴더의 루트 또는 하위 폴더에 설치할 수 있습니다 `CredentialProviders`  . 자격 증명 공급자가 여러 파일/어셈블리를 사용 하는 경우 하위 폴더를 사용 하 여 공급자를 구성 된 상태로 유지할 수 있습니다.

- **환경 변수에서** : 자격 증명 공급자를 어디에 든 저장 하 고 `nuget.exe` 환경 변수를 공급자 위치로 설정 하 여에 액세스할 수 있습니다 `%NUGET_CREDENTIALPROVIDERS_PATH%` . 여러 위치가 있는 경우이 변수는 세미콜론으로 구분 된 목록 (예:) 일 수 있습니다 `path1;path2` .

- **nuget.exe와 함께** nuget.exe 자격 증명 공급자를와 동일한 폴더에 배치할 수 있습니다 `nuget.exe` .

자격 증명 공급자를 로드할 때는 `nuget.exe` 위의 위치에서 라는 파일을 순서 대로 검색 `credentialprovider*.exe` 한 다음 해당 파일을 찾은 순서 대로 로드 합니다. 동일한 폴더에 여러 자격 증명 공급자가 있으면 알파벳 순서로 로드 됩니다.

## <a name="creating-a-nugetexe-credential-provider"></a>nuget.exe 자격 증명 공급자 만들기

자격 증명 공급자는 형식으로 이름이 지정 되 고, `CredentialProvider*.exe` 입력을 수집 하 고, 적절 한 자격 증명을 얻은 다음, 적절 한 종료 상태 코드와 표준 출력을 반환 하는 명령줄 실행 파일입니다.

공급자는 다음을 수행 해야 합니다.

- 자격 증명 획득을 시작 하기 전에 대상 URI에 대 한 자격 증명을 제공할 수 있는지 여부를 확인 합니다. 그렇지 않으면 자격 증명 없이 상태 코드 1을 반환 해야 합니다.
- 수정 하지 않습니다 `Nuget.Config` (예: 자격 증명 설정).
- NuGet은 플러그 인에 프록시 정보를 제공 하지 않으므로 자체에서 HTTP 프록시 구성을 처리 합니다.
- `nuget.exe`Utf-8 인코딩을 사용 하 여 JSON 응답 개체 (아래 참조)를 stdout에 기록 하 여 자격 증명 또는 오류 정보를에 반환 합니다.
- 필요에 따라 stderr로 추가 추적 로깅을 내보냅니다. 세부 정보 표시 수준이 "정상" 또는 "자세히" 인 경우에는 NuGet에 의해 콘솔에 대 한 자세한 정보가 표시 되기 때문에 stderr에는 비밀 정보가 기록 되지 않습니다.
- 이후 버전의 NuGet과의 호환성을 제공 하 여 예기치 않은 매개 변수를 무시 해야 합니다.

### <a name="input-parameters"></a>입력 매개 변수

| 매개 변수/스위치 |Description|
|----------------|-----------|
| Uri {value} | 자격 증명을 요구 하는 패키지 소스 URI입니다.|
| NonInteractive | 제공 되는 경우 공급자는 대화형 프롬프트를 실행 하지 않습니다. |
| IsRetry | 표시 되는 경우이 시도는 이전에 실패 한 시도를 다시 시도 함을 나타냅니다. 일반적으로 공급자는이 플래그를 사용 하 여 기존 캐시를 우회 하 고 가능한 경우 새 자격 증명을 묻는 메시지를 표시 합니다.|
| 자세한 정도 {value} | 있는 경우 "normal", "quiet" 또는 "detailed" 중 하나입니다. 값을 지정 하지 않으면 기본적으로 "normal"이 됩니다. 공급자는 표준 오류 스트림으로 내보낼 선택적 로깅 수준에 대 한 표시로이를 사용 해야 합니다. |

### <a name="exit-codes"></a>종료 코드

| 코드 |결과 | Description |
|----------------|-----------|-----------|
| 0 | 성공 | 자격 증명을 성공적으로 획득 하 고 stdout에 썼습니다.|
| 1 | ProviderNotApplicable | 현재 공급자가 지정 된 URI에 대 한 자격 증명을 제공 하지 않습니다.|
| 2 | 실패 | 공급자는 지정 된 URI에 대 한 올바른 공급자 이지만 자격 증명을 제공할 수 없습니다. 이 경우 nuget.exe는 인증을 다시 시도 하지 않고 실패 합니다. 일반적으로 사용자가 대화형 로그인을 취소 한 경우를 들 수 있습니다. |

### <a name="standard-output"></a>표준 출력

| 속성 |메모|
|----------------|-----------|
| 사용자 이름 | 인증 된 요청에 대 한 사용자 이름입니다.|
| 암호 | 인증 된 요청에 대 한 암호입니다.|
| 메시지 | 실패 사례에 추가 세부 정보를 표시 하는 데에만 사용 되는 응답에 대 한 선택적 세부 정보입니다. |

예 stdout:

    { "Username" : "freddy@example.com",
      "Password" : "bwm3bcx6txhprzmxhl2x63mdsul6grctazoomtdb6kfbof7m3a3z",
      "Message"  : "" }

## <a name="troubleshooting-a-credential-provider"></a>자격 증명 공급자 문제 해결

현재, NuGet은 사용자 지정 자격 증명 공급자를 디버깅 하는 데 많은 직접적인 지원을 제공 하지 않습니다. [문제 4598](https://github.com/NuGet/Home/issues/4598) 에서이 작업을 추적 하 고 있습니다.

다음 작업도 수행할 수 있습니다.

- 스위치를 사용 하 여 nuget.exe `-verbosity` 를 실행 하 여 자세한 출력을 검사 합니다.
- 적절 한 위치에서에 디버그 메시지를 추가 `stdout` 합니다.
- nuget.exe 3.3 이상을 사용 하 고 있는지를 알고 있어야 합니다.
- 시작 시 다음 코드 조각으로 디버거를 연결 합니다.

    ```cs
    while (!Debugger.IsAttached)
    {
        System.Threading.Thread.Sleep(100);
    }
    Debugger.Break();
    ```
