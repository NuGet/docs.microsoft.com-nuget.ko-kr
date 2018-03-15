---
title: "NuGet CLI 기호 명령을 | Microsoft Docs"
author: dtivel
ms.author: dtivel
manager: doronm
ms.date: 03/06/2018
ms.topic: reference
ms.prod: nuget
ms.technology: 
description: "Nuget.exe sign 명령에 대 한 참조"
keywords: "nuget 기호 참조, sign 명령"
ms.reviewer:
- karann
- rmpablos
ms.openlocfilehash: f600a0830472703f40ef62f1b1538c53671703a9
ms.sourcegitcommit: 74c21b406302288c158e8ae26057132b12960be8
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 03/15/2018
---
# <a name="sign-command-nuget-cli"></a><span data-ttu-id="742b0-104">sign 명령 (NuGet CLI)</span><span class="sxs-lookup"><span data-stu-id="742b0-104">sign command (NuGet CLI)</span></span>

<span data-ttu-id="742b0-105">**적용 대상:** 패키지 만들기가 &bullet; **지원 되는 버전:** 4.6 이상</span><span class="sxs-lookup"><span data-stu-id="742b0-105">**Applies to:** package creation &bullet; **Supported versions:** 4.6+</span></span>

<span data-ttu-id="742b0-106">인증서와 함께 첫 번째 인수를 일치 하는 모든 패키지에 서명 합니다.</span><span class="sxs-lookup"><span data-stu-id="742b0-106">Signs all the packages matching the first argument with a certificate.</span></span> <span data-ttu-id="742b0-107">주체 이름이 나 지문을 제공 하 여 인증서 저장소에 설치 된 인증서 또는 파일에서 인증서와 개인 키를 얻을 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="742b0-107">The certificate with the private key can be obtained from a file or from a certificate installed in a certificate store by providing a subject name or a thumbprint.</span></span>

<span data-ttu-id="742b0-108">패키지를 서명 아직 지원 되지 않습니다 모노 또는 Windows 이외의 플랫폼에서 합니다.</span><span class="sxs-lookup"><span data-stu-id="742b0-108">Package signing is not yet supported under Mono or on non-Windows platforms.</span></span>

## <a name="usage"></a><span data-ttu-id="742b0-109">사용법</span><span class="sxs-lookup"><span data-stu-id="742b0-109">Usage</span></span>

```cli
nuget sign <package(s)> [options]
```

<span data-ttu-id="742b0-110">여기서 `<package(s)>` 는 하나 이상의 `.nupkg` 파일입니다.</span><span class="sxs-lookup"><span data-stu-id="742b0-110">where `<package(s)>` is one or more `.nupkg` files.</span></span>

## <a name="options"></a><span data-ttu-id="742b0-111">옵션</span><span class="sxs-lookup"><span data-stu-id="742b0-111">Options</span></span>

