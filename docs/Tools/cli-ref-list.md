---
title: "NuGet CLI 목록 표시 명령 | Microsoft Docs"
author: kraigb
ms.author: kraigb
manager: ghogen
ms.date: 10/24/2017
ms.topic: reference
ms.prod: nuget
ms.technology: 
ms.assetid: 728c8452-0457-4bb8-bfdc-de77fe1570bd
description: "Nuget.exe 목록 명령에 대 한 참조"
keywords: "nuget 목록 참조 패키지 목록 표시 명령"
ms.reviewer:
- karann-msft
- unniravindranathan
ms.openlocfilehash: 62a7077e7adac1e4d8cf305fd6e66a6ce5ebfb76
ms.sourcegitcommit: d0ba99bfe019b779b75731bafdca8a37e35ef0d9
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 12/14/2017
---
# <a name="list-command-nuget-cli"></a><span data-ttu-id="1c365-104">목록 표시 명령 (NuGet CLI)</span><span class="sxs-lookup"><span data-stu-id="1c365-104">list command (NuGet CLI)</span></span>

<span data-ttu-id="1c365-105">**적용 대상:** 패키지 소비, 게시 &bullet; **지원 되는 버전:** 모든</span><span class="sxs-lookup"><span data-stu-id="1c365-105">**Applies to:** package consumption, publishing &bullet; **Supported versions:** all</span></span>

<span data-ttu-id="1c365-106">지정된 된 원본에서 패키지의 목록이 표시 됩니다.</span><span class="sxs-lookup"><span data-stu-id="1c365-106">Displays a list of packages from a given source.</span></span> <span data-ttu-id="1c365-107">모든 소스에서 글로벌 구성 파일에 정의 된 원본이 지정 된 경우 `%AppData%\NuGet\NuGet.Config`, 사용 됩니다.</span><span class="sxs-lookup"><span data-stu-id="1c365-107">If no sources are specified, all sources defined in the global configuration file, `%AppData%\NuGet\NuGet.Config`, are used.</span></span> <span data-ttu-id="1c365-108">경우 `NuGet.Config` 다음 원본이 없습니다 지정 `list` 기본 피드 (nuget.org)를 사용 하 여 합니다.</span><span class="sxs-lookup"><span data-stu-id="1c365-108">If `NuGet.Config` specifies no sources, then `list` uses the default feed (nuget.org).</span></span>

## <a name="usage"></a><span data-ttu-id="1c365-109">용도</span><span class="sxs-lookup"><span data-stu-id="1c365-109">Usage</span></span>

```
nuget list [search terms] [options]
```

<span data-ttu-id="1c365-110">여기서 선택적 검색 단어에 표시 된 목록을 필터링 합니다.</span><span class="sxs-lookup"><span data-stu-id="1c365-110">where the optional search terms will filter the displayed list.</span></span> <span data-ttu-id="1c365-111">검색어는 패키지, 태그 및 패키지 설명의 이름에 적용 됩니다.</span><span class="sxs-lookup"><span data-stu-id="1c365-111">Search terms are applied to the names of packages, tags, and package descriptions.</span></span>

