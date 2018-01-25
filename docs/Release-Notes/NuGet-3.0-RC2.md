---
title: "NuGet 3.0 RC2 릴리스 정보 | Microsoft Docs"
author: karann-msft
ms.author: karann-msft
manager: ghogen
ms.date: 11/11/2016
ms.topic: article
ms.prod: nuget
ms.technology: 
description: "NuGet 3.0 r c 2에 대 한 릴리스 정보를 알려진된 문제, 버그 수정, 추가 된 기능 및 Dcr를 포함 합니다."
keywords: "NuGet 3.0 RC2 릴리스 정보, 버그 수정, 알려진 문제, 추가 기능을 Dcr"
ms.reviewer:
- karann-msft
- unniravindranathan
ms.openlocfilehash: 67299408170ae3c3676c2866bec2945b41ad4184
ms.sourcegitcommit: 262d026beeffd4f3b6fc47d780a2f701451663a8
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 01/25/2018
---
# <a name="nuget-30-rc2-release-notes"></a><span data-ttu-id="f83c8-104">NuGet 3.0 RC2 릴리스 정보</span><span class="sxs-lookup"><span data-stu-id="f83c8-104">NuGet 3.0 RC2 Release Notes</span></span>

<span data-ttu-id="f83c8-105">[NuGet 3.0 RC 릴리스 정보](../release-notes/nuget-3.0-RC.md) | [NuGet 3.0 릴리스 정보](../release-notes/nuget-3.0.0.md)</span><span class="sxs-lookup"><span data-stu-id="f83c8-105">[NuGet 3.0 RC Release Notes](../release-notes/nuget-3.0-RC.md) | [NuGet 3.0 Release Notes](../release-notes/nuget-3.0.0.md)</span></span>

