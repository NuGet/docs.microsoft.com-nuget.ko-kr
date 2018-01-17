---
title: "NuGet CLI 지역 명령을 | Microsoft Docs"
author: kraigb
ms.author: kraigb
manager: ghogen
ms.date: 10/24/2017
ms.topic: reference
ms.prod: nuget
ms.technology: 
ms.assetid: 7f672c7c-74c9-4296-bc27-4d47882b541c
description: "Nuget.exe 지역 명령에 대 한 참조"
keywords: "nuget 지역 변수 참조, 지역 명령"
ms.reviewer:
- karann-msft
- unniravindranathan
ms.openlocfilehash: 8cc06eedc20507e2bdd210e40c471ff551b89563
ms.sourcegitcommit: d0ba99bfe019b779b75731bafdca8a37e35ef0d9
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 12/14/2017
---
## <a name="locals-command-nuget-cli"></a><span data-ttu-id="25dd7-104">지역 명령 (NuGet CLI)</span><span class="sxs-lookup"><span data-stu-id="25dd7-104">locals command (NuGet CLI)</span></span>

<span data-ttu-id="25dd7-105">**적용 대상:** 소비 패키지 &bullet; **지원 되는 버전:** 3.3 +</span><span class="sxs-lookup"><span data-stu-id="25dd7-105">**Applies to:** package consumption &bullet; **Supported versions:** 3.3+</span></span>

<span data-ttu-id="25dd7-106">Http 요청 캐시, 패키지 캐시 및 시스템 수준의 글로벌 패키지 폴더와 같은 로컬 NuGet 리소스를 나열 하거나 선택을 취소 합니다.</span><span class="sxs-lookup"><span data-stu-id="25dd7-106">Clears or lists local NuGet resources such as the http-request cache, packages cache, and the machine-wide global packages folder.</span></span> <span data-ttu-id="25dd7-107">`locals` 해당 위치의 목록을 표시 하려면 명령을 사용할 수도 있습니다.</span><span class="sxs-lookup"><span data-stu-id="25dd7-107">The `locals` command can also be used to display a list of those locations.</span></span> <span data-ttu-id="25dd7-108">자세한 내용은 참조 [NuGet 캐시 관리](../consume-packages/managing-the-nuget-cache.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="25dd7-108">For more information, see [Managing the NuGet Cache](../consume-packages/managing-the-nuget-cache.md).</span></span>

## <a name="usage"></a><span data-ttu-id="25dd7-109">용도</span><span class="sxs-lookup"><span data-stu-id="25dd7-109">Usage</span></span>

```
nuget locals <cache> [options]
```

<span data-ttu-id="25dd7-110">여기서 `<cache>` 중 하나인 `all`, `http-cache`, `packages-cache`, `global-packages`, 및 `temp` *(3.4 +)*합니다.</span><span class="sxs-lookup"><span data-stu-id="25dd7-110">where `<cache>` is one of `all`, `http-cache`, `packages-cache`, `global-packages`, and `temp` *(3.4+)*.</span></span>

## <a name="options"></a><span data-ttu-id="25dd7-111">옵션</span><span class="sxs-lookup"><span data-stu-id="25dd7-111">Options</span></span>

| <span data-ttu-id="25dd7-112">옵션</span><span class="sxs-lookup"><span data-stu-id="25dd7-112">Option</span></span> | <span data-ttu-id="25dd7-113">설명</span><span class="sxs-lookup"><span data-stu-id="25dd7-113">Description</span></span> |
| --- | --- |
| <span data-ttu-id="25dd7-114">지우기</span><span class="sxs-lookup"><span data-stu-id="25dd7-114">Clear</span></span> | <span data-ttu-id="25dd7-115">지정된 된 캐시를 지웁니다.</span><span class="sxs-lookup"><span data-stu-id="25dd7-115">Clears the specified cache.</span></span> |
| <span data-ttu-id="25dd7-116">ConfigFile</span><span class="sxs-lookup"><span data-stu-id="25dd7-116">ConfigFile</span></span> | <span data-ttu-id="25dd7-117">적용할 NuGet 구성 파일입니다.</span><span class="sxs-lookup"><span data-stu-id="25dd7-117">The NuGet configuration file to apply.</span></span> <span data-ttu-id="25dd7-118">지정 하지 않으면 *%AppData%\NuGet\NuGet.Config* 사용 됩니다.</span><span class="sxs-lookup"><span data-stu-id="25dd7-118">If not specified, *%AppData%\NuGet\NuGet.Config* is used.</span></span> |
| <span data-ttu-id="25dd7-119">ForceEnglishOutput</span><span class="sxs-lookup"><span data-stu-id="25dd7-119">ForceEnglishOutput</span></span> | <span data-ttu-id="25dd7-120">*(3.5 +)*  고정, 영어 기반 문화권을 사용 하 여 실행할 nuget.exe를 강제로 수행 합니다.</span><span class="sxs-lookup"><span data-stu-id="25dd7-120">*(3.5+)* Forces nuget.exe to run using an invariant, English-based culture.</span></span> |
| <span data-ttu-id="25dd7-121">도움말</span><span class="sxs-lookup"><span data-stu-id="25dd7-121">Help</span></span> | <span data-ttu-id="25dd7-122">도움말의 명령에 대 한 정보를 표시 합니다.</span><span class="sxs-lookup"><span data-stu-id="25dd7-122">Displays help information for the command.</span></span> |
| <span data-ttu-id="25dd7-123">목록</span><span class="sxs-lookup"><span data-stu-id="25dd7-123">List</span></span> | <span data-ttu-id="25dd7-124">지정된 된 캐시의 위치 또는 함께 사용할 경우 모든 캐시의 위치 나열 *모든*합니다.</span><span class="sxs-lookup"><span data-stu-id="25dd7-124">Lists the location of the specified cache, or the locations of all caches when used with *all*.</span></span> |
| <span data-ttu-id="25dd7-125">비 대화형</span><span class="sxs-lookup"><span data-stu-id="25dd7-125">NonInteractive</span></span> | <span data-ttu-id="25dd7-126">사용자 입력 또는 확인에 대 한 프롬프트를 표시 하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="25dd7-126">Suppresses prompts for user input or confirmations.</span></span> |
| <span data-ttu-id="25dd7-127">자세한 정도</span><span class="sxs-lookup"><span data-stu-id="25dd7-127">Verbosity</span></span> | <span data-ttu-id="25dd7-128">출력에 표시 되는 세부 정보 수준을 지정: *일반*, *quiet*, *자세한*합니다.</span><span class="sxs-lookup"><span data-stu-id="25dd7-128">Specifies the amount of detail displayed in the output: *normal*, *quiet*, *detailed*.</span></span> |

<span data-ttu-id="25dd7-129">또한 참조 [환경 변수](cli-ref-environment-variables.md)</span><span class="sxs-lookup"><span data-stu-id="25dd7-129">Also see [Environment variables](cli-ref-environment-variables.md)</span></span>

## <a name="examples"></a><span data-ttu-id="25dd7-130">예제</span><span class="sxs-lookup"><span data-stu-id="25dd7-130">Examples</span></span>

```
nuget locals all -list
nuget locals http-cache -clear
```