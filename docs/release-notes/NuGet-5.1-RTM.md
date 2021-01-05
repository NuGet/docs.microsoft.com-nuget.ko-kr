---
title: NuGet 5.1 RTM 릴리스 정보
description: 새 기능, 버그 수정 및 Ecrs를 비롯 한 NuGet 5.1에 대 한 릴리스 정보입니다.
author: karann-msft
ms.author: karann
ms.date: 05/21/2019
ms.topic: conceptual
ms.openlocfilehash: 2a94360dc375ba90b90c1045f4acbcfca81fea5b
ms.sourcegitcommit: 53b06e27bcfef03500a69548ba2db069b55837f1
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 12/19/2020
ms.locfileid: "97699864"
---
# <a name="nuget-51-release-notes"></a><span data-ttu-id="d5f9e-103">NuGet 5.1 릴리스 정보</span><span class="sxs-lookup"><span data-stu-id="d5f9e-103">NuGet 5.1 Release Notes</span></span>

<span data-ttu-id="d5f9e-104">NuGet 배포 차량:</span><span class="sxs-lookup"><span data-stu-id="d5f9e-104">NuGet distribution vehicles:</span></span>

| <span data-ttu-id="d5f9e-105">NuGet 버전</span><span class="sxs-lookup"><span data-stu-id="d5f9e-105">NuGet version</span></span> | <span data-ttu-id="d5f9e-106">Visual Studio 버전에서 사용 가능</span><span class="sxs-lookup"><span data-stu-id="d5f9e-106">Available in Visual Studio version</span></span>| <span data-ttu-id="d5f9e-107">.NET SDK에서 사용 가능</span><span class="sxs-lookup"><span data-stu-id="d5f9e-107">Available in .NET SDK(s)</span></span>|
|:---|:---|:---|
| [<span data-ttu-id="d5f9e-108">**5.1.0**</span><span class="sxs-lookup"><span data-stu-id="d5f9e-108">**5.1.0**</span></span>](https://nuget.org/downloads) | [<span data-ttu-id="d5f9e-109">Visual Studio 2019 버전 16.1</span><span class="sxs-lookup"><span data-stu-id="d5f9e-109">Visual Studio 2019 version 16.1</span></span>](https://visualstudio.microsoft.com/downloads/) | <span data-ttu-id="d5f9e-110">[2.1.70 x](https://dotnet.microsoft.com/download/dotnet-core/2.1)<sup>1</sup>, [2.2.30 x](https://dotnet.microsoft.com/download/dotnet-core/2.2)<sup>2</sup></span><span class="sxs-lookup"><span data-stu-id="d5f9e-110">[2.1.70X](https://dotnet.microsoft.com/download/dotnet-core/2.1)<sup>1</sup>, [2.2.30X](https://dotnet.microsoft.com/download/dotnet-core/2.2)<sup>2</sup></span></span> |

<span data-ttu-id="d5f9e-111"><sup>1</sup> .NET Core 워크 로드와 함께 Visual Studio 2019와 함께 설치 됨</span><span class="sxs-lookup"><span data-stu-id="d5f9e-111"><sup>1</sup>Installed with Visual Studio 2019 with .NET Core workload</span></span> 

<span data-ttu-id="d5f9e-112"><sup>2</sup> .NET Core 워크 로드와 함께 Visual Studio 2019을 사용 하 여 선택적으로 설치할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="d5f9e-112"><sup>2</sup>Available as an optional install with Visual Studio 2019 with .NET Core workload</span></span>

## <a name="summary-whats-new-in-51"></a><span data-ttu-id="d5f9e-113">요약: 5.1의 새로운 기능</span><span class="sxs-lookup"><span data-stu-id="d5f9e-113">Summary: What's New in 5.1</span></span>

* <span data-ttu-id="d5f9e-114">CI/CD 워크플로와의 통합이 가능 하도록 패키지 푸시가 이미 있는 경우이를 건너뛰도록 지원- [#1630](https://github.com/NuGet/Home/issues/1630#issuecomment-483461100)</span><span class="sxs-lookup"><span data-stu-id="d5f9e-114">Support to skip a package push if it already exists to allow for better integration with CI/CD workflows - [#1630](https://github.com/NuGet/Home/issues/1630#issuecomment-483461100)</span></span>

* <span data-ttu-id="d5f9e-115">이제 Visual Studio에서 패키지의 nuget.org 갤러리 페이지에 대 한 편리한 링크를 제공 [#5299](https://github.com/NuGet/Home/issues/5299#issuecomment-494458510)</span><span class="sxs-lookup"><span data-stu-id="d5f9e-115">Visual Studio now provides a convenient link to the the package's nuget.org gallery page - [#5299](https://github.com/NuGet/Home/issues/5299#issuecomment-494458510)</span></span>

* <span data-ttu-id="d5f9e-116">새 .NET Core 3.0 자산에 대 한 지원 (예: [대상 팩](https://github.com/dotnet/cli/issues/10006) 및 [런타임 팩](https://github.com/dotnet/cli/issues/10007) )</span><span class="sxs-lookup"><span data-stu-id="d5f9e-116">Support for new .NET Core 3.0 assets such as [Targeting Packs](https://github.com/dotnet/cli/issues/10006) and [Runtime Packs](https://github.com/dotnet/cli/issues/10007)</span></span>
  * <span data-ttu-id="d5f9e-117">FrameworkReferences에서 대상 지정 및 런타임 패키지 참조를 사용할 수 있도록 하는 NuGet 팩 및 복원 지원- [#7342](https://github.com/NuGet/Home/issues/7342)</span><span class="sxs-lookup"><span data-stu-id="d5f9e-117">NuGet pack and restore support for FrameworkReferences to enable targeting and runtime package references - [#7342](https://github.com/NuGet/Home/issues/7342)</span></span>
  * <span data-ttu-id="d5f9e-118">PackageDownload를 사용 하 여 "다운로드 전용" 패키지 시나리오를 지원 [#7339](https://github.com/NuGet/Home/issues/7339)</span><span class="sxs-lookup"><span data-stu-id="d5f9e-118">Support "download only" package scenario with PackageDownload - [#7339](https://github.com/NuGet/Home/issues/7339)</span></span>
  * <span data-ttu-id="d5f9e-119">PackageType를 사용 하 여 & 복원 그래프 검색 결과에서 런타임 및 대상 팩을 제외 [#7337](https://github.com/NuGet/Home/issues/7337)</span><span class="sxs-lookup"><span data-stu-id="d5f9e-119">Exclude runtime and targeting packs from search results & restore graph using PackageType - [#7337](https://github.com/NuGet/Home/issues/7337)</span></span>

### <a name="issues-fixed-in-this-release"></a><span data-ttu-id="d5f9e-120">이번 릴리스에서 수정된 문제</span><span class="sxs-lookup"><span data-stu-id="d5f9e-120">Issues fixed in this release</span></span>

<span data-ttu-id="d5f9e-121">**버그**</span><span class="sxs-lookup"><span data-stu-id="d5f9e-121">**Bugs**</span></span>

* <span data-ttu-id="d5f9e-122">플러그 인: 플러그 인을 만드는 동안 예외 정보 손실- [#8057](https://github.com/NuGet/Home/issues/8057)</span><span class="sxs-lookup"><span data-stu-id="d5f9e-122">Plugins:  exception details lost during plugin creation - [#8057](https://github.com/NuGet/Home/issues/8057)</span></span>

* <span data-ttu-id="d5f9e-123">하한값이 원본 중 하나에 있는 경우에는 하 한이 아닌 PackageReference 범위가 작동 하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="d5f9e-123">PackageReference range with exclusive lower bound does not work if the lower bound is present on one of the sources.</span></span><span data-ttu-id="d5f9e-124"> - [#8054](https://github.com/NuGet/Home/issues/8054)</span><span class="sxs-lookup"><span data-stu-id="d5f9e-124"> - [#8054](https://github.com/NuGet/Home/issues/8054)</span></span>

* <span data-ttu-id="d5f9e-125">IsPackableFalseError 메시지 개선- [#8021](https://github.com/NuGet/Home/issues/8021)</span><span class="sxs-lookup"><span data-stu-id="d5f9e-125">Improve IsPackableFalseError message - [#8021](https://github.com/NuGet/Home/issues/8021)</span></span>

* <span data-ttu-id="d5f9e-126">패키지 잠금 파일-프로젝트 그래프가 변경 될 때 잠금 파일 다시 생성- [#8019](https://github.com/NuGet/Home/issues/8019)</span><span class="sxs-lookup"><span data-stu-id="d5f9e-126">Packages Lock File - regenerate lock file when project graph changes - [#8019](https://github.com/NuGet/Home/issues/8019)</span></span>

* <span data-ttu-id="d5f9e-127">ProjectSystem 버그: 자동으로 제거 되는 Nuget 패키지- [#8017](https://github.com/NuGet/Home/issues/8017)</span><span class="sxs-lookup"><span data-stu-id="d5f9e-127">ProjectSystem bug: Nuget Packages getting auto removed - [#8017](https://github.com/NuGet/Home/issues/8017)</span></span>

* <span data-ttu-id="d5f9e-128">CollectPackageDownloads 및 CollectPackageReferences와 유사한 FrameworkReference를 반환 하기 위한 대상을 추가 [#8005](https://github.com/NuGet/Home/issues/8005)</span><span class="sxs-lookup"><span data-stu-id="d5f9e-128">Add a target for returning the FrameworkReference similar to CollectPackageDownloads and CollectPackageReferences - [#8005](https://github.com/NuGet/Home/issues/8005)</span></span>

* <span data-ttu-id="d5f9e-129">HTTP 캐시: RepositoryResources 리소스는 버전이 지정 된 방식으로 캐시 되지 않습니다.- [#7997](https://github.com/NuGet/Home/issues/7997)</span><span class="sxs-lookup"><span data-stu-id="d5f9e-129">HTTP cache:  RepositoryResources resource is not cached in a versioned way - [#7997](https://github.com/NuGet/Home/issues/7997)</span></span>

* <span data-ttu-id="d5f9e-130">로깅: 예외 호출 스택 상세 세부 정보 표시로 보고 되지 않습니다. [#7955](https://github.com/NuGet/Home/issues/7955)</span><span class="sxs-lookup"><span data-stu-id="d5f9e-130">Logging:  exception callstacks are not reported with detailed verbosity - [#7955](https://github.com/NuGet/Home/issues/7955)</span></span>

* <span data-ttu-id="d5f9e-131">모든 NuGet 문서 Url을 변경 하 여 HTTPS를 사용 합니다. [#7950](https://github.com/NuGet/Home/issues/7950)</span><span class="sxs-lookup"><span data-stu-id="d5f9e-131">Change all NuGet Docs URLs to use HTTPS - [#7950](https://github.com/NuGet/Home/issues/7950)</span></span>

* <span data-ttu-id="d5f9e-132">NU3024 경고 메시지 개선- [#7933](https://github.com/NuGet/Home/issues/7933)</span><span class="sxs-lookup"><span data-stu-id="d5f9e-132">Improve NU3024 warning message - [#7933](https://github.com/NuGet/Home/issues/7933)</span></span>

* <span data-ttu-id="d5f9e-133">packagereference 제거 될 때 잠금 파일 업데이트 안 함- [#7930](https://github.com/NuGet/Home/issues/7930)</span><span class="sxs-lookup"><span data-stu-id="d5f9e-133">lock file not updating when packagereference removed - [#7930](https://github.com/NuGet/Home/issues/7930)</span></span>

* <span data-ttu-id="d5f9e-134">Nuspec에서 licenseurl 및 license 요소의 유효성을 검사할 때 오류 사례 처리를 향상 시킵니다 [#7915](https://github.com/NuGet/Home/issues/7915)</span><span class="sxs-lookup"><span data-stu-id="d5f9e-134">Improve the error case handling when validating licenseurl and license element in nuspec - [#7915](https://github.com/NuGet/Home/issues/7915)</span></span>

* <span data-ttu-id="d5f9e-135">PM UI-탭 헤더를 마우스 오른쪽 단추로 클릭 하 고 "파일 위치 열기"를 클릭 하면 오류가 발생 합니다. [#7913](https://github.com/NuGet/Home/issues/7913)</span><span class="sxs-lookup"><span data-stu-id="d5f9e-135">PM UI - right click on tab header and clicking "Open file location" results in error - [#7913](https://github.com/NuGet/Home/issues/7913)</span></span>

* <span data-ttu-id="d5f9e-136">플러그 인: 플러그 인 프로세스가 종료 될 때 기록- [#7907](https://github.com/NuGet/Home/issues/7907)</span><span class="sxs-lookup"><span data-stu-id="d5f9e-136">Plugins:  log when plugin process exits - [#7907](https://github.com/NuGet/Home/issues/7907)</span></span>

* <span data-ttu-id="d5f9e-137">플러그 인: datetime 값 로깅의 높은 충돌 률- [#7899](https://github.com/NuGet/Home/issues/7899)</span><span class="sxs-lookup"><span data-stu-id="d5f9e-137">Plugins:  high collision rate in logging datetime values - [#7899](https://github.com/NuGet/Home/issues/7899)</span></span>

* <span data-ttu-id="d5f9e-138">매니페스트. [#7894](https://github.com/NuGet/Home/issues/7894) LicenseExpression를 사용 하 여 Nuspec에서 readfrom이 실패 합니다.</span><span class="sxs-lookup"><span data-stu-id="d5f9e-138">Manifest.ReadFrom fails on any nuspec with LicenseExpression - [#7894](https://github.com/NuGet/Home/issues/7894)</span></span>

* <span data-ttu-id="d5f9e-139">RestoreLockedMode: ProjectReference가 사용자 지정 AssemblyName- [#7889](https://github.com/NuGet/Home/issues/7889) 프로젝트를 참조 하는 경우 예기치 않은 NU1004</span><span class="sxs-lookup"><span data-stu-id="d5f9e-139">RestoreLockedMode: Unexpected NU1004 when ProjectReference refers to a project with custom AssemblyName - [#7889](https://github.com/NuGet/Home/issues/7889)</span></span>

* <span data-ttu-id="d5f9e-140">예외가 발생 하 여 플러그 인 시작이 실패할 경우 더 나은 오류 메시지 [#7857](https://github.com/NuGet/Home/issues/7857)</span><span class="sxs-lookup"><span data-stu-id="d5f9e-140">Better error message when the plugin startup fails with an exception - [#7857](https://github.com/NuGet/Home/issues/7857)</span></span>

* <span data-ttu-id="d5f9e-141">NoOp 복원 작업을 수행 하는 경우에는 .dgspec.js[#7854](https://github.com/NuGet/Home/issues/7854) obj 디렉터리에 쓸 필요가 없습니다.</span><span class="sxs-lookup"><span data-stu-id="d5f9e-141">When doing a NoOp restore, avoid \*.dgspec.json write in obj directory - [#7854](https://github.com/NuGet/Home/issues/7854)</span></span>

* <span data-ttu-id="d5f9e-142">GeneratePathProperty = true 인 경우 대/소문자 불일치 시 속성이 생성 되지 않습니다.- [#7843](https://github.com/NuGet/Home/issues/7843)</span><span class="sxs-lookup"><span data-stu-id="d5f9e-142">GeneratePathProperty=true fails to generate property on case mismatch - [#7843](https://github.com/NuGet/Home/issues/7843)</span></span>

* <span data-ttu-id="d5f9e-143">설정: 패키지 원본 경로에 잘못 된 문자가 있을 수 있습니다. VS- [#7820](https://github.com/NuGet/Home/issues/7820)</span><span class="sxs-lookup"><span data-stu-id="d5f9e-143">Settings:  illegal character in package source path can crash VS - [#7820](https://github.com/NuGet/Home/issues/7820)</span></span>

* <span data-ttu-id="d5f9e-144">잠금 파일이 삭제 된 경우 NoOp- [#7807](https://github.com/NuGet/Home/issues/7807) 에서 잠금 파일을 생성 하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="d5f9e-144">If lock file is deleted, restore does not generate lock file on NoOp  - [#7807](https://github.com/NuGet/Home/issues/7807)</span></span>

* <span data-ttu-id="d5f9e-145">라이선스 URL 및 라이선스 때문에 메타 데이터를 읽는 동안 오류가 발생 했습니다.- [#7547](https://github.com/NuGet/Home/issues/7547)</span><span class="sxs-lookup"><span data-stu-id="d5f9e-145">License URL and license causes read error with Metadata - [#7547](https://github.com/NuGet/Home/issues/7547)</span></span>

* <span data-ttu-id="d5f9e-146">V2FeedParser의 처리 되지 않은 예외- [#7523](https://github.com/NuGet/Home/issues/7523)</span><span class="sxs-lookup"><span data-stu-id="d5f9e-146">Unhandled exceptions in V2FeedParser - [#7523](https://github.com/NuGet/Home/issues/7523)</span></span>

* <span data-ttu-id="d5f9e-147">잘못 된 인수에 대 한 nuget.exe 종료 코드 0을 반환 합니다. [#7178](https://github.com/NuGet/Home/issues/7178)</span><span class="sxs-lookup"><span data-stu-id="d5f9e-147">nuget.exe returns exit code zero for invalid arguments - [#7178](https://github.com/NuGet/Home/issues/7178)</span></span>

* <span data-ttu-id="d5f9e-148">서명 관련 시나리오를 반영 하 여 오류 및 경고 문서 업데이트- [#6498](https://github.com/NuGet/Home/issues/6498)</span><span class="sxs-lookup"><span data-stu-id="d5f9e-148">Update Errors and warning docs to reflect signing related scenarios - [#6498](https://github.com/NuGet/Home/issues/6498)</span></span>

* <span data-ttu-id="d5f9e-149">자산 파일은 상대 경로를 사용 하 여 프로젝트를 보다 쉽게 이동할 수 있도록 합니다. [#4582](https://github.com/NuGet/Home/issues/4582)</span><span class="sxs-lookup"><span data-stu-id="d5f9e-149">Assets file should use relative paths to enable moving projects more easily - [#4582](https://github.com/NuGet/Home/issues/4582)</span></span>

<span data-ttu-id="d5f9e-150">**DCR**</span><span class="sxs-lookup"><span data-stu-id="d5f9e-150">**DCRs**</span></span>

* <span data-ttu-id="d5f9e-151">플러그 인: 진단 로깅 사용- [#7859](https://github.com/NuGet/Home/issues/7859)</span><span class="sxs-lookup"><span data-stu-id="d5f9e-151">Plugins:  enable diagnostic logging - [#7859](https://github.com/NuGet/Home/issues/7859)</span></span>

* <span data-ttu-id="d5f9e-152">Tizen 6 map을 NetStandard 2.1로 설정- [#7773](https://github.com/NuGet/Home/issues/7773)</span><span class="sxs-lookup"><span data-stu-id="d5f9e-152">Make Tizen 6 map to NetStandard 2.1 - [#7773](https://github.com/NuGet/Home/issues/7773)</span></span>

<span data-ttu-id="d5f9e-153">**[이 릴리스에서 해결 된 모든 문제 목록-5.1 RTM](https://github.com/nuget/home/issues?q=is%3Aissue+is%3Aclosed+milestone%3A%225.1")**</span><span class="sxs-lookup"><span data-stu-id="d5f9e-153">**[List of all issues fixed in this release - 5.1 RTM](https://github.com/nuget/home/issues?q=is%3Aissue+is%3Aclosed+milestone%3A%225.1")**</span></span>
