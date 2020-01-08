---
title: Visual Studio용 NuGet 자격 증명 공급 기업
description: NuGet 자격 증명 공급자는 Visual Studio 확장에서 IVsCredentialProvider 인터페이스를 구현 하 여 피드에 인증 합니다.
author: karann-msft
ms.author: karann
ms.date: 01/09/2017
ms.topic: conceptual
ms.openlocfilehash: 906d07eb22599eb423b00300954ff2601dd33369
ms.sourcegitcommit: 26a8eae00af2d4be581171e7a73009f94534c336
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 12/25/2019
ms.locfileid: "75383553"
---
# <a name="authenticating-feeds-in-visual-studio-with-nuget-credential-providers"></a><span data-ttu-id="10e6c-103">NuGet 자격 증명 공급자를 사용 하 여 Visual Studio에서 피드 인증</span><span class="sxs-lookup"><span data-stu-id="10e6c-103">Authenticating feeds in Visual Studio with NuGet credential providers</span></span>

<span data-ttu-id="10e6c-104">NuGet Visual Studio 확장 3.6 +는 NuGet이 인증 된 피드에 사용할 수 있도록 하는 자격 증명 공급자를 지원 합니다.</span><span class="sxs-lookup"><span data-stu-id="10e6c-104">The NuGet Visual Studio Extension 3.6+ supports credential providers, which enable NuGet to work with authenticated feeds.</span></span>
<span data-ttu-id="10e6c-105">Visual Studio 용 NuGet 자격 증명 공급자를 설치 하면 NuGet Visual Studio 확장에서 필요한 경우 인증 된 피드에 대 한 자격 증명을 자동으로 획득 하 고 새로 고칩니다.</span><span class="sxs-lookup"><span data-stu-id="10e6c-105">After you install a NuGet credential provider for Visual Studio, the NuGet Visual Studio extension will automatically acquire and refresh credentials for authenticated feeds as necessary.</span></span>

