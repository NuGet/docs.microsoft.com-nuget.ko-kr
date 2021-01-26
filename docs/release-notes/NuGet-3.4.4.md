---
title: NuGet 3.4.4 릴리스 정보
description: 알려진 문제, 버그 수정, 추가 된 기능 및 3.4.4를 포함 하는 NuGet에 대 한 릴리스 정보입니다.
author: JonDouglas
ms.author: jodou
ms.date: 11/11/2016
ms.topic: conceptual
ms.openlocfilehash: 4e5e635432147afba4809562035bc8c762d31af4
ms.sourcegitcommit: ee6c3f203648a5561c809db54ebeb1d0f0598b68
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 01/26/2021
ms.locfileid: "98780221"
---
# <a name="nuget-344-release-notes"></a><span data-ttu-id="f9f15-103">NuGet 3.4.4 릴리스 정보</span><span class="sxs-lookup"><span data-stu-id="f9f15-103">NuGet 3.4.4 Release Notes</span></span>

<span data-ttu-id="f9f15-104">[NuGet 3.4.3 릴리스 정보](../release-notes/nuget-3.4.3.md)  |  [NuGet 3.5-베타 릴리스 정보](../release-notes/nuget-3.5-Beta.md)</span><span class="sxs-lookup"><span data-stu-id="f9f15-104">[NuGet 3.4.3 Release Notes](../release-notes/nuget-3.4.3.md) | [NuGet 3.5-Beta Release Notes](../release-notes/nuget-3.5-Beta.md)</span></span>

<span data-ttu-id="f9f15-105">이 릴리스의 주요 초점은 Visual Studio 확장에 대 한 몇 가지 수정 사항이 포함 된 nuget.exe 3.4.3 버전의 품질 향상 이었습니다.</span><span class="sxs-lookup"><span data-stu-id="f9f15-105">The primary focus of this release was improvements to the quality of 3.4.3 version of nuget.exe with a few fixes to the Visual Studio extension as well.</span></span>

<span data-ttu-id="f9f15-106">VSIX를 다운로드 하 고 [여기](https://dist.nuget.org/index.html)에서 nuget.exe 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="f9f15-106">You can download both the VSIX and nuget.exe [here](https://dist.nuget.org/index.html).</span></span>

## <a name="344-rtm-2016-05-19"></a><span data-ttu-id="f9f15-107">[3.4.4-rtm](https://github.com/NuGet/NuGet.Client/tree/3.4.4-rtm) (2016-05-19)</span><span class="sxs-lookup"><span data-stu-id="f9f15-107">[3.4.4-rtm](https://github.com/NuGet/NuGet.Client/tree/3.4.4-rtm) (2016-05-19)</span></span>

[<span data-ttu-id="f9f15-108">전체 변경 로그</span><span class="sxs-lookup"><span data-stu-id="f9f15-108">Full Changelog</span></span>](https://github.com/NuGet/NuGet.Client/compare/3.5.0-beta-final...3.4.4-rtm)

[<span data-ttu-id="f9f15-109">문제 목록</span><span class="sxs-lookup"><span data-stu-id="f9f15-109">List of Issues</span></span>](https://github.com/NuGet/Home/issues?q=is%3Aissue+milestone%3A3.4.4+is%3Aclosed)

### <a name="changes"></a><span data-ttu-id="f9f15-110">변경</span><span class="sxs-lookup"><span data-stu-id="f9f15-110">Changes</span></span>

- <span data-ttu-id="f9f15-111">팩의 향상 된 기능: 기호를 압축 하 `project.json` 고, 및 [ \# 606](https://github.com/NuGet/NuGet.Client/pull/606) 를 사용 하 여 압축</span><span class="sxs-lookup"><span data-stu-id="f9f15-111">Pack Improvements: Improvements to packing symbols, packing with `project.json` and more [\#606](https://github.com/NuGet/NuGet.Client/pull/606)</span></span>
- <span data-ttu-id="f9f15-112">업데이트 명령 [605]에서 프로젝트를 찾을 수 없는 경우 예외를 표시 합니다. \#https://github.com/NuGet/NuGet.Client/pull/605</span><span class="sxs-lookup"><span data-stu-id="f9f15-112">Display exception when there is a failure finding projects in update command [\#605](https://github.com/NuGet/NuGet.Client/pull/605</span></span>
- <span data-ttu-id="f9f15-113">입력에서 패키지 유형을 읽고 `.nuspec` , `project.json` [ \# 603](https://github.com/NuGet/NuGet.Client/pull/603) 를 압축 하는 경우</span><span class="sxs-lookup"><span data-stu-id="f9f15-113">Read package type from input `.nuspec` and `project.json` when packing [\#603](https://github.com/NuGet/NuGet.Client/pull/603)</span></span>
- <span data-ttu-id="f9f15-114">NuGet을 만듭니다. 프로젝트는 공유 되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="f9f15-114">Make NuGet.Shared not a project.</span></span> [<span data-ttu-id="f9f15-115">\#602</span><span class="sxs-lookup"><span data-stu-id="f9f15-115">\#602</span></span>](https://github.com/NuGet/NuGet.Client/pull/602)
- <span data-ttu-id="f9f15-116">HTTP 응답 시간 제한 [ \# 599](https://github.com/NuGet/NuGet.Client/pull/599) 로 푸시 제한 시간을 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="f9f15-116">Use the push timeout as the HTTP response timeout [\#599](https://github.com/NuGet/NuGet.Client/pull/599)</span></span>
- <span data-ttu-id="f9f15-117">이후 시간에 패키지 파일의 시간이 사용 되지 않습니다. [ \# 597](https://github.com/NuGet/NuGet.Client/pull/597)</span><span class="sxs-lookup"><span data-stu-id="f9f15-117">Package files with future times will not have their times used [\#597](https://github.com/NuGet/NuGet.Client/pull/597)</span></span>
- <span data-ttu-id="f9f15-118">`NuGet.Core.dll`XML 문제 [ \# 594](https://github.com/NuGet/NuGet.Client/pull/594) 을 해결 하기 위해 버전을 2.12.0로 업데이트 하는 중</span><span class="sxs-lookup"><span data-stu-id="f9f15-118">Updating `NuGet.Core.dll` version to 2.12.0 to fix XML issue [\#594](https://github.com/NuGet/NuGet.Client/pull/594)</span></span>
- <span data-ttu-id="f9f15-119">/NuGet.CommandLine.XPlat-v \<verbosity\> \<mode\> [ \# 593](https://github.com/NuGet/NuGet.Client/pull/593)</span><span class="sxs-lookup"><span data-stu-id="f9f15-119">Support ./NuGet.CommandLine.XPlat -v \<verbosity\> \<mode\> [\#593](https://github.com/NuGet/NuGet.Client/pull/593)</span></span>
- <span data-ttu-id="f9f15-120">`project.json`또는 `packages.config` [ \# 590](https://github.com/NuGet/NuGet.Client/pull/590) 를 사용 하지 않고 오류 복원 표시</span><span class="sxs-lookup"><span data-stu-id="f9f15-120">Display error restoring without `project.json` or `packages.config` [\#590](https://github.com/NuGet/NuGet.Client/pull/590)</span></span>
- <span data-ttu-id="f9f15-121">필요한 버전이 다른 경우 종속성 버전 수정 [ \# 559](https://github.com/NuGet/NuGet.Client/pull/559)</span><span class="sxs-lookup"><span data-stu-id="f9f15-121">Fixing dependency versions when required versions differ [\#559](https://github.com/NuGet/NuGet.Client/pull/559)</span></span>