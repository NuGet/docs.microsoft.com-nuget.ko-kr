---
title: 서명된 NuGet 패키지 설치
description: 서명된 NuGet 패키지를 설치하고 패키지 서명 신뢰 설정을 구성하는 프로세스를 설명합니다.
author: karann-msft
ms.author: karann
ms.date: 11/29/2018
ms.topic: conceptual
ms.openlocfilehash: 11ffaee96b6f6a9260f38c534328b6631cd96abf
ms.sourcegitcommit: 673e580ae749544a4a071b4efe7d42fd2bb6d209
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 12/06/2018
ms.locfileid: "52977837"
---
# <a name="install-a-signed-package"></a><span data-ttu-id="74556-103">서명된 패키지 설치</span><span class="sxs-lookup"><span data-stu-id="74556-103">Install a signed package</span></span>

<span data-ttu-id="74556-104">서명된 패키지는 특별한 조치 없이 설치할 수 있지만 패키지가 서명된 이후에 내용이 수정된 경우 설치가 차단되고 [NU3008](../reference/errors-and-warnings/NU3008.md) 오류가 발생합니다.</span><span class="sxs-lookup"><span data-stu-id="74556-104">Signed packages don't require any specific action to be installed; however, if the content has been modified since it was signed, the installation is blocked with error [NU3008](../reference/errors-and-warnings/NU3008.md).</span></span>

> [!Warning]
> <span data-ttu-id="74556-105">신뢰할 수 없는 인증서로 서명된 패키지는 서명되지 않은 것으로 간주되고, 다른 서명되지 않은 패키지처럼 경고나 오류 없이 설치됩니다.</span><span class="sxs-lookup"><span data-stu-id="74556-105">Packages signed with untrusted certificates are considered as unsigned and are installed without any warnings or errors like any other unsigned package.</span></span>

## <a name="configure-package-signature-requirements"></a><span data-ttu-id="74556-106">패키지 서명 요구 사항 구성</span><span class="sxs-lookup"><span data-stu-id="74556-106">Configure package signature requirements</span></span>

> [!Note]
> <span data-ttu-id="74556-107">Windows에 NuGet 4.9.0+ 및 Visual Studio 버전 15.9 이상 필요</span><span class="sxs-lookup"><span data-stu-id="74556-107">Requires NuGet 4.9.0+ and Visual Studio version 15.9 and later on Windows</span></span>

<span data-ttu-id="74556-108">[`nuget config`](../tools/cli-ref-config) 명령을 사용하여 [nuget.config](../reference/nuget-config-file) 파일에서 `signatureValidationMode`를 `require`로 설정하여 NuGet 클라이언트가 패키지 서명의 유효성을 검사하는 방법을 구성할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="74556-108">You can configure how NuGet clients validate package signatures by setting the `signatureValidationMode` to `require` in the [nuget.config](../reference/nuget-config-file) file using the [`nuget config`](../tools/cli-ref-config) command.</span></span>

```cmd
nuget.exe config -set signatureValidationMode=require
```

```xml
  <config>
    <add key="signatureValidationMode" value="require" />
  </config>
```

<span data-ttu-id="74556-109">이 모드는 모든 패키지가 `nuget.config` 파일에서 신뢰할 수 있는 인증서로 서명되었는지 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="74556-109">This mode will verify that all packages are signed by any of the certificates trusted in the `nuget.config` file.</span></span> <span data-ttu-id="74556-110">이 파일을 통해 인증서 지문에 기반하여 신뢰할 수 있는 작성자 및/또는 리포지토리를 지정할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="74556-110">This file allows you to specify which authors and/or repositories are trusted based on the certificate's fingerprint.</span></span>

### <a name="trust-package-author"></a><span data-ttu-id="74556-111">패키지 작성자 신뢰</span><span class="sxs-lookup"><span data-stu-id="74556-111">Trust package author</span></span>

