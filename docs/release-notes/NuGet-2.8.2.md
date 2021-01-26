---
title: NuGet 2.8.2 릴리스 정보
description: 알려진 문제, 버그 수정, 추가 된 기능 및 2.8.2를 포함 하는 NuGet에 대 한 릴리스 정보입니다.
author: JonDouglas
ms.author: jodou
ms.date: 11/11/2016
ms.topic: conceptual
ms.openlocfilehash: d39f2dc9a429ed264461174325c2080468fa8aae
ms.sourcegitcommit: ee6c3f203648a5561c809db54ebeb1d0f0598b68
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 01/26/2021
ms.locfileid: "98780369"
---
# <a name="nuget-282-release-notes"></a><span data-ttu-id="e2491-103">NuGet 2.8.2 릴리스 정보</span><span class="sxs-lookup"><span data-stu-id="e2491-103">NuGet 2.8.2 Release Notes</span></span>

<span data-ttu-id="e2491-104">[NuGet 2.8.1 릴리스 정보](../release-notes/nuget-2.8.1.md)  |  [NuGet 2.8.3 릴리스 정보](../release-notes/nuget-2.8.3.md)</span><span class="sxs-lookup"><span data-stu-id="e2491-104">[NuGet 2.8.1 Release Notes](../release-notes/nuget-2.8.1.md) | [NuGet 2.8.3 Release Notes](../release-notes/nuget-2.8.3.md)</span></span>

<span data-ttu-id="e2491-105">NuGet 2.8.2는 2014 년 5 월 22 일에 릴리스 되었습니다.</span><span class="sxs-lookup"><span data-stu-id="e2491-105">NuGet 2.8.2 was released on May 22, 2014.</span></span>  <span data-ttu-id="e2491-106">이 릴리스에는 nuget.exe 명령줄, NuGet. 서버 패키지 및 기타 NuGet 패키지에 대 한 변경 내용만 포함 되었습니다.</span><span class="sxs-lookup"><span data-stu-id="e2491-106">This release only included changes to the nuget.exe command-line, the NuGet.Server package and other NuGet packages.</span></span>  <span data-ttu-id="e2491-107">릴리스에 업데이트 된 Visual Studio 확장 또는 WebMatrix 확장이 포함 되어 있지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="e2491-107">The release did not include an updated Visual Studio extension or WebMatrix extension.</span></span>

## <a name="notable-updates"></a><span data-ttu-id="e2491-108">주목할 만한 업데이트</span><span class="sxs-lookup"><span data-stu-id="e2491-108">Notable Updates</span></span>

<span data-ttu-id="e2491-109">가장 주목할 만한 업데이트는 nuget.exe 명령줄과 NuGet. 서버 패키지 (자체 호스팅 NuGet 피드의 경우)에 있습니다.</span><span class="sxs-lookup"><span data-stu-id="e2491-109">The most notable updates were in the nuget.exe command-line and the NuGet.Server package (for self-hosted NuGet feeds).</span></span>

### <a name="important-nugetexe-bug-fixes"></a><span data-ttu-id="e2491-110">중요 nuget.exe 버그 수정</span><span class="sxs-lookup"><span data-stu-id="e2491-110">Important nuget.exe Bug Fixes</span></span>

