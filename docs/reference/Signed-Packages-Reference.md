---
title: 서명 된 패키지
description: NuGet 패키지를 서명 하는 것에 대 한 요구 사항입니다.
author: rido-min
ms.author: rmpablos
ms.date: 05/18/2018
ms.topic: reference
ms.reviewer: ananguar
ms.openlocfilehash: 952256a24246543ecd4c37285cd001622aa2bc46
ms.sourcegitcommit: b6810860b77b2d50aab031040b047c20a333aca3
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 06/28/2019
ms.locfileid: "67426171"
---
# <a name="signed-packages"></a><span data-ttu-id="14bbb-103">서명된 패키지</span><span class="sxs-lookup"><span data-stu-id="14bbb-103">Signed packages</span></span>

<span data-ttu-id="14bbb-104">*NuGet 4.6.0+ 및 Visual Studio 2017 버전 15.6 이상*</span><span class="sxs-lookup"><span data-stu-id="14bbb-104">*NuGet 4.6.0+ and Visual Studio 2017 version 15.6 and later*</span></span>

<span data-ttu-id="14bbb-105">NuGet 패키지는 변조 된 콘텐츠에 대 한 보호를 제공 하는 디지털 서명을 포함 될 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="14bbb-105">NuGet packages can include a digital signature that provides protection against tampered content.</span></span> <span data-ttu-id="14bbb-106">이 서명은 신뢰성 증명 패키지의 실제 원본에 추가 하는 X.509 인증서에서 생성 됩니다.</span><span class="sxs-lookup"><span data-stu-id="14bbb-106">This signature is produced from an X.509 certificate that also adds authenticity proofs to the actual origin of the package.</span></span>

