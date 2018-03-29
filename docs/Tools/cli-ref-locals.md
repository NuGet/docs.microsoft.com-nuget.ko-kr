---
title: NuGet CLI 지역 명령을 | Microsoft Docs
author: kraigb
ms.author: kraigb
manager: ghogen
ms.date: 03/19/2018
ms.topic: reference
ms.prod: nuget
ms.technology: ''
description: Nuget.exe 지역 명령에 대 한 참조
keywords: nuget 지역 변수 참조, 지역 명령
ms.reviewer:
- karann-msft
- unniravindranathan
ms.workload:
- dotnet
- aspnet
ms.openlocfilehash: 0122c79e55b12838bd123cf91bfcbc5dbbd2a65c
ms.sourcegitcommit: beb229893559824e8abd6ab16707fd5fe1c6ac26
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 03/28/2018
---
# <a name="locals-command-nuget-cli"></a><span data-ttu-id="e6912-104">지역 명령 (NuGet CLI)</span><span class="sxs-lookup"><span data-stu-id="e6912-104">locals command (NuGet CLI)</span></span>

<span data-ttu-id="e6912-105">**적용 대상:** 소비 패키지 &bullet; **지원 되는 버전:** 3.3 +</span><span class="sxs-lookup"><span data-stu-id="e6912-105">**Applies to:** package consumption &bullet; **Supported versions:** 3.3+</span></span>

