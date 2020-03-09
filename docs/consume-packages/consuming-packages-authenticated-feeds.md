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
# <a name="consuming-packages-from-authenticated-feeds"></a><span data-ttu-id="39fff-103">인증된 피드의 패키지 사용</span><span class="sxs-lookup"><span data-stu-id="39fff-103">Consuming packages from authenticated feeds</span></span>

<span data-ttu-id="39fff-104">nuget.org [퍼블릭 피드](https://api.nuget.org/v3/index.json) 외에도 NuGet 클라이언트는 파일 피드 및 프라이빗 http 피드와 상호 작용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="39fff-104">In addition to the nuget.org [public feed](https://api.nuget.org/v3/index.json), NuGet clients have the ability to interact with file feeds and private http feeds.</span></span>


<span data-ttu-id="39fff-105">프라이빗 http 피드로 인증하려면 다음 두 가지 방법이 있습니다.</span><span class="sxs-lookup"><span data-stu-id="39fff-105">To authenticate with private http feeds, the 2 approaches are:</span></span>

* <span data-ttu-id="39fff-106">[NuGet.config](../reference/nuget-config-file.md#packagesourcecredentials)에 자격 증명을 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="39fff-106">Add credentials in the [NuGet.config](../reference/nuget-config-file.md#packagesourcecredentials)</span></span>
* <span data-ttu-id="39fff-107">사용한 클라이언트에 따라 여러 확장성 모델 중 하나로 인증합니다.</span><span class="sxs-lookup"><span data-stu-id="39fff-107">Authenticate using one of the many extensibility models depending on the client used.</span></span>

## <a name="nuget-clients-authentication-extensibility"></a><span data-ttu-id="39fff-108">NuGet 클라이언트의 인증 확장성</span><span class="sxs-lookup"><span data-stu-id="39fff-108">NuGet clients' authentication extensibility</span></span>

<span data-ttu-id="39fff-109">다양한 NuGet 클라이언트에서 인증 책임은 프라이빗 피드 공급자 자체에 있습니다.</span><span class="sxs-lookup"><span data-stu-id="39fff-109">For the various NuGet clients, the private feed provider itself is responsible for authentication.</span></span>
<span data-ttu-id="39fff-110">모든 NuGet 클라이언트에는 이 기능을 지원하는 확장성 방법이 있습니다.</span><span class="sxs-lookup"><span data-stu-id="39fff-110">All NuGet clients have extensibility methods to support this.</span></span> <span data-ttu-id="39fff-111">자격 증명을 검색하기 위해 NuGet과 통신할 수 있는 플러그 인이거나 Visual Studio 확장입니다.</span><span class="sxs-lookup"><span data-stu-id="39fff-111">These are either a Visual Studio extension or a plugin that can communicate with NuGet to retrieve credentials.</span></span>

### <a name="visual-studio"></a><span data-ttu-id="39fff-112">Visual Studio</span><span class="sxs-lookup"><span data-stu-id="39fff-112">Visual Studio</span></span>

<span data-ttu-id="39fff-113">Visual Studio에서 NuGet은 피드 공급자가 구현하고 고객에게 제공할 수 있는 인터페이스를 노출합니다.</span><span class="sxs-lookup"><span data-stu-id="39fff-113">In Visual Studio, NuGet exposes an interface that feed providers can implement and provide to their customers.</span></span> <span data-ttu-id="39fff-114">자세한 내용은 [Visual Studio 자격 증명 공급자를 만드는 방법](../reference/extensibility/NuGet-Credential-Providers-for-Visual-Studio.md) 문서를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="39fff-114">For more details, please refer to the documentation on [how to create a Visual Studio credential provider](../reference/extensibility/NuGet-Credential-Providers-for-Visual-Studio.md).</span></span>

#### <a name="available-nuget-credential-providers-for-visual-studio"></a><span data-ttu-id="39fff-115">사용 가능한 Visual Studio용 NuGet 자격 증명 공급자</span><span class="sxs-lookup"><span data-stu-id="39fff-115">Available NuGet credential providers for Visual Studio</span></span>

<span data-ttu-id="39fff-116">Visual Studio에는 Azure DevOps를 지원하기 위해 기본 제공되는 자격 증명 공급자가 있습니다.</span><span class="sxs-lookup"><span data-stu-id="39fff-116">There is a credential provider built into Visual Studio to support Azure DevOps.</span></span>


<span data-ttu-id="39fff-117">사용 가능한 플러그 인 자격 증명 공급자는 다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="39fff-117">Available plug-in credential providers include:</span></span>

* [<span data-ttu-id="39fff-118">MyGet Credential Provider for Visual Studio</span><span class="sxs-lookup"><span data-stu-id="39fff-118">MyGet Credential Provider for Visual Studio</span></span>](http://docs.myget.org/docs/reference/credential-provider-for-visual-studio)

### <a name="nugetexe"></a><span data-ttu-id="39fff-119">nuget.exe</span><span class="sxs-lookup"><span data-stu-id="39fff-119">nuget.exe</span></span>

<span data-ttu-id="39fff-120">`nuget.exe`는 피드로 인증하는 데 자격 증명이 필요한 경우 다음과 같은 방식으로 자격 증명을 찾습니다.</span><span class="sxs-lookup"><span data-stu-id="39fff-120">When `nuget.exe` needs credentials to authenticate with a feed, it looks for them in the following manner:</span></span>

1. <span data-ttu-id="39fff-121">`NuGet.config` 파일에서 자격 증명을 찾습니다.</span><span class="sxs-lookup"><span data-stu-id="39fff-121">Look for credentials in `NuGet.config` files.</span></span>
1. <span data-ttu-id="39fff-122">V2 플러그 인 자격 증명 공급자 사용</span><span class="sxs-lookup"><span data-stu-id="39fff-122">Use V2 plug-in credential providers</span></span>
1. <span data-ttu-id="39fff-123">V1 플러그 인 자격 증명 공급자 사용</span><span class="sxs-lookup"><span data-stu-id="39fff-123">Use V1 plug-in credential providers</span></span>
1. <span data-ttu-id="39fff-124">그런 다음 NuGet은 명령줄에서 자격 증명을 묻는 메시지를 사용자에게 표시합니다.</span><span class="sxs-lookup"><span data-stu-id="39fff-124">NuGet then prompts the user for credentials on the command line.</span></span>

#### <a name="nugetexe-and-v2-credential-providers"></a><span data-ttu-id="39fff-125">nuget.exe 및 V2 자격 증명 공급자</span><span class="sxs-lookup"><span data-stu-id="39fff-125">nuget.exe and V2 credential providers</span></span>

<span data-ttu-id="39fff-126">버전 `4.8`에서 NuGet은 새 인증 플러그 인 메커니즘(V2 자격 증명 공급자)을 정의했습니다.</span><span class="sxs-lookup"><span data-stu-id="39fff-126">In version `4.8` NuGet defined a new authentication plugin mechanism, hereafter referred to as V2 credential providers.</span></span>
<span data-ttu-id="39fff-127">이러한 공급자의 설치 및 검색에 대한 자세한 내용은 [NuGet 플랫폼 간 플러그 인](../reference/extensibility/NuGet-Cross-Platform-Plugins.md#plugin-installation-and-discovery)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="39fff-127">For the installation and discovery of those providers, refer to [NuGet cross platform plugins](../reference/extensibility/NuGet-Cross-Platform-Plugins.md#plugin-installation-and-discovery).</span></span>

#### <a name="nugetexe-and-v1-credential-providers"></a><span data-ttu-id="39fff-128">nuget.exe 및 V1 자격 증명 공급자</span><span class="sxs-lookup"><span data-stu-id="39fff-128">nuget.exe and V1 credential providers</span></span>

<span data-ttu-id="39fff-129">버전 `3.3`에서 NuGet은 첫 번째 인증 플러그 인 버전을 도입했습니다.</span><span class="sxs-lookup"><span data-stu-id="39fff-129">In version `3.3` NuGet introduced the first version of authentication plugins.</span></span>
<span data-ttu-id="39fff-130">이러한 공급자의 설치 및 검색에 대한 자세한 내용은 [nuget.exe 자격 증명 공급자](../reference/extensibility/nuget-exe-Credential-Providers.md#nugetexe-credential-provider-discovery)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="39fff-130">For the installation and discovery of those providers refer to [nuget.exe credential providers](../reference/extensibility/nuget-exe-Credential-Providers.md#nugetexe-credential-provider-discovery)</span></span>

#### <a name="available-credential-providers-for-nugetexe"></a><span data-ttu-id="39fff-131">nuget.exe에 사용 가능한 자격 증명 공급자</span><span class="sxs-lookup"><span data-stu-id="39fff-131">Available credential providers for nuget.exe</span></span>

* <span data-ttu-id="39fff-132">[Azure DevOps V2 자격 증명 공급자](/azure/devops/artifacts/nuget/nuget-exe?view=azure-devops#add-a-feed-to-nuget-482-or-later) 또는 [Azure Artifacts 자격 증명 공급자](https://github.com/microsoft/artifacts-credprovider)</span><span class="sxs-lookup"><span data-stu-id="39fff-132">[Azure DevOps V2 Credential Providers](/azure/devops/artifacts/nuget/nuget-exe?view=azure-devops#add-a-feed-to-nuget-482-or-later) or [Azure Artifacts Credential Provider](https://github.com/microsoft/artifacts-credprovider)</span></span>

<span data-ttu-id="39fff-133">Visual Studio 2017 버전 15.9 이상에서는 Azure DevOps 자격 증명 공급자가 Visual Studio와 함께 제공됩니다.</span><span class="sxs-lookup"><span data-stu-id="39fff-133">With Visual Studio 2017 version 15.9 and later, the Azure DevOps credential provider is bundled in Visual Studio.</span></span>
<span data-ttu-id="39fff-134">`nuget.exe`가 해당 Visual Studio 도구 세트의 MSBuild를 사용하는 경우 플러그 인이 자동으로 검색됩니다.</span><span class="sxs-lookup"><span data-stu-id="39fff-134">If `nuget.exe` uses MSBuild from that specific Visual Studio toolset, then the plugin will be discovered automatically.</span></span>

### <a name="dotnetexe"></a><span data-ttu-id="39fff-135">dotnet.exe</span><span class="sxs-lookup"><span data-stu-id="39fff-135">dotnet.exe</span></span>

<span data-ttu-id="39fff-136">`dotnet.exe`는 피드로 인증하는 데 자격 증명이 필요한 경우 다음과 같은 방식으로 자격 증명을 찾습니다.</span><span class="sxs-lookup"><span data-stu-id="39fff-136">When `dotnet.exe` needs credentials to authenticate with a feed, it looks for them in the following manner:</span></span>

1. <span data-ttu-id="39fff-137">`NuGet.config` 파일에서 자격 증명을 찾습니다.</span><span class="sxs-lookup"><span data-stu-id="39fff-137">Look for credentials in `NuGet.config` files.</span></span>
1. <span data-ttu-id="39fff-138">V2 플러그 인 자격 증명 공급자 사용</span><span class="sxs-lookup"><span data-stu-id="39fff-138">Use V2 plug-in credential providers</span></span>

<span data-ttu-id="39fff-139">기본적으로 `dotnet.exe`는 대화형이 아니므로 인증 시 차단을 위한 도구를 가져오기 위해 `--interactive` 플래그를 전달해야 할 수도 있습니다.</span><span class="sxs-lookup"><span data-stu-id="39fff-139">By default `dotnet.exe` is not interactive, so you might need to pass an `--interactive` flag to get the tool to block for authentication.</span></span>

#### <a name="dotnetexe-and-v2-credential-providers"></a><span data-ttu-id="39fff-140">dotnet.exe 및 V2 자격 증명 공급자</span><span class="sxs-lookup"><span data-stu-id="39fff-140">dotnet.exe and V2 credential providers</span></span>

<span data-ttu-id="39fff-141">SDK 버전 `2.2.100`에서 NuGet은 모든 클라이언트에서 작동하는 인증 플러그 인 메커니즘을 정의했습니다.</span><span class="sxs-lookup"><span data-stu-id="39fff-141">In version `2.2.100` of the SDK, NuGet defined an authentication plugin mechanism that works in all clients.</span></span>
<span data-ttu-id="39fff-142">이러한 공급자의 설치 및 검색에 대한 자세한 내용은 [NuGet 플랫폼 간 플러그 인](../reference/extensibility/NuGet-Cross-Platform-Plugins.md#plugin-installation-and-discovery)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="39fff-142">For the installation and discovery of those providers, refer to [NuGet cross platform plugins](../reference/extensibility/NuGet-Cross-Platform-Plugins.md#plugin-installation-and-discovery).</span></span>

#### <a name="available-credential-providers-for-dotnetexe"></a><span data-ttu-id="39fff-143">dotnet.exe에 사용 가능한 자격 증명 공급자</span><span class="sxs-lookup"><span data-stu-id="39fff-143">Available credential providers for dotnet.exe</span></span>

* [<span data-ttu-id="39fff-144">Azure Artifacts 자격 증명 공급자</span><span class="sxs-lookup"><span data-stu-id="39fff-144">Azure Artifacts Credential Provider</span></span>](https://github.com/microsoft/artifacts-credprovider)

### <a name="msbuildexe"></a><span data-ttu-id="39fff-145">MSBuild.exe</span><span class="sxs-lookup"><span data-stu-id="39fff-145">MSBuild.exe</span></span>

<span data-ttu-id="39fff-146">`MSBuild.exe`는 피드로 인증하는 데 자격 증명이 필요한 경우 다음과 같은 방식으로 자격 증명을 찾습니다.</span><span class="sxs-lookup"><span data-stu-id="39fff-146">When `MSBuild.exe` needs credentials to authenticate with a feed, it looks for them in the following manner:</span></span>

1. <span data-ttu-id="39fff-147">`NuGet.config` 파일에서 자격 증명을 찾습니다.</span><span class="sxs-lookup"><span data-stu-id="39fff-147">Look for credentials in `NuGet.config` files</span></span>
1. <span data-ttu-id="39fff-148">V2 플러그 인 자격 증명 공급자 사용</span><span class="sxs-lookup"><span data-stu-id="39fff-148">Use V2 plug-in credential providers</span></span>

<span data-ttu-id="39fff-149">기본적으로 `MSBuild.exe`는 대화형이 아니므로 인증 시 차단을 위한 도구를 가져오기 위해 `/p:NuGetInteractive=true` 속성을 설정해야 할 수도 있습니다.</span><span class="sxs-lookup"><span data-stu-id="39fff-149">By default `MSBuild.exe` is not interactive, so you might need to set the `/p:NuGetInteractive=true` property to get the tool to block for authentication.</span></span>

#### <a name="msbuildexe-and-v2-credential-providers"></a><span data-ttu-id="39fff-150">MSBuild.exe 및 V2 자격 증명 공급자</span><span class="sxs-lookup"><span data-stu-id="39fff-150">MSBuild.exe and V2 credential providers</span></span>

<span data-ttu-id="39fff-151">Visual Studio 2019 업데이트 9에서 NuGet은 모든 클라이언트에서 작동하는 인증 플러그 인 메커니즘을 정의했습니다.</span><span class="sxs-lookup"><span data-stu-id="39fff-151">In Visual Studio 2019 Update 9, NuGet defined an authentication plugin mechanism that works in all clients.</span></span>
<span data-ttu-id="39fff-152">이러한 공급자의 설치 및 검색에 대한 자세한 내용은 [NuGet 플랫폼 간 플러그 인](../reference/extensibility/NuGet-Cross-Platform-Plugins.md#plugin-installation-and-discovery)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="39fff-152">For the installation and discovery of those providers, refer to [NuGet cross platform plugins](../reference/extensibility/NuGet-Cross-Platform-Plugins.md#plugin-installation-and-discovery).</span></span>

#### <a name="available-credential-providers-for-msbuildexe"></a><span data-ttu-id="39fff-153">MSBuild.exe에 사용 가능한 자격 증명 공급자</span><span class="sxs-lookup"><span data-stu-id="39fff-153">Available credential providers for MSBuild.exe</span></span>

* [<span data-ttu-id="39fff-154">Azure Artifacts 자격 증명 공급자</span><span class="sxs-lookup"><span data-stu-id="39fff-154">Azure Artifacts Credential Provider</span></span>](https://github.com/microsoft/artifacts-credprovider)

<span data-ttu-id="39fff-155">Visual Studio 2017 업데이트 9 이상에서는 Azure DevOps 자격 증명 공급자가 Visual Studio와 함께 제공됩니다.</span><span class="sxs-lookup"><span data-stu-id="39fff-155">With Visual Studio 2017 Update 9 and later, the Azure DevOps credential provider is bundled in Visual Studio.</span></span> <span data-ttu-id="39fff-156">추가 단계는 필요하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="39fff-156">No additional steps are required.</span></span>
