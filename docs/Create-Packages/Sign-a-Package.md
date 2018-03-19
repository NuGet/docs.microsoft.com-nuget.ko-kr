---
title: "NuGet 패키지 서명 | Microsoft Docs"
author: rido-min
ms.author: rido-min
manager: unniravindranathan
ms.date: 03/06/2018
ms.topic: article
ms.prod: nuget
ms.technology: 
description: "서명된 패키지를 사용하여 콘텐츠 무결성 검사를 활성화하는 방법을 설명합니다."
keywords: "NuGet 패키지 서명, NuGet 보안, 서명된 패키지 만들기"
ms.reviewer:
- karann-msft
- anangaur
ms.openlocfilehash: aaf6ab7d7a9e66d4d9519d8aa79f0d0fac646d3a
ms.sourcegitcommit: 74c21b406302288c158e8ae26057132b12960be8
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 03/15/2018
---
# <a name="signing-nuget-packages"></a><span data-ttu-id="049ba-104">NuGet 패키지 서명</span><span class="sxs-lookup"><span data-stu-id="049ba-104">Signing NuGet Packages</span></span>

<span data-ttu-id="049ba-105">패키지 서명은 패키지가 생성된 후 수정되지 않았는지 확인하는 프로세스입니다.</span><span class="sxs-lookup"><span data-stu-id="049ba-105">Signing a package is a process that makes sure the package has not been modified since its creation.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="049ba-106">전제 조건</span><span class="sxs-lookup"><span data-stu-id="049ba-106">Prerequisites</span></span>

1. <span data-ttu-id="049ba-107">서명할 패키지(`.nupkg` 파일)입니다.</span><span class="sxs-lookup"><span data-stu-id="049ba-107">The package (a `.nupkg` file) to sign.</span></span> <span data-ttu-id="049ba-108">[패키지 만들기](creating-a-package.md)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="049ba-108">See [Creating a package](creating-a-package.md).</span></span>

