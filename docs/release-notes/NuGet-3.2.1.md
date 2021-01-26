---
title: NuGet 3.2.1 릴리스 정보
description: 알려진 문제, 버그 수정, 추가 된 기능 및 3.2.1를 포함 하는 NuGet에 대 한 릴리스 정보입니다.
author: JonDouglas
ms.author: jodou
ms.date: 11/11/2016
ms.topic: conceptual
ms.openlocfilehash: cbbef3517122ceda91cb4b4463fe8be43d204db4
ms.sourcegitcommit: ee6c3f203648a5561c809db54ebeb1d0f0598b68
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 01/26/2021
ms.locfileid: "98776527"
---
# <a name="nuget-321-release-notes"></a><span data-ttu-id="b9673-103">NuGet 3.2.1 릴리스 정보</span><span class="sxs-lookup"><span data-stu-id="b9673-103">NuGet 3.2.1 Release Notes</span></span>

<span data-ttu-id="b9673-104">[NuGet 3.2 릴리스 정보](../release-notes/nuget-3.2.md)  |  [NuGet 3.3 릴리스 정보](../release-notes/nuget-3.3.md)</span><span class="sxs-lookup"><span data-stu-id="b9673-104">[NuGet 3.2 Release Notes](../release-notes/nuget-3.2.md) | [NuGet 3.3 Release Notes](../release-notes/nuget-3.3.md)</span></span>

<span data-ttu-id="b9673-105">명령줄에 대 한 NuGet 3.2.1는 3.2 릴리스에 대 한 몇 가지 최적화와 픽스를 갖춘 2015 년 10 월 12 일에 출시 되었으며 [dist.nuget.org](http://dist.nuget.org/index.html)에서 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="b9673-105">NuGet 3.2.1 for the command-line was released October 12, 2015 with a handful of optimizations and fixes for the 3.2 release and is available from [dist.nuget.org](http://dist.nuget.org/index.html).</span></span>

## <a name="improvements"></a><span data-ttu-id="b9673-106">향상 된 기능</span><span class="sxs-lookup"><span data-stu-id="b9673-106">Improvements</span></span>

* <span data-ttu-id="b9673-107">이제 NuGet은의 원래 대/소문자 구분과 함께 구성 파일을 사용 `NuGet.Config` 합니다.</span><span class="sxs-lookup"><span data-stu-id="b9673-107">NuGet now uses the configuration file with the original casing of `NuGet.Config`.</span></span>  <span data-ttu-id="b9673-108">이는 대/소문자를 구분 하는 운영 체제 [1427](https://github.com/NuGet/Home/issues/1427) 에 중요 합니다.</span><span class="sxs-lookup"><span data-stu-id="b9673-108">This is important on case-sensitive operating systems [1427](https://github.com/NuGet/Home/issues/1427)</span></span>
* <span data-ttu-id="b9673-109">이제 NuGet 복원에서 `*.xproj` 1227를 사용 하 여 처리 해야 하는 dnx 프로젝트 ()를 무시 합니다. `dnu` [](https://github.com/NuGet/Home/issues/1227)</span><span class="sxs-lookup"><span data-stu-id="b9673-109">NuGet restore will now ignore dnx projects (`*.xproj`) that should be processed with `dnu` [1227](https://github.com/NuGet/Home/issues/1227)</span></span>
* <span data-ttu-id="b9673-110">`index.json`및 패키지 등록 데이터 [1426](https://github.com/NuGet/Home/issues/1426) 를 사용할 때 네트워크 사용률 최적화</span><span class="sxs-lookup"><span data-stu-id="b9673-110">Optimized network utilization when working with `index.json` and package registration data [1426](https://github.com/NuGet/Home/issues/1426)</span></span>
* <span data-ttu-id="b9673-111">V2 서비스를 사용 하 여 보다 강력한 리소스 다운로드 처리 기능 [1448](https://github.com/NuGet/Home/issues/1448)</span><span class="sxs-lookup"><span data-stu-id="b9673-111">Improved resource download handling to be more robust with v2 services [1448](https://github.com/NuGet/Home/issues/1448)</span></span>

## <a name="fixes"></a><span data-ttu-id="b9673-112">수정 프로그램</span><span class="sxs-lookup"><span data-stu-id="b9673-112">Fixes</span></span>

* <span data-ttu-id="b9673-113">NuGet 업데이트가 `.csproj` / `.vcxproj` 참조 [1483](https://github.com/NuGet/Home/issues/1483) 를 올바르게 업데이트 합니다.</span><span class="sxs-lookup"><span data-stu-id="b9673-113">NuGet update correctly updates `.csproj`/`.vcxproj` references [1483](https://github.com/NuGet/Home/issues/1483)</span></span>
* <span data-ttu-id="b9673-114">이제 SpecialFolders을 찾을 수 없는 경우 로컬 nuget 폴더가 생성 되지 않도록 합니다. [1531](https://github.com/NuGet/Home/issues/1531)</span><span class="sxs-lookup"><span data-stu-id="b9673-114">Now preventing a local .nuget folder from being created when a SpecialFolders.UserProfile cannot be located [1531](https://github.com/NuGet/Home/issues/1531)</span></span>
* <span data-ttu-id="b9673-115">다운로드 하는 동안 손상 된 로컬 캐시의 패키지 처리 향상 [1405](https://github.com/NuGet/Home/issues/1405) [1157](https://github.com/NuGet/Home/issues/1157)</span><span class="sxs-lookup"><span data-stu-id="b9673-115">Improved handling of packages in local cache that are corrupted during download [1405](https://github.com/NuGet/Home/issues/1405) [1157](https://github.com/NuGet/Home/issues/1157)</span></span>

<span data-ttu-id="b9673-116">명령줄 및 Visual Studio 확장에 대해 해결 된 문제의 전체 목록은 NuGet GitHub [3.2.1 마일스 톤](https://github.com/NuGet/Home/issues?q=milestone%3A3.2.1+is%3Aclosed) 에서 찾을 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="b9673-116">A complete list of issues addressed for the command-line and Visual Studio extension can be found in the NuGet GitHub [3.2.1 milestone](https://github.com/NuGet/Home/issues?q=milestone%3A3.2.1+is%3Aclosed)</span></span>

## <a name="known-issues"></a><span data-ttu-id="b9673-117">알려진 문제</span><span class="sxs-lookup"><span data-stu-id="b9673-117">Known Issues</span></span>

<span data-ttu-id="b9673-118">Microsoft는 GitHub 문제 목록에서 다음 위치에 있는 문제를 계속 추적 합니다. [http://github.com/nuget/home/issues](http://github.com/nuget/home/issues)</span><span class="sxs-lookup"><span data-stu-id="b9673-118">We continue to track issues on our GitHub issues list which can be found at: [http://github.com/nuget/home/issues](http://github.com/nuget/home/issues)</span></span>