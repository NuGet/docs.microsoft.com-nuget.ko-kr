---
title: "NuGet 2.8.5 릴리스 정보 | Microsoft Docs"
author: karann-msft
ms.author: karann-msft
manager: ghogen
ms.date: 11/11/2016
ms.topic: article
ms.prod: nuget
ms.technology: 
ms.assetid: 60b96b2e-2a61-4f10-b5ad-3299f5a6d453
description: "NuGet 2.8.5 포함에 대 한 릴리스 정보는 문제, 버그 수정, 추가 된 기능 및 Dcr 알려져 있습니다."
keywords: "NuGet 2.8.5 릴리스 정보, 버그 수정, 알려진 문제, 추가 기능을 Dcr"
ms.reviewer:
- karann-msft
- unniravindranathan
ms.openlocfilehash: 3b297704968b8423f60e9de08e27860dc375c019
ms.sourcegitcommit: d0ba99bfe019b779b75731bafdca8a37e35ef0d9
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 12/14/2017
---
# <a name="nuget-285-release-notes"></a><span data-ttu-id="863f1-104">NuGet 2.8.5 릴리스 정보</span><span class="sxs-lookup"><span data-stu-id="863f1-104">NuGet 2.8.5 Release Notes</span></span>

<span data-ttu-id="863f1-105">[NuGet 2.8.3 릴리스 정보](../release-notes/nuget-2.8.3.md) | [NuGet 2.8.6 릴리스 정보](../release-notes/nuget-2.8.6.md)</span><span class="sxs-lookup"><span data-stu-id="863f1-105">[NuGet 2.8.3 Release Notes](../release-notes/nuget-2.8.3.md) | [NuGet 2.8.6 Release Notes](../release-notes/nuget-2.8.6.md)</span></span>

<span data-ttu-id="863f1-106">NuGet 2.8.5 2015 년 3 월 30 일에 발표 되었습니다.</span><span class="sxs-lookup"><span data-stu-id="863f1-106">NuGet 2.8.5 was released March 30, 2015.</span></span> <span data-ttu-id="863f1-107">한 부분 업데이트는 우리의 2.8.3 일부와 VSIX 대상 수정 합니다.</span><span class="sxs-lookup"><span data-stu-id="863f1-107">It is a minor update to our 2.8.3 VSIX with some targeted fixes.</span></span>

<span data-ttu-id="863f1-108">NuGet 패키지 관리자 대화 상자에 대 한 지원이 추가 되었습니다이 릴리스에서 [DNX 대상 프레임 워크 모니커](https://github.com/aspnet/dnx)합니다.</span><span class="sxs-lookup"><span data-stu-id="863f1-108">In this release, the support for NuGet Package Manager dialog was added for [DNX Target Framework Monikers](https://github.com/aspnet/dnx).</span></span>  <span data-ttu-id="863f1-109">지원 되는 이러한 새 프레임 워크 모니커는 다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="863f1-109">These new framework monikers that are supported include:</span></span>

* <span data-ttu-id="863f1-110">**core50** -는 'base' 대상 Core CLR 호환 되는 프레임 워크 모니커 (TFM).</span><span class="sxs-lookup"><span data-stu-id="863f1-110">**core50** - A 'base' target framework moniker (TFM) that is compatible with the Core CLR.</span></span>
* <span data-ttu-id="863f1-111">**dnx452** -전체 4.5.2를 사용 하 여 A TFM DNX 기반 특정 앱의 프레임 워크 버전</span><span class="sxs-lookup"><span data-stu-id="863f1-111">**dnx452** - A TFM specific to DNX-based apps using the full 4.5.2 version of the framework</span></span>
* <span data-ttu-id="863f1-112">**dnx46** -4.6 전체 버전의 framework 사용 하 여 A TFM DNX 기반 특정 앱</span><span class="sxs-lookup"><span data-stu-id="863f1-112">**dnx46** - A TFM specific to DNX-based apps using the full 4.6 version of the framework</span></span>
* <span data-ttu-id="863f1-113">**dnxcore50** -Core 5.0 버전의 framework 사용 하 여 A TFM DNX 기반 특정 앱</span><span class="sxs-lookup"><span data-stu-id="863f1-113">**dnxcore50** - A TFM specific to DNX-based apps using the Core 5.0 version of the framework</span></span>

<span data-ttu-id="863f1-114">FSharp 프로젝트에 제대로 설치에서 금지 패키지 하 한 버그 수정:</span><span class="sxs-lookup"><span data-stu-id="863f1-114">One bug was fixed that prevented packages from installing into FSharp projects properly:</span></span>

<span data-ttu-id="863f1-115">https://nuget.codeplex.com/workitem/4400</span><span class="sxs-lookup"><span data-stu-id="863f1-115">https://nuget.codeplex.com/workitem/4400</span></span>