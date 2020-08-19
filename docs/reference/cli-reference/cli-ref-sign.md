---
title: NuGet CLI sign 명령
description: nuget.exe sign 명령에 대 한 참조
author: dtivel
ms.author: dtivel
ms.date: 03/06/2018
ms.topic: reference
ms.reviewer: rmpablos
ms.openlocfilehash: 84386f1752b98688f1fd34e453f5b72ae8afdd92
ms.sourcegitcommit: cbc87fe51330cdd3eacaad3e8656eb4258882fc7
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/19/2020
ms.locfileid: "88622774"
---
# <a name="sign-command-nuget-cli"></a><span data-ttu-id="a5e6d-103">sign 명령 (NuGet CLI)</span><span class="sxs-lookup"><span data-stu-id="a5e6d-103">sign command (NuGet CLI)</span></span>

<span data-ttu-id="a5e6d-104">**적용 대상:** 패키지 만들기 &bullet; **지원 버전:** 4.6 +</span><span class="sxs-lookup"><span data-stu-id="a5e6d-104">**Applies to:** package creation &bullet; **Supported versions:** 4.6+</span></span>

<span data-ttu-id="a5e6d-105">인증서를 사용 하 여 첫 번째 인수와 일치 하는 모든 패키지에 서명 합니다.</span><span class="sxs-lookup"><span data-stu-id="a5e6d-105">Signs all the packages matching the first argument with a certificate.</span></span> <span data-ttu-id="a5e6d-106">개인 키가 있는 인증서는 주체 이름 또는 지문을 제공 하 여 인증서 저장소에 설치 된 인증서 또는 파일에서 가져올 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="a5e6d-106">The certificate with the private key can be obtained from a file or from a certificate installed in a certificate store by providing a subject name or a thumbprint.</span></span>

> [!Note]
> <span data-ttu-id="a5e6d-107">패키지 서명은 .NET Core, Mono 또는 Windows 이외의 플랫폼에서 아직 지원 되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="a5e6d-107">Package signing is not yet supported in .NET Core, under Mono, or on non-Windows platforms.</span></span>

## <a name="usage"></a><span data-ttu-id="a5e6d-108">사용량</span><span class="sxs-lookup"><span data-stu-id="a5e6d-108">Usage</span></span>

```cli
nuget sign <package(s)> [options]
```

<span data-ttu-id="a5e6d-109">여기서 `<package(s)>` 는 하나 이상의 `.nupkg` 파일입니다.</span><span class="sxs-lookup"><span data-stu-id="a5e6d-109">where `<package(s)>` is one or more `.nupkg` files.</span></span>

## <a name="options"></a><span data-ttu-id="a5e6d-110">옵션</span><span class="sxs-lookup"><span data-stu-id="a5e6d-110">Options</span></span>

- **`-CertificateFingerprint`**

  <span data-ttu-id="a5e6d-111">인증서에 대 한 로컬 인증서 저장소를 검색 하는 데 사용 되는 인증서의 SHA-1 지문을 지정 합니다.</span><span class="sxs-lookup"><span data-stu-id="a5e6d-111">Specifies the SHA-1 fingerprint of the certificate used to search a local certificate store for the certificate.</span></span>

- **`-CertificatePassword`**

  <span data-ttu-id="a5e6d-112">필요한 경우 인증서 암호를 지정 합니다.</span><span class="sxs-lookup"><span data-stu-id="a5e6d-112">Specifies the certificate password, if needed.</span></span> <span data-ttu-id="a5e6d-113">인증서가 암호로 보호 되어 있지만 암호를 제공 하지 않으면 명령이 전달 되지 않는 한 런타임에 암호를 입력 하 라는 메시지가 표시 됩니다 `-NonInteractive` .</span><span class="sxs-lookup"><span data-stu-id="a5e6d-113">If a certificate is password protected but no password is provided, the command will prompt for a password at run time, unless the `-NonInteractive` option is passed.</span></span>

- **`-CertificatePath`**

  <span data-ttu-id="a5e6d-114">패키지에 서명 하는 데 사용할 인증서의 파일 경로를 지정 합니다.</span><span class="sxs-lookup"><span data-stu-id="a5e6d-114">Specifies the file path to the certificate to be used in signing the package.</span></span>

