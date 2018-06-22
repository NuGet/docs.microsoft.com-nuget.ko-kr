---
title: 3.2.1 NuGet 릴리스 정보
description: 3.2.1 NuGet 포함에 대 한 릴리스 정보는 문제, 버그 수정, 추가 된 기능 및 Dcr 알려져 있습니다.
author: karann-msft
ms.author: karann
manager: unnir
ms.date: 11/11/2016
ms.topic: conceptual
ms.openlocfilehash: 039fabaaacfdffd76fa88ff8183548e97cd4719b
ms.sourcegitcommit: 3eab9c4dd41ea7ccd2c28bb5ab16f6fbbec13708
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/26/2018
ms.locfileid: "31820146"
---
# <a name="nuget-321-release-notes"></a><span data-ttu-id="cc237-103">3.2.1 NuGet 릴리스 정보</span><span class="sxs-lookup"><span data-stu-id="cc237-103">NuGet 3.2.1 Release Notes</span></span>

<span data-ttu-id="cc237-104">[NuGet 3.2 릴리스 정보](../release-notes/nuget-3.2.md) | [NuGet 3.3 릴리스 정보](../release-notes/nuget-3.3.md)</span><span class="sxs-lookup"><span data-stu-id="cc237-104">[NuGet 3.2 Release Notes](../release-notes/nuget-3.2.md) | [NuGet 3.3 Release Notes](../release-notes/nuget-3.3.md)</span></span>

<span data-ttu-id="cc237-105">명령줄에 대 한 NuGet 3.2.1 3.2 버전에 대 한 수정 및 최적화는 소수의 함께 2015 년 10 월 12 일에 출시 된 및에서 사용할 수 [dist.nuget.org](http://dist.nuget.org/index.html)합니다.</span><span class="sxs-lookup"><span data-stu-id="cc237-105">NuGet 3.2.1 for the command-line was released October 12, 2015 with a handful of optimizations and fixes for the 3.2 release and is available from [dist.nuget.org](http://dist.nuget.org/index.html).</span></span>

## <a name="improvements"></a><span data-ttu-id="cc237-106">향상 된 기능</span><span class="sxs-lookup"><span data-stu-id="cc237-106">Improvements</span></span>

* <span data-ttu-id="cc237-107">NuGet의 원래 대/소문자와 구성 파일을 이제 사용 `NuGet.Config`합니다.</span><span class="sxs-lookup"><span data-stu-id="cc237-107">NuGet now uses the configuration file with the original casing of `NuGet.Config`.</span></span>  <span data-ttu-id="cc237-108">이 대/소문자 구분 운영 체제에서 중요 [1427](https://github.com/NuGet/Home/issues/1427)</span><span class="sxs-lookup"><span data-stu-id="cc237-108">This is important on case-sensitive operating systems [1427](https://github.com/NuGet/Home/issues/1427)</span></span>
* <span data-ttu-id="cc237-109">NuGet 복원에서 dnx 프로젝트를 무시 이제 (`*.xproj`) 사용 하 여 처리 해야 하는 `dnu` [1227](https://github.com/NuGet/Home/issues/1227)</span><span class="sxs-lookup"><span data-stu-id="cc237-109">NuGet restore will now ignore dnx projects (`*.xproj`) that should be processed with `dnu` [1227](https://github.com/NuGet/Home/issues/1227)</span></span>
* <span data-ttu-id="cc237-110">작업할 때 네트워크 사용률을 최적화 `index.json` 등록 데이터를 패키지 하 고 [1426](https://github.com/NuGet/Home/issues/1426)</span><span class="sxs-lookup"><span data-stu-id="cc237-110">Optimized network utilization when working with `index.json` and package registration data [1426](https://github.com/NuGet/Home/issues/1426)</span></span>
* <span data-ttu-id="cc237-111">향상 된 리소스 다운로드 v2 서비스와 함께 보다 강력 하도록 처리 [1448](https://github.com/NuGet/Home/issues/1448)</span><span class="sxs-lookup"><span data-stu-id="cc237-111">Improved resource download handling to be more robust with v2 services [1448](https://github.com/NuGet/Home/issues/1448)</span></span>

## <a name="fixes"></a><span data-ttu-id="cc237-112">수정 프로그램</span><span class="sxs-lookup"><span data-stu-id="cc237-112">Fixes</span></span>

* <span data-ttu-id="cc237-113">NuGet 업데이트를 올바로 업데이트 `.csproj` / `.vcxproj` 참조 [1483](https://github.com/NuGet/Home/issues/1483)</span><span class="sxs-lookup"><span data-stu-id="cc237-113">NuGet update correctly updates `.csproj`/`.vcxproj` references [1483](https://github.com/NuGet/Home/issues/1483)</span></span>
* <span data-ttu-id="cc237-114">이제 로컬.nuget 폴더가 SpecialFolders.UserProfile 찾을 수 없으면 만들어지지 않도록 방지 [1531](https://github.com/NuGet/Home/issues/1531)</span><span class="sxs-lookup"><span data-stu-id="cc237-114">Now preventing a local .nuget folder from being created when a SpecialFolders.UserProfile cannot be located [1531](https://github.com/NuGet/Home/issues/1531)</span></span>
* <span data-ttu-id="cc237-115">로컬 캐시에 다운로드 하는 동안 손상 되는 패키지의 처리를 향상 [1405](https://github.com/NuGet/Home/issues/1405) [1157](https://github.com/NuGet/Home/issues/1157)</span><span class="sxs-lookup"><span data-stu-id="cc237-115">Improved handling of packages in local cache that are corrupted during download [1405](https://github.com/NuGet/Home/issues/1405) [1157](https://github.com/NuGet/Home/issues/1157)</span></span>

<span data-ttu-id="cc237-116">명령줄과 Visual Studio extension NuGet GitHub에서 찾을 수 있습니다에 대 한 처리 문제의 전체 목록은 [3.2.1 마일스 톤](https://github.com/NuGet/Home/issues?q=milestone%3A3.2.1+is%3Aclosed)</span><span class="sxs-lookup"><span data-stu-id="cc237-116">A complete list of issues addressed for the command-line and Visual Studio extension can be found in the NuGet GitHub [3.2.1 milestone](https://github.com/NuGet/Home/issues?q=milestone%3A3.2.1+is%3Aclosed)</span></span>

## <a name="known-issues"></a><span data-ttu-id="cc237-117">알려진 문제</span><span class="sxs-lookup"><span data-stu-id="cc237-117">Known Issues</span></span>

<span data-ttu-id="cc237-118">찾을 수 있는 GitHub 문제 목록에서 문제 추적 계속 합니다. [http://github.com/nuget/home/issues](http://github.com/nuget/home/issues)</span><span class="sxs-lookup"><span data-stu-id="cc237-118">We continue to track issues on our GitHub issues list which can be found at: [http://github.com/nuget/home/issues](http://github.com/nuget/home/issues)</span></span>