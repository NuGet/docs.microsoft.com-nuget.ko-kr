---
ms.openlocfilehash: 5197447531288a8b071354dbeb3a3ae02f7cce09
ms.sourcegitcommit: 39f2ae79fbbc308e06acf67ee8e24cfcdb2c831b
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 11/05/2019
ms.locfileid: "73610527"
---
#### <a name="windows"></a>Windows

> [!Note]
> NuGet.exe 5.0 이상을 실행하려면 .NET Framework 4.7.2 이상이 필요합니다.

1. [nuget.org/downloads](https://nuget.org/downloads)를 방문하고 NuGet 3.3 이상을 선택합니다(2.8.6은 Mono와 호환되지 않음). 언제나 최신 버전이 권장되며, 패키지를 nuget.org에 게시하려면 4.1.0 이상이 필요합니다.
1. 각 다운로드는 `nuget.exe` 파일을 직접 다운로드합니다. 브라우저의 지침에 따라 선택한 폴더에 파일을 저장합니다. 파일은 설치 관리자가 ‘아니며’, 브라우저에서 직접 실행하는 경우 아무것도 표시되지 않습니다. 
1. `nuget.exe`를 둔 폴더를 PATH 환경 변수에 추가하여 어디서나 CLI 도구를 사용합니다.

#### <a name="macoslinux"></a>macOS/Linux

OS 배포에 따라 동작이 약간 다를 수 있습니다.

1. [Mono 4.4.2 이상](https://www.mono-project.com/docs/getting-started/install/)을 설치합니다.

1. 셸 프롬프트에서 다음 명령을 실행합니다.

    ```bash
    # Download the latest stable `nuget.exe` to `/usr/local/bin`
    sudo curl -o /usr/local/bin/nuget.exe https://dist.nuget.org/win-x86-commandline/latest/nuget.exe
    ```

1. 다음 스크립트를 OS에 해당하는 파일에 추가하여 별칭을 만듭니다(일반적으로 `~/.bash_aliases` 또는 `~/.bash_profile`).

    ```bash
    # Create as alias for nuget
    alias nuget="mono /usr/local/bin/nuget.exe"
    ```

1. 셸을 다시 로드합니다.  매개 변수 없이 `nuget`을 입력하여 설치를 테스트합니다. NuGet CLI 도움말이 표시됩니다.