<span data-ttu-id="10e6c-106">샘플 구현은 [VsCredentialProvider 샘플](https://github.com/NuGet/Samples/tree/master/VsCredentialProvider)에서 찾을 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="10e6c-106">A sample implementation can be found in [the VsCredentialProvider sample](https://github.com/NuGet/Samples/tree/master/VsCredentialProvider).</span></span>

<span data-ttu-id="10e6c-107">Visual Studio에서 4.8 + NuGet 부터는 새로운 플랫폼 간 인증 플러그 인도 지원 하지만 성능상의 이유로 권장 되는 방법은 아닙니다.</span><span class="sxs-lookup"><span data-stu-id="10e6c-107">Starting with 4.8+ NuGet in Visual Studio supports the new cross platform authentication plugins as well, but they are not the recommended approach for performance reasons.</span></span>

> [!Note]
> <span data-ttu-id="10e6c-108">Visual Studio 용 NuGet 자격 증명 공급자는 일반 Visual Studio 확장으로 설치 해야 하며 [Visual studio 2017](https://aka.ms/vs/15/release/vs_enterprise.exe) 이상이 필요 합니다.</span><span class="sxs-lookup"><span data-stu-id="10e6c-108">NuGet credential providers for Visual Studio must be installed as a regular Visual Studio extension and will require [Visual Studio 2017](https://aka.ms/vs/15/release/vs_enterprise.exe) or above.</span></span>
>
> <span data-ttu-id="10e6c-109">Visual Studio 용 NuGet 자격 증명 공급자는 Visual Studio 에서만 작동 합니다 (dotnet restore 또는 nuget.exe는 아님).</span><span class="sxs-lookup"><span data-stu-id="10e6c-109">NuGet credential providers for Visual Studio work only in Visual Studio (not in dotnet restore or nuget.exe).</span></span> <span data-ttu-id="10e6c-110">Nuget.exe를 사용 하는 자격 증명 공급자는 [Nuget.exe 자격 증명 공급자](nuget-exe-Credential-providers.md)를 참조 하세요.</span><span class="sxs-lookup"><span data-stu-id="10e6c-110">For credential providers with nuget.exe, see [nuget.exe Credential Providers](nuget-exe-Credential-providers.md).</span></span>
> <span data-ttu-id="10e6c-111">Dotnet 및 msbuild의 자격 증명 공급자의 경우 [NuGet 플랫폼 간 플러그 인](nuget-cross-platform-authentication-plugin.md) 을 참조 하세요.</span><span class="sxs-lookup"><span data-stu-id="10e6c-111">For credential providers in dotnet and msbuild see [NuGet cross platform plugins](nuget-cross-platform-authentication-plugin.md)</span></span>

## <a name="available-nuget-credential-providers-for-visual-studio"></a><span data-ttu-id="10e6c-112">Visual Studio 용 사용 가능한 NuGet 자격 증명 공급자</span><span class="sxs-lookup"><span data-stu-id="10e6c-112">Available NuGet credential providers for Visual Studio</span></span>

<span data-ttu-id="10e6c-113">Visual Studio Team Services를 지원 하기 위해 Visual Studio NuGet 확장에 기본 제공 되는 자격 증명 공급자가 있습니다.</span><span class="sxs-lookup"><span data-stu-id="10e6c-113">There is a credential provider built into the Visual Studio NuGet extension to support Visual Studio Team Services.</span></span>

<span data-ttu-id="10e6c-114">NuGet Visual Studio 확장은 플러그 인 자격 증명 공급자도 검색 하는 내부 `VsCredentialProviderImporter`를 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="10e6c-114">The NuGet Visual Studio Extension uses an internal `VsCredentialProviderImporter` which also scans for plug-in credential providers.</span></span> <span data-ttu-id="10e6c-115">이러한 플러그 인 자격 증명 공급자는 `IVsCredentialProvider`형식의 MEF 내보내기로 검색할 수 있어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="10e6c-115">These plug-in credential providers must be discoverable as a MEF Export of type `IVsCredentialProvider`.</span></span>

<span data-ttu-id="10e6c-116">사용 가능한 플러그 인 자격 증명 공급자는 다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="10e6c-116">Available plug-in credential providers include:</span></span>

- [<span data-ttu-id="10e6c-117">Visual Studio 용 MyGet 자격 증명 공급자</span><span class="sxs-lookup"><span data-stu-id="10e6c-117">MyGet Credential Provider for Visual Studio</span></span>](http://docs.myget.org/docs/reference/credential-provider-for-visual-studio)

## <a name="creating-a-nuget-credential-provider-for-visual-studio"></a><span data-ttu-id="10e6c-118">Visual Studio 용 NuGet 자격 증명 공급자 만들기</span><span class="sxs-lookup"><span data-stu-id="10e6c-118">Creating a NuGet credential provider for Visual Studio</span></span>

<span data-ttu-id="10e6c-119">NuGet Visual Studio 확장 3.6 +는 자격 증명을 획득 하는 데 사용 되는 내부 CredentialService를 구현 합니다.</span><span class="sxs-lookup"><span data-stu-id="10e6c-119">The NuGet Visual Studio Extension 3.6+ implements an internal CredentialService that is used to acquire credentials.</span></span> <span data-ttu-id="10e6c-120">CredentialService에는 기본 제공 및 플러그 인 자격 증명 공급자 목록이 있습니다.</span><span class="sxs-lookup"><span data-stu-id="10e6c-120">The CredentialService has a list of built-in and plug-in credential providers.</span></span> <span data-ttu-id="10e6c-121">각 공급자는 자격 증명을 가져올 때까지 순차적으로 시도 됩니다.</span><span class="sxs-lookup"><span data-stu-id="10e6c-121">Each provider is tried sequentially until credentials are acquired.</span></span>

<span data-ttu-id="10e6c-122">자격 증명을 획득 하는 동안 자격 증명 서비스는 다음 순서로 자격 증명 공급자를 시도 합니다. 자격 증명을 획득 하는 즉시 중지 됩니다.</span><span class="sxs-lookup"><span data-stu-id="10e6c-122">During credential acquisition, the credential service will try credential providers in the following order, stopping as soon as credentials are acquired:</span></span>

1. <span data-ttu-id="10e6c-123">기본 제공 `SettingsCredentialProvider`를 사용 하 여 NuGet 구성 파일에서 자격 증명이 인출 됩니다.</span><span class="sxs-lookup"><span data-stu-id="10e6c-123">Credentials will be fetched from NuGet configuration files (using the built-in `SettingsCredentialProvider`).</span></span>
1. <span data-ttu-id="10e6c-124">패키지 소스가 Visual Studio Team Services에 있는 경우 `VisualStudioAccountProvider` 사용 됩니다.</span><span class="sxs-lookup"><span data-stu-id="10e6c-124">If the package source is on Visual Studio Team Services, the `VisualStudioAccountProvider` will be used.</span></span>
1. <span data-ttu-id="10e6c-125">다른 모든 플러그 인 Visual Studio 자격 증명 공급자는 순차적으로 시도 됩니다.</span><span class="sxs-lookup"><span data-stu-id="10e6c-125">All other plug-in Visual Studio credential providers will be tried sequentially.</span></span>
1. <span data-ttu-id="10e6c-126">모든 NuGet 교차 플랫폼 자격 증명 공급자를 순차적으로 사용 하려고 합니다.</span><span class="sxs-lookup"><span data-stu-id="10e6c-126">Try to use all NuGet cross platform credential providers sequentially.</span></span>
1. <span data-ttu-id="10e6c-127">자격 증명을 아직 가져오지 않은 경우 표준 기본 인증 대화 상자를 사용 하 여 자격 증명을 입력 하 라는 메시지가 표시 됩니다.</span><span class="sxs-lookup"><span data-stu-id="10e6c-127">If no credentials have been acquired yet, the user will be prompted for credentials using a standard basic authentication dialog.</span></span>

### <a name="implementing-ivscredentialprovidergetcredentialsasync"></a><span data-ttu-id="10e6c-128">IVsCredentialProvider GetCredentialsAsync를 구현 합니다.</span><span class="sxs-lookup"><span data-stu-id="10e6c-128">Implementing IVsCredentialProvider.GetCredentialsAsync</span></span>

<span data-ttu-id="10e6c-129">Visual Studio 용 NuGet 자격 증명 공급자를 만들려면 `IVsCredentialProvider` 유형을 구현 하는 공용 MEF 내보내기를 제공 하는 Visual Studio 확장을 만들고 아래에 설명 된 원칙을 준수 합니다.</span><span class="sxs-lookup"><span data-stu-id="10e6c-129">To create a NuGet credential provider for Visual Studio, create a Visual Studio Extension that exposes a public MEF Export implementing the `IVsCredentialProvider` type, and adheres to the principles outlined below.</span></span>

```cs
public interface IVsCredentialProvider
{
    Task<ICredentials> GetCredentialsAsync(
        Uri uri,
        IWebProxy proxy,
        bool isProxyRequest,
        bool isRetry,
        bool nonInteractive,
        CancellationToken cancellationToken);
}
```

<span data-ttu-id="10e6c-130">샘플 구현은 [VsCredentialProvider 샘플](https://github.com/NuGet/Samples/tree/master/VsCredentialProvider)에서 찾을 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="10e6c-130">A sample implementation can be found in [the VsCredentialProvider sample](https://github.com/NuGet/Samples/tree/master/VsCredentialProvider).</span></span>

<span data-ttu-id="10e6c-131">각 Visual Studio 용 NuGet 자격 증명 공급자는 다음을 수행 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="10e6c-131">Each NuGet credential provider for Visual Studio must:</span></span>

1. <span data-ttu-id="10e6c-132">자격 증명 획득을 시작 하기 전에 대상 URI에 대 한 자격 증명을 제공할 수 있는지 여부를 확인 합니다.</span><span class="sxs-lookup"><span data-stu-id="10e6c-132">Determine whether it can provide credentials for the targeted URI before initiating credential acquisition.</span></span> <span data-ttu-id="10e6c-133">공급자가 대상 소스에 대 한 자격 증명을 제공할 수 없는 경우 `null`을 반환 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="10e6c-133">If the provider cannot supply credentials for the targeted source, then it should return `null`.</span></span>
1. <span data-ttu-id="10e6c-134">공급자가 대상 URI에 대 한 요청을 처리 하지만 자격 증명을 제공할 수 없는 경우 예외가 throw 됩니다.</span><span class="sxs-lookup"><span data-stu-id="10e6c-134">If the provider does handle requests for the targeted URI, but cannot supply credentials, an exception should be thrown.</span></span>

<span data-ttu-id="10e6c-135">Visual Studio 용 사용자 지정 NuGet 자격 증명 공급자는 [VisualStudio 패키지](https://www.nuget.org/packages/NuGet.VisualStudio/)에서 사용할 수 있는 `IVsCredentialProvider` 인터페이스를 구현 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="10e6c-135">A custom NuGet credential provider for Visual Studio must implement the `IVsCredentialProvider` interface available in the [NuGet.VisualStudio package](https://www.nuget.org/packages/NuGet.VisualStudio/).</span></span>

#### <a name="getcredentialasync"></a><span data-ttu-id="10e6c-136">GetCredentialAsync</span><span class="sxs-lookup"><span data-stu-id="10e6c-136">GetCredentialAsync</span></span>

| <span data-ttu-id="10e6c-137">입력 매개 변수</span><span class="sxs-lookup"><span data-stu-id="10e6c-137">Input Parameter</span></span> |<span data-ttu-id="10e6c-138">설명</span><span class="sxs-lookup"><span data-stu-id="10e6c-138">Description</span></span>|
| ----------------|-----------|
| <span data-ttu-id="10e6c-139">Uri uri</span><span class="sxs-lookup"><span data-stu-id="10e6c-139">Uri uri</span></span> | <span data-ttu-id="10e6c-140">자격 증명을 요청 하는 패키지 원본 Uri입니다.</span><span class="sxs-lookup"><span data-stu-id="10e6c-140">The package source Uri for which credentials are being requested.</span></span>|
| <span data-ttu-id="10e6c-141">IWebProxy 프록시</span><span class="sxs-lookup"><span data-stu-id="10e6c-141">IWebProxy proxy</span></span> | <span data-ttu-id="10e6c-142">네트워크에서 통신할 때 사용할 웹 프록시입니다.</span><span class="sxs-lookup"><span data-stu-id="10e6c-142">Web proxy to use when communicating on the network.</span></span> <span data-ttu-id="10e6c-143">프록시 인증을 구성 하지 않은 경우 Null입니다.</span><span class="sxs-lookup"><span data-stu-id="10e6c-143">Null if there is no proxy authentication configured.</span></span> |
| <span data-ttu-id="10e6c-144">bool isProxyRequest</span><span class="sxs-lookup"><span data-stu-id="10e6c-144">bool isProxyRequest</span></span> | <span data-ttu-id="10e6c-145">이 요청이 프록시 인증 자격 증명을 가져오는 경우 True입니다.</span><span class="sxs-lookup"><span data-stu-id="10e6c-145">True if this request is to get proxy authentication credentials.</span></span> <span data-ttu-id="10e6c-146">구현이 프록시 자격 증명을 획득 하는 데 적합 하지 않은 경우 null이 반환 됩니다.</span><span class="sxs-lookup"><span data-stu-id="10e6c-146">If the implementation is not valid for acquiring proxy credentials, then null should be returned.</span></span> |
| <span data-ttu-id="10e6c-147">bool isRetry</span><span class="sxs-lookup"><span data-stu-id="10e6c-147">bool isRetry</span></span> | <span data-ttu-id="10e6c-148">이 Uri에 대해 이전에 자격 증명을 요청 했지만 제공 된 자격 증명에서 권한 있는 액세스를 허용 하지 않은 경우 True입니다.</span><span class="sxs-lookup"><span data-stu-id="10e6c-148">True if credentials were previously requested for this Uri, but the supplied credentials did not allow authorized access.</span></span> |
| <span data-ttu-id="10e6c-149">bool 비 대화형</span><span class="sxs-lookup"><span data-stu-id="10e6c-149">bool nonInteractive</span></span> | <span data-ttu-id="10e6c-150">True 이면 자격 증명 공급자가 모든 사용자 프롬프트를 표시 하지 않고 대신 기본값을 사용 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="10e6c-150">If true, the credential provider must suppress all user prompts and use default values instead.</span></span> |
| <span data-ttu-id="10e6c-151">CancellationToken cancellationToken</span><span class="sxs-lookup"><span data-stu-id="10e6c-151">CancellationToken cancellationToken</span></span> | <span data-ttu-id="10e6c-152">자격 증명을 요청 하는 작업이 취소 되었는지 확인 하려면이 취소 토큰을 확인 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="10e6c-152">This cancellation token should be checked to determine if the operation requesting credentials has been cancelled.</span></span> |

<span data-ttu-id="10e6c-153">**반환 값**: [`System.Net.ICredentials` 인터페이스](/dotnet/api/system.net.icredentials?view=netstandard-2.0)를 구현 하는 자격 증명 개체입니다.</span><span class="sxs-lookup"><span data-stu-id="10e6c-153">**Return value**: A credentials object implementing the [`System.Net.ICredentials` interface](/dotnet/api/system.net.icredentials?view=netstandard-2.0).</span></span>
