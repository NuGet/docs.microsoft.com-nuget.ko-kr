---
title: NuGet CLI 사양 명령
description: Nuget.exe 사양 명령에 대 한 참조
author: kraigb
ms.author: kraigb
manager: douge
ms.date: 01/18/2018
ms.topic: reference
ms.openlocfilehash: 68d661030ce7bcff7d7a3a1c96c07e149ad4ffea
ms.sourcegitcommit: 3eab9c4dd41ea7ccd2c28bb5ab16f6fbbec13708
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/26/2018
---
# <a name="spec-command-nuget-cli"></a><span data-ttu-id="34f35-103">명령 (NuGet CLI) 사양</span><span class="sxs-lookup"><span data-stu-id="34f35-103">spec command (NuGet CLI)</span></span>

<span data-ttu-id="34f35-104">**적용 대상:** 패키지 만들기가 &bullet; **지원 되는 버전:** 모든</span><span class="sxs-lookup"><span data-stu-id="34f35-104">**Applies to:** package creation &bullet; **Supported versions:** all</span></span>

<span data-ttu-id="34f35-105">생성 된 `.nuspec` 새 패키지에 대 한 파일입니다.</span><span class="sxs-lookup"><span data-stu-id="34f35-105">Generates a `.nuspec` file for a new package.</span></span> <span data-ttu-id="34f35-106">프로젝트 파일을 같은 폴더에서 실행 되는 경우 (`.csproj`, `.vbproj`, `.fsproj`), `spec` 만듭니다는 토큰화 된 `.nuspec` 파일입니다.</span><span class="sxs-lookup"><span data-stu-id="34f35-106">If run in the same folder as a project file (`.csproj`, `.vbproj`, `.fsproj`), `spec` creates a tokenized `.nuspec` file.</span></span> <span data-ttu-id="34f35-107">자세한 내용은 참조 하십시오. [패키지를 만드는](../create-packages/creating-a-package.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="34f35-107">For additional information, see [Creating a Package](../create-packages/creating-a-package.md).</span></span>

## <a name="usage"></a><span data-ttu-id="34f35-108">사용법</span><span class="sxs-lookup"><span data-stu-id="34f35-108">Usage</span></span>

```cli
nuget spec [<packageID>] [options]
```

<span data-ttu-id="34f35-109">여기서 `<packageID>` 에 저장 하는 선택적 패키지 식별자는 `.nuspec` 파일입니다.</span><span class="sxs-lookup"><span data-stu-id="34f35-109">where `<packageID>` is an optional package identifier to save in the `.nuspec` file.</span></span>

## <a name="options"></a><span data-ttu-id="34f35-110">옵션</span><span class="sxs-lookup"><span data-stu-id="34f35-110">Options</span></span>

| <span data-ttu-id="34f35-111">옵션</span><span class="sxs-lookup"><span data-stu-id="34f35-111">Option</span></span> | <span data-ttu-id="34f35-112">설명</span><span class="sxs-lookup"><span data-stu-id="34f35-112">Description</span></span> |
| --- | --- |
| <span data-ttu-id="34f35-113">AssemblyPath</span><span class="sxs-lookup"><span data-stu-id="34f35-113">AssemblyPath</span></span> | <span data-ttu-id="34f35-114">메타 데이터에 사용할 어셈블리의 경로를 지정 합니다.</span><span class="sxs-lookup"><span data-stu-id="34f35-114">Specifies the path to the assembly to use for metadata.</span></span> |
| <span data-ttu-id="34f35-115">강제</span><span class="sxs-lookup"><span data-stu-id="34f35-115">Force</span></span> | <span data-ttu-id="34f35-116">모든 기존 덮어씁니다 `.nuspec` 파일입니다.</span><span class="sxs-lookup"><span data-stu-id="34f35-116">Overwrites any existing `.nuspec` file.</span></span> |
| <span data-ttu-id="34f35-117">ForceEnglishOutput</span><span class="sxs-lookup"><span data-stu-id="34f35-117">ForceEnglishOutput</span></span> | <span data-ttu-id="34f35-118">*(3.5 +)*  고정, 영어 기반 문화권을 사용 하 여 실행할 nuget.exe를 강제로 수행 합니다.</span><span class="sxs-lookup"><span data-stu-id="34f35-118">*(3.5+)* Forces nuget.exe to run using an invariant, English-based culture.</span></span> |
| <span data-ttu-id="34f35-119">도움말</span><span class="sxs-lookup"><span data-stu-id="34f35-119">Help</span></span> | <span data-ttu-id="34f35-120">도움말의 명령에 대 한 정보를 표시 합니다.</span><span class="sxs-lookup"><span data-stu-id="34f35-120">Displays help information for the command.</span></span> |
| <span data-ttu-id="34f35-121">비 대화형</span><span class="sxs-lookup"><span data-stu-id="34f35-121">NonInteractive</span></span> | <span data-ttu-id="34f35-122">사용자 입력 또는 확인에 대 한 프롬프트를 표시 하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="34f35-122">Suppresses prompts for user input or confirmations.</span></span> |
| <span data-ttu-id="34f35-123">자세한 정도</span><span class="sxs-lookup"><span data-stu-id="34f35-123">Verbosity</span></span> | <span data-ttu-id="34f35-124">출력에 표시 되는 세부 정보 수준을 지정: *일반*, *quiet*, *자세한*합니다.</span><span class="sxs-lookup"><span data-stu-id="34f35-124">Specifies the amount of detail displayed in the output: *normal*, *quiet*, *detailed*.</span></span> |

<span data-ttu-id="34f35-125">또한 참조 [환경 변수](cli-ref-environment-variables.md)</span><span class="sxs-lookup"><span data-stu-id="34f35-125">Also see [Environment variables](cli-ref-environment-variables.md)</span></span>

## <a name="examples"></a><span data-ttu-id="34f35-126">예제</span><span class="sxs-lookup"><span data-stu-id="34f35-126">Examples</span></span>

```cli
nuget spec

nuget spec MyPackage

nuget spec -a MyAssembly.dll
```
