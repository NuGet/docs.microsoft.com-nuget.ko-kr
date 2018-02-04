---
title: "NuGet 3.4.4 릴리스 정보 | Microsoft Docs"
author: karann-msft
ms.author: karann-msft
manager: ghogen
ms.date: 11/11/2016
ms.topic: article
ms.prod: nuget
ms.technology: 
description: "NuGet 3.4.4 포함에 대 한 릴리스 정보는 문제, 버그 수정, 추가 된 기능 및 Dcr 알려져 있습니다."
keywords: "NuGet 3.4.4 릴리스 정보, 버그 수정, 알려진 문제, 추가 기능을 Dcr"
ms.reviewer:
- karann-msft
- unniravindranathan
ms.openlocfilehash: fabc10ae5c8e0bd43581f85c7763eb23e9483aaf
ms.sourcegitcommit: 4651b16a3a08f6711669fc4577f5d63b600f8f58
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 02/02/2018
---
# <a name="nuget-344-release-notes"></a><span data-ttu-id="34774-104">NuGet 3.4.4 릴리스 정보</span><span class="sxs-lookup"><span data-stu-id="34774-104">NuGet 3.4.4 Release Notes</span></span>

<span data-ttu-id="34774-105">[NuGet 3.4.3 릴리스 정보](../release-notes/nuget-3.4.3.md) | [NuGet 3.5 베타 릴리스 정보](../release-notes/nuget-3.5-Beta.md)</span><span class="sxs-lookup"><span data-stu-id="34774-105">[NuGet 3.4.3 Release Notes](../release-notes/nuget-3.4.3.md) | [NuGet 3.5-Beta Release Notes](../release-notes/nuget-3.5-Beta.md)</span></span>

<span data-ttu-id="34774-106">이 버전의 주된 초점은 3.4.3의 품질을 향상 된 버전도 Visual Studio 확장에 몇 가지 수정 프로그램으로 nuget.exe의 합니다.</span><span class="sxs-lookup"><span data-stu-id="34774-106">The primary focus of this release was improvements to the quality of 3.4.3 version of nuget.exe with a few fixes to the Visual Studio extension as well.</span></span>

