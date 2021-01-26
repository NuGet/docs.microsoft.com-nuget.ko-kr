---
title: NuGet CLI 도움말 명령
description: nuget.exe 도움말 명령에 대 한 참조
author: JonDouglas
ms.author: jodou
ms.date: 01/18/2018
ms.topic: reference
ms.openlocfilehash: 5d91638c4a6f167ea8a04e5dfa2905cb55084ddd
ms.sourcegitcommit: ee6c3f203648a5561c809db54ebeb1d0f0598b68
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 01/26/2021
ms.locfileid: "98779356"
---
# <a name="help-or--command-nuget-cli"></a><span data-ttu-id="e8980-103">help or ?</span><span class="sxs-lookup"><span data-stu-id="e8980-103">help or ?</span></span> <span data-ttu-id="e8980-104">command (NuGet CLI)</span><span class="sxs-lookup"><span data-stu-id="e8980-104">command (NuGet CLI)</span></span>

<span data-ttu-id="e8980-105">**적용 대상:** &bullet; **지원 되** 는 모든 버전: 모두</span><span class="sxs-lookup"><span data-stu-id="e8980-105">**Applies to:** all &bullet; **Supported versions**: all</span></span>

<span data-ttu-id="e8980-106">일반 도움말 정보 및 특정 명령에 대 한 도움말 정보를 표시 합니다.</span><span class="sxs-lookup"><span data-stu-id="e8980-106">Displays general help information and help information about specific commands.</span></span>

## <a name="usage"></a><span data-ttu-id="e8980-107">사용량</span><span class="sxs-lookup"><span data-stu-id="e8980-107">Usage</span></span>

```cli
nuget help [command] [options]
nuget ? [command] [options]
```

<span data-ttu-id="e8980-108">여기서 [command]는 도움말을 표시할 특정 명령을 식별 합니다.</span><span class="sxs-lookup"><span data-stu-id="e8980-108">where [command] identifies a specific command for which to display help.</span></span>

> [!Warning]
> <span data-ttu-id="e8980-109"> `nuget help install` Nuget.org에 "help" 라는 패키지가 있기 때문에 몇 가지 명령을 사용 하 여에 대 한 도움말을 먼저 지정 하는 것에 유의 해야 합니다. 명령을 지정 하면 `nuget install help` install 명령에 대 한 도움말을 볼 수 없지만 대신 help 라는 이름의 패키지를 설치 합니다.</span><span class="sxs-lookup"><span data-stu-id="e8980-109">With some commands, be mindful to specify *help* first, as with `nuget help install`, because there is a package named "help" on nuget.org. If you give the command `nuget install help`, you won't get help on the install command but will instead install the package named help.</span></span>

## <a name="options"></a><span data-ttu-id="e8980-110">옵션</span><span class="sxs-lookup"><span data-stu-id="e8980-110">Options</span></span>

- **`-All`**

  <span data-ttu-id="e8980-111">사용 가능한 모든 명령에 대 한 자세한 도움말을 인쇄 합니다. 특정 명령이 지정 된 경우 무시 됩니다.</span><span class="sxs-lookup"><span data-stu-id="e8980-111">Print detailed help for all available commands; ignored if a specific command is given.</span></span>

- **`-ConfigFile`**

  <span data-ttu-id="e8980-112">적용할 NuGet 구성 파일입니다.</span><span class="sxs-lookup"><span data-stu-id="e8980-112">The NuGet configuration file to apply.</span></span> <span data-ttu-id="e8980-113">지정 하지 않으면 `%AppData%\NuGet\NuGet.Config` (Windows) 또는 `~/.nuget/NuGet/NuGet.Config` 또는 `~/.config/NuGet/NuGet.Config` (Mac/Linux)가 사용 됩니다.</span><span class="sxs-lookup"><span data-stu-id="e8980-113">If not specified, `%AppData%\NuGet\NuGet.Config` (Windows), or `~/.nuget/NuGet/NuGet.Config` or `~/.config/NuGet/NuGet.Config` (Mac/Linux) is used.</span></span>

- **`-ForceEnglishOutput`**

  <span data-ttu-id="e8980-114">*(3.5 +)* 고정 된 영어 기반 문화권을 사용 하 여 nuget.exe을 강제로 실행 합니다.</span><span class="sxs-lookup"><span data-stu-id="e8980-114">*(3.5+)* Forces nuget.exe to run using an invariant, English-based culture.</span></span>

- **`-?|-help`**

  <span data-ttu-id="e8980-115">명령에 대 한 도움말 정보를 표시 합니다.</span><span class="sxs-lookup"><span data-stu-id="e8980-115">Displays help information for the command.</span></span>

- **`-Markdown`**

  <span data-ttu-id="e8980-116">에서 사용 하는 경우 자세한 도움말을 markdown 형식으로 인쇄 `-All` 합니다.</span><span class="sxs-lookup"><span data-stu-id="e8980-116">Print detailed help in markdown format when used with `-All`.</span></span> <span data-ttu-id="e8980-117">그렇지 않으면 무시 됩니다.</span><span class="sxs-lookup"><span data-stu-id="e8980-117">Ignored otherwise.</span></span>

- **`-NonInteractive`**

  <span data-ttu-id="e8980-118">사용자 입력 또는 확인에 대 한 프롬프트를 표시 하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="e8980-118">Suppresses prompts for user input or confirmations.</span></span>

- **`-Verbosity [normal|quiet|detailed]`**

  <span data-ttu-id="e8980-119">출력에 표시 되는 세부 정보의 양을 지정 합니다. `normal` (기본값), `quiet` 또는 `detailed` 입니다.</span><span class="sxs-lookup"><span data-stu-id="e8980-119">Specifies the amount of detail displayed in the output: `normal` (the default), `quiet`, or `detailed`.</span></span>

<span data-ttu-id="e8980-120">[환경 변수](cli-ref-environment-variables.md) 참조</span><span class="sxs-lookup"><span data-stu-id="e8980-120">Also see [Environment variables](cli-ref-environment-variables.md)</span></span>

## <a name="examples"></a><span data-ttu-id="e8980-121">예</span><span class="sxs-lookup"><span data-stu-id="e8980-121">Examples</span></span>

```cli
nuget help
nuget help push
nuget ?
nuget push -?
nuget help -All -Markdown
```
