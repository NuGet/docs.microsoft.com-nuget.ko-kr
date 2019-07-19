---
title: NuGet CLI 신뢰-서명자 명령
description: Nuget.exe trusted-서명자 명령에 대 한 참조
author: patbel
ms.author: patbel
ms.date: 11/12/2018
ms.topic: reference
ms.reviewer: rmpablos
ms.openlocfilehash: 197f2eaeed1a4a11f0f3ed426534807a0136271e
ms.sourcegitcommit: efc18d484fdf0c7a8979b564dcb191c030601bb4
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/18/2019
ms.locfileid: "68327540"
---
# <a name="trusted-signers-command-nuget-cli"></a><span data-ttu-id="da895-103">trusted-서명자 명령 (NuGet CLI)</span><span class="sxs-lookup"><span data-stu-id="da895-103">trusted-signers command (NuGet CLI)</span></span>

<span data-ttu-id="da895-104">**적용 대상:** 패키지 &bullet; 사용 **지원 버전:** 4.9.1+</span><span class="sxs-lookup"><span data-stu-id="da895-104">**Applies to:** package consumption &bullet; **Supported versions:** 4.9.1+</span></span>

<span data-ttu-id="da895-105">NuGet 구성에 대해 신뢰할 수 있는 서명자를 가져오거나 설정 합니다.</span><span class="sxs-lookup"><span data-stu-id="da895-105">Gets or sets trusted signers to the NuGet configuration.</span></span> <span data-ttu-id="da895-106">추가 사용에 대해서는 [일반적인 NuGet 구성](../../consume-packages/configuring-nuget-behavior.md)을 참조 하세요.</span><span class="sxs-lookup"><span data-stu-id="da895-106">For additional usage, see [Common NuGet configurations](../../consume-packages/configuring-nuget-behavior.md).</span></span> <span data-ttu-id="da895-107">Nuget 스키마의 모양에 대 한 자세한 내용은 [nuget 구성 파일 참조](../nuget-config-file.md)를 참조 하세요.</span><span class="sxs-lookup"><span data-stu-id="da895-107">For details on how the nuget.config schema looks like, refer to the [NuGet config file reference](../nuget-config-file.md).</span></span>

## <a name="usage"></a><span data-ttu-id="da895-108">사용법</span><span class="sxs-lookup"><span data-stu-id="da895-108">Usage</span></span>

```cli
nuget trusted-signers <list|add|remove|sync> [options]
```

<span data-ttu-id="da895-109">을 지정 하지 않으면 명령은 기본적으로로 `list`지정 됩니다. `list|add|remove|sync`</span><span class="sxs-lookup"><span data-stu-id="da895-109">if none of `list|add|remove|sync` is specified, the command will default to `list`.</span></span>

## <a name="nuget-trusted-signers-list"></a><span data-ttu-id="da895-110">nuget 신뢰할 수 있는 서명자 목록</span><span class="sxs-lookup"><span data-stu-id="da895-110">nuget trusted-signers list</span></span>

<span data-ttu-id="da895-111">구성의 모든 신뢰할 수 있는 서명자를 나열 합니다.</span><span class="sxs-lookup"><span data-stu-id="da895-111">Lists all the trusted signers in the configuration.</span></span> <span data-ttu-id="da895-112">이 옵션에는 각 서명자가 있는 모든 인증서 (지문 및 지문 알고리즘 포함)가 포함 됩니다.</span><span class="sxs-lookup"><span data-stu-id="da895-112">This option will include all the certificates (with fingerprint and fingerprint algorithm) each signer has.</span></span> <span data-ttu-id="da895-113">인증서에 앞 `[U]`에가 있는 경우 인증서 항목이로 `true`설정 되어 `allowUntrustedRoot` 있음을 의미 합니다.</span><span class="sxs-lookup"><span data-stu-id="da895-113">If a certificate has a preceding `[U]`, it means that certificate entry has `allowUntrustedRoot` set as `true`.</span></span>

