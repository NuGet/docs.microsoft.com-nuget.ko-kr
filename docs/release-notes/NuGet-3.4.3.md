---
title: NuGet 3.4.3 릴리스 정보
description: NuGet 3.4.3 포함에 대 한 릴리스 정보는 문제, 버그 수정, 추가 된 기능 및 Dcr 알려져 있습니다.
author: karann-msft
ms.author: karann
manager: unnir
ms.date: 11/11/2016
ms.topic: conceptual
ms.openlocfilehash: 6c25d3b678e6e72eca3e1157f91a75bfa8cbb18e
ms.sourcegitcommit: 3eab9c4dd41ea7ccd2c28bb5ab16f6fbbec13708
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/26/2018
ms.locfileid: "31820328"
---
# <a name="nuget-343-release-notes"></a><span data-ttu-id="6e103-103">NuGet 3.4.3 릴리스 정보</span><span class="sxs-lookup"><span data-stu-id="6e103-103">NuGet 3.4.3 Release Notes</span></span>

<span data-ttu-id="6e103-104">[NuGet 3.4.2 릴리스 정보](../release-notes/nuget-3.4.2.md) | [NuGet 3.4.4 릴리스 정보](../release-notes/nuget-3.4.4.md)</span><span class="sxs-lookup"><span data-stu-id="6e103-104">[NuGet 3.4.2 Release Notes](../release-notes/nuget-3.4.2.md) | [NuGet 3.4.4 Release Notes](../release-notes/nuget-3.4.4.md)</span></span>

<span data-ttu-id="6e103-105">3.4.3 NuGet 3.4 및 이후 버전에서 식별 된 몇 가지 문제를 해결 하기 위해 2016 년 4 월 22 일에 출시 되었습니다.</span><span class="sxs-lookup"><span data-stu-id="6e103-105">NuGet 3.4.3 was released on April 22, 2016 to address several issues that were identified in the 3.4 and subsequent releases.</span></span>

<span data-ttu-id="6e103-106">VSIX와 nuget.exe를 다운로드할 수 있습니다 [여기](https://dist.nuget.org/index.html)합니다.</span><span class="sxs-lookup"><span data-stu-id="6e103-106">You can download both the VSIX and nuget.exe [here](https://dist.nuget.org/index.html).</span></span>

## <a name="updates-and-improvements"></a><span data-ttu-id="6e103-107">업데이트 및 향상 기능</span><span class="sxs-lookup"><span data-stu-id="6e103-107">Updates and Improvements</span></span>

* <span data-ttu-id="6e103-108">Visual Studio 안정성이 향상된 됩니다.</span><span class="sxs-lookup"><span data-stu-id="6e103-108">Improved Visual Studio reliability.</span></span> <span data-ttu-id="6e103-109">Visual Studio에서 충돌 발생 시킨 NuGet에서 몇 가지 문제를 해결 했습니다.</span><span class="sxs-lookup"><span data-stu-id="6e103-109">We have fixed some issues in NuGet that caused crashes in Visual Studio.</span></span>

## <a name="fixes"></a><span data-ttu-id="6e103-110">수정 프로그램</span><span class="sxs-lookup"><span data-stu-id="6e103-110">Fixes</span></span>

* <span data-ttu-id="6e103-111">피드 암호로 보호 된 개인 nuget이 포함 된 일부 인증 문제가 해결 되었습니다.</span><span class="sxs-lookup"><span data-stu-id="6e103-111">Fixed some authorization issues with password protected private nuget feeds.</span></span>
* <span data-ttu-id="6e103-112">주위에서 PCL 복원할 수 없는 문제가 해결 되었습니다. `project.json` 지정 런타임을 사용 하 여 합니다.</span><span class="sxs-lookup"><span data-stu-id="6e103-112">Fixed an issue around being unable to restore PCL's from `project.json` with runtimes specified.</span></span>
* <span data-ttu-id="6e103-113">일부 고객 실행 중이 던 일시적인 오류가 발생에 패키지를 설치할 때.</span><span class="sxs-lookup"><span data-stu-id="6e103-113">Some customers were running into intermittent failures when installing packages.</span></span> <span data-ttu-id="6e103-114">이제이 릴리스에서 수정 되었습니다.</span><span class="sxs-lookup"><span data-stu-id="6e103-114">This has now been fixed in this release.</span></span>
* <span data-ttu-id="6e103-115">C + 복원 실패를 발생 시킨 문제가 해결 되었습니다. + /CLI 프로젝트와 `project.json`합니다.</span><span class="sxs-lookup"><span data-stu-id="6e103-115">Fixed an issue that caused restore failures in C++/CLI projects with `project.json`.</span></span>
* <span data-ttu-id="6e103-116">사용 되 고 있지 푼 올바르게 모노에서 nuget을 사용할 때 일부 패키지 (예: ModernHttpClient).</span><span class="sxs-lookup"><span data-stu-id="6e103-116">Some packages (E.g ModernHttpClient) where not being unzipped correctly when you use nuget in mono.</span></span> <span data-ttu-id="6e103-117">이제이 릴리스에서 수정 되었습니다.</span><span class="sxs-lookup"><span data-stu-id="6e103-117">This has now been fixed in this release.</span></span>

<span data-ttu-id="6e103-118">수정 사항 및이 릴리스에서 향상 된 전체 목록은 체크 아웃 문제 목록 [여기](https://github.com/NuGet/Home/issues?q=is%3Aissue+milestone%3A3.4.3+is%3Aclosed)합니다.</span><span class="sxs-lookup"><span data-stu-id="6e103-118">For the complete list of fixes and improvements in this release, check out the list of issues [here](https://github.com/NuGet/Home/issues?q=is%3Aissue+milestone%3A3.4.3+is%3Aclosed).</span></span>