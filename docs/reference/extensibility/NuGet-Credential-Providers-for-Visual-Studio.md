---
title: Visual Studio용 NuGet 자격 증명 공급 기업
description: NuGet 자격 증명 공급자는 Visual Studio 확장에서 IVsCredentialProvider 인터페이스를 구현 하 여 피드에 인증 합니다.
author: JonDouglas
ms.author: jodou
ms.date: 01/09/2017
ms.topic: conceptual
ms.openlocfilehash: ab3bde0d320375f854a8f0a98fb90acfecf54aa3
ms.sourcegitcommit: bb9560dcc7055bde84b4940c5eb0db402bf46a48
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 03/23/2021
ms.locfileid: "104859098"
---
# <a name="authenticating-feeds-in-visual-studio-with-nuget-credential-providers"></a><span data-ttu-id="f0b6a-103">NuGet 자격 증명 공급자를 사용 하 여 Visual Studio에서 피드 인증</span><span class="sxs-lookup"><span data-stu-id="f0b6a-103">Authenticating feeds in Visual Studio with NuGet credential providers</span></span>

<span data-ttu-id="f0b6a-104">NuGet Visual Studio 확장 3.6 +는 NuGet이 인증 된 피드에 사용할 수 있도록 하는 자격 증명 공급자를 지원 합니다.</span><span class="sxs-lookup"><span data-stu-id="f0b6a-104">The NuGet Visual Studio Extension 3.6+ supports credential providers, which enable NuGet to work with authenticated feeds.</span></span>
<span data-ttu-id="f0b6a-105">Visual Studio 용 NuGet 자격 증명 공급자를 설치 하면 NuGet Visual Studio 확장에서 필요한 경우 인증 된 피드에 대 한 자격 증명을 자동으로 획득 하 고 새로 고칩니다.</span><span class="sxs-lookup"><span data-stu-id="f0b6a-105">After you install a NuGet credential provider for Visual Studio, the NuGet Visual Studio extension will automatically acquire and refresh credentials for authenticated feeds as necessary.</span></span>