1. [<span data-ttu-id="e2491-111">nuget.exe 푸시가 실패 하 고 다시 시도 합니다.</span><span class="sxs-lookup"><span data-stu-id="e2491-111">nuget.exe Push fails and keeps retrying</span></span>](https://nuget.codeplex.com/workitem/4000)
1. [<span data-ttu-id="e2491-112">nuget.exe Push는 기본 인증 자격 증명을 올바르게 보내지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="e2491-112">nuget.exe Push does not send Basic Auth credentials correctly</span></span>](https://nuget.codeplex.com/workitem/4109)
1. [<span data-ttu-id="e2491-113">nuget.exe 푸시는 임시 리디렉션을 따르지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="e2491-113">nuget.exe Push won't follow temporary redirect</span></span>](https://nuget.codeplex.com/workitem/4050)

### <a name="important-nugetserver-bug-fix"></a><span data-ttu-id="e2491-114">중요 NuGet. 서버 버그 수정</span><span class="sxs-lookup"><span data-stu-id="e2491-114">Important NuGet.Server Bug Fix</span></span>

1. [<span data-ttu-id="e2491-115">NuGet. 서버에서 반환 된 IsAbsoluteLatestVersion의 값이 잘못 되었습니다.</span><span class="sxs-lookup"><span data-stu-id="e2491-115">Wrong value of IsAbsoluteLatestVersion returned by NuGet.Server</span></span>](https://nuget.codeplex.com/workitem/4147)

## <a name="packages-updated"></a><span data-ttu-id="e2491-116">패키지가 업데이트 됨</span><span class="sxs-lookup"><span data-stu-id="e2491-116">Packages Updated</span></span>

<span data-ttu-id="e2491-117">nuget.exe 명령줄 및 NuGet. 서버 픽스는 NuGet 패키지 업데이트로 제공 됩니다.</span><span class="sxs-lookup"><span data-stu-id="e2491-117">The nuget.exe command-line and NuGet.Server fixes are shipped as NuGet package updates.</span></span>  <span data-ttu-id="e2491-118">2.8.2으로 업데이트 된 다른 패키지도 있습니다.</span><span class="sxs-lookup"><span data-stu-id="e2491-118">There were other packages updated with 2.8.2 as well.</span></span>

<span data-ttu-id="e2491-119">업데이트 된 패키지 목록은 다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="e2491-119">Here's the list of updated packages:</span></span>

1. [<span data-ttu-id="e2491-120">NuGet. 핵심</span><span class="sxs-lookup"><span data-stu-id="e2491-120">NuGet.Core</span></span>](https://www.nuget.org/packages/NuGet.Core/)
1. [<span data-ttu-id="e2491-121">NuGet 명령줄</span><span class="sxs-lookup"><span data-stu-id="e2491-121">NuGet.CommandLine</span></span>](https://www.nuget.org/packages/NuGet.CommandLine/)
1. [<span data-ttu-id="e2491-122">NuGet.Server</span><span class="sxs-lookup"><span data-stu-id="e2491-122">NuGet.Server</span></span>](https://www.nuget.org/packages/NuGet.Server/)
1. [<span data-ttu-id="e2491-123">NuGet 빌드</span><span class="sxs-lookup"><span data-stu-id="e2491-123">NuGet.Build</span></span>](https://www.nuget.org/packages/NuGet.Build/)
1. <span data-ttu-id="e2491-124">[VisualStudio](https://www.nuget.org/packages/NuGet.VisualStudio/) (확장명이 아닌 패키지)</span><span class="sxs-lookup"><span data-stu-id="e2491-124">[NuGet.VisualStudio](https://www.nuget.org/packages/NuGet.VisualStudio/) (the package, not the extension)</span></span>

## <a name="all-changes"></a><span data-ttu-id="e2491-125">모든 변경 내용</span><span class="sxs-lookup"><span data-stu-id="e2491-125">All Changes</span></span>
<span data-ttu-id="e2491-126">릴리스에서는 10 개의 문제가 해결 되었습니다.</span><span class="sxs-lookup"><span data-stu-id="e2491-126">There were 10 issues addressed in the release.</span></span> <span data-ttu-id="e2491-127">NuGet 2.8.2에서 수정 된 작업 항목의 전체 목록은 [이 릴리스에 대 한 Nuget 문제 추적기](https://nuget.codeplex.com/workitem/list/advanced?keyword=&status=All&type=All&priority=All&release=NuGet%202.8.2&assignedTo=All&component=All&sortField=LastUpdatedDate&sortDirection=Descending&page=0&reasonClosed=All)를 확인 하세요.</span><span class="sxs-lookup"><span data-stu-id="e2491-127">For a full list of the work items fixed in NuGet 2.8.2, please view the [NuGet Issue Tracker for this release](https://nuget.codeplex.com/workitem/list/advanced?keyword=&status=All&type=All&priority=All&release=NuGet%202.8.2&assignedTo=All&component=All&sortField=LastUpdatedDate&sortDirection=Descending&page=0&reasonClosed=All).</span></span>
