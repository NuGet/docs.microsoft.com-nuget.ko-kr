---
title: Visual Studio 용 NuGet 자격 증명 공급자
description: NuGet 자격 증명 공급자는 Visual Studio 확장에서 IVsCredentialProvider 인터페이스를 구현 하 여 피드를 사용 하 여 인증 합니다.
author: karann-msft
ms.author: karann
manager: unnir
ms.date: 01/09/2017
ms.topic: conceptual
ms.openlocfilehash: e8d8ae22300b55b93badb65864163d959105dca2
ms.sourcegitcommit: 8d5121af528e68789485405e24e2100fda2868d6
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/23/2018
ms.locfileid: "42793905"
---
# <a name="authenticating-feeds-in-visual-studio-with-nuget-credential-providers"></a><span data-ttu-id="1aa63-103">NuGet 자격 증명 공급자를 사용 하 여 Visual Studio에서 피드를 인증합니다.</span><span class="sxs-lookup"><span data-stu-id="1aa63-103">Authenticating feeds in Visual Studio with NuGet credential providers</span></span>

<span data-ttu-id="1aa63-104">NuGet Visual Studio 확장 3.6 이상 인증 된 피드를 사용 하는 NuGet을 사용 하도록 설정 된 자격 증명 공급자를 지원 합니다.</span><span class="sxs-lookup"><span data-stu-id="1aa63-104">The NuGet Visual Studio Extension 3.6+ supports credential providers, which enable NuGet to work with authenticated feeds.</span></span>
<span data-ttu-id="1aa63-105">Visual Studio 용 NuGet 자격 증명 공급자를 설치 하면 NuGet Visual Studio 확장을 자동으로 획득를 필요에 따라 인증 된 피드에 대 한 자격 증명 새로 고침 합니다.</span><span class="sxs-lookup"><span data-stu-id="1aa63-105">After you install a NuGet credential provider for Visual Studio, the NuGet Visual Studio extension will automatically acquire and refresh credentials for authenticated feeds as necessary.</span></span>

