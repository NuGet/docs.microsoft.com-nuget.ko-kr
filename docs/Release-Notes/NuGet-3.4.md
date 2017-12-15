---
title: "NuGet 3.4 릴리스 정보 | Microsoft Docs"
author: karann-msft
ms.author: karann-msft
manager: ghogen
ms.date: 11/11/2016
ms.topic: article
ms.prod: nuget
ms.technology: 
ms.assetid: 80a429f5-7569-4349-ad7f-4fe9218eac23
description: "알려진된 문제, 버그 수정, 추가 된 기능 및 Dcr를 포함 하 여 NuGet 3.4에 대 한 릴리스 정보입니다."
keywords: "NuGet 3.4 릴리스 정보, 버그 수정, 알려진 문제, 추가 기능을 Dcr"
ms.reviewer:
- karann-msft
- unniravindranathan
ms.openlocfilehash: 911e4377ad9c8b1f865b0721f43ff73b62df6d1e
ms.sourcegitcommit: d0ba99bfe019b779b75731bafdca8a37e35ef0d9
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 12/14/2017
---
# <a name="nuget-34-release-notes"></a><span data-ttu-id="116d5-104">NuGet 3.4 릴리스 정보</span><span class="sxs-lookup"><span data-stu-id="116d5-104">NuGet 3.4 Release Notes</span></span>

<span data-ttu-id="116d5-105">[NuGet 3.4 RC 릴리스 정보](../release-notes/nuget-3.4-RC.md) | [NuGet 3.4.1 릴리스 정보](../release-notes/nuget-3.4.1.md)</span><span class="sxs-lookup"><span data-stu-id="116d5-105">[NuGet 3.4-RC Release Notes](../release-notes/nuget-3.4-RC.md) | [NuGet 3.4.1 Release Notes](../release-notes/nuget-3.4.1.md)</span></span>

<span data-ttu-id="116d5-106">NuGet 3.4 2016 년 3 월 30 일의 Visual Studio 2015 업데이트 2 및 Visual Studio 15 Preview 릴리스 일환으로 릴리스 되었습니다 및 사람들에 몇 가지 개념을 사용 하 여 빌드한 되었습니다.</span><span class="sxs-lookup"><span data-stu-id="116d5-106">NuGet 3.4 was released March 30, 2016 as part of the Visual Studio 2015 Update 2 and Visual Studio 15 Preview Release and was built with a few tenets in minds:</span></span>

*  <span data-ttu-id="116d5-107">크로스 플랫폼 지원</span><span class="sxs-lookup"><span data-stu-id="116d5-107">Cross-Platform support</span></span>
*  <span data-ttu-id="116d5-108">성능 향상</span><span class="sxs-lookup"><span data-stu-id="116d5-108">Performance improvements</span></span>
*  <span data-ttu-id="116d5-109">보조 UI 개선 사항</span><span class="sxs-lookup"><span data-stu-id="116d5-109">Minor UI improvements</span></span>

<span data-ttu-id="116d5-110">다음과 같은 기능 RC에서 이전에 추가 된 및 업데이트 되었거나 3.4 릴리스에 대 한 완료 되었습니다.</span><span class="sxs-lookup"><span data-stu-id="116d5-110">The following features were previously added in the RC and have been updated or completed for the 3.4 release:</span></span>

## <a name="new-features"></a><span data-ttu-id="116d5-111">새 기능</span><span class="sxs-lookup"><span data-stu-id="116d5-111">New Features</span></span>

* <span data-ttu-id="116d5-112">NuGet 클라이언트가 gzip 콘텐츠 인코딩 저장소에서 이제 지원</span><span class="sxs-lookup"><span data-stu-id="116d5-112">NuGet clients now support gzip content-encoding from repositories</span></span>
* <span data-ttu-id="116d5-113">Xproj 프로젝트에서 패키지의 Pdb에 대 한 지원</span><span class="sxs-lookup"><span data-stu-id="116d5-113">Support for PDBs from packages in xproj projects</span></span>
* <span data-ttu-id="116d5-114">IOS 및 Android 빌드 작업에서 콘텐츠 파일 요소에 대 한 지원</span><span class="sxs-lookup"><span data-stu-id="116d5-114">Support for iOS and Android build actions in the contentFiles element</span></span>
* <span data-ttu-id="116d5-115">Netstandard 및 netstandardapp 프레임 워크 모니커에 대 한 지원</span><span class="sxs-lookup"><span data-stu-id="116d5-115">Support for the netstandard and netstandardapp framework monikers</span></span>

## <a name="new-user-interface-features"></a><span data-ttu-id="116d5-116">새로운 사용자 인터페이스 기능</span><span class="sxs-lookup"><span data-stu-id="116d5-116">New User Interface Features</span></span>

