---
title: 인증된 피드의 패키지 사용
description: 모든 NuGet 클라이언트 시나리오에서 인증된 피드의 패키지 사용
author: nkolev92
ms.author: nikolev
ms.date: 02/28/2020
ms.topic: conceptual
ms.openlocfilehash: bb624ec6987dd5c6ee38d5bb7e01200487dd4bed
ms.sourcegitcommit: c81561e93a7be467c1983d639158d4e3dc25b93a
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 03/02/2020
ms.locfileid: "78231742"
---
# <a name="consuming-packages-from-authenticated-feeds"></a>인증된 피드의 패키지 사용

nuget.org [퍼블릭 피드](https://api.nuget.org/v3/index.json) 외에도 NuGet 클라이언트는 파일 피드 및 프라이빗 http 피드와 상호 작용할 수 있습니다.


프라이빗 http 피드로 인증하려면 다음 두 가지 방법이 있습니다.

* [NuGet.config](../reference/nuget-config-file.md#packagesourcecredentials)에 자격 증명을 추가합니다.
* 사용한 클라이언트에 따라 여러 확장성 모델 중 하나로 인증합니다.

## <a name="nuget-clients-authentication-extensibility"></a>NuGet 클라이언트의 인증 확장성

다양한 NuGet 클라이언트에서 인증 책임은 프라이빗 피드 공급자 자체에 있습니다.
모든 NuGet 클라이언트에는 이 기능을 지원하는 확장성 방법이 있습니다. 자격 증명을 검색하기 위해 NuGet과 통신할 수 있는 플러그 인이거나 Visual Studio 확장입니다.

### <a name="visual-studio"></a>Visual Studio

Visual Studio에서 NuGet은 피드 공급자가 구현하고 고객에게 제공할 수 있는 인터페이스를 노출합니다. 자세한 내용은 [Visual Studio 자격 증명 공급자를 만드는 방법](../reference/extensibility/NuGet-Credential-Providers-for-Visual-Studio.md) 문서를 참조하세요.

#### <a name="available-nuget-credential-providers-for-visual-studio"></a>사용 가능한 Visual Studio용 NuGet 자격 증명 공급자

Visual Studio에는 Azure DevOps를 지원하기 위해 기본 제공되는 자격 증명 공급자가 있습니다.


사용 가능한 플러그 인 자격 증명 공급자는 다음과 같습니다.

* [MyGet Credential Provider for Visual Studio](http://docs.myget.org/docs/reference/credential-provider-for-visual-studio)

### <a name="nugetexe"></a>nuget.exe

`nuget.exe`는 피드로 인증하는 데 자격 증명이 필요한 경우 다음과 같은 방식으로 자격 증명을 찾습니다.

1. `NuGet.config` 파일에서 자격 증명을 찾습니다.
1. V2 플러그 인 자격 증명 공급자 사용
1. V1 플러그 인 자격 증명 공급자 사용
1. 그런 다음 NuGet은 명령줄에서 자격 증명을 묻는 메시지를 사용자에게 표시합니다.

#### <a name="nugetexe-and-v2-credential-providers"></a>nuget.exe 및 V2 자격 증명 공급자

버전 `4.8`에서 NuGet은 새 인증 플러그 인 메커니즘(V2 자격 증명 공급자)을 정의했습니다.
이러한 공급자의 설치 및 검색에 대한 자세한 내용은 [NuGet 플랫폼 간 플러그 인](../reference/extensibility/NuGet-Cross-Platform-Plugins.md#plugin-installation-and-discovery)을 참조하세요.

#### <a name="nugetexe-and-v1-credential-providers"></a>nuget.exe 및 V1 자격 증명 공급자

버전 `3.3`에서 NuGet은 첫 번째 인증 플러그 인 버전을 도입했습니다.
이러한 공급자의 설치 및 검색에 대한 자세한 내용은 [nuget.exe 자격 증명 공급자](../reference/extensibility/nuget-exe-Credential-Providers.md#nugetexe-credential-provider-discovery)를 참조하세요.

#### <a name="available-credential-providers-for-nugetexe"></a>nuget.exe에 사용 가능한 자격 증명 공급자

* [Azure DevOps V2 자격 증명 공급자](/azure/devops/artifacts/nuget/nuget-exe?view=azure-devops#add-a-feed-to-nuget-482-or-later) 또는 [Azure Artifacts 자격 증명 공급자](https://github.com/microsoft/artifacts-credprovider)

Visual Studio 2017 버전 15.9 이상에서는 Azure DevOps 자격 증명 공급자가 Visual Studio와 함께 제공됩니다.
`nuget.exe`가 해당 Visual Studio 도구 세트의 MSBuild를 사용하는 경우 플러그 인이 자동으로 검색됩니다.

### <a name="dotnetexe"></a>dotnet.exe

`dotnet.exe`는 피드로 인증하는 데 자격 증명이 필요한 경우 다음과 같은 방식으로 자격 증명을 찾습니다.

1. `NuGet.config` 파일에서 자격 증명을 찾습니다.
1. V2 플러그 인 자격 증명 공급자 사용

기본적으로 `dotnet.exe`는 대화형이 아니므로 인증 시 차단을 위한 도구를 가져오기 위해 `--interactive` 플래그를 전달해야 할 수도 있습니다.

#### <a name="dotnetexe-and-v2-credential-providers"></a>dotnet.exe 및 V2 자격 증명 공급자

SDK 버전 `2.2.100`에서 NuGet은 모든 클라이언트에서 작동하는 인증 플러그 인 메커니즘을 정의했습니다.
이러한 공급자의 설치 및 검색에 대한 자세한 내용은 [NuGet 플랫폼 간 플러그 인](../reference/extensibility/NuGet-Cross-Platform-Plugins.md#plugin-installation-and-discovery)을 참조하세요.

#### <a name="available-credential-providers-for-dotnetexe"></a>dotnet.exe에 사용 가능한 자격 증명 공급자

* [Azure Artifacts 자격 증명 공급자](https://github.com/microsoft/artifacts-credprovider)

### <a name="msbuildexe"></a>MSBuild.exe

`MSBuild.exe`는 피드로 인증하는 데 자격 증명이 필요한 경우 다음과 같은 방식으로 자격 증명을 찾습니다.

1. `NuGet.config` 파일에서 자격 증명을 찾습니다.
1. V2 플러그 인 자격 증명 공급자 사용

기본적으로 `MSBuild.exe`는 대화형이 아니므로 인증 시 차단을 위한 도구를 가져오기 위해 `/p:NuGetInteractive=true` 속성을 설정해야 할 수도 있습니다.

#### <a name="msbuildexe-and-v2-credential-providers"></a>MSBuild.exe 및 V2 자격 증명 공급자

Visual Studio 2019 업데이트 9에서 NuGet은 모든 클라이언트에서 작동하는 인증 플러그 인 메커니즘을 정의했습니다.
이러한 공급자의 설치 및 검색에 대한 자세한 내용은 [NuGet 플랫폼 간 플러그 인](../reference/extensibility/NuGet-Cross-Platform-Plugins.md#plugin-installation-and-discovery)을 참조하세요.

#### <a name="available-credential-providers-for-msbuildexe"></a>MSBuild.exe에 사용 가능한 자격 증명 공급자

* [Azure Artifacts 자격 증명 공급자](https://github.com/microsoft/artifacts-credprovider)

Visual Studio 2017 업데이트 9 이상에서는 Azure DevOps 자격 증명 공급자가 Visual Studio와 함께 제공됩니다. 추가 단계는 필요하지 않습니다.