<span data-ttu-id="34774-107">VSIX와 nuget.exe를 다운로드할 수 있습니다 [여기](https://dist.nuget.org/index.html)합니다.</span><span class="sxs-lookup"><span data-stu-id="34774-107">You can download both the VSIX and nuget.exe [here](https://dist.nuget.org/index.html).</span></span>

## <a name="344-rtmhttpsgithubcomnugetnugetclienttree344-rtm-2016-05-19"></a><span data-ttu-id="34774-108">[3.4.4-rtm](https://github.com/NuGet/NuGet.Client/tree/3.4.4-rtm) (2016-05-19)</span><span class="sxs-lookup"><span data-stu-id="34774-108">[3.4.4-rtm](https://github.com/NuGet/NuGet.Client/tree/3.4.4-rtm) (2016-05-19)</span></span>

[<span data-ttu-id="34774-109">전체 변경 로그</span><span class="sxs-lookup"><span data-stu-id="34774-109">Full Changelog</span></span>](https://github.com/NuGet/NuGet.Client/compare/3.5.0-beta-final...3.4.4-rtm)

[<span data-ttu-id="34774-110">문제의 목록</span><span class="sxs-lookup"><span data-stu-id="34774-110">List of Issues</span></span>](https://github.com/NuGet/Home/issues?q=is%3Aissue+milestone%3A3.4.4+is%3Aclosed)

### <a name="changes"></a><span data-ttu-id="34774-111">변경 내용</span><span class="sxs-lookup"><span data-stu-id="34774-111">Changes</span></span>

- <span data-ttu-id="34774-112">팩 개선 기능: 향상 된 기호를 압축으로 압축 `project.json` 많은 [ \#606](https://github.com/NuGet/NuGet.Client/pull/606)</span><span class="sxs-lookup"><span data-stu-id="34774-112">Pack Improvements: Improvements to packing symbols, packing with `project.json` and more [\#606](https://github.com/NuGet/NuGet.Client/pull/606)</span></span>
- <span data-ttu-id="34774-113">업데이트 명령에서 프로젝트를 찾는 오류가 있을 경우 예외를 표시 합니다. [\#605] (https://github.com/NuGet/NuGet.Client/pull/605</span><span class="sxs-lookup"><span data-stu-id="34774-113">Display exception when there is a failure finding projects in update command [\#605](https://github.com/NuGet/NuGet.Client/pull/605</span></span>
- <span data-ttu-id="34774-114">입력에서 패키지 유형 읽기 `.nuspec` 및 `project.json` 압축 때 [ \#603](https://github.com/NuGet/NuGet.Client/pull/603)</span><span class="sxs-lookup"><span data-stu-id="34774-114">Read package type from input `.nuspec` and `project.json` when packing [\#603](https://github.com/NuGet/NuGet.Client/pull/603)</span></span>
- <span data-ttu-id="34774-115">프로젝트가 아니라 NuGet.Shared를 확인 합니다.</span><span class="sxs-lookup"><span data-stu-id="34774-115">Make NuGet.Shared not a project.</span></span> [<span data-ttu-id="34774-116">\#602</span><span class="sxs-lookup"><span data-stu-id="34774-116">\#602</span></span>](https://github.com/NuGet/NuGet.Client/pull/602)
- <span data-ttu-id="34774-117">HTTP 응답 시간 초과로 밀어넣기 제한 시간을 사용 하 여 [ \#599](https://github.com/NuGet/NuGet.Client/pull/599)</span><span class="sxs-lookup"><span data-stu-id="34774-117">Use the push timeout as the HTTP response timeout [\#599](https://github.com/NuGet/NuGet.Client/pull/599)</span></span>
- <span data-ttu-id="34774-118">이후 시간을 사용 하 여 패키지 파일에는 사용 되는 시간에 따라 각각 [ \#597](https://github.com/NuGet/NuGet.Client/pull/597)</span><span class="sxs-lookup"><span data-stu-id="34774-118">Package files with future times will not have their times used [\#597](https://github.com/NuGet/NuGet.Client/pull/597)</span></span>
- <span data-ttu-id="34774-119">업데이트 `NuGet.Core.dll` 버전 XML 문제를 해결 하려면 2.12.0 [ \#594](https://github.com/NuGet/NuGet.Client/pull/594)</span><span class="sxs-lookup"><span data-stu-id="34774-119">Updating `NuGet.Core.dll` version to 2.12.0 to fix XML issue [\#594](https://github.com/NuGet/NuGet.Client/pull/594)</span></span>
- <span data-ttu-id="34774-120">Support ./NuGet.CommandLine.XPlat -v \<verbosity\> \<mode\> [\#593](https://github.com/NuGet/NuGet.Client/pull/593)</span><span class="sxs-lookup"><span data-stu-id="34774-120">Support ./NuGet.CommandLine.XPlat -v \<verbosity\> \<mode\> [\#593](https://github.com/NuGet/NuGet.Client/pull/593)</span></span>
- <span data-ttu-id="34774-121">오류를 표시 하지 않고 복원 `project.json` 또는 `packages.config` [ \#590](https://github.com/NuGet/NuGet.Client/pull/590)</span><span class="sxs-lookup"><span data-stu-id="34774-121">Display error restoring without `project.json` or `packages.config` [\#590](https://github.com/NuGet/NuGet.Client/pull/590)</span></span>
- <span data-ttu-id="34774-122">필요한 버전이 다른 경우 종속성 버전을 수정 [ \#559](https://github.com/NuGet/NuGet.Client/pull/559)</span><span class="sxs-lookup"><span data-stu-id="34774-122">Fixing dependency versions when required versions differ [\#559](https://github.com/NuGet/NuGet.Client/pull/559)</span></span>