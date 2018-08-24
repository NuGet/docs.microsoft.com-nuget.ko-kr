---
title: NuGet CLI locals 명령
description: Nuget.exe locals 명령에 대 한 참조
author: karann-msft
ms.author: karann
manager: unnir
ms.date: 03/19/2018
ms.topic: reference
ms.openlocfilehash: 38d8b9366fb2749b77c987c950da3aa9e7f029fc
ms.sourcegitcommit: 8d5121af528e68789485405e24e2100fda2868d6
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/23/2018
ms.locfileid: "42794137"
---
# <a name="locals-command-nuget-cli"></a><span data-ttu-id="d5163-103">locals 명령(NuGet CLI)</span><span class="sxs-lookup"><span data-stu-id="d5163-103">locals command (NuGet CLI)</span></span>

<span data-ttu-id="d5163-104">**적용 대상:** 소비 패키지 &bullet; **지원 되는 버전:** 3.3 이상</span><span class="sxs-lookup"><span data-stu-id="d5163-104">**Applies to:** package consumption &bullet; **Supported versions:** 3.3+</span></span>

<span data-ttu-id="d5163-105">같은 로컬 NuGet 리소스를 나열 하거나 선택을 취소 합니다 *http 캐시*를 *전역 패키지* 폴더 및 임시 폴더입니다.</span><span class="sxs-lookup"><span data-stu-id="d5163-105">Clears or lists local NuGet resources such as the *http-cache*, *global-packages* folder, and the temp folder.</span></span> <span data-ttu-id="d5163-106">`locals` 해당 위치의 목록을 표시 하려면 명령을 사용할 수도 있습니다.</span><span class="sxs-lookup"><span data-stu-id="d5163-106">The `locals` command can also be used to display a list of those locations.</span></span> <span data-ttu-id="d5163-107">자세한 내용은 [전역 패키지 및 캐시 폴더 관리](../consume-packages/managing-the-global-packages-and-cache-folders.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="d5163-107">For more information, see [Managing the global packages and cache folders](../consume-packages/managing-the-global-packages-and-cache-folders.md).</span></span>

## <a name="usage"></a><span data-ttu-id="d5163-108">사용법</span><span class="sxs-lookup"><span data-stu-id="d5163-108">Usage</span></span>

```cli
nuget locals <folder> [options]
```

<span data-ttu-id="d5163-109">여기서 `<folder>` 중 하나인 `all`를 `http-cache`, `packages-cache` *(3.5 및 이전 버전)* 를 `global-packages`를 `temp` *(3.4 이상)*, 및 `plugins-cache` *(4.8 이상)* 합니다.</span><span class="sxs-lookup"><span data-stu-id="d5163-109">where `<folder>` is one of `all`, `http-cache`, `packages-cache` *(3.5 and earlier)*, `global-packages`, `temp` *(3.4+)*, and `plugins-cache` *(4.8+)*.</span></span>

## <a name="options"></a><span data-ttu-id="d5163-110">옵션</span><span class="sxs-lookup"><span data-stu-id="d5163-110">Options</span></span>

| <span data-ttu-id="d5163-111">옵션</span><span class="sxs-lookup"><span data-stu-id="d5163-111">Option</span></span> | <span data-ttu-id="d5163-112">설명</span><span class="sxs-lookup"><span data-stu-id="d5163-112">Description</span></span> |
| --- | --- |
| <span data-ttu-id="d5163-113">지우기</span><span class="sxs-lookup"><span data-stu-id="d5163-113">Clear</span></span> | <span data-ttu-id="d5163-114">지정된 된 폴더를 지웁니다.</span><span class="sxs-lookup"><span data-stu-id="d5163-114">Clears the specified folder.</span></span> |
| <span data-ttu-id="d5163-115">ConfigFile</span><span class="sxs-lookup"><span data-stu-id="d5163-115">ConfigFile</span></span> | <span data-ttu-id="d5163-116">NuGet 구성 파일을 적용 합니다.</span><span class="sxs-lookup"><span data-stu-id="d5163-116">The NuGet configuration file to apply.</span></span> <span data-ttu-id="d5163-117">지정 하지 않으면 `%AppData%\NuGet\NuGet.Config` (Windows) 또는 `~/.nuget/NuGet/NuGet.Config` (Mac/Linux)가 사용 됩니다.</span><span class="sxs-lookup"><span data-stu-id="d5163-117">If not specified, `%AppData%\NuGet\NuGet.Config` (Windows) or `~/.nuget/NuGet/NuGet.Config` (Mac/Linux) is used.</span></span>|
| <span data-ttu-id="d5163-118">ForceEnglishOutput</span><span class="sxs-lookup"><span data-stu-id="d5163-118">ForceEnglishOutput</span></span> | <span data-ttu-id="d5163-119">*(3.5 이상)*  고정 영어 기반 문화권을 사용 하 여 실행할 nuget.exe를 강제로 수행 합니다.</span><span class="sxs-lookup"><span data-stu-id="d5163-119">*(3.5+)* Forces nuget.exe to run using an invariant, English-based culture.</span></span> |
| <span data-ttu-id="d5163-120">도움말</span><span class="sxs-lookup"><span data-stu-id="d5163-120">Help</span></span> | <span data-ttu-id="d5163-121">도움말의 명령에 대 한 정보를 표시 합니다.</span><span class="sxs-lookup"><span data-stu-id="d5163-121">Displays help information for the command.</span></span> |
| <span data-ttu-id="d5163-122">목록</span><span class="sxs-lookup"><span data-stu-id="d5163-122">List</span></span> | <span data-ttu-id="d5163-123">지정된 된 폴더의 위치 또는 함께 사용할 경우 모든 폴더의 위치 나열 *모든*합니다.</span><span class="sxs-lookup"><span data-stu-id="d5163-123">Lists the location of the specified folder, or the locations of all folders when used with *all*.</span></span> |
| <span data-ttu-id="d5163-124">NonInteractive</span><span class="sxs-lookup"><span data-stu-id="d5163-124">NonInteractive</span></span> | <span data-ttu-id="d5163-125">사용자 입력 또는 확인에 대 한 프롬프트를 표시 하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="d5163-125">Suppresses prompts for user input or confirmations.</span></span> |
| <span data-ttu-id="d5163-126">자세한 정도</span><span class="sxs-lookup"><span data-stu-id="d5163-126">Verbosity</span></span> | <span data-ttu-id="d5163-127">출력에 표시 되는 세부 정보의 양을 지정: *정상적인*, *quiet*, *자세한*합니다.</span><span class="sxs-lookup"><span data-stu-id="d5163-127">Specifies the amount of detail displayed in the output: *normal*, *quiet*, *detailed*.</span></span> |

<span data-ttu-id="d5163-128">또한 참조 [환경 변수](cli-ref-environment-variables.md)</span><span class="sxs-lookup"><span data-stu-id="d5163-128">Also see [Environment variables](cli-ref-environment-variables.md)</span></span>

## <a name="examples"></a><span data-ttu-id="d5163-129">예제</span><span class="sxs-lookup"><span data-stu-id="d5163-129">Examples</span></span>

```cli
nuget locals all -list
nuget locals http-cache -clear
```

<span data-ttu-id="d5163-130">추가 예제를 보려면 [전역 패키지 및 캐시 폴더 관리](../consume-packages/managing-the-global-packages-and-cache-folders.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="d5163-130">For additional examples, see [Managing the global packages and cache folders](../consume-packages/managing-the-global-packages-and-cache-folders.md).</span></span>