<span data-ttu-id="74556-112">작성자 서명에 기반하여 패키지를 신뢰하려면 [`trusted-signers`](..tools/cli-ref-trusted-signers) 명령을 사용하여 nuget.config에서 `author` 속성을 설정합니다.</span><span class="sxs-lookup"><span data-stu-id="74556-112">To trust packages based on the author signature use the [`trusted-signers`](..tools/cli-ref-trusted-signers) command to set the `author` property in the nuget.config.</span></span>

```cmd
nuget.exe  trusted-signers Add -Name MyCompanyCert -CertificateFingerprint CE40881FF5F0AD3E58965DA20A9F571EF1651A56933748E1BF1C99E537C4E039 -FingerprintAlgorithm SHA256
```

```xml
<trustedSigners>
  <author name="MyCompanyCert">
    <certificate fingerprint="CE40881FF5F0AD3E58965DA20A9F571EF1651A56933748E1BF1C99E537C4E039" hashAlgorithm="SHA256" allowUntrustedRoot="false" />
  </author>
</trustedSigners>
```

>[!TIP]
><span data-ttu-id="74556-113">`nuget.exe` [명령 확인](https://docs.microsoft.com/en-us/nuget/tools/cli-ref-verify)을 사용하여 인증서 지문의 `SHA256` 값을 가져옵니다.</span><span class="sxs-lookup"><span data-stu-id="74556-113">Use the `nuget.exe` [verify command](https://docs.microsoft.com/en-us/nuget/tools/cli-ref-verify) to get the `SHA256` value of the certificate's fingerprint.</span></span>


### <a name="trust-all-packages-from-a-repository"></a><span data-ttu-id="74556-114">리포지토리의 모든 패키지 신뢰</span><span class="sxs-lookup"><span data-stu-id="74556-114">Trust all packages from a repository</span></span>

<span data-ttu-id="74556-115">리포지토리 서명에 기반하여 패키지를 신뢰하려면 `repository` 요소를 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="74556-115">To trust packages based on the repository signature use the `repository` element:</span></span>

```xml
<trustedSigners>  
  <repository name="nuget.org" serviceIndex="https://api.nuget.org/v3/index.json">
    <certificate fingerprint="0E5F38F57DC1BCC806D8494F4F90FBCEDD988B4676070...." 
                  hashAlgorithm="SHA256" 
                allowUntrustedRoot="false" />
  </repository>
</trustedSigners>
```

### <a name="trust-package-owners"></a><span data-ttu-id="74556-116">패키지 소유자 신뢰</span><span class="sxs-lookup"><span data-stu-id="74556-116">Trust Package Owners</span></span>

<span data-ttu-id="74556-117">리포지토리 서명에는 제출 시 패키지 소유자를 판별하는 추가 메타데이터가 포함됩니다.</span><span class="sxs-lookup"><span data-stu-id="74556-117">Repository signatures include additional metadata to determine the owners of the package at the time of submission.</span></span> <span data-ttu-id="74556-118">소유자 목록에 기반하여 리포지토리에서 패키지를 제한할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="74556-118">You can restrict packages from a repository based on a list of owners:</span></span>

```xml
<trustedSigners>  
  <repository name="nuget.org" serviceIndex="https://api.nuget.org/v3/index.json">
    <certificate fingerprint="0E5F38F57DC1BCC806D8494F4F90FBCEDD988B4676070...." 
                  hashAlgorithm="SHA256" 
                allowUntrustedRoot="false" />
      <owners>microsoft;nuget</owners>
  </repository>
</trustedSigners>
```

<span data-ttu-id="74556-119">패키지에 여러 소유자가 있고 해당 소유자 중 한 명이 신뢰할 수 있는 목록에 있는 경우 패키지 설치가 성공합니다.</span><span class="sxs-lookup"><span data-stu-id="74556-119">If a package has multiple owners, and any one of those owners is in the trusted list, the package installation will succeed.</span></span>

### <a name="untrusted-root-certificates"></a><span data-ttu-id="74556-120">신뢰할 수 없는 루트 인증서</span><span class="sxs-lookup"><span data-stu-id="74556-120">Untrusted Root certificates</span></span>

<span data-ttu-id="74556-121">일부 상황에서는 로컬 머신에서 신뢰할 수 있는 루트에 체인되지 않은 인증서를 사용하여 확인을 활성화할 수도 있습니다.</span><span class="sxs-lookup"><span data-stu-id="74556-121">In some situations you may want to enable verification using certificates that do not chain to a trusted root in the local machine.</span></span> <span data-ttu-id="74556-122">`allowUntrustedRoot` 특성을 사용하여 이 동작을 사용자 지정할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="74556-122">You can use the `allowUntrustedRoot` attribute to customize this behavior.</span></span>

### <a name="sync-repository-certificates"></a><span data-ttu-id="74556-123">리포지토리 인증서 동기화</span><span class="sxs-lookup"><span data-stu-id="74556-123">Sync repository certificates</span></span>

<span data-ttu-id="74556-124">패키지 리포지토리는 [서비스 인덱스](https://docs.microsoft.com/en-us/nuget/api/service-index)에서 사용하는 인증서를 알려야 합니다.</span><span class="sxs-lookup"><span data-stu-id="74556-124">Package repositories should announce the certificates they use in their [service index](https://docs.microsoft.com/en-us/nuget/api/service-index).</span></span> <span data-ttu-id="74556-125">결과적으로, 리포지토리는 이러한 인증서를 업데이트하게 됩니다(예: 인증서가 만료되는 경우).</span><span class="sxs-lookup"><span data-stu-id="74556-125">Eventually the repository will update these certificates, e.g. when the certificate expires.</span></span> <span data-ttu-id="74556-126">이 경우, 특정 정책이 있는 클라이언트는 새로 추가된 인증서를 포함하도록 구성을 업데이트해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="74556-126">When that happens, clients with specific policies will require an update to the configuration to include the newly added certificate.</span></span> <span data-ttu-id="74556-127">`nuget.exe` [신뢰할 수 있는 서명자 동기화 명령](/nuget/tools/cli-ref-trusted-signers.md#nuget-trusted-signers-sync--name-)을 사용하여 리포지토리에 연결된 신뢰할 수 있는 서명자를 쉽게 업그레이드할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="74556-127">You can easily upgrade the trusted signers associated to a repository by using the `nuget.exe` [trusted-signers sync command](/nuget/tools/cli-ref-trusted-signers.md#nuget-trusted-signers-sync--name-).</span></span>

### <a name="schema-reference"></a><span data-ttu-id="74556-128">스키마 참조</span><span class="sxs-lookup"><span data-stu-id="74556-128">Schema reference</span></span>

<span data-ttu-id="74556-129">클라이언트 정책에 대한 완전한 스키마 참조는 [nuget.config 참조](/nuget/reference/nuget-config-file#trustedsigners-section)에서 확인할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="74556-129">The complete schema reference for the client policies can be found in the [nuget.config reference](/nuget/reference/nuget-config-file#trustedsigners-section)</span></span>

## <a name="related-articles"></a><span data-ttu-id="74556-130">관련 문서</span><span class="sxs-lookup"><span data-stu-id="74556-130">Related articles</span></span>

- [<span data-ttu-id="74556-131">NuGet 패키지를 설치하는 다양한 방법</span><span class="sxs-lookup"><span data-stu-id="74556-131">Different ways to install a NuGet Package</span></span>](ways-to-install-a-package.md)
- [<span data-ttu-id="74556-132">NuGet 패키지 서명</span><span class="sxs-lookup"><span data-stu-id="74556-132">Signing NuGet Packages</span></span>](../create-packages/Sign-a-Package.md)
- [<span data-ttu-id="74556-133">서명된 패키지 참조</span><span class="sxs-lookup"><span data-stu-id="74556-133">Signed Packages Reference</span></span>](../reference/Signed-Packages-Reference.md)
