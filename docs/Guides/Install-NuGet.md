---
title: "NuGet 클라이언트 도구 설치 | Microsoft Docs"
author: kraigb
ms.author: kraigb
manager: ghogen
ms.date: 10/02/2017
ms.topic: get-started-article
ms.prod: nuget
ms.technology: 
ms.assetid: 683b8b34-a6f4-4d56-b9cd-2483bfbad1ad
description: "클라이언트 도구, CLI(명령줄 인터페이스) 및 Visual Studio용 패키지 관리자 설치에 대한 지침입니다."
keywords: "nuget.exe CLI, NuGet 클라이언트 도구, NuGet 패키지 관리자, NuGet 패키지 관리자 콘솔, Visual Studio용 NuGet, NuGet 베타 채널"
ms.reviewer:
- karann-msft
- unniravindranathan
ms.openlocfilehash: b1abb30458c9ebfb0ffb28be254efd9709a9627f
ms.sourcegitcommit: d0ba99bfe019b779b75731bafdca8a37e35ef0d9
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 12/14/2017
---
# <a name="installing-nuget-client-tools"></a>NuGet 클라이언트 도구 설치

> [!Tip]
> **패키지 설치를 원하십니까? [빠른 시작 - 패키지 사용](../Quickstart/Use-a-Package.md)을 참조하세요.**

NuGet 패키지를 빌드, 게시 및 사용하는 데 사용할 수 있는 두 가지 기본 도구가 있습니다.

