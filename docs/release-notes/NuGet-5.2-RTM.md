---
title: NuGet 5.2 RTM 릴리스 정보
description: 새 기능, 버그 수정 및 Ecrs를 비롯 한 NuGet 5.2에 대 한 릴리스 정보입니다.
author: karann-msft
ms.author: karann
ms.date: 07/23/2019
ms.topic: conceptual
ms.openlocfilehash: f94bd8ddb8fac8bf47c2826bf5b417595b0efa8b
ms.sourcegitcommit: f291ff91561a6b58c2aec41c624d798e00ce41fa
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/24/2019
ms.locfileid: "68471186"
---
# <a name="nuget-52-release-notes"></a><span data-ttu-id="e1df1-103">NuGet 5.2 릴리스 정보</span><span class="sxs-lookup"><span data-stu-id="e1df1-103">NuGet 5.2 Release Notes</span></span>

<span data-ttu-id="e1df1-104">NuGet 배포 차량:</span><span class="sxs-lookup"><span data-stu-id="e1df1-104">NuGet distribution vehicles:</span></span>

| <span data-ttu-id="e1df1-105">NuGet 버전</span><span class="sxs-lookup"><span data-stu-id="e1df1-105">NuGet version</span></span> | <span data-ttu-id="e1df1-106">Visual Studio 버전에서 사용 가능</span><span class="sxs-lookup"><span data-stu-id="e1df1-106">Available in Visual Studio version</span></span>| <span data-ttu-id="e1df1-107">.NET SDK에서 사용 가능</span><span class="sxs-lookup"><span data-stu-id="e1df1-107">Available in .NET SDK(s)</span></span>|
|:---|:---|:---|
| [<span data-ttu-id="e1df1-108">**5.2.0**</span><span class="sxs-lookup"><span data-stu-id="e1df1-108">**5.2.0**</span></span>](https://nuget.org/downloads) | [<span data-ttu-id="e1df1-109">Visual Studio 2019 버전 16.2</span><span class="sxs-lookup"><span data-stu-id="e1df1-109">Visual Studio 2019 version 16.2</span></span>](https://visualstudio.microsoft.com/downloads/) | <span data-ttu-id="e1df1-110">[2.1.80 X](https://dotnet.microsoft.com/download/dotnet-core/2.1) <sup>1</sup>, [2.2.40 X](https://dotnet.microsoft.com/download/dotnet-core/2.2)<sup>2</sup></span><span class="sxs-lookup"><span data-stu-id="e1df1-110">[2.1.80X](https://dotnet.microsoft.com/download/dotnet-core/2.1)<sup>1</sup>, [2.2.40X](https://dotnet.microsoft.com/download/dotnet-core/2.2)<sup>2</sup></span></span> |

<span data-ttu-id="e1df1-111"><sup>1</sup> .NET Core 워크 로드와 함께 Visual Studio 2019와 함께 설치 됨</span><span class="sxs-lookup"><span data-stu-id="e1df1-111"><sup>1</sup>Installed with Visual Studio 2019 with .NET Core workload</span></span> 

<span data-ttu-id="e1df1-112"><sup>2</sup> .NET Core 워크 로드와 함께 Visual Studio 2019을 사용 하 여 선택적으로 설치할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="e1df1-112"><sup>2</sup>Available as an optional install with Visual Studio 2019 with .NET Core workload</span></span>

## <a name="summary-whats-new-in-52"></a><span data-ttu-id="e1df1-113">요약: 5.2의 새로운 기능</span><span class="sxs-lookup"><span data-stu-id="e1df1-113">Summary: What's New in 5.2</span></span>

* <span data-ttu-id="e1df1-114">Linux & Mac의 경로 문제로 인 한 NuGet 작업 실패를 야기 하는 중요 한 버그를 수정 했습니다 [#7341](https://github.com/NuGet/Home/issues/7341)</span><span class="sxs-lookup"><span data-stu-id="e1df1-114">Fixed a critical bug that caused occasional NuGet operation failures due to path issues on Linux & Mac - [#7341](https://github.com/NuGet/Home/issues/7341)</span></span>

* <span data-ttu-id="e1df1-115">Visual Studio의 NuGet 패키지 관리자 UI를 사용 하 여 패키지를 검색할 때 UI 응답성이 향상 되었습니다. 특히 속도가 느려지는 경우에는 특히 그렇습니다 [#8039](https://github.com/NuGet/Home/issues/8039)</span><span class="sxs-lookup"><span data-stu-id="e1df1-115">Improved UI responsiveness when browsing packages using the NuGet package manager UI in Visual Studio especially noticeable for slow sources - [#8039](https://github.com/NuGet/Home/issues/8039)</span></span>

* <span data-ttu-id="e1df1-116">잠금 파일 ([#8187](https://github.com/NuGet/Home/issues/8187),[#8160](https://github.com/NuGet/Home/issues/8160),[#8114](https://github.com/NuGet/Home/issues/8114),[#7840](https://github.com/NuGet/Home/issues/7840)) 및 인증 플러그 인 ([#8300](https://github.com/NuGet/Home/issues/8300),[#8271](https://github.com/NuGet/Home/issues/8271),[#8269](https://github.com/NuGet/Home/issues/8269),[#8210](https://github.com/NuGet/Home/issues/8210),[#8198](https://github.com/NuGet/Home/issues/8198),[#7845](https://github.com/NuGet/Home/issues/7845))의 다양 한 안정성 수정</span><span class="sxs-lookup"><span data-stu-id="e1df1-116">Tons of reliability fixes for lock file ([#8187](https://github.com/NuGet/Home/issues/8187),[#8160](https://github.com/NuGet/Home/issues/8160),[#8114](https://github.com/NuGet/Home/issues/8114),[#7840](https://github.com/NuGet/Home/issues/7840)) and authentication plugin ([#8300](https://github.com/NuGet/Home/issues/8300),[#8271](https://github.com/NuGet/Home/issues/8271),[#8269](https://github.com/NuGet/Home/issues/8269),[#8210](https://github.com/NuGet/Home/issues/8210),[#8198](https://github.com/NuGet/Home/issues/8198),[#7845](https://github.com/NuGet/Home/issues/7845))</span></span>

### <a name="issues-fixed-in-this-release"></a><span data-ttu-id="e1df1-117">이번 릴리스에서 수정된 문제</span><span class="sxs-lookup"><span data-stu-id="e1df1-117">Issues fixed in this release</span></span>

<span data-ttu-id="e1df1-118">**버그**</span><span class="sxs-lookup"><span data-stu-id="e1df1-118">**Bugs**</span></span>

* <span data-ttu-id="e1df1-119">성능 패키지 관리자 콘솔:  "기본 프로젝트" 콤보 상자에서 선택한 값- [#8235](https://github.com/NuGet/Home/issues/8235) UI 지연 업데이트</span><span class="sxs-lookup"><span data-stu-id="e1df1-119">Perf: Package Manager Console:  UI delay updating "Default project" combobox selected value - [#8235](https://github.com/NuGet/Home/issues/8235)</span></span>

* <span data-ttu-id="e1df1-120">성능 PM UI의 성능 향상- [#8039](https://github.com/NuGet/Home/issues/8039)</span><span class="sxs-lookup"><span data-stu-id="e1df1-120">Perf: Performance improvements in the PM UI - [#8039](https://github.com/NuGet/Home/issues/8039)</span></span>

* <span data-ttu-id="e1df1-121">성능 PMC에서 기본 프로젝트를 읽을 때 UI 지연이 발생 [#6824](https://github.com/NuGet/Home/issues/6824)</span><span class="sxs-lookup"><span data-stu-id="e1df1-121">Perf: UI Delay when reading Default Project in PMC - [#6824](https://github.com/NuGet/Home/issues/6824)</span></span>

* <span data-ttu-id="e1df1-122">Perf: [vsfeedback] 로컬 패키지 원본에 대 한 NuGet 업데이트 탭이 동결 됨- [#6470](https://github.com/NuGet/Home/issues/6470)</span><span class="sxs-lookup"><span data-stu-id="e1df1-122">Perf: [vsfeedback] NuGet Update tab freezes for a local package source - [#6470](https://github.com/NuGet/Home/issues/6470)</span></span>

* <span data-ttu-id="e1df1-123">인의  플러그 인이 시작 되지 않거나 조기에 종료 되 면 NuGet에서 전체 핸드셰이크 시간 제한을 대기 합니다. [#8300](https://github.com/NuGet/Home/issues/8300)</span><span class="sxs-lookup"><span data-stu-id="e1df1-123">Plugins:  NuGet waits full handshake timeout if plugin fails to launch or terminates early - [#8300](https://github.com/NuGet/Home/issues/8300)</span></span>

* <span data-ttu-id="e1df1-124">플러그 인: 플러그 인 시작 오류 진단 가능 개선- [#8271](https://github.com/NuGet/Home/issues/8271)</span><span class="sxs-lookup"><span data-stu-id="e1df1-124">Plugins:  improve diagnosability of plugin launch failure - [#8271](https://github.com/NuGet/Home/issues/8271)</span></span>

* <span data-ttu-id="e1df1-125">인의 기본 제공 플러그인의 nuget.exe 검색 문제- [#8269](https://github.com/NuGet/Home/issues/8269)</span><span class="sxs-lookup"><span data-stu-id="e1df1-125">Plugins: Issue with nuget.exe discovery of built in plugins - [#8269](https://github.com/NuGet/Home/issues/8269)</span></span>

* <span data-ttu-id="e1df1-126">플러그 인: 캐시 파일을 읽을 수 없습니다. [#8210](https://github.com/NuGet/Home/issues/8210)</span><span class="sxs-lookup"><span data-stu-id="e1df1-126">Plugins:  cache file is never read - [#8210](https://github.com/NuGet/Home/issues/8210)</span></span>

* <span data-ttu-id="e1df1-127">인의  "작업이 취소 되었습니다."</span><span class="sxs-lookup"><span data-stu-id="e1df1-127">Plugins:  "A task was canceled."</span></span> <span data-ttu-id="e1df1-128">복원 중 인증 플러그 인 오류- [#8198](https://github.com/NuGet/Home/issues/8198)</span><span class="sxs-lookup"><span data-stu-id="e1df1-128">errors with authentication plugin during restore - [#8198](https://github.com/NuGet/Home/issues/8198)</span></span>

* <span data-ttu-id="e1df1-129">Linux 플랫폼에서 일시적으로 검색 가능 하지 않은 플러그 인 캐시- [#7845](https://github.com/NuGet/Home/issues/7845)</span><span class="sxs-lookup"><span data-stu-id="e1df1-129">Plugins cache not discoverable intermittently on linux platforms - [#7845](https://github.com/NuGet/Home/issues/7845)</span></span>

* <span data-ttu-id="e1df1-130">LockFile: ATF를 사용 하는 경우 잘못 된 대상 프레임 워크 같음 [#8187](https://github.com/NuGet/Home/issues/8187) 검사로 인해 false NU1004</span><span class="sxs-lookup"><span data-stu-id="e1df1-130">LockFile: with ATF, it has false NU1004 due to a bad target framework equality check - [#8187](https://github.com/NuGet/Home/issues/8187)</span></span>

* <span data-ttu-id="e1df1-131">LockFile: 잠금 파일이 비어 있거나 형식이 잘못 된 경우 '--잠금 모드 ' 복원 플래그가 적용 되지 않습니다. [#8160](https://github.com/NuGet/Home/issues/8160)</span><span class="sxs-lookup"><span data-stu-id="e1df1-131">LockFile: '--locked-mode' restore flag not respected if lock file is empty or malformed - [#8160](https://github.com/NuGet/Home/issues/8160)</span></span>

* <span data-ttu-id="e1df1-132">LockFile: 패키지 잠금 파일에 사용자 지정 어셈블리 이름을 사용 하는 프로젝트를 소문자로 지정 하지 않음- [#8114](https://github.com/NuGet/Home/issues/8114)</span><span class="sxs-lookup"><span data-stu-id="e1df1-132">LockFile: Don't lowercase projects with custom assembly names in packages lock file - [#8114](https://github.com/NuGet/Home/issues/8114)</span></span>

* <span data-ttu-id="e1df1-133">LockFile: 잠금 파일에서 프로젝트 참조를 소문자로 설정- [#7840](https://github.com/NuGet/Home/issues/7840)</span><span class="sxs-lookup"><span data-stu-id="e1df1-133">LockFile: Make project reference lower case in lock file  - [#7840](https://github.com/NuGet/Home/issues/7840)</span></span>

* <span data-ttu-id="e1df1-134">복원: 변조 된 서명 된 패키지를 설치 하면 여러 번의 실패 한 설치 시도가 발생 합니다 (반복 된 출력 포함). [#8175](https://github.com/NuGet/Home/issues/8175)</span><span class="sxs-lookup"><span data-stu-id="e1df1-134">Restore:  installing a tampered signed package results in multiple failed install attempts (with repeated output) - [#8175](https://github.com/NuGet/Home/issues/8175)</span></span>

* <span data-ttu-id="e1df1-135">VS: 솔루션 사용자 옵션은 NuGet 업데이트 후 deserialize 되지 않습니다.- [#8166](https://github.com/NuGet/Home/issues/8166)</span><span class="sxs-lookup"><span data-stu-id="e1df1-135">VS: solution user options fail to deserialize after NuGet update - [#8166](https://github.com/NuGet/Home/issues/8166)</span></span>

* <span data-ttu-id="e1df1-136">dotnet-list-단위 테스트 프로젝트의 패키지에서 오류를 반환 [#8154](https://github.com/NuGet/Home/issues/8154)</span><span class="sxs-lookup"><span data-stu-id="e1df1-136">dotnet-list-package in a UnitTest project returns an error - [#8154](https://github.com/NuGet/Home/issues/8154)</span></span>

* <span data-ttu-id="e1df1-137">VS 설치 관리자에 대 한 NuGet 패키지 그룹 만들기-일부 VSIX 설정 문제 해결- [#8033](https://github.com/NuGet/Home/issues/8033)</span><span class="sxs-lookup"><span data-stu-id="e1df1-137">Create NuGet package group for VS installer - fixing some VSIX setup problems - [#8033](https://github.com/NuGet/Home/issues/8033)</span></span>

* <span data-ttu-id="e1df1-138">GeneratePackageOnBuild는 NoBuild를 설정 하면 안 됩니다.</span><span class="sxs-lookup"><span data-stu-id="e1df1-138">GeneratePackageOnBuild should not set NoBuild.</span></span><span data-ttu-id="e1df1-139"> - [#7801](https://github.com/NuGet/Home/issues/7801)</span><span class="sxs-lookup"><span data-stu-id="e1df1-139"> - [#7801](https://github.com/NuGet/Home/issues/7801)</span></span>

* <span data-ttu-id="e1df1-140">새 옵션인 "-기호 Packageformat snupkg"는 nuspec 파일에 명시적 어셈블리 참조 [#7638](https://github.com/NuGet/Home/issues/7638) 요소가 포함 된 경우 오류를 생성 합니다.</span><span class="sxs-lookup"><span data-stu-id="e1df1-140">The new option "-SymbolPackageFormat snupkg" generates an error when the .nuspec file contains an explicit assembly reference element - [#7638](https://github.com/NuGet/Home/issues/7638)</span></span>

* <span data-ttu-id="e1df1-141">Nuget.exe (498, 5): 오류: '/Tmp/NuGetScratch- [#7341](https://github.com/NuGet/Home/issues/7341) 경로의 일부를 찾을 수 없습니다.</span><span class="sxs-lookup"><span data-stu-id="e1df1-141">NuGet.targets(498,5): error : Could not find a part of the path '/tmp/NuGetScratch - [#7341](https://github.com/NuGet/Home/issues/7341)</span></span>

<span data-ttu-id="e1df1-142">**DCR:**</span><span class="sxs-lookup"><span data-stu-id="e1df1-142">**DCR:**</span></span>

* <span data-ttu-id="e1df1-143">PackageDownload가 지원 됨을 나타내는 msbuild 속성을 추가 [#8106](https://github.com/NuGet/Home/issues/8106)</span><span class="sxs-lookup"><span data-stu-id="e1df1-143">Add an msbuild property that indicates that PackageDownload is supported - [#8106](https://github.com/NuGet/Home/issues/8106)</span></span>

* <span data-ttu-id="e1df1-144">FrameworkReference FrameworkReference를 통해 종속성 흐름을 표시 하지 않습니다. PrivateAssets- [#7988](https://github.com/NuGet/Home/issues/7988)</span><span class="sxs-lookup"><span data-stu-id="e1df1-144">FrameworkReference suppress dependency flow via FrameworkReference.PrivateAssets - [#7988](https://github.com/NuGet/Home/issues/7988)</span></span>

* <span data-ttu-id="e1df1-145">패키지 외부에서 런타임 json을 제공 하기 위한 메커니즘- [#7351](https://github.com/NuGet/Home/issues/7351)</span><span class="sxs-lookup"><span data-stu-id="e1df1-145">Mechanism for supplying runtime.json outside of a package - [#7351](https://github.com/NuGet/Home/issues/7351)</span></span>

<span data-ttu-id="e1df1-146">**[이 릴리스에서 해결 된 모든 문제 목록-5.2 RTM](https://github.com/nuget/home/issues?q=is%3Aissue+is%3Aclosed+milestone%3A%225.2")**</span><span class="sxs-lookup"><span data-stu-id="e1df1-146">**[List of all issues fixed in this release - 5.2 RTM](https://github.com/nuget/home/issues?q=is%3Aissue+is%3Aclosed+milestone%3A%225.2")**</span></span>


