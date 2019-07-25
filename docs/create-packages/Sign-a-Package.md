---
title: NuGet 패키지 서명
description: 서명된 패키지를 사용하여 콘텐츠 무결성 검사를 활성화하는 방법을 설명합니다.
author: rido-min
ms.author: rmpablos
ms.date: 03/06/2018
ms.topic: conceptual
ms.reviewer: anangaur
ms.openlocfilehash: 85a862852761b68db882abdc1ca0e84d83d95f07
ms.sourcegitcommit: efc18d484fdf0c7a8979b564dcb191c030601bb4
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/18/2019
ms.locfileid: "68317637"
---
# <a name="signing-nuget-packages"></a><span data-ttu-id="9ae25-103">NuGet 패키지 서명</span><span class="sxs-lookup"><span data-stu-id="9ae25-103">Signing NuGet Packages</span></span>

<span data-ttu-id="9ae25-104">서명된 패키지는 콘텐츠 손상을 방지해 주는 콘텐츠 무결성 확인 검사를 포함합니다.</span><span class="sxs-lookup"><span data-stu-id="9ae25-104">Signed packages allows for content integrity verification checks which provides protection against content tampering.</span></span> <span data-ttu-id="9ae25-105">또한 패키지 서명은 패키지의 실제 원본에 대한 단일 기준 데이터(Single Source of Truth) 역할을 하고 소비자의 패키지 신뢰성을 강화합니다.</span><span class="sxs-lookup"><span data-stu-id="9ae25-105">The package signature also serves as the single source of truth about the actual origin of the package and bolsters package authenticity for the consumer.</span></span> <span data-ttu-id="9ae25-106">이 가이드에서는 이미 [패키지를 만들었다고](creating-a-package.md) 가정합니다.</span><span class="sxs-lookup"><span data-stu-id="9ae25-106">This guide assumes you have already [created a package](creating-a-package.md).</span></span>

## <a name="get-a-code-signing-certificate"></a><span data-ttu-id="9ae25-107">코드 서명 인증서 가져오기</span><span class="sxs-lookup"><span data-stu-id="9ae25-107">Get a code signing certificate</span></span>