1. <span data-ttu-id="049ba-109">nuget.exe 4.6.0 이상.</span><span class="sxs-lookup"><span data-stu-id="049ba-109">nuget.exe 4.6.0 or later.</span></span> <span data-ttu-id="049ba-110">[NuGet CLI 설치](../install-nuget-client-tools.md#nugetexe-cli) 방법을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="049ba-110">See how to [Install NuGet CLI](../install-nuget-client-tools.md#nugetexe-cli).</span></span>

1. <span data-ttu-id="049ba-111">[코드 서명 인증서](../reference/signed-packages-reference.md#get-a-code-signing-certificate).</span><span class="sxs-lookup"><span data-stu-id="049ba-111">[A code signing certificate](../reference/signed-packages-reference.md#get-a-code-signing-certificate).</span></span>

> [!Warning]
> <span data-ttu-id="049ba-112">nuget.org는 현재 서명된 패키지를 받아들이지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="049ba-112">nuget.org does not currently accept signed packages.</span></span> <span data-ttu-id="049ba-113">사용자 지정 피드에 게시할 패키지에 서명할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="049ba-113">You can sign packages for publishing to custom feeds.</span></span>

## <a name="sign-a-package"></a><span data-ttu-id="049ba-114">패키지 서명</span><span class="sxs-lookup"><span data-stu-id="049ba-114">Sign a package</span></span>

<span data-ttu-id="049ba-115">패키지에 서명하려면 [nuget 기호](../tools/cli-ref-sign.md)를 사용하세요.</span><span class="sxs-lookup"><span data-stu-id="049ba-115">To sign a package, use [nuget sign](../tools/cli-ref-sign.md):</span></span>

```cli
nuget sign MyPackage.nupkg -CertificateSubjectName <MyCertSubjectName> -Timestamper <TimestampServiceURL>
```

<span data-ttu-id="049ba-116">명령 참조에서 설명한 것처럼 인증서 저장소에 있는 인증서나 파일의 인증서를 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="049ba-116">As described in the command reference, you can use a certificate available in the certificate store or use a certificate from a file.</span></span>

### <a name="common-problems-when-signing-a-package"></a><span data-ttu-id="049ba-117">패키지에 서명 시 발생하는 일반적인 문제</span><span class="sxs-lookup"><span data-stu-id="049ba-117">Common problems when signing a package</span></span>

- <span data-ttu-id="049ba-118">인증서가 코드 서명에 적합하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="049ba-118">The certificate is not valid for code signing.</span></span> <span data-ttu-id="049ba-119">지정된 인증서에 적절한 확장 키 사용(EKU 1.3.6.1.5.5.7.3.3)이 있어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="049ba-119">You must ensure the certificate specified has the appropriate extended key usage (EKU 1.3.6.1.5.5.7.3.3).</span></span>
- <span data-ttu-id="049ba-120">인증서가 RSA SHA-256 서명 알고리즘 또는 공개 키 2048비트 이상과 같은 기본 요구 사항을 충족하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="049ba-120">The certificate does not satisfy the basic requirements such as the RSA SHA-256 signature algorithm or a public key 2048 bits or greater.</span></span>
- <span data-ttu-id="049ba-121">인증서가 만료 또는 해지되었습니다.</span><span class="sxs-lookup"><span data-stu-id="049ba-121">The certificate has expired or has been revoked.</span></span>
- <span data-ttu-id="049ba-122">타임스탬프 서버가 인증서 요구 사항을 충족하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="049ba-122">The timestamp server does not satisfy the certificate requirements.</span></span>

> [!Note]
> <span data-ttu-id="049ba-123">서명 인증서가 만료된 경우 서명된 패키지에 서명이 유효하다는 것을 확인해 주는 타임스탬프가 포함되어 있어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="049ba-123">Signed packages should include a timestamp to make sure the signature remains valid when the signing certificate has expired.</span></span> <span data-ttu-id="049ba-124">타임스탬프 없이 서명할 경우 서명 작업 시 [경고 NU3002](../reference/Errors-and-Warnings.md#nu3002)가 발생합니다.</span><span class="sxs-lookup"><span data-stu-id="049ba-124">The sign operation produce a [warning NU3002](../reference/Errors-and-Warnings.md#nu3002) when signing without a timestamp.</span></span>

## <a name="verify-a-signed-package"></a><span data-ttu-id="049ba-125">서명된 패키지 확인</span><span class="sxs-lookup"><span data-stu-id="049ba-125">Verify a signed package</span></span>

<span data-ttu-id="049ba-126">특정 패키지의 서명 정보를 확인하려면 [nuget verify](../tools/cli-ref-verify.md)를 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="049ba-126">Use [nuget verify](../tools/cli-ref-verify.md) to see the signature details of a given package:</span></span>

```cli
nuget verify -signature MyPackage.nupkg
```

## <a name="install-a-signed-package"></a><span data-ttu-id="049ba-127">서명된 패키지 설치</span><span class="sxs-lookup"><span data-stu-id="049ba-127">Install a signed package</span></span>

<span data-ttu-id="049ba-128">서명된 패키지는 특별한 조치 없이 설치할 수 있지만 패키지가 서명된 이후에 내용이 수정된 경우 설치가 차단되고 [오류 NU3008](../reference/Errors-and-Warnings.md#nu3008)이 발생합니다.</span><span class="sxs-lookup"><span data-stu-id="049ba-128">Signed packages don't require any specific action to be installed; however, if the content has been modified since it was signed, the installation be blocked and produces a [error NU3008](../reference/Errors-and-Warnings.md#nu3008).</span></span>

> [!Warning]
> <span data-ttu-id="049ba-129">신뢰할 수 없는 인증서로 서명된 패키지는 서명되지 않은 것으로 간주되고, 다른 서명되지 않은 패키지처럼 경고나 오류 없이 설치됩니다.</span><span class="sxs-lookup"><span data-stu-id="049ba-129">Packages signed with untrusted certificates are considered as unsigned and are installed without any warnings or errors like any other unsigned package.</span></span>

## <a name="see-also"></a><span data-ttu-id="049ba-130">참고 항목</span><span class="sxs-lookup"><span data-stu-id="049ba-130">See also</span></span>

[<span data-ttu-id="049ba-131">서명된 패키지 참조</span><span class="sxs-lookup"><span data-stu-id="049ba-131">Signed Packages Reference</span></span>](../reference/Signed-Packages-Reference.md)
