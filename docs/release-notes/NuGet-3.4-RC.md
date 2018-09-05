---
title: NuGet 3.4 RC 릴리스 정보
description: NuGet 3.4 RC 알려진된 문제, 버그 수정, 추가 된 기능 및 Dcr 포함에 대 한 릴리스 정보입니다.
author: karann-msft
ms.author: karann
ms.date: 11/11/2016
ms.topic: conceptual
ms.openlocfilehash: 795bdcfaa2e22447856b60d05807aeb0992cdfa0
ms.sourcegitcommit: 1d1406764c6af5fb7801d462e0c4afc9092fa569
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 09/04/2018
ms.locfileid: "43546756"
---
# <a name="nuget-34-rc-release-notes"></a><span data-ttu-id="a8a0c-103">NuGet 3.4 RC 릴리스 정보</span><span class="sxs-lookup"><span data-stu-id="a8a0c-103">NuGet 3.4-RC Release Notes</span></span>

<span data-ttu-id="a8a0c-104">[NuGet 3.3 릴리스 정보](../release-notes/nuget-3.3.md) | [NuGet 3.4 릴리스 정보](../release-notes/nuget-3.4.md)</span><span class="sxs-lookup"><span data-stu-id="a8a0c-104">[NuGet 3.3 Release Notes](../release-notes/nuget-3.3.md) | [NuGet 3.4 Release Notes](../release-notes/nuget-3.4.md)</span></span>

<span data-ttu-id="a8a0c-105">NuGet 3.4 RC Visual Studio 2015 업데이트 2 RC와 함께 2016 년 3 월 3 일에 릴리스 되었으며 머리에 몇 가지 개념을 사용 하 여 빌드된:</span><span class="sxs-lookup"><span data-stu-id="a8a0c-105">NuGet 3.4-RC was released March 3, 2016 alongside the Visual Studio 2015 Update 2 RC and was built with a few tenets in minds:</span></span>

* <span data-ttu-id="a8a0c-106">플랫폼 간 지원</span><span class="sxs-lookup"><span data-stu-id="a8a0c-106">Cross-Platform support</span></span>
* <span data-ttu-id="a8a0c-107">성능 향상</span><span class="sxs-lookup"><span data-stu-id="a8a0c-107">Performance improvements</span></span>
* <span data-ttu-id="a8a0c-108">보조 UI 개선 사항</span><span class="sxs-lookup"><span data-stu-id="a8a0c-108">Minor UI improvements</span></span>

<span data-ttu-id="a8a0c-109">다음 기능은 수 더 3.4 최종 릴리스에 대 한 계획 된이 RC에서 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="a8a0c-109">The following features are available in this RC, with more planned for the 3.4 final release.</span></span>

## <a name="new-features"></a><span data-ttu-id="a8a0c-110">새 기능</span><span class="sxs-lookup"><span data-stu-id="a8a0c-110">New Features</span></span>

* <span data-ttu-id="a8a0c-111">NuGet 클라이언트는 이제 gzip 콘텐츠 인코딩 리포지토리에서 지원</span><span class="sxs-lookup"><span data-stu-id="a8a0c-111">NuGet clients now support gzip content-encoding from repositories</span></span>
* <span data-ttu-id="a8a0c-112">Xproj 프로젝트에서 패키지의 Pdb에 대 한 지원</span><span class="sxs-lookup"><span data-stu-id="a8a0c-112">Support for PDBs from packages in xproj projects</span></span>
* <span data-ttu-id="a8a0c-113">ContentFiles 요소에서 작업을 iOS 및 Android 빌드에 대 한 지원</span><span class="sxs-lookup"><span data-stu-id="a8a0c-113">Support for iOS and Android build actions in the contentFiles element</span></span>
* <span data-ttu-id="a8a0c-114">Netstandard 및 netstandardapp 프레임 워크 모니커 지원</span><span class="sxs-lookup"><span data-stu-id="a8a0c-114">Support for the netstandard and netstandardapp framework monikers</span></span>

## <a name="new-user-interface-features"></a><span data-ttu-id="a8a0c-115">새로운 사용자 인터페이스 기능</span><span class="sxs-lookup"><span data-stu-id="a8a0c-115">New User Interface Features</span></span>

