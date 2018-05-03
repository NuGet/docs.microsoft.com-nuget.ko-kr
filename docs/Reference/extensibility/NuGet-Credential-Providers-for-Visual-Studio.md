---
title: Visual Studio 용 NuGet 자격 증명 공급자
description: 자격 증명 공급자 NuGet 피드 Visual Studio 확장에 IVsCredentialProvider 인터페이스를 구현 하 여 인증 합니다.
author: kraigb
ms.author: kraigb
manager: douge
ms.date: 01/09/2017
ms.topic: conceptual
ms.openlocfilehash: 740df87b0d663aac482d888e916662528ce27030
ms.sourcegitcommit: 3eab9c4dd41ea7ccd2c28bb5ab16f6fbbec13708
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/26/2018
---
# <a name="authenticating-feeds-in-visual-studio-with-nuget-credential-providers"></a><span data-ttu-id="db750-103">Visual Studio에서 NuGet 자격 증명 공급자를 사용한 피드 인증</span><span class="sxs-lookup"><span data-stu-id="db750-103">Authenticating feeds in Visual Studio with NuGet credential providers</span></span>

<span data-ttu-id="db750-104">NuGet Visual Studio 확장 3.6 이상 인증 된 피드를 사용 하는 NuGet을 사용 하도록 설정 된 자격 증명 공급자를 지원 합니다.</span><span class="sxs-lookup"><span data-stu-id="db750-104">The NuGet Visual Studio Extension 3.6+ supports credential providers, which enable NuGet to work with authenticated feeds.</span></span>
<span data-ttu-id="db750-105">Visual Studio 용 NuGet 자격 증명 공급자를 설치한 후 Visual Studio 확장 자동으로 확보 하 고 필요에 따라 인증 된 피드에 대 한 자격 증명을 새로 고칩니다.</span><span class="sxs-lookup"><span data-stu-id="db750-105">After you install a NuGet credential provider for Visual Studio, the NuGet Visual Studio extension will automatically acquire and refresh credentials for authenticated feeds as necessary.</span></span>

