---
title: 서명 된 패키지
description: NuGet 패키지 서명에 대 한 요구 사항입니다.
author: rido-min
ms.author: rmpablos
ms.date: 05/18/2018
ms.topic: reference
ms.reviewer: ananguar
ms.openlocfilehash: 85fdf7a41cc033d92bbd0326648142aec27a9970
ms.sourcegitcommit: 1462f9f42ae36b3c990762ad4f02e38ab799ad09
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/15/2021
ms.locfileid: "107508802"
---
# <a name="signed-packages"></a><span data-ttu-id="69386-103">서명된 패키지</span><span class="sxs-lookup"><span data-stu-id="69386-103">Signed packages</span></span>

<span data-ttu-id="69386-104">*NuGet 4.6.0 + 및 Visual Studio 2017 버전 15.6 이상*</span><span class="sxs-lookup"><span data-stu-id="69386-104">*NuGet 4.6.0+ and Visual Studio 2017 version 15.6 and later*</span></span>

<span data-ttu-id="69386-105">NuGet 패키지에는 변조 된 콘텐츠에 대 한 보호를 제공 하는 디지털 서명이 포함 될 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="69386-105">NuGet packages can include a digital signature that provides protection against tampered content.</span></span> <span data-ttu-id="69386-106">이 서명은 패키지의 실제 원본에도 신뢰성 증명을 추가 하는 x.509 인증서에서 생성 됩니다.</span><span class="sxs-lookup"><span data-stu-id="69386-106">This signature is produced from an X.509 certificate that also adds authenticity proofs to the actual origin of the package.</span></span>

