---
title: NuGet 3.4-RC 릴리스 정보
description: 알려진 문제, 버그 수정, 추가 된 기능 및 Ecrs를 포함 하는 NuGet 3.4 RC에 대 한 릴리스 정보입니다.
author: JonDouglas
ms.author: jodou
ms.date: 11/11/2016
ms.topic: conceptual
ms.openlocfilehash: 3023dd3727c7c585212032d38c042bded4135c1e
ms.sourcegitcommit: ee6c3f203648a5561c809db54ebeb1d0f0598b68
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 01/26/2021
ms.locfileid: "98780240"
---
# <a name="nuget-34-rc-release-notes"></a><span data-ttu-id="637a6-103">NuGet 3.4-RC 릴리스 정보</span><span class="sxs-lookup"><span data-stu-id="637a6-103">NuGet 3.4-RC Release Notes</span></span>

<span data-ttu-id="637a6-104">[NuGet 3.3 릴리스 정보](../release-notes/nuget-3.3.md)  |  [NuGet 3.4 릴리스 정보](../release-notes/nuget-3.4.md)</span><span class="sxs-lookup"><span data-stu-id="637a6-104">[NuGet 3.3 Release Notes](../release-notes/nuget-3.3.md) | [NuGet 3.4 Release Notes](../release-notes/nuget-3.4.md)</span></span>

<span data-ttu-id="637a6-105">NuGet 3.4-RC는 Visual Studio 2015 업데이트 2 RC와 함께 2016 년 3 월 3 일에 출시 되었으며 바뀌어에서 몇 가지 개념를 사용 하 여 빌드 되었습니다.</span><span class="sxs-lookup"><span data-stu-id="637a6-105">NuGet 3.4-RC was released March 3, 2016 alongside the Visual Studio 2015 Update 2 RC and was built with a few tenets in minds:</span></span>

* <span data-ttu-id="637a6-106">플랫폼 간 지원</span><span class="sxs-lookup"><span data-stu-id="637a6-106">Cross-Platform support</span></span>
* <span data-ttu-id="637a6-107">성능 향상</span><span class="sxs-lookup"><span data-stu-id="637a6-107">Performance improvements</span></span>
* <span data-ttu-id="637a6-108">사소한 UI 개선</span><span class="sxs-lookup"><span data-stu-id="637a6-108">Minor UI improvements</span></span>

<span data-ttu-id="637a6-109">다음 기능은이 RC에서 사용할 수 있으며, 3.4 최종 릴리스에 대 한 추가 계획을 제공 합니다.</span><span class="sxs-lookup"><span data-stu-id="637a6-109">The following features are available in this RC, with more planned for the 3.4 final release.</span></span>

## <a name="new-features"></a><span data-ttu-id="637a6-110">새로운 기능</span><span class="sxs-lookup"><span data-stu-id="637a6-110">New Features</span></span>

* <span data-ttu-id="637a6-111">NuGet 클라이언트는 이제 리포지토리에서 gzip 콘텐츠 인코딩을 지원 합니다.</span><span class="sxs-lookup"><span data-stu-id="637a6-111">NuGet clients now support gzip content-encoding from repositories</span></span>
* <span data-ttu-id="637a6-112">Xproj 프로젝트의 패키지에서 Pdb에 대 한 지원</span><span class="sxs-lookup"><span data-stu-id="637a6-112">Support for PDBs from packages in xproj projects</span></span>
* <span data-ttu-id="637a6-113">ContentFiles 요소에서 iOS 및 Android 빌드 작업에 대 한 지원</span><span class="sxs-lookup"><span data-stu-id="637a6-113">Support for iOS and Android build actions in the contentFiles element</span></span>
* <span data-ttu-id="637a6-114">Netstandard.library 및 netstandardapp framework 모니커 지원</span><span class="sxs-lookup"><span data-stu-id="637a6-114">Support for the netstandard and netstandardapp framework monikers</span></span>