<span data-ttu-id="9ae25-108">유효한 인증서는 [Symantec](https://trustcenter.websecurity.symantec.com/process/trust/productOptions?productType=SoftwareValidationClass3), [DigiCert](https://www.digicert.com/code-signing/), [Go Daddy](https://www.godaddy.com/web-security/code-signing-certificate), [Global Sign](https://www.globalsign.com/en/code-signing-certificate/), [Comodo](https://www.comodo.com/e-commerce/code-signing/code-signing-certificate.php), [Certum](https://www.certum.eu/certum/cert,offer_en_open_source_cs.xml) 등의 공용 인증서 기관에서 얻을 수 있으며, Windows에서 신뢰할 수 있는 인증 기관의 전체 목록은 [http://aka.ms/trustcertpartners](http://aka.ms/trustcertpartners)에서 확인할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="9ae25-108">Valid certificates may be obtained from a public certificate authority such as [Symantec](https://trustcenter.websecurity.symantec.com/process/trust/productOptions?productType=SoftwareValidationClass3), [DigiCert](https://www.digicert.com/code-signing/), [Go Daddy](https://www.godaddy.com/web-security/code-signing-certificate), [Global Sign](https://www.globalsign.com/en/code-signing-certificate/), [Comodo](https://www.comodo.com/e-commerce/code-signing/code-signing-certificate.php), [Certum](https://www.certum.eu/certum/cert,offer_en_open_source_cs.xml), etc. The complete list of certification authorities trusted by Windows can be obtained from [http://aka.ms/trustcertpartners](http://aka.ms/trustcertpartners).</span></span>

<span data-ttu-id="9ae25-109">테스트 목적으로 자체 발급된 인증서를 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="9ae25-109">You can use self-issued certificates for testing purposes.</span></span> <span data-ttu-id="9ae25-110">그러나 자체 발급된 인증서를 사용하여 서명된 패키지는 NuGet.org에서 수락되지 않습니다. [테스트 인증서 만들기](#create-a-test-certificate)에 대해 자세히 알아보세요.</span><span class="sxs-lookup"><span data-stu-id="9ae25-110">However, packages signed using self-issued certificates are not accepted by NuGet.org. Learn more about [creating a test certificate](#create-a-test-certificate)</span></span>

## <a name="export-the-certificate-file"></a><span data-ttu-id="9ae25-111">인증서 파일 가져오기</span><span class="sxs-lookup"><span data-stu-id="9ae25-111">Export the certificate file</span></span>

* <span data-ttu-id="9ae25-112">인증서 내보내기 마법사를 사용하여 기존 인증서를 이진 DER 형식으로 내보낼 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="9ae25-112">You can export an existing certificate to a binary DER format by using the Certificate Export Wizard.</span></span>

  ![인증서 내보내기 마법사](../reference/media/CertificateExportWizard.png)

* <span data-ttu-id="9ae25-114">또한 [Export-Certificate PowerShell 명령](/powershell/module/pkiclient/export-certificate)을 사용하여 인증서를 내보낼 수도 있습니다.</span><span class="sxs-lookup"><span data-stu-id="9ae25-114">You can also export the certificate using the [Export-Certificate PowerShell command](/powershell/module/pkiclient/export-certificate).</span></span>

## <a name="sign-the-package"></a><span data-ttu-id="9ae25-115">패키지 서명</span><span class="sxs-lookup"><span data-stu-id="9ae25-115">Sign the package</span></span>

> [!note]
> <span data-ttu-id="9ae25-116">nuget.exe 4.6.0 이상 필요</span><span class="sxs-lookup"><span data-stu-id="9ae25-116">Requires nuget.exe 4.6.0 or later</span></span>

<span data-ttu-id="9ae25-117">[nuget sign](../reference/cli-reference/cli-ref-sign.md)을 사용하여 패키지에 서명:</span><span class="sxs-lookup"><span data-stu-id="9ae25-117">Sign the package using [nuget sign](../reference/cli-reference/cli-ref-sign.md):</span></span>

```cli
nuget sign MyPackage.nupkg -CertificatePath <PathToTheCertificate> -Timestamper <TimestampServiceURL>
```

> [!Tip]
> <span data-ttu-id="9ae25-118">인증서 공급 기업은 위에서 표시된 `Timestamper` 선택적 인수에 사용할 수 있는 타임스탬프 서버 URL을 제공하는 경우가 많습니다.</span><span class="sxs-lookup"><span data-stu-id="9ae25-118">The certificate provider often also provides a timestamping server URL which you can use for the `Timestamper` optional argument show above.</span></span> <span data-ttu-id="9ae25-119">공급 기업의 설명서 및/또는 해당 서비스 URL에 대한 지원으로 문의하세요.</span><span class="sxs-lookup"><span data-stu-id="9ae25-119">Consult with your provider's documentation and/or support for that service URL.</span></span>

* <span data-ttu-id="9ae25-120">인증서 저장소에 있는 인증서나 파일의 인증서를 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="9ae25-120">You can use a certificate available in the certificate store or use a certificate from a file.</span></span> <span data-ttu-id="9ae25-121">[nuget sign](../reference/cli-reference/cli-ref-sign.md)에 대한 CLI 참조를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="9ae25-121">See CLI reference for [nuget sign](../reference/cli-reference/cli-ref-sign.md).</span></span>
* <span data-ttu-id="9ae25-122">서명 인증서가 만료된 경우 서명된 패키지에 서명이 유효하다는 것을 확인해 주는 타임스탬프가 포함되어 있어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="9ae25-122">Signed packages should include a timestamp to make sure the signature remains valid when the signing certificate has expired.</span></span> <span data-ttu-id="9ae25-123">그렇지 않으면 서명 작업에서 [경고](../reference/errors-and-warnings/NU3002.md)가 발생합니다.</span><span class="sxs-lookup"><span data-stu-id="9ae25-123">Else the sign operation will produce a [warning](../reference/errors-and-warnings/NU3002.md).</span></span>
* <span data-ttu-id="9ae25-124">[nuget verify](../reference/cli-reference/cli-ref-verify.md)를 사용하여 특정 패키지의 서명 정보를 확인할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="9ae25-124">You can see the signature details of a given package using [nuget verify](../reference/cli-reference/cli-ref-verify.md).</span></span>

## <a name="register-the-certificate-on-nugetorg"></a><span data-ttu-id="9ae25-125">NuGet.org에서 인증서 등록</span><span class="sxs-lookup"><span data-stu-id="9ae25-125">Register the certificate on NuGet.org</span></span>

<span data-ttu-id="9ae25-126">서명된 패키지를 게시하려면 먼저 NuGet.org를 사용하여 인증서를 등록해야 합니다. 이진 DER 형식의 `.cer` 파일로 인증서가 필요합니다.</span><span class="sxs-lookup"><span data-stu-id="9ae25-126">To publish a signed package, you must first register the certificate with NuGet.org. You need the certificate as a `.cer` file in a binary DER format.</span></span>

1. <span data-ttu-id="9ae25-127">NuGet.org레 [로그인](https://www.nuget.org/users/account/LogOn?returnUrl=%2F)합니다.</span><span class="sxs-lookup"><span data-stu-id="9ae25-127">[Sign in](https://www.nuget.org/users/account/LogOn?returnUrl=%2F) to NuGet.org.</span></span>
1. <span data-ttu-id="9ae25-128">`Account settings`(또는 조직 계정으로 인증서를 등록하려는 경우 `Manage Organization` **>** `Edit Organziation`)으로 이동합니다.</span><span class="sxs-lookup"><span data-stu-id="9ae25-128">Go to `Account settings` (or `Manage Organization` **>** `Edit Organziation` if you would like to register the certificate with an Organization account).</span></span>
1. <span data-ttu-id="9ae25-129">`Certificates` 섹션을 확장하고 `Register new`을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="9ae25-129">Expand the `Certificates` section and select `Register new`.</span></span>
1. <span data-ttu-id="9ae25-130">이전에 내보낸 인증서 파일을 찾아서 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="9ae25-130">Browse and select the certficate file that was exported earlier.</span></span>
  <span data-ttu-id="9ae25-131">![등록된 인증서](../reference/media/registered-certs.png)</span><span class="sxs-lookup"><span data-stu-id="9ae25-131">![Registered Certificates](../reference/media/registered-certs.png)</span></span>

<span data-ttu-id="9ae25-132">**참고:**</span><span class="sxs-lookup"><span data-stu-id="9ae25-132">**Note**</span></span>
* <span data-ttu-id="9ae25-133">한 명의 사용자가 여러 인증서를 제출하고 여러 사용자가 동일한 인증서를 등록할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="9ae25-133">One user can submit multiple certificates and the same certificate can be registered by multiple users.</span></span>
* <span data-ttu-id="9ae25-134">한 명의 사용자에게 하나의 인증서가 등록되면 이후 모든 패키지 제출 시 이러한 인증서 중 하나로 **반드시** 서명해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="9ae25-134">Once a user has a certificate registered, all future package submissions **must** be signed with one of the certificates.</span></span> <span data-ttu-id="9ae25-135">[NuGet.org에서 패키지에 대한 서명 요구 사항 관리](#manage-signing-requirements-for-your-package-on-nugetorg)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="9ae25-135">See [Manage signing requirements for your package on NuGet.org](#manage-signing-requirements-for-your-package-on-nugetorg)</span></span>
* <span data-ttu-id="9ae25-136">사용자는 계정에서 등록된 인증서를 제거할 수도 있습니다.</span><span class="sxs-lookup"><span data-stu-id="9ae25-136">Users can also remove a registered certificate from the account.</span></span> <span data-ttu-id="9ae25-137">인증서가 제거되면 해당 인증서로 서명한 새 패키지는 제출에 실패합니다.</span><span class="sxs-lookup"><span data-stu-id="9ae25-137">Once a certificate is removed, new packages signed with that certificate will fail at submission.</span></span> <span data-ttu-id="9ae25-138">기존 패키지는 영향을 받지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="9ae25-138">Existing packages aren't affected.</span></span>

## <a name="publish-the-package"></a><span data-ttu-id="9ae25-139">패키지 게시</span><span class="sxs-lookup"><span data-stu-id="9ae25-139">Publish the package</span></span>

<span data-ttu-id="9ae25-140">이제 NuGet.org에 패키지를 게시할 준비가 되었습니다. [패키지 게시](../nuget-org/Publish-a-package.md)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="9ae25-140">You are now ready to publish the package to NuGet.org. See [Publishing packages](../nuget-org/Publish-a-package.md).</span></span>

## <a name="create-a-test-certificate"></a><span data-ttu-id="9ae25-141">테스트 인증서 만들기</span><span class="sxs-lookup"><span data-stu-id="9ae25-141">Create a test certificate</span></span>

<span data-ttu-id="9ae25-142">테스트 목적으로 자체 발급된 인증서를 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="9ae25-142">You can use self-issued certificates for testing purposes.</span></span> <span data-ttu-id="9ae25-143">자체 발급된 인증서를 만들려면 [New-SelfSignedCertificate PowerShell 명령](/powershell/module/pkiclient/new-selfsignedcertificate)을 사용하세요.</span><span class="sxs-lookup"><span data-stu-id="9ae25-143">To create a self-issued certificate, use the [New-SelfSignedCertificate PowerShell command](/powershell/module/pkiclient/new-selfsignedcertificate).</span></span>

```ps
New-SelfSignedCertificate -Subject "CN=NuGet Test Developer, OU=Use for testing purposes ONLY" `
                          -FriendlyName "NuGetTestDeveloper" `
                          -Type CodeSigning `
                          -KeyUsage DigitalSignature `
                          -KeyLength 2048 `
                          -KeyAlgorithm RSA `
                          -HashAlgorithm SHA256 `
                          -Provider "Microsoft Enhanced RSA and AES Cryptographic Provider" `
                          -CertStoreLocation "Cert:\CurrentUser\My" 
```

<span data-ttu-id="9ae25-144">이 명령은 현재 사용자의 개인 인증서 저장소에서 사용할 수 있는 테스트 인증서를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="9ae25-144">This command creates a testing certificate available in the current user's personal certificate store.</span></span> <span data-ttu-id="9ae25-145">`certmgr.msc`를 실행하여 인증서 저장소를 열어 새로 만든 인증서를 볼 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="9ae25-145">You can open the certificate store by running `certmgr.msc` to see the newly created certificate.</span></span>

> [!Warning]
> <span data-ttu-id="9ae25-146">NuGet.org는 자체 발급된 인증서로 서명된 패키지를 수락하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="9ae25-146">NuGet.org does not accept packages signed with self-issued certificates.</span></span>

## <a name="manage-signing-requirements-for-your-package-on-nugetorg"></a><span data-ttu-id="9ae25-147">NuGet.org에서 패키지에 대한 서명 요구 사항 관리</span><span class="sxs-lookup"><span data-stu-id="9ae25-147">Manage signing requirements for your package on NuGet.org</span></span>
1. <span data-ttu-id="9ae25-148">NuGet.org로 [로그인](https://www.nuget.org/users/account/LogOn?returnUrl=%2F)합니다.</span><span class="sxs-lookup"><span data-stu-id="9ae25-148">[Sign in](https://www.nuget.org/users/account/LogOn?returnUrl=%2F) to NuGet.org.</span></span>

1. <span data-ttu-id="9ae25-149">`Manage Packages` 
   ![패키지 서명자 구성](../reference/media/configure-package-signers.png)으로 이동</span><span class="sxs-lookup"><span data-stu-id="9ae25-149">Go to `Manage Packages` 
![Configure package signers](../reference/media/configure-package-signers.png)</span></span>

* <span data-ttu-id="9ae25-150">사용자가 패키지의 유일한 소유자인 경우 필수 서명자입니다. 즉, 등록된 인증서 중 어느 것이나 사용하여 패키지를 서명한 후 NuGet.org로 게시할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="9ae25-150">If you are the sole owner of a package, you are the required signer i.e. you can use any of the registered certificates to sign and publish your packages to NuGet.org.</span></span>

* <span data-ttu-id="9ae25-151">패키지에 여러 소유자가 있는 경우 기본적으로 “임의” 소유자의 인증서를 사용하여 패키지를 서명할 수 있습니다.,</span><span class="sxs-lookup"><span data-stu-id="9ae25-151">If a package has multiple owners, by default, "Any" owner's certificates can be used to sign the package.</span></span> <span data-ttu-id="9ae25-152">패키지의 공동 소유자인 경우 본인 또는 임의의 다른 공동 소유자가 필수 사용자가 되도록 “임의”를 재정의할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="9ae25-152">As a co-owner of the package, you can override "Any" with yourself or any other co-owner to be the required signer.</span></span> <span data-ttu-id="9ae25-153">등록된 인증서가 없는 소유자를 만들면 서명되지 않은 패키지가 허용됩니다.</span><span class="sxs-lookup"><span data-stu-id="9ae25-153">If you make an owner  who does not have any certificate registered, then unsigned packages will be allowed.</span></span> 

* <span data-ttu-id="9ae25-154">마찬가지로, 한 명의 소유자에게는 등록된 인증서가 있고 다른 소유자에게는 등록된 인증서가 없는 경우 패키지에 기본 “임의” 옵션을 선택하면 NuGet.org는 소유자 중 한 명이 등록한 서명으로 서명된 패키지 또는 서명되지 않은 패키지를 수락합니다(소유자 중 한 명에게 등록된 인증서가 없으므로).</span><span class="sxs-lookup"><span data-stu-id="9ae25-154">Similarly, if the default "Any" option is selected for a package where one owner has a certificate registered and another owner does not have any certificate registered, then NuGet.org accepts either a signed package with a signature registered by one of its owners or an unsigned package (because one of the owners does not have any certificate registered).</span></span>

## <a name="related-articles"></a><span data-ttu-id="9ae25-155">관련 문서</span><span class="sxs-lookup"><span data-stu-id="9ae25-155">Related articles</span></span>

- [<span data-ttu-id="9ae25-156">패키지 트러스트 영역 관리</span><span class="sxs-lookup"><span data-stu-id="9ae25-156">Manage package trust boundaries</span></span>](../consume-packages/installing-signed-packages.md)
- [<span data-ttu-id="9ae25-157">서명된 패키지 참조</span><span class="sxs-lookup"><span data-stu-id="9ae25-157">Signed Packages Reference</span></span>](../reference/Signed-Packages-Reference.md)
