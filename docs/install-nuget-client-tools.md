---
title: NuGet 클라이언트 도구 설치
description: 클라이언트 도구, dotnet 및 nuget CLI(명령줄 인터페이스) 및 Visual Studio용 패키지 관리자 설치에 대한 지침입니다.
author: karann-msft
ms.author: karann
ms.date: 06/20/2019
ms.topic: quickstart
ms.openlocfilehash: 09c859c0ab6767ea80b6a64c194aa2623ee5c505
ms.sourcegitcommit: 39f2ae79fbbc308e06acf67ee8e24cfcdb2c831b
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 11/05/2019
ms.locfileid: "73610511"
---
# <a name="install-nuget-client-tools"></a>NuGet 클라이언트 도구 설치

> **패키지 설치를 원하십니까? [NuGet 패키지를 설치하는 방법](consume-packages/overview-and-workflow.md#ways-to-install-a-nuget-package)을 참조하세요.**

NuGet으로 작업하려면 패키지 소비자 또는 작성자로서 CLI(명령줄 인터페이스) 도구와 Visual Studio의 NuGet 기능을 사용할 수 있습니다. 이 문서에서는 다양한 도구의 기능, 설치 방법 및 비교 [기능 가용성](#feature-availability)에 대해 간략하게 설명합니다. NuGet으로 패키지 사용을 시작하려면 [패키지 설치 및 사용(dotnet CLI)](quickstart/install-and-use-a-package-using-the-dotnet-cli.md) 및 [패키지 설치 및 사용(Visual Studio)](quickstart/install-and-use-a-package-in-visual-studio.md)을 참조하세요. NuGet 패키지를 만들기 시작하려면 [NET Standard 패키지 만들기 및 게시(dotnet CLI)](quickstart/create-and-publish-a-package-using-the-dotnet-cli.md) 및 [NET Standard 패키지 만들기 및 게시(Visual Studio)](quickstart/create-and-publish-a-package-using-visual-studio.md)를 참조하세요.

| 도구&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; | 설명 | 다운로드&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; |
|:------------- |:-------------|:-----|
| [dotnet.exe](#dotnetexe-cli) | .NET Core 및 .NET Standard 라이브러리와 .NET Framework를 대상으로 하는 것과 같은 [SDK 스타일 프로젝트](resources/check-project-format.md)를 위한 CLI 도구입니다. .NET Core SDK에 포함되며 모든 플랫폼에서 핵심 NuGet 기능을 제공합니다. (Visual Studio 2017부터 dotnet CLI는 모든 .NET Core 관련 워크로드와 함께 자동으로 설치됩니다.)| [.NET Core SDK](https://www.microsoft.com/net/download/) |
| [nuget.exe](#nugetexe-cli) | .NET Framework 라이브러리와 .NET Standard 라이브러리를 대상으로 하는 것과 같은 [비 SDK 스타일 프로젝트](resources/check-project-format.md)를 위한 CLI 도구입니다. Windows에서 모든 NuGet 기능을 제공하며 Mono로 실행 중일 경우 Mac 및 Linux에서 대부분의 기능을 제공합니다. | [nuget.exe](https://dist.nuget.org/win-x86-commandline/latest/nuget.exe) |
| [Visual Studio](#visual-studio) | Windows에서 패키지 관리자 UI 및 패키지 관리자 콘솔을 통해 NuGet 기능을 제공합니다(.NET 관련 워크로드와 함께 포함). Mac에서는 UI를 통해 특정 기능을 제공합니다. Visual Studio Code에서 NuGet 기능은 확장을 통해 제공됩니다. | [Visual Studio](https://www.visualstudio.com/downloads/) |

[MSBuild CLI](reference/msbuild-targets.md)는 주로 빌드 서버에서 유용한 패키지를 복원하고 만들 수 있는 기능을 제공합니다. MSBuild는 NuGet을 사용하기 위한 범용 도구가 아닙니다.

## <a name="cli-tools"></a>CLI 도구

두 NuGet CLI 도구는 `dotnet.exe` 및 `nuget.exe`입니다. 이 둘을 비교하려면 [기능 가용성](#feature-availability)을 참조하세요.

* .NET Core 또는 .NET Standard를 대상으로 하려면 dotnet CLI를 사용합니다. `dotnet` CLI는 [SDK 특성](/dotnet/core/tools/csproj#additions)을 사용하는 SDK 스타일 프로젝트 형식에 필요합니다.
* .NET Framework(SDK 스타일이 아닌 프로젝트에만 해당)를 대상으로 하려면 `nuget.exe` CLI를 사용합니다. 프로젝트가 `packages.config`에서 PackageReference로 마이그레이션되면 dotnet CLI를 사용합니다.

### <a name="dotnetexe-cli"></a>dotnet.exe CLI

.NET Core 2.0 CLI `dotnet.exe`는 모든 플랫폼(Windows, Mac 및 Linux)에서 작동하며 패키지 설치, 복원 및 게시와 같은 핵심 NuGet 기능을 제공합니다. `dotnet`은 대부분의 시나리오에서 유용한 .NET Core 프로젝트 파일(예: `.csproj`)과의 직접 통합을 제공합니다. `dotnet`은 각 플랫폼에 대해 직접 빌드되며 Mono를 설치할 필요가 없습니다.

설치:

- 개발자 컴퓨터에서 [.NET Core SDK](https://aka.ms/dotnetcoregs)를 설치합니다. Visual Studio 2017부터 dotnet CLI는 모든 .NET Core 관련 워크로드와 함께 자동으로 설치됩니다.
- 빌드 서버의 경우 [지속적인 통합에 .NET Core SDK 및 도구 사용](/dotnet/core/tools/using-ci-with-cli)에 대한 지침을 따르세요.

dotnet CLI에서 기본 명령을 사용하는 방법에 대한 자세한 내용은 [dotnet CLI를 사용하여 패키지 설치 및 사용](consume-packages/install-use-packages-dotnet-cli.md)을 참조하세요.

### <a name="nugetexe-cli"></a>nuget.exe CLI

`nuget.exe` CLI인 `nuget.exe`는 모든 NuGet 기능을 제공하는 Windows용 명령줄 유틸리티입니다. 약간의 제한이 있지만 [Mono](https://www.mono-project.com/docs/getting-started/install/)를 사용하여 Mac OSX 및 Linux에서 실행할 수도 있습니다.

`nuget.exe` CLI에서 기본 명령을 사용하는 방법에 대한 자세한 내용은 [nuget.exe CLI를 사용하여 패키지 설치 및 사용](consume-packages/install-use-packages-nuget-cli.md)을 참조하세요.

설치:

[!INCLUDE [install-cli](includes/install-cli.md)]

> [!Tip]
> Windows에서 `nuget update -self`를 사용하여 기존 nuget.exe를 최신 버전으로 업데이트합니다.

> [!Note]
> 최신 권장 NuGet CLI는 항상 `https://dist.nuget.org/win-x86-commandline/latest/nuget.exe`에서 사용할 수 있습니다. 이전의 지속적인 통합(CI) 시스템과 호환되도록 이전 URL `https://nuget.org/nuget.exe`에서 현재 [사용되지 않는 2.8.6 CLI 도구](https://github.com/NuGet/NuGetGallery/issues/5381)를 제공합니다.

## <a name="visual-studio"></a>Visual Studio

- Visual Studio Code: NuGet 기능은 마켓플레이스 확장을 통해 사용 가능하거나 `dotnet.exe` 또는 `nuget.exe` CLI 도구를 사용합니다.

- Mac용 Visual Studio: 특정 NuGet 기능이 직접 기본 제공됩니다. 연습은 [프로젝트에 NuGet 패키지 포함](/visualstudio/mac/nuget-walkthrough)을 참조하세요. 기타 기능의 경우 `dotnet.exe` 또는 `nuget.exe` CLI 도구를 사용합니다.

- Windows의 Visual Studio: **NuGet 패키지 관리자**는 Visual Studio 2012 이상 버전에 포함됩니다. Visual Studio는 대부분의 NuGet 작업을 실행할 수 있는 [패키지 관리자 UI](consume-packages/install-use-packages-visual-studio.md) 및 [패키지 관리자 콘솔](consume-packages/install-use-packages-powershell.md)을 제공합니다.
  - Visual Studio 2017부터 설치 관리자에는 .NET을 사용하는 모든 워크로드가 있는 NuGet 패키지 관리자가 포함되어 있습니다. 별도로 설치하거나 패키지 관리자가 설치되어 있는지 확인하려면 Visual Studio 설치 관리자를 실행하고 **개별 구성 요소 > 코드 도구 > NuGet 패키지 관리자** 아래에서 옵션을 확인합니다.
  - 패키지 관리자 UI 및 콘솔은 Windows의 Visual Studio에만 있습니다. 현재 Mac용 Visual Studio에서는 사용할 수 없습니다.
  - CLI 도구는 IDE에서 NuGet 기능을 지원하는 데 필요합니다. `dotnet` CLI 또는 `nuget.exe` CLI를 사용할 수 있습니다. `dotnet` CLI는 .NET Core와 같은 Visual Studio 워크로드와 함께 설치됩니다. `nuget.exe` CLI는 앞에서 설명한 대로 별도로 설치해야 합니다.
  - 패키지 관리자 콘솔 명령은 Windows의 Visual Studio 내에서만 작동하며 다른 PowerShell 환경에서는 작동하지 않습니다.
  - Visual Studio 2010 이하의 경우 “Visual Studio용 NuGet 패키지 관리자” 확장을 설치합니다.
  - Visual Studio 2013 및 2015용 NuGet 확장은 [https://dist.nuget.org/index.html](https://dist.nuget.org/index.html)에서 다운로드할 수도 있습니다.
  - 예정된 NuGet 기능을 미리 보려면 Visual Studio Stable 릴리스와 함께 작동하는 [Visual Studio Preview](https://www.visualstudio.com/vs/preview/)를 설치합니다. Preview에 대한 문제를 보고하거나 아이디어를 공유하려면 [NuGet GitHub 리포지토리](https://github.com/Nuget/Home/issues)에서 이슈를 제기합니다.

## <a name="feature-availability"></a>기능 가용성

| 기능 | dotnet CLI | nuget CLI(Windows) | nuget CLI(Mono) | Visual Studio(Windows) | Mac용 Visual Studio |
| --- | --- | --- | --- | --- | --- |
| 패키지 검색 |  | &#10004; | &#10004; | &#10004; | &#10004; |
| 패키지 설치/제거 | &#10004; | &#10004;(1) | &#10004; | &#10004; | &#10004; |
| 패키지 업데이트 | &#10004; | &#10004; | | &#10004; | &#10004; |
| 패키지 복원 | &#10004; | &#10004; | &#10004;(2) | &#10004; | &#10004; |
| 패키지 피드(소스) 관리 | | &#10004; | &#10004; | &#10004; | &#10004; |
| 피드에서 패키지 관리 | &#10004; | &#10004; | &#10004; | | |
| 피드에 대한 API 키 설정 | | &#10004; | &#10004; | | |
| 패키지 만들기(3) | &#10004; | &#10004; | &#10004;(4) | &#10004; | |
| 패키지 게시 | &#10004; | &#10004; | &#10004; | &#10004; |  |
| 패키지 복제 |  | &#10004; | &#10004; | | |
| *global-package* 및 캐시 폴더 관리 | &#10004; | &#10004; | &#10004; | | |
| NuGet 구성 관리 | | &#10004; | &#10004; | | |

(1) 프로젝트 파일에 영향을 주지 않습니다. 대신 `dotnet.exe`를 사용합니다.

(2) 솔루션(`.sln`) 파일이 아닌 `packages.config` 파일에서만 작동합니다.

(3) Visual Studio UI 도구에 표시되지 않는 다양한 고급 패키지 기능은 CLI를 통해 사용할 수 있습니다.

(4) `.nuspec` 파일에서 작동하지만 프로젝트 파일에서 작동하지 않습니다.

### <a name="related-topics"></a>관련 항목

- [Visual Studio를 사용하여 패키지 설치 및 관리](consume-packages/install-use-packages-visual-studio.md)
- [PowerShell을 사용하여 패키지 설치 및 관리](consume-packages/install-use-packages-powershell.md)
- [dotnet CLI를 사용하여 패키지 설치 및 관리](consume-packages/install-use-packages-dotnet-cli.md)
- [nuget.exe CLI를 사용하여 패키지 설치 및 관리](consume-packages/install-use-packages-nuget-cli.md)
- [패키지 관리자 콘솔 PowerShell 참조](reference/powershell-reference.md)
- [패키지 만들기](create-packages/creating-a-package.md)
- [패키지 게시](nuget-org/publish-a-package.md)

Windows에서 작업하는 개발자는 NuGet 패키지를 시각적으로 탐색, 생성 및 편집할 수 있는 오픈 소스 독립 실행형 도구인 [NuGet 패키지 탐색기](https://github.com/NuGetPackageExplorer/NuGetPackageExplorer)를 탐색할 수도 있습니다. 예를 들어 패키지를 다시 빌드할 필요 없이 패키지 구조를 실험적으로 변경하는 것이 매우 유용합니다.