<span data-ttu-id="1aa63-106">샘플 구현에서 찾을 수 있습니다 [VsCredentialProvider 샘플](https://github.com/NuGet/Samples/tree/master/VsCredentialProvider)합니다.</span><span class="sxs-lookup"><span data-stu-id="1aa63-106">A sample implementation can be found in [the VsCredentialProvider sample](https://github.com/NuGet/Samples/tree/master/VsCredentialProvider).</span></span>

<span data-ttu-id="1aa63-107">4.8 이상부터 Visual Studio의 NuGet도 새 플랫폼 간 인증 플러그인을 지원 하지만 성능상의 이유로 권장 되지 수도 있습니다.</span><span class="sxs-lookup"><span data-stu-id="1aa63-107">Starting with 4.8+ NuGet in Visual Studio supports the new cross platform authentication plugins as well, but they are not the recommended approach for performance reasons.</span></span>

> [!Note]
> <span data-ttu-id="1aa63-108">Visual Studio 용 NuGet 자격 증명 공급자는 일반 Visual Studio 확장으로 설치 하 고 해야 [Visual Studio 2017](http://aka.ms/vs/15/release/vs_enterprise.exe) 이상.</span><span class="sxs-lookup"><span data-stu-id="1aa63-108">NuGet credential providers for Visual Studio must be installed as a regular Visual Studio extension and will require [Visual Studio 2017](http://aka.ms/vs/15/release/vs_enterprise.exe) or above.</span></span>
>
> <span data-ttu-id="1aa63-109">Visual Studio 용 NuGet 자격 증명 공급자 (나타나지 dotnet restore 또는 nuget.exe) Visual Studio 에서만 작동합니다.</span><span class="sxs-lookup"><span data-stu-id="1aa63-109">NuGet credential providers for Visual Studio work only in Visual Studio (not in dotnet restore or nuget.exe).</span></span> <span data-ttu-id="1aa63-110">Nuget.exe 사용 하 여 자격 증명 공급자를 참조 하세요 [nuget.exe 자격 증명 공급자](nuget-exe-Credential-providers.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="1aa63-110">For credential providers with nuget.exe, see [nuget.exe Credential Providers](nuget-exe-Credential-providers.md).</span></span>
> <span data-ttu-id="1aa63-111">Dotnet msbuild에 공급자 자격 증명에 대 한 참조 [플러그 인 플랫폼 간 NuGet](nuget-cross-platform-authentication-plugin.md)</span><span class="sxs-lookup"><span data-stu-id="1aa63-111">For credential providers in dotnet and msbuild see [NuGet cross platform plugins](nuget-cross-platform-authentication-plugin.md)</span></span>

## <a name="available-nuget-credential-providers-for-visual-studio"></a><span data-ttu-id="1aa63-112">Visual Studio 용 NuGet 자격 증명 공급자를 사용할 수 있습니다</span><span class="sxs-lookup"><span data-stu-id="1aa63-112">Available NuGet credential providers for Visual Studio</span></span>

<span data-ttu-id="1aa63-113">Visual Studio Team Services를 지원 하기 위해 Visual Studio NuGet 확장에 내장 된 자격 증명 공급자가 있습니다.</span><span class="sxs-lookup"><span data-stu-id="1aa63-113">There is a credential provider built into the Visual Studio NuGet extension to support Visual Studio Team Services.</span></span>

<span data-ttu-id="1aa63-114">내부 NuGet Visual Studio 확장을 사용 하 여 `VsCredentialProviderImporter` 또한 플러그 인 자격 증명 공급자에 대 한 검색입니다.</span><span class="sxs-lookup"><span data-stu-id="1aa63-114">The NuGet Visual Studio Extension uses an internal `VsCredentialProviderImporter` which also scans for plug-in credential providers.</span></span> <span data-ttu-id="1aa63-115">이러한 플러그 인 자격 증명 공급자는 형식의 MEF 내보내기를으로 검색이 가능 해야 합니다. `IVsCredentialProvider`합니다.</span><span class="sxs-lookup"><span data-stu-id="1aa63-115">These plug-in credential providers must be discoverable as a MEF Export of type `IVsCredentialProvider`.</span></span>

<span data-ttu-id="1aa63-116">사용 가능한 플러그 인 자격 증명 공급자는 다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="1aa63-116">Available plug-in credential providers include:</span></span>

- [<span data-ttu-id="1aa63-117">MyGet Credential Provider for Visual Studio 2017</span><span class="sxs-lookup"><span data-stu-id="1aa63-117">MyGet Credential Provider for Visual Studio 2017</span></span>](http://docs.myget.org/docs/reference/credential-provider-for-visual-studio)

## <a name="creating-a-nuget-credential-provider-for-visual-studio"></a><span data-ttu-id="1aa63-118">Visual Studio 용 NuGet 자격 증명 공급자 만들기</span><span class="sxs-lookup"><span data-stu-id="1aa63-118">Creating a NuGet credential provider for Visual Studio</span></span>

<span data-ttu-id="1aa63-119">NuGet Visual Studio 확장 3.6 이상 자격 증명을 획득 하는 데 사용 되는 내부 CredentialService를 구현 합니다.</span><span class="sxs-lookup"><span data-stu-id="1aa63-119">The NuGet Visual Studio Extension 3.6+ implements an internal CredentialService that is used to acquire credentials.</span></span> <span data-ttu-id="1aa63-120">CredentialService에 기본 제공 및 플러그 인 자격 증명 공급자의 목록이 있습니다.</span><span class="sxs-lookup"><span data-stu-id="1aa63-120">The CredentialService has a list of built-in and plug-in credential providers.</span></span> <span data-ttu-id="1aa63-121">각 공급자는 자격 증명을 획득 될 때까지 순차적으로 시도 됩니다.</span><span class="sxs-lookup"><span data-stu-id="1aa63-121">Each provider is tried sequentially until credentials are acquired.</span></span>

<span data-ttu-id="1aa63-122">자격 증명 획득 하는 동안 자격 증명 서비스 자격 증명을 획득 하는 즉시 중지를 다음 순서 대로 자격 증명 공급자를 시도 합니다.</span><span class="sxs-lookup"><span data-stu-id="1aa63-122">During credential acquisition, the credential service will try credential providers in the following order, stopping as soon as credentials are acquired:</span></span>

1. <span data-ttu-id="1aa63-123">NuGet 구성 파일에서 인출 되는 자격 증명 (기본 제공을 사용 하 여 `SettingsCredentialProvider`).</span><span class="sxs-lookup"><span data-stu-id="1aa63-123">Credentials will be fetched from NuGet configuration files (using the built-in `SettingsCredentialProvider`).</span></span>
1. <span data-ttu-id="1aa63-124">Visual Studio Team Services에서 패키지 원본이 있으면는 `VisualStudioAccountProvider` 사용 됩니다.</span><span class="sxs-lookup"><span data-stu-id="1aa63-124">If the package source is on Visual Studio Team Services, the `VisualStudioAccountProvider` will be used.</span></span>
1. <span data-ttu-id="1aa63-125">다른 모든 플러그 인 Visual Studio 자격 증명 공급자는 순차적으로 시도 합니다.</span><span class="sxs-lookup"><span data-stu-id="1aa63-125">All other plug-in Visual Studio credential providers will be tried sequentially.</span></span>
1. <span data-ttu-id="1aa63-126">순차적으로 플랫폼 자격 증명 공급자 간 모든 NuGet을 사용 하려고 합니다.</span><span class="sxs-lookup"><span data-stu-id="1aa63-126">Try to use all NuGet cross platform credential providers sequentially.</span></span>
1. <span data-ttu-id="1aa63-127">자격 증명 없이 아직 획득 하는 경우 표준 기본 인증 대화 상자를 사용 하 여 자격 증명에 대 한 사용자 라는 메시지가 표시 됩니다.</span><span class="sxs-lookup"><span data-stu-id="1aa63-127">If no credentials have been acquired yet, the user will be prompted for credentials using a standard basic authentication dialog.</span></span>

### <a name="implementing-ivscredentialprovidergetcredentialsasync"></a><span data-ttu-id="1aa63-128">IVsCredentialProvider.GetCredentialsAsync 구현</span><span class="sxs-lookup"><span data-stu-id="1aa63-128">Implementing IVsCredentialProvider.GetCredentialsAsync</span></span>

<span data-ttu-id="1aa63-129">Visual Studio 용 NuGet 자격 증명 공급자를 만들려면 공개 MEF 내보내기 구현 하는 노출 하는 Visual Studio 확장을 `IVsCredentialProvider` 를 입력 하 고 아래에 설명 된 원칙을 준수 합니다.</span><span class="sxs-lookup"><span data-stu-id="1aa63-129">To create a NuGet credential provider for Visual Studio, create a Visual Studio Extension that exposes a public MEF Export implementing the `IVsCredentialProvider` type, and adheres to the principles outlined below.</span></span>

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

<span data-ttu-id="1aa63-130">샘플 구현에서 찾을 수 있습니다 [VsCredentialProvider 샘플](https://github.com/NuGet/Samples/tree/master/VsCredentialProvider)합니다.</span><span class="sxs-lookup"><span data-stu-id="1aa63-130">A sample implementation can be found in [the VsCredentialProvider sample](https://github.com/NuGet/Samples/tree/master/VsCredentialProvider).</span></span>

<span data-ttu-id="1aa63-131">Visual Studio 용 NuGet 자격 증명 공급자 각 수행 해야합니다.</span><span class="sxs-lookup"><span data-stu-id="1aa63-131">Each NuGet credential provider for Visual Studio must:</span></span>

1. <span data-ttu-id="1aa63-132">여부를 제공할 수 있습니다 자격 증명을 대상으로 지정 된 URI에 대 한 자격 증명 획득을 시작 하기 전에 확인 합니다.</span><span class="sxs-lookup"><span data-stu-id="1aa63-132">Determine whether it can provide credentials for the targeted URI before initiating credential acquisition.</span></span> <span data-ttu-id="1aa63-133">공급자를 대상으로 지정 된 원본에 대 한 자격 증명을 제공할 수 없는 경우 반환할 `null`합니다.</span><span class="sxs-lookup"><span data-stu-id="1aa63-133">If the provider cannot supply credentials for the targeted source, then it should return `null`.</span></span>
1. <span data-ttu-id="1aa63-134">공급자는 대상된 URI에 대 한 요청을 처리 하는 자격 증명을 제공할 수 없습니다. 하지만 경우 예외가 throw 됩니다.</span><span class="sxs-lookup"><span data-stu-id="1aa63-134">If the provider does handle requests for the targeted URI, but cannot supply credentials, an exception should be thrown.</span></span>

<span data-ttu-id="1aa63-135">Visual Studio에 대 한 사용자 지정 NuGet 자격 증명 공급자를 구현 해야 합니다는 `IVsCredentialProvider` 에서 사용할 수 있는 인터페이스를 [참고로, NuGet.VisualStudio 패키지](https://www.nuget.org/packages/NuGet.VisualStudio/)합니다.</span><span class="sxs-lookup"><span data-stu-id="1aa63-135">A custom NuGet credential provider for Visual Studio must implement the `IVsCredentialProvider` interface available in the [NuGet.VisualStudio package](https://www.nuget.org/packages/NuGet.VisualStudio/).</span></span>

#### <a name="getcredentialasync"></a><span data-ttu-id="1aa63-136">GetCredentialAsync</span><span class="sxs-lookup"><span data-stu-id="1aa63-136">GetCredentialAsync</span></span>

| <span data-ttu-id="1aa63-137">매개 변수를 입력 합니다.</span><span class="sxs-lookup"><span data-stu-id="1aa63-137">Input Parameter</span></span> |<span data-ttu-id="1aa63-138">설명</span><span class="sxs-lookup"><span data-stu-id="1aa63-138">Description</span></span>|
| ----------------|-----------|
| <span data-ttu-id="1aa63-139">Uri uri</span><span class="sxs-lookup"><span data-stu-id="1aa63-139">Uri uri</span></span> | <span data-ttu-id="1aa63-140">패키지 원본에 자격 증명이 요청 되는 Uri입니다.</span><span class="sxs-lookup"><span data-stu-id="1aa63-140">The package source Uri for which credentials are being requested.</span></span>|
| <span data-ttu-id="1aa63-141">IWebProxy 프록시</span><span class="sxs-lookup"><span data-stu-id="1aa63-141">IWebProxy proxy</span></span> | <span data-ttu-id="1aa63-142">네트워크에서 통신할 때 사용할 웹 프록시입니다.</span><span class="sxs-lookup"><span data-stu-id="1aa63-142">Web proxy to use when communicating on the network.</span></span> <span data-ttu-id="1aa63-143">구성 된 프록시 인증이 없는 경우 null입니다.</span><span class="sxs-lookup"><span data-stu-id="1aa63-143">Null if there is no proxy authentication configured.</span></span> |
| <span data-ttu-id="1aa63-144">bool isProxyRequest</span><span class="sxs-lookup"><span data-stu-id="1aa63-144">bool isProxyRequest</span></span> | <span data-ttu-id="1aa63-145">이 요청은 프록시 인증 자격 증명을 가져오는 경우 true입니다.</span><span class="sxs-lookup"><span data-stu-id="1aa63-145">True if this request is to get proxy authentication credentials.</span></span> <span data-ttu-id="1aa63-146">구현에서는 프록시 자격 증명을 획득 하기 위해 유효 하지 않은, 경우에 null은 반환 되어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="1aa63-146">If the implementation is not valid for acquiring proxy credentials, then null should be returned.</span></span> |
| <span data-ttu-id="1aa63-147">bool isRetry</span><span class="sxs-lookup"><span data-stu-id="1aa63-147">bool isRetry</span></span> | <span data-ttu-id="1aa63-148">이 Uri에 대 한 자격 증명 이전에 요청한 하지만 제공된 된 자격 증명 권한 있는 액세스를 허용 하지 않은 경우 true입니다.</span><span class="sxs-lookup"><span data-stu-id="1aa63-148">True if credentials were previously requested for this Uri, but the supplied credentials did not allow authorized access.</span></span> |
| <span data-ttu-id="1aa63-149">비 대화형 bool</span><span class="sxs-lookup"><span data-stu-id="1aa63-149">bool nonInteractive</span></span> | <span data-ttu-id="1aa63-150">True 인 경우 자격 증명 공급자를 모든 사용자 프롬프트를 표시 하지 않으려면를 업데이트 하 고 기본 값을 대신 사용 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="1aa63-150">If true, the credential provider must suppress all user prompts and use default values instead.</span></span> |
| <span data-ttu-id="1aa63-151">CancellationToken cancellationToken</span><span class="sxs-lookup"><span data-stu-id="1aa63-151">CancellationToken cancellationToken</span></span> | <span data-ttu-id="1aa63-152">이 취소 토큰은 작업 자격 증명을 요청 취소 되었습니다 결정할 선택 되어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="1aa63-152">This cancellation token should be checked to determine if the operation requesting credentials has been cancelled.</span></span> |

<span data-ttu-id="1aa63-153">**값 반환**: 구현 하는 자격 증명 개체를 [ `System.Net.ICredentials` 인터페이스](/dotnet/api/system.net.icredentials?view=netstandard-2.0)합니다.</span><span class="sxs-lookup"><span data-stu-id="1aa63-153">**Return value**: A credentials object implementing the [`System.Net.ICredentials` interface](/dotnet/api/system.net.icredentials?view=netstandard-2.0).</span></span>
