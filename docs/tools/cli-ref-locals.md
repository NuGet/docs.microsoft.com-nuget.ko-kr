---
title: NuGet CLI 지역 명령
description: Nuget.exe 지역 명령에 대 한 참조
author: karann-msft
ms.author: karann
manager: unnir
ms.date: 03/19/2018
ms.topic: reference
ms.openlocfilehash: 90e8c85e7a3e0e9520933e2ddd6dd84447475f2b
ms.sourcegitcommit: 2a6d200012cdb4cbf5ab1264f12fecf9ae12d769
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 06/06/2018
ms.locfileid: "34818203"
---
# <a name="locals-command-nuget-cli"></a><span data-ttu-id="401d5-103">locals 명령(NuGet CLI)</span><span class="sxs-lookup"><span data-stu-id="401d5-103">locals command (NuGet CLI)</span></span>

<span data-ttu-id="401d5-104">**적용 대상:** 소비 패키지 &bullet; **지원 되는 버전:** 3.3 +</span><span class="sxs-lookup"><span data-stu-id="401d5-104">**Applies to:** package consumption &bullet; **Supported versions:** 3.3+</span></span>

<span data-ttu-id="401d5-105">와 같은 로컬 NuGet 리소스를 나열 하거나 선택을 취소는 *http 캐시*, *전역 패키지* 폴더 및 임시 폴더입니다.</span><span class="sxs-lookup"><span data-stu-id="401d5-105">Clears or lists local NuGet resources such as the *http-cache*, *global-packages* folder, and the temp folder.</span></span> <span data-ttu-id="401d5-106">`locals` 해당 위치의 목록을 표시 하려면 명령을 사용할 수도 있습니다.</span><span class="sxs-lookup"><span data-stu-id="401d5-106">The `locals` command can also be used to display a list of those locations.</span></span> <span data-ttu-id="401d5-107">자세한 내용은 참조 [전역 패키지 및 캐시 폴더 관리](../consume-packages/managing-the-global-packages-and-cache-folders.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="401d5-107">For more information, see [Managing the global packages and cache folders](../consume-packages/managing-the-global-packages-and-cache-folders.md).</span></span>

## <a name="usage"></a><span data-ttu-id="401d5-108">사용법</span><span class="sxs-lookup"><span data-stu-id="401d5-108">Usage</span></span>

```cli
nuget locals <folder> [options]
```

<span data-ttu-id="401d5-109">여기서 `<folder>` 중 하나인 `all`, `http-cache`, `packages-cache` *(3.5 및 이전 버전)*, `global-packages`, 및 `temp` *(3.4 +)* 합니다.</span><span class="sxs-lookup"><span data-stu-id="401d5-109">where `<folder>` is one of `all`, `http-cache`, `packages-cache` *(3.5 and earlier)*, `global-packages`, and `temp` *(3.4+)*.</span></span>

## <a name="options"></a><span data-ttu-id="401d5-110">옵션</span><span class="sxs-lookup"><span data-stu-id="401d5-110">Options</span></span>

| <span data-ttu-id="401d5-111">옵션</span><span class="sxs-lookup"><span data-stu-id="401d5-111">Option</span></span> | <span data-ttu-id="401d5-112">설명</span><span class="sxs-lookup"><span data-stu-id="401d5-112">Description</span></span> |
| --- | --- |
| <span data-ttu-id="401d5-113">지우기</span><span class="sxs-lookup"><span data-stu-id="401d5-113">Clear</span></span> | <span data-ttu-id="401d5-114">지정된 된 폴더를 지웁니다.</span><span class="sxs-lookup"><span data-stu-id="401d5-114">Clears the specified folder.</span></span> |
| <span data-ttu-id="401d5-115">ConfigFile</span><span class="sxs-lookup"><span data-stu-id="401d5-115">ConfigFile</span></span> | <span data-ttu-id="401d5-116">적용할 NuGet 구성 파일입니다.</span><span class="sxs-lookup"><span data-stu-id="401d5-116">The NuGet configuration file to apply.</span></span> <span data-ttu-id="401d5-117">지정 하지 않으면 `%AppData%\NuGet\NuGet.Config` (Windows) 또는 `~/.nuget/NuGet/NuGet.Config` (Mac/Linux)가 사용 됩니다.</span><span class="sxs-lookup"><span data-stu-id="401d5-117">If not specified, `%AppData%\NuGet\NuGet.Config` (Windows) or `~/.nuget/NuGet/NuGet.Config` (Mac/Linux) is used.</span></span>|
| <span data-ttu-id="401d5-118">ForceEnglishOutput</span><span class="sxs-lookup"><span data-stu-id="401d5-118">ForceEnglishOutput</span></span> | <span data-ttu-id="401d5-119">*(3.5 +)*  고정, 영어 기반 문화권을 사용 하 여 실행할 nuget.exe를 강제로 수행 합니다.</span><span class="sxs-lookup"><span data-stu-id="401d5-119">*(3.5+)* Forces nuget.exe to run using an invariant, English-based culture.</span></span> |
| <span data-ttu-id="401d5-120">도움말</span><span class="sxs-lookup"><span data-stu-id="401d5-120">Help</span></span> | <span data-ttu-id="401d5-121">도움말의 명령에 대 한 정보를 표시 합니다.</span><span class="sxs-lookup"><span data-stu-id="401d5-121">Displays help information for the command.</span></span> |
| <span data-ttu-id="401d5-122">목록</span><span class="sxs-lookup"><span data-stu-id="401d5-122">List</span></span> | <span data-ttu-id="401d5-123">지정된 된 폴더의 위치 또는 함께 사용할 경우 모든 폴더의 위치 나열 *모든*합니다.</span><span class="sxs-lookup"><span data-stu-id="401d5-123">Lists the location of the specified folder, or the locations of all folders when used with *all*.</span></span> |
| <span data-ttu-id="401d5-124">NonInteractive</span><span class="sxs-lookup"><span data-stu-id="401d5-124">NonInteractive</span></span> | <span data-ttu-id="401d5-125">사용자 입력 또는 확인에 대 한 프롬프트를 표시 하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="401d5-125">Suppresses prompts for user input or confirmations.</span></span> |
| <span data-ttu-id="401d5-126">자세한 정도</span><span class="sxs-lookup"><span data-stu-id="401d5-126">Verbosity</span></span> | <span data-ttu-id="401d5-127">출력에 표시 되는 세부 정보 수준을 지정: *일반*, *quiet*, *자세한*합니다.</span><span class="sxs-lookup"><span data-stu-id="401d5-127">Specifies the amount of detail displayed in the output: *normal*, *quiet*, *detailed*.</span></span> |

<span data-ttu-id="401d5-128">또한 참조 [환경 변수](cli-ref-environment-variables.md)</span><span class="sxs-lookup"><span data-stu-id="401d5-128">Also see [Environment variables](cli-ref-environment-variables.md)</span></span>

## <a name="examples"></a><span data-ttu-id="401d5-129">예제</span><span class="sxs-lookup"><span data-stu-id="401d5-129">Examples</span></span>

```cli
nuget locals all -list
nuget locals http-cache -clear
```

<span data-ttu-id="401d5-130">추가 예제를 참조 하십시오. [전역 패키지 및 캐시 폴더 관리](../consume-packages/managing-the-global-packages-and-cache-folders.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="401d5-130">For additional examples, see [Managing the global packages and cache folders](../consume-packages/managing-the-global-packages-and-cache-folders.md).</span></span>
