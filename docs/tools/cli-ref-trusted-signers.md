---
title: NuGet CLI 신뢰할 수 있는 서명자 명령
description: Nuget.exe 신뢰할 수 있는 서명자 명령에 대 한 참조
author: patbel
ms.author: patbel
ms.date: 11/12/2018
ms.topic: reference
ms.reviewer: rmpablos
ms.openlocfilehash: c22c7f0a6b6878bec4f8396e02e2d97998170455
ms.sourcegitcommit: b6810860b77b2d50aab031040b047c20a333aca3
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 06/28/2019
ms.locfileid: "67425977"
---
# <a name="trusted-signers-command-nuget-cli"></a><span data-ttu-id="46684-103">신뢰할 수 있는 서명자 명령 (NuGet CLI)</span><span class="sxs-lookup"><span data-stu-id="46684-103">trusted-signers command (NuGet CLI)</span></span>

<span data-ttu-id="46684-104">**적용 대상:** 소비 패키지 &bullet; **지원 되는 버전:** 4.9.1+</span><span class="sxs-lookup"><span data-stu-id="46684-104">**Applies to:** package consumption &bullet; **Supported versions:** 4.9.1+</span></span>

<span data-ttu-id="46684-105">NuGet 구성에 신뢰할 수 있는 서명자를 가져오거나 설정 합니다.</span><span class="sxs-lookup"><span data-stu-id="46684-105">Gets or sets trusted signers to the NuGet configuration.</span></span> <span data-ttu-id="46684-106">추가 사용량에 대 한 참조 [일반적인 NuGet 구성](../consume-packages/configuring-nuget-behavior.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="46684-106">For additional usage, see [Common NuGet configurations](../consume-packages/configuring-nuget-behavior.md).</span></span> <span data-ttu-id="46684-107">Nuget.config 스키마에서 참조 하는 등을 표시 하는 방법에 대 한 내용은 합니다 [NuGet 구성 파일 참조](../reference/nuget-config-file.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="46684-107">For details on how the nuget.config schema looks like, refer to the [NuGet config file reference](../reference/nuget-config-file.md).</span></span>

## <a name="usage"></a><span data-ttu-id="46684-108">사용법</span><span class="sxs-lookup"><span data-stu-id="46684-108">Usage</span></span>

```cli
nuget trusted-signers <list|add|remove|sync> [options]
```

<span data-ttu-id="46684-109">없으면 `list|add|remove|sync` 지정 된 경우이 명령은 기본적으로 `list`입니다.</span><span class="sxs-lookup"><span data-stu-id="46684-109">if none of `list|add|remove|sync` is specified, the command will default to `list`.</span></span>

## <a name="nuget-trusted-signers-list"></a><span data-ttu-id="46684-110">nuget 신뢰할 수 있는 서명자 목록</span><span class="sxs-lookup"><span data-stu-id="46684-110">nuget trusted-signers list</span></span>

<span data-ttu-id="46684-111">구성에 대 한 모든 신뢰할 수 있는 서명자를 나열합니다.</span><span class="sxs-lookup"><span data-stu-id="46684-111">Lists all the trusted signers in the configuration.</span></span> <span data-ttu-id="46684-112">이 옵션에는 모든 인증서 포함 됩니다 (지문 및 지문 알고리즘) 각 서명자 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="46684-112">This option will include all the certificates (with fingerprint and fingerprint algorithm) each signer has.</span></span> <span data-ttu-id="46684-113">인증서를 앞에 있으면 `[U]`, 인증서 항목에는 의미 `allowUntrustedRoot` 로 `true`합니다.</span><span class="sxs-lookup"><span data-stu-id="46684-113">If a certificate has a preceding `[U]`, it means that certificate entry has `allowUntrustedRoot` set as `true`.</span></span>

<span data-ttu-id="46684-114">다음은이 명령의 예제 출력:</span><span class="sxs-lookup"><span data-stu-id="46684-114">Below is an example output from this command:</span></span>

```cli
$ nuget trusted-signers
Registered trusted signers:


 1.   nuget.org [repository]
      Service Index: https://api.nuget.org/v3/index.json
      Certificate fingerprint(s):
        SHA256 - 0E5F38F57DC1BCC806D8494F4F90FBCEDD988B46760709CBEEC6F4219AA6157D

 2.   microsoft [author]
      Certificate fingerprint(s):
        SHA256 - 3F9001EA83C560D712C24CF213C3D312CB3BFF51EE89435D3430BD06B5D0EECE

 3.   myUntrustedAuthorSignature [author]
      Certificate fingerprint(s):
        [U] SHA256 - 518F9CF082C0872025EFB2587B6A6AB198208F63EA58DD54D2B9FF6735CA4434
        
```

## <a name="nuget-trusted-signers-add-options"></a><span data-ttu-id="46684-115">nuget trusted-signers add [options]</span><span class="sxs-lookup"><span data-stu-id="46684-115">nuget trusted-signers add [options]</span></span>

<span data-ttu-id="46684-116">구성에 지정 된 이름의 신뢰할 수 있는 서명자를 추가합니다. 이 옵션은 신뢰할 수 있는 작성자 또는 리포지토리를 추가 하려면 다른 제스처입니다.</span><span class="sxs-lookup"><span data-stu-id="46684-116">Adds a trusted signer with the given name to the config. This option has different gestures to add a trusted author or repository.</span></span>

## <a name="options-for-add-based-on-a-package"></a><span data-ttu-id="46684-117">패키지를 기반으로 하는 추가 옵션</span><span class="sxs-lookup"><span data-stu-id="46684-117">Options for add based on a package</span></span>

```cli
nuget trusted-signers add <package(s)> -Name <name> [options]
```

<span data-ttu-id="46684-118">여기서 `<package(s)>` 는 하나 이상의 `.nupkg` 파일입니다.</span><span class="sxs-lookup"><span data-stu-id="46684-118">where `<package(s)>` is one or more `.nupkg` files.</span></span>

| <span data-ttu-id="46684-119">옵션</span><span class="sxs-lookup"><span data-stu-id="46684-119">Option</span></span> | <span data-ttu-id="46684-120">설명</span><span class="sxs-lookup"><span data-stu-id="46684-120">Description</span></span> |
| --- | --- |
| <span data-ttu-id="46684-121">만든 이</span><span class="sxs-lookup"><span data-stu-id="46684-121">Author</span></span> | <span data-ttu-id="46684-122">패키지의 작성자 서명의 신뢰할 수 있음을 지정 합니다.</span><span class="sxs-lookup"><span data-stu-id="46684-122">Specifies that the author signature of the package(s) should be trusted.</span></span> |
| <span data-ttu-id="46684-123">리포지토리</span><span class="sxs-lookup"><span data-stu-id="46684-123">Repository</span></span> | <span data-ttu-id="46684-124">리포지토리 서명 하거나 연대 서명 된 패키지의을 신뢰할 수 있음을 지정 합니다.</span><span class="sxs-lookup"><span data-stu-id="46684-124">Specifies that the repository signature or countersignature of the package(s) should be trusted.</span></span> |
| <span data-ttu-id="46684-125">AllowUntrustedRoot</span><span class="sxs-lookup"><span data-stu-id="46684-125">AllowUntrustedRoot</span></span> | <span data-ttu-id="46684-126">신뢰할 수 있는 서명자 인증서 신뢰할 수 없는 루트에 연결할 수 있어야 하는 경우를 지정 합니다.</span><span class="sxs-lookup"><span data-stu-id="46684-126">Specifies if the certificate for the trusted signer should be allowed to chain to an untrusted root.</span></span> |
| <span data-ttu-id="46684-127">Owners</span><span class="sxs-lookup"><span data-stu-id="46684-127">Owners</span></span> | <span data-ttu-id="46684-128">저장소의 신뢰를 더욱 제한 하려면 신뢰할 수 있는 소유자의 세미콜론으로 구분 된 목록입니다.</span><span class="sxs-lookup"><span data-stu-id="46684-128">Semi-colon separated list of trusted owners to further restrict the trust of a repository.</span></span> <span data-ttu-id="46684-129">사용 하는 경우에 유효 합니다 `-Repository` 옵션입니다.</span><span class="sxs-lookup"><span data-stu-id="46684-129">Only valid when using the `-Repository` option.</span></span> |

<span data-ttu-id="46684-130">둘 다 제공할 `-Author` 고 `-Repository` 동시에 지원 되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="46684-130">Providing both `-Author` and `-Repository` at the same time is not supported.</span></span>

## <a name="options-for-add-based-on-a-service-index"></a><span data-ttu-id="46684-131">서비스 인덱스를 기준으로 하는 추가 옵션</span><span class="sxs-lookup"><span data-stu-id="46684-131">Options for add based on a service index</span></span>

```cli
nuget trusted-signers add -Name <name> [options]
```

<span data-ttu-id="46684-132">_참고_: 이 옵션에서 신뢰할 수 있는 리포지토리를 추가 합니다.</span><span class="sxs-lookup"><span data-stu-id="46684-132">_Note_: This option will only add trusted repositories.</span></span> 

| <span data-ttu-id="46684-133">옵션</span><span class="sxs-lookup"><span data-stu-id="46684-133">Option</span></span> | <span data-ttu-id="46684-134">설명</span><span class="sxs-lookup"><span data-stu-id="46684-134">Description</span></span> |
| --- | --- |
| <span data-ttu-id="46684-135">ServiceIndex</span><span class="sxs-lookup"><span data-stu-id="46684-135">ServiceIndex</span></span> | <span data-ttu-id="46684-136">신뢰할 수 있는 리포지토리의 V3 서비스 인덱스를 지정 합니다.</span><span class="sxs-lookup"><span data-stu-id="46684-136">Specifies the V3 service index of the repository to be trusted.</span></span> <span data-ttu-id="46684-137">이 리포지토리는 리포지토리 서명을 리소스를 지원 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="46684-137">This repository has to support the repository signatures resource.</span></span> <span data-ttu-id="46684-138">같은 패키지 원본에 대해 명령이 표시 됩니다 제공 되지 않으면 `-Name` 및 여기에서 서비스 인덱스를 가져옵니다.</span><span class="sxs-lookup"><span data-stu-id="46684-138">If not provided, the command will look for a package source with the same `-Name` and get the service index from there.</span></span> |
| <span data-ttu-id="46684-139">AllowUntrustedRoot</span><span class="sxs-lookup"><span data-stu-id="46684-139">AllowUntrustedRoot</span></span> | <span data-ttu-id="46684-140">신뢰할 수 있는 서명자 인증서 신뢰할 수 없는 루트에 연결할 수 있어야 하는 경우를 지정 합니다.</span><span class="sxs-lookup"><span data-stu-id="46684-140">Specifies if the certificate for the trusted signer should be allowed to chain to an untrusted root.</span></span> |
| <span data-ttu-id="46684-141">Owners</span><span class="sxs-lookup"><span data-stu-id="46684-141">Owners</span></span> | <span data-ttu-id="46684-142">저장소의 신뢰를 더욱 제한 하려면 신뢰할 수 있는 소유자의 세미콜론으로 구분 된 목록입니다.</span><span class="sxs-lookup"><span data-stu-id="46684-142">Semi-colon separated list of trusted owners to further restrict the trust of a repository.</span></span> |

## <a name="options-for-add-based-on-the-certificate-information"></a><span data-ttu-id="46684-143">인증서 정보를 기반으로 하는 추가 옵션</span><span class="sxs-lookup"><span data-stu-id="46684-143">Options for add based on the certificate information</span></span>

```cli
nuget trusted-signers add -Name <name> [options]
```

<span data-ttu-id="46684-144">_참고_: 지정 된 이름의 신뢰할 수 있는 서명자가 이미 있는 경우 인증서 항목은 서명자에 추가 됩니다.</span><span class="sxs-lookup"><span data-stu-id="46684-144">_Note_: If a trusted signer with the given name already exists, the certificate item will be added to that signer.</span></span> <span data-ttu-id="46684-145">그렇지 않으면 신뢰할 수 있는 작성자 만들어집니다 인증서 항목을 사용 하 여에서 인증서 정보를 제공 합니다.</span><span class="sxs-lookup"><span data-stu-id="46684-145">Otherwise a trusted author will be created with a certificate item from given certificate information.</span></span>

| <span data-ttu-id="46684-146">옵션</span><span class="sxs-lookup"><span data-stu-id="46684-146">Option</span></span> | <span data-ttu-id="46684-147">설명</span><span class="sxs-lookup"><span data-stu-id="46684-147">Description</span></span> |
| --- | --- |
| <span data-ttu-id="46684-148">CertificateFingerprint</span><span class="sxs-lookup"><span data-stu-id="46684-148">CertificateFingerprint</span></span> | <span data-ttu-id="46684-149">서명 된 패키지는 인증서의 지문을 사용 하 여 서명 해야 하는 인증서를 지정 합니다.</span><span class="sxs-lookup"><span data-stu-id="46684-149">Specifies a certificate fingerprints of a certificate which signed packages must be signed with.</span></span> <span data-ttu-id="46684-150">인증서 지문은 인증서의 해시입니다.</span><span class="sxs-lookup"><span data-stu-id="46684-150">A certificate fingerprint is a hash of the certificate.</span></span> <span data-ttu-id="46684-151">이 해시 해야 계산에 사용 된 해시 알고리즘의 지정 된 `FingerprintAlgorithm` 옵션입니다.</span><span class="sxs-lookup"><span data-stu-id="46684-151">The hash algorithm used for calculating this hash should be specifies in the `FingerprintAlgorithm` option.</span></span> |
| <span data-ttu-id="46684-152">FingerprintAlgorithm</span><span class="sxs-lookup"><span data-stu-id="46684-152">FingerprintAlgorithm</span></span> | <span data-ttu-id="46684-153">인증서 지문을 계산 하는 데 해시 알고리즘을 지정 합니다.</span><span class="sxs-lookup"><span data-stu-id="46684-153">Specifies the hash algorithm used to calculate the certificate fingerprint.</span></span> <span data-ttu-id="46684-154">기본값은 `SHA256`입니다.</span><span class="sxs-lookup"><span data-stu-id="46684-154">Defaults to `SHA256`.</span></span> <span data-ttu-id="46684-155">값이 지원 됨 `SHA256`, `SHA384` 및 `SHA512`</span><span class="sxs-lookup"><span data-stu-id="46684-155">Values supported are `SHA256`, `SHA384` and `SHA512`</span></span> |
| <span data-ttu-id="46684-156">AllowUntrustedRoot</span><span class="sxs-lookup"><span data-stu-id="46684-156">AllowUntrustedRoot</span></span> | <span data-ttu-id="46684-157">신뢰할 수 있는 서명자 인증서 신뢰할 수 없는 루트에 연결할 수 있어야 하는 경우를 지정 합니다.</span><span class="sxs-lookup"><span data-stu-id="46684-157">Specifies if the certificate for the trusted signer should be allowed to chain to an untrusted root.</span></span> |

## <a name="nuget-trusted-signers-remove--name-name"></a><span data-ttu-id="46684-158">nuget 신뢰할 수 있는 서명자 이름을 제거 <name></span><span class="sxs-lookup"><span data-stu-id="46684-158">nuget trusted-signers remove -Name <name></span></span>

<span data-ttu-id="46684-159">지정 된 이름과 일치 하는 모든 신뢰할 수 있는 서명자를 제거 합니다.</span><span class="sxs-lookup"><span data-stu-id="46684-159">Removes any trusted signers that match the given name.</span></span>

## <a name="nuget-trusted-signers-sync--name-name"></a><span data-ttu-id="46684-160">nuget trusted-signers sync -Name <name></span><span class="sxs-lookup"><span data-stu-id="46684-160">nuget trusted-signers sync -Name <name></span></span>

<span data-ttu-id="46684-161">최신 목록을 업데이트 하려면 현재 신뢰할 수 있는 저장소에 사용 되는 인증서 요청을 신뢰할 수 있는 서명자의 기존 인증서 목록입니다.</span><span class="sxs-lookup"><span data-stu-id="46684-161">Requests the latest list of certificates used in a currently trusted repository to update the the existing certificate list in the trusted signer.</span></span>

<span data-ttu-id="46684-162">_참고_: 이 제스처는 인증서의 현재 목록을 삭제 하 고 리포지토리에서 최신 목록을 바꿉니다.</span><span class="sxs-lookup"><span data-stu-id="46684-162">_Note_: This gesture will delete the current list of certificates and replace them with an up-to-date list from the repository.</span></span>

## <a name="options"></a><span data-ttu-id="46684-163">옵션</span><span class="sxs-lookup"><span data-stu-id="46684-163">Options</span></span>

| <span data-ttu-id="46684-164">옵션</span><span class="sxs-lookup"><span data-stu-id="46684-164">Option</span></span> | <span data-ttu-id="46684-165">설명</span><span class="sxs-lookup"><span data-stu-id="46684-165">Description</span></span> |
| --- | --- |
| <span data-ttu-id="46684-166">ConfigFile</span><span class="sxs-lookup"><span data-stu-id="46684-166">ConfigFile</span></span> | <span data-ttu-id="46684-167">적용할 NuGet 설정 파일입니다.</span><span class="sxs-lookup"><span data-stu-id="46684-167">The NuGet configuration file to apply.</span></span> <span data-ttu-id="46684-168">지정하지 않으면 기본적으로 Windows에서는 `%AppData%\NuGet\NuGet.Config`, Mac이나 Linux에서는 `~/.nuget/NuGet/NuGet.Config`가 사용됩니다.</span><span class="sxs-lookup"><span data-stu-id="46684-168">If not specified, `%AppData%\NuGet\NuGet.Config` (Windows) or `~/.nuget/NuGet/NuGet.Config` (Mac/Linux) is used.</span></span>|
| <span data-ttu-id="46684-169">ForceEnglishOutput</span><span class="sxs-lookup"><span data-stu-id="46684-169">ForceEnglishOutput</span></span> | <span data-ttu-id="46684-170">고정 영어 기반 문화권을 사용 하 여 실행할 nuget.exe를 강제로 수행 합니다.</span><span class="sxs-lookup"><span data-stu-id="46684-170">Forces nuget.exe to run using an invariant, English-based culture.</span></span> |
| <span data-ttu-id="46684-171">Help</span><span class="sxs-lookup"><span data-stu-id="46684-171">Help</span></span> | <span data-ttu-id="46684-172">명령어에 대한 도움말을 표시합니다.</span><span class="sxs-lookup"><span data-stu-id="46684-172">Displays help information for the command.</span></span> |
| <span data-ttu-id="46684-173">Verbosity</span><span class="sxs-lookup"><span data-stu-id="46684-173">Verbosity</span></span> | <span data-ttu-id="46684-174">출력에 표시되는 세부정보의 양을 지정합니다: *정상적인*, *조용한*, *자세한*합니다.</span><span class="sxs-lookup"><span data-stu-id="46684-174">Specifies the amount of detail displayed in the output: *normal*, *quiet*, *detailed*.</span></span> |

## <a name="examples"></a><span data-ttu-id="46684-175">예제</span><span class="sxs-lookup"><span data-stu-id="46684-175">Examples</span></span>

```cli
nuget trusted-signers list

nuget trusted-signers Add -Name existingSource

nuget trusted-signers Add -Name trustedRepo -ServiceIndex https://trustedRepo.test/v3ServiceIndex

nuget trusted-signers Add -Name author1 -CertificateFingerprint CE40881FF5F0AD3E58965DA20A9F571EF1651A56933748E1BF1C99E537C4E039 -FingerprintAlgorithm SHA256

nuget trusted-signers Add -Repository .\..\MyRepositorySignedPackage.nupkg -Name TrustedRepo

nuget-trusted-signers Remove -Name TrustedRepo

nuget-trusted-signers Sync -Name TrustedRepo
```
