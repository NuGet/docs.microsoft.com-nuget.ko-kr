---
title: NuGet 2.8.5 릴리스 정보
description: 알려진 문제, 버그 수정, 추가 된 기능 및 2.8.5를 포함 하는 NuGet에 대 한 릴리스 정보입니다.
author: JonDouglas
ms.author: jodou
ms.date: 11/11/2016
ms.topic: conceptual
ms.openlocfilehash: f729092bc964b286a007564bd3bbd8c79bc895c9
ms.sourcegitcommit: ee6c3f203648a5561c809db54ebeb1d0f0598b68
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 01/26/2021
ms.locfileid: "98780359"
---
# <a name="nuget-285-release-notes"></a><span data-ttu-id="61e99-103">NuGet 2.8.5 릴리스 정보</span><span class="sxs-lookup"><span data-stu-id="61e99-103">NuGet 2.8.5 Release Notes</span></span>

<span data-ttu-id="61e99-104">[NuGet 2.8.3 릴리스 정보](../release-notes/nuget-2.8.3.md)  |  [NuGet 2.8.6 릴리스 정보](../release-notes/nuget-2.8.6.md)</span><span class="sxs-lookup"><span data-stu-id="61e99-104">[NuGet 2.8.3 Release Notes](../release-notes/nuget-2.8.3.md) | [NuGet 2.8.6 Release Notes](../release-notes/nuget-2.8.6.md)</span></span>

<span data-ttu-id="61e99-105">NuGet 2.8.5는 2015 년 3 월 30 일에 출시 되었습니다.</span><span class="sxs-lookup"><span data-stu-id="61e99-105">NuGet 2.8.5 was released March 30, 2015.</span></span> <span data-ttu-id="61e99-106">2.8.3 VSIX에 대 한 사소한 업데이트 이며 일부 대상 수정이 있습니다.</span><span class="sxs-lookup"><span data-stu-id="61e99-106">It is a minor update to our 2.8.3 VSIX with some targeted fixes.</span></span>

<span data-ttu-id="61e99-107">이 릴리스에서는 [Dnx 대상 프레임 워크 모니커에](https://github.com/aspnet/dnx)대해 NuGet 패키지 관리자에 대 한 지원이 추가 되었습니다.</span><span class="sxs-lookup"><span data-stu-id="61e99-107">In this release, the support for NuGet Package Manager dialog was added for [DNX Target Framework Monikers](https://github.com/aspnet/dnx).</span></span>  <span data-ttu-id="61e99-108">지원 되는 새로운 프레임 워크 모니커는 다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="61e99-108">These new framework monikers that are supported include:</span></span>

* <span data-ttu-id="61e99-109">**core50** -핵심 CLR과 호환 되는 ' 기본 ' TFM (대상 프레임 워크 모니커)입니다.</span><span class="sxs-lookup"><span data-stu-id="61e99-109">**core50** - A 'base' target framework moniker (TFM) that is compatible with the Core CLR.</span></span>
* <span data-ttu-id="61e99-110">**dnx452** -전체 4.5.2 버전의 프레임 워크를 사용 하는 dnx 기반 앱 관련 TFM</span><span class="sxs-lookup"><span data-stu-id="61e99-110">**dnx452** - A TFM specific to DNX-based apps using the full 4.5.2 version of the framework</span></span>
* <span data-ttu-id="61e99-111">**dnx46** -전체 4.6 버전의 프레임 워크를 사용 하는 dnx 기반 앱 관련 TFM</span><span class="sxs-lookup"><span data-stu-id="61e99-111">**dnx46** - A TFM specific to DNX-based apps using the full 4.6 version of the framework</span></span>
* <span data-ttu-id="61e99-112">**dnxcore50** -핵심 5.0 버전의 프레임 워크를 사용 하는 dnx 기반 앱과 관련 된 TFM</span><span class="sxs-lookup"><span data-stu-id="61e99-112">**dnxcore50** - A TFM specific to DNX-based apps using the Core 5.0 version of the framework</span></span>

<span data-ttu-id="61e99-113">패키지를 Fsharp.core 프로젝트에 제대로 설치 하지 못하게 하는 한 가지 버그가 수정 되었습니다.</span><span class="sxs-lookup"><span data-stu-id="61e99-113">One bug was fixed that prevented packages from installing into FSharp projects properly:</span></span>

https://nuget.codeplex.com/workitem/4400