---
title: 서명 된 패키지
description: NuGet 패키지를 서명 하는 것에 대 한 요구 사항입니다.
author: rido-min
ms.author: rmpablos
ms.date: 05/18/2018
ms.topic: reference
ms.reviewer: ananguar
ms.openlocfilehash: c36db9486ad787f19430c75fc38a2e9dd8ba6e37
ms.sourcegitcommit: 1d1406764c6af5fb7801d462e0c4afc9092fa569
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 09/04/2018
ms.locfileid: "43550423"
---
# <a name="signed-packages"></a><span data-ttu-id="b49e2-103">서명 된 패키지</span><span class="sxs-lookup"><span data-stu-id="b49e2-103">Signed packages</span></span>

<span data-ttu-id="b49e2-104">*NuGet 4.6.0+ 및 Visual Studio 2017 버전 15.6 이상*</span><span class="sxs-lookup"><span data-stu-id="b49e2-104">*NuGet 4.6.0+ and Visual Studio 2017 version 15.6 and later*</span></span>

<span data-ttu-id="b49e2-105">NuGet 패키지는 변조 된 콘텐츠에 대 한 보호를 제공 하는 디지털 서명을 포함 될 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="b49e2-105">NuGet packages can include a digital signature that provides protection against tampered content.</span></span> <span data-ttu-id="b49e2-106">이 서명은 신뢰성 증명 패키지의 실제 원본에 추가 하는 X.509 인증서에서 생성 됩니다.</span><span class="sxs-lookup"><span data-stu-id="b49e2-106">This signature is produced from an X.509 certificate that also adds authenticity proofs to the actual origin of the package.</span></span>