- **`-CertificateStoreLocation`**

  <span data-ttu-id="a5e6d-115">인증서를 검색 하는 데 사용 하는 x.509 인증서 저장소의 이름을 지정 합니다.</span><span class="sxs-lookup"><span data-stu-id="a5e6d-115">Specifies the name of the X.509 certificate store use to search for the certificate.</span></span> <span data-ttu-id="a5e6d-116">기본값은 현재 사용자가 사용 하는 x.509 인증서 저장소 인 "CurrentUser"입니다.</span><span class="sxs-lookup"><span data-stu-id="a5e6d-116">Defaults to "CurrentUser", the X.509 certificate store used by the current user.</span></span> <span data-ttu-id="a5e6d-117">또는 옵션을 통해 인증서를 지정할 때이 옵션을 사용 해야 합니다 `-CertificateSubjectName` `-CertificateFingerprint` .</span><span class="sxs-lookup"><span data-stu-id="a5e6d-117">This option should be used when specifying the certificate via `-CertificateSubjectName` or `-CertificateFingerprint` options.</span></span>

- **`-CertificateStoreName`**

  <span data-ttu-id="a5e6d-118">인증서를 검색 하는 데 사용할 x.509 인증서 저장소의 이름을 지정 합니다.</span><span class="sxs-lookup"><span data-stu-id="a5e6d-118">Specifies the name of the X.509 certificate store to use to search for the certificate.</span></span> <span data-ttu-id="a5e6d-119">기본값은 개인 인증서에 대 한 x.509 인증서 저장소 인 "My"입니다.</span><span class="sxs-lookup"><span data-stu-id="a5e6d-119">Defaults to "My", the X.509 certificate store for personal certificates.</span></span> <span data-ttu-id="a5e6d-120">또는 옵션을 통해 인증서를 지정할 때이 옵션을 사용 해야 합니다 `-CertificateSubjectName` `-CertificateFingerprint` .</span><span class="sxs-lookup"><span data-stu-id="a5e6d-120">This option should be used when specifying the certificate via `-CertificateSubjectName` or `-CertificateFingerprint` options.</span></span>

- **`-CertificateSubjectName`**

  <span data-ttu-id="a5e6d-121">인증서에 대 한 로컬 인증서 저장소를 검색 하는 데 사용 되는 인증서의 주체 이름을 지정 합니다.</span><span class="sxs-lookup"><span data-stu-id="a5e6d-121">Specifies the subject name of the certificate used to search a local certificate store for the certificate.</span></span>  <span data-ttu-id="a5e6d-122">검색은 제공 된 값을 사용 하 여 대/소문자를 구분 하지 않는 문자열 비교로, 다른 주체 값에 관계 없이 해당 문자열을 포함 하는 주체 이름을 가진 모든 인증서를 찾습니다.</span><span class="sxs-lookup"><span data-stu-id="a5e6d-122">The search is a case-insensitive string comparison using the supplied value, which will find all certificates with the subject name containing that string, regardless of other subject values.</span></span>  <span data-ttu-id="a5e6d-123">인증서 저장소는 및 옵션으로 지정할 수 있습니다 `-CertificateStoreName` `-CertificateStoreLocation` .</span><span class="sxs-lookup"><span data-stu-id="a5e6d-123">The certificate store can be specified by `-CertificateStoreName` and `-CertificateStoreLocation` options.</span></span>

- **`-ConfigFile`**

  <span data-ttu-id="a5e6d-124">적용할 NuGet 구성 파일입니다.</span><span class="sxs-lookup"><span data-stu-id="a5e6d-124">The NuGet configuration file to apply.</span></span> <span data-ttu-id="a5e6d-125">지정 하지 않으면 `%AppData%\NuGet\NuGet.Config` (Windows) 또는 `~/.nuget/NuGet/NuGet.Config` 또는 `~/.config/NuGet/NuGet.Config` (Mac/Linux)가 사용 됩니다.</span><span class="sxs-lookup"><span data-stu-id="a5e6d-125">If not specified, `%AppData%\NuGet\NuGet.Config` (Windows), or `~/.nuget/NuGet/NuGet.Config` or `~/.config/NuGet/NuGet.Config` (Mac/Linux) is used.</span></span>

