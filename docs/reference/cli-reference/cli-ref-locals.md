---
title: NuGet CLI 지역 명령
description: Nuget.exe 지역 명령에 대 한 참조
author: karann-msft
ms.author: karann
ms.date: 03/19/2018
ms.topic: reference
ms.openlocfilehash: b02360c38ad66c95bbe3c7d403ef4a959112c91a
ms.sourcegitcommit: efc18d484fdf0c7a8979b564dcb191c030601bb4
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/18/2019
ms.locfileid: "68327810"
---
# <a name="locals-command-nuget-cli"></a><span data-ttu-id="99ce8-103">locals 명령(NuGet CLI)</span><span class="sxs-lookup"><span data-stu-id="99ce8-103">locals command (NuGet CLI)</span></span>

<span data-ttu-id="99ce8-104">**적용 대상:** 패키지 &bullet; 사용 **지원 버전:** 3.3+</span><span class="sxs-lookup"><span data-stu-id="99ce8-104">**Applies to:** package consumption &bullet; **Supported versions:** 3.3+</span></span>

<span data-ttu-id="99ce8-105">*Http 캐시*, *전역 패키지* 폴더 및 임시 폴더와 같은 로컬 NuGet 리소스를 지우거 나 나열 합니다.</span><span class="sxs-lookup"><span data-stu-id="99ce8-105">Clears or lists local NuGet resources such as the *http-cache*, *global-packages* folder, and the temp folder.</span></span> <span data-ttu-id="99ce8-106">`locals` 명령을 사용 하 여 해당 위치의 목록을 표시할 수도 있습니다.</span><span class="sxs-lookup"><span data-stu-id="99ce8-106">The `locals` command can also be used to display a list of those locations.</span></span> <span data-ttu-id="99ce8-107">자세한 내용은 [전역 패키지 및 캐시 폴더 관리](../../consume-packages/managing-the-global-packages-and-cache-folders.md)를 참조 하세요.</span><span class="sxs-lookup"><span data-stu-id="99ce8-107">For more information, see [Managing the global packages and cache folders](../../consume-packages/managing-the-global-packages-and-cache-folders.md).</span></span>

## <a name="usage"></a><span data-ttu-id="99ce8-108">사용</span><span class="sxs-lookup"><span data-stu-id="99ce8-108">Usage</span></span>

```cli
nuget locals <folder> [options]
```

<span data-ttu-id="99ce8-109">여기서 `<folder>` 는 `all` `global-packages` `temp` , `plugins-cache`, (3.5 및 이전 버전),, (3.4 +) 및 (4.8 +) 중 하나입니다. `packages-cache` `http-cache`</span><span class="sxs-lookup"><span data-stu-id="99ce8-109">where `<folder>` is one of `all`, `http-cache`, `packages-cache` *(3.5 and earlier)*, `global-packages`, `temp` *(3.4+)*, and `plugins-cache` *(4.8+)*.</span></span>

## <a name="options"></a><span data-ttu-id="99ce8-110">변수</span><span class="sxs-lookup"><span data-stu-id="99ce8-110">Options</span></span>

