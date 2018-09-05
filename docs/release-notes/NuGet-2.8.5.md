---
title: 2.8.5 NuGet 릴리스 정보
description: NuGet 2.8.5 포함에 대 한 릴리스 정보는 문제, 버그 수정, 추가 된 기능 및 Dcr 알려져 있습니다.
author: karann-msft
ms.author: karann
ms.date: 11/11/2016
ms.topic: conceptual
ms.openlocfilehash: aa03b00a0043a4805f33900124c13b0777c2b7a3
ms.sourcegitcommit: 1d1406764c6af5fb7801d462e0c4afc9092fa569
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 09/04/2018
ms.locfileid: "43548627"
---
# <a name="nuget-285-release-notes"></a><span data-ttu-id="d0895-103">2.8.5 NuGet 릴리스 정보</span><span class="sxs-lookup"><span data-stu-id="d0895-103">NuGet 2.8.5 Release Notes</span></span>

<span data-ttu-id="d0895-104">[NuGet 2.8.3 릴리스 정보](../release-notes/nuget-2.8.3.md) | [2.8.6 NuGet 릴리스 정보](../release-notes/nuget-2.8.6.md)</span><span class="sxs-lookup"><span data-stu-id="d0895-104">[NuGet 2.8.3 Release Notes](../release-notes/nuget-2.8.3.md) | [NuGet 2.8.6 Release Notes](../release-notes/nuget-2.8.6.md)</span></span>

<span data-ttu-id="d0895-105">NuGet 2.8.5 2015 년 3 월 30 일에 출시 되었습니다.</span><span class="sxs-lookup"><span data-stu-id="d0895-105">NuGet 2.8.5 was released March 30, 2015.</span></span> <span data-ttu-id="d0895-106">사소한 업데이트는 2.8.3 VSIX 일부를 사용 하 여 대상 수정 합니다.</span><span class="sxs-lookup"><span data-stu-id="d0895-106">It is a minor update to our 2.8.3 VSIX with some targeted fixes.</span></span>

<span data-ttu-id="d0895-107">이 릴리스에서 NuGet 패키지 관리자 대화 상자에 대 한 지원에 대 한 추가 되었습니다 [DNX 대상 프레임 워크 모니커의](https://github.com/aspnet/dnx)합니다.</span><span class="sxs-lookup"><span data-stu-id="d0895-107">In this release, the support for NuGet Package Manager dialog was added for [DNX Target Framework Monikers](https://github.com/aspnet/dnx).</span></span>  <span data-ttu-id="d0895-108">지원 되는 이러한 새 프레임 워크 모니커는 다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="d0895-108">These new framework monikers that are supported include:</span></span>

* <span data-ttu-id="d0895-109">**core50** -'base' 대상 Core CLR 호환 되는 프레임 워크 모니커 (TFM).</span><span class="sxs-lookup"><span data-stu-id="d0895-109">**core50** - A 'base' target framework moniker (TFM) that is compatible with the Core CLR.</span></span>
* <span data-ttu-id="d0895-110">**dnx452** -전체 4.5.2를 사용 하는 TFM DNX 기반 특정 앱 프레임 워크의 버전</span><span class="sxs-lookup"><span data-stu-id="d0895-110">**dnx452** - A TFM specific to DNX-based apps using the full 4.5.2 version of the framework</span></span>
* <span data-ttu-id="d0895-111">**dnx46** -프레임 워크의 전체 4.6 버전을 사용 하는 TFM DNX 기반 특정 앱</span><span class="sxs-lookup"><span data-stu-id="d0895-111">**dnx46** - A TFM specific to DNX-based apps using the full 4.6 version of the framework</span></span>
* <span data-ttu-id="d0895-112">**dnxcore50** -Core 5.0 버전의 framework 사용 하 여는 TFM DNX 기반 관련 앱</span><span class="sxs-lookup"><span data-stu-id="d0895-112">**dnxcore50** - A TFM specific to DNX-based apps using the Core 5.0 version of the framework</span></span>

<span data-ttu-id="d0895-113">하나의 버그가 방지 패키지를 사용 하는 FSharp 프로젝트에 제대로 설치에서 수정 된:</span><span class="sxs-lookup"><span data-stu-id="d0895-113">One bug was fixed that prevented packages from installing into FSharp projects properly:</span></span>

https://nuget.codeplex.com/workitem/4400