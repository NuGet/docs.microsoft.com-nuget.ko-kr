---
title: NuGet 3.4.4 릴리스 정보
description: NuGet 3.4.4 포함에 대 한 릴리스 정보는 문제, 버그 수정, 추가 된 기능 및 Dcr 알려져 있습니다.
author: karann-msft
ms.author: karann
manager: unnir
ms.date: 11/11/2016
ms.topic: conceptual
ms.openlocfilehash: 891d5c7ee884d31f405118739b57a169b9cd93b3
ms.sourcegitcommit: 3eab9c4dd41ea7ccd2c28bb5ab16f6fbbec13708
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/26/2018
ms.locfileid: "31820869"
---
# <a name="nuget-344-release-notes"></a><span data-ttu-id="8b9de-103">NuGet 3.4.4 릴리스 정보</span><span class="sxs-lookup"><span data-stu-id="8b9de-103">NuGet 3.4.4 Release Notes</span></span>

<span data-ttu-id="8b9de-104">[NuGet 3.4.3 릴리스 정보](../release-notes/nuget-3.4.3.md) | [NuGet 3.5 베타 릴리스 정보](../release-notes/nuget-3.5-Beta.md)</span><span class="sxs-lookup"><span data-stu-id="8b9de-104">[NuGet 3.4.3 Release Notes](../release-notes/nuget-3.4.3.md) | [NuGet 3.5-Beta Release Notes](../release-notes/nuget-3.5-Beta.md)</span></span>

<span data-ttu-id="8b9de-105">이 버전의 주된 초점은 3.4.3의 품질을 향상 된 버전도 Visual Studio 확장에 몇 가지 수정 프로그램으로 nuget.exe의 합니다.</span><span class="sxs-lookup"><span data-stu-id="8b9de-105">The primary focus of this release was improvements to the quality of 3.4.3 version of nuget.exe with a few fixes to the Visual Studio extension as well.</span></span>