<span data-ttu-id="14bbb-107">서명 된 패키지는 가장 강력한 종단 간 유효성 검사를 제공 합니다.</span><span class="sxs-lookup"><span data-stu-id="14bbb-107">Signed packages provide the strongest end-to-end validation.</span></span> <span data-ttu-id="14bbb-108">두 가지 유형의 NuGet 서명 가지</span><span class="sxs-lookup"><span data-stu-id="14bbb-108">There are two different types of NuGet signatures:</span></span>
- <span data-ttu-id="14bbb-109">**서명 작성**합니다.</span><span class="sxs-lookup"><span data-stu-id="14bbb-109">**Author Signature**.</span></span> <span data-ttu-id="14bbb-110">작성자 서명 보장 작성자에서 든 관계 없이 패키지를 서명 후 수정 되지 않은 패키지 리포지토리 또는 패키지에 전달 되는 메서드를 전송 하는 합니다.</span><span class="sxs-lookup"><span data-stu-id="14bbb-110">An author signature guarantees that the package has not been modified since the author signed the package, no matter from which repository or what transport method the package is delivered.</span></span> <span data-ttu-id="14bbb-111">또한 작성자 서명 된 패키지 서명 인증서를 미리 등록 되어 있어야 하기 때문에 nuget.org 게시 파이프라인에 추가 인증 메커니즘을 제공 합니다.</span><span class="sxs-lookup"><span data-stu-id="14bbb-111">Additionally, author-signed packages provide an extra authentication mechanism to the nuget.org publishing pipeline because the signing certificate must be registered ahead of time.</span></span> <span data-ttu-id="14bbb-112">자세한 내용은 [인증서 등록](#signature-requirements-on-nugetorg)합니다.</span><span class="sxs-lookup"><span data-stu-id="14bbb-112">For more information, see [Register certificates](#signature-requirements-on-nugetorg).</span></span>
- <span data-ttu-id="14bbb-113">**리포지토리 서명**합니다.</span><span class="sxs-lookup"><span data-stu-id="14bbb-113">**Repository Signature**.</span></span> <span data-ttu-id="14bbb-114">저장소에 대 한 무결성 보장을 서명은 **모든** 패키지만 있었던 원래 저장소와 다른 위치에서 가져온 경우에 작성자 부호가 있거나 없는 되었든 관계 없이 리포지토리에서 패키지 서명.</span><span class="sxs-lookup"><span data-stu-id="14bbb-114">Repository signatures provide an integrity guarantee for **all** packages in a repository whether they are author signed or not, even if those packages are obtained from a different location than the original repository where they were signed.</span></span>   

<span data-ttu-id="14bbb-115">작성자 서명 된 패키지를 만드는 방법에 대 한 세부 정보를 참조 하세요 [패키지 서명](../create-packages/Sign-a-package.md) 하며 [nuget 서명 명령](../tools/cli-ref-sign.md)입니다.</span><span class="sxs-lookup"><span data-stu-id="14bbb-115">For details on creating an author signed package, see [Signing Packages](../create-packages/Sign-a-package.md) and the [nuget sign command](../tools/cli-ref-sign.md).</span></span>

> [!Important]
> <span data-ttu-id="14bbb-116">패키지 서명에 Windows에서 nuget.exe를 사용 하는 경우에 현재 지원 됩니다.</span><span class="sxs-lookup"><span data-stu-id="14bbb-116">Package signing is currently supported only when using nuget.exe on Windows.</span></span> <span data-ttu-id="14bbb-117">서명 된 패키지 확인은 현재 Windows에서 Visual Studio 또는 nuget.exe를 사용 하는 경우에 지원 됩니다.</span><span class="sxs-lookup"><span data-stu-id="14bbb-117">Verification of signed packages is currently supported only when using nuget.exe or Visual Studio on Windows.</span></span>

## <a name="certificate-requirements"></a><span data-ttu-id="14bbb-118">인증서 요구 사항</span><span class="sxs-lookup"><span data-stu-id="14bbb-118">Certificate requirements</span></span>

<span data-ttu-id="14bbb-119">코드 서명 인증서에 유효한 인증서의 특수 형식에 필요한 패키지를 서명 합니다 `id-kp-codeSigning` 용도 [[RFC 5280 섹션 4.2.1.12](https://tools.ietf.org/html/rfc5280#section-4.2.1.12)].</span><span class="sxs-lookup"><span data-stu-id="14bbb-119">Package signing requires a code signing certificate, which is a special type of certificate that is valid for the `id-kp-codeSigning` purpose [[RFC 5280 section 4.2.1.12](https://tools.ietf.org/html/rfc5280#section-4.2.1.12)].</span></span> <span data-ttu-id="14bbb-120">또한 인증서에는 RSA 공개 키 길이가 2048 비트 이상 있어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="14bbb-120">Additionally, the certificate must have an RSA public key length of 2048 bits or higher.</span></span>

## <a name="timestamp-requirements"></a><span data-ttu-id="14bbb-121">타임 스탬프 요구 사항</span><span class="sxs-lookup"><span data-stu-id="14bbb-121">Timestamp requirements</span></span>

<span data-ttu-id="14bbb-122">서명 된 패키지는 패키지 서명 인증서의 유효 기간이 초과 서명 유효성을 확인할 RFC 3161 타임 스탬프를 포함 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="14bbb-122">Signed packages should include an RFC 3161 timestamp to ensure signature validity beyond the package signing certificate's validity period.</span></span> <span data-ttu-id="14bbb-123">타임 스탬프를 로그인에 사용 된 인증서에 대해 유효 해야 합니다 `id-kp-timeStamping` 용도 [[RFC 5280 섹션 4.2.1.12](https://tools.ietf.org/html/rfc5280#section-4.2.1.12)].</span><span class="sxs-lookup"><span data-stu-id="14bbb-123">The certificate used to sign the timestamp must be valid for the `id-kp-timeStamping` purpose [[RFC 5280 section 4.2.1.12](https://tools.ietf.org/html/rfc5280#section-4.2.1.12)].</span></span> <span data-ttu-id="14bbb-124">또한 인증서에는 RSA 공개 키 길이가 2048 비트 이상 있어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="14bbb-124">Additionally, the certificate must have an RSA public key length of 2048 bits or higher.</span></span>

<span data-ttu-id="14bbb-125">추가 기술 세부 정보에서 확인할 수 있습니다 합니다 [패키지 서명을 기술 사양은](https://github.com/NuGet/Home/wiki/Package-Signatures-Technical-Details) (GitHub).</span><span class="sxs-lookup"><span data-stu-id="14bbb-125">Additional technical details can be found in the [package signature technical specs](https://github.com/NuGet/Home/wiki/Package-Signatures-Technical-Details) (GitHub).</span></span>

## <a name="signature-requirements-on-nugetorg"></a><span data-ttu-id="14bbb-126">NuGet.org에서 서명 요구 사항</span><span class="sxs-lookup"><span data-stu-id="14bbb-126">Signature requirements on NuGet.org</span></span>

<span data-ttu-id="14bbb-127">nuget.org에는 서명 된 패키지를 적용 하기 위한 추가 요구 사항이 있습니다.</span><span class="sxs-lookup"><span data-stu-id="14bbb-127">nuget.org has additional requirements for accepting a signed package:</span></span>

- <span data-ttu-id="14bbb-128">주 서명이 작성자 서명이 있어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="14bbb-128">The primary signature must be an author signature.</span></span>
- <span data-ttu-id="14bbb-129">주 서명이 유효한 타임 스탬프를 단일 있어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="14bbb-129">The primary signature must have a single valid timestamp.</span></span>
- <span data-ttu-id="14bbb-130">작성자 시그니처와 해당 타임 스탬프 서명을 모두에 대 한 X.509 인증서:</span><span class="sxs-lookup"><span data-stu-id="14bbb-130">The X.509 certificates for both the author signature and its timestamp signature:</span></span>
  - <span data-ttu-id="14bbb-131">RSA 공개 키 2048 비트 있어야 합니다. 이상.</span><span class="sxs-lookup"><span data-stu-id="14bbb-131">Must have an RSA public key 2048 bits or greater.</span></span>
  - <span data-ttu-id="14bbb-132">Nuget.org의 패키지 유효성 검사의 시간이 현재 UTC 시간 당 유효 기간 내에 있어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="14bbb-132">Must be within its validity period per current UTC time at time of package validation on nuget.org.</span></span>
  - <span data-ttu-id="14bbb-133">Windows에서 기본적으로 신뢰할 수 있는 신뢰할 수 있는 루트 기관에 연결 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="14bbb-133">Must chain to a trusted root authority that is trusted by default on Windows.</span></span> <span data-ttu-id="14bbb-134">자체 발급 된 인증서로 서명 된 패키지 거부 됩니다.</span><span class="sxs-lookup"><span data-stu-id="14bbb-134">Packages signed with self-issued certificates are rejected.</span></span>
  - <span data-ttu-id="14bbb-135">용도 맞는 해야 유효 합니다.</span><span class="sxs-lookup"><span data-stu-id="14bbb-135">Must be valid for its purpose:</span></span> 
    - <span data-ttu-id="14bbb-136">인증서 서명 작성자 코드 서명에 적합 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="14bbb-136">The author signing certificate must be valid for code signing.</span></span>
    - <span data-ttu-id="14bbb-137">타임 스탬프 인증서 타임 스탬프에 대 한 유효 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="14bbb-137">The timestamp certificate must be valid for timestamping.</span></span>
  - <span data-ttu-id="14bbb-138">서명할 때 취소할 수 있어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="14bbb-138">Must not be revoked at signing time.</span></span> <span data-ttu-id="14bbb-139">(이 아닐 수도 제출 시 knowable 있으므로 nuget.org 해지 상태를 주기적으로 다시).</span><span class="sxs-lookup"><span data-stu-id="14bbb-139">(This may not be knowable at submission time, so nuget.org periodically rechecks revocation status).</span></span>
  
  
## <a name="related-articles"></a><span data-ttu-id="14bbb-140">관련 문서</span><span class="sxs-lookup"><span data-stu-id="14bbb-140">Related articles</span></span>

- [<span data-ttu-id="14bbb-141">NuGet 패키지 서명</span><span class="sxs-lookup"><span data-stu-id="14bbb-141">Signing NuGet Packages</span></span>](../create-packages/Sign-a-Package.md)
- [<span data-ttu-id="14bbb-142">패키지 트러스트 관리</span><span class="sxs-lookup"><span data-stu-id="14bbb-142">Manage package trust boundaries</span></span>](../consume-packages/installing-signed-packages.md)