<span data-ttu-id="da895-114">다음은이 명령의 출력 예제입니다.</span><span class="sxs-lookup"><span data-stu-id="da895-114">Below is an example output from this command:</span></span>

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

## <a name="nuget-trusted-signers-add-options"></a><span data-ttu-id="da895-115">nuget trusted-signers add [options]</span><span class="sxs-lookup"><span data-stu-id="da895-115">nuget trusted-signers add [options]</span></span>

<span data-ttu-id="da895-116">지정 된 이름의 신뢰할 수 있는 서명자를 구성에 추가 합니다. 이 옵션은 신뢰할 수 있는 작성자 또는 리포지토리를 추가 하는 다른 제스처를 포함 합니다.</span><span class="sxs-lookup"><span data-stu-id="da895-116">Adds a trusted signer with the given name to the config. This option has different gestures to add a trusted author or repository.</span></span>

## <a name="options-for-add-based-on-a-package"></a><span data-ttu-id="da895-117">패키지 기반 추가 옵션</span><span class="sxs-lookup"><span data-stu-id="da895-117">Options for add based on a package</span></span>

```cli
nuget trusted-signers add <package(s)> -Name <name> [options]
```

<span data-ttu-id="da895-118">여기서 `<package(s)>` 는 하나 `.nupkg` 이상의 파일입니다.</span><span class="sxs-lookup"><span data-stu-id="da895-118">where `<package(s)>` is one or more `.nupkg` files.</span></span>

| <span data-ttu-id="da895-119">옵션</span><span class="sxs-lookup"><span data-stu-id="da895-119">Option</span></span> | <span data-ttu-id="da895-120">Description</span><span class="sxs-lookup"><span data-stu-id="da895-120">Description</span></span> |
| --- | --- |
| <span data-ttu-id="da895-121">작성자</span><span class="sxs-lookup"><span data-stu-id="da895-121">Author</span></span> | <span data-ttu-id="da895-122">패키지의 작성자 서명을 신뢰할 수 있도록 지정 합니다.</span><span class="sxs-lookup"><span data-stu-id="da895-122">Specifies that the author signature of the package(s) should be trusted.</span></span> |
| <span data-ttu-id="da895-123">리포지토리</span><span class="sxs-lookup"><span data-stu-id="da895-123">Repository</span></span> | <span data-ttu-id="da895-124">패키지의 저장소 서명 또는 연대 서명을 신뢰할 수 있도록 지정 합니다.</span><span class="sxs-lookup"><span data-stu-id="da895-124">Specifies that the repository signature or countersignature of the package(s) should be trusted.</span></span> |
| <span data-ttu-id="da895-125">AllowUntrustedRoot</span><span class="sxs-lookup"><span data-stu-id="da895-125">AllowUntrustedRoot</span></span> | <span data-ttu-id="da895-126">신뢰할 수 있는 서명자에 대 한 인증서를 신뢰할 수 없는 루트에 연결할 수 있는지 여부를 지정 합니다.</span><span class="sxs-lookup"><span data-stu-id="da895-126">Specifies if the certificate for the trusted signer should be allowed to chain to an untrusted root.</span></span> |
| <span data-ttu-id="da895-127">소유자</span><span class="sxs-lookup"><span data-stu-id="da895-127">Owners</span></span> | <span data-ttu-id="da895-128">리포지토리의 신뢰를 추가로 제한 하는 신뢰할 수 있는 소유자의 세미콜론으로 구분 된 목록입니다.</span><span class="sxs-lookup"><span data-stu-id="da895-128">Semi-colon separated list of trusted owners to further restrict the trust of a repository.</span></span> <span data-ttu-id="da895-129">옵션을 사용 하는 `-Repository` 경우에만 유효 합니다.</span><span class="sxs-lookup"><span data-stu-id="da895-129">Only valid when using the `-Repository` option.</span></span> |

