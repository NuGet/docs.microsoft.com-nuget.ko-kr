---
title: 패키지 참조 서명 | Microsoft Docs
author: rido-min
ms.author: rido-min
manager: unniravindranathan
ms.date: 03/06/2018
ms.topic: reference
ms.prod: nuget
ms.technology: ''
description: 패키지 기능 설명을 서명합니다.
keywords: NuGet 패키지 서명, 서명, 인증서
ms.reviewer:
- ananguar
- karann-msft
- unniravindranathan
ms.workload:
- dotnet
- aspnet
ms.openlocfilehash: a2a338596f7d98ded11da6fb02bafba3521249ab
ms.sourcegitcommit: beb229893559824e8abd6ab16707fd5fe1c6ac26
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 03/28/2018
---
# <a name="signed-packages"></a><span data-ttu-id="0596e-104">서명 된 패키지</span><span class="sxs-lookup"><span data-stu-id="0596e-104">Signed packages</span></span>

<span data-ttu-id="0596e-105">*NuGet 4.6.0+ 및 Visual Studio 2017 15.6 이상 버전*</span><span class="sxs-lookup"><span data-stu-id="0596e-105">*NuGet 4.6.0+ and Visual Studio 2017 version 15.6 and later*</span></span>

<span data-ttu-id="0596e-106">NuGet 패키지는 변조 된 콘텐츠에 대 한 보호를 제공 하는 디지털 서명을 포함할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="0596e-106">NuGet packages can include a digital signature that provides protection against tampered content.</span></span> <span data-ttu-id="0596e-107">이 서명은 패키지의 실제 출처에도 정품 증명을 추가 하는 X.509 인증서에서 생성 됩니다.</span><span class="sxs-lookup"><span data-stu-id="0596e-107">This signature is produced from an X.509 certificate that also adds authenticity proofs to the actual origin of the package.</span></span>

<span data-ttu-id="0596e-108">서명 된 패키지는 가장 강력한 종단 간 유효성 검사를 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="0596e-108">Signed packages provide the strongest end-to-end validation.</span></span> <span data-ttu-id="0596e-109">만든 서명을 보장 작성자에서 관계 없이 패키지를 서명 후 수정 되지 않은 패키지 저장소 또는 어떤 전송 패키지에서 전달 되는 메서드는 합니다.</span><span class="sxs-lookup"><span data-stu-id="0596e-109">An author signature guarantees that the package has not been modified since the author signed the package, no matter from which repository or what transport method the package is delivered.</span></span>

<span data-ttu-id="0596e-110">잠긴 환경 요구 하는 특정 작성자 인증서로 서명 된 패키지에 필요할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="0596e-110">Consumers who demand a locked-down environment can require packages signed with a specific author certificate.</span></span>

<span data-ttu-id="0596e-111">또한 패키지 작성자 서명 미리 서명 인증서를 등록 해야 하기 때문에 nuget.org 게시 파이프라인에는 추가 인증 메커니즘을 제공 합니다.</span><span class="sxs-lookup"><span data-stu-id="0596e-111">Additionally, author-signed packages provide an extra authentication mechanism to the nuget.org publishing pipeline because the signing certificate must be registered ahead of time.</span></span>