<span data-ttu-id="f83c8-106">릴리스를 사용할 수 있는 Visual Studio 2015 확장 갤러리에서로 NuGet 3.0 RC2 2015 년 6 월 3 일에 출시 및 [Codeplex](https://nuget.codeplex.com/releases/view/615507)합니다.</span><span class="sxs-lookup"><span data-stu-id="f83c8-106">NuGet 3.0 RC2 was released on June 3, 2015 as an interim release available from the Visual Studio 2015 Extension Gallery and [Codeplex](https://nuget.codeplex.com/releases/view/615507).</span></span> <span data-ttu-id="f83c8-107">이 릴리스에 다양 한 중요 한 버그 수정 및 성능 향상을 이끌어 더 쉬워집니다 된 완료 된 Visual Studio 2015 릴리스 전에 해제 하는 것이 중요 합니다.</span><span class="sxs-lookup"><span data-stu-id="f83c8-107">This release has a number of important bug fixes and performance improvements that we felt were important to release before the completed Visual Studio 2015 release.</span></span> <span data-ttu-id="f83c8-108">이 NuGet 확장 버전은 Visual Studio 2015에 사용할 수만 있습니다.</span><span class="sxs-lookup"><span data-stu-id="f83c8-108">This NuGet extension version is only available for Visual Studio 2015.</span></span>

<span data-ttu-id="f83c8-109">전체적으로 우리 158이 릴리스의 문제 닫히고 검토할 수 있습니다는 [문제 GitHub에서의 전체 목록은](https://github.com/NuGet/Home/issues?utf8=%E2%9C%93&q=is%3Aclosed+milestone%3A3.0.0-RTM+sort%3Aupdated-asc+updated%3A%3C%3D2015-06-01)합니다.</span><span class="sxs-lookup"><span data-stu-id="f83c8-109">In total, we closed 158 issues in this release, and you can review the [complete list of issues on GitHub](https://github.com/NuGet/Home/issues?utf8=%E2%9C%93&q=is%3Aclosed+milestone%3A3.0.0-RTM+sort%3Aupdated-asc+updated%3A%3C%3D2015-06-01).</span></span>

## <a name="summary-of-top-issues-resolved"></a><span data-ttu-id="f83c8-110">주요 문제 해결의 요약</span><span class="sxs-lookup"><span data-stu-id="f83c8-110">Summary of top issues resolved</span></span>

* [<span data-ttu-id="f83c8-111">패키지 관리자 창을 새로 고칠 때 자주 네트워크 업데이트 호출</span><span class="sxs-lookup"><span data-stu-id="f83c8-111">Frequent network update calls when package manager window refreshes</span></span>](https://github.com/NuGet/Home/issues/515)
* [<span data-ttu-id="f83c8-112">패키지 관리자에 보기를 설치를 변경 하면 스크롤 지연</span><span class="sxs-lookup"><span data-stu-id="f83c8-112">Delayed scroll when changing to installed view in package manager</span></span>](https://github.com/NuGet/Home/issues/519)
* [<span data-ttu-id="f83c8-113">백그라운드 스레드에서 네트워크 호출을 실행 해야</span><span class="sxs-lookup"><span data-stu-id="f83c8-113">Network calls should be run on a background thread</span></span>](https://github.com/NuGet/Home/issues/516)
* [<span data-ttu-id="f83c8-114">'미리 보기 창 표시 안 함' 확인란을 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="f83c8-114">Added 'Do not show preview window' checkbox</span></span>](https://github.com/NuGet/Home/issues/566)
* [<span data-ttu-id="f83c8-115">추가 된 프로세스 프로세서 사용량을 줄이기 위해 조절</span><span class="sxs-lookup"><span data-stu-id="f83c8-115">Added process throttling to reduce processor usage</span></span>](https://github.com/NuGet/Home/issues/356)
* <span data-ttu-id="f83c8-116">쉽게 이식 가능한 클래스 라이브러리 참조 처리</span><span class="sxs-lookup"><span data-stu-id="f83c8-116">Improved portable-class-library reference handling</span></span>
    * [<span data-ttu-id="f83c8-117">https://github.com/NuGet/Home/issues/562</span><span class="sxs-lookup"><span data-stu-id="f83c8-117">https://github.com/NuGet/Home/issues/562</span></span>](https://github.com/NuGet/Home/issues/562)
    * [<span data-ttu-id="f83c8-118">https://github.com/NuGet/Home/issues/454</span><span class="sxs-lookup"><span data-stu-id="f83c8-118">https://github.com/NuGet/Home/issues/454</span></span>](https://github.com/NuGet/Home/issues/454)
    * [<span data-ttu-id="f83c8-119">https://github.com/NuGet/Home/issues/440</span><span class="sxs-lookup"><span data-stu-id="f83c8-119">https://github.com/NuGet/Home/issues/440</span></span>](https://github.com/NuGet/Home/issues/440)
* [<span data-ttu-id="f83c8-120">자동 완성 서비스에서 대/소문자 구분</span><span class="sxs-lookup"><span data-stu-id="f83c8-120">Autocomplete service was case sensitive</span></span>](https://github.com/NuGet/Home/issues/198)
* [<span data-ttu-id="f83c8-121">기본 인증 자격 증명을 다시 삽입 하는 업데이트</span><span class="sxs-lookup"><span data-stu-id="f83c8-121">Update to reintroduce basic auth credentials</span></span>](https://github.com/NuGet/Home/issues/456)
* [<span data-ttu-id="f83c8-122">향상 된 오류 로깅</span><span class="sxs-lookup"><span data-stu-id="f83c8-122">Improved error logging</span></span>](https://github.com/NuGet/Home/issues/407)
* [<span data-ttu-id="f83c8-123">업데이트 패키지를 호출할 때 향상 된 powershell 오류 메시지</span><span class="sxs-lookup"><span data-stu-id="f83c8-123">Improved powershell error messages when calling Update-Package</span></span>](https://github.com/NuGet/Home/issues/5)

<span data-ttu-id="f83c8-124">이 다운로드 [NuGet 확장 프로그램에 업데이트](https://nuget.codeplex.com/releases/view/615507) Codeplex에서에 유의 하십시오 및 [블로그에서](http://blog.nuget.org) 자세한 진행률 및 NuGet 3.0에 대 한 공지 사항!</span><span class="sxs-lookup"><span data-stu-id="f83c8-124">Download this [update to the NuGet extension](https://nuget.codeplex.com/releases/view/615507) from Codeplex and please keep an eye on [our blog](http://blog.nuget.org) for more progress and announcements for NuGet 3.0!</span></span>