* <span data-ttu-id="116d5-117">설치 됨, 업데이트 및 통합 탭에 특히 중요 한 성능 향상</span><span class="sxs-lookup"><span data-stu-id="116d5-117">Significant performance improvements especially on the Installed, Updates, and Consolidate tabs</span></span>
* <span data-ttu-id="116d5-118">집계 ' 모든 패키지 소스 ' 소스를 적절 한 검색 결과 병합을 사용할 수</span><span class="sxs-lookup"><span data-stu-id="116d5-118">Aggregate 'All Package Sources' Source is available with proper search result merging</span></span>
* <span data-ttu-id="116d5-119">설치 및 업데이트 탭 이제 사전순으로 정렬 됩니다.</span><span class="sxs-lookup"><span data-stu-id="116d5-119">Installed and Updates tabs are now sorted alphabetically</span></span>
* <span data-ttu-id="116d5-120">검색을 새로 고칠 수 있도록 새로 고침 단추를 추가 합니다.</span><span class="sxs-lookup"><span data-stu-id="116d5-120">Added a Refresh button that allows a search to be refreshed</span></span>
* <span data-ttu-id="116d5-121">버전 목록 맨 위에 있는 최신 빌드 옵션</span><span class="sxs-lookup"><span data-stu-id="116d5-121">Latest Build options at the top of the Version list</span></span>

## <a name="updates-and-improvements"></a><span data-ttu-id="116d5-122">업데이트 및 향상 기능</span><span class="sxs-lookup"><span data-stu-id="116d5-122">Updates and Improvements</span></span>

* <span data-ttu-id="116d5-123">패키지에서 참조 `project.json` 부동 있는 버전 모든 빌드에 대해 업데이트 되지 것입니다.</span><span class="sxs-lookup"><span data-stu-id="116d5-123">Packages referenced in `project.json` that have a floating version will not update on every build.</span></span> <span data-ttu-id="116d5-124">대신, 복원, 정리, 다시 작성 또는 수정 해야 하는 경우에 업데이트 됩니다 `project.json`합니다.</span><span class="sxs-lookup"><span data-stu-id="116d5-124">Instead, they will update only when forced to restore, clean, rebuild, or modify `project.json`.</span></span>
* <span data-ttu-id="116d5-125">nuget.org 리포지토리 소스는 NuGet 구성 UI를 사용 하는 경우 프로젝트 구성에 더 이상 강제 됩니다.</span><span class="sxs-lookup"><span data-stu-id="116d5-125">nuget.org repository sources are no longer forced into a project configuration when you use the NuGet configuration UI.</span></span>
* <span data-ttu-id="116d5-126">NuGet에 더 이상 공유 프로젝트의 패키지를 복원 하거나 잠금 파일을 씁니다.</span><span class="sxs-lookup"><span data-stu-id="116d5-126">NuGet no longer restores packages in shared projects nor writes a lock file.</span></span>
* <span data-ttu-id="116d5-127">네트워크 오류를 개선 했습니다 하 고 연결할 수 없거나 대 한 느린 응답 서버에 대 한 처리를 다시 시도 하십시오.</span><span class="sxs-lookup"><span data-stu-id="116d5-127">We've improved network failure and retry handling for unreachable or slow-to-respond servers.</span></span>
* <span data-ttu-id="116d5-128">Visual Studio 패키지 관리자 UI에서 키보드 및 마우스 동작 개선 되었습니다.</span><span class="sxs-lookup"><span data-stu-id="116d5-128">Keyboard and mouse behaviors are improved in the Visual Studio Package Manager UI.</span></span>
* <span data-ttu-id="116d5-129">이제 최신 지원 `project.json` DNX의 스키마입니다.</span><span class="sxs-lookup"><span data-stu-id="116d5-129">We now support the latest `project.json` schema in DNX.</span></span>

## <a name="breaking-changes"></a><span data-ttu-id="116d5-130">주요 변경 사항</span><span class="sxs-lookup"><span data-stu-id="116d5-130">Breaking Changes</span></span>

