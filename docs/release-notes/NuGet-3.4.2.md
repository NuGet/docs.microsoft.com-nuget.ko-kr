---
title: NuGet 3.4.2 릴리스 정보
description: 포함 하 여 NuGet 3.4.2에 대 한 릴리스 정보는 문제, 버그 수정, 추가 된 기능 및 Dcr 알려져 있습니다.
author: karann-msft
ms.author: karann
manager: unnir
ms.date: 11/11/2016
ms.topic: conceptual
ms.openlocfilehash: 88d29a84e280433663ab6c1c04ae16e1329420f7
ms.sourcegitcommit: 3eab9c4dd41ea7ccd2c28bb5ab16f6fbbec13708
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/26/2018
ms.locfileid: "31819668"
---
# <a name="nuget-342-release-notes"></a><span data-ttu-id="46b88-103">NuGet 3.4.2 릴리스 정보</span><span class="sxs-lookup"><span data-stu-id="46b88-103">NuGet 3.4.2 Release Notes</span></span>

<span data-ttu-id="46b88-104">[NuGet 3.4.1 릴리스 정보](../release-notes/nuget-3.4.1.md) | [NuGet 3.4.3 릴리스 정보](../release-notes/nuget-3.4.3.md)</span><span class="sxs-lookup"><span data-stu-id="46b88-104">[NuGet 3.4.1 Release Notes](../release-notes/nuget-3.4.1.md) | [NuGet 3.4.3 Release Notes](../release-notes/nuget-3.4.3.md)</span></span>

<span data-ttu-id="46b88-105">3.4.2 NuGet 3.4는 및 3.4.1에서 식별 된 몇 가지 문제를 해결 하기 2016 년 4 월 8 일에 릴리스된 해제 합니다.</span><span class="sxs-lookup"><span data-stu-id="46b88-105">NuGet 3.4.2 was released on April 8, 2016 to address several issues that were identified in the 3.4 and 3.4.1 release.</span></span>

## <a name="nugetexe-342-rc-is-now-available"></a><span data-ttu-id="46b88-106">nuget.exe 3.4.2 RC 출시 되었습니다.</span><span class="sxs-lookup"><span data-stu-id="46b88-106">nuget.exe 3.4.2 RC is now available</span></span>

