---
title: NuGet CLI 서명 명령
description: Nuget.exe 서명 명령에 대 한 참조
author: dtivel
ms.author: dtivel
ms.date: 03/06/2018
ms.topic: reference
ms.reviewer: rmpablos
ms.openlocfilehash: e941a9f34058f5ebed13a8f68c8cfa23ba5fb6d1
ms.sourcegitcommit: 1d1406764c6af5fb7801d462e0c4afc9092fa569
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 09/04/2018
ms.locfileid: "43546365"
---
# <a name="sign-command-nuget-cli"></a><span data-ttu-id="99dd0-103">sign 명령(NuGet CLI)</span><span class="sxs-lookup"><span data-stu-id="99dd0-103">sign command (NuGet CLI)</span></span>

<span data-ttu-id="99dd0-104">**적용 대상:** 패키지 만들기 &bullet; **지원 되는 버전:** 4.6 +</span><span class="sxs-lookup"><span data-stu-id="99dd0-104">**Applies to:** package creation &bullet; **Supported versions:** 4.6+</span></span>

<span data-ttu-id="99dd0-105">인증서를 사용 하 여 첫 번째 인수를 일치 하는 모든 패키지에 서명 합니다.</span><span class="sxs-lookup"><span data-stu-id="99dd0-105">Signs all the packages matching the first argument with a certificate.</span></span> <span data-ttu-id="99dd0-106">주체 이름 또는 지문을 제공 하 여 인증서 저장소에 설치 된 인증서 또는 파일에서 개인 키를 사용 하 여 인증서를 가져올 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="99dd0-106">The certificate with the private key can be obtained from a file or from a certificate installed in a certificate store by providing a subject name or a thumbprint.</span></span>

<span data-ttu-id="99dd0-107">아직.NET Core, mono, 또는 Windows 이외의 플랫폼에서에서 패키지 서명이 지원 되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="99dd0-107">Package signing is not yet supported in .NET Core, under Mono, or on non-Windows platforms.</span></span>

## <a name="usage"></a><span data-ttu-id="99dd0-108">사용법</span><span class="sxs-lookup"><span data-stu-id="99dd0-108">Usage</span></span>

```cli
nuget sign <package(s)> [options]
```

<span data-ttu-id="99dd0-109">여기서 `<package(s)>` 는 하나 이상의 `.nupkg` 파일입니다.</span><span class="sxs-lookup"><span data-stu-id="99dd0-109">where `<package(s)>` is one or more `.nupkg` files.</span></span>

## <a name="options"></a><span data-ttu-id="99dd0-110">옵션</span><span class="sxs-lookup"><span data-stu-id="99dd0-110">Options</span></span>

