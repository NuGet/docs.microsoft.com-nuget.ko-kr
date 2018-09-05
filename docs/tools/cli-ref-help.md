---
title: NuGet CLI help 명령
description: Nuget.exe help 명령에 대 한 참조
author: karann-msft
ms.author: karann
ms.date: 01/18/2018
ms.topic: reference
ms.openlocfilehash: 3c8b07cb02144da3d88e06956d079b216b3f530f
ms.sourcegitcommit: 1d1406764c6af5fb7801d462e0c4afc9092fa569
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 09/04/2018
ms.locfileid: "43546565"
---
# <a name="help-or--command-nuget-cli"></a><span data-ttu-id="dd745-103">help or ?</span><span class="sxs-lookup"><span data-stu-id="dd745-103">help or ?</span></span> <span data-ttu-id="dd745-104">명령(NuGet CLI)</span><span class="sxs-lookup"><span data-stu-id="dd745-104">command (NuGet CLI)</span></span>

<span data-ttu-id="dd745-105">**적용 대상:** 모든 &bullet; **지원 되는 버전**: 모두</span><span class="sxs-lookup"><span data-stu-id="dd745-105">**Applies to:** all &bullet; **Supported versions**: all</span></span>

<span data-ttu-id="dd745-106">일반 표시 도움말 정보 및 특정 명령에 대 한 정보입니다.</span><span class="sxs-lookup"><span data-stu-id="dd745-106">Displays general help information and help information about specific commands.</span></span>

## <a name="usage"></a><span data-ttu-id="dd745-107">사용법</span><span class="sxs-lookup"><span data-stu-id="dd745-107">Usage</span></span>

```cli
nuget help [command] [options]
nuget ? [command] [options]
```

<span data-ttu-id="dd745-108">여기서 [command] 도움말을 표시 하려는 특정 명령을 식별 합니다.</span><span class="sxs-lookup"><span data-stu-id="dd745-108">where [command] identifies a specific command for which to display help.</span></span>

> [!Warning]
> <span data-ttu-id="dd745-109">일부 명령을 사용 하 여 되도록 주의 해야 *도움말* 먼저를 사용 하 여 `nuget help install`nuget.org에서 "도움말" 라는 패키지 중이기 때문입니다. 명령을 제공 하는 경우 `nuget install help`, 설치 명령에서 도움을 받으려면지 않습니다 하지만 대신 도움말 라는 패키지를 설치 합니다.</span><span class="sxs-lookup"><span data-stu-id="dd745-109">With some commands, be mindful to specify *help* first, as with `nuget help install`, because there is a package named "help" on nuget.org. If you give the command `nuget install help`, you won't get help on the install command but will instead install the package named help.</span></span>

## <a name="options"></a><span data-ttu-id="dd745-110">옵션</span><span class="sxs-lookup"><span data-stu-id="dd745-110">Options</span></span>

| <span data-ttu-id="dd745-111">옵션</span><span class="sxs-lookup"><span data-stu-id="dd745-111">Option</span></span> | <span data-ttu-id="dd745-112">설명</span><span class="sxs-lookup"><span data-stu-id="dd745-112">Description</span></span> |
| --- | --- |
| <span data-ttu-id="dd745-113">모두</span><span class="sxs-lookup"><span data-stu-id="dd745-113">All</span></span> | <span data-ttu-id="dd745-114">사용 가능한 명령 모두;에 대 한 자세한 도움말을 인쇄 특정 명령을 지정 하는 경우 무시 됩니다.</span><span class="sxs-lookup"><span data-stu-id="dd745-114">Print detailed help for all available commands; ignored if a specific command is given.</span></span> |
| <span data-ttu-id="dd745-115">ConfigFile</span><span class="sxs-lookup"><span data-stu-id="dd745-115">ConfigFile</span></span> | <span data-ttu-id="dd745-116">NuGet 구성 파일을 적용 합니다.</span><span class="sxs-lookup"><span data-stu-id="dd745-116">The NuGet configuration file to apply.</span></span> <span data-ttu-id="dd745-117">지정 하지 않으면 `%AppData%\NuGet\NuGet.Config` (Windows) 또는 `~/.nuget/NuGet/NuGet.Config` (Mac/Linux)가 사용 됩니다.</span><span class="sxs-lookup"><span data-stu-id="dd745-117">If not specified, `%AppData%\NuGet\NuGet.Config` (Windows) or `~/.nuget/NuGet/NuGet.Config` (Mac/Linux) is used.</span></span>|
| <span data-ttu-id="dd745-118">ForceEnglishOutput</span><span class="sxs-lookup"><span data-stu-id="dd745-118">ForceEnglishOutput</span></span> | <span data-ttu-id="dd745-119">*(3.5 이상)*  고정 영어 기반 문화권을 사용 하 여 실행할 nuget.exe를 강제로 수행 합니다.</span><span class="sxs-lookup"><span data-stu-id="dd745-119">*(3.5+)* Forces nuget.exe to run using an invariant, English-based culture.</span></span> |
| <span data-ttu-id="dd745-120">도움말</span><span class="sxs-lookup"><span data-stu-id="dd745-120">Help</span></span> | <span data-ttu-id="dd745-121">도움말 도움말 명령 자체에 대 한 정보를 표시 합니다.</span><span class="sxs-lookup"><span data-stu-id="dd745-121">Displays help information for the help command itself.</span></span> |
| <span data-ttu-id="dd745-122">Markdown</span><span class="sxs-lookup"><span data-stu-id="dd745-122">Markdown</span></span> | <span data-ttu-id="dd745-123">마크 다운 형식으로 사용 하는 경우 자세한 도움말을 인쇄 `-All`합니다.</span><span class="sxs-lookup"><span data-stu-id="dd745-123">Print detailed help in markdown format when used with `-All`.</span></span> <span data-ttu-id="dd745-124">그렇지 않으면 무시 됩니다.</span><span class="sxs-lookup"><span data-stu-id="dd745-124">Ignored otherwise.</span></span> |
| <span data-ttu-id="dd745-125">NonInteractive</span><span class="sxs-lookup"><span data-stu-id="dd745-125">NonInteractive</span></span> | <span data-ttu-id="dd745-126">사용자 입력 또는 확인에 대 한 프롬프트를 표시 하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="dd745-126">Suppresses prompts for user input or confirmations.</span></span> |
| <span data-ttu-id="dd745-127">자세한 정도</span><span class="sxs-lookup"><span data-stu-id="dd745-127">Verbosity</span></span> | <span data-ttu-id="dd745-128">출력에 표시 되는 세부 정보의 양을 지정: *정상적인*, *quiet*, *자세한*합니다.</span><span class="sxs-lookup"><span data-stu-id="dd745-128">Specifies the amount of detail displayed in the output: *normal*, *quiet*, *detailed*.</span></span> |

<span data-ttu-id="dd745-129">또한 참조 [환경 변수](cli-ref-environment-variables.md)</span><span class="sxs-lookup"><span data-stu-id="dd745-129">Also see [Environment variables](cli-ref-environment-variables.md)</span></span>

## <a name="examples"></a><span data-ttu-id="dd745-130">예제</span><span class="sxs-lookup"><span data-stu-id="dd745-130">Examples</span></span>

```cli
nuget help
nuget help push
nuget ?
nuget push -?
nuget help -All -Markdown
```