* <span data-ttu-id="116d5-131">패키지 버전 번호 형식으로 정규화 된 이제은 *주요*. *사소한*. *패치*-*시험판* 패치 및 사소한, 각각의 주 버전, 정수로 처리 되 고 모든 앞에 오는 0을 삭제 합니다.</span><span class="sxs-lookup"><span data-stu-id="116d5-131">Package version numbers are now normalized to the format *major*.*minor*.*patch*-*prerelease*   Each of major, minor, and patch are treated as integers and drop any leading zeroes.</span></span>  <span data-ttu-id="116d5-132">시험판 정보를 문자열로 취급 되며 및에 적용 된 변경 내용이 없습니다.</span><span class="sxs-lookup"><span data-stu-id="116d5-132">The prerelease information is treated as a string and no changes are applied to it.</span></span> <span data-ttu-id="116d5-133">이러한 번호는 NuGet 클라이언트 및 nuget.org 서비스에서 제공 된 검색에 쿼리에서 사용 됩니다.</span><span class="sxs-lookup"><span data-stu-id="116d5-133">These numbers are used in queries by the NuGet clients and the search provided by the nuget.org service.</span></span>  <span data-ttu-id="116d5-134">자세한 내용은 아래에서 NuGet 문서에서 확인할 수 있습니다 [시험판 버전](../create-packages/prerelease-packages.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="116d5-134">More details can be found in the NuGet Docs under [Prerelease Versions](../create-packages/prerelease-packages.md).</span></span>

## <a name="known-issues"></a><span data-ttu-id="116d5-135">알려진 문제</span><span class="sxs-lookup"><span data-stu-id="116d5-135">Known Issues</span></span>

* <span data-ttu-id="116d5-136">**문제:** 문제 또는 심지어는 Visual Studio 충돌 Visual Studio에서 Powershell과 함께 다음과 같은 시나리오에서 Windows 10 v1511 사용자가 발생할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="116d5-136">**Issue:** Windows 10 v1511 users may experience issues or even a Visual Studio crash with Powershell in Visual Studio in the following scenarios:</span></span>
    * <span data-ttu-id="116d5-137">Install.ps1 있는 패키지를 제거 / 설치 / uninstall.ps1 스크립트</span><span class="sxs-lookup"><span data-stu-id="116d5-137">Installing / Uninstalling packages that have install.ps1 / uninstall.ps1 scripts</span></span>
    * <span data-ttu-id="116d5-138">Init.ps1 스크립트가 (예: EntityFramework) 프로젝트를 로드 합니다.</span><span class="sxs-lookup"><span data-stu-id="116d5-138">Loading projects that have an init.ps1 script (like EntityFramework)</span></span>
    * <span data-ttu-id="116d5-139">웹 콘텐츠 게시</span><span class="sxs-lookup"><span data-stu-id="116d5-139">Publishing web content</span></span>

* <span data-ttu-id="116d5-140">**해결 방법:** 귀하의 Windows 10 설치에 적용 된 최신 패치, expecially 2016 년 1 월 (KB 3124263) 또는 이후 업데이트가 있는지 확인 합니다.</span><span class="sxs-lookup"><span data-stu-id="116d5-140">**Workaround:** Ensure that your Windows 10 install has the latest patches applied, expecially the January 2016 (KB 3124263) or a later update.</span></span>  <span data-ttu-id="116d5-141">자세한 내용은에서 사용할 수 있는 [GitHub 문제 #1638](http://github.com/nuget/home/issues/1638)</span><span class="sxs-lookup"><span data-stu-id="116d5-141">More details are available on [GitHub issue #1638](http://github.com/nuget/home/issues/1638)</span></span>

* <span data-ttu-id="116d5-142">**문제:** NuGet v2 프로토콜 리디렉션이 끊어집니다.</span><span class="sxs-lookup"><span data-stu-id="116d5-142">**Issue:** NuGet v2 protocol redirects are broken.</span></span>
<span data-ttu-id="116d5-143">대체 호스트에 요청을 리디렉션하는 사용자 지정 NuGet 리포지토리에서 리디렉션 요청을 인식하지 못합니다.</span><span class="sxs-lookup"><span data-stu-id="116d5-143">Custom NuGet repositories that redirect requests to an alternative host do not honor the redirect request.</span></span>
* <span data-ttu-id="116d5-144">**해결 방법:** 이 문제를 해결 하려면 리디렉션된 서버 위치를 가리키도록 설정에서 패키지 리포지토리 URI를 구성 합니다.</span><span class="sxs-lookup"><span data-stu-id="116d5-144">**Workaround:**  To work around this issue, configure the package repository URI in settings to point to the redirected server location.</span></span>
<span data-ttu-id="116d5-145">자세한 내용은 참조 [GitHub 끌어오기 요청 #387](https://github.com/NuGet/NuGet.Client/pull/387)합니다.</span><span class="sxs-lookup"><span data-stu-id="116d5-145">For more information, see [GitHub pull request #387](https://github.com/NuGet/NuGet.Client/pull/387).</span></span>

<span data-ttu-id="116d5-146">찾을 수 있는 GitHub 문제 목록에서 문제를 추적 하려면 계속 하기: [http://github.com/nuget/home/issues](http://github.com/nuget/home/issues)</span><span class="sxs-lookup"><span data-stu-id="116d5-146">We continue to track issues on our GitHub issues list which can be found at: [http://github.com/nuget/home/issues](http://github.com/nuget/home/issues)</span></span>