---
title: "NuGet CLI init 명령을 | Microsoft Docs"
author: kraigb
ms.author: kraigb
manager: ghogen
ms.date: 01/18/2018
ms.topic: reference
ms.prod: nuget
ms.technology: 
description: "Nuget.exe 초기화 명령에 대 한 참조"
keywords: "nuget init 참조, init 명령"
ms.reviewer:
- karann-msft
- unniravindranathan
ms.openlocfilehash: 6d7710cd024e2c2956fb73aa767c3be55b9fb0f9
ms.sourcegitcommit: 262d026beeffd4f3b6fc47d780a2f701451663a8
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 01/25/2018
---
# <a name="init-command-nuget-cli"></a><span data-ttu-id="69302-104">초기화 명령 (NuGet CLI)</span><span class="sxs-lookup"><span data-stu-id="69302-104">init command (NuGet CLI)</span></span>

<span data-ttu-id="69302-105">**적용 대상:** 패키지 만들기가 &bullet; **지원 되는 버전:** 3.3 +</span><span class="sxs-lookup"><span data-stu-id="69302-105">**Applies to:** package creation &bullet; **Supported versions:** 3.3+</span></span>

<span data-ttu-id="69302-106">에 대 한 설명 된 대로 계층 레이아웃을 사용 하 여 대상 폴더를 단일 폴더에서 모든 패키지를 복사는 [명령을 추가](cli-ref-add.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="69302-106">Copies all the packages from a flat folder to a destination folder using a hierarchical layout as described for the [add command](cli-ref-add.md).</span></span> <span data-ttu-id="69302-107">즉, 사용 하 여 `init` 사용 하는 `add` 폴더에 각 패키지에 명령 합니다.</span><span class="sxs-lookup"><span data-stu-id="69302-107">That is, using `init` is equivalent to using the `add` command on each package in the folder.</span></span>

<span data-ttu-id="69302-108">와 마찬가지로 `add`, 대상 로컬 폴더 또는 UNC 경로 여야 합니다 Nuget.org 또는 개인 서버와 같이 HTTP 패키지 저장소는 지원 되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="69302-108">As with `add`, the destination must be either a local folder or a UNC path; HTTP package repositories such as nuget.org or private servers are not supported.</span></span>

## <a name="usage"></a><span data-ttu-id="69302-109">사용법</span><span class="sxs-lookup"><span data-stu-id="69302-109">Usage</span></span>

```cli
nuget init <source> <destination> [options]
```

<span data-ttu-id="69302-110">여기서 `<source>` 는 패키지가 포함 된 폴더 및 `<destination>` 로컬 폴더 인지 패키지 복사 되는 UNC 경로 이름입니다.</span><span class="sxs-lookup"><span data-stu-id="69302-110">where `<source>` is the folder containing packages and `<destination>` is the local folder or UNC pathname to which the packages are copied.</span></span>

## <a name="options"></a><span data-ttu-id="69302-111">옵션</span><span class="sxs-lookup"><span data-stu-id="69302-111">Options</span></span>

| <span data-ttu-id="69302-112">옵션</span><span class="sxs-lookup"><span data-stu-id="69302-112">Option</span></span> | <span data-ttu-id="69302-113">설명</span><span class="sxs-lookup"><span data-stu-id="69302-113">Description</span></span> |
| --- | --- |
| <span data-ttu-id="69302-114">ConfigFile</span><span class="sxs-lookup"><span data-stu-id="69302-114">ConfigFile</span></span> | <span data-ttu-id="69302-115">적용할 NuGet 구성 파일입니다.</span><span class="sxs-lookup"><span data-stu-id="69302-115">The NuGet configuration file to apply.</span></span> <span data-ttu-id="69302-116">지정 하지 않으면 *%AppData%\NuGet\NuGet.Config* 사용 됩니다.</span><span class="sxs-lookup"><span data-stu-id="69302-116">If not specified, *%AppData%\NuGet\NuGet.Config* is used.</span></span> |
| <span data-ttu-id="69302-117">ForceEnglishOutput</span><span class="sxs-lookup"><span data-stu-id="69302-117">ForceEnglishOutput</span></span> | <span data-ttu-id="69302-118">*(3.5 +)*  고정, 영어 기반 문화권을 사용 하 여 실행할 nuget.exe를 강제로 수행 합니다.</span><span class="sxs-lookup"><span data-stu-id="69302-118">*(3.5+)* Forces nuget.exe to run using an invariant, English-based culture.</span></span> |
| <span data-ttu-id="69302-119">Expand</span><span class="sxs-lookup"><span data-stu-id="69302-119">Expand</span></span> | <span data-ttu-id="69302-120">모든 파일은 패키지 소스에 추가 된 각 패키지에 추가 와 동일 `-Expand` 와 `add` 명령입니다.</span><span class="sxs-lookup"><span data-stu-id="69302-120">Adds all files in each package that's added to the package source; same as `-Expand` with the `add` command.</span></span> |
| <span data-ttu-id="69302-121">도움말</span><span class="sxs-lookup"><span data-stu-id="69302-121">Help</span></span> | <span data-ttu-id="69302-122">도움말의 명령에 대 한 정보를 표시 합니다.</span><span class="sxs-lookup"><span data-stu-id="69302-122">Displays help information for the command.</span></span> |
| <span data-ttu-id="69302-123">NonInteractive</span><span class="sxs-lookup"><span data-stu-id="69302-123">NonInteractive</span></span> | <span data-ttu-id="69302-124">사용자 입력 또는 확인에 대 한 프롬프트를 표시 하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="69302-124">Suppresses prompts for user input or confirmations.</span></span> |
| <span data-ttu-id="69302-125">자세한 정도</span><span class="sxs-lookup"><span data-stu-id="69302-125">Verbosity</span></span> | <span data-ttu-id="69302-126">출력에 표시 되는 세부 정보 수준을 지정: *일반*, *quiet*, *자세한*합니다.</span><span class="sxs-lookup"><span data-stu-id="69302-126">Specifies the amount of detail displayed in the output: *normal*, *quiet*, *detailed*.</span></span> |

<span data-ttu-id="69302-127">또한 참조 [환경 변수](cli-ref-environment-variables.md)</span><span class="sxs-lookup"><span data-stu-id="69302-127">Also see [Environment variables](cli-ref-environment-variables.md)</span></span>

## <a name="examples"></a><span data-ttu-id="69302-128">예제</span><span class="sxs-lookup"><span data-stu-id="69302-128">Examples</span></span>

```cli
nuget init c:\foo c:\bar
nuget init \\foo\packages \\bar\packages -Expand
```
