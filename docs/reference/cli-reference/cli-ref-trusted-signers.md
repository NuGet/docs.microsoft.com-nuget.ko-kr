---
title: NuGet CLI 신뢰-서명자 명령
description: nuget.exe 신뢰할 수 있는 서명자 명령에 대 한 참조
author: patbel
ms.author: patbel
ms.date: 11/12/2018
ms.topic: reference
ms.reviewer: rmpablos
ms.openlocfilehash: 2753f92601b3d8b43593762cc07cd8384646feea
ms.sourcegitcommit: cbc87fe51330cdd3eacaad3e8656eb4258882fc7
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/19/2020
ms.locfileid: "88622670"
---
# <a name="trusted-signers-command-nuget-cli"></a><span data-ttu-id="80f3c-103">trusted-서명자 명령 (NuGet CLI)</span><span class="sxs-lookup"><span data-stu-id="80f3c-103">trusted-signers command (NuGet CLI)</span></span>

<span data-ttu-id="80f3c-104">**적용 대상:** 패키지 사용 &bullet; **지원 버전:** 4.9.1 +</span><span class="sxs-lookup"><span data-stu-id="80f3c-104">**Applies to:** package consumption &bullet; **Supported versions:** 4.9.1+</span></span>

<span data-ttu-id="80f3c-105">NuGet 구성에 대해 신뢰할 수 있는 서명자를 가져오거나 설정 합니다.</span><span class="sxs-lookup"><span data-stu-id="80f3c-105">Gets or sets trusted signers to the NuGet configuration.</span></span> <span data-ttu-id="80f3c-106">추가 사용에 대해서는 [일반적인 NuGet 구성](../../consume-packages/configuring-nuget-behavior.md)을 참조 하세요.</span><span class="sxs-lookup"><span data-stu-id="80f3c-106">For additional usage, see [Common NuGet configurations](../../consume-packages/configuring-nuget-behavior.md).</span></span> <span data-ttu-id="80f3c-107">nuget.config 스키마의 모양에 대 한 자세한 내용은 [NuGet 구성 파일 참조](../nuget-config-file.md)를 참조 하세요.</span><span class="sxs-lookup"><span data-stu-id="80f3c-107">For details on how the nuget.config schema looks like, refer to the [NuGet config file reference](../nuget-config-file.md).</span></span>

## <a name="usage"></a><span data-ttu-id="80f3c-108">사용량</span><span class="sxs-lookup"><span data-stu-id="80f3c-108">Usage</span></span>

```cli
nuget trusted-signers <list|add|remove|sync> [options]
```

<span data-ttu-id="80f3c-109">을 `list|add|remove|sync` 지정 하지 않으면 명령은 기본적으로로 지정 됩니다 `list` .</span><span class="sxs-lookup"><span data-stu-id="80f3c-109">if none of `list|add|remove|sync` is specified, the command will default to `list`.</span></span>

## <a name="nuget-trusted-signers-list"></a><span data-ttu-id="80f3c-110">nuget 신뢰할 수 있는 서명자 목록</span><span class="sxs-lookup"><span data-stu-id="80f3c-110">nuget trusted-signers list</span></span>

<span data-ttu-id="80f3c-111">구성의 모든 신뢰할 수 있는 서명자를 나열 합니다.</span><span class="sxs-lookup"><span data-stu-id="80f3c-111">Lists all the trusted signers in the configuration.</span></span> <span data-ttu-id="80f3c-112">이 옵션에는 각 서명자가 있는 모든 인증서 (지문 및 지문 알고리즘 포함)가 포함 됩니다.</span><span class="sxs-lookup"><span data-stu-id="80f3c-112">This option will include all the certificates (with fingerprint and fingerprint algorithm) each signer has.</span></span> <span data-ttu-id="80f3c-113">인증서에 앞에가 있는 경우 `[U]` 인증서 항목이로 설정 되어 있음을 의미 `allowUntrustedRoot` `true` 합니다.</span><span class="sxs-lookup"><span data-stu-id="80f3c-113">If a certificate has a preceding `[U]`, it means that certificate entry has `allowUntrustedRoot` set as `true`.</span></span>

<span data-ttu-id="80f3c-114">다음은이 명령의 출력 예제입니다.</span><span class="sxs-lookup"><span data-stu-id="80f3c-114">Below is an example output from this command:</span></span>

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

## <a name="nuget-trusted-signers-add-options"></a><span data-ttu-id="80f3c-115">nuget 신뢰할 수 있는 서명자 add [options]</span><span class="sxs-lookup"><span data-stu-id="80f3c-115">nuget trusted-signers add [options]</span></span>