1. [**NuGet CLI**](#nuget-cli)는 모든 NuGet 기능을 제공하는 Windows용 명령줄 유틸리티입니다. Mono 또는 .NET Core CLI(`dotnet`)를 사용하여 Mac OSX 및 Linux에서 실행할 수도 있습니다.
1. [**Visual Studio의 NuGet 패키지 관리자**](#nuget-package-manager-in-visual-studio)(Windows 전용)는 패키지를 관리하기 위한 GUI 도구이며, Visual Studio 내에서 특정 NuGet 명령을 직접 사용할 수 있는 PowerShell 콘솔을 포함하고 있습니다. 패키지 관리자 UI 및 콘솔은 모두 Visual Studio(Windows) 2012 이상에 포함되어 있으며 이전 버전에는 수동으로 설치할 수 있습니다.

    Mac용 Visual Studio에는 NuGet 기능이 직접 기본적으로 제공됩니다. 연습은 [프로젝트에 NuGet 패키지 포함](https://docs.microsoft.com/visualstudio/mac/nuget-walkthrough)을 참조하세요.

    현재 Visual Studio Code에는 기본 제공 NuGet 지원이 없습니다. NuGet CLI 또는 [dotnet CLI](../Tools/dotnet-Commands.md)를 사용합니다.

NuGet CLI 및 패키지 관리자는 모두 다음 작업을 지원합니다.

- 패키지 검색
- 패키지 설치
- 패키지 업데이트
- 패키지 제거
- 패키지 복원(패키지 관리자에서 UI만)
- NuGet 원본 관리

다음 기능은 NuGet CLI에서만 지원됩니다.

- 패키지 관리(nuget.org 또는 개인 피드)
- 패키지 만들기 
- 패키지 게시
- Nuget.Config 관리
- NuGet 캐시 관리
- 패키지 복제

> [!Note]
> 또 다른 좋은 도구는 NuGet 패키지를 시각적으로 탐색, 생성 및 편집할 수 있는 오픈 소스 독립 실행형 도구인 [NuGet 패키지 탐색기](https://github.com/NuGetPackageExplorer/NuGetPackageExplorer)입니다. 예를 들어 매번 패키지를 다시 빌드할 필요 없이 패키지 구조를 실험적으로 변경하는 것이 매우 유용합니다.
> .NET Core 응용 프로그램 개발에 사용되는 플랫폼 간 [.NET Core CLI](https://docs.microsoft.com/dotnet/articles/core/tools/index#installation) 도구 체인은 delete, locals, push, pack 및 restore와 같은 몇 가지 NuGet 명령을 지원합니다. 

## <a name="nuget-cli"></a>NuGet CLI

NuGet 명령줄 인터페이스는 모든 NuGet 기능에 대한 액세스를 제공하며, 다음 섹션에서 설명한 대로 Windows, Mac OSX 및 Linux에서 실행할 수 있습니다.

### <a name="windows"></a>Windows

**직접 다운로드:**

[!INCLUDE[install-cli](../includes/install-cli.md)]

> [!Note]
> NuGet 1.4 이상을 사용하면 `nuget update -self`를 사용하여 기존 nuget.exe를 최신 버전으로 업데이트할 수 있습니다.

**다른 방법:**

- **Chocolatey**: [Chocolatey](http://chocolatey.org) 클라이언트를 사용하여 [NuGet.CommandLine](http://chocolatey.org/packages/NuGet.CommandLine) Chocolatey 패키지를 설치합니다. 

    ```ps
    choco install nuget.commandline
    ```

- **Visual Studio**: Visual Studio의 패키지 관리자 콘솔에서 [NuGet.CommandLine](http://www.nuget.org/packages/NuGet.CommandLine/) 패키지를 설치합니다.

    > [!Note]
    > **NuGet 2.x 사용자의 경우**: NuGet 3.2에 도입된 주요 변경으로 인해 [https://nuget.org/nuget.exe](https://nuget.org/nuget.exe)는 지속적인 통합 시스템이 잠재적으로 손상되지 않도록 안정적인 최신 NuGet 2.x 릴리스를 가리킵니다.

<a name="compatibility-with-mono"></a>

## <a name="mac-osx-and-linux"></a>Mac OSX 및 Linux

Mac OSX 및 Linux의 경우 NuGet CLI를 실행하는 다음 두 가지 방법이 있습니다.

- 핵심 NuGet 기능이 포함된 [.NET Core SDK](https://www.microsoft.com/net/download/core)를 설치합니다. 다운로드는 [github.com/dotnet/cli](https://github.com/dotnet/cli)에도 나열되어 있습니다. 더 완벽한 기능이 필요한 경우 아래의 두 번째 옵션을 사용하여 Mono에서 `nuget.exe`를 사용합니다.

- [Mono](http://www.mono-project.com/docs/getting-started/install/)를 설치한 다음 [nuget.org/downloads](https://nuget.org/downloads)에서 `nuget.exe` Windows용 명령줄 실행 파일(버전 3.2 이상)을 사용합니다. Mono에서 NuGet을 실행하는 경우 적용되는 제한 사항은 다음과 같습니다.

    - 제대로 작동하는지 테스트된 명령:
        - config
        - 삭제
        - 도움말
        - install
        - list
        - push
        - setApiKey
        - sources
        - spec

    - 부분적으로 작동하는 명령:
        - pack: `.nuspec` 파일은 사용할 수 있지만 프로젝트 파일은 사용할 수 없습니다.
        - restore: `packages.config` 및 `project.json` 파일은 사용할 수 있지만 솔루션(`.sln`) 파일은 사용할 수 없습니다.

    - 작동하지 않는 명령:
        - 업데이트

### <a name="related-topics"></a>관련 항목

- [NuGet CLI 참조](../tools/nuget-exe-cli-reference.md)
- [패키지 만들기](../create-packages/creating-a-package.md)
- [패키지 게시](../create-packages/publish-a-package.md)

## <a name="nuget-package-manager-in-visual-studio"></a>Visual Studio의 NuGet 패키지 관리자

Windows의 모든 Visual Studio 버전(2012 이상)에는 NuGet 패키지 관리자가 포함됩니다. 여기에는 패키지 관리자 UI([참조](../tools/package-manager-ui.md)) 및 특정 패키지([참조](../tools/package-manager-console.md))와 함께 제공되는 도구에 액세스할 수 있는 패키지 관리자 콘솔이 포함되어 있습니다.

Visual Studio 2017 설치 관리자에는 .NET을 사용하는 모든 워크로드가 있는 NuGet 패키지 관리자가 포함되어 있습니다. 별도로 설치하거나 패키지 관리자가 설치되어 있는지 확인하려면 Visual Studio 2017 설치 관리자를 실행하고 **개별 구성 요소 > 코드 도구 > NuGet 패키지 관리자** 아래에서 옵션을 확인합니다.

> [!Note]
> 콘솔에는 Windows 7 이상 및 Windows Server 2008 R2 이상에 이미 설치되어 있는 [PowerShell 2.0](http://support.microsoft.com/kb/968929)이 필요합니다.
>
> 또한 패키지 관리자 콘솔 명령은 Windows의 Visual Studio 내에서만 작동합니다. Mac용 Visual Studio 및 Visual Studio Code를 포함하여 해당 환경 외부에서 NuGet CLI를 사용합니다.

### <a name="package-manager-installation-for-visual-studio-2010-and-earlier"></a>Visual Studio 2010 및 이전 버전용 패키지 관리자 설치

*패키지 관리자가 이미 포함된 Visual Studio 2012 이상에서는 다음 단계가 필요하지 않습니다.*

1. Visual Studio 2010 및 이전 버전에서는 **도구 > 확장 및 업데이트**를 차례로 클릭합니다.
1. **온라인**으로 이동한 다음 "Visual Studio용 NuGet 패키지 관리자"를 검색하고 **다운로드**를 클릭합니다.
1. 설치 관리자 대화 상자에서 **설치**를 클릭합니다.
1. 설치가 완료되면 Visual Studio를 다시 시작합니다.

> [!Tip]
> Visual Studio에서 **확장 및 업데이트** 대화 상자를 사용할 수 없는 경우(예: 프록시로 인해 차단된 경우) [https://dist.nuget.org/index.html](https://dist.nuget.org/index.html)에서 직접 Visual Studio 2013 및 2015용 확장을 다운로드할 수 있습니다.

### <a name="updating-the-package-manager"></a>패키지 관리자 업데이트

Visual Studio 2015 업데이트 2 이상의 경우, 패키지 관리자는 자동으로 안정적인 최신 릴리스로 업데이트됩니다.

Visual Studio 2015 업데이트 1 및 이전 버전의 경우, **도구 > 확장 및 업데이트**  명령을 선택하고 **업데이트** 탭을 클릭하여 패키지 관리자의 새 버전을 사용할 수 있는지 확인합니다.  

### <a name="nuget-previews"></a>NuGet 미리 보기

예정된 NuGet 기능을 미리 보려면 안정적인 Visual Studio 릴리스와 함께 작동하는 [Visual Studio 2017 미리 보기](https://www.visualstudio.com/vs/preview/)를 설치합니다.

이전의 Visual Studio 2015용 NuGet 베타 채널(`https://dotnet.myget.org/F/nuget-beta/vsix/`)은 더 이상 사용되지 않습니다.

모든 NuGet 릴리스 관련 문제를 보고하거나 아이디어를 공유하려면 [NuGet GitHub 리포지토리](https://github.com/Nuget/Home)에서 문제를 공개해 주세요.

### <a name="related-topics"></a>관련 항목

- [패키지 관리자 UI 참조](../tools/package-manager-ui.md)
- [패키지 관리자 콘솔 참조](../tools/package-manager-console.md)
- [패키지 관리자 콘솔 PowerShell 참조](../tools/powershell-reference.md)