<span data-ttu-id="0596e-112">서명된 된 패키지를 만드는 방법에 대 한 세부 정보를 참조 하십시오. [패키지 서명](../create-packages/Sign-a-package.md) 및 [nuget sign 명령](../tools/cli-ref-sign.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="0596e-112">For details on creating a signed package, see [Signing Packages](../create-packages/Sign-a-package.md) and the [nuget sign command](../tools/cli-ref-sign.md).</span></span>

> [!Important]
> <span data-ttu-id="0596e-113">nuget.org 현재 서명 된 패키지를 받아들이지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="0596e-113">nuget.org does not presently accept signed packages.</span></span> <span data-ttu-id="0596e-114">사용자 지정 피드에 게시할 패키지에 서명할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="0596e-114">You can sign packages for publishing to custom feeds.</span></span>

## <a name="certificate-requirements"></a><span data-ttu-id="0596e-115">인증서 요구 사항</span><span class="sxs-lookup"><span data-stu-id="0596e-115">Certificate requirements</span></span>

<span data-ttu-id="0596e-116">코드 서명 인증서는 특수 한 유형의에 유효한 인증서를 필요한 패키지를 서명는 `id-kp-codeSigning` 용도 [[RFC 5280 섹션 4.2.1.12](https://tools.ietf.org/html/rfc5280#section-4.2.1.12)].</span><span class="sxs-lookup"><span data-stu-id="0596e-116">Package signing requires a code signing certificate, which is a special type of certificate that is valid for the `id-kp-codeSigning` purpose [[RFC 5280 section 4.2.1.12](https://tools.ietf.org/html/rfc5280#section-4.2.1.12)].</span></span> <span data-ttu-id="0596e-117">또한 인증서는 RSA 공개 키 길이가 2048 비트 이상이 있어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="0596e-117">Additionally, the certificate must have an RSA public key length of 2048 bits or higher.</span></span>

## <a name="get-a-code-signing-certificate"></a><span data-ttu-id="0596e-118">코드 서명 인증서를 가져오기</span><span class="sxs-lookup"><span data-stu-id="0596e-118">Get a code signing certificate</span></span>

<span data-ttu-id="0596e-119">같은 공용 인증 기관에서 유효한 인증서를 구할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="0596e-119">Valid certificates may be obtained from public certificate authorities like:</span></span>

- [<span data-ttu-id="0596e-120">Symantec</span><span class="sxs-lookup"><span data-stu-id="0596e-120">Symantec</span></span>](https://trustcenter.websecurity.symantec.com/process/trust/productOptions?productType=SoftwareValidationClass3)
- [<span data-ttu-id="0596e-121">DigiCert</span><span class="sxs-lookup"><span data-stu-id="0596e-121">DigiCert</span></span>](https://www.digicert.com/code-signing/)
- [<span data-ttu-id="0596e-122">Go Daddy</span><span class="sxs-lookup"><span data-stu-id="0596e-122">Go Daddy</span></span>](https://www.godaddy.com/web-security/code-signing-certificate)
- [<span data-ttu-id="0596e-123">전역 기호</span><span class="sxs-lookup"><span data-stu-id="0596e-123">Global Sign</span></span>](https://www.globalsign.com/en/code-signing-certificate/)
- [<span data-ttu-id="0596e-124">Comodo</span><span class="sxs-lookup"><span data-stu-id="0596e-124">Comodo</span></span>](https://www.comodo.com/e-commerce/code-signing/code-signing-certificate.php)
- [<span data-ttu-id="0596e-125">Certum</span><span class="sxs-lookup"><span data-stu-id="0596e-125">Certum</span></span>](https://www.certum.eu/certum/cert,offer_en_open_source_cs.xml) 

<span data-ttu-id="0596e-126">Windows에서 신뢰할 수 있는 인증 기관의 전체 목록을 가져올 수 있습니다 [ http://aka.ms/trustcertpartners ](http://aka.ms/trustcertpartners)합니다.</span><span class="sxs-lookup"><span data-stu-id="0596e-126">The complete list of certification authorities trusted by Windows can be obtained from [http://aka.ms/trustcertpartners](http://aka.ms/trustcertpartners).</span></span>

## <a name="create-a-test-certificate"></a><span data-ttu-id="0596e-127">테스트 인증서 만들기</span><span class="sxs-lookup"><span data-stu-id="0596e-127">Create a test certificate</span></span>

<span data-ttu-id="0596e-128">테스트용으로 자체 발급 된 인증서를 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="0596e-128">You can use self-issued certificates for testing purposes.</span></span> <span data-ttu-id="0596e-129">자체 발급 된 인증서를 만들려면 사용는 [New-selfsignedcertificate](https://docs.microsoft.com/en-us/powershell/module/pkiclient/new-selfsignedcertificate) PowerShell 명령입니다.</span><span class="sxs-lookup"><span data-stu-id="0596e-129">To create a self-issued certificate, use the [New-SelfSignedCertificate](https://docs.microsoft.com/en-us/powershell/module/pkiclient/new-selfsignedcertificate) PowerShell command.</span></span>

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

<span data-ttu-id="0596e-130">이 명령은 현재 사용자의 개인 인증서 저장소에 사용할 수 있는 테스트 인증서를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="0596e-130">This command creates a testing certificate available in the current user's personal certificate store.</span></span> <span data-ttu-id="0596e-131">실행 하 여 인증서 저장소를 열 수 `certmgr.msc` 새로 만든된 인증서를 볼 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="0596e-131">You can open the certificate store by running `certmgr.msc` to see the newly created certificate.</span></span>

## <a name="timestamp-requirements"></a><span data-ttu-id="0596e-132">타임 스탬프 요구 사항</span><span class="sxs-lookup"><span data-stu-id="0596e-132">Timestamp requirements</span></span>

<span data-ttu-id="0596e-133">서명 된 패키지는 패키지 서명 인증서의 유효 기간이 초과 서명 유효성을 보장 하도록는 RFC 3161 타임 스탬프를 포함 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="0596e-133">Signed packages should include an RFC 3161 timestamp to ensure signature validity beyond the package signing certificate's validity period.</span></span> <span data-ttu-id="0596e-134">타임 스탬프를 서명에 사용 된 인증서에 대해 유효 해야 합니다.는 `id-kp-timeStamping` 용도 [[RFC 5280 섹션 4.2.1.12](https://tools.ietf.org/html/rfc5280#section-4.2.1.12)].</span><span class="sxs-lookup"><span data-stu-id="0596e-134">The certificate used to sign the timestamp must be valid for the `id-kp-timeStamping` purpose [[RFC 5280 section 4.2.1.12](https://tools.ietf.org/html/rfc5280#section-4.2.1.12)].</span></span> <span data-ttu-id="0596e-135">또한 인증서는 RSA 공개 키 길이가 2048 비트 이상이 있어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="0596e-135">Additionally, the certificate must have an RSA public key length of 2048 bits or higher.</span></span>

<span data-ttu-id="0596e-136">추가 기술 세부 정보에서 찾을 수 있습니다는 [패키지 서명을 기술 사양](https://github.com/NuGet/Home/wiki/Package-Signatures-Technical-Details) (GitHub).</span><span class="sxs-lookup"><span data-stu-id="0596e-136">Additional technical details can be found in the [package signature technical specs](https://github.com/NuGet/Home/wiki/Package-Signatures-Technical-Details) (GitHub).</span></span>