* <span data-ttu-id="a8a0c-116">설치 됨, 업데이트 및 통합 탭에서 특히 중요 한 성능 향상</span><span class="sxs-lookup"><span data-stu-id="a8a0c-116">Significant performance improvements especially on the Installed, Updates, and Consolidate tabs</span></span>
* <span data-ttu-id="a8a0c-117">설치 하 고 이제 업데이트 탭은 사전순으로 정렬</span><span class="sxs-lookup"><span data-stu-id="a8a0c-117">Installed and Updates tabs are now sorted alphabetically</span></span>
* <span data-ttu-id="a8a0c-118">검색을 새로 고칠 수 있도록 새로 고침 단추를 추가 합니다.</span><span class="sxs-lookup"><span data-stu-id="a8a0c-118">Added a Refresh button that allows a search to be refreshed</span></span>

## <a name="updates-and-improvements"></a><span data-ttu-id="a8a0c-119">업데이트 및 향상 된 기능</span><span class="sxs-lookup"><span data-stu-id="a8a0c-119">Updates and Improvements</span></span>

* <span data-ttu-id="a8a0c-120">참조 된 패키지 `project.json` 부동 있는 버전 모든 빌드에 대해 업데이트 되지 것입니다.</span><span class="sxs-lookup"><span data-stu-id="a8a0c-120">Packages referenced in `project.json` that have a floating version will not update on every build.</span></span> <span data-ttu-id="a8a0c-121">대신, 복원, 정리, 다시 작성 하거나 수정 해야 하는 경우에 업데이트 됩니다 `project.json`합니다.</span><span class="sxs-lookup"><span data-stu-id="a8a0c-121">Instead, they will update only when forced to restore, clean, rebuild, or modify `project.json`.</span></span>
* <span data-ttu-id="a8a0c-122">nuget.org 리포지토리 소스는 NuGet 구성 UI를 사용 하는 경우 프로젝트 구성에 더 이상 강제 됩니다.</span><span class="sxs-lookup"><span data-stu-id="a8a0c-122">nuget.org repository sources are no longer forced into a project configuration when you use the NuGet configuration UI.</span></span>
* <span data-ttu-id="a8a0c-123">NuGet에 더 이상 공유 프로젝트에서 패키지를 복원 하거나 잠금 파일을 씁니다.</span><span class="sxs-lookup"><span data-stu-id="a8a0c-123">NuGet no longer restores packages in shared projects nor writes a lock file.</span></span>
* <span data-ttu-id="a8a0c-124">향상 되었습니다. 네트워크 오류가 발생 하 고 연결할 수 없거나 응답 속도가 느린 서버에 대 한 처리를 다시 시도 하세요.</span><span class="sxs-lookup"><span data-stu-id="a8a0c-124">We've improved network failure and retry handling for unreachable or slow-to-respond servers.</span></span>
* <span data-ttu-id="a8a0c-125">Visual Studio 패키지 관리자 UI에서 키보드 및 마우스 동작 개선 되었습니다.</span><span class="sxs-lookup"><span data-stu-id="a8a0c-125">Keyboard and mouse behaviors are improved in the Visual Studio Package Manager UI.</span></span>
* <span data-ttu-id="a8a0c-126">이제 최신 지원 `project.json` 스키마 DNX에서.</span><span class="sxs-lookup"><span data-stu-id="a8a0c-126">We now support the latest `project.json` schema in DNX.</span></span>

## <a name="known-issues"></a><span data-ttu-id="a8a0c-127">알려진 문제</span><span class="sxs-lookup"><span data-stu-id="a8a0c-127">Known Issues</span></span>

<span data-ttu-id="a8a0c-128">찾을 수 있는 GitHub 문제 목록에서 문제를 추적 하려면 계속 합니다. [http://github.com/nuget/home/issues](http://github.com/nuget/home/issues)</span><span class="sxs-lookup"><span data-stu-id="a8a0c-128">We continue to track issues on our GitHub issues list which can be found at: [http://github.com/nuget/home/issues](http://github.com/nuget/home/issues)</span></span>