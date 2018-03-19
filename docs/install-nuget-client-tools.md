---
title: "NuGet 클라이언트 도구 설치 | Microsoft Docs"
author: kraigb
ms.author: kraigb
manager: ghogen
ms.date: 01/24/2018
ms.topic: get-started-article
ms.prod: nuget
ms.technology: 
description: "클라이언트 도구, dotnet 및 nuget CLI(명령줄 인터페이스) 및 Visual Studio용 패키지 관리자 설치에 대한 지침입니다."
keywords: "dotnet.exe CLI, nuget.exe CLI, NuGet 클라이언트 도구, NuGet 패키지 관리자, NuGet 패키지 관리자 콘솔, Visual Studio용 NuGet, NuGet 베타 채널"
ms.reviewer:
- karann-msft
- unniravindranathan
ms.openlocfilehash: 462557e939e769f26fe05d6f9e2994eaf43c6e11
ms.sourcegitcommit: 8f26d10bdf256f72962010348083ff261dae81b9
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 03/08/2018
---
# <a name="installing-nuget-client-tools"></a>NuGet 클라이언트 도구 설치

> **패키지 설치를 원하십니까? [NuGet 패키지를 설치하는 방법](consume-packages/ways-to-install-a-package.md)을 참조하세요.**

NuGet으로 작업하려면 패키지 소비자 또는 작성자로서 [플랫폼 간 CLI(명령줄 인터페이스) 도구](#cli-tools)와 [Visual Studio의 NuGet 기능](#visual-studio)을 사용할 수 있습니다. 이 문서에서는 다양한 도구의 기능, 설치 방법 및 비교 [기능 가용성](#feature-availability)에 대해 간략하게 설명합니다.

| 도구&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; | 설명 | 다운로드&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; |
|:------------- |:-------------|:-----|
| [dotnet.exe](#dotnetexe-cli) | .NET Core SDK에 포함되며 모든 플랫폼에서 핵심 NuGet 기능을 제공합니다. | [.NET Core SDK](https://www.microsoft.com/net/download/) |
| [nuget.exe](#nugetexe-cli) | Windows의 모든 NuGet 기능 및 Mac과 Linux에서 [Mono](http://www.mono-project.com/docs/getting-started/install/)로 실행되는 대부분의 기능을 제공합니다. | [nuget.exe](https://dist.nuget.org/win-x86-commandline/latest/nuget.exe) |
| [Visual Studio](#visual-studio) | 패키지 관리자 UI 및 패키지 관리자 콘솔을 통해 NuGet 기능을 제공합니다(.NET 관련 워크로드와 함께 포함). | [Visual Studio 2017](https://www.visualstudio.com/downloads/) |

[MSBuild CLI](reference/msbuild-targets.md)는 주로 빌드 서버에서 유용한 패키지를 복원하고 만들 수 있는 기능을 제공합니다. 이외의 경우에는 MSBuild는 NuGet에서 작동하는 일반 용도의 도구가 아닙니다.

## <a name="cli-tools"></a>CLI 도구

두 NuGet CLI 도구는 `dotnet.exe` 및 `nuget.exe`입니다. 비교를 보려면 [기능 가용성](#feature-availability)을 참조하세요.

### <a name="dotnetexe-cli"></a>dotnet.exe CLI

.NET Core 2.0 CLI `dotnet.exe`는 모든 플랫폼(Windows, Mac 및 Linux)에서 작동하며 패키지 설치, 복원 및 게시와 같은 핵심 NuGet 기능을 제공합니다. ‘dotnet’은 대부분의 시나리오에서 유용한 .NET Core 프로젝트 파일(예: `.csproj`)과의 직접 통합을 제공합니다. `dotnet`은 각 플랫폼에 대해 직접 빌드되며 Mono를 설치할 필요가 없습니다.

설치:

- 개발자 컴퓨터에서 [.NET Core SDK](https://aka.ms/dotnetcoregs)를 설치합니다.
- 빌드 서버의 경우 [지속적인 통합에 .NET Core SDK 및 도구 사용](/dotnet/core/tools/using-ci-with-cli)에 대한 지침을 따르세요.

자세한 내용은 [.NET Core 명령줄 인터페이스 도구](/dotnet/core/tools/index?tabs=netcore2x#tabpanel_fXL5YCOYDa_netcore2x)를 참조하세요.

### <a name="nugetexe-cli"></a>nuget.exe CLI

NuGet CLI `nuget.exe`는 모든 NuGet 기능을 제공하는 Windows용 명령줄 유틸리티입니다. 약간의 제한이 있지만 Mono를 사용하여 Mac OSX 및 Linux에서 실행할 수도 있습니다. `dotnet`과 달리, `nuget.exe` CLI는 프로젝트 파일에 영향을 주지 않습니다.

설치:

[!INCLUDE[install-cli](includes/install-cli.md)]

> [!Tip]
> `nuget update -self`를 사용하여 기존 nuget.exe를 최신 버전으로 업데이트합니다.

> [!Note]
> 최신 권장 NuGet CLI는 항상 `https://dist.nuget.org/win-x86-commandline/latest/nuget.exe`에서 사용할 수 있습니다. 이전 지속적인 통합 시스템과 호환되도록 이전 URL `https://nuget.org/nuget.exe`는 현재 2.8.6 CLI 도구를 제공합니다. [이 항목은 사용되지 않습니다](https://github.com/NuGet/NuGetGallery/issues/5381).

## <a name="visual-studio"></a>Visual Studio

- Visual Studio Code: NuGet 기능은 마켓플레이스 확장을 통해 사용 가능하거나 `dotnet.exe` 또는 `nuget.exe` CLI 도구를 사용합니다.
- Mac용 Visual Studio: 특정 NuGet 기능이 직접 기본 제공됩니다. 연습은 [프로젝트에 NuGet 패키지 포함](/visualstudio/mac/nuget-walkthrough)을 참조하세요. 기타 기능의 경우 `dotnet.exe` 또는 `nuget.exe` CLI 도구를 사용합니다.

- Windows의 Visual Studio: **NuGet 패키지 관리자**는 Visual Studio 2012 이상 버전에 포함됩니다. 패키지 관리자는 대부분의 NuGet 작업을 실행할 수 있는 [패키지 관리자 UI](tools/package-manager-ui.md) 및 [패키지 관리자 콘솔](tools/package-manager-console.md)을 제공합니다.
  - Visual Studio 2017 설치 관리자에는 .NET을 사용하는 모든 워크로드가 있는 NuGet 패키지 관리자가 포함되어 있습니다. 별도로 설치하거나 패키지 관리자가 설치되어 있는지 확인하려면 Visual Studio 2017 설치 관리자를 실행하고 **개별 구성 요소 > 코드 도구 > NuGet 패키지 관리자** 아래에서 옵션을 확인합니다.
  - 패키지 관리자 UI 및 콘솔은 Windows의 Visual Studio에 고유합니다. 현재 Mac용 Visual Studio에서는 사용할 수 없습니다.
  - Visual Studio에는 `nuget.exe` CLI가 자동으로 포함되지 않습니다. 이 CLI는 이전에 설명한 대로 별도로 설치해야 합니다.
  - 패키지 관리자 콘솔 명령은 Windows의 Visual Studio 내에서만 작동하며 다른 PowerShell 환경에서는 작동하지 않습니다.
  - Visual Studio 2010 이하의 경우 “Visual Studio용 NuGet 패키지 관리자” 확장을 설치합니다.
  - Visual Studio 2013 및 2015용 NuGet 확장은 [https://dist.nuget.org/index.html](https://dist.nuget.org/index.html)에서 다운로드할 수도 있습니다.
  - 예정된 NuGet 기능을 미리 보려면 안정적인 Visual Studio 릴리스와 함께 작동하는 [Visual Studio 2017 미리 보기](https://www.visualstudio.com/vs/preview/)를 설치합니다. 미리 보기에 대한 문제를 보고하거나 아이디어를 공유하려면 [NuGet GitHub 리포지토리](https://github.com/Nuget/Home/issues)에서 문제를 엽니다.

## <a name="feature-availability"></a>기능 가용성

| 기능 | dotnet CLI | nuget CLI(Windows) | nuget CLI(Mono) | Visual Studio(Windows) | Visual Studio for Mac |
| --- | --- | --- | --- | --- | --- |
| 패키지 검색 |  | &#10004; | &#10004; | &#10004; | &#10004; |
| 패키지 설치/제거 | &#10004;(1) | &#10004;(2) | &#10004; | &#10004; | &#10004; |
| 패키지 업데이트 | &#10004; | &#10004; | | &#10004; | &#10004; |
| 패키지 복원 | &#10004; | &#10004; | &#10004;(3) | &#10004; | &#10004; |
| 패키지 피드(소스) 관리 | | &#10004; | &#10004; | &#10004; | &#10004; |
| 피드에서 패키지 관리 | &#10004;(1) | &#10004; | &#10004; | | |
| 피드에 대한 API 키 설정 | | &#10004; | &#10004; | | |
| 패키지 만들기(4) | &#10004; | &#10004; | &#10004;(5) | &#10004; | |
| 패키지 게시 | &#10004;(1) | &#10004; | &#10004; | &#10004; |  |
| 패키지 복제 |  | &#10004; | &#10004; | | |
| NuGet 캐시 관리 | &#10004; | &#10004; | &#10004; | | |
| NuGet 구성 관리 | | &#10004; | &#10004; | | |

(1) nuget.org의 패키지만

(2) 프로젝트 파일에 영향을 주지 않습니다. 대신 `dotnet.exe`를 사용합니다.

(3) 솔루션(`.sln`) 파일이 아닌 `packages.config` 파일에서만 작동합니다.

(4) Visual Studio UI 도구에 표시되지 않는 다양한 고급 패키지 기능은 CLI를 통해 사용할 수 있습니다.

(5) `.nuspec` 파일에서 작동하지만 프로젝트 파일에서 작동하지 않습니다.

### <a name="related-topics"></a>관련 항목

- [dotnet 명령](tools/dotnet-commands.md)
- [NuGet CLI 참조](tools/nuget-exe-cli-reference.md)
- [패키지 관리자 UI 참조](tools/package-manager-ui.md)
- [패키지 관리자 콘솔 참조](tools/package-manager-console.md)
- [패키지 관리자 콘솔 PowerShell 참조](tools/powershell-reference.md)
- [패키지 만들기](create-packages/creating-a-package.md)
- [패키지 게시](create-packages/publish-a-package.md)

Windows에서 작업하는 개발자는 NuGet 패키지를 시각적으로 탐색, 생성 및 편집할 수 있는 오픈 소스 독립 실행형 도구인 [NuGet 패키지 탐색기](https://github.com/NuGetPackageExplorer/NuGetPackageExplorer)를 탐색할 수도 있습니다. 예를 들어 패키지를 다시 빌드할 필요 없이 패키지 구조를 실험적으로 변경하는 것이 매우 유용합니다.