<span data-ttu-id="b49e2-107">서명 된 패키지는 가장 강력한 종단 간 유효성 검사를 제공 합니다.</span><span class="sxs-lookup"><span data-stu-id="b49e2-107">Signed packages provide the strongest end-to-end validation.</span></span> <span data-ttu-id="b49e2-108">두 가지 유형의 NuGet 서명 가지</span><span class="sxs-lookup"><span data-stu-id="b49e2-108">There are two different types of NuGet signatures:</span></span>
- <span data-ttu-id="b49e2-109">**서명 작성**합니다.</span><span class="sxs-lookup"><span data-stu-id="b49e2-109">**Author Signature**.</span></span> <span data-ttu-id="b49e2-110">작성자 서명 보장 작성자에서 든 관계 없이 패키지를 서명 후 수정 되지 않은 패키지 리포지토리 또는 패키지에 전달 되는 메서드를 전송 하는 합니다.</span><span class="sxs-lookup"><span data-stu-id="b49e2-110">An author signature guarantees that the package has not been modified since the author signed the package, no matter from which repository or what transport method the package is delivered.</span></span> <span data-ttu-id="b49e2-111">또한 작성자 서명 된 패키지 서명 인증서를 미리 등록 되어 있어야 하기 때문에 nuget.org 게시 파이프라인에 추가 인증 메커니즘을 제공 합니다.</span><span class="sxs-lookup"><span data-stu-id="b49e2-111">Additionally, author-signed packages provide an extra authentication mechanism to the nuget.org publishing pipeline because the signing certificate must be registered ahead of time.</span></span> <span data-ttu-id="b49e2-112">자세한 내용은 [인증서 등록](#register-certificate-on-nugetorg)합니다.</span><span class="sxs-lookup"><span data-stu-id="b49e2-112">For more information, see [Register certificates](#register-certificate-on-nugetorg).</span></span>
- <span data-ttu-id="b49e2-113">**리포지토리 서명**합니다.</span><span class="sxs-lookup"><span data-stu-id="b49e2-113">**Repository Signature**.</span></span> <span data-ttu-id="b49e2-114">저장소에 대 한 무결성 보장을 서명은 **모든** 패키지만 있었던 원래 저장소와 다른 위치에서 가져온 경우에 작성자 부호가 있거나 없는 되었든 관계 없이 리포지토리에서 패키지 서명.</span><span class="sxs-lookup"><span data-stu-id="b49e2-114">Repository signatures provide an integrity guarantee for **all** packages in a repository whether they are author signed or not, even if those packages are obtained from a different location than the original repository where they were signed.</span></span>   

<span data-ttu-id="b49e2-115">작성자 서명 된 패키지를 만드는 방법에 대 한 세부 정보를 참조 하세요 [패키지 서명](../create-packages/Sign-a-package.md) 하며 [nuget 서명 명령](../tools/cli-ref-sign.md)입니다.</span><span class="sxs-lookup"><span data-stu-id="b49e2-115">For details on creating an author signed package, see [Signing Packages](../create-packages/Sign-a-package.md) and the [nuget sign command](../tools/cli-ref-sign.md).</span></span>

> [!Important]
> <span data-ttu-id="b49e2-116">패키지 서명에 Windows에서 nuget.exe를 사용 하는 경우에 현재 지원 됩니다.</span><span class="sxs-lookup"><span data-stu-id="b49e2-116">Package signing is currently supported only when using nuget.exe on Windows.</span></span> <span data-ttu-id="b49e2-117">서명 된 패키지 확인은 현재 Windows에서 Visual Studio 또는 nuget.exe를 사용 하는 경우에 지원 됩니다.</span><span class="sxs-lookup"><span data-stu-id="b49e2-117">Verification of signed packages is currently supported only when using nuget.exe or Visual Studio on Windows.</span></span>

## <a name="certificate-requirements"></a><span data-ttu-id="b49e2-118">인증서 요구 사항</span><span class="sxs-lookup"><span data-stu-id="b49e2-118">Certificate requirements</span></span>

<span data-ttu-id="b49e2-119">코드 서명 인증서에 유효한 인증서의 특수 형식에 필요한 패키지를 서명 합니다 `id-kp-codeSigning` 용도 [[RFC 5280 섹션 4.2.1.12](https://tools.ietf.org/html/rfc5280#section-4.2.1.12)].</span><span class="sxs-lookup"><span data-stu-id="b49e2-119">Package signing requires a code signing certificate, which is a special type of certificate that is valid for the `id-kp-codeSigning` purpose [[RFC 5280 section 4.2.1.12](https://tools.ietf.org/html/rfc5280#section-4.2.1.12)].</span></span> <span data-ttu-id="b49e2-120">또한 인증서에는 RSA 공개 키 길이가 2048 비트 이상 있어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="b49e2-120">Additionally, the certificate must have an RSA public key length of 2048 bits or higher.</span></span>

## <a name="get-a-code-signing-certificate"></a><span data-ttu-id="b49e2-121">코드 서명 인증서를 가져오려면</span><span class="sxs-lookup"><span data-stu-id="b49e2-121">Get a code signing certificate</span></span>

<span data-ttu-id="b49e2-122">와 같은 공용 인증 기관의 유효한 인증서를 구할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="b49e2-122">Valid certificates may be obtained from a public certificate authority like:</span></span>

- [<span data-ttu-id="b49e2-123">Symantec</span><span class="sxs-lookup"><span data-stu-id="b49e2-123">Symantec</span></span>](https://trustcenter.websecurity.symantec.com/process/trust/productOptions?productType=SoftwareValidationClass3)
- [<span data-ttu-id="b49e2-124">DigiCert</span><span class="sxs-lookup"><span data-stu-id="b49e2-124">DigiCert</span></span>](https://www.digicert.com/code-signing/)
- [<span data-ttu-id="b49e2-125">Go Daddy</span><span class="sxs-lookup"><span data-stu-id="b49e2-125">Go Daddy</span></span>](https://www.godaddy.com/web-security/code-signing-certificate)
- [<span data-ttu-id="b49e2-126">전역 기호</span><span class="sxs-lookup"><span data-stu-id="b49e2-126">Global Sign</span></span>](https://www.globalsign.com/en/code-signing-certificate/)
- [<span data-ttu-id="b49e2-127">Comodo</span><span class="sxs-lookup"><span data-stu-id="b49e2-127">Comodo</span></span>](https://www.comodo.com/e-commerce/code-signing/code-signing-certificate.php)
- [<span data-ttu-id="b49e2-128">Certum</span><span class="sxs-lookup"><span data-stu-id="b49e2-128">Certum</span></span>](https://www.certum.eu/certum/cert,offer_en_open_source_cs.xml) 

<span data-ttu-id="b49e2-129">전체 목록은 Windows에서 신뢰할 수 있는 인증 기관에서 가져올 수 있습니다 [ http://aka.ms/trustcertpartners ](http://aka.ms/trustcertpartners)합니다.</span><span class="sxs-lookup"><span data-stu-id="b49e2-129">The complete list of certification authorities trusted by Windows can be obtained from [http://aka.ms/trustcertpartners](http://aka.ms/trustcertpartners).</span></span>

## <a name="create-a-test-certificate"></a><span data-ttu-id="b49e2-130">테스트 인증서 만들기</span><span class="sxs-lookup"><span data-stu-id="b49e2-130">Create a test certificate</span></span>

<span data-ttu-id="b49e2-131">테스트 목적으로 자체 발급 된 인증서를 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="b49e2-131">You can use self-issued certificates for testing purposes.</span></span> <span data-ttu-id="b49e2-132">자체 발급 된 인증서를 만들려면 사용 합니다 [New-selfsignedcertificate PowerShell 명령을](/powershell/module/pkiclient/new-selfsignedcertificate.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="b49e2-132">To create a self-issued certificate, use the [New-SelfSignedCertificate PowerShell command](/powershell/module/pkiclient/new-selfsignedcertificate.md).</span></span>

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

<span data-ttu-id="b49e2-133">이 명령은 현재 사용자의 개인 인증서 저장소에서 사용할 수 있는 테스트 인증서를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="b49e2-133">This command creates a testing certificate available in the current user's personal certificate store.</span></span> <span data-ttu-id="b49e2-134">실행 하 여 인증서 저장소를 열면 `certmgr.msc` 새로 만든된 인증서를 확인 합니다.</span><span class="sxs-lookup"><span data-stu-id="b49e2-134">You can open the certificate store by running `certmgr.msc` to see the newly created certificate.</span></span>

> [!Warning]
> <span data-ttu-id="b49e2-135">nuget.org에 패키지를 사용할 수 없습니다 자체 발급 된 인증서를 사용 하 여 서명 합니다.</span><span class="sxs-lookup"><span data-stu-id="b49e2-135">nuget.org does not accept packages signed with self-issued certificates.</span></span>

## <a name="timestamp-requirements"></a><span data-ttu-id="b49e2-136">타임 스탬프 요구 사항</span><span class="sxs-lookup"><span data-stu-id="b49e2-136">Timestamp requirements</span></span>

<span data-ttu-id="b49e2-137">서명 된 패키지는 패키지 서명 인증서의 유효 기간이 초과 서명 유효성을 확인할 RFC 3161 타임 스탬프를 포함 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="b49e2-137">Signed packages should include an RFC 3161 timestamp to ensure signature validity beyond the package signing certificate's validity period.</span></span> <span data-ttu-id="b49e2-138">타임 스탬프를 로그인에 사용 된 인증서에 대해 유효 해야 합니다 `id-kp-timeStamping` 용도 [[RFC 5280 섹션 4.2.1.12](https://tools.ietf.org/html/rfc5280#section-4.2.1.12)].</span><span class="sxs-lookup"><span data-stu-id="b49e2-138">The certificate used to sign the timestamp must be valid for the `id-kp-timeStamping` purpose [[RFC 5280 section 4.2.1.12](https://tools.ietf.org/html/rfc5280#section-4.2.1.12)].</span></span> <span data-ttu-id="b49e2-139">또한 인증서에는 RSA 공개 키 길이가 2048 비트 이상 있어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="b49e2-139">Additionally, the certificate must have an RSA public key length of 2048 bits or higher.</span></span>

<span data-ttu-id="b49e2-140">추가 기술 세부 정보에서 확인할 수 있습니다 합니다 [패키지 서명을 기술 사양은](https://github.com/NuGet/Home/wiki/Package-Signatures-Technical-Details) (GitHub).</span><span class="sxs-lookup"><span data-stu-id="b49e2-140">Additional technical details can be found in the [package signature technical specs](https://github.com/NuGet/Home/wiki/Package-Signatures-Technical-Details) (GitHub).</span></span>

## <a name="signature-requirements-on-nugetorg"></a><span data-ttu-id="b49e2-141">Nuget.org에서 서명 요구 사항</span><span class="sxs-lookup"><span data-stu-id="b49e2-141">Signature requirements on nuget.org</span></span>

<span data-ttu-id="b49e2-142">nuget.org에는 서명 된 패키지를 적용 하기 위한 추가 요구 사항이 있습니다.</span><span class="sxs-lookup"><span data-stu-id="b49e2-142">nuget.org has additional requirements for accepting a signed package:</span></span>

- <span data-ttu-id="b49e2-143">주 서명이 작성자 서명이 있어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="b49e2-143">The primary signature must be an author signature.</span></span>
- <span data-ttu-id="b49e2-144">주 서명이 유효한 타임 스탬프를 단일 있어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="b49e2-144">The primary signature must have a single valid timestamp.</span></span>
- <span data-ttu-id="b49e2-145">작성자 시그니처와 해당 타임 스탬프 서명을 모두에 대 한 X.509 인증서:</span><span class="sxs-lookup"><span data-stu-id="b49e2-145">The X.509 certificates for both the author signature and its timestamp signature:</span></span>
  - <span data-ttu-id="b49e2-146">RSA 공개 키 2048 비트 있어야 합니다. 이상.</span><span class="sxs-lookup"><span data-stu-id="b49e2-146">Must have an RSA public key 2048 bits or greater.</span></span>
  - <span data-ttu-id="b49e2-147">Nuget.org의 패키지 유효성 검사의 시간이 현재 UTC 시간 당 유효 기간 내에 있어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="b49e2-147">Must be within its validity period per current UTC time at time of package validation on nuget.org.</span></span>
  - <span data-ttu-id="b49e2-148">Windows에서 기본적으로 신뢰할 수 있는 신뢰할 수 있는 루트 기관에 연결 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="b49e2-148">Must chain to a trusted root authority that is trusted by default on Windows.</span></span> <span data-ttu-id="b49e2-149">자체 발급 된 인증서로 서명 된 패키지 거부 됩니다.</span><span class="sxs-lookup"><span data-stu-id="b49e2-149">Packages signed with self-issued certificates are rejected.</span></span>
  - <span data-ttu-id="b49e2-150">용도 맞는 해야 유효 합니다.</span><span class="sxs-lookup"><span data-stu-id="b49e2-150">Must be valid for its purpose:</span></span> 
    - <span data-ttu-id="b49e2-151">인증서 서명 작성자 코드 서명에 적합 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="b49e2-151">The author signing certificate must be valid for code signing.</span></span>
    - <span data-ttu-id="b49e2-152">타임 스탬프 인증서 타임 스탬프에 대 한 유효 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="b49e2-152">The timestamp certificate must be valid for timestamping.</span></span>
  - <span data-ttu-id="b49e2-153">서명할 때 취소할 수 있어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="b49e2-153">Must not be revoked at signing time.</span></span> <span data-ttu-id="b49e2-154">(이 아닐 수도 제출 시 knowable 있으므로 nuget.org 해지 상태를 주기적으로 다시).</span><span class="sxs-lookup"><span data-stu-id="b49e2-154">(This may not be knowable at submission time, so nuget.org periodically rechecks revocation status).</span></span>

## <a name="register-certificate-on-nugetorg"></a><span data-ttu-id="b49e2-155">Nuget.org에서 인증서 등록</span><span class="sxs-lookup"><span data-stu-id="b49e2-155">Register certificate on nuget.org</span></span>

<span data-ttu-id="b49e2-156">서명된 된 패키지를 제출 하려면 먼저 nuget.org를 사용 하 여 인증서를 등록 해야 합니다. 해야 하는 대로 인증서를 `.cer` 이진 DER 형식에서 파일입니다.</span><span class="sxs-lookup"><span data-stu-id="b49e2-156">To submit a signed package, you must first register the certificate with nuget.org. You need the certificate as a `.cer` file in a binary DER format.</span></span> <span data-ttu-id="b49e2-157">인증서 내보내기 마법사를 사용 하 여 기존 인증서를 DER 이진 형식으로 내보낼 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="b49e2-157">You can export an existing certificate to a binary DER format by using the Certificate Export Wizard.</span></span>

![인증서 내보내기 마법사](media/CertificateExportWizard.png)

<span data-ttu-id="b49e2-159">고급 사용자를 사용 하 여 인증서를 내보낼 수 있습니다 합니다 [인증서 내보내기 PowerShell 명령을](/powershell/module/pkiclient/export-certificate.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="b49e2-159">Advanced users can export the certificate using the [Export-Certificate PowerShell command](/powershell/module/pkiclient/export-certificate.md).</span></span>

<span data-ttu-id="b49e2-160">Nuget.org를 사용 하 여 인증서를 등록 하려면로 이동 `Certificates` 섹션에서 `Account settings` 페이지 (또는 조직의 설정 페이지)를 선택 하 고 `Register new certificate`입니다.</span><span class="sxs-lookup"><span data-stu-id="b49e2-160">To register the certificate with nuget.org, go to `Certificates` section on `Account settings` page (or the Organization's settings page) and select `Register new certificate`.</span></span>

![등록 된 인증서](media/registered-certs.png)

> [!Tip]
> <span data-ttu-id="b49e2-162">한 명의 사용자가 여러 사용자가 여러 인증서와 동일한 인증서를 등록할 수 있습니다을 제출할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="b49e2-162">One user can submit multiple certificates and the same certificate can be registered by multiple users.</span></span>

<span data-ttu-id="b49e2-163">사용자는 인증서를 등록, 모든 향후 패키지 제출을 **해야** 인증서 중 하나를 사용 하 여 서명 합니다.</span><span class="sxs-lookup"><span data-stu-id="b49e2-163">Once a user has a certificate registered, all future package submissions **must** be signed with one of the certificates.</span></span>

<span data-ttu-id="b49e2-164">사용자 계정에서 등록 된 인증서를 제거할 수도 있습니다.</span><span class="sxs-lookup"><span data-stu-id="b49e2-164">Users can also remove a registered certificate from the account.</span></span> <span data-ttu-id="b49e2-165">인증서 제거 되 면 해당 인증서로 서명 된 패키지 제출에 실패 합니다.</span><span class="sxs-lookup"><span data-stu-id="b49e2-165">Once a certificate is removed, packages signed with that certificate fail at submission.</span></span> <span data-ttu-id="b49e2-166">기존 패키지에는 다음 영향을 받지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="b49e2-166">Existing packages aren't affected.</span></span>

## <a name="configure-package-signing-requirements"></a><span data-ttu-id="b49e2-167">패키지 서명 요구 사항을 구성 합니다.</span><span class="sxs-lookup"><span data-stu-id="b49e2-167">Configure package signing requirements</span></span>

<span data-ttu-id="b49e2-168">패키지의 유일한 소유자 인 경우 필요한 서명자를 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="b49e2-168">If you are the sole owner of a package, you are the required signer.</span></span> <span data-ttu-id="b49e2-169">즉, 패키지를 로그인 하 여 nuget.org에 제출 하는 등록 된 인증서를 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="b49e2-169">That is, you can use any of the registered certificates to sign your packages and submit to nuget.org.</span></span>

<span data-ttu-id="b49e2-170">패키지에 여러 소유자에 게 기본적으로 있는 경우 "임의" 소유자의 인증서 패키지 서명에 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="b49e2-170">If a package has multiple owners, by default, "Any" owner's certificates can be used to sign the package.</span></span> <span data-ttu-id="b49e2-171">패키지의 공동 소유자로 자신을 사용 하 여 "Any" 또는 다른 공동 소유자 필요한 서명자를 재정의할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="b49e2-171">As a co-owner of the package, you can override "Any" with yourself or any other co-owner to be the required signer.</span></span> <span data-ttu-id="b49e2-172">소유자로, 등록 된 모든 인증서가 없는 경우, 서명 되지 않은 패키지 허용 됩니다.</span><span class="sxs-lookup"><span data-stu-id="b49e2-172">If you make an owner  who does not have any certificate registered, then unsigned packages will be allowed.</span></span> 

<span data-ttu-id="b49e2-173">마찬가지로, 한 명의 소유자의 등록 된 인증서에 있는 패키지 및 다른 소유자에 대 한 "Any" 옵션을 선택 하는 기본 등록 된 모든 인증서에 없는 경우 다음 nuget.org 허용 서명된 된 패키지 소유자 중 하나로 등록 서명을 사용 하 여 또는 부호 없는 (없으므로 소유자 중 한 명이 등록 된 모든 인증서)를 패키지 합니다.</span><span class="sxs-lookup"><span data-stu-id="b49e2-173">Similarly, if the default "Any" option is selected for a package where one owner has a certificate registered and another owner does not have any certificate registered, then nuget.org accepts either a signed package with a signature registered by one of its owners or an unsigned package (because one of the owners does not have any certificate registered).</span></span>

![패키지 서명자를 구성 합니다.](media/configure-package-signers.png)
