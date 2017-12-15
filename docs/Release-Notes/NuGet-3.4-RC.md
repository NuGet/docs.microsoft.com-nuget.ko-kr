---
title: "NuGet 3.4 RC 릴리스 정보 | Microsoft Docs"
author: karann-msft
ms.author: karann-msft
manager: ghogen
ms.date: 11/11/2016
ms.topic: article
ms.prod: nuget
ms.technology: 
ms.assetid: 239d3d95-5a72-4fac-8389-b6deac27884d
description: "NuGet 3.4 RC 알려진된 문제, 버그 수정, 추가 된 기능 및 Dcr를 포함 하 여에 대 한 릴리스 정보입니다."
keywords: "NuGet 3.4 RC 릴리스 정보, 버그 수정, 알려진 문제, 추가 기능을 Dcr"
ms.reviewer:
- karann-msft
- unniravindranathan
ms.openlocfilehash: 86c37d516eede2ac5e6e5e842f687a8f3b17c0a4
ms.sourcegitcommit: d0ba99bfe019b779b75731bafdca8a37e35ef0d9
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 12/14/2017
---
# <a name="nuget-34-rc-release-notes"></a><span data-ttu-id="c79e7-104">NuGet 3.4 RC 릴리스 정보</span><span class="sxs-lookup"><span data-stu-id="c79e7-104">NuGet 3.4-RC Release Notes</span></span>

<span data-ttu-id="c79e7-105">[NuGet 3.3 릴리스 정보](../release-notes/nuget-3.3.md) | [NuGet 3.4 릴리스 정보](../release-notes/nuget-3.4.md)</span><span class="sxs-lookup"><span data-stu-id="c79e7-105">[NuGet 3.3 Release Notes](../release-notes/nuget-3.3.md) | [NuGet 3.4 Release Notes](../release-notes/nuget-3.4.md)</span></span>

<span data-ttu-id="c79e7-106">NuGet 3.4 RC Visual Studio 2015 업데이트 2 RC와 함께 2016 년 3 월 3 일에 릴리스된 및 사람들에 몇 가지 개념을 사용 하 여 빌드한 되었습니다.</span><span class="sxs-lookup"><span data-stu-id="c79e7-106">NuGet 3.4-RC was released March 3, 2016 alongside the Visual Studio 2015 Update 2 RC and was built with a few tenets in minds:</span></span>

*  <span data-ttu-id="c79e7-107">크로스 플랫폼 지원</span><span class="sxs-lookup"><span data-stu-id="c79e7-107">Cross-Platform support</span></span>
*  <span data-ttu-id="c79e7-108">성능 향상</span><span class="sxs-lookup"><span data-stu-id="c79e7-108">Performance improvements</span></span>
*  <span data-ttu-id="c79e7-109">보조 UI 개선 사항</span><span class="sxs-lookup"><span data-stu-id="c79e7-109">Minor UI improvements</span></span>

<span data-ttu-id="c79e7-110">다음 기능은이 RC에서 사용할 수 있는 3.4 최종 릴리스에 계획입니다.</span><span class="sxs-lookup"><span data-stu-id="c79e7-110">The following features are available in this RC, with more planned for the 3.4 final release.</span></span>

## <a name="new-features"></a><span data-ttu-id="c79e7-111">새 기능</span><span class="sxs-lookup"><span data-stu-id="c79e7-111">New Features</span></span>

* <span data-ttu-id="c79e7-112">NuGet 클라이언트가 gzip 콘텐츠 인코딩 저장소에서 이제 지원</span><span class="sxs-lookup"><span data-stu-id="c79e7-112">NuGet clients now support gzip content-encoding from repositories</span></span>
* <span data-ttu-id="c79e7-113">Xproj 프로젝트에서 패키지의 Pdb에 대 한 지원</span><span class="sxs-lookup"><span data-stu-id="c79e7-113">Support for PDBs from packages in xproj projects</span></span>
* <span data-ttu-id="c79e7-114">IOS 및 Android 빌드 작업에서 콘텐츠 파일 요소에 대 한 지원</span><span class="sxs-lookup"><span data-stu-id="c79e7-114">Support for iOS and Android build actions in the contentFiles element</span></span>
* <span data-ttu-id="c79e7-115">Netstandard 및 netstandardapp 프레임 워크 모니커에 대 한 지원</span><span class="sxs-lookup"><span data-stu-id="c79e7-115">Support for the netstandard and netstandardapp framework monikers</span></span>