<span data-ttu-id="80f3c-116">지정 된 이름의 신뢰할 수 있는 서명자를 구성에 추가 합니다. 이 옵션은 신뢰할 수 있는 작성자 또는 리포지토리를 추가 하는 다른 제스처를 포함 합니다.</span><span class="sxs-lookup"><span data-stu-id="80f3c-116">Adds a trusted signer with the given name to the config. This option has different gestures to add a trusted author or repository.</span></span>

## <a name="options-for-add-based-on-a-package"></a><span data-ttu-id="80f3c-117">패키지 기반 추가 옵션</span><span class="sxs-lookup"><span data-stu-id="80f3c-117">Options for add based on a package</span></span>

```cli
nuget trusted-signers add <package(s)> -Name <name> [options]
```

<span data-ttu-id="80f3c-118">여기서 `<package(s)>` 는 하나 이상의 `.nupkg` 파일입니다.</span><span class="sxs-lookup"><span data-stu-id="80f3c-118">where `<package(s)>` is one or more `.nupkg` files.</span></span>

- **`-Author`**

  <span data-ttu-id="80f3c-119">패키지의 작성자 서명을 신뢰할 수 있도록 지정 합니다.</span><span class="sxs-lookup"><span data-stu-id="80f3c-119">Specifies that the author signature of the package(s) should be trusted.</span></span>

- **`-AllowUntrustedRoot`**

  <span data-ttu-id="80f3c-120">신뢰할 수 있는 서명자에 대 한 인증서를 신뢰할 수 없는 루트에 연결할 수 있는지 여부를 지정 합니다.</span><span class="sxs-lookup"><span data-stu-id="80f3c-120">Specifies if the certificate for the trusted signer should be allowed to chain to an untrusted root.</span></span>

- **`-Owners`**

  <span data-ttu-id="80f3c-121">리포지토리의 신뢰를 추가로 제한 하는 신뢰할 수 있는 소유자의 세미콜론으로 구분 된 목록입니다.</span><span class="sxs-lookup"><span data-stu-id="80f3c-121">Semi-colon separated list of trusted owners to further restrict the trust of a repository.</span></span> <span data-ttu-id="80f3c-122">옵션을 사용 하는 경우에만 유효 `-Repository` 합니다.</span><span class="sxs-lookup"><span data-stu-id="80f3c-122">Only valid when using the `-Repository` option.</span></span>

- **`-Repository`**

  <span data-ttu-id="80f3c-123">패키지의 저장소 서명 또는 연대 서명을 신뢰할 수 있도록 지정 합니다.</span><span class="sxs-lookup"><span data-stu-id="80f3c-123">Specifies that the repository signature or countersignature of the package(s) should be trusted.</span></span>

<span data-ttu-id="80f3c-124">와를 `-Author` `-Repository` 동시에 제공 하는 것은 지원 되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="80f3c-124">Providing both `-Author` and `-Repository` at the same time is not supported.</span></span>

## <a name="options-for-add-based-on-a-service-index"></a><span data-ttu-id="80f3c-125">서비스 인덱스를 기반으로 하는 추가 옵션</span><span class="sxs-lookup"><span data-stu-id="80f3c-125">Options for add based on a service index</span></span>

```cli
nuget trusted-signers add -Name <name> [options]
```

<span data-ttu-id="80f3c-126">_참고_:이 옵션은 신뢰할 수 있는 리포지토리만 추가 합니다.</span><span class="sxs-lookup"><span data-stu-id="80f3c-126">_Note_: This option will only add trusted repositories.</span></span> 

- **`-AllowUntrustedRoot`**

  <span data-ttu-id="80f3c-127">신뢰할 수 있는 서명자에 대 한 인증서를 신뢰할 수 없는 루트에 연결할 수 있는지 여부를 지정 합니다.</span><span class="sxs-lookup"><span data-stu-id="80f3c-127">Specifies if the certificate for the trusted signer should be allowed to chain to an untrusted root.</span></span>

- **`-Owners`**

  <span data-ttu-id="80f3c-128">리포지토리의 신뢰를 추가로 제한 하는 신뢰할 수 있는 소유자의 세미콜론으로 구분 된 목록입니다.</span><span class="sxs-lookup"><span data-stu-id="80f3c-128">Semi-colon separated list of trusted owners to further restrict the trust of a repository.</span></span>