## <a name="new-user-interface-features"></a><span data-ttu-id="637a6-115">새 사용자 인터페이스 기능</span><span class="sxs-lookup"><span data-stu-id="637a6-115">New User Interface Features</span></span>

* <span data-ttu-id="637a6-116">설치, 업데이트 및 통합 탭에서 특히 성능이 크게 향상 되었습니다.</span><span class="sxs-lookup"><span data-stu-id="637a6-116">Significant performance improvements especially on the Installed, Updates, and Consolidate tabs</span></span>
* <span data-ttu-id="637a6-117">설치 됨 및 업데이트 탭은 이제 사전순으로 정렬 됩니다.</span><span class="sxs-lookup"><span data-stu-id="637a6-117">Installed and Updates tabs are now sorted alphabetically</span></span>
* <span data-ttu-id="637a6-118">검색을 새로 고칠 수 있는 새로 고침 단추를 추가 했습니다.</span><span class="sxs-lookup"><span data-stu-id="637a6-118">Added a Refresh button that allows a search to be refreshed</span></span>

## <a name="updates-and-improvements"></a><span data-ttu-id="637a6-119">업데이트 및 개선 사항</span><span class="sxs-lookup"><span data-stu-id="637a6-119">Updates and Improvements</span></span>

* <span data-ttu-id="637a6-120">부동 버전이 있는에서 참조 되는 패키지는 `project.json` 모든 빌드에서 업데이트 되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="637a6-120">Packages referenced in `project.json` that have a floating version will not update on every build.</span></span> <span data-ttu-id="637a6-121">대신 복원, 정리, 다시 빌드 또는 수정이 적용 되는 경우에만 업데이트 됩니다 `project.json` .</span><span class="sxs-lookup"><span data-stu-id="637a6-121">Instead, they will update only when forced to restore, clean, rebuild, or modify `project.json`.</span></span>
* <span data-ttu-id="637a6-122">NuGet 구성 UI를 사용 하는 경우 nuget.org 리포지토리 원본은 더 이상 프로젝트 구성에 적용 되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="637a6-122">nuget.org repository sources are no longer forced into a project configuration when you use the NuGet configuration UI.</span></span>
* <span data-ttu-id="637a6-123">NuGet은 더 이상 공유 프로젝트의 패키지를 복원 하거나 잠금 파일을 쓰지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="637a6-123">NuGet no longer restores packages in shared projects nor writes a lock file.</span></span>
* <span data-ttu-id="637a6-124">네트워크 오류를 개선 하 고 연결이 불가능 하거나 응답 하지 않는 서버에 대 한 처리를 다시 시도 했습니다.</span><span class="sxs-lookup"><span data-stu-id="637a6-124">We've improved network failure and retry handling for unreachable or slow-to-respond servers.</span></span>
* <span data-ttu-id="637a6-125">Visual Studio 패키지 관리자 UI에서 키보드 및 마우스 동작이 개선 되었습니다.</span><span class="sxs-lookup"><span data-stu-id="637a6-125">Keyboard and mouse behaviors are improved in the Visual Studio Package Manager UI.</span></span>
* <span data-ttu-id="637a6-126">이제 `project.json` DNX에서 최신 스키마를 지원 합니다.</span><span class="sxs-lookup"><span data-stu-id="637a6-126">We now support the latest `project.json` schema in DNX.</span></span>

## <a name="known-issues"></a><span data-ttu-id="637a6-127">알려진 문제</span><span class="sxs-lookup"><span data-stu-id="637a6-127">Known Issues</span></span>

<span data-ttu-id="637a6-128">Microsoft는 GitHub 문제 목록에서 다음 위치에 있는 문제를 계속 추적 합니다. [http://github.com/nuget/home/issues](http://github.com/nuget/home/issues)</span><span class="sxs-lookup"><span data-stu-id="637a6-128">We continue to track issues on our GitHub issues list which can be found at: [http://github.com/nuget/home/issues](http://github.com/nuget/home/issues)</span></span>