## <a name="options"></a><span data-ttu-id="1c365-112">옵션</span><span class="sxs-lookup"><span data-stu-id="1c365-112">Options</span></span>
| <span data-ttu-id="1c365-113">옵션</span><span class="sxs-lookup"><span data-stu-id="1c365-113">Option</span></span> | <span data-ttu-id="1c365-114">설명</span><span class="sxs-lookup"><span data-stu-id="1c365-114">Description</span></span> |
| --- | --- |
| <span data-ttu-id="1c365-115">AllVersions</span><span class="sxs-lookup"><span data-stu-id="1c365-115">AllVersions</span></span> | <span data-ttu-id="1c365-116">패키지의 모든 버전을 나열 합니다.</span><span class="sxs-lookup"><span data-stu-id="1c365-116">List all versions of a package.</span></span> <span data-ttu-id="1c365-117">기본적으로는 최신 패키지 버전에만 표시 됩니다.</span><span class="sxs-lookup"><span data-stu-id="1c365-117">By default, only the latest package version is displayed.</span></span> |
| <span data-ttu-id="1c365-118">ConfigFile</span><span class="sxs-lookup"><span data-stu-id="1c365-118">ConfigFile</span></span> | <span data-ttu-id="1c365-119">*(2.5 +)*  NuGet 구성 파일을 적용 합니다.</span><span class="sxs-lookup"><span data-stu-id="1c365-119">*(2.5+)* The NuGet configuration file to apply.</span></span> <span data-ttu-id="1c365-120">지정 하지 않으면 *%AppData%\NuGet\NuGet.Config* 사용 됩니다.</span><span class="sxs-lookup"><span data-stu-id="1c365-120">If not specified, *%AppData%\NuGet\NuGet.Config* is used.</span></span> |
| <span data-ttu-id="1c365-121">ForceEnglishOutput</span><span class="sxs-lookup"><span data-stu-id="1c365-121">ForceEnglishOutput</span></span> | <span data-ttu-id="1c365-122">*(3.5 +)*  고정, 영어 기반 문화권을 사용 하 여 실행할 nuget.exe를 강제로 수행 합니다.</span><span class="sxs-lookup"><span data-stu-id="1c365-122">*(3.5+)* Forces nuget.exe to run using an invariant, English-based culture.</span></span> |
| <span data-ttu-id="1c365-123">도움말</span><span class="sxs-lookup"><span data-stu-id="1c365-123">Help</span></span> | <span data-ttu-id="1c365-124">도움말의 명령에 대 한 정보를 표시 합니다.</span><span class="sxs-lookup"><span data-stu-id="1c365-124">Displays help information for the command.</span></span> |
| <span data-ttu-id="1c365-125">IncludeDelisted</span><span class="sxs-lookup"><span data-stu-id="1c365-125">IncludeDelisted</span></span> | <span data-ttu-id="1c365-126">*(3.2 +)*  목록에 없는 패키지를 표시 합니다.</span><span class="sxs-lookup"><span data-stu-id="1c365-126">*(3.2+)* Display unlisted packages.</span></span> |
| <span data-ttu-id="1c365-127">비 대화형</span><span class="sxs-lookup"><span data-stu-id="1c365-127">NonInteractive</span></span> | <span data-ttu-id="1c365-128">사용자 입력 또는 확인에 대 한 프롬프트를 표시 하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="1c365-128">Suppresses prompts for user input or confirmations.</span></span> |
| <span data-ttu-id="1c365-129">시험판</span><span class="sxs-lookup"><span data-stu-id="1c365-129">PreRelease</span></span> | <span data-ttu-id="1c365-130">목록에 시험판 패키지를 포함합니다.</span><span class="sxs-lookup"><span data-stu-id="1c365-130">Includes prerelease packages in the list.</span></span> |
| <span data-ttu-id="1c365-131">소스</span><span class="sxs-lookup"><span data-stu-id="1c365-131">Source</span></span> | <span data-ttu-id="1c365-132">검색할 패키지 소스 목록을 지정 합니다.</span><span class="sxs-lookup"><span data-stu-id="1c365-132">Specifies a list of packages sources to search.</span></span> |
| <span data-ttu-id="1c365-133">자세한 정도</span><span class="sxs-lookup"><span data-stu-id="1c365-133">Verbosity</span></span> | <span data-ttu-id="1c365-134">출력에 표시 되는 세부 정보 수준을 지정: *일반*, *quiet*, *세부 (2.5 이상)*합니다.</span><span class="sxs-lookup"><span data-stu-id="1c365-134">Specifies the amount of detail displayed in the output: *normal*, *quiet*, *detailed (2.5+)*.</span></span> |

<span data-ttu-id="1c365-135">또한 참조 [환경 변수](cli-ref-environment-variables.md)</span><span class="sxs-lookup"><span data-stu-id="1c365-135">Also see [Environment variables](cli-ref-environment-variables.md)</span></span>

## <a name="examples"></a><span data-ttu-id="1c365-136">예제</span><span class="sxs-lookup"><span data-stu-id="1c365-136">Examples</span></span>

```
nuget list

nuget list -Verbosity detailed -AllVersions
```