- **`-ServiceIndex`**

  <span data-ttu-id="80f3c-129">신뢰할 리포지토리의 V3 서비스 인덱스를 지정 합니다.</span><span class="sxs-lookup"><span data-stu-id="80f3c-129">Specifies the V3 service index of the repository to be trusted.</span></span> <span data-ttu-id="80f3c-130">이 리포지토리는 리포지토리 서명 리소스를 지원 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="80f3c-130">This repository has to support the repository signatures resource.</span></span> <span data-ttu-id="80f3c-131">지정 하지 않으면 명령이 동일한 패키지 소스를 검색 하 여 해당 위치 `-Name` 에서 서비스 인덱스를 가져옵니다.</span><span class="sxs-lookup"><span data-stu-id="80f3c-131">If not provided, the command will look for a package source with the same `-Name` and get the service index from there.</span></span>

## <a name="options-for-add-based-on-the-certificate-information"></a><span data-ttu-id="80f3c-132">인증서 정보에 따라 추가 옵션</span><span class="sxs-lookup"><span data-stu-id="80f3c-132">Options for add based on the certificate information</span></span>

```cli
nuget trusted-signers add -Name <name> [options]
```

<span data-ttu-id="80f3c-133">_참고_: 지정 된 이름의 신뢰할 수 있는 서명자가 이미 있는 경우 해당 서명자에 게 인증서 항목이 추가 됩니다.</span><span class="sxs-lookup"><span data-stu-id="80f3c-133">_Note_: If a trusted signer with the given name already exists, the certificate item will be added to that signer.</span></span> <span data-ttu-id="80f3c-134">그렇지 않으면 지정 된 인증서 정보에서 인증서 항목을 사용 하 여 신뢰할 수 있는 작성자가 만들어집니다.</span><span class="sxs-lookup"><span data-stu-id="80f3c-134">Otherwise a trusted author will be created with a certificate item from given certificate information.</span></span>


- **`-AllowUntrustedRoot`**

  <span data-ttu-id="80f3c-135">신뢰할 수 있는 서명자에 대 한 인증서를 신뢰할 수 없는 루트에 연결할 수 있는지 여부를 지정 합니다.</span><span class="sxs-lookup"><span data-stu-id="80f3c-135">Specifies if the certificate for the trusted signer should be allowed to chain to an untrusted root.</span></span>

- **`-CertificateFingerprint`**

  <span data-ttu-id="80f3c-136">서명 된 패키지에 서명 해야 하는 인증서의 인증서 지문을 지정 합니다.</span><span class="sxs-lookup"><span data-stu-id="80f3c-136">Specifies a certificate fingerprints of a certificate which signed packages must be signed with.</span></span> <span data-ttu-id="80f3c-137">인증서 지문을 인증서의 해시입니다.</span><span class="sxs-lookup"><span data-stu-id="80f3c-137">A certificate fingerprint is a hash of the certificate.</span></span> <span data-ttu-id="80f3c-138">이 해시를 계산 하는 데 사용 되는 해시 알고리즘은 옵션에서 지정 해야 합니다 `FingerprintAlgorithm` .</span><span class="sxs-lookup"><span data-stu-id="80f3c-138">The hash algorithm used for calculating this hash should be specifies in the `FingerprintAlgorithm` option.</span></span>

- **`-FingerprintAlgorithm`**

  <span data-ttu-id="80f3c-139">인증서 지문을 계산 하는 데 사용 되는 해시 알고리즘을 지정 합니다.</span><span class="sxs-lookup"><span data-stu-id="80f3c-139">Specifies the hash algorithm used to calculate the certificate fingerprint.</span></span> <span data-ttu-id="80f3c-140">기본값은 `SHA256`입니다.</span><span class="sxs-lookup"><span data-stu-id="80f3c-140">Defaults to `SHA256`.</span></span> <span data-ttu-id="80f3c-141">지원 되는 값은 `SHA256` , `SHA384` 및 `SHA512` 입니다.</span><span class="sxs-lookup"><span data-stu-id="80f3c-141">Values supported are `SHA256`, `SHA384` and `SHA512`.</span></span>

## <a name="nuget-trusted-signers-remove--name-name"></a><span data-ttu-id="80f3c-142">nuget 신뢰할 수 있는 서명자 이름 제거 \<name\></span><span class="sxs-lookup"><span data-stu-id="80f3c-142">nuget trusted-signers remove -Name \<name\></span></span>

<span data-ttu-id="80f3c-143">지정 된 이름과 일치 하는 모든 신뢰할 수 있는 서명자를 제거 합니다.</span><span class="sxs-lookup"><span data-stu-id="80f3c-143">Removes any trusted signers that match the given name.</span></span>