<span data-ttu-id="69386-107">서명 된 패키지는 가장 강력한 종단 간 유효성 검사를 제공 합니다.</span><span class="sxs-lookup"><span data-stu-id="69386-107">Signed packages provide the strongest end-to-end validation.</span></span> <span data-ttu-id="69386-108">NuGet 서명에는 다음과 같은 두 가지 유형이 있습니다.</span><span class="sxs-lookup"><span data-stu-id="69386-108">There are two different types of NuGet signatures:</span></span>
- <span data-ttu-id="69386-109">**작성자 서명**.</span><span class="sxs-lookup"><span data-stu-id="69386-109">**Author signature**.</span></span> <span data-ttu-id="69386-110">작성자 서명은 패키지가 전송 되는 리포지토리 또는 전송 방법에 관계 없이 패키지가 서명 된 이후 패키지가 수정 되지 않았음을 보장 합니다.</span><span class="sxs-lookup"><span data-stu-id="69386-110">An author signature guarantees that the package has not been modified since the author signed the package, no matter from which repository or what transport method the package is delivered.</span></span> <span data-ttu-id="69386-111">또한 작성자 서명 된 패키지는 서명 인증서를 미리 등록 해야 하기 때문에 nuget.org 게시 파이프라인에 추가 인증 메커니즘을 제공 합니다.</span><span class="sxs-lookup"><span data-stu-id="69386-111">Additionally, author-signed packages provide an extra authentication mechanism to the nuget.org publishing pipeline because the signing certificate must be registered ahead of time.</span></span> <span data-ttu-id="69386-112">자세한 내용은 [인증서 등록](#signature-requirements-on-nugetorg)을 참조 하세요.</span><span class="sxs-lookup"><span data-stu-id="69386-112">For more information, see [Register certificates](#signature-requirements-on-nugetorg).</span></span>
- <span data-ttu-id="69386-113">**리포지토리 서명**.</span><span class="sxs-lookup"><span data-stu-id="69386-113">**Repository signature**.</span></span> <span data-ttu-id="69386-114">리포지토리에 서명 되었는지 여부에 관계 없이 리포지토리의 **모든** 패키지에 대 한 무결성 보장을 제공 합니다 .이는 해당 패키지가 서명 된 원본 리포지토리와 다른 위치에서 가져오는 경우에도 마찬가지입니다.</span><span class="sxs-lookup"><span data-stu-id="69386-114">Repository signatures provide an integrity guarantee for **all** packages in a repository whether they are author signed or not, even if those packages are obtained from a different location than the original repository where they were signed.</span></span>   

<span data-ttu-id="69386-115">작성자 서명 된 패키지를 만드는 방법에 대 한 자세한 내용은 [패키지 서명](../create-packages/Sign-a-package.md) 및 [nuget sign 명령](../reference/cli-reference/cli-ref-sign.md)을 참조 하세요.</span><span class="sxs-lookup"><span data-stu-id="69386-115">For details on creating an author signed package, see [Signing Packages](../create-packages/Sign-a-package.md) and the [nuget sign command](../reference/cli-reference/cli-ref-sign.md).</span></span> <span data-ttu-id="69386-116">[Dotnet nuget verify](/dotnet/core/tools/dotnet-nuget-verify) 또는 [nuget verify](../reference/cli-reference/cli-ref-verify.md) 명령을 사용 하 여 패키지의 서명을 확인할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="69386-116">You can verify packages' signatures using the [dotnet nuget verify](/dotnet/core/tools/dotnet-nuget-verify) or [nuget verify](../reference/cli-reference/cli-ref-verify.md) commands.</span></span>

> [!Important]
> <span data-ttu-id="69386-117">작성자 서명 패키지는 현재 Windows의 nuget.exe 에서만 지원 됩니다.</span><span class="sxs-lookup"><span data-stu-id="69386-117">Author signing packages is only supported by nuget.exe on Windows at this time.</span></span> <span data-ttu-id="69386-118">그러나 nuget.org에 업로드 된 모든 패키지는 자동으로 리포지토리에 서명 됩니다.</span><span class="sxs-lookup"><span data-stu-id="69386-118">However, all packages uploaded to nuget.org are automatically repository signed.</span></span>

## <a name="certificate-requirements"></a><span data-ttu-id="69386-119">인증서 요구 사항</span><span class="sxs-lookup"><span data-stu-id="69386-119">Certificate requirements</span></span>

<span data-ttu-id="69386-120">패키지 서명에는 코드 서명 인증서가 필요 합니다 .이 인증서는 `id-kp-codeSigning` 목적 [[RFC 5280 섹션 4.2.1.12](https://tools.ietf.org/html/rfc5280#section-4.2.1.12)]에 유효한 특수 한 인증서 형식입니다.</span><span class="sxs-lookup"><span data-stu-id="69386-120">Package signing requires a code signing certificate, which is a special type of certificate that is valid for the `id-kp-codeSigning` purpose [[RFC 5280 section 4.2.1.12](https://tools.ietf.org/html/rfc5280#section-4.2.1.12)].</span></span> <span data-ttu-id="69386-121">또한 인증서에는 RSA 공개 키 길이가 2048 비트 이상 이어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="69386-121">Additionally, the certificate must have an RSA public key length of 2048 bits or higher.</span></span>

## <a name="timestamp-requirements"></a><span data-ttu-id="69386-122">타임 스탬프 요구 사항</span><span class="sxs-lookup"><span data-stu-id="69386-122">Timestamp requirements</span></span>

<span data-ttu-id="69386-123">서명 된 패키지에는 서명 인증서의 유효 기간을 초과 하 여 서명 유효성을 보장 하기 위해 RFC 3161 타임 스탬프가 포함 되어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="69386-123">Signed packages should include an RFC 3161 timestamp to ensure signature validity beyond the package signing certificate's validity period.</span></span> <span data-ttu-id="69386-124">타임 스탬프에 서명 하는 데 사용 되는 인증서는 `id-kp-timeStamping` 용도 [[RFC 5280 section 4.2.1.12](https://tools.ietf.org/html/rfc5280#section-4.2.1.12)]에 대해 유효 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="69386-124">The certificate used to sign the timestamp must be valid for the `id-kp-timeStamping` purpose [[RFC 5280 section 4.2.1.12](https://tools.ietf.org/html/rfc5280#section-4.2.1.12)].</span></span> <span data-ttu-id="69386-125">또한 인증서에는 RSA 공개 키 길이가 2048 비트 이상 이어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="69386-125">Additionally, the certificate must have an RSA public key length of 2048 bits or higher.</span></span>

<span data-ttu-id="69386-126">추가 기술 세부 정보는 [패키지 서명 기술 사양](https://github.com/NuGet/Home/wiki/Package-Signatures-Technical-Details) (GitHub)에서 찾을 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="69386-126">Additional technical details can be found in the [package signature technical specs](https://github.com/NuGet/Home/wiki/Package-Signatures-Technical-Details) (GitHub).</span></span>

## <a name="signature-requirements-on-nugetorg"></a><span data-ttu-id="69386-127">NuGet.org의 서명 요구 사항</span><span class="sxs-lookup"><span data-stu-id="69386-127">Signature requirements on NuGet.org</span></span>

<span data-ttu-id="69386-128">nuget.org에는 서명 된 패키지를 수락 하기 위한 추가 요구 사항이 있습니다.</span><span class="sxs-lookup"><span data-stu-id="69386-128">nuget.org has additional requirements for accepting a signed package:</span></span>

- <span data-ttu-id="69386-129">기본 서명은 작성자 서명 이어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="69386-129">The primary signature must be an author signature.</span></span>
- <span data-ttu-id="69386-130">기본 서명에 유효한 타임 스탬프가 하나 있어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="69386-130">The primary signature must have a single valid timestamp.</span></span>
- <span data-ttu-id="69386-131">작성자 서명 및 해당 타임 스탬프 시그니처의 x.509 인증서입니다.</span><span class="sxs-lookup"><span data-stu-id="69386-131">The X.509 certificates for both the author signature and its timestamp signature:</span></span>
  - <span data-ttu-id="69386-132">RSA 공개 키 2048 비트 이상 이어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="69386-132">Must have an RSA public key 2048 bits or greater.</span></span>
  - <span data-ttu-id="69386-133">Nuget.org에 대 한 패키지 유효성 검사 시 현재 UTC 시간 당 유효 기간 내에 있어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="69386-133">Must be within its validity period per current UTC time at time of package validation on nuget.org.</span></span>
  - <span data-ttu-id="69386-134">Windows에서 기본적으로 신뢰 되는 신뢰할 수 있는 루트 인증 기관에 연결 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="69386-134">Must chain to a trusted root authority that is trusted by default on Windows.</span></span> <span data-ttu-id="69386-135">자체 발급 된 인증서로 서명 된 패키지는 거부 됩니다.</span><span class="sxs-lookup"><span data-stu-id="69386-135">Packages signed with self-issued certificates are rejected.</span></span>
  - <span data-ttu-id="69386-136">은 (는) 용도에 맞게 유효 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="69386-136">Must be valid for its purpose:</span></span> 
    - <span data-ttu-id="69386-137">작성자 서명 인증서가 코드 서명에 유효 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="69386-137">The author signing certificate must be valid for code signing.</span></span>
    - <span data-ttu-id="69386-138">타임 스탬프 인증서는 타임 스탬프에 유효 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="69386-138">The timestamp certificate must be valid for timestamping.</span></span>
  - <span data-ttu-id="69386-139">서명 시 해지 해서는 안 됩니다.</span><span class="sxs-lookup"><span data-stu-id="69386-139">Must not be revoked at signing time.</span></span> <span data-ttu-id="69386-140">(이는 제출 시 knowable 되지 않을 수 있으므로 nuget.org는 주기적으로 해지 상태를 재확인 합니다.)</span><span class="sxs-lookup"><span data-stu-id="69386-140">(This may not be knowable at submission time, so nuget.org periodically rechecks revocation status).</span></span>
  
  
## <a name="related-articles"></a><span data-ttu-id="69386-141">관련된 문서</span><span class="sxs-lookup"><span data-stu-id="69386-141">Related articles</span></span>

- [<span data-ttu-id="69386-142">NuGet 패키지 서명</span><span class="sxs-lookup"><span data-stu-id="69386-142">Signing NuGet Packages</span></span>](../create-packages/Sign-a-Package.md)
- [<span data-ttu-id="69386-143">Dotnet CLI를 사용 하 여 서명 된 패키지 확인</span><span class="sxs-lookup"><span data-stu-id="69386-143">Verify signed packages using the dotnet CLI</span></span>](/dotnet/core/tools/dotnet-nuget-verify)
- [<span data-ttu-id="69386-144">nuget.exe를 사용 하 여 서명 된 패키지 확인 </span><span class="sxs-lookup"><span data-stu-id="69386-144">Verify signed packages using nuget.exe</span></span>](../reference/cli-reference/cli-ref-verify.md)
- [<span data-ttu-id="69386-145">패키지 트러스트 영역 관리</span><span class="sxs-lookup"><span data-stu-id="69386-145">Manage package trust boundaries</span></span>](../consume-packages/installing-signed-packages.md)