<span data-ttu-id="da895-130">`-Author` 와`-Repository` 를 동시에 제공 하는 것은 지원 되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="da895-130">Providing both `-Author` and `-Repository` at the same time is not supported.</span></span>

## <a name="options-for-add-based-on-a-service-index"></a><span data-ttu-id="da895-131">서비스 인덱스를 기반으로 하는 추가 옵션</span><span class="sxs-lookup"><span data-stu-id="da895-131">Options for add based on a service index</span></span>

```cli
nuget trusted-signers add -Name <name> [options]
```

<span data-ttu-id="da895-132">_참고_: 이 옵션은 신뢰할 수 있는 리포지토리만 추가 합니다.</span><span class="sxs-lookup"><span data-stu-id="da895-132">_Note_: This option will only add trusted repositories.</span></span> 

| <span data-ttu-id="da895-133">옵션</span><span class="sxs-lookup"><span data-stu-id="da895-133">Option</span></span> | <span data-ttu-id="da895-134">설명</span><span class="sxs-lookup"><span data-stu-id="da895-134">Description</span></span> |
| --- | --- |
| <span data-ttu-id="da895-135">ServiceIndex</span><span class="sxs-lookup"><span data-stu-id="da895-135">ServiceIndex</span></span> | <span data-ttu-id="da895-136">신뢰할 리포지토리의 V3 서비스 인덱스를 지정 합니다.</span><span class="sxs-lookup"><span data-stu-id="da895-136">Specifies the V3 service index of the repository to be trusted.</span></span> <span data-ttu-id="da895-137">이 리포지토리는 리포지토리 서명 리소스를 지원 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="da895-137">This repository has to support the repository signatures resource.</span></span> <span data-ttu-id="da895-138">지정 하지 않으면 명령이 동일한 `-Name` 패키지 소스를 검색 하 여 해당 위치에서 서비스 인덱스를 가져옵니다.</span><span class="sxs-lookup"><span data-stu-id="da895-138">If not provided, the command will look for a package source with the same `-Name` and get the service index from there.</span></span> |
| <span data-ttu-id="da895-139">AllowUntrustedRoot</span><span class="sxs-lookup"><span data-stu-id="da895-139">AllowUntrustedRoot</span></span> | <span data-ttu-id="da895-140">신뢰할 수 있는 서명자에 대 한 인증서를 신뢰할 수 없는 루트에 연결할 수 있는지 여부를 지정 합니다.</span><span class="sxs-lookup"><span data-stu-id="da895-140">Specifies if the certificate for the trusted signer should be allowed to chain to an untrusted root.</span></span> |
| <span data-ttu-id="da895-141">소유자</span><span class="sxs-lookup"><span data-stu-id="da895-141">Owners</span></span> | <span data-ttu-id="da895-142">리포지토리의 신뢰를 추가로 제한 하는 신뢰할 수 있는 소유자의 세미콜론으로 구분 된 목록입니다.</span><span class="sxs-lookup"><span data-stu-id="da895-142">Semi-colon separated list of trusted owners to further restrict the trust of a repository.</span></span> |

## <a name="options-for-add-based-on-the-certificate-information"></a><span data-ttu-id="da895-143">인증서 정보에 따라 추가 옵션</span><span class="sxs-lookup"><span data-stu-id="da895-143">Options for add based on the certificate information</span></span>

```cli
nuget trusted-signers add -Name <name> [options]
```

<span data-ttu-id="da895-144">_참고_: 지정 된 이름의 신뢰할 수 있는 서명자가 이미 있는 경우 해당 서명자에 게 인증서 항목이 추가 됩니다.</span><span class="sxs-lookup"><span data-stu-id="da895-144">_Note_: If a trusted signer with the given name already exists, the certificate item will be added to that signer.</span></span> <span data-ttu-id="da895-145">그렇지 않으면 지정 된 인증서 정보에서 인증서 항목을 사용 하 여 신뢰할 수 있는 작성자가 만들어집니다.</span><span class="sxs-lookup"><span data-stu-id="da895-145">Otherwise a trusted author will be created with a certificate item from given certificate information.</span></span>

