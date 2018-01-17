---
title: "NuGet 2.8.1 릴리스 정보 | Microsoft Docs"
author: karann-msft
ms.author: karann-msft
manager: ghogen
ms.date: 11/11/2016
ms.topic: article
ms.prod: nuget
ms.technology: 
ms.assetid: eebbbae4-fc6a-4c05-9102-4ec66b4c64a4
description: "NuGet 2.8.1 포함에 대 한 릴리스 정보는 문제, 버그 수정, 추가 된 기능 및 Dcr 알려져 있습니다."
keywords: "NuGet 2.8.1 릴리스 정보, 버그 수정, 알려진 문제, 추가 기능을 Dcr"
ms.reviewer:
- karann-msft
- unniravindranathan
ms.openlocfilehash: ac33369644d312591bfe8c06540935b2c6063c5d
ms.sourcegitcommit: d0ba99bfe019b779b75731bafdca8a37e35ef0d9
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 12/14/2017
---
# <a name="nuget-281-release-notes"></a><span data-ttu-id="20644-104">NuGet 2.8.1 릴리스 정보</span><span class="sxs-lookup"><span data-stu-id="20644-104">NuGet 2.8.1 Release Notes</span></span>

<span data-ttu-id="20644-105">[NuGet 2.8 릴리스 정보](../release-notes/nuget-2.8.md) | [NuGet 2.8.2 릴리스 정보](../release-notes/nuget-2.8.2.md)</span><span class="sxs-lookup"><span data-stu-id="20644-105">[NuGet 2.8 Release Notes](../release-notes/nuget-2.8.md) | [NuGet 2.8.2 Release Notes](../release-notes/nuget-2.8.2.md)</span></span>

<span data-ttu-id="20644-106">NuGet 2.8.1 2014 년 4 월 2 일에 출시 되었습니다.</span><span class="sxs-lookup"><span data-stu-id="20644-106">NuGet 2.8.1 was released on April 2, 2014.</span></span>

## <a name="notable-features-in-the-release"></a><span data-ttu-id="20644-107">릴리스에서 주목할 만한 기능</span><span class="sxs-lookup"><span data-stu-id="20644-107">Notable features in the release</span></span>

### <a name="support-for-windows-phone-81-projects"></a><span data-ttu-id="20644-108">Windows Phone 8.1 프로젝트에 대 한 지원</span><span class="sxs-lookup"><span data-stu-id="20644-108">Support for Windows Phone 8.1 Projects</span></span>
<span data-ttu-id="20644-109">이 릴리스에서 이제 대상 Windows Phone 8.1 프로젝트에 사용할 수 있는 다음과 같은 새 대상 프레임 워크 모니커를 지원 합니다.</span><span class="sxs-lookup"><span data-stu-id="20644-109">This release now supports the following new target framework monikers which can be used to target Windows Phone 8.1 projects:</span></span>

* <span data-ttu-id="20644-110">WindowsPhone81 / WP81 (Windows Phone Silverlight 기반 프로젝트)의 경우</span><span class="sxs-lookup"><span data-stu-id="20644-110">WindowsPhone81 / WP81 (for Silverlight-based Windows Phone projects)</span></span>
* <span data-ttu-id="20644-111">WindowsPhoneApp81 / WPA81 (WinRT 기반 Windows Phone 앱 프로젝트)의 경우</span><span class="sxs-lookup"><span data-stu-id="20644-111">WindowsPhoneApp81 / WPA81 (for WinRT-based Windows Phone App projects)</span></span>

