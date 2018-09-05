---
title: NuGet CLI init 명령
description: Nuget.exe init 명령에 대 한 참조
author: karann-msft
ms.author: karann
ms.date: 01/18/2018
ms.topic: reference
ms.openlocfilehash: 4441dc3cc35a96736b51867c196313fc9ccfdac2
ms.sourcegitcommit: 1d1406764c6af5fb7801d462e0c4afc9092fa569
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 09/04/2018
ms.locfileid: "43551412"
---
# <a name="init-command-nuget-cli"></a><span data-ttu-id="c3fec-103">init 명령 (NuGet CLI)</span><span class="sxs-lookup"><span data-stu-id="c3fec-103">init command (NuGet CLI)</span></span>

<span data-ttu-id="c3fec-104">**적용 대상:** 패키지 만들기 &bullet; **지원 되는 버전:** 3.3 이상</span><span class="sxs-lookup"><span data-stu-id="c3fec-104">**Applies to:** package creation &bullet; **Supported versions:** 3.3+</span></span>

<span data-ttu-id="c3fec-105">에 설명 된 대로 계층형 레이아웃을 사용 하 여 대상 폴더에 플랫 폴더에서 모든 패키지를 복사 합니다 [명령을 추가](cli-ref-add.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="c3fec-105">Copies all the packages from a flat folder to a destination folder using a hierarchical layout as described for the [add command](cli-ref-add.md).</span></span> <span data-ttu-id="c3fec-106">즉, 사용 하 여 `init` 사용 하는 것과 같습니다는 `add` 각 패키지 폴더에서 명령을 합니다.</span><span class="sxs-lookup"><span data-stu-id="c3fec-106">That is, using `init` is equivalent to using the `add` command on each package in the folder.</span></span>

<span data-ttu-id="c3fec-107">와 마찬가지로 `add`, 대상 로컬 폴더 또는 UNC 경로 해야 합니다. Nuget.org 또는 개인 서버와 같은 HTTP 패키지 리포지토리 지원 되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="c3fec-107">As with `add`, the destination must be either a local folder or a UNC path; HTTP package repositories such as nuget.org or private servers are not supported.</span></span>

## <a name="usage"></a><span data-ttu-id="c3fec-108">사용법</span><span class="sxs-lookup"><span data-stu-id="c3fec-108">Usage</span></span>

```cli
nuget init <source> <destination> [options]
```

<span data-ttu-id="c3fec-109">여기서 `<source>` 는 패키지가 포함 된 폴더 및 `<destination>` 로컬 폴더 인지 패키지 복사 되는 UNC 경로 이름입니다.</span><span class="sxs-lookup"><span data-stu-id="c3fec-109">where `<source>` is the folder containing packages and `<destination>` is the local folder or UNC pathname to which the packages are copied.</span></span>

## <a name="options"></a><span data-ttu-id="c3fec-110">옵션</span><span class="sxs-lookup"><span data-stu-id="c3fec-110">Options</span></span>

| <span data-ttu-id="c3fec-111">옵션</span><span class="sxs-lookup"><span data-stu-id="c3fec-111">Option</span></span> | <span data-ttu-id="c3fec-112">설명</span><span class="sxs-lookup"><span data-stu-id="c3fec-112">Description</span></span> |
| --- | --- |
| <span data-ttu-id="c3fec-113">ConfigFile</span><span class="sxs-lookup"><span data-stu-id="c3fec-113">ConfigFile</span></span> | <span data-ttu-id="c3fec-114">NuGet 구성 파일을 적용 합니다.</span><span class="sxs-lookup"><span data-stu-id="c3fec-114">The NuGet configuration file to apply.</span></span> <span data-ttu-id="c3fec-115">지정 하지 않으면 `%AppData%\NuGet\NuGet.Config` (Windows) 또는 `~/.nuget/NuGet/NuGet.Config` (Mac/Linux)가 사용 됩니다.</span><span class="sxs-lookup"><span data-stu-id="c3fec-115">If not specified, `%AppData%\NuGet\NuGet.Config` (Windows) or `~/.nuget/NuGet/NuGet.Config` (Mac/Linux) is used.</span></span>|
| <span data-ttu-id="c3fec-116">ForceEnglishOutput</span><span class="sxs-lookup"><span data-stu-id="c3fec-116">ForceEnglishOutput</span></span> | <span data-ttu-id="c3fec-117">*(3.5 이상)*  고정 영어 기반 문화권을 사용 하 여 실행할 nuget.exe를 강제로 수행 합니다.</span><span class="sxs-lookup"><span data-stu-id="c3fec-117">*(3.5+)* Forces nuget.exe to run using an invariant, English-based culture.</span></span> |
| <span data-ttu-id="c3fec-118">Expand</span><span class="sxs-lookup"><span data-stu-id="c3fec-118">Expand</span></span> | <span data-ttu-id="c3fec-119">모든 파일은 패키지 소스에 추가 되는 각 패키지에 추가 합니다. 동일 `-Expand` 사용 하 여는 `add` 명령입니다.</span><span class="sxs-lookup"><span data-stu-id="c3fec-119">Adds all files in each package that's added to the package source; same as `-Expand` with the `add` command.</span></span> |
| <span data-ttu-id="c3fec-120">도움말</span><span class="sxs-lookup"><span data-stu-id="c3fec-120">Help</span></span> | <span data-ttu-id="c3fec-121">도움말의 명령에 대 한 정보를 표시 합니다.</span><span class="sxs-lookup"><span data-stu-id="c3fec-121">Displays help information for the command.</span></span> |
| <span data-ttu-id="c3fec-122">NonInteractive</span><span class="sxs-lookup"><span data-stu-id="c3fec-122">NonInteractive</span></span> | <span data-ttu-id="c3fec-123">사용자 입력 또는 확인에 대 한 프롬프트를 표시 하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="c3fec-123">Suppresses prompts for user input or confirmations.</span></span> |
| <span data-ttu-id="c3fec-124">자세한 정도</span><span class="sxs-lookup"><span data-stu-id="c3fec-124">Verbosity</span></span> | <span data-ttu-id="c3fec-125">출력에 표시 되는 세부 정보의 양을 지정: *정상적인*, *quiet*, *자세한*합니다.</span><span class="sxs-lookup"><span data-stu-id="c3fec-125">Specifies the amount of detail displayed in the output: *normal*, *quiet*, *detailed*.</span></span> |

<span data-ttu-id="c3fec-126">또한 참조 [환경 변수](cli-ref-environment-variables.md)</span><span class="sxs-lookup"><span data-stu-id="c3fec-126">Also see [Environment variables](cli-ref-environment-variables.md)</span></span>

## <a name="examples"></a><span data-ttu-id="c3fec-127">예제</span><span class="sxs-lookup"><span data-stu-id="c3fec-127">Examples</span></span>

```cli
nuget init c:\foo c:\bar
nuget init \\foo\packages \\bar\packages -Expand
```
