---
title: "NuGet CLI 도움말 명령을 | Microsoft Docs"
author: kraigb
ms.author: kraigb
manager: ghogen
ms.date: 10/24/2017
ms.topic: reference
ms.prod: nuget
ms.technology: 
ms.assetid: 780d7f52-d6c6-45cd-8a62-218ff8c0b270
description: "Nuget.exe 도움말 명령에 대 한 참조"
keywords: "nuget 도움말 참조, 도움말 명령"
ms.reviewer:
- karann-msft
- unniravindranathan
ms.openlocfilehash: 55dc263fedd7ed5a3e48b76dbc9a3ccc220655cf
ms.sourcegitcommit: d0ba99bfe019b779b75731bafdca8a37e35ef0d9
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 12/14/2017
---
# <a name="help-or--command-nuget-cli"></a><span data-ttu-id="09aeb-104">도움말 또는?</span><span class="sxs-lookup"><span data-stu-id="09aeb-104">help or ?</span></span> <span data-ttu-id="09aeb-105">명령 (NuGet CLI)</span><span class="sxs-lookup"><span data-stu-id="09aeb-105">command (NuGet CLI)</span></span>

<span data-ttu-id="09aeb-106">**적용 대상:** 모든 &bullet; **지원 되는 버전**: 모든</span><span class="sxs-lookup"><span data-stu-id="09aeb-106">**Applies to:** all &bullet; **Supported versions**: all</span></span>

<span data-ttu-id="09aeb-107">일반 표시 도움말 정보 및 특정 명령에 대 한 정보를 지원 합니다.</span><span class="sxs-lookup"><span data-stu-id="09aeb-107">Displays general help information and help information about specific commands.</span></span>

## <a name="usage"></a><span data-ttu-id="09aeb-108">용도</span><span class="sxs-lookup"><span data-stu-id="09aeb-108">Usage</span></span>

```
nuget help [command] [options]
nuget ? [command] [options]
```

<span data-ttu-id="09aeb-109">여기서 [command] 도움말을 표시 하려는 특정 명령을 식별 합니다.</span><span class="sxs-lookup"><span data-stu-id="09aeb-109">where [command] identifies a specific command for which to display help.</span></span>

> [!Warning]
> <span data-ttu-id="09aeb-110">일부 명령으로 지정 하려면 주의 해야 *도움말* 와 함께으로 first `nuget help install`nuget.org에 "help" 라는 패키지 이므로, 합니다. 명령을 제공 하는 경우 `nuget install help`, 대신 도움말 라는 패키지를 설치 하지만 설치 명령을 한 도움말을 볼 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="09aeb-110">With some commands, be mindful to specify *help* first, as with `nuget help install`, because there is a package named "help" on nuget.org. If you give the command `nuget install help`, you'll not get help on the install command but will instead install the package named help.</span></span>

## <a name="options"></a><span data-ttu-id="09aeb-111">옵션</span><span class="sxs-lookup"><span data-stu-id="09aeb-111">Options</span></span>

| <span data-ttu-id="09aeb-112">옵션</span><span class="sxs-lookup"><span data-stu-id="09aeb-112">Option</span></span> | <span data-ttu-id="09aeb-113">설명</span><span class="sxs-lookup"><span data-stu-id="09aeb-113">Description</span></span> |
| --- | --- |
| <span data-ttu-id="09aeb-114">모두</span><span class="sxs-lookup"><span data-stu-id="09aeb-114">All</span></span> | <span data-ttu-id="09aeb-115">사용 가능한 모든 명령;에 대 한 자세한 도움말이 인쇄 특정 명령을 지정 하는 경우 무시 됩니다.</span><span class="sxs-lookup"><span data-stu-id="09aeb-115">Print detailed help for all available commands; ignored if a specific command is given.</span></span> |
| <span data-ttu-id="09aeb-116">ConfigFile</span><span class="sxs-lookup"><span data-stu-id="09aeb-116">ConfigFile</span></span> | <span data-ttu-id="09aeb-117">*(2.5 +)*  NuGet 구성 파일을 적용 합니다.</span><span class="sxs-lookup"><span data-stu-id="09aeb-117">*(2.5+)* The NuGet configuration file to apply.</span></span> <span data-ttu-id="09aeb-118">지정 하지 않으면 *%AppData%\NuGet\NuGet.Config* 사용 됩니다.</span><span class="sxs-lookup"><span data-stu-id="09aeb-118">If not specified, *%AppData%\NuGet\NuGet.Config* is used.</span></span> |
| <span data-ttu-id="09aeb-119">ForceEnglishOutput</span><span class="sxs-lookup"><span data-stu-id="09aeb-119">ForceEnglishOutput</span></span> | <span data-ttu-id="09aeb-120">*(3.5 +)*  고정, 영어 기반 문화권을 사용 하 여 실행할 nuget.exe를 강제로 수행 합니다.</span><span class="sxs-lookup"><span data-stu-id="09aeb-120">*(3.5+)* Forces nuget.exe to run using an invariant, English-based culture.</span></span> |
| <span data-ttu-id="09aeb-121">도움말</span><span class="sxs-lookup"><span data-stu-id="09aeb-121">Help</span></span> | <span data-ttu-id="09aeb-122">도움말 도움말 명령 자체에 대 한 정보를 표시 합니다.</span><span class="sxs-lookup"><span data-stu-id="09aeb-122">Displays help information for the help command itself.</span></span> |
| <span data-ttu-id="09aeb-123">Markdown</span><span class="sxs-lookup"><span data-stu-id="09aeb-123">Markdown</span></span> | <span data-ttu-id="09aeb-124">마크 다운 형태로 함께 사용할 경우 자세한 도움말을 인쇄 `-All`합니다.</span><span class="sxs-lookup"><span data-stu-id="09aeb-124">Print detailed help in markdown format when used with `-All`.</span></span> <span data-ttu-id="09aeb-125">그렇지 않은 경우 무시 됩니다.</span><span class="sxs-lookup"><span data-stu-id="09aeb-125">Ignored otherwise.</span></span> |
| <span data-ttu-id="09aeb-126">비 대화형</span><span class="sxs-lookup"><span data-stu-id="09aeb-126">NonInteractive</span></span> | <span data-ttu-id="09aeb-127">사용자 입력 또는 확인에 대 한 프롬프트를 표시 하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="09aeb-127">Suppresses prompts for user input or confirmations.</span></span> |
| <span data-ttu-id="09aeb-128">자세한 정도</span><span class="sxs-lookup"><span data-stu-id="09aeb-128">Verbosity</span></span> | <span data-ttu-id="09aeb-129">출력에 표시 되는 세부 정보 수준을 지정: *일반*, *quiet*, *세부 (2.5 이상)*합니다.</span><span class="sxs-lookup"><span data-stu-id="09aeb-129">Specifies the amount of detail displayed in the output: *normal*, *quiet*, *detailed (2.5+)*.</span></span> |

<span data-ttu-id="09aeb-130">또한 참조 [환경 변수](cli-ref-environment-variables.md)</span><span class="sxs-lookup"><span data-stu-id="09aeb-130">Also see [Environment variables](cli-ref-environment-variables.md)</span></span>

## <a name="examples"></a><span data-ttu-id="09aeb-131">예제</span><span class="sxs-lookup"><span data-stu-id="09aeb-131">Examples</span></span>

```
nuget help
nuget help push
nuget ?
nuget push -?
nuget help -All -Markdown
```