| <span data-ttu-id="da895-146">옵션</span><span class="sxs-lookup"><span data-stu-id="da895-146">Option</span></span> | <span data-ttu-id="da895-147">Description</span><span class="sxs-lookup"><span data-stu-id="da895-147">Description</span></span> |
| --- | --- |
| <span data-ttu-id="da895-148">CertificateFingerprint</span><span class="sxs-lookup"><span data-stu-id="da895-148">CertificateFingerprint</span></span> | <span data-ttu-id="da895-149">서명 된 패키지에 서명 해야 하는 인증서의 인증서 지문을 지정 합니다.</span><span class="sxs-lookup"><span data-stu-id="da895-149">Specifies a certificate fingerprints of a certificate which signed packages must be signed with.</span></span> <span data-ttu-id="da895-150">인증서 지문을 인증서의 해시입니다.</span><span class="sxs-lookup"><span data-stu-id="da895-150">A certificate fingerprint is a hash of the certificate.</span></span> <span data-ttu-id="da895-151">이 해시를 계산 하는 데 사용 되는 해시 알고리즘은 `FingerprintAlgorithm` 옵션에서 지정 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="da895-151">The hash algorithm used for calculating this hash should be specifies in the `FingerprintAlgorithm` option.</span></span> |
| <span data-ttu-id="da895-152">FingerprintAlgorithm</span><span class="sxs-lookup"><span data-stu-id="da895-152">FingerprintAlgorithm</span></span> | <span data-ttu-id="da895-153">인증서 지문을 계산 하는 데 사용 되는 해시 알고리즘을 지정 합니다.</span><span class="sxs-lookup"><span data-stu-id="da895-153">Specifies the hash algorithm used to calculate the certificate fingerprint.</span></span> <span data-ttu-id="da895-154">기본값은 `SHA256`입니다.</span><span class="sxs-lookup"><span data-stu-id="da895-154">Defaults to `SHA256`.</span></span> <span data-ttu-id="da895-155">지원 되는 `SHA256`값 `SHA384` 은, 및입니다.`SHA512`</span><span class="sxs-lookup"><span data-stu-id="da895-155">Values supported are `SHA256`, `SHA384` and `SHA512`</span></span> |
| <span data-ttu-id="da895-156">AllowUntrustedRoot</span><span class="sxs-lookup"><span data-stu-id="da895-156">AllowUntrustedRoot</span></span> | <span data-ttu-id="da895-157">신뢰할 수 있는 서명자에 대 한 인증서를 신뢰할 수 없는 루트에 연결할 수 있는지 여부를 지정 합니다.</span><span class="sxs-lookup"><span data-stu-id="da895-157">Specifies if the certificate for the trusted signer should be allowed to chain to an untrusted root.</span></span> |

## <a name="nuget-trusted-signers-remove--name-name"></a><span data-ttu-id="da895-158">nuget 신뢰할 수 있는 서명자 이름 제거<name></span><span class="sxs-lookup"><span data-stu-id="da895-158">nuget trusted-signers remove -Name <name></span></span>

<span data-ttu-id="da895-159">지정 된 이름과 일치 하는 모든 신뢰할 수 있는 서명자를 제거 합니다.</span><span class="sxs-lookup"><span data-stu-id="da895-159">Removes any trusted signers that match the given name.</span></span>

## <a name="nuget-trusted-signers-sync--name-name"></a><span data-ttu-id="da895-160">nuget 신뢰할 수 있는 서명자 동기화-이름<name></span><span class="sxs-lookup"><span data-stu-id="da895-160">nuget trusted-signers sync -Name <name></span></span>

<span data-ttu-id="da895-161">현재 신뢰할 수 있는 리포지토리에서 사용 되는 인증서의 최신 목록을 요청 하 여 신뢰할 수 있는 서명자의 기존 인증서 목록을 업데이트 합니다.</span><span class="sxs-lookup"><span data-stu-id="da895-161">Requests the latest list of certificates used in a currently trusted repository to update the the existing certificate list in the trusted signer.</span></span>