| <span data-ttu-id="99ce8-111">옵션</span><span class="sxs-lookup"><span data-stu-id="99ce8-111">Option</span></span> | <span data-ttu-id="99ce8-112">Description</span><span class="sxs-lookup"><span data-stu-id="99ce8-112">Description</span></span> |
| --- | --- |
| <span data-ttu-id="99ce8-113">Clear</span><span class="sxs-lookup"><span data-stu-id="99ce8-113">Clear</span></span> | <span data-ttu-id="99ce8-114">지정 된 폴더를 지웁니다.</span><span class="sxs-lookup"><span data-stu-id="99ce8-114">Clears the specified folder.</span></span> |
| <span data-ttu-id="99ce8-115">ConfigFile</span><span class="sxs-lookup"><span data-stu-id="99ce8-115">ConfigFile</span></span> | <span data-ttu-id="99ce8-116">적용할 NuGet 설정 파일입니다.</span><span class="sxs-lookup"><span data-stu-id="99ce8-116">The NuGet configuration file to apply.</span></span> <span data-ttu-id="99ce8-117">지정하지 않으면 기본적으로 Windows에서는 `%AppData%\NuGet\NuGet.Config`, Mac이나 Linux에서는 `~/.nuget/NuGet/NuGet.Config`가 사용됩니다.</span><span class="sxs-lookup"><span data-stu-id="99ce8-117">If not specified, `%AppData%\NuGet\NuGet.Config` (Windows) or `~/.nuget/NuGet/NuGet.Config` (Mac/Linux) is used.</span></span>|
| <span data-ttu-id="99ce8-118">ForceEnglishOutput</span><span class="sxs-lookup"><span data-stu-id="99ce8-118">ForceEnglishOutput</span></span> | <span data-ttu-id="99ce8-119">*(3.5 이상)*  현재 언어 설정을 무시하고 영어를 기반으로 nuget.exe를 강제로 실행합니다.</span><span class="sxs-lookup"><span data-stu-id="99ce8-119">*(3.5+)* Forces nuget.exe to run using an invariant, English-based culture.</span></span> |
| <span data-ttu-id="99ce8-120">Help</span><span class="sxs-lookup"><span data-stu-id="99ce8-120">Help</span></span> | <span data-ttu-id="99ce8-121">명령어에 대한 도움말을 표시합니다.</span><span class="sxs-lookup"><span data-stu-id="99ce8-121">Displays help information for the command.</span></span> |
| <span data-ttu-id="99ce8-122">List</span><span class="sxs-lookup"><span data-stu-id="99ce8-122">List</span></span> | <span data-ttu-id="99ce8-123">지정 된 폴더의 위치 또는 모든 폴더의 위치를 *모두*함께 사용할 경우 나열 합니다.</span><span class="sxs-lookup"><span data-stu-id="99ce8-123">Lists the location of the specified folder, or the locations of all folders when used with *all*.</span></span> |
| <span data-ttu-id="99ce8-124">NonInteractive</span><span class="sxs-lookup"><span data-stu-id="99ce8-124">NonInteractive</span></span> | <span data-ttu-id="99ce8-125">사용자 입력이나 확인에 대한 프롬프트를 표시하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="99ce8-125">Suppresses prompts for user input or confirmations.</span></span> |
| <span data-ttu-id="99ce8-126">Verbosity</span><span class="sxs-lookup"><span data-stu-id="99ce8-126">Verbosity</span></span> | <span data-ttu-id="99ce8-127">출력에 표시되는 세부정보의 양을 지정합니다: *정상적인*, *조용한*, *자세한*합니다.</span><span class="sxs-lookup"><span data-stu-id="99ce8-127">Specifies the amount of detail displayed in the output: *normal*, *quiet*, *detailed*.</span></span> |

<span data-ttu-id="99ce8-128">또한 [환경 변수](cli-ref-environment-variables.md)에 대한 정보를 참조할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="99ce8-128">Also see [Environment variables](cli-ref-environment-variables.md)</span></span>

## <a name="examples"></a><span data-ttu-id="99ce8-129">예</span><span class="sxs-lookup"><span data-stu-id="99ce8-129">Examples</span></span>

```cli
nuget locals all -list
nuget locals http-cache -clear
```

<span data-ttu-id="99ce8-130">추가 예제는 [전역 패키지 및 캐시 폴더 관리](../../consume-packages/managing-the-global-packages-and-cache-folders.md)를 참조 하세요.</span><span class="sxs-lookup"><span data-stu-id="99ce8-130">For additional examples, see [Managing the global packages and cache folders](../../consume-packages/managing-the-global-packages-and-cache-folders.md).</span></span>
