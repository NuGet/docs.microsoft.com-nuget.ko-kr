---
title: NuGet 3.4.3 릴리스 정보
description: 알려진 문제, 버그 수정, 추가 된 기능 및 3.4.3를 포함 하는 NuGet에 대 한 릴리스 정보입니다.
author: JonDouglas
ms.author: jodou
ms.date: 11/11/2016
ms.topic: conceptual
ms.openlocfilehash: f0d9740aaf0a82b9e4023b5e4990c8f4adbea63c
ms.sourcegitcommit: ee6c3f203648a5561c809db54ebeb1d0f0598b68
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 01/26/2021
ms.locfileid: "98776469"
---
# <a name="nuget-343-release-notes"></a><span data-ttu-id="1de75-103">NuGet 3.4.3 릴리스 정보</span><span class="sxs-lookup"><span data-stu-id="1de75-103">NuGet 3.4.3 Release Notes</span></span>

<span data-ttu-id="1de75-104">[NuGet 3.4.2 릴리스 정보](../release-notes/nuget-3.4.2.md)  |  [NuGet 3.4.4 릴리스 정보](../release-notes/nuget-3.4.4.md)</span><span class="sxs-lookup"><span data-stu-id="1de75-104">[NuGet 3.4.2 Release Notes](../release-notes/nuget-3.4.2.md) | [NuGet 3.4.4 Release Notes](../release-notes/nuget-3.4.4.md)</span></span>

<span data-ttu-id="1de75-105">NuGet 3.4.3는 3.4 및 이후 릴리스에서 확인 된 몇 가지 문제를 해결 하기 위해 2016 년 4 월 22 일에 릴리스 되었습니다.</span><span class="sxs-lookup"><span data-stu-id="1de75-105">NuGet 3.4.3 was released on April 22, 2016 to address several issues that were identified in the 3.4 and subsequent releases.</span></span>

<span data-ttu-id="1de75-106">VSIX를 다운로드 하 고 [여기](https://dist.nuget.org/index.html)에서 nuget.exe 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="1de75-106">You can download both the VSIX and nuget.exe [here](https://dist.nuget.org/index.html).</span></span>

## <a name="updates-and-improvements"></a><span data-ttu-id="1de75-107">업데이트 및 개선 사항</span><span class="sxs-lookup"><span data-stu-id="1de75-107">Updates and Improvements</span></span>

* <span data-ttu-id="1de75-108">향상 된 Visual Studio 안정성.</span><span class="sxs-lookup"><span data-stu-id="1de75-108">Improved Visual Studio reliability.</span></span> <span data-ttu-id="1de75-109">Visual Studio에서 충돌을 일으킨 NuGet 문제를 해결 했습니다.</span><span class="sxs-lookup"><span data-stu-id="1de75-109">We have fixed some issues in NuGet that caused crashes in Visual Studio.</span></span>

## <a name="fixes"></a><span data-ttu-id="1de75-110">수정 프로그램</span><span class="sxs-lookup"><span data-stu-id="1de75-110">Fixes</span></span>

* <span data-ttu-id="1de75-111">암호로 보호 되는 개인 nuget 피드의 몇 가지 권한 부여 문제를 수정 했습니다.</span><span class="sxs-lookup"><span data-stu-id="1de75-111">Fixed some authorization issues with password protected private nuget feeds.</span></span>
* <span data-ttu-id="1de75-112">지정 된 런타임을 사용 하 여 PCL을 복원할 수 없는 문제를 해결 `project.json` 했습니다.</span><span class="sxs-lookup"><span data-stu-id="1de75-112">Fixed an issue around being unable to restore PCL's from `project.json` with runtimes specified.</span></span>
* <span data-ttu-id="1de75-113">일부 고객은 패키지를 설치할 때 일시적인 오류가 발생 했습니다.</span><span class="sxs-lookup"><span data-stu-id="1de75-113">Some customers were running into intermittent failures when installing packages.</span></span> <span data-ttu-id="1de75-114">이제이 릴리스에서 수정 되었습니다.</span><span class="sxs-lookup"><span data-stu-id="1de75-114">This has now been fixed in this release.</span></span>
* <span data-ttu-id="1de75-115">를 사용 하 여 c + +/CLI 프로젝트에서 복원 실패를 야기 하는 문제를 해결 `project.json` 했습니다.</span><span class="sxs-lookup"><span data-stu-id="1de75-115">Fixed an issue that caused restore failures in C++/CLI projects with `project.json`.</span></span>
* <span data-ttu-id="1de75-116">Mono에서 nuget을 사용할 때 제대로 압축 해제 되지 않는 일부 패키지 (예: ModernHttpClient)입니다.</span><span class="sxs-lookup"><span data-stu-id="1de75-116">Some packages (E.g ModernHttpClient) where not being unzipped correctly when you use nuget in mono.</span></span> <span data-ttu-id="1de75-117">이제이 릴리스에서 수정 되었습니다.</span><span class="sxs-lookup"><span data-stu-id="1de75-117">This has now been fixed in this release.</span></span>

<span data-ttu-id="1de75-118">이 릴리스의 수정 사항 및 개선 사항에 대 한 전체 목록은 [여기](https://github.com/NuGet/Home/issues?q=is%3Aissue+milestone%3A3.4.3+is%3Aclosed)에서 문제 목록을 확인 하세요.</span><span class="sxs-lookup"><span data-stu-id="1de75-118">For the complete list of fixes and improvements in this release, check out the list of issues [here](https://github.com/NuGet/Home/issues?q=is%3Aissue+milestone%3A3.4.3+is%3Aclosed).</span></span>