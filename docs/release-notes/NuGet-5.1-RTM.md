---
title: NuGet 5.1 RTM 릴리스 정보
description: 새로운 기능, 버그 수정 및 Dcr 포함 하 여 NuGet 5.1에 대 한 릴리스 정보입니다.
author: karann-msft
ms.author: karann
ms.date: 05/21/2019
ms.topic: conceptual
ms.openlocfilehash: 384145947b19af6577dc1255985df1a361c72bb5
ms.sourcegitcommit: 0dea3b153ef823230a9d5f38351b7cef057cb299
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/12/2019
ms.locfileid: "67842572"
---
# <a name="nuget-51-release-notes"></a><span data-ttu-id="0892f-103">NuGet 5.1 릴리스 정보</span><span class="sxs-lookup"><span data-stu-id="0892f-103">NuGet 5.1 Release Notes</span></span>

<span data-ttu-id="0892f-104">NuGet 배포 차량:</span><span class="sxs-lookup"><span data-stu-id="0892f-104">NuGet distribution vehicles:</span></span>

| <span data-ttu-id="0892f-105">NuGet 버전</span><span class="sxs-lookup"><span data-stu-id="0892f-105">NuGet version</span></span> | <span data-ttu-id="0892f-106">Visual Studio 버전에서 사용 가능</span><span class="sxs-lookup"><span data-stu-id="0892f-106">Available in Visual Studio version</span></span>| <span data-ttu-id="0892f-107">.NET SDK에서 사용 가능</span><span class="sxs-lookup"><span data-stu-id="0892f-107">Available in .NET SDK(s)</span></span>|
|:---|:---|:---|
| [<span data-ttu-id="0892f-108">**5.1.0**</span><span class="sxs-lookup"><span data-stu-id="0892f-108">**5.1.0**</span></span>](https://nuget.org/downloads) | [<span data-ttu-id="0892f-109">Visual Studio 2019 버전 16.1</span><span class="sxs-lookup"><span data-stu-id="0892f-109">Visual Studio 2019 version 16.1</span></span>](https://visualstudio.microsoft.com/downloads/) | <span data-ttu-id="0892f-110">[2.1.70X](https://dotnet.microsoft.com/download/dotnet-core/2.1)<sup>1</sup>, [2.2.30X](https://dotnet.microsoft.com/download/dotnet-core/2.2)<sup>2</sup></span><span class="sxs-lookup"><span data-stu-id="0892f-110">[2.1.70X](https://dotnet.microsoft.com/download/dotnet-core/2.1)<sup>1</sup>, [2.2.30X](https://dotnet.microsoft.com/download/dotnet-core/2.2)<sup>2</sup></span></span> |

<span data-ttu-id="0892f-111"><sup>1</sup>.NET Core 워크 로드를 사용 하 여 Visual Studio 2019와 함께 설치</span><span class="sxs-lookup"><span data-stu-id="0892f-111"><sup>1</sup>Installed with Visual Studio 2019 with .NET Core workload</span></span> 

<span data-ttu-id="0892f-112"><sup>2</sup>.NET Core 워크 로드를 사용 하 여 Visual Studio 2019를 사용 하 여 설치를 선택적으로 사용 가능</span><span class="sxs-lookup"><span data-stu-id="0892f-112"><sup>2</sup>Available as an optional install with Visual Studio 2019 with .NET Core workload</span></span>

## <a name="summary-whats-new-in-51"></a><span data-ttu-id="0892f-113">요약: 5.1의 새로운 기능</span><span class="sxs-lookup"><span data-stu-id="0892f-113">Summary: What's New in 5.1</span></span>

* <span data-ttu-id="0892f-114">CI/CD 워크플로에-를 사용 하 여 더 나은 통합 수 있도록 이미 있는 경우 패키지 푸시를 표시 하지 않으려면 지원 [#1630](https://github.com/NuGet/Home/issues/1630#issuecomment-483461100)</span><span class="sxs-lookup"><span data-stu-id="0892f-114">Support to skip a package push if it already exists to allow for better integration with CI/CD workflows - [#1630](https://github.com/NuGet/Home/issues/1630#issuecomment-483461100)</span></span>

* <span data-ttu-id="0892f-115">Visual Studio에는 이제 편리한 링크를 제공 된 패키지를 nuget.org 갤러리 페이지- [#5299](https://github.com/NuGet/Home/issues/5299#issuecomment-494458510)</span><span class="sxs-lookup"><span data-stu-id="0892f-115">Visual Studio now provides a convenient link to the the package's nuget.org gallery page - [#5299](https://github.com/NuGet/Home/issues/5299#issuecomment-494458510)</span></span>

* <span data-ttu-id="0892f-116">와 같은 새.NET Core 3.0 자산에 대 한 지원 [타기 팅 팩](https://github.com/dotnet/cli/issues/10006) 고 [런타임 팩](https://github.com/dotnet/cli/issues/10007)</span><span class="sxs-lookup"><span data-stu-id="0892f-116">Support for new .NET Core 3.0 assets such as [Targeting Packs](https://github.com/dotnet/cli/issues/10006) and [Runtime Packs](https://github.com/dotnet/cli/issues/10007)</span></span>
  * <span data-ttu-id="0892f-117">NuGet pack 및 restore 대상 지정 및 런타임 패키지 참조를 사용 하도록 설정 하려면 FrameworkReferences 지원 [#7342](https://github.com/NuGet/Home/issues/7342)</span><span class="sxs-lookup"><span data-stu-id="0892f-117">NuGet pack and restore support for FrameworkReferences to enable targeting and runtime package references - [#7342](https://github.com/NuGet/Home/issues/7342)</span></span>
  * <span data-ttu-id="0892f-118">지원 PackageDownload-를 사용 하 여 패키지 시나리오 "다운로드" [#7339](https://github.com/NuGet/Home/issues/7339)</span><span class="sxs-lookup"><span data-stu-id="0892f-118">Support "download only" package scenario with PackageDownload - [#7339](https://github.com/NuGet/Home/issues/7339)</span></span>
  * <span data-ttu-id="0892f-119">Exlcude 런타임 및 타기 팅 팩이 복원 검색 결과에서 그래프를 사용 하 여 PackageType- [#7337](https://github.com/NuGet/Home/issues/7337)</span><span class="sxs-lookup"><span data-stu-id="0892f-119">Exlcude runtime and targeting packs from search results & restore graph using PackageType - [#7337](https://github.com/NuGet/Home/issues/7337)</span></span>

### <a name="issues-fixed-in-this-release"></a><span data-ttu-id="0892f-120">이번 릴리스에서 수정된 문제</span><span class="sxs-lookup"><span data-stu-id="0892f-120">Issues fixed in this release</span></span>

<span data-ttu-id="0892f-121">**버그**</span><span class="sxs-lookup"><span data-stu-id="0892f-121">**Bugs**</span></span>

* <span data-ttu-id="0892f-122">플러그 인: 플러그 인 만들기 중 예외 정보 손실 [#8057](https://github.com/NuGet/Home/issues/8057)</span><span class="sxs-lookup"><span data-stu-id="0892f-122">Plugins:  exception details lost during plugin creation - [#8057](https://github.com/NuGet/Home/issues/8057)</span></span>

* <span data-ttu-id="0892f-123">단독 하한값을 사용 하 여 PackageReference 범위 하한값 원본 중 하나에 있는 경우 작동 하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="0892f-123">PackageReference range with exclusive lower bound does not work if the lower bound is present on one of the sources.</span></span><span data-ttu-id="0892f-124"> - [#8054](https://github.com/NuGet/Home/issues/8054)</span><span class="sxs-lookup"><span data-stu-id="0892f-124"> - [#8054](https://github.com/NuGet/Home/issues/8054)</span></span>

* <span data-ttu-id="0892f-125">IsPackableFalseError 메시지 개선 [#8021](https://github.com/NuGet/Home/issues/8021)</span><span class="sxs-lookup"><span data-stu-id="0892f-125">Improve IsPackableFalseError message - [#8021](https://github.com/NuGet/Home/issues/8021)</span></span>

* <span data-ttu-id="0892f-126">-프로젝트 그래프 변경 될 때 파일 다시 생성 잠금-잠금 파일 [#8019](https://github.com/NuGet/Home/issues/8019)</span><span class="sxs-lookup"><span data-stu-id="0892f-126">Packages Lock File - regenerate lock file when project graph changes - [#8019](https://github.com/NuGet/Home/issues/8019)</span></span>

* <span data-ttu-id="0892f-127">ProjectSystem 버그: 자동 시작 하는 Nuget 패키지 제거- [#8017](https://github.com/NuGet/Home/issues/8017)</span><span class="sxs-lookup"><span data-stu-id="0892f-127">ProjectSystem bug: Nuget Packages getting auto removed - [#8017](https://github.com/NuGet/Home/issues/8017)</span></span>

* <span data-ttu-id="0892f-128">FrameworkReference 반환에 대 한 대상을 추가 CollectPackageDownloads 및 CollectPackageReferences-비슷합니다 [#8005](https://github.com/NuGet/Home/issues/8005)</span><span class="sxs-lookup"><span data-stu-id="0892f-128">Add a target for returning the FrameworkReference similar to CollectPackageDownloads and CollectPackageReferences - [#8005](https://github.com/NuGet/Home/issues/8005)</span></span>

* <span data-ttu-id="0892f-129">HTTP 캐시:  RepositoryResources 리소스 버전 관리 방식-캐시 되지 [#7997](https://github.com/NuGet/Home/issues/7997)</span><span class="sxs-lookup"><span data-stu-id="0892f-129">HTTP cache:  RepositoryResources resource is not cached in a versioned way - [#7997](https://github.com/NuGet/Home/issues/7997)</span></span>

* <span data-ttu-id="0892f-130">로깅: 예외 호출 스택 세부 자세한 정도-를 사용 하 여 보고 되지 않습니다 [#7955](https://github.com/NuGet/Home/issues/7955)</span><span class="sxs-lookup"><span data-stu-id="0892f-130">Logging:  exception callstacks are not reported with detailed verbosity - [#7955](https://github.com/NuGet/Home/issues/7955)</span></span>

* <span data-ttu-id="0892f-131">-HTTPS를 사용 하도록 모든 NuGet Docs Url 변경 [#7950](https://github.com/NuGet/Home/issues/7950)</span><span class="sxs-lookup"><span data-stu-id="0892f-131">Change all NuGet Docs URLs to use HTTPS - [#7950](https://github.com/NuGet/Home/issues/7950)</span></span>

* <span data-ttu-id="0892f-132">NU3024 경고 메시지 개선 [#7933](https://github.com/NuGet/Home/issues/7933)</span><span class="sxs-lookup"><span data-stu-id="0892f-132">Improve NU3024 warning message - [#7933](https://github.com/NuGet/Home/issues/7933)</span></span>

* <span data-ttu-id="0892f-133">잠금 파일 업데이트 되지 않는 경우 제거 하는 packagereference [#7930](https://github.com/NuGet/Home/issues/7930)</span><span class="sxs-lookup"><span data-stu-id="0892f-133">lock file not updating when packagereference removed - [#7930](https://github.com/NuGet/Home/issues/7930)</span></span>

* <span data-ttu-id="0892f-134">Nuspec-의 licenseurl 및 라이선스 요소의 유효성을 검사 하는 경우 오류 사례 처리 향상 [#7915](https://github.com/NuGet/Home/issues/7915)</span><span class="sxs-lookup"><span data-stu-id="0892f-134">Improve the error case handling when validating licenseurl and license element in nuspec - [#7915](https://github.com/NuGet/Home/issues/7915)</span></span>

* <span data-ttu-id="0892f-135">탭 헤더에 오류가-발생 클릭 "파일 위치 열기" PM UI-마우스 오른쪽 단추로 클릭 [#7913](https://github.com/NuGet/Home/issues/7913)</span><span class="sxs-lookup"><span data-stu-id="0892f-135">PM UI - right click on tab header and clicking "Open file location" results in error - [#7913](https://github.com/NuGet/Home/issues/7913)</span></span>

* <span data-ttu-id="0892f-136">플러그 인:-플러그 인 프로세스를 종료 하는 경우 로그 [#7907](https://github.com/NuGet/Home/issues/7907)</span><span class="sxs-lookup"><span data-stu-id="0892f-136">Plugins:  log when plugin process exits - [#7907](https://github.com/NuGet/Home/issues/7907)</span></span>

* <span data-ttu-id="0892f-137">플러그 인: 로깅 날짜/시간 값에서 높은 충돌 비율 [#7899](https://github.com/NuGet/Home/issues/7899)</span><span class="sxs-lookup"><span data-stu-id="0892f-137">Plugins:  high collision rate in logging datetime values - [#7899](https://github.com/NuGet/Home/issues/7899)</span></span>

* <span data-ttu-id="0892f-138">Manifest.ReadFrom LicenseExpression-를 사용 하 여 모든 nuspec에서 실패 [#7894](https://github.com/NuGet/Home/issues/7894)</span><span class="sxs-lookup"><span data-stu-id="0892f-138">Manifest.ReadFrom fails on any nuspec with LicenseExpression - [#7894](https://github.com/NuGet/Home/issues/7894)</span></span>

* <span data-ttu-id="0892f-139">RestoreLockedMode: ProjectReference 사용자 지정 AssemblyName-를 사용 하 여 프로젝트를 참조할 때 예기치 않은 NU1004 [#7889](https://github.com/NuGet/Home/issues/7889)</span><span class="sxs-lookup"><span data-stu-id="0892f-139">RestoreLockedMode: Unexpected NU1004 when ProjectReference refers to a project with custom AssemblyName - [#7889](https://github.com/NuGet/Home/issues/7889)</span></span>

* <span data-ttu-id="0892f-140">플러그 인 시작 실패-예외가 발생 하는 경우 더 나은 오류 메시지가 [#7857](https://github.com/NuGet/Home/issues/7857)</span><span class="sxs-lookup"><span data-stu-id="0892f-140">Better error message when the plugin startup fails with an exception - [#7857](https://github.com/NuGet/Home/issues/7857)</span></span>

* <span data-ttu-id="0892f-141">방지 NoOp 복원 작업을 수행 하는 경우 \*. obj 디렉터리-dgspec.json 쓰기 [#7854](https://github.com/NuGet/Home/issues/7854)</span><span class="sxs-lookup"><span data-stu-id="0892f-141">When doing a NoOp restore, avoid \*.dgspec.json write in obj directory - [#7854](https://github.com/NuGet/Home/issues/7854)</span></span>

* <span data-ttu-id="0892f-142">GeneratePathProperty 사례 일치 하지 않아서에서 속성을 생성 하는 true 실패 = [#7843](https://github.com/NuGet/Home/issues/7843)</span><span class="sxs-lookup"><span data-stu-id="0892f-142">GeneratePathProperty=true fails to generate property on case mismatch - [#7843](https://github.com/NuGet/Home/issues/7843)</span></span>

* <span data-ttu-id="0892f-143">설정: 패키지 원본 경로에 잘못 된 문자가-VS와 충돌할 수 있다 [#7820](https://github.com/NuGet/Home/issues/7820)</span><span class="sxs-lookup"><span data-stu-id="0892f-143">Settings:  illegal character in package source path can crash VS - [#7820](https://github.com/NuGet/Home/issues/7820)</span></span>

* <span data-ttu-id="0892f-144">복원-NoOp에 잠금 파일을 생성 하지 않습니다 잠금 파일 삭제 되 면 [#7807](https://github.com/NuGet/Home/issues/7807)</span><span class="sxs-lookup"><span data-stu-id="0892f-144">If lock file is deleted, restore does not generate lock file on NoOp  - [#7807](https://github.com/NuGet/Home/issues/7807)</span></span>

* <span data-ttu-id="0892f-145">라이선스 URL 및 읽기-메타 데이터를 사용 하 여 오류 라이선스 원인 [#7547](https://github.com/NuGet/Home/issues/7547)</span><span class="sxs-lookup"><span data-stu-id="0892f-145">License URL and license causes read error with Metadata - [#7547](https://github.com/NuGet/Home/issues/7547)</span></span>

* <span data-ttu-id="0892f-146">처리 되지 않은 예외가 V2FeedParser- [#7523](https://github.com/NuGet/Home/issues/7523)</span><span class="sxs-lookup"><span data-stu-id="0892f-146">Unhandled exceptions in V2FeedParser - [#7523](https://github.com/NuGet/Home/issues/7523)</span></span>

* <span data-ttu-id="0892f-147">잘못 된 인수-에 대 한 종료 코드 0을 반환 하는 nuget.exe [#7178](https://github.com/NuGet/Home/issues/7178)</span><span class="sxs-lookup"><span data-stu-id="0892f-147">nuget.exe returns exit code zero for invalid arguments - [#7178](https://github.com/NuGet/Home/issues/7178)</span></span>

* <span data-ttu-id="0892f-148">오류 및 경고 문서 서명 관련된 시나리오에 맞게 업데이트 [#6498](https://github.com/NuGet/Home/issues/6498)</span><span class="sxs-lookup"><span data-stu-id="0892f-148">Update Errors and warning docs to reflect signing related scenarios - [#6498](https://github.com/NuGet/Home/issues/6498)</span></span>

* <span data-ttu-id="0892f-149">자산 파일 상대 경로 사용 하 여 이동 프로젝트를 더 쉽게 사용 하도록 설정 해야 [#4582](https://github.com/NuGet/Home/issues/4582)</span><span class="sxs-lookup"><span data-stu-id="0892f-149">Assets file should use relative paths to enable moving projects more easily - [#4582](https://github.com/NuGet/Home/issues/4582)</span></span>

<span data-ttu-id="0892f-150">**DCRs**</span><span class="sxs-lookup"><span data-stu-id="0892f-150">**DCRs**</span></span>

* <span data-ttu-id="0892f-151">플러그 인: 진단 로깅을- [#7859](https://github.com/NuGet/Home/issues/7859)</span><span class="sxs-lookup"><span data-stu-id="0892f-151">Plugins:  enable diagnostic logging - [#7859](https://github.com/NuGet/Home/issues/7859)</span></span>

* <span data-ttu-id="0892f-152">확인 Tizen 6 매핑할 NetStandard 2.1- [#7773](https://github.com/NuGet/Home/issues/7773)</span><span class="sxs-lookup"><span data-stu-id="0892f-152">Make Tizen 6 map to NetStandard 2.1 - [#7773](https://github.com/NuGet/Home/issues/7773)</span></span>

<span data-ttu-id="0892f-153">**[이 릴리스에 5.1 RTM에서 수정 된 모든 문제 목록](https://github.com/nuget/home/issues?q=is%3Aissue+is%3Aclosed+milestone%3A%225.1")**</span><span class="sxs-lookup"><span data-stu-id="0892f-153">**[List of all issues fixed in this release - 5.1 RTM](https://github.com/nuget/home/issues?q=is%3Aissue+is%3Aclosed+milestone%3A%225.1")**</span></span>