<span data-ttu-id="8b9de-106">VSIX와 nuget.exe를 다운로드할 수 있습니다 [여기](https://dist.nuget.org/index.html)합니다.</span><span class="sxs-lookup"><span data-stu-id="8b9de-106">You can download both the VSIX and nuget.exe [here](https://dist.nuget.org/index.html).</span></span>

## <a name="344-rtmhttpsgithubcomnugetnugetclienttree344-rtm-2016-05-19"></a><span data-ttu-id="8b9de-107">[3.4.4-rtm](https://github.com/NuGet/NuGet.Client/tree/3.4.4-rtm) (2016-05-19)</span><span class="sxs-lookup"><span data-stu-id="8b9de-107">[3.4.4-rtm](https://github.com/NuGet/NuGet.Client/tree/3.4.4-rtm) (2016-05-19)</span></span>

[<span data-ttu-id="8b9de-108">전체 변경 로그</span><span class="sxs-lookup"><span data-stu-id="8b9de-108">Full Changelog</span></span>](https://github.com/NuGet/NuGet.Client/compare/3.5.0-beta-final...3.4.4-rtm)

[<span data-ttu-id="8b9de-109">문제의 목록</span><span class="sxs-lookup"><span data-stu-id="8b9de-109">List of Issues</span></span>](https://github.com/NuGet/Home/issues?q=is%3Aissue+milestone%3A3.4.4+is%3Aclosed)

### <a name="changes"></a><span data-ttu-id="8b9de-110">변경 내용</span><span class="sxs-lookup"><span data-stu-id="8b9de-110">Changes</span></span>

- <span data-ttu-id="8b9de-111">팩 개선 기능: 향상 된 기호를 압축으로 압축 `project.json` 많은 [ \#606](https://github.com/NuGet/NuGet.Client/pull/606)</span><span class="sxs-lookup"><span data-stu-id="8b9de-111">Pack Improvements: Improvements to packing symbols, packing with `project.json` and more [\#606](https://github.com/NuGet/NuGet.Client/pull/606)</span></span>
- <span data-ttu-id="8b9de-112">업데이트 명령에서 프로젝트를 찾는 오류가 있을 경우 예외를 표시 합니다. [\#605] (https://github.com/NuGet/NuGet.Client/pull/605</span><span class="sxs-lookup"><span data-stu-id="8b9de-112">Display exception when there is a failure finding projects in update command [\#605](https://github.com/NuGet/NuGet.Client/pull/605</span></span>
- <span data-ttu-id="8b9de-113">입력에서 패키지 유형 읽기 `.nuspec` 및 `project.json` 압축 때 [ \#603](https://github.com/NuGet/NuGet.Client/pull/603)</span><span class="sxs-lookup"><span data-stu-id="8b9de-113">Read package type from input `.nuspec` and `project.json` when packing [\#603](https://github.com/NuGet/NuGet.Client/pull/603)</span></span>
- <span data-ttu-id="8b9de-114">프로젝트가 아니라 NuGet.Shared를 확인 합니다.</span><span class="sxs-lookup"><span data-stu-id="8b9de-114">Make NuGet.Shared not a project.</span></span> [<span data-ttu-id="8b9de-115">\#602</span><span class="sxs-lookup"><span data-stu-id="8b9de-115">\#602</span></span>](https://github.com/NuGet/NuGet.Client/pull/602)
- <span data-ttu-id="8b9de-116">HTTP 응답 시간 초과로 밀어넣기 제한 시간을 사용 하 여 [ \#599](https://github.com/NuGet/NuGet.Client/pull/599)</span><span class="sxs-lookup"><span data-stu-id="8b9de-116">Use the push timeout as the HTTP response timeout [\#599](https://github.com/NuGet/NuGet.Client/pull/599)</span></span>
- <span data-ttu-id="8b9de-117">이후 시간을 사용 하 여 패키지 파일에는 사용 되는 시간에 따라 각각 [ \#597](https://github.com/NuGet/NuGet.Client/pull/597)</span><span class="sxs-lookup"><span data-stu-id="8b9de-117">Package files with future times will not have their times used [\#597](https://github.com/NuGet/NuGet.Client/pull/597)</span></span>
- <span data-ttu-id="8b9de-118">업데이트 `NuGet.Core.dll` 버전 XML 문제를 해결 하려면 2.12.0 [ \#594](https://github.com/NuGet/NuGet.Client/pull/594)</span><span class="sxs-lookup"><span data-stu-id="8b9de-118">Updating `NuGet.Core.dll` version to 2.12.0 to fix XML issue [\#594](https://github.com/NuGet/NuGet.Client/pull/594)</span></span>
- <span data-ttu-id="8b9de-119">./NuGet.CommandLine.XPlat v 지원 \<자세한 정도\> \<모드\> [ \#593](https://github.com/NuGet/NuGet.Client/pull/593)</span><span class="sxs-lookup"><span data-stu-id="8b9de-119">Support ./NuGet.CommandLine.XPlat -v \<verbosity\> \<mode\> [\#593](https://github.com/NuGet/NuGet.Client/pull/593)</span></span>
- <span data-ttu-id="8b9de-120">오류를 표시 하지 않고 복원 `project.json` 또는 `packages.config` [ \#590](https://github.com/NuGet/NuGet.Client/pull/590)</span><span class="sxs-lookup"><span data-stu-id="8b9de-120">Display error restoring without `project.json` or `packages.config` [\#590](https://github.com/NuGet/NuGet.Client/pull/590)</span></span>
- <span data-ttu-id="8b9de-121">필요한 버전이 다른 경우 종속성 버전을 수정 [ \#559](https://github.com/NuGet/NuGet.Client/pull/559)</span><span class="sxs-lookup"><span data-stu-id="8b9de-121">Fixing dependency versions when required versions differ [\#559](https://github.com/NuGet/NuGet.Client/pull/559)</span></span>