- **`-ForceEnglishOutput`**

  <span data-ttu-id="a5e6d-126">고정 된 영어 기반 문화권을 사용 하 여 nuget.exe을 강제로 실행 합니다.</span><span class="sxs-lookup"><span data-stu-id="a5e6d-126">Forces nuget.exe to run using an invariant, English-based culture.</span></span>

- **`-HashAlgorithm`**

  <span data-ttu-id="a5e6d-127">패키지에 서명 하는 데 사용할 해시 알고리즘입니다.</span><span class="sxs-lookup"><span data-stu-id="a5e6d-127">Hash algorithm to be used to sign the package.</span></span> <span data-ttu-id="a5e6d-128">기본값은 SHA256입니다.</span><span class="sxs-lookup"><span data-stu-id="a5e6d-128">Defaults to SHA256.</span></span> <span data-ttu-id="a5e6d-129">가능한 값은 SHA256, SHA384 및 SHA512입니다.</span><span class="sxs-lookup"><span data-stu-id="a5e6d-129">Possible values are SHA256, SHA384, and SHA512.</span></span>

- **`-?|-help`**

  <span data-ttu-id="a5e6d-130">명령에 대 한 도움말 정보를 표시 합니다.</span><span class="sxs-lookup"><span data-stu-id="a5e6d-130">Displays help information for the command.</span></span>

- **`-NonInteractive`**

  <span data-ttu-id="a5e6d-131">사용자 입력 또는 확인에 대 한 프롬프트를 표시 하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="a5e6d-131">Suppresses prompts for user input or confirmations.</span></span>

- **`-OutputDirectory`**

  <span data-ttu-id="a5e6d-132">서명 된 패키지를 저장할 디렉터리를 지정 합니다.</span><span class="sxs-lookup"><span data-stu-id="a5e6d-132">Specifies the directory where the signed package should be saved.</span></span> <span data-ttu-id="a5e6d-133">기본적으로 서명 된 패키지가 원래 패키지를 덮어씁니다.</span><span class="sxs-lookup"><span data-stu-id="a5e6d-133">By default the original package is overwritten by the signed package.</span></span>

- **`-Overwrite`**

  <span data-ttu-id="a5e6d-134">현재 서명을 덮어쓸지 여부를 나타내는로 전환 합니다.</span><span class="sxs-lookup"><span data-stu-id="a5e6d-134">Switch to indicate if the current signature should be overwritten.</span></span> <span data-ttu-id="a5e6d-135">기본적으로 패키지에 이미 서명이 있으면 명령이 실패 합니다.</span><span class="sxs-lookup"><span data-stu-id="a5e6d-135">By default the command will fail if the package already has a signature.</span></span>

- **`-Timestamper`**

  <span data-ttu-id="a5e6d-136">RFC 3161 타임 스탬프 서버의 URL입니다.</span><span class="sxs-lookup"><span data-stu-id="a5e6d-136">URL to an RFC 3161 timestamping server.</span></span>

- **`-TimestampHashAlgorithm`**

  <span data-ttu-id="a5e6d-137">RFC 3161 타임 스탬프 서버에서 사용 되는 해시 알고리즘입니다.</span><span class="sxs-lookup"><span data-stu-id="a5e6d-137">Hash algorithm to be used by the RFC 3161 timestamp server.</span></span> <span data-ttu-id="a5e6d-138">기본값은 SHA256입니다.</span><span class="sxs-lookup"><span data-stu-id="a5e6d-138">Defaults to SHA256.</span></span>

- **`-Verbosity [normal|quiet|detailed]`**

  <span data-ttu-id="a5e6d-139">출력에 표시 되는 세부 정보의 양을 지정 합니다. `normal` (기본값), `quiet` 또는 `detailed` 입니다.</span><span class="sxs-lookup"><span data-stu-id="a5e6d-139">Specifies the amount of detail displayed in the output: `normal` (the default), `quiet`, or `detailed`.</span></span>

## <a name="examples"></a><span data-ttu-id="a5e6d-140">예</span><span class="sxs-lookup"><span data-stu-id="a5e6d-140">Examples</span></span>

```cli
nuget sign MyPackage.nupkg -CertificatePath .\..\certificate.pfx -Timestamper http://timestamp.test

nuget sign .\..\MyPackage.nupkg -CertificateStoreLocation CurrentUser -CertificateStoreName My -CertificateSubjectName 'subject name' -Timestamper http://timestamp.test -OutputDirectory .\..\Signed
```