<span data-ttu-id="f0b6a-106">샘플 구현은 [VsCredentialProvider 샘플](https://github.com/NuGet/Samples/tree/main/VsCredentialProvider)에서 찾을 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="f0b6a-106">A sample implementation can be found in [the VsCredentialProvider sample](https://github.com/NuGet/Samples/tree/main/VsCredentialProvider).</span></span>

<span data-ttu-id="f0b6a-107">Visual Studio 내에서 NuGet은 플러그 인 `VsCredentialProviderImporter` 자격 증명 공급자도 검색 하는 내부를 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="f0b6a-107">Within Visual Studio, NuGet uses an internal `VsCredentialProviderImporter` which also scans for plug-in credential providers.</span></span> <span data-ttu-id="f0b6a-108">이러한 플러그 인 자격 증명 공급자는 형식의 MEF 내보내기로 검색할 수 있어야 합니다 `IVsCredentialProvider` .</span><span class="sxs-lookup"><span data-stu-id="f0b6a-108">These plug-in credential providers must be discoverable as a MEF Export of type `IVsCredentialProvider`.</span></span>

<span data-ttu-id="f0b6a-109">Visual Studio에서 4.8 + NuGet 부터는 새로운 플랫폼 간 인증 플러그 인도 지원 하지만 성능상의 이유로 권장 되는 방법은 아닙니다.</span><span class="sxs-lookup"><span data-stu-id="f0b6a-109">Starting with 4.8+ NuGet in Visual Studio supports the new cross platform authentication plugins as well, but they are not the recommended approach for performance reasons.</span></span>

> [!Note]
> <span data-ttu-id="f0b6a-110">Visual Studio 용 NuGet 자격 증명 공급자는 일반 Visual Studio 확장으로 설치 해야 하며 [Visual studio 2017](https://aka.ms/vs/15/release/vs_enterprise.exe) 이상이 필요 합니다.</span><span class="sxs-lookup"><span data-stu-id="f0b6a-110">NuGet credential providers for Visual Studio must be installed as a regular Visual Studio extension and will require [Visual Studio 2017](https://aka.ms/vs/15/release/vs_enterprise.exe) or above.</span></span>
>
> <span data-ttu-id="f0b6a-111">Visual Studio 용 NuGet 자격 증명 공급자는 Visual Studio 에서만 작동 합니다 (dotnet restore 또는 nuget.exe).</span><span class="sxs-lookup"><span data-stu-id="f0b6a-111">NuGet credential providers for Visual Studio work only in Visual Studio (not in dotnet restore or nuget.exe).</span></span> <span data-ttu-id="f0b6a-112">nuget.exe 자격 증명 공급자는 [nuget.exe 자격 증명 공급자](nuget-exe-Credential-providers.md)를 참조 하세요.</span><span class="sxs-lookup"><span data-stu-id="f0b6a-112">For credential providers with nuget.exe, see [nuget.exe Credential Providers](nuget-exe-Credential-providers.md).</span></span>
> <span data-ttu-id="f0b6a-113">Dotnet 및 msbuild의 자격 증명 공급자의 경우 [NuGet 플랫폼 간 플러그 인](nuget-cross-platform-authentication-plugin.md) 을 참조 하세요.</span><span class="sxs-lookup"><span data-stu-id="f0b6a-113">For credential providers in dotnet and msbuild see [NuGet cross platform plugins](nuget-cross-platform-authentication-plugin.md)</span></span>

## <a name="creating-a-nuget-credential-provider-for-visual-studio"></a><span data-ttu-id="f0b6a-114">Visual Studio 용 NuGet 자격 증명 공급자 만들기</span><span class="sxs-lookup"><span data-stu-id="f0b6a-114">Creating a NuGet credential provider for Visual Studio</span></span>

<span data-ttu-id="f0b6a-115">NuGet Visual Studio 확장 3.6 +는 자격 증명을 획득 하는 데 사용 되는 내부 CredentialService를 구현 합니다.</span><span class="sxs-lookup"><span data-stu-id="f0b6a-115">The NuGet Visual Studio Extension 3.6+ implements an internal CredentialService that is used to acquire credentials.</span></span> <span data-ttu-id="f0b6a-116">CredentialService에는 기본 제공 및 플러그 인 자격 증명 공급자 목록이 있습니다.</span><span class="sxs-lookup"><span data-stu-id="f0b6a-116">The CredentialService has a list of built-in and plug-in credential providers.</span></span> <span data-ttu-id="f0b6a-117">각 공급자는 자격 증명을 가져올 때까지 순차적으로 시도 됩니다.</span><span class="sxs-lookup"><span data-stu-id="f0b6a-117">Each provider is tried sequentially until credentials are acquired.</span></span>

<span data-ttu-id="f0b6a-118">자격 증명을 획득 하는 동안 자격 증명 서비스는 다음 순서로 자격 증명 공급자를 시도 합니다. 자격 증명을 획득 하는 즉시 중지 됩니다.</span><span class="sxs-lookup"><span data-stu-id="f0b6a-118">During credential acquisition, the credential service will try credential providers in the following order, stopping as soon as credentials are acquired:</span></span>

1. <span data-ttu-id="f0b6a-119">기본 제공을 사용 하 여 NuGet 구성 파일에서 자격 증명을 인출 `SettingsCredentialProvider` 합니다.</span><span class="sxs-lookup"><span data-stu-id="f0b6a-119">Credentials will be fetched from NuGet configuration files (using the built-in `SettingsCredentialProvider`).</span></span>
1. <span data-ttu-id="f0b6a-120">패키지 소스가 Visual Studio Team Services에 있는 경우가 사용 됩니다 `VisualStudioAccountProvider` .</span><span class="sxs-lookup"><span data-stu-id="f0b6a-120">If the package source is on Visual Studio Team Services, the `VisualStudioAccountProvider` will be used.</span></span>
1. <span data-ttu-id="f0b6a-121">다른 모든 플러그 인 Visual Studio 자격 증명 공급자는 순차적으로 시도 됩니다.</span><span class="sxs-lookup"><span data-stu-id="f0b6a-121">All other plug-in Visual Studio credential providers will be tried sequentially.</span></span>
1. <span data-ttu-id="f0b6a-122">모든 NuGet 교차 플랫폼 자격 증명 공급자를 순차적으로 사용 하려고 합니다.</span><span class="sxs-lookup"><span data-stu-id="f0b6a-122">Try to use all NuGet cross platform credential providers sequentially.</span></span>
1. <span data-ttu-id="f0b6a-123">자격 증명을 아직 가져오지 않은 경우 표준 기본 인증 대화 상자를 사용 하 여 자격 증명을 입력 하 라는 메시지가 표시 됩니다.</span><span class="sxs-lookup"><span data-stu-id="f0b6a-123">If no credentials have been acquired yet, the user will be prompted for credentials using a standard basic authentication dialog.</span></span>

### <a name="implementing-ivscredentialprovidergetcredentialsasync"></a><span data-ttu-id="f0b6a-124">IVsCredentialProvider GetCredentialsAsync를 구현 합니다.</span><span class="sxs-lookup"><span data-stu-id="f0b6a-124">Implementing IVsCredentialProvider.GetCredentialsAsync</span></span>

<span data-ttu-id="f0b6a-125">Visual Studio 용 NuGet 자격 증명 공급자를 만들려면 형식을 구현 하는 공용 MEF 내보내기를 제공 하는 Visual Studio 확장을 만들고 `IVsCredentialProvider` 아래에 설명 된 원칙을 따릅니다.</span><span class="sxs-lookup"><span data-stu-id="f0b6a-125">To create a NuGet credential provider for Visual Studio, create a Visual Studio Extension that exposes a public MEF Export implementing the `IVsCredentialProvider` type, and adheres to the principles outlined below.</span></span>

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

<span data-ttu-id="f0b6a-126">샘플 구현은 [VsCredentialProvider 샘플](https://github.com/NuGet/Samples/tree/main/VsCredentialProvider)에서 찾을 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="f0b6a-126">A sample implementation can be found in [the VsCredentialProvider sample](https://github.com/NuGet/Samples/tree/main/VsCredentialProvider).</span></span>

<span data-ttu-id="f0b6a-127">각 Visual Studio 용 NuGet 자격 증명 공급자는 다음을 수행 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="f0b6a-127">Each NuGet credential provider for Visual Studio must:</span></span>

1. <span data-ttu-id="f0b6a-128">자격 증명 획득을 시작 하기 전에 대상 URI에 대 한 자격 증명을 제공할 수 있는지 여부를 확인 합니다.</span><span class="sxs-lookup"><span data-stu-id="f0b6a-128">Determine whether it can provide credentials for the targeted URI before initiating credential acquisition.</span></span> <span data-ttu-id="f0b6a-129">공급자가 대상 소스에 대 한 자격 증명을 제공할 수 없는 경우를 반환 해야 `null` 합니다.</span><span class="sxs-lookup"><span data-stu-id="f0b6a-129">If the provider cannot supply credentials for the targeted source, then it should return `null`.</span></span>
1. <span data-ttu-id="f0b6a-130">공급자가 대상 URI에 대 한 요청을 처리 하지만 자격 증명을 제공할 수 없는 경우 예외가 throw 됩니다.</span><span class="sxs-lookup"><span data-stu-id="f0b6a-130">If the provider does handle requests for the targeted URI, but cannot supply credentials, an exception should be thrown.</span></span>

<span data-ttu-id="f0b6a-131">Visual Studio 용 사용자 지정 NuGet 자격 증명 공급자는 `IVsCredentialProvider` [VisualStudio 패키지](https://www.nuget.org/packages/NuGet.VisualStudio/)에서 사용할 수 있는 인터페이스를 구현 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="f0b6a-131">A custom NuGet credential provider for Visual Studio must implement the `IVsCredentialProvider` interface available in the [NuGet.VisualStudio package](https://www.nuget.org/packages/NuGet.VisualStudio/).</span></span>

#### <a name="getcredentialasync"></a><span data-ttu-id="f0b6a-132">GetCredentialAsync</span><span class="sxs-lookup"><span data-stu-id="f0b6a-132">GetCredentialAsync</span></span>

| <span data-ttu-id="f0b6a-133">입력 매개 변수</span><span class="sxs-lookup"><span data-stu-id="f0b6a-133">Input Parameter</span></span> |<span data-ttu-id="f0b6a-134">Description</span><span class="sxs-lookup"><span data-stu-id="f0b6a-134">Description</span></span>|
| ----------------|-----------|
| <span data-ttu-id="f0b6a-135">Uri uri</span><span class="sxs-lookup"><span data-stu-id="f0b6a-135">Uri uri</span></span> | <span data-ttu-id="f0b6a-136">자격 증명을 요청 하는 패키지 원본 Uri입니다.</span><span class="sxs-lookup"><span data-stu-id="f0b6a-136">The package source Uri for which credentials are being requested.</span></span>|
| <span data-ttu-id="f0b6a-137">IWebProxy 프록시</span><span class="sxs-lookup"><span data-stu-id="f0b6a-137">IWebProxy proxy</span></span> | <span data-ttu-id="f0b6a-138">네트워크에서 통신할 때 사용할 웹 프록시입니다.</span><span class="sxs-lookup"><span data-stu-id="f0b6a-138">Web proxy to use when communicating on the network.</span></span> <span data-ttu-id="f0b6a-139">프록시 인증을 구성 하지 않은 경우 Null입니다.</span><span class="sxs-lookup"><span data-stu-id="f0b6a-139">Null if there is no proxy authentication configured.</span></span> |
| <span data-ttu-id="f0b6a-140">bool isProxyRequest</span><span class="sxs-lookup"><span data-stu-id="f0b6a-140">bool isProxyRequest</span></span> | <span data-ttu-id="f0b6a-141">이 요청이 프록시 인증 자격 증명을 가져오는 경우 True입니다.</span><span class="sxs-lookup"><span data-stu-id="f0b6a-141">True if this request is to get proxy authentication credentials.</span></span> <span data-ttu-id="f0b6a-142">구현이 프록시 자격 증명을 획득 하는 데 적합 하지 않은 경우 null이 반환 됩니다.</span><span class="sxs-lookup"><span data-stu-id="f0b6a-142">If the implementation is not valid for acquiring proxy credentials, then null should be returned.</span></span> |
| <span data-ttu-id="f0b6a-143">bool isRetry</span><span class="sxs-lookup"><span data-stu-id="f0b6a-143">bool isRetry</span></span> | <span data-ttu-id="f0b6a-144">이 Uri에 대해 이전에 자격 증명을 요청 했지만 제공 된 자격 증명에서 권한 있는 액세스를 허용 하지 않은 경우 True입니다.</span><span class="sxs-lookup"><span data-stu-id="f0b6a-144">True if credentials were previously requested for this Uri, but the supplied credentials did not allow authorized access.</span></span> |
| <span data-ttu-id="f0b6a-145">bool 비 대화형</span><span class="sxs-lookup"><span data-stu-id="f0b6a-145">bool nonInteractive</span></span> | <span data-ttu-id="f0b6a-146">True 이면 자격 증명 공급자가 모든 사용자 프롬프트를 표시 하지 않고 대신 기본값을 사용 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="f0b6a-146">If true, the credential provider must suppress all user prompts and use default values instead.</span></span> |
| <span data-ttu-id="f0b6a-147">CancellationToken cancellationToken</span><span class="sxs-lookup"><span data-stu-id="f0b6a-147">CancellationToken cancellationToken</span></span> | <span data-ttu-id="f0b6a-148">자격 증명을 요청 하는 작업이 취소 되었는지 확인 하려면이 취소 토큰을 확인 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="f0b6a-148">This cancellation token should be checked to determine if the operation requesting credentials has been cancelled.</span></span> |

<span data-ttu-id="f0b6a-149">**반환 값**: [ `System.Net.ICredentials` 인터페이스](/dotnet/api/system.net.icredentials)를 구현 하는 자격 증명 개체입니다.</span><span class="sxs-lookup"><span data-stu-id="f0b6a-149">**Return value**: A credentials object implementing the [`System.Net.ICredentials` interface](/dotnet/api/system.net.icredentials).</span></span>