<span data-ttu-id="46b88-107">Nuget.exe 3.4.2의 릴리스 후보를 다운로드할 수 있습니다 [여기](https://dist.nuget.org/index.html)합니다.</span><span class="sxs-lookup"><span data-stu-id="46b88-107">You can download the release candidate of nuget.exe 3.4.2 [here](https://dist.nuget.org/index.html).</span></span>

## <a name="updates-and-improvements"></a><span data-ttu-id="46b88-108">업데이트 및 향상 기능</span><span class="sxs-lookup"><span data-stu-id="46b88-108">Updates and Improvements</span></span>

* <span data-ttu-id="46b88-109">특정 시나리오에서는 여기서 상세한 종속성 그래프를 사용 하 여 패키지에 대 한 업데이트 시간이 매우 오래 걸린 하 고 Visual Studio 중지 되었습니다. 업데이트의 성능을 크게 개선 했습니다.</span><span class="sxs-lookup"><span data-stu-id="46b88-109">We have significantly improved the performance of updates in a specific scenario, where updates on packages with deep dependency graphs took a really long time and hung Visual Studio.</span></span>
* <span data-ttu-id="46b88-110">네트워크 트래픽 없이 nuget 복원 2.5-3 배 Visual Studio 내에서 더 빠른 배입니다.</span><span class="sxs-lookup"><span data-stu-id="46b88-110">nuget restore without network traffic is 2.5x – 3x faster within Visual Studio.</span></span>
* <span data-ttu-id="46b88-111">이 변경 외에도 해결 했습니다 문제가 있는 VS UI에 계산 업데이트를 인출 하는 경우에 두 번 네트워크 적중 된 것입니다.</span><span class="sxs-lookup"><span data-stu-id="46b88-111">In addition to this change, we have fixed an issue where we were hitting the network twice when fetching the update count in the VS UI.</span></span> <span data-ttu-id="46b88-112">이 부분적으로 3.4/3.4.1 한 경험이 일부 시간 초과 문제 고객에 대 한 책임입니다.</span><span class="sxs-lookup"><span data-stu-id="46b88-112">This was partially responsible for some timeout issues customers experienced in 3.4/3.4.1.</span></span>
* <span data-ttu-id="46b88-113">No_proxy 설정에 대 한 지원 추가</span><span class="sxs-lookup"><span data-stu-id="46b88-113">Added support for no_proxy setting</span></span>

## <a name="fixes"></a><span data-ttu-id="46b88-114">수정 프로그램</span><span class="sxs-lookup"><span data-stu-id="46b88-114">Fixes</span></span>

* <span data-ttu-id="46b88-115">3.4.1으로 업데이트 한 후 nuget.org 소스 NuGet 설정 또는 구성에서 누락 된 문제를 해결 합니다.</span><span class="sxs-lookup"><span data-stu-id="46b88-115">Fixed an issue where nuget.org source was missing in NuGet settings or config after updating to 3.4.1.</span></span>
* <span data-ttu-id="46b88-116">3.4.1 FindPackagesById 대/소문자 변경 Artifactory을 중단 문제를 해결 합니다.</span><span class="sxs-lookup"><span data-stu-id="46b88-116">Fixed an issue where a casing change to FindPackagesById in 3.4.1 breaks Artifactory.</span></span>
* <span data-ttu-id="46b88-117">FIPS nuget.exe와 NuGet 복원 오류를 발생 시킨 문제를 수정 했습니다.</span><span class="sxs-lookup"><span data-stu-id="46b88-117">Corrected an issue with FIPS that caused failures with NuGet restore with nuget.exe.</span></span>
* <span data-ttu-id="46b88-118">잘못 된 아이콘 URL로 소스를 검색할 때 충돌을 수정 했습니다.</span><span class="sxs-lookup"><span data-stu-id="46b88-118">Fixed a crash when browsing sources with invalid icon URL.</span></span>
* <span data-ttu-id="46b88-119">버전 및 ' 모든 소스 '에서 항목을 병합을 문제가 해결된 되었습니다.</span><span class="sxs-lookup"><span data-stu-id="46b88-119">Fixed issues with merging versions and entries from 'All Sources'.</span></span>

## <a name="known-issues-in-342-windows-x86-commandline-rc"></a><span data-ttu-id="46b88-120">알려진 문제 3.4.2에 Windows x86 명령줄 (RC)</span><span class="sxs-lookup"><span data-stu-id="46b88-120">Known Issues in 3.4.2 Windows x86 Commandline (RC)</span></span>

<span data-ttu-id="46b88-121">이러한 문제는 다음 주 초기 RTM 도달하기 전에 수정 됩니다.</span><span class="sxs-lookup"><span data-stu-id="46b88-121">These issues will be fixed early next week before we hit RTM.</span></span>

*  <span data-ttu-id="46b88-122">솔루션에 대 한 실행 중인 nuget 복원을 솔루션 파일은 프로젝트 파일 보다 더 낮은 폴더 계층 구조에 저장 하는 경우 실패 합니다.</span><span class="sxs-lookup"><span data-stu-id="46b88-122">Running nuget restore on a solution will fail if the solution file is placed in a lower folder hierarchy than the project files.</span></span>
*  <span data-ttu-id="46b88-123">Nuget delete 명령을 V2 피드를 사용 하 여 패키지 실행이 실패 합니다.</span><span class="sxs-lookup"><span data-stu-id="46b88-123">Running nuget delete command on a package using the V2 feed will fail.</span></span> <span data-ttu-id="46b88-124">V3 피드를 대신 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="46b88-124">Use V3 feed instead.</span></span>


<span data-ttu-id="46b88-125">수정 사항 및이 릴리스에서 향상 된 전체 목록은 체크 아웃 문제 목록 [여기](https://github.com/NuGet/Home/issues?utf8=%E2%9C%93&q=is%3Aissue+milestone%3A3.4.2++is%3Aclosed+)합니다.</span><span class="sxs-lookup"><span data-stu-id="46b88-125">For the complete list of fixes and improvements in this release, check out the list of issues [here](https://github.com/NuGet/Home/issues?utf8=%E2%9C%93&q=is%3Aissue+milestone%3A3.4.2++is%3Aclosed+).</span></span>