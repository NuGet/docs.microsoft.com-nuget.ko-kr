---
title: NuGet CLI init 명령
description: Nuget.exe init 명령에 대 한 참조
author: karann-msft
ms.author: karann
ms.date: 01/18/2018
ms.topic: reference
ms.openlocfilehash: 4441dc3cc35a96736b51867c196313fc9ccfdac2
ms.sourcegitcommit: efc18d484fdf0c7a8979b564dcb191c030601bb4
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/18/2019
ms.locfileid: "68327780"
---
# <a name="init-command-nuget-cli"></a><span data-ttu-id="a28ca-103">init 명령 (NuGet CLI)</span><span class="sxs-lookup"><span data-stu-id="a28ca-103">init command (NuGet CLI)</span></span>

<span data-ttu-id="a28ca-104">**적용 대상:** 패키지 만들기 &bullet; **지원 되는 버전:** 3.3+</span><span class="sxs-lookup"><span data-stu-id="a28ca-104">**Applies to:** package creation &bullet; **Supported versions:** 3.3+</span></span>

<span data-ttu-id="a28ca-105">[추가 명령](cli-ref-add.md)에 설명 된 대로 계층적 레이아웃을 사용 하 여 플랫 폴더의 모든 패키지를 대상 폴더에 복사 합니다.</span><span class="sxs-lookup"><span data-stu-id="a28ca-105">Copies all the packages from a flat folder to a destination folder using a hierarchical layout as described for the [add command](cli-ref-add.md).</span></span> <span data-ttu-id="a28ca-106">즉,를 사용 `init` 하는 것은 폴더 `add` 의 각 패키지에 대해 명령을 사용 하는 것과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="a28ca-106">That is, using `init` is equivalent to using the `add` command on each package in the folder.</span></span>

<span data-ttu-id="a28ca-107">와 `add`마찬가지로 대상은 로컬 폴더 또는 UNC 경로 여야 합니다. Nuget.org 또는 private 서버와 같은 HTTP 패키지 리포지토리는 지원 되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="a28ca-107">As with `add`, the destination must be either a local folder or a UNC path; HTTP package repositories such as nuget.org or private servers are not supported.</span></span>

## <a name="usage"></a><span data-ttu-id="a28ca-108">사용법</span><span class="sxs-lookup"><span data-stu-id="a28ca-108">Usage</span></span>

```cli
nuget init <source> <destination> [options]
```

<span data-ttu-id="a28ca-109">여기서 `<source>` 는 패키지가 포함 된 폴더이 `<destination>` 고은 패키지가 복사 되는 로컬 폴더 또는 UNC 경로 이름입니다.</span><span class="sxs-lookup"><span data-stu-id="a28ca-109">where `<source>` is the folder containing packages and `<destination>` is the local folder or UNC pathname to which the packages are copied.</span></span>

## <a name="options"></a><span data-ttu-id="a28ca-110">변수</span><span class="sxs-lookup"><span data-stu-id="a28ca-110">Options</span></span>

| <span data-ttu-id="a28ca-111">옵션</span><span class="sxs-lookup"><span data-stu-id="a28ca-111">Option</span></span> | <span data-ttu-id="a28ca-112">설명</span><span class="sxs-lookup"><span data-stu-id="a28ca-112">Description</span></span> |
| --- | --- |
| <span data-ttu-id="a28ca-113">ConfigFile</span><span class="sxs-lookup"><span data-stu-id="a28ca-113">ConfigFile</span></span> | <span data-ttu-id="a28ca-114">적용할 NuGet 설정 파일입니다.</span><span class="sxs-lookup"><span data-stu-id="a28ca-114">The NuGet configuration file to apply.</span></span> <span data-ttu-id="a28ca-115">지정하지 않으면 기본적으로 Windows에서는 `%AppData%\NuGet\NuGet.Config`, Mac이나 Linux에서는 `~/.nuget/NuGet/NuGet.Config`가 사용됩니다.</span><span class="sxs-lookup"><span data-stu-id="a28ca-115">If not specified, `%AppData%\NuGet\NuGet.Config` (Windows) or `~/.nuget/NuGet/NuGet.Config` (Mac/Linux) is used.</span></span>|
| <span data-ttu-id="a28ca-116">ForceEnglishOutput</span><span class="sxs-lookup"><span data-stu-id="a28ca-116">ForceEnglishOutput</span></span> | <span data-ttu-id="a28ca-117">*(3.5 이상)*  현재 언어 설정을 무시하고 영어를 기반으로 nuget.exe를 강제로 실행합니다.</span><span class="sxs-lookup"><span data-stu-id="a28ca-117">*(3.5+)* Forces nuget.exe to run using an invariant, English-based culture.</span></span> |
| <span data-ttu-id="a28ca-118">Expand</span><span class="sxs-lookup"><span data-stu-id="a28ca-118">Expand</span></span> | <span data-ttu-id="a28ca-119">패키지 소스에 추가 된 각 패키지의 모든 파일을 추가 합니다. 명령을 사용 `-Expand` 하는 `add` 것과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="a28ca-119">Adds all files in each package that's added to the package source; same as `-Expand` with the `add` command.</span></span> |
| <span data-ttu-id="a28ca-120">Help</span><span class="sxs-lookup"><span data-stu-id="a28ca-120">Help</span></span> | <span data-ttu-id="a28ca-121">명령어에 대한 도움말을 표시합니다.</span><span class="sxs-lookup"><span data-stu-id="a28ca-121">Displays help information for the command.</span></span> |
| <span data-ttu-id="a28ca-122">NonInteractive</span><span class="sxs-lookup"><span data-stu-id="a28ca-122">NonInteractive</span></span> | <span data-ttu-id="a28ca-123">사용자 입력이나 확인에 대한 프롬프트를 표시하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="a28ca-123">Suppresses prompts for user input or confirmations.</span></span> |
| <span data-ttu-id="a28ca-124">Verbosity</span><span class="sxs-lookup"><span data-stu-id="a28ca-124">Verbosity</span></span> | <span data-ttu-id="a28ca-125">출력에 표시되는 세부정보의 양을 지정합니다: *정상적인*, *조용한*, *자세한*합니다.</span><span class="sxs-lookup"><span data-stu-id="a28ca-125">Specifies the amount of detail displayed in the output: *normal*, *quiet*, *detailed*.</span></span> |

<span data-ttu-id="a28ca-126">또한 [환경 변수](cli-ref-environment-variables.md)에 대한 정보를 참조할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="a28ca-126">Also see [Environment variables](cli-ref-environment-variables.md)</span></span>

## <a name="examples"></a><span data-ttu-id="a28ca-127">예제</span><span class="sxs-lookup"><span data-stu-id="a28ca-127">Examples</span></span>

```cli
nuget init c:\foo c:\bar
nuget init \\foo\packages \\bar\packages -Expand
```
