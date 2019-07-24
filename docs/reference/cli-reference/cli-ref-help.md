---
title: NuGet CLI 도움말 명령
description: Nuget.exe 도움말 명령에 대 한 참조입니다.
author: karann-msft
ms.author: karann
ms.date: 01/18/2018
ms.topic: reference
ms.openlocfilehash: 3c8b07cb02144da3d88e06956d079b216b3f530f
ms.sourcegitcommit: efc18d484fdf0c7a8979b564dcb191c030601bb4
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/18/2019
ms.locfileid: "68327800"
---
# <a name="help-or--command-nuget-cli"></a><span data-ttu-id="17253-103">help or ?</span><span class="sxs-lookup"><span data-stu-id="17253-103">help or ?</span></span> <span data-ttu-id="17253-104">명령(NuGet CLI)</span><span class="sxs-lookup"><span data-stu-id="17253-104">command (NuGet CLI)</span></span>

<span data-ttu-id="17253-105">\*\*\*\*모든 버전에서 모두 지원됩니다.\*\*</span><span class="sxs-lookup"><span data-stu-id="17253-105">**Applies to:** all &bullet; **Supported versions**: all</span></span>

<span data-ttu-id="17253-106">일반 도움말 정보 및 특정 명령에 대 한 도움말 정보를 표시 합니다.</span><span class="sxs-lookup"><span data-stu-id="17253-106">Displays general help information and help information about specific commands.</span></span>

## <a name="usage"></a><span data-ttu-id="17253-107">사용법</span><span class="sxs-lookup"><span data-stu-id="17253-107">Usage</span></span>

```cli
nuget help [command] [options]
nuget ? [command] [options]
```

<span data-ttu-id="17253-108">여기서 [command]는 도움말을 표시할 특정 명령을 식별 합니다.</span><span class="sxs-lookup"><span data-stu-id="17253-108">where [command] identifies a specific command for which to display help.</span></span>

> [!Warning]
> <span data-ttu-id="17253-109">Nuget.org에 "help" 라는 패키지가 있기  때문에 몇 가지 명령을 `nuget help install`사용 하 여에 대 한 도움말을 먼저 지정 하는 것에 유의 해야 합니다. 명령을 `nuget install help`지정 하면 install 명령에 대 한 도움말을 볼 수 없지만 대신 help 라는 이름의 패키지를 설치 합니다.</span><span class="sxs-lookup"><span data-stu-id="17253-109">With some commands, be mindful to specify *help* first, as with `nuget help install`, because there is a package named "help" on nuget.org. If you give the command `nuget install help`, you won't get help on the install command but will instead install the package named help.</span></span>

## <a name="options"></a><span data-ttu-id="17253-110">변수</span><span class="sxs-lookup"><span data-stu-id="17253-110">Options</span></span>

| <span data-ttu-id="17253-111">옵션</span><span class="sxs-lookup"><span data-stu-id="17253-111">Option</span></span> | <span data-ttu-id="17253-112">Description</span><span class="sxs-lookup"><span data-stu-id="17253-112">Description</span></span> |
| --- | --- |
| <span data-ttu-id="17253-113">모두</span><span class="sxs-lookup"><span data-stu-id="17253-113">All</span></span> | <span data-ttu-id="17253-114">사용 가능한 모든 명령에 대 한 자세한 도움말을 인쇄 합니다. 특정 명령이 지정 된 경우 무시 됩니다.</span><span class="sxs-lookup"><span data-stu-id="17253-114">Print detailed help for all available commands; ignored if a specific command is given.</span></span> |
| <span data-ttu-id="17253-115">ConfigFile</span><span class="sxs-lookup"><span data-stu-id="17253-115">ConfigFile</span></span> | <span data-ttu-id="17253-116">적용할 NuGet 설정 파일입니다.</span><span class="sxs-lookup"><span data-stu-id="17253-116">The NuGet configuration file to apply.</span></span> <span data-ttu-id="17253-117">지정하지 않으면 기본적으로 Windows에서는 `%AppData%\NuGet\NuGet.Config`, Mac이나 Linux에서는 `~/.nuget/NuGet/NuGet.Config`가 사용됩니다.</span><span class="sxs-lookup"><span data-stu-id="17253-117">If not specified, `%AppData%\NuGet\NuGet.Config` (Windows) or `~/.nuget/NuGet/NuGet.Config` (Mac/Linux) is used.</span></span>|
| <span data-ttu-id="17253-118">ForceEnglishOutput</span><span class="sxs-lookup"><span data-stu-id="17253-118">ForceEnglishOutput</span></span> | <span data-ttu-id="17253-119">*(3.5 이상)*  현재 언어 설정을 무시하고 영어를 기반으로 nuget.exe를 강제로 실행합니다.</span><span class="sxs-lookup"><span data-stu-id="17253-119">*(3.5+)* Forces nuget.exe to run using an invariant, English-based culture.</span></span> |
| <span data-ttu-id="17253-120">Help</span><span class="sxs-lookup"><span data-stu-id="17253-120">Help</span></span> | <span data-ttu-id="17253-121">도움말 명령 자체에 대 한 도움말 정보를 표시 합니다.</span><span class="sxs-lookup"><span data-stu-id="17253-121">Displays help information for the help command itself.</span></span> |
| <span data-ttu-id="17253-122">Markdown</span><span class="sxs-lookup"><span data-stu-id="17253-122">Markdown</span></span> | <span data-ttu-id="17253-123">에서 사용 하 `-All`는 경우 자세한 도움말을 markdown 형식으로 인쇄 합니다.</span><span class="sxs-lookup"><span data-stu-id="17253-123">Print detailed help in markdown format when used with `-All`.</span></span> <span data-ttu-id="17253-124">그렇지 않으면 무시 됩니다.</span><span class="sxs-lookup"><span data-stu-id="17253-124">Ignored otherwise.</span></span> |
| <span data-ttu-id="17253-125">NonInteractive</span><span class="sxs-lookup"><span data-stu-id="17253-125">NonInteractive</span></span> | <span data-ttu-id="17253-126">사용자 입력이나 확인에 대한 프롬프트를 표시하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="17253-126">Suppresses prompts for user input or confirmations.</span></span> |
| <span data-ttu-id="17253-127">Verbosity</span><span class="sxs-lookup"><span data-stu-id="17253-127">Verbosity</span></span> | <span data-ttu-id="17253-128">출력에 표시되는 세부정보의 양을 지정합니다: *정상적인*, *조용한*, *자세한*합니다.</span><span class="sxs-lookup"><span data-stu-id="17253-128">Specifies the amount of detail displayed in the output: *normal*, *quiet*, *detailed*.</span></span> |

<span data-ttu-id="17253-129">또한 [환경 변수](cli-ref-environment-variables.md)에 대한 정보를 참조할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="17253-129">Also see [Environment variables](cli-ref-environment-variables.md)</span></span>

## <a name="examples"></a><span data-ttu-id="17253-130">예제</span><span class="sxs-lookup"><span data-stu-id="17253-130">Examples</span></span>

```cli
nuget help
nuget help push
nuget ?
nuget push -?
nuget help -All -Markdown
```