<span data-ttu-id="db750-106">샘플 구현을 찾을 수 있습니다 [VsCredentialProvider 샘플](https://github.com/NuGet/Samples/tree/master/VsCredentialProvider)합니다.</span><span class="sxs-lookup"><span data-stu-id="db750-106">A sample implementation can be found in [the VsCredentialProvider sample](https://github.com/NuGet/Samples/tree/master/VsCredentialProvider).</span></span>

> [!Note]
> <span data-ttu-id="db750-107">Visual Studio에 대 한 자격 증명 공급자 NuGet 일반 Visual Studio 확장으로 설치 되어 있어야 하며 내용의 [Visual Studio 2017](https://aka.ms/vs/15/preview/vs_enterprise) (현재 미리 보기)에 이상.</span><span class="sxs-lookup"><span data-stu-id="db750-107">NuGet credential providers for Visual Studio must be installed as a regular Visual Studio extension and will require [Visual Studio 2017](https://aka.ms/vs/15/preview/vs_enterprise) (currently in preview) or above.</span></span>
>
> <span data-ttu-id="db750-108">Visual Studio 용 NuGet 자격 증명 공급자 (에 없는 dotnet 복원 또는 nuget.exe) Visual Studio 에서만 작동합니다.</span><span class="sxs-lookup"><span data-stu-id="db750-108">NuGet credential providers for Visual Studio work only in Visual Studio (not in dotnet restore or nuget.exe).</span></span> <span data-ttu-id="db750-109">Nuget.exe와 자격 증명 공급자를 참조 하십시오. [nuget.exe 자격 증명 공급자](nuget-exe-Credential-providers.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="db750-109">For credential providers with nuget.exe, see [nuget.exe Credential Providers](nuget-exe-Credential-providers.md).</span></span>

## <a name="available-nuget-credential-providers-for-visual-studio"></a><span data-ttu-id="db750-110">Visual Studio 용 NuGet 자격 증명 공급자를 사용할 수 있는</span><span class="sxs-lookup"><span data-stu-id="db750-110">Available NuGet credential providers for Visual Studio</span></span>

<span data-ttu-id="db750-111">Visual Studio Team Services를 지원 하기 위해 Visual Studio NuGet 확장에 기본 제공 자격 증명 공급자가 있습니다.</span><span class="sxs-lookup"><span data-stu-id="db750-111">There is a credential provider built into the Visual Studio NuGet extension to support Visual Studio Team Services.</span></span>

<span data-ttu-id="db750-112">Visual Studio Extension NuGet를 사용 하 여 내부 `VsCredentialProviderImporter` 도 플러그 인 자격 증명 공급자 검색입니다.</span><span class="sxs-lookup"><span data-stu-id="db750-112">The NuGet Visual Studio Extension uses an internal `VsCredentialProviderImporter` which also scans for plug-in credential providers.</span></span> <span data-ttu-id="db750-113">이러한 플러그 인 자격 증명 공급자는 형식의 MEF 내보낼 처럼 검색이 가능 해야 합니다. `IVsCredentialProvider`합니다.</span><span class="sxs-lookup"><span data-stu-id="db750-113">These plug-in credential providers must be discoverable as a MEF Export of type `IVsCredentialProvider`.</span></span>

<span data-ttu-id="db750-114">사용 가능한 플러그 인 자격 증명 공급자는 다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="db750-114">Available plug-in credential providers include:</span></span>

- [<span data-ttu-id="db750-115">MyGet Credential Provider for Visual Studio 2017</span><span class="sxs-lookup"><span data-stu-id="db750-115">MyGet Credential Provider for Visual Studio 2017</span></span>](http://docs.myget.org/docs/reference/credential-provider-for-visual-studio)

## <a name="creating-a-nuget-credential-provider-for-visual-studio"></a><span data-ttu-id="db750-116">Visual Studio 용 NuGet 자격 증명 공급자 만들기</span><span class="sxs-lookup"><span data-stu-id="db750-116">Creating a NuGet credential provider for Visual Studio</span></span>

<span data-ttu-id="db750-117">NuGet Visual Studio 확장 3.6 +는 자격 증명을 획득 하는 데 사용 되는 내부 CredentialService을 구현 합니다.</span><span class="sxs-lookup"><span data-stu-id="db750-117">The NuGet Visual Studio Extension 3.6+ implements an internal CredentialService that is used to acquire credentials.</span></span> <span data-ttu-id="db750-118">CredentialService에 기본 제공 및 플러그 인 자격 증명 공급자의 목록이 있습니다.</span><span class="sxs-lookup"><span data-stu-id="db750-118">The CredentialService has a list of built-in and plug-in credential providers.</span></span> <span data-ttu-id="db750-119">각 공급자는 자격 증명 획득 될 때까지 순차적으로 시도 됩니다.</span><span class="sxs-lookup"><span data-stu-id="db750-119">Each provider is tried sequentially until credentials are acquired.</span></span>

<span data-ttu-id="db750-120">자격 증명 획득 하는 동안 자격 증명 서비스 자격 증명 공급자 자격 증명 획득 되는 즉시 중지 하는 다음 순서 대로 시도 합니다.</span><span class="sxs-lookup"><span data-stu-id="db750-120">During credential acquisition, the credential service will try credential providers in the following order, stopping as soon as credentials are acquired:</span></span>

1. <span data-ttu-id="db750-121">NuGet 구성 파일에서 인출 되는 자격 증명 (기본 제공을 사용 하 여 `SettingsCredentialProvider`).</span><span class="sxs-lookup"><span data-stu-id="db750-121">Credentials will be fetched from NuGet configuration files (using the built-in `SettingsCredentialProvider`).</span></span>
1. <span data-ttu-id="db750-122">패키지 원본이 Visual Studio Team Services에 있으면는 `VisualStudioAccountProvider` 사용 됩니다.</span><span class="sxs-lookup"><span data-stu-id="db750-122">If the package source is on Visual Studio Team Services, the `VisualStudioAccountProvider` will be used.</span></span>
1. <span data-ttu-id="db750-123">다른 모든 플러그 인 자격 증명 공급자를 순차적으로 시도 합니다.</span><span class="sxs-lookup"><span data-stu-id="db750-123">All other plug-in credential providers will be tried sequentially.</span></span>
1. <span data-ttu-id="db750-124">자격 증명이 없는 아직 획득 하는 경우 자격 증명 표준 기본 인증 대화 상자를 사용 하 여 사용자를 입력 합니다.</span><span class="sxs-lookup"><span data-stu-id="db750-124">If no credentials have been acquired yet, the user will be prompted for credentials using a standard basic authentication dialog.</span></span>

### <a name="implementing-ivscredentialprovidergetcredentialsasync"></a><span data-ttu-id="db750-125">IVsCredentialProvider.GetCredentialsAsync 구현</span><span class="sxs-lookup"><span data-stu-id="db750-125">Implementing IVsCredentialProvider.GetCredentialsAsync</span></span>

<span data-ttu-id="db750-126">Visual Studio 용 NuGet 자격 증명 공급자를 만들려면 공용 MEF 내보내기 구현 하는 노출 하는 Visual Studio 확장을 만듭니다는 `IVsCredentialProvider` 를 입력 하 고 아래에서 설명 하는 원칙을 준수 합니다.</span><span class="sxs-lookup"><span data-stu-id="db750-126">To create a NuGet credential provider for Visual Studio, create a Visual Studio Extension that exposes a public MEF Export implementing the `IVsCredentialProvider` type, and adheres to the principles outlined below.</span></span>

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

<span data-ttu-id="db750-127">샘플 구현을 찾을 수 있습니다 [VsCredentialProvider 샘플](https://github.com/NuGet/Samples/tree/master/VsCredentialProvider)합니다.</span><span class="sxs-lookup"><span data-stu-id="db750-127">A sample implementation can be found in [the VsCredentialProvider sample](https://github.com/NuGet/Samples/tree/master/VsCredentialProvider).</span></span>

<span data-ttu-id="db750-128">Visual Studio 용 NuGet 자격 증명 공급자 각 수행 해야합니다.</span><span class="sxs-lookup"><span data-stu-id="db750-128">Each NuGet credential provider for Visual Studio must:</span></span>

1. <span data-ttu-id="db750-129">있는지 여부를 제공할 수 있습니다 자격 증명의 대상된 URI에 대 한 자격 증명 획득을 시작 하기 전에 확인 합니다.</span><span class="sxs-lookup"><span data-stu-id="db750-129">Determine whether it can provide credentials for the targeted URI before initiating credential acquisition.</span></span> <span data-ttu-id="db750-130">공급자 대상으로 지정 된 원본에 대 한 자격 증명을 제공할 수 없는 경우 다음을 반환 해야 `null`합니다.</span><span class="sxs-lookup"><span data-stu-id="db750-130">If the provider cannot supply credentials for the targeted source, then it should return `null`.</span></span>
1. <span data-ttu-id="db750-131">대상된 URI에 대 한 요청을 처리 하는 공급자 자격 증명을 제공할 수 없는 경우 예외가 throw 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="db750-131">If the provider does handle requests for the targeted URI, but cannot supply credentials, an exception should be thrown.</span></span>

<span data-ttu-id="db750-132">Visual Studio에 대 한 사용자 지정 NuGet 자격 증명 공급자를 구현 해야는 `IVsCredentialProvider` 에서 사용할 수 있는 인터페이스는 [NuGet.VisualStudio 패키지](https://www.nuget.org/packages/NuGet.VisualStudio/)합니다.</span><span class="sxs-lookup"><span data-stu-id="db750-132">A custom NuGet credential provider for Visual Studio must implement the `IVsCredentialProvider` interface available in the [NuGet.VisualStudio package](https://www.nuget.org/packages/NuGet.VisualStudio/).</span></span>

#### <a name="getcredentialasync"></a><span data-ttu-id="db750-133">GetCredentialAsync</span><span class="sxs-lookup"><span data-stu-id="db750-133">GetCredentialAsync</span></span>

| <span data-ttu-id="db750-134">입력된 매개 변수</span><span class="sxs-lookup"><span data-stu-id="db750-134">Input Parameter</span></span> |<span data-ttu-id="db750-135">설명</span><span class="sxs-lookup"><span data-stu-id="db750-135">Description</span></span>|
| ----------------|-----------|
| <span data-ttu-id="db750-136">Uri uri</span><span class="sxs-lookup"><span data-stu-id="db750-136">Uri uri</span></span> | <span data-ttu-id="db750-137">패키지 원본에 자격 증명이 요청 Uri입니다.</span><span class="sxs-lookup"><span data-stu-id="db750-137">The package source Uri for which credentials are being requested.</span></span>|
| <span data-ttu-id="db750-138">IWebProxy 프록시</span><span class="sxs-lookup"><span data-stu-id="db750-138">IWebProxy proxy</span></span> | <span data-ttu-id="db750-139">네트워크에서 통신에 사용할 웹 프록시입니다.</span><span class="sxs-lookup"><span data-stu-id="db750-139">Web proxy to use when communicating on the network.</span></span> <span data-ttu-id="db750-140">구성 된 프록시 인증이 없는 경우 null입니다.</span><span class="sxs-lookup"><span data-stu-id="db750-140">Null if there is no proxy authentication configured.</span></span> |
| <span data-ttu-id="db750-141">bool isProxyRequest</span><span class="sxs-lookup"><span data-stu-id="db750-141">bool isProxyRequest</span></span> | <span data-ttu-id="db750-142">True 이면이 요청은 프록시 인증 자격 증명을 가져옵니다.</span><span class="sxs-lookup"><span data-stu-id="db750-142">True if this request is to get proxy authentication credentials.</span></span> <span data-ttu-id="db750-143">프록시 자격 증명을 얻는 데 유효 하지 않으면 구현 하는 경우 null 반환 합니다.</span><span class="sxs-lookup"><span data-stu-id="db750-143">If the implementation is not valid for acquiring proxy credentials, then null should be returned.</span></span> |
| <span data-ttu-id="db750-144">bool isRetry</span><span class="sxs-lookup"><span data-stu-id="db750-144">bool isRetry</span></span> | <span data-ttu-id="db750-145">True 자격 증명 이전에이 Uri에 대해 요청 된 있지만 제공 된 자격 증명 권한이 부여 된 액세스를 허용 하지 않았습니다.</span><span class="sxs-lookup"><span data-stu-id="db750-145">True if credentials were previously requested for this Uri, but the supplied credentials did not allow authorized access.</span></span> |
| <span data-ttu-id="db750-146">비 대화형 bool</span><span class="sxs-lookup"><span data-stu-id="db750-146">bool nonInteractive</span></span> | <span data-ttu-id="db750-147">True 인 경우, 자격 증명 공급자는 모든 사용자 프롬프트를 표시 하지 않는 하 고 기본값을 대신 사용 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="db750-147">If true, the credential provider must suppress all user prompts and use default values instead.</span></span> |
| <span data-ttu-id="db750-148">CancellationToken cancellationToken</span><span class="sxs-lookup"><span data-stu-id="db750-148">CancellationToken cancellationToken</span></span> | <span data-ttu-id="db750-149">이 취소 토큰을 선택 하 여를 작업 요청 자격 증명 취소 되었습니다 결정 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="db750-149">This cancellation token should be checked to determine if the operation requesting credentials has been cancelled.</span></span> |

<span data-ttu-id="db750-150">**반환 값**: 구현 하는 자격 증명 개체는 [ `System.Net.ICredentials` 인터페이스](/dotnet/api/system.net.icredentials?view=netstandard-2.0)합니다.</span><span class="sxs-lookup"><span data-stu-id="db750-150">**Return value**: A credentials object implementing the [`System.Net.ICredentials` interface](/dotnet/api/system.net.icredentials?view=netstandard-2.0).</span></span>