### <a name="update-of-the-nuget-webmatrix-extension"></a><span data-ttu-id="20644-112">NuGet WebMatrix 확장 업데이트</span><span class="sxs-lookup"><span data-stu-id="20644-112">Update of the NuGet WebMatrix Extension</span></span>
<span data-ttu-id="20644-113">이 릴리스를 WebMatrix에는 NuGet 클라이언트 업데이트 [NuGet.Core](https://www.nuget.org/packages/Nuget.Core/2.6.1) 2.6.1 맡고 XDT 변환을 같은 특징으로 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="20644-113">This release updates the NuGet client found in WebMatrix to [NuGet.Core](https://www.nuget.org/packages/Nuget.Core/2.6.1) 2.6.1 and brings with it features such as XDT transformations.</span></span> <span data-ttu-id="20644-114">2.6.1 무엇 보다도 코어 업데이트를 사용 하면 WebMatrix 클라이언트가 더 최신 버전을 포함 하는 NuGet 패키지를 설치 하는 `.nuspec` ASP.NET NuGet 패키지를 포함 하는 스키마입니다.</span><span class="sxs-lookup"><span data-stu-id="20644-114">More importantly, the 2.6.1 core update enables the WebMatrix client to install NuGet packages which contain more recent versions of the `.nuspec` schema, which includes the ASP.NET NuGet packages.</span></span>

<span data-ttu-id="20644-115">WebMatrix 확장을 업데이트 하는 방법에 대 한 자세한 내용은 해당 특정 참조 [릴리스 정보](../release-notes/nuget-2.6.1-for-WebMatrix.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="20644-115">For more information about the WebMatrix Extension update, see those specific [release notes](../release-notes/nuget-2.6.1-for-WebMatrix.md).</span></span>

### <a name="bug-fixes"></a><span data-ttu-id="20644-116">버그 수정</span><span class="sxs-lookup"><span data-stu-id="20644-116">Bug Fixes</span></span>
<span data-ttu-id="20644-117">이러한 기능 외에도이 버전의 NuGet 다른 버그 수정 포함합니다.</span><span class="sxs-lookup"><span data-stu-id="20644-117">In addition to these features, this release of NuGet includes other bug fixes.</span></span> <span data-ttu-id="20644-118">16 총 문제는 릴리스에서 해결 했습니다.</span><span class="sxs-lookup"><span data-stu-id="20644-118">There were 16 total issues addressed in the release.</span></span> <span data-ttu-id="20644-119">작업의 전체 목록에 대 한 항목에서에서 수정 된 NuGet 2.8.1, 하십시오 보기는 [이 릴리스에 대 한 NuGet 문제 추적기](https://nuget.codeplex.com/workitem/list/advanced?keyword=&status=All&type=All&priority=All&release=NuGet%202.8.1&assignedTo=All&component=All&sortField=LastUpdatedDate&sortDirection=Descending&page=0&reasonClosed=All)합니다.</span><span class="sxs-lookup"><span data-stu-id="20644-119">For a full list of the work items fixed in NuGet 2.8.1, please view the [NuGet Issue Tracker for this release](https://nuget.codeplex.com/workitem/list/advanced?keyword=&status=All&type=All&priority=All&release=NuGet%202.8.1&assignedTo=All&component=All&sortField=LastUpdatedDate&sortDirection=Descending&page=0&reasonClosed=All).</span></span>

### <a name="reshipping-with-visual-studio-14-ctp"></a><span data-ttu-id="20644-120">Visual studio "14" CTP reshipping</span><span class="sxs-lookup"><span data-stu-id="20644-120">Reshipping with Visual Studio "14" CTP</span></span>
<span data-ttu-id="20644-121">Visual Studio "14" ctp 3 번째 2014 년 6 월에 발표에서 NuGet 2.8.1 상자에 함께 제공 됩니다.</span><span class="sxs-lookup"><span data-stu-id="20644-121">In Visual Studio "14" CTP released on June 3rd 2014, NuGet 2.8.1 is shipped in the box.</span></span> <span data-ttu-id="20644-122">아니므로 지원 기능 유지 par에 다른 2.8.1와 Visual Studio 2013에 대 한 것과 같은 VSIXes 합니다.</span><span class="sxs-lookup"><span data-stu-id="20644-122">The features it support remain in-par with other 2.8.1 VSIXes such as the one for Visual Studio 2013.</span></span>