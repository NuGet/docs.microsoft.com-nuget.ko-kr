---
title: NuGet 5.3 릴리스 정보
description: 새 기능, 버그 수정 및 Ecrs를 비롯 한 NuGet 5.3에 대 한 릴리스 정보입니다.
author: karann-msft
ms.author: karann
ms.date: 09/06/2019
ms.topic: conceptual
ms.openlocfilehash: f16bfe5481009f7924a61f03233d288d25ac618f
ms.sourcegitcommit: f4bfdbf62302c95f1f39e81ccf998f8bbc6d56b0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 09/06/2019
ms.locfileid: "70774088"
---
# <a name="nuget-53-release-notes"></a><span data-ttu-id="fcd08-103">NuGet 5.3 릴리스 정보</span><span class="sxs-lookup"><span data-stu-id="fcd08-103">NuGet 5.3 Release Notes</span></span>

<span data-ttu-id="fcd08-104">NuGet 배포 차량:</span><span class="sxs-lookup"><span data-stu-id="fcd08-104">NuGet distribution vehicles:</span></span>

| <span data-ttu-id="fcd08-105">NuGet 버전</span><span class="sxs-lookup"><span data-stu-id="fcd08-105">NuGet version</span></span> | <span data-ttu-id="fcd08-106">Visual Studio 버전에서 사용 가능</span><span class="sxs-lookup"><span data-stu-id="fcd08-106">Available in Visual Studio version</span></span>| <span data-ttu-id="fcd08-107">.NET SDK에서 사용 가능</span><span class="sxs-lookup"><span data-stu-id="fcd08-107">Available in .NET SDK(s)</span></span>|
|:---|:---|:---|
| [<span data-ttu-id="fcd08-108">**5.3.0-preview3**</span><span class="sxs-lookup"><span data-stu-id="fcd08-108">**5.3.0-preview3**</span></span>](https://nuget.org/downloads) | [<span data-ttu-id="fcd08-109">Visual Studio 2019 버전 16.3 Preview 3</span><span class="sxs-lookup"><span data-stu-id="fcd08-109">Visual Studio 2019 version 16.3 Preview 3</span></span>](https://visualstudio.microsoft.com/vs/preview/) | <span data-ttu-id="fcd08-110">[3.0.100-preview9](https://dotnet.microsoft.com/download/dotnet-core/3.0) <sup>1</sup></span><span class="sxs-lookup"><span data-stu-id="fcd08-110">[3.0.100-preview9](https://dotnet.microsoft.com/download/dotnet-core/3.0)<sup>1</sup></span></span> |

<span data-ttu-id="fcd08-111"><sup>1</sup> .NET Core 워크 로드와 함께 Visual Studio 2019와 함께 설치 됨</span><span class="sxs-lookup"><span data-stu-id="fcd08-111"><sup>1</sup>Installed with Visual Studio 2019 with .NET Core workload</span></span>

## <a name="summary-whats-new-in-53-preview-3"></a><span data-ttu-id="fcd08-112">요약: 5.3 preview 3의 새로운 기능</span><span class="sxs-lookup"><span data-stu-id="fcd08-112">Summary: What's New in 5.3 preview 3</span></span>

* <span data-ttu-id="fcd08-113">패키지 아이콘은 외부 URL이 필요 하지 않고 [패키지에 포함 될 수 있습니다](../reference/msbuild-targets.md#packing-an-icon-image-file).</span><span class="sxs-lookup"><span data-stu-id="fcd08-113">[Package Icon can be embedded in the package](../reference/msbuild-targets.md#packing-an-icon-image-file), instead of needing an external URL.</span></span><span data-ttu-id="fcd08-114"> - [#352](https://github.com/NuGet/Home/issues/352)</span><span class="sxs-lookup"><span data-stu-id="fcd08-114"> - [#352](https://github.com/NuGet/Home/issues/352)</span></span>

* <span data-ttu-id="fcd08-115">패키지에 대 한 SHA 추적 및 적용을 통한 보안 향상- [#7281](https://github.com/NuGet/Home/issues/7281)</span><span class="sxs-lookup"><span data-stu-id="fcd08-115">Improved security with SHA tracking and enforcement for Packages.Config - [#7281](https://github.com/NuGet/Home/issues/7281)</span></span>

### <a name="issues-fixed-in-this-release"></a><span data-ttu-id="fcd08-116">이번 릴리스에서 수정된 문제</span><span class="sxs-lookup"><span data-stu-id="fcd08-116">Issues fixed in this release</span></span>

<span data-ttu-id="fcd08-117">**버그**</span><span class="sxs-lookup"><span data-stu-id="fcd08-117">**Bugs**</span></span>

* <span data-ttu-id="fcd08-118">VS: 어셈블리는 부분적으로 ngen 되지 않고 완전히 ngen 됩니다 [#8513](https://github.com/NuGet/Home/issues/8513)</span><span class="sxs-lookup"><span data-stu-id="fcd08-118">VS: assemblies are fully ngen-ed not partially ngen-ed - [#8513](https://github.com/NuGet/Home/issues/8513)</span></span>

* <span data-ttu-id="fcd08-119">메모리 사용 줄이기 (이벤트 구독 취소)- [#8471](https://github.com/NuGet/Home/issues/8471)</span><span class="sxs-lookup"><span data-stu-id="fcd08-119">Reduce memory usage (unsubscribe from events) - [#8471](https://github.com/NuGet/Home/issues/8471)</span></span>

* <span data-ttu-id="fcd08-120">"Error_UnableToFindProjectInfo" 메시지가 문법적으로 올바르지 않습니다.- [#8441](https://github.com/NuGet/Home/issues/8441)</span><span class="sxs-lookup"><span data-stu-id="fcd08-120">"Error_UnableToFindProjectInfo" message is not grammatically correct - [#8441](https://github.com/NuGet/Home/issues/8441)</span></span>

* <span data-ttu-id="fcd08-121">NU1403 개선-모든 패키지의 유효성을 검사 하 고 예상/실제 sha 값을 포함 합니다.- [#8424](https://github.com/NuGet/Home/issues/8424)</span><span class="sxs-lookup"><span data-stu-id="fcd08-121">NU1403 improvements - validate all packages, include the expected/actual sha values - [#8424](https://github.com/NuGet/Home/issues/8424)</span></span>

* <span data-ttu-id="fcd08-122">NuGetPackageManager에 여러 개의 열거가 있습니다. PreviewUpdatePackagesAsync- [#8401](https://github.com/NuGet/Home/issues/8401)</span><span class="sxs-lookup"><span data-stu-id="fcd08-122">Multiple enumeration in NuGetPackageManager.PreviewUpdatePackagesAsync - [#8401](https://github.com/NuGet/Home/issues/8401)</span></span>

* <span data-ttu-id="fcd08-123">PluginProcess에서 "공용-> 내부" 변경 내용 되돌리기- [#8390](https://github.com/NuGet/Home/issues/8390)</span><span class="sxs-lookup"><span data-stu-id="fcd08-123">Revert "public -> internal" change in PluginProcess - [#8390](https://github.com/NuGet/Home/issues/8390)</span></span>

* <span data-ttu-id="fcd08-124">IVsPackageSourceProvider. GetSources (...)에 잘못 된 예외 동작이 있습니다.- [#8383](https://github.com/NuGet/Home/issues/8383)</span><span class="sxs-lookup"><span data-stu-id="fcd08-124">IVsPackageSourceProvider.GetSources(…) has ill-defined exception behavior - [#8383](https://github.com/NuGet/Home/issues/8383)</span></span>

* <span data-ttu-id="fcd08-125">PluginManager 생성자를 다시 공용으로 설정- [#8379](https://github.com/NuGet/Home/issues/8379)</span><span class="sxs-lookup"><span data-stu-id="fcd08-125">Make PluginManager constructor public again - [#8379](https://github.com/NuGet/Home/issues/8379)</span></span>

* <span data-ttu-id="fcd08-126">PM UI의 새로 고침 빈도를 추적 하는 메트릭- [#8369](https://github.com/NuGet/Home/issues/8369)</span><span class="sxs-lookup"><span data-stu-id="fcd08-126">Metrics to track the refresh rate of the PM UI - [#8369](https://github.com/NuGet/Home/issues/8369)</span></span>

* <span data-ttu-id="fcd08-127">패키지 관리자 UI를 통해 설치할 때 UI 새로 고침 수 줄이기- [#8358](https://github.com/NuGet/Home/issues/8358)</span><span class="sxs-lookup"><span data-stu-id="fcd08-127">Decrease the number of UI refreshes when installing through the Package Manager UI - [#8358](https://github.com/NuGet/Home/issues/8358)</span></span>

* <span data-ttu-id="fcd08-128">원격 분석: datetime 값은 문화권별 형식을 사용 합니다. [#8351](https://github.com/NuGet/Home/issues/8351)</span><span class="sxs-lookup"><span data-stu-id="fcd08-128">Telemetry:  datetime values use culture-specific formats - [#8351](https://github.com/NuGet/Home/issues/8351)</span></span>

* <span data-ttu-id="fcd08-129">패키지 관리자 UI의 찾아보기 탭에서 UI 새로 고침 축소 #6570- [#8339](https://github.com/NuGet/Home/issues/8339)</span><span class="sxs-lookup"><span data-stu-id="fcd08-129">Reduce UI refreshes in browse tab of Package Manager UI #6570 - [#8339](https://github.com/NuGet/Home/issues/8339)</span></span>

* <span data-ttu-id="fcd08-130">[테스트 실패] "구성 파일을 구문 분석할 수 없습니다." 메시지가 표시 되 면 두 번 [#8320](https://github.com/NuGet/Home/issues/8320)</span><span class="sxs-lookup"><span data-stu-id="fcd08-130">[Test Failure] “Unable to parse config file” will prompt twice - [#8320](https://github.com/NuGet/Home/issues/8320)</span></span>

* <span data-ttu-id="fcd08-131">고객 수정 (패키지에 필요한 nuspec 파일이 누락 됨)을 설명 하는 좋은 doc 페이지로 NU5037 오류 발생- [#8291](https://github.com/NuGet/Home/issues/8291)</span><span class="sxs-lookup"><span data-stu-id="fcd08-131">Raise NU5037 error with good doc page that explains customer fixes (The package is missing the required nuspec file) - [#8291](https://github.com/NuGet/Home/issues/8291)</span></span>

* <span data-ttu-id="fcd08-132">프로젝트의 RuntimeIdentifier가 변경 되 면 잠금 모드 복원이 실패 [#8260](https://github.com/NuGet/Home/issues/8260)</span><span class="sxs-lookup"><span data-stu-id="fcd08-132">Locked-mode restore fails when a project's RuntimeIdentifier is changed - [#8260](https://github.com/NuGet/Home/issues/8260)</span></span>

* <span data-ttu-id="fcd08-133">VS 지연- [#8156](https://github.com/NuGet/Home/issues/8156) 에서 설정을 읽습니다.</span><span class="sxs-lookup"><span data-stu-id="fcd08-133">Make the Settings reading in VS lazy - [#8156](https://github.com/NuGet/Home/issues/8156)</span></span>

* <span data-ttu-id="fcd08-134">' Nuget 원본에서의 회귀 추가 ' 원인 "': ' 문자, 16 진수 값 0x3A를 이름" 오류- [#7948](https://github.com/NuGet/Home/issues/7948) 에 포함할 수 없습니다.</span><span class="sxs-lookup"><span data-stu-id="fcd08-134">Regression in 'Nuget sources add' causes "The ':' character, hexadecimal value 0x3A, cannot be included in a name" errors - [#7948](https://github.com/NuGet/Home/issues/7948)</span></span>

* <span data-ttu-id="fcd08-135">NuGet 플러그 인 자격 증명 공급자-프로세스 창을 숨깁니다.- [#7511](https://github.com/NuGet/Home/issues/7511)</span><span class="sxs-lookup"><span data-stu-id="fcd08-135">NuGet plugin credential providers - hide the process window - [#7511](https://github.com/NuGet/Home/issues/7511)</span></span>

* <span data-ttu-id="fcd08-136">PackagePathResolver 적용은 절대 경로- [#7349](https://github.com/NuGet/Home/issues/7349)</span><span class="sxs-lookup"><span data-stu-id="fcd08-136">Enforce PackagePathResolver is an absolute path - [#7349](https://github.com/NuGet/Home/issues/7349)</span></span>

* <span data-ttu-id="fcd08-137">패키지 관리자 UI의 설치 및 업데이트 탭에서 UI 새로 고침 축소- [#6570](https://github.com/NuGet/Home/issues/6570)</span><span class="sxs-lookup"><span data-stu-id="fcd08-137">Reduce UI refreshes in install and update tabs of Package Manager UI - [#6570](https://github.com/NuGet/Home/issues/6570)</span></span>

<span data-ttu-id="fcd08-138">**DCR:**</span><span class="sxs-lookup"><span data-stu-id="fcd08-138">**DCR:**</span></span>

* <span data-ttu-id="fcd08-139">NetStandard 2.1에 매핑되도록 Xamarin 프레임 워크 업데이트- [#8368](https://github.com/NuGet/Home/issues/8368)</span><span class="sxs-lookup"><span data-stu-id="fcd08-139">Update Xamarin frameworks to map to NetStandard 2.1 - [#8368](https://github.com/NuGet/Home/issues/8368)</span></span>

* <span data-ttu-id="fcd08-140">설치/업데이트- [#8324](https://github.com/NuGet/Home/issues/8324) 에 대 한 패키지 관리자 "미리 보기 창"의 콘텐츠 복사 사용</span><span class="sxs-lookup"><span data-stu-id="fcd08-140">Enable copying the contents of package manager "preview window" for install/update - [#8324](https://github.com/NuGet/Home/issues/8324)</span></span>

* <span data-ttu-id="fcd08-141">Proj 파일에서 복원 사용- [#8212](https://github.com/NuGet/Home/issues/8212)</span><span class="sxs-lookup"><span data-stu-id="fcd08-141">Enable restore on .proj files - [#8212](https://github.com/NuGet/Home/issues/8212)</span></span>

* <span data-ttu-id="fcd08-142">같은 `NUGET_NETFX_PLUGIN_PATHS` 시간 `NUGET_NETCORE_PLUGIN_PATHS` 에 및의 구성을 모두 지원 하기 위해 및를 도입 [#8151](https://github.com/NuGet/Home/issues/8151)</span><span class="sxs-lookup"><span data-stu-id="fcd08-142">Introduce `NUGET_NETFX_PLUGIN_PATHS` and `NUGET_NETCORE_PLUGIN_PATHS` to support configuration of both at same time - [#8151](https://github.com/NuGet/Home/issues/8151)</span></span>

* <span data-ttu-id="fcd08-143">버전 특성을 통해 PackageDownload에 여러 버전 사용- [#8074](https://github.com/NuGet/Home/issues/8074)</span><span class="sxs-lookup"><span data-stu-id="fcd08-143">Enable multiple versions for a PackageDownload via Version attribute - [#8074](https://github.com/NuGet/Home/issues/8074)</span></span>

* <span data-ttu-id="fcd08-144">Nuget.exe 디렉터리 및-PackageDirectory 옵션을 nuget.exe pack에 추가- [#7163](https://github.com/NuGet/Home/issues/7163)</span><span class="sxs-lookup"><span data-stu-id="fcd08-144">Add -SolutionDirectory and -PackageDirectory options to nuget.exe pack - [#7163](https://github.com/NuGet/Home/issues/7163)</span></span>

* <span data-ttu-id="fcd08-145">NuGet Pack을 결정적으로 사용 하도록 설정 [#6229](https://github.com/NuGet/Home/issues/6229)</span><span class="sxs-lookup"><span data-stu-id="fcd08-145">Enable NuGet Pack to be deterministic - [#6229](https://github.com/NuGet/Home/issues/6229)</span></span>

<span data-ttu-id="fcd08-146">**[이 릴리스에서 해결 된 모든 문제 목록-5.3 preview 3](https://github.com/nuget/home/issues?q=is%3Aissue+is%3Aclosed+milestone%3A%225.3")**</span><span class="sxs-lookup"><span data-stu-id="fcd08-146">**[List of all issues fixed in this release - 5.3 preview 3](https://github.com/nuget/home/issues?q=is%3Aissue+is%3Aclosed+milestone%3A%225.3")**</span></span>
