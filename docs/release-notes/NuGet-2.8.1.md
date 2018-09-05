---
title: 2.8.1 NuGet 릴리스 정보
description: NuGet 2.8.1 포함에 대 한 릴리스 정보는 문제, 버그 수정, 추가 된 기능 및 Dcr 알려져 있습니다.
author: karann-msft
ms.author: karann
ms.date: 11/11/2016
ms.topic: conceptual
ms.openlocfilehash: 39fb7db00e18e32eef15adc11764a122c97ddfd5
ms.sourcegitcommit: 1d1406764c6af5fb7801d462e0c4afc9092fa569
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 09/04/2018
ms.locfileid: "43545241"
---
# <a name="nuget-281-release-notes"></a><span data-ttu-id="7785c-103">2.8.1 NuGet 릴리스 정보</span><span class="sxs-lookup"><span data-stu-id="7785c-103">NuGet 2.8.1 Release Notes</span></span>

<span data-ttu-id="7785c-104">[NuGet 2.8 릴리스 정보](../release-notes/nuget-2.8.md) | [2.8.2 NuGet 릴리스 정보](../release-notes/nuget-2.8.2.md)</span><span class="sxs-lookup"><span data-stu-id="7785c-104">[NuGet 2.8 Release Notes](../release-notes/nuget-2.8.md) | [NuGet 2.8.2 Release Notes](../release-notes/nuget-2.8.2.md)</span></span>

<span data-ttu-id="7785c-105">NuGet 2.8.1는 2014 년 4 월 2 일에 출시 되었습니다.</span><span class="sxs-lookup"><span data-stu-id="7785c-105">NuGet 2.8.1 was released on April 2, 2014.</span></span>

## <a name="notable-features-in-the-release"></a><span data-ttu-id="7785c-106">릴리스에서 주목할 만한 기능</span><span class="sxs-lookup"><span data-stu-id="7785c-106">Notable features in the release</span></span>

### <a name="support-for-windows-phone-81-projects"></a><span data-ttu-id="7785c-107">Windows Phone 8.1 프로젝트에 대 한 지원</span><span class="sxs-lookup"><span data-stu-id="7785c-107">Support for Windows Phone 8.1 Projects</span></span>
<span data-ttu-id="7785c-108">이 릴리스에서 이제 Windows Phone 8.1을 대상으로 프로젝트에 사용할 수 있는 다음 새 대상 프레임 워크 모니커를 지원 합니다.</span><span class="sxs-lookup"><span data-stu-id="7785c-108">This release now supports the following new target framework monikers which can be used to target Windows Phone 8.1 projects:</span></span>

* <span data-ttu-id="7785c-109">WindowsPhone81 / WP81 (Windows Phone Silverlight 기반 프로젝트용)</span><span class="sxs-lookup"><span data-stu-id="7785c-109">WindowsPhone81 / WP81 (for Silverlight-based Windows Phone projects)</span></span>
* <span data-ttu-id="7785c-110">WindowsPhoneApp81 / WPA81 (WinRT 기반 Windows Phone 앱 프로젝트)의 경우</span><span class="sxs-lookup"><span data-stu-id="7785c-110">WindowsPhoneApp81 / WPA81 (for WinRT-based Windows Phone App projects)</span></span>

### <a name="update-of-the-nuget-webmatrix-extension"></a><span data-ttu-id="7785c-111">NuGet WebMatrix 확장의 업데이트</span><span class="sxs-lookup"><span data-stu-id="7785c-111">Update of the NuGet WebMatrix Extension</span></span>
<span data-ttu-id="7785c-112">이 릴리스에서 업데이트를 WebMatrix 있는 NuGet 클라이언트 [NuGet.Core](https://www.nuget.org/packages/Nuget.Core/2.6.1) 2.6.1 제공 및 사용 하 여 XDT 변환 같은 기능.</span><span class="sxs-lookup"><span data-stu-id="7785c-112">This release updates the NuGet client found in WebMatrix to [NuGet.Core](https://www.nuget.org/packages/Nuget.Core/2.6.1) 2.6.1 and brings with it features such as XDT transformations.</span></span> <span data-ttu-id="7785c-113">2.6.1 무엇 보다도 core 업데이트 WebMatrix 클라이언트가 포함 하는 최신 버전의 NuGet 패키지를 설치 하는 데 사용 된 `.nuspec` ASP.NET NuGet 패키지를 포함 하는 스키마입니다.</span><span class="sxs-lookup"><span data-stu-id="7785c-113">More importantly, the 2.6.1 core update enables the WebMatrix client to install NuGet packages which contain more recent versions of the `.nuspec` schema, which includes the ASP.NET NuGet packages.</span></span>

<span data-ttu-id="7785c-114">WebMatrix 확장 업데이트에 대 한 자세한 내용은 참조는 특정 [릴리스](../release-notes/nuget-2.6.1-for-WebMatrix.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="7785c-114">For more information about the WebMatrix Extension update, see those specific [release notes](../release-notes/nuget-2.6.1-for-WebMatrix.md).</span></span>

### <a name="bug-fixes"></a><span data-ttu-id="7785c-115">버그 수정</span><span class="sxs-lookup"><span data-stu-id="7785c-115">Bug Fixes</span></span>
<span data-ttu-id="7785c-116">이러한 기능 외에이 릴리스의 NuGet에는 다른 버그 수정을 포함 합니다.</span><span class="sxs-lookup"><span data-stu-id="7785c-116">In addition to these features, this release of NuGet includes other bug fixes.</span></span> <span data-ttu-id="7785c-117">릴리스에서 해결 16 총 문제가 있었습니다.</span><span class="sxs-lookup"><span data-stu-id="7785c-117">There were 16 total issues addressed in the release.</span></span> <span data-ttu-id="7785c-118">작업의 전체 목록은 항목 고정 2.8.1, nuget에서 하세요 보기는 [이 릴리스의 NuGet 문제 추적기](https://nuget.codeplex.com/workitem/list/advanced?keyword=&status=All&type=All&priority=All&release=NuGet%202.8.1&assignedTo=All&component=All&sortField=LastUpdatedDate&sortDirection=Descending&page=0&reasonClosed=All)합니다.</span><span class="sxs-lookup"><span data-stu-id="7785c-118">For a full list of the work items fixed in NuGet 2.8.1, please view the [NuGet Issue Tracker for this release](https://nuget.codeplex.com/workitem/list/advanced?keyword=&status=All&type=All&priority=All&release=NuGet%202.8.1&assignedTo=All&component=All&sortField=LastUpdatedDate&sortDirection=Descending&page=0&reasonClosed=All).</span></span>

### <a name="reshipping-with-visual-studio-14-ctp"></a><span data-ttu-id="7785c-119">Visual studio "14" CTP reshipping</span><span class="sxs-lookup"><span data-stu-id="7785c-119">Reshipping with Visual Studio "14" CTP</span></span>
<span data-ttu-id="7785c-120">타사 2014 년 6 월에 릴리스된 Visual Studio "14" ctp에서는 NuGet 2.8.1 상자에 제공 됩니다.</span><span class="sxs-lookup"><span data-stu-id="7785c-120">In Visual Studio "14" CTP released on June 3rd 2014, NuGet 2.8.1 is shipped in the box.</span></span> <span data-ttu-id="7785c-121">지원 기능 유지 par에서 다른 2.8.1를 사용 하 여 Visual Studio 2013에 대 한 것과 같은 VSIXes 합니다.</span><span class="sxs-lookup"><span data-stu-id="7785c-121">The features it support remain in-par with other 2.8.1 VSIXes such as the one for Visual Studio 2013.</span></span>
