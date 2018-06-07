---
title: NuGet CLI init 명령
description: Nuget.exe 초기화 명령에 대 한 참조
author: karann-msft
ms.author: karann
manager: unnir
ms.date: 01/18/2018
ms.topic: reference
ms.openlocfilehash: f4fda33aabd51fbbf0e5559baaa42af065366ba4
ms.sourcegitcommit: 2a6d200012cdb4cbf5ab1264f12fecf9ae12d769
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 06/06/2018
ms.locfileid: "34817820"
---
# <a name="init-command-nuget-cli"></a><span data-ttu-id="5f4a8-103">초기화 명령 (NuGet CLI)</span><span class="sxs-lookup"><span data-stu-id="5f4a8-103">init command (NuGet CLI)</span></span>

<span data-ttu-id="5f4a8-104">**적용 대상:** 패키지 만들기가 &bullet; **지원 되는 버전:** 3.3 +</span><span class="sxs-lookup"><span data-stu-id="5f4a8-104">**Applies to:** package creation &bullet; **Supported versions:** 3.3+</span></span>

<span data-ttu-id="5f4a8-105">에 대 한 설명 된 대로 계층 레이아웃을 사용 하 여 대상 폴더를 단일 폴더에서 모든 패키지를 복사는 [명령을 추가](cli-ref-add.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="5f4a8-105">Copies all the packages from a flat folder to a destination folder using a hierarchical layout as described for the [add command](cli-ref-add.md).</span></span> <span data-ttu-id="5f4a8-106">즉, 사용 하 여 `init` 사용 하는 `add` 폴더에 각 패키지에 명령 합니다.</span><span class="sxs-lookup"><span data-stu-id="5f4a8-106">That is, using `init` is equivalent to using the `add` command on each package in the folder.</span></span>

<span data-ttu-id="5f4a8-107">와 마찬가지로 `add`, 대상 로컬 폴더 또는 UNC 경로 여야 합니다 Nuget.org 또는 개인 서버와 같이 HTTP 패키지 저장소는 지원 되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="5f4a8-107">As with `add`, the destination must be either a local folder or a UNC path; HTTP package repositories such as nuget.org or private servers are not supported.</span></span>

## <a name="usage"></a><span data-ttu-id="5f4a8-108">사용법</span><span class="sxs-lookup"><span data-stu-id="5f4a8-108">Usage</span></span>

```cli
nuget init <source> <destination> [options]
```

<span data-ttu-id="5f4a8-109">여기서 `<source>` 는 패키지가 포함 된 폴더 및 `<destination>` 로컬 폴더 인지 패키지 복사 되는 UNC 경로 이름입니다.</span><span class="sxs-lookup"><span data-stu-id="5f4a8-109">where `<source>` is the folder containing packages and `<destination>` is the local folder or UNC pathname to which the packages are copied.</span></span>

## <a name="options"></a><span data-ttu-id="5f4a8-110">옵션</span><span class="sxs-lookup"><span data-stu-id="5f4a8-110">Options</span></span>

| <span data-ttu-id="5f4a8-111">옵션</span><span class="sxs-lookup"><span data-stu-id="5f4a8-111">Option</span></span> | <span data-ttu-id="5f4a8-112">설명</span><span class="sxs-lookup"><span data-stu-id="5f4a8-112">Description</span></span> |
| --- | --- |
| <span data-ttu-id="5f4a8-113">ConfigFile</span><span class="sxs-lookup"><span data-stu-id="5f4a8-113">ConfigFile</span></span> | <span data-ttu-id="5f4a8-114">적용할 NuGet 구성 파일입니다.</span><span class="sxs-lookup"><span data-stu-id="5f4a8-114">The NuGet configuration file to apply.</span></span> <span data-ttu-id="5f4a8-115">지정 하지 않으면 `%AppData%\NuGet\NuGet.Config` (Windows) 또는 `~/.nuget/NuGet/NuGet.Config` (Mac/Linux)가 사용 됩니다.</span><span class="sxs-lookup"><span data-stu-id="5f4a8-115">If not specified, `%AppData%\NuGet\NuGet.Config` (Windows) or `~/.nuget/NuGet/NuGet.Config` (Mac/Linux) is used.</span></span>|
| <span data-ttu-id="5f4a8-116">ForceEnglishOutput</span><span class="sxs-lookup"><span data-stu-id="5f4a8-116">ForceEnglishOutput</span></span> | <span data-ttu-id="5f4a8-117">*(3.5 +)*  고정, 영어 기반 문화권을 사용 하 여 실행할 nuget.exe를 강제로 수행 합니다.</span><span class="sxs-lookup"><span data-stu-id="5f4a8-117">*(3.5+)* Forces nuget.exe to run using an invariant, English-based culture.</span></span> |
| <span data-ttu-id="5f4a8-118">Expand</span><span class="sxs-lookup"><span data-stu-id="5f4a8-118">Expand</span></span> | <span data-ttu-id="5f4a8-119">모든 파일은 패키지 소스에 추가 된 각 패키지에 추가 와 동일 `-Expand` 와 `add` 명령입니다.</span><span class="sxs-lookup"><span data-stu-id="5f4a8-119">Adds all files in each package that's added to the package source; same as `-Expand` with the `add` command.</span></span> |
| <span data-ttu-id="5f4a8-120">도움말</span><span class="sxs-lookup"><span data-stu-id="5f4a8-120">Help</span></span> | <span data-ttu-id="5f4a8-121">도움말의 명령에 대 한 정보를 표시 합니다.</span><span class="sxs-lookup"><span data-stu-id="5f4a8-121">Displays help information for the command.</span></span> |
| <span data-ttu-id="5f4a8-122">NonInteractive</span><span class="sxs-lookup"><span data-stu-id="5f4a8-122">NonInteractive</span></span> | <span data-ttu-id="5f4a8-123">사용자 입력 또는 확인에 대 한 프롬프트를 표시 하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="5f4a8-123">Suppresses prompts for user input or confirmations.</span></span> |
| <span data-ttu-id="5f4a8-124">자세한 정도</span><span class="sxs-lookup"><span data-stu-id="5f4a8-124">Verbosity</span></span> | <span data-ttu-id="5f4a8-125">출력에 표시 되는 세부 정보 수준을 지정: *일반*, *quiet*, *자세한*합니다.</span><span class="sxs-lookup"><span data-stu-id="5f4a8-125">Specifies the amount of detail displayed in the output: *normal*, *quiet*, *detailed*.</span></span> |

<span data-ttu-id="5f4a8-126">또한 참조 [환경 변수](cli-ref-environment-variables.md)</span><span class="sxs-lookup"><span data-stu-id="5f4a8-126">Also see [Environment variables](cli-ref-environment-variables.md)</span></span>

## <a name="examples"></a><span data-ttu-id="5f4a8-127">예제</span><span class="sxs-lookup"><span data-stu-id="5f4a8-127">Examples</span></span>

```cli
nuget init c:\foo c:\bar
nuget init \\foo\packages \\bar\packages -Expand
```