| <span data-ttu-id="99dd0-111">옵션</span><span class="sxs-lookup"><span data-stu-id="99dd0-111">Option</span></span> | <span data-ttu-id="99dd0-112">설명</span><span class="sxs-lookup"><span data-stu-id="99dd0-112">Description</span></span> |
| --- | --- |
| <span data-ttu-id="99dd0-113">CertificateFingerprint</span><span class="sxs-lookup"><span data-stu-id="99dd0-113">CertificateFingerprint</span></span> | <span data-ttu-id="99dd0-114">인증서에 대 한 로컬 인증서 저장소를 검색에 사용 된 인증서의 SHA-1(secure 지문을 지정 합니다.</span><span class="sxs-lookup"><span data-stu-id="99dd0-114">Specifies the SHA-1 fingerprint of the certificate used to search a local certificate store for the certificate.</span></span> |
| <span data-ttu-id="99dd0-115">CertificatePassword</span><span class="sxs-lookup"><span data-stu-id="99dd0-115">CertificatePassword</span></span> | <span data-ttu-id="99dd0-116">필요한 경우 인증서 암호를 지정 합니다.</span><span class="sxs-lookup"><span data-stu-id="99dd0-116">Specifies the certificate password, if needed.</span></span> <span data-ttu-id="99dd0-117">인증서가 암호로 보호 없는 암호를 제공 하지만 명령을 암호를 묻는 런타임에 경우가 아니면-비 대화형 옵션에 전달 됩니다.</span><span class="sxs-lookup"><span data-stu-id="99dd0-117">If a certificate is password protected but no password is provided, the command will prompt for a password at run time, unless the -NonInteractive option is passed.</span></span> |
| <span data-ttu-id="99dd0-118">CertificatePath</span><span class="sxs-lookup"><span data-stu-id="99dd0-118">CertificatePath</span></span> | <span data-ttu-id="99dd0-119">패키지에 서명 하는 데 사용할 인증서 파일 경로 지정 합니다.</span><span class="sxs-lookup"><span data-stu-id="99dd0-119">Specifies the file path to the certificate to be used in signing the package.</span></span> |
| <span data-ttu-id="99dd0-120">CertificateStoreLocation</span><span class="sxs-lookup"><span data-stu-id="99dd0-120">CertificateStoreLocation</span></span> | <span data-ttu-id="99dd0-121">X.509 인증서 저장소를 사용 하 여 인증서에 대 한 검색의 이름을 지정 합니다.</span><span class="sxs-lookup"><span data-stu-id="99dd0-121">Specifies the name of the X.509 certificate store use to search for the certificate.</span></span> <span data-ttu-id="99dd0-122">기본값은 "CurrentUser", 현재 사용자가 사용 되는 X.509 인증서 저장소입니다.</span><span class="sxs-lookup"><span data-stu-id="99dd0-122">Defaults to "CurrentUser", the X.509 certificate store used by the current user.</span></span> <span data-ttu-id="99dd0-123">-CertificateSubjectName 또는-CertificateFingerprint 옵션을 통해 인증서를 지정 하는 경우이 옵션을 사용할 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="99dd0-123">This option should be used when specifying the certificate via -CertificateSubjectName or -CertificateFingerprint options.</span></span> |
| <span data-ttu-id="99dd0-124">CertificateStoreName</span><span class="sxs-lookup"><span data-stu-id="99dd0-124">CertificateStoreName</span></span> | <span data-ttu-id="99dd0-125">인증서를 검색 하는 데 X.509 인증서 저장소의 이름을 지정 합니다.</span><span class="sxs-lookup"><span data-stu-id="99dd0-125">Specifies the name of the X.509 certificate store to use to search for the certificate.</span></span> <span data-ttu-id="99dd0-126">기본값은 "My", 개인 인증서용 X.509 인증서 저장소입니다.</span><span class="sxs-lookup"><span data-stu-id="99dd0-126">Defaults to "My", the X.509 certificate store for personal certificates.</span></span> <span data-ttu-id="99dd0-127">-CertificateSubjectName 또는-CertificateFingerprint 옵션을 통해 인증서를 지정 하는 경우이 옵션을 사용할 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="99dd0-127">This option should be used when specifying the certificate via -CertificateSubjectName or -CertificateFingerprint options.</span></span> |
| <span data-ttu-id="99dd0-128">CertificateSubjectName</span><span class="sxs-lookup"><span data-stu-id="99dd0-128">CertificateSubjectName</span></span> | <span data-ttu-id="99dd0-129">인증서에 대 한 로컬 인증서 저장소를 검색 하는 데 사용 되는 인증서의 주체 이름을 지정 합니다.</span><span class="sxs-lookup"><span data-stu-id="99dd0-129">Specifies the subject name of the certificate used to search a local certificate store for the certificate.</span></span>  <span data-ttu-id="99dd0-130">검색은 다른 주체 값에 관계 없이 해당 문자열이 포함 된 주체 이름을 가진 모든 인증서를 찾습니다는 제공된 된 값을 사용 하 여 대/소문자 구분 문자열 비교.</span><span class="sxs-lookup"><span data-stu-id="99dd0-130">The search is a case-insensitive string comparison using the supplied value, which will find all certificates with the subject name containing that string, regardless of other subject values.</span></span>  <span data-ttu-id="99dd0-131">인증서 저장소 CertificateStoreName-및-CertificateStoreLocation 옵션에 지정할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="99dd0-131">The certificate store can be specified by -CertificateStoreName and -CertificateStoreLocation options.</span></span> |
| <span data-ttu-id="99dd0-132">ConfigFile</span><span class="sxs-lookup"><span data-stu-id="99dd0-132">ConfigFile</span></span> | <span data-ttu-id="99dd0-133">NuGet 구성 파일을 적용 합니다.</span><span class="sxs-lookup"><span data-stu-id="99dd0-133">The NuGet configuration file to apply.</span></span> <span data-ttu-id="99dd0-134">지정 하지 않으면 `%AppData%\NuGet\NuGet.Config` (Windows) 또는 `~/.nuget/NuGet/NuGet.Config` (Mac/Linux)가 사용 됩니다.</span><span class="sxs-lookup"><span data-stu-id="99dd0-134">If not specified, `%AppData%\NuGet\NuGet.Config` (Windows) or `~/.nuget/NuGet/NuGet.Config` (Mac/Linux) is used.</span></span>|
| <span data-ttu-id="99dd0-135">ForceEnglishOutput</span><span class="sxs-lookup"><span data-stu-id="99dd0-135">ForceEnglishOutput</span></span> | <span data-ttu-id="99dd0-136">고정 영어 기반 문화권을 사용 하 여 실행할 nuget.exe를 강제로 수행 합니다.</span><span class="sxs-lookup"><span data-stu-id="99dd0-136">Forces nuget.exe to run using an invariant, English-based culture.</span></span> |
| <span data-ttu-id="99dd0-137">HashAlgorithm</span><span class="sxs-lookup"><span data-stu-id="99dd0-137">HashAlgorithm</span></span> | <span data-ttu-id="99dd0-138">패키지에 서명 하는 데 사용할 해시 알고리즘입니다.</span><span class="sxs-lookup"><span data-stu-id="99dd0-138">Hash algorithm to be used to sign the package.</span></span> <span data-ttu-id="99dd0-139">기본값은 SHA256입니다.</span><span class="sxs-lookup"><span data-stu-id="99dd0-139">Defaults to SHA256.</span></span> |
| <span data-ttu-id="99dd0-140">도움말</span><span class="sxs-lookup"><span data-stu-id="99dd0-140">Help</span></span> | <span data-ttu-id="99dd0-141">도움말의 명령에 대 한 정보를 표시 합니다.</span><span class="sxs-lookup"><span data-stu-id="99dd0-141">Displays help information for the command.</span></span> |
| <span data-ttu-id="99dd0-142">NonInteractive</span><span class="sxs-lookup"><span data-stu-id="99dd0-142">NonInteractive</span></span> | <span data-ttu-id="99dd0-143">사용자 입력 또는 확인에 대 한 프롬프트를 표시 하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="99dd0-143">Suppresses prompts for user input or confirmations.</span></span> |
| <span data-ttu-id="99dd0-144">OutputDirectory</span><span class="sxs-lookup"><span data-stu-id="99dd0-144">OutputDirectory</span></span> | <span data-ttu-id="99dd0-145">서명된 된 패키지를 저장할 디렉터리를 지정 합니다.</span><span class="sxs-lookup"><span data-stu-id="99dd0-145">Specifies the directory where the signed package should be saved.</span></span> <span data-ttu-id="99dd0-146">기본적으로 서명된 된 패키지는 원본 패키지를 덮어씁니다.</span><span class="sxs-lookup"><span data-stu-id="99dd0-146">By default the original package is overwritten by the signed package.</span></span> |
| <span data-ttu-id="99dd0-147">덮어쓰기</span><span class="sxs-lookup"><span data-stu-id="99dd0-147">Overwrite</span></span> | <span data-ttu-id="99dd0-148">전환 덮어쓸 경우 현재 서명 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="99dd0-148">Switch to indicate if the current signature should be overwritten.</span></span> <span data-ttu-id="99dd0-149">기본적으로 패키지 서명을 이미 있으면 명령이 실패 합니다.</span><span class="sxs-lookup"><span data-stu-id="99dd0-149">By default the command will fail if the package already has a signature.</span></span> |
| <span data-ttu-id="99dd0-150">Timestamper</span><span class="sxs-lookup"><span data-stu-id="99dd0-150">Timestamper</span></span> | <span data-ttu-id="99dd0-151">RFC 3161 타임 스탬프 서버 URL입니다.</span><span class="sxs-lookup"><span data-stu-id="99dd0-151">URL to an RFC 3161 timestamping server.</span></span> |
| <span data-ttu-id="99dd0-152">TimestampHashAlgorithm</span><span class="sxs-lookup"><span data-stu-id="99dd0-152">TimestampHashAlgorithm</span></span> | <span data-ttu-id="99dd0-153">RFC 3161 타임 스탬프 서버에서 사용할 해시 알고리즘입니다.</span><span class="sxs-lookup"><span data-stu-id="99dd0-153">Hash algorithm to be used by the RFC 3161 timestamp server.</span></span> <span data-ttu-id="99dd0-154">기본값은 SHA256입니다.</span><span class="sxs-lookup"><span data-stu-id="99dd0-154">Defaults to SHA256.</span></span> |
| <span data-ttu-id="99dd0-155">자세한 정도</span><span class="sxs-lookup"><span data-stu-id="99dd0-155">Verbosity</span></span> | <span data-ttu-id="99dd0-156">출력에 표시 되는 세부 정보의 양을 지정: *정상적인*, *quiet*, *자세한*합니다.</span><span class="sxs-lookup"><span data-stu-id="99dd0-156">Specifies the amount of detail displayed in the output: *normal*, *quiet*, *detailed*.</span></span> |

## <a name="examples"></a><span data-ttu-id="99dd0-157">예제</span><span class="sxs-lookup"><span data-stu-id="99dd0-157">Examples</span></span>

```cli
nuget sign MyPackage.nupkg -Timestamper http://timestamp.test

nuget sign .\..\MyPackage.nupkg -Timestamper http://timestamp.test -OutputDirectory .\..\Signed
```