## <a name="nuget-trusted-signers-sync--name-name"></a><span data-ttu-id="80f3c-144">nuget 신뢰할 수 있는 서명자 동기화-이름 \<name\></span><span class="sxs-lookup"><span data-stu-id="80f3c-144">nuget trusted-signers sync -Name \<name\></span></span>

<span data-ttu-id="80f3c-145">현재 신뢰할 수 있는 리포지토리에서 사용 되는 인증서의 최신 목록을 요청 하 여 신뢰할 수 있는 서명자의 기존 인증서 목록을 업데이트 합니다.</span><span class="sxs-lookup"><span data-stu-id="80f3c-145">Requests the latest list of certificates used in a currently trusted repository to update the the existing certificate list in the trusted signer.</span></span>

<span data-ttu-id="80f3c-146">_참고_:이 제스처는 현재 인증서 목록을 삭제 하 고 리포지토리의 최신 목록으로 바꿉니다.</span><span class="sxs-lookup"><span data-stu-id="80f3c-146">_Note_: This gesture will delete the current list of certificates and replace them with an up-to-date list from the repository.</span></span>

## <a name="options"></a><span data-ttu-id="80f3c-147">옵션</span><span class="sxs-lookup"><span data-stu-id="80f3c-147">Options</span></span>

- **`-ConfigFile`**

  <span data-ttu-id="80f3c-148">적용할 NuGet 구성 파일입니다.</span><span class="sxs-lookup"><span data-stu-id="80f3c-148">The NuGet configuration file to apply.</span></span> <span data-ttu-id="80f3c-149">지정 하지 않으면 `%AppData%\NuGet\NuGet.Config` (Windows) 또는 `~/.nuget/NuGet/NuGet.Config` 또는 `~/.config/NuGet/NuGet.Config` (Mac/Linux)가 사용 됩니다.</span><span class="sxs-lookup"><span data-stu-id="80f3c-149">If not specified, `%AppData%\NuGet\NuGet.Config` (Windows), or `~/.nuget/NuGet/NuGet.Config` or `~/.config/NuGet/NuGet.Config` (Mac/Linux) is used.</span></span>

- **`-ForceEnglishOutput`**

  <span data-ttu-id="80f3c-150">고정 된 영어 기반 문화권을 사용 하 여 nuget.exe을 강제로 실행 합니다.</span><span class="sxs-lookup"><span data-stu-id="80f3c-150">Forces nuget.exe to run using an invariant, English-based culture.</span></span>

- **`-?|-help`**

  <span data-ttu-id="80f3c-151">명령에 대 한 도움말 정보를 표시 합니다.</span><span class="sxs-lookup"><span data-stu-id="80f3c-151">Displays help information for the command.</span></span>

- **`-Name`**

  <span data-ttu-id="80f3c-152">신뢰할 수 있는 서명자의 이름입니다.</span><span class="sxs-lookup"><span data-stu-id="80f3c-152">Name of the trusted signer.</span></span>

- **`-NonInteractive`**

  <span data-ttu-id="80f3c-153">사용자 입력 또는 확인에 대 한 프롬프트를 표시 하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="80f3c-153">Suppresses prompts for user input or confirmations.</span></span>

- **`-Verbosity [normal|quiet|detailed]`**

  <span data-ttu-id="80f3c-154">출력에 표시 되는 세부 정보의 양을 지정 합니다. `normal` (기본값), `quiet` 또는 `detailed` 입니다.</span><span class="sxs-lookup"><span data-stu-id="80f3c-154">Specifies the amount of detail displayed in the output: `normal` (the default), `quiet`, or `detailed`.</span></span>


## <a name="examples"></a><span data-ttu-id="80f3c-155">예</span><span class="sxs-lookup"><span data-stu-id="80f3c-155">Examples</span></span>

```cli
nuget trusted-signers list

nuget trusted-signers Add -Name existingSource

nuget trusted-signers Add -Name trustedRepo -ServiceIndex https://trustedRepo.test/v3ServiceIndex

nuget trusted-signers Add -Name author1 -CertificateFingerprint CE40881FF5F0AD3E58965DA20A9F571EF1651A56933748E1BF1C99E537C4E039 -FingerprintAlgorithm SHA256

nuget trusted-signers Add -Repository .\..\MyRepositorySignedPackage.nupkg -Name TrustedRepo

nuget-trusted-signers Remove -Name TrustedRepo

nuget-trusted-signers Sync -Name TrustedRepo
```