<span data-ttu-id="da895-162">_참고_: 이 제스처는 현재 인증서 목록을 삭제 하 고 리포지토리의 최신 목록으로 바꿉니다.</span><span class="sxs-lookup"><span data-stu-id="da895-162">_Note_: This gesture will delete the current list of certificates and replace them with an up-to-date list from the repository.</span></span>

## <a name="options"></a><span data-ttu-id="da895-163">변수</span><span class="sxs-lookup"><span data-stu-id="da895-163">Options</span></span>

| <span data-ttu-id="da895-164">옵션</span><span class="sxs-lookup"><span data-stu-id="da895-164">Option</span></span> | <span data-ttu-id="da895-165">설명</span><span class="sxs-lookup"><span data-stu-id="da895-165">Description</span></span> |
| --- | --- |
| <span data-ttu-id="da895-166">ConfigFile</span><span class="sxs-lookup"><span data-stu-id="da895-166">ConfigFile</span></span> | <span data-ttu-id="da895-167">적용할 NuGet 설정 파일입니다.</span><span class="sxs-lookup"><span data-stu-id="da895-167">The NuGet configuration file to apply.</span></span> <span data-ttu-id="da895-168">지정하지 않으면 기본적으로 Windows에서는 `%AppData%\NuGet\NuGet.Config`, Mac이나 Linux에서는 `~/.nuget/NuGet/NuGet.Config`가 사용됩니다.</span><span class="sxs-lookup"><span data-stu-id="da895-168">If not specified, `%AppData%\NuGet\NuGet.Config` (Windows) or `~/.nuget/NuGet/NuGet.Config` (Mac/Linux) is used.</span></span>|
| <span data-ttu-id="da895-169">ForceEnglishOutput</span><span class="sxs-lookup"><span data-stu-id="da895-169">ForceEnglishOutput</span></span> | <span data-ttu-id="da895-170">고정 영어 기반 문화권을 사용 하 여 nuget.exe를 실행 합니다.</span><span class="sxs-lookup"><span data-stu-id="da895-170">Forces nuget.exe to run using an invariant, English-based culture.</span></span> |
| <span data-ttu-id="da895-171">Help</span><span class="sxs-lookup"><span data-stu-id="da895-171">Help</span></span> | <span data-ttu-id="da895-172">명령어에 대한 도움말을 표시합니다.</span><span class="sxs-lookup"><span data-stu-id="da895-172">Displays help information for the command.</span></span> |
| <span data-ttu-id="da895-173">Verbosity</span><span class="sxs-lookup"><span data-stu-id="da895-173">Verbosity</span></span> | <span data-ttu-id="da895-174">출력에 표시되는 세부정보의 양을 지정합니다: *정상적인*, *조용한*, *자세한*합니다.</span><span class="sxs-lookup"><span data-stu-id="da895-174">Specifies the amount of detail displayed in the output: *normal*, *quiet*, *detailed*.</span></span> |

## <a name="examples"></a><span data-ttu-id="da895-175">예</span><span class="sxs-lookup"><span data-stu-id="da895-175">Examples</span></span>

```cli
nuget trusted-signers list

nuget trusted-signers Add -Name existingSource

nuget trusted-signers Add -Name trustedRepo -ServiceIndex https://trustedRepo.test/v3ServiceIndex

nuget trusted-signers Add -Name author1 -CertificateFingerprint CE40881FF5F0AD3E58965DA20A9F571EF1651A56933748E1BF1C99E537C4E039 -FingerprintAlgorithm SHA256

nuget trusted-signers Add -Repository .\..\MyRepositorySignedPackage.nupkg -Name TrustedRepo

nuget-trusted-signers Remove -Name TrustedRepo

nuget-trusted-signers Sync -Name TrustedRepo
```