## <a name="new-user-interface-features"></a><span data-ttu-id="c79e7-116">새로운 사용자 인터페이스 기능</span><span class="sxs-lookup"><span data-stu-id="c79e7-116">New User Interface Features</span></span>

* <span data-ttu-id="c79e7-117">설치 됨, 업데이트 및 통합 탭에 특히 중요 한 성능 향상</span><span class="sxs-lookup"><span data-stu-id="c79e7-117">Significant performance improvements especially on the Installed, Updates, and Consolidate tabs</span></span>
* <span data-ttu-id="c79e7-118">설치 및 업데이트 탭 이제 사전순으로 정렬 됩니다.</span><span class="sxs-lookup"><span data-stu-id="c79e7-118">Installed and Updates tabs are now sorted alphabetically</span></span>
* <span data-ttu-id="c79e7-119">검색을 새로 고칠 수 있도록 새로 고침 단추를 추가 합니다.</span><span class="sxs-lookup"><span data-stu-id="c79e7-119">Added a Refresh button that allows a search to be refreshed</span></span>

## <a name="updates-and-improvements"></a><span data-ttu-id="c79e7-120">업데이트 및 향상 기능</span><span class="sxs-lookup"><span data-stu-id="c79e7-120">Updates and Improvements</span></span>

* <span data-ttu-id="c79e7-121">패키지에서 참조 `project.json` 부동 있는 버전 모든 빌드에 대해 업데이트 되지 것입니다.</span><span class="sxs-lookup"><span data-stu-id="c79e7-121">Packages referenced in `project.json` that have a floating version will not update on every build.</span></span> <span data-ttu-id="c79e7-122">대신, 복원, 정리, 다시 작성 또는 수정 해야 하는 경우에 업데이트 됩니다 `project.json`합니다.</span><span class="sxs-lookup"><span data-stu-id="c79e7-122">Instead, they will update only when forced to restore, clean, rebuild, or modify `project.json`.</span></span>
* <span data-ttu-id="c79e7-123">nuget.org 리포지토리 소스는 NuGet 구성 UI를 사용 하는 경우 프로젝트 구성에 더 이상 강제 됩니다.</span><span class="sxs-lookup"><span data-stu-id="c79e7-123">nuget.org repository sources are no longer forced into a project configuration when you use the NuGet configuration UI.</span></span>
* <span data-ttu-id="c79e7-124">NuGet에 더 이상 공유 프로젝트의 패키지를 복원 하거나 잠금 파일을 씁니다.</span><span class="sxs-lookup"><span data-stu-id="c79e7-124">NuGet no longer restores packages in shared projects nor writes a lock file.</span></span>
* <span data-ttu-id="c79e7-125">네트워크 오류를 개선 했습니다 하 고 연결할 수 없거나 대 한 느린 응답 서버에 대 한 처리를 다시 시도 하십시오.</span><span class="sxs-lookup"><span data-stu-id="c79e7-125">We've improved network failure and retry handling for unreachable or slow-to-respond servers.</span></span>
* <span data-ttu-id="c79e7-126">Visual Studio 패키지 관리자 UI에서 키보드 및 마우스 동작 개선 되었습니다.</span><span class="sxs-lookup"><span data-stu-id="c79e7-126">Keyboard and mouse behaviors are improved in the Visual Studio Package Manager UI.</span></span>
* <span data-ttu-id="c79e7-127">이제 최신 지원 `project.json` DNX의 스키마입니다.</span><span class="sxs-lookup"><span data-stu-id="c79e7-127">We now support the latest `project.json` schema in DNX.</span></span>

## <a name="known-issues"></a><span data-ttu-id="c79e7-128">알려진 문제</span><span class="sxs-lookup"><span data-stu-id="c79e7-128">Known Issues</span></span>

<span data-ttu-id="c79e7-129">찾을 수 있는 GitHub 문제 목록에서 문제를 추적 하려면 계속 하기: [http://github.com/nuget/home/issues](http://github.com/nuget/home/issues)</span><span class="sxs-lookup"><span data-stu-id="c79e7-129">We continue to track issues on our GitHub issues list which can be found at: [http://github.com/nuget/home/issues](http://github.com/nuget/home/issues)</span></span>