<span data-ttu-id="e6912-106">와 같은 로컬 NuGet 리소스를 나열 하거나 선택을 취소는 *http 캐시*, *전역 패키지* 폴더 및 임시 폴더입니다.</span><span class="sxs-lookup"><span data-stu-id="e6912-106">Clears or lists local NuGet resources such as the *http-cache*, *global-packages* folder, and the temp folder.</span></span> <span data-ttu-id="e6912-107">`locals` 해당 위치의 목록을 표시 하려면 명령을 사용할 수도 있습니다.</span><span class="sxs-lookup"><span data-stu-id="e6912-107">The `locals` command can also be used to display a list of those locations.</span></span> <span data-ttu-id="e6912-108">자세한 내용은 참조 [전역 패키지 및 캐시 폴더 관리](../consume-packages/managing-the-global-packages-and-cache-folders.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="e6912-108">For more information, see [Managing the global packages and cache folders](../consume-packages/managing-the-global-packages-and-cache-folders.md).</span></span>

## <a name="usage"></a><span data-ttu-id="e6912-109">사용법</span><span class="sxs-lookup"><span data-stu-id="e6912-109">Usage</span></span>

```cli
nuget locals <folder> [options]
```

<span data-ttu-id="e6912-110">여기서 `<folder>` 중 하나인 `all`, `http-cache`, `packages-cache` *(3.5 및 이전 버전)*, `global-packages`, 및 `temp` *(3.4 +)*합니다.</span><span class="sxs-lookup"><span data-stu-id="e6912-110">where `<folder>` is one of `all`, `http-cache`, `packages-cache` *(3.5 and earlier)*, `global-packages`, and `temp` *(3.4+)*.</span></span>

## <a name="options"></a><span data-ttu-id="e6912-111">옵션</span><span class="sxs-lookup"><span data-stu-id="e6912-111">Options</span></span>

| <span data-ttu-id="e6912-112">옵션</span><span class="sxs-lookup"><span data-stu-id="e6912-112">Option</span></span> | <span data-ttu-id="e6912-113">설명</span><span class="sxs-lookup"><span data-stu-id="e6912-113">Description</span></span> |
| --- | --- |
| <span data-ttu-id="e6912-114">지우기</span><span class="sxs-lookup"><span data-stu-id="e6912-114">Clear</span></span> | <span data-ttu-id="e6912-115">지정된 된 폴더를 지웁니다.</span><span class="sxs-lookup"><span data-stu-id="e6912-115">Clears the specified folder.</span></span> |
| <span data-ttu-id="e6912-116">ConfigFile</span><span class="sxs-lookup"><span data-stu-id="e6912-116">ConfigFile</span></span> | <span data-ttu-id="e6912-117">적용할 NuGet 구성 파일입니다.</span><span class="sxs-lookup"><span data-stu-id="e6912-117">The NuGet configuration file to apply.</span></span> <span data-ttu-id="e6912-118">지정 하지 않으면 `%AppData%\NuGet\NuGet.Config` (Windows) 또는 `~/.nuget/NuGet/NuGet.Config` (Mac/Linux)가 사용 됩니다.</span><span class="sxs-lookup"><span data-stu-id="e6912-118">If not specified, `%AppData%\NuGet\NuGet.Config` (Windows) or `~/.nuget/NuGet/NuGet.Config` (Mac/Linux) is used.</span></span>|
| <span data-ttu-id="e6912-119">ForceEnglishOutput</span><span class="sxs-lookup"><span data-stu-id="e6912-119">ForceEnglishOutput</span></span> | <span data-ttu-id="e6912-120">*(3.5 +)*  고정, 영어 기반 문화권을 사용 하 여 실행할 nuget.exe를 강제로 수행 합니다.</span><span class="sxs-lookup"><span data-stu-id="e6912-120">*(3.5+)* Forces nuget.exe to run using an invariant, English-based culture.</span></span> |
| <span data-ttu-id="e6912-121">도움말</span><span class="sxs-lookup"><span data-stu-id="e6912-121">Help</span></span> | <span data-ttu-id="e6912-122">도움말의 명령에 대 한 정보를 표시 합니다.</span><span class="sxs-lookup"><span data-stu-id="e6912-122">Displays help information for the command.</span></span> |
| <span data-ttu-id="e6912-123">목록</span><span class="sxs-lookup"><span data-stu-id="e6912-123">List</span></span> | <span data-ttu-id="e6912-124">지정된 된 폴더의 위치 또는 함께 사용할 경우 모든 폴더의 위치 나열 *모든*합니다.</span><span class="sxs-lookup"><span data-stu-id="e6912-124">Lists the location of the specified folder, or the locations of all folders when used with *all*.</span></span> |
| <span data-ttu-id="e6912-125">NonInteractive</span><span class="sxs-lookup"><span data-stu-id="e6912-125">NonInteractive</span></span> | <span data-ttu-id="e6912-126">사용자 입력 또는 확인에 대 한 프롬프트를 표시 하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="e6912-126">Suppresses prompts for user input or confirmations.</span></span> |
| <span data-ttu-id="e6912-127">자세한 정도</span><span class="sxs-lookup"><span data-stu-id="e6912-127">Verbosity</span></span> | <span data-ttu-id="e6912-128">출력에 표시 되는 세부 정보 수준을 지정: *일반*, *quiet*, *자세한*합니다.</span><span class="sxs-lookup"><span data-stu-id="e6912-128">Specifies the amount of detail displayed in the output: *normal*, *quiet*, *detailed*.</span></span> |

<span data-ttu-id="e6912-129">또한 참조 [환경 변수](cli-ref-environment-variables.md)</span><span class="sxs-lookup"><span data-stu-id="e6912-129">Also see [Environment variables](cli-ref-environment-variables.md)</span></span>

## <a name="examples"></a><span data-ttu-id="e6912-130">예제</span><span class="sxs-lookup"><span data-stu-id="e6912-130">Examples</span></span>

```cli
nuget locals all -list
nuget locals http-cache -clear
```

<span data-ttu-id="e6912-131">추가 예제를 참조 하십시오. [전역 패키지 및 캐시 폴더 관리](../consume-packages/managing-the-global-packages-and-cache-folders.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="e6912-131">For additional examples, see [Managing the global packages and cache folders](../consume-packages/managing-the-global-packages-and-cache-folders.md).</span></span>