| <span data-ttu-id="742b0-112">옵션</span><span class="sxs-lookup"><span data-stu-id="742b0-112">Option</span></span> | <span data-ttu-id="742b0-113">설명</span><span class="sxs-lookup"><span data-stu-id="742b0-113">Description</span></span> |
| --- | --- |
| <span data-ttu-id="742b0-114">CertificateFingerprint</span><span class="sxs-lookup"><span data-stu-id="742b0-114">CertificateFingerprint</span></span> | <span data-ttu-id="742b0-115">인증서에 대 한 로컬 인증서 저장소를 검색 하는 데 사용 되는 인증서의 sha-1 지문을 지정 합니다.</span><span class="sxs-lookup"><span data-stu-id="742b0-115">Specifies the SHA-1 fingerprint of the certificate used to search a local certificate store for the certificate.</span></span> |
| <span data-ttu-id="742b0-116">CertificatePassword</span><span class="sxs-lookup"><span data-stu-id="742b0-116">CertificatePassword</span></span> | <span data-ttu-id="742b0-117">필요한 경우 인증서 암호를 지정 합니다.</span><span class="sxs-lookup"><span data-stu-id="742b0-117">Specifies the certificate password, if needed.</span></span> <span data-ttu-id="742b0-118">인증서는 암호로 보호 하는 경우 암호가 제공 됩니다 명령 됩니다 암호를 묻는 메시지를 실행 하지 않는 한-비 대화형 옵션 전달 됩니다.</span><span class="sxs-lookup"><span data-stu-id="742b0-118">If a certificate is password protected but no password is provided, the command will prompt for a password at run time, unless the -NonInteractive option is passed.</span></span> |
| <span data-ttu-id="742b0-119">CertificatePath</span><span class="sxs-lookup"><span data-stu-id="742b0-119">CertificatePath</span></span> | <span data-ttu-id="742b0-120">패키지에 서명 하는 데 사용할 인증서를 파일 경로 지정 합니다.</span><span class="sxs-lookup"><span data-stu-id="742b0-120">Specifies the file path to the certificate to be used in signing the package.</span></span> |
| <span data-ttu-id="742b0-121">CertificateStoreLocation</span><span class="sxs-lookup"><span data-stu-id="742b0-121">CertificateStoreLocation</span></span> | <span data-ttu-id="742b0-122">인증서를 검색할 X.509 인증서 저장소 사용의 이름을 지정 합니다.</span><span class="sxs-lookup"><span data-stu-id="742b0-122">Specifies the name of the X.509 certificate store use to search for the certificate.</span></span> <span data-ttu-id="742b0-123">기본값은 "CurrentUser", 현재 사용자가 사용 되는 X.509 인증서 저장소입니다.</span><span class="sxs-lookup"><span data-stu-id="742b0-123">Defaults to "CurrentUser", the X.509 certificate store used by the current user.</span></span> <span data-ttu-id="742b0-124">-CertificateSubjectName 또는-CertificateFingerprint 옵션을 통해 인증서를 지정 하는 경우이 옵션을 사용 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="742b0-124">This option should be used when specifying the certificate via -CertificateSubjectName or -CertificateFingerprint options.</span></span> |
| <span data-ttu-id="742b0-125">CertificateStoreName</span><span class="sxs-lookup"><span data-stu-id="742b0-125">CertificateStoreName</span></span> | <span data-ttu-id="742b0-126">X.509 인증서 저장소를 사용 하는 인증서에 대 한 검색의 이름을 지정 합니다.</span><span class="sxs-lookup"><span data-stu-id="742b0-126">Specifies the name of the X.509 certificate store to use to search for the certificate.</span></span> <span data-ttu-id="742b0-127">기본값은 "My", 개인 인증서에 대 한 X.509 인증서 저장소입니다.</span><span class="sxs-lookup"><span data-stu-id="742b0-127">Defaults to "My", the X.509 certificate store for personal certificates.</span></span> <span data-ttu-id="742b0-128">-CertificateSubjectName 또는-CertificateFingerprint 옵션을 통해 인증서를 지정 하는 경우이 옵션을 사용 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="742b0-128">This option should be used when specifying the certificate via -CertificateSubjectName or -CertificateFingerprint options.</span></span> |
| <span data-ttu-id="742b0-129">CertificateSubjectName</span><span class="sxs-lookup"><span data-stu-id="742b0-129">CertificateSubjectName</span></span> | <span data-ttu-id="742b0-130">인증서에 대 한 로컬 인증서 저장소를 검색 하는 데 사용 되는 인증서의 주체 이름을 지정 합니다.</span><span class="sxs-lookup"><span data-stu-id="742b0-130">Specifies the subject name of the certificate used to search a local certificate store for the certificate.</span></span>  <span data-ttu-id="742b0-131">검색은 다른 주체 값에 관계 없이 해당 문자열을 포함 하는 주체 이름을 가진 모든 인증서를 찾습니다는 제공 된 값을 사용 하 여 대/소문자 구분 문자열 비교 합니다.</span><span class="sxs-lookup"><span data-stu-id="742b0-131">The search is a case-insensitive string comparison using the supplied value, which will find all certificates with the subject name containing that string, regardless of other subject values.</span></span>  <span data-ttu-id="742b0-132">인증서 저장소-CertificateStoreName 및-CertificateStoreLocation 옵션에 지정할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="742b0-132">The certificate store can be specified by -CertificateStoreName and -CertificateStoreLocation options.</span></span> |
| <span data-ttu-id="742b0-133">ConfigFile</span><span class="sxs-lookup"><span data-stu-id="742b0-133">ConfigFile</span></span> | <span data-ttu-id="742b0-134">적용할 NuGet 구성 파일입니다.</span><span class="sxs-lookup"><span data-stu-id="742b0-134">The NuGet configuration file to apply.</span></span> <span data-ttu-id="742b0-135">지정 하지 않으면 `%AppData%\NuGet\NuGet.Config` (Windows) 또는 `~/.nuget/NuGet/NuGet.Config` (Mac/Linux)가 사용 됩니다.</span><span class="sxs-lookup"><span data-stu-id="742b0-135">If not specified, `%AppData%\NuGet\NuGet.Config` (Windows) or `~/.nuget/NuGet/NuGet.Config` (Mac/Linux) is used.</span></span>|
| <span data-ttu-id="742b0-136">ForceEnglishOutput</span><span class="sxs-lookup"><span data-stu-id="742b0-136">ForceEnglishOutput</span></span> | <span data-ttu-id="742b0-137">Nuget.exe 고정, 영어 기반 문화권을 사용 하 여 실행을 강제로 수행 합니다.</span><span class="sxs-lookup"><span data-stu-id="742b0-137">Forces nuget.exe to run using an invariant, English-based culture.</span></span> |
| <span data-ttu-id="742b0-138">HashAlgorithm</span><span class="sxs-lookup"><span data-stu-id="742b0-138">HashAlgorithm</span></span> | <span data-ttu-id="742b0-139">패키지에 서명 하는 데 사용할 해시 알고리즘입니다.</span><span class="sxs-lookup"><span data-stu-id="742b0-139">Hash algorithm to be used to sign the package.</span></span> <span data-ttu-id="742b0-140">기본값은 s h a 256입니다.</span><span class="sxs-lookup"><span data-stu-id="742b0-140">Defaults to SHA256.</span></span> |
| <span data-ttu-id="742b0-141">도움말</span><span class="sxs-lookup"><span data-stu-id="742b0-141">Help</span></span> | <span data-ttu-id="742b0-142">도움말의 명령에 대 한 정보를 표시 합니다.</span><span class="sxs-lookup"><span data-stu-id="742b0-142">Displays help information for the command.</span></span> |
| <span data-ttu-id="742b0-143">NonInteractive</span><span class="sxs-lookup"><span data-stu-id="742b0-143">NonInteractive</span></span> | <span data-ttu-id="742b0-144">사용자 입력 또는 확인에 대 한 프롬프트를 표시 하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="742b0-144">Suppresses prompts for user input or confirmations.</span></span> |
| <span data-ttu-id="742b0-145">OutputDirectory</span><span class="sxs-lookup"><span data-stu-id="742b0-145">OutputDirectory</span></span> | <span data-ttu-id="742b0-146">서명된 된 패키지를 저장할 디렉터리를 지정 합니다.</span><span class="sxs-lookup"><span data-stu-id="742b0-146">Specifies the directory where the signed package should be saved.</span></span> <span data-ttu-id="742b0-147">기본적으로 서명된 된 패키지는 원본 패키지를 덮어씁니다.</span><span class="sxs-lookup"><span data-stu-id="742b0-147">By default the original package is overwritten by the signed package.</span></span> |
| <span data-ttu-id="742b0-148">덮어쓰기</span><span class="sxs-lookup"><span data-stu-id="742b0-148">Overwrite</span></span> | <span data-ttu-id="742b0-149">현재 서명 덮어써야 하는 경우를 나타내기 위해 스위치입니다.</span><span class="sxs-lookup"><span data-stu-id="742b0-149">Switch to indicate if the current signature should be overwritten.</span></span> <span data-ttu-id="742b0-150">기본적으로 패키지 서명을 이미 있으면 명령이 실패 합니다.</span><span class="sxs-lookup"><span data-stu-id="742b0-150">By default the command will fail if the package already has a signature.</span></span> |
| <span data-ttu-id="742b0-151">Timestamper</span><span class="sxs-lookup"><span data-stu-id="742b0-151">Timestamper</span></span> | <span data-ttu-id="742b0-152">RFC 3161 타임 스탬프 서버 URL입니다.</span><span class="sxs-lookup"><span data-stu-id="742b0-152">URL to an RFC 3161 timestamping server.</span></span> |
| <span data-ttu-id="742b0-153">TimestampHashAlgorithm</span><span class="sxs-lookup"><span data-stu-id="742b0-153">TimestampHashAlgorithm</span></span> | <span data-ttu-id="742b0-154">RFC 3161 타임 스탬프 서버에서 사용할 해시 알고리즘입니다.</span><span class="sxs-lookup"><span data-stu-id="742b0-154">Hash algorithm to be used by the RFC 3161 timestamp server.</span></span> <span data-ttu-id="742b0-155">기본값은 s h a 256입니다.</span><span class="sxs-lookup"><span data-stu-id="742b0-155">Defaults to SHA256.</span></span> |
| <span data-ttu-id="742b0-156">자세한 정도</span><span class="sxs-lookup"><span data-stu-id="742b0-156">Verbosity</span></span> | <span data-ttu-id="742b0-157">출력에 표시 되는 세부 정보 수준을 지정: *일반*, *quiet*, *자세한*합니다.</span><span class="sxs-lookup"><span data-stu-id="742b0-157">Specifies the amount of detail displayed in the output: *normal*, *quiet*, *detailed*.</span></span> |

## <a name="examples"></a><span data-ttu-id="742b0-158">예제</span><span class="sxs-lookup"><span data-stu-id="742b0-158">Examples</span></span>

```cli
nuget sign MyPackage.nupkg -Timestamper http://timestamp.test

nuget sign .\..\MyPackage.nupkg -Timestamper http://timestamp.test -OutputDirectory .\..\Signed
```