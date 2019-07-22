---
title: NuGet CLI 사양 명령
description: Nuget.exe 사양 명령에 대 한 참조입니다.
author: karann-msft
ms.author: karann
ms.date: 01/18/2018
ms.topic: reference
ms.openlocfilehash: be6e4fdfe127d5582ecf9983a753a41e6760afe2
ms.sourcegitcommit: efc18d484fdf0c7a8979b564dcb191c030601bb4
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/18/2019
ms.locfileid: "68327570"
---
# <a name="spec-command-nuget-cli"></a><span data-ttu-id="ccbc0-103">spec 명령 (NuGet CLI)</span><span class="sxs-lookup"><span data-stu-id="ccbc0-103">spec command (NuGet CLI)</span></span>

<span data-ttu-id="ccbc0-104">**적용 대상:** 패키지 만들기 &bullet; **지원 되는 버전:** 모두</span><span class="sxs-lookup"><span data-stu-id="ccbc0-104">**Applies to:** package creation &bullet; **Supported versions:** all</span></span>

<span data-ttu-id="ccbc0-105">새 패키지 `.nuspec` 에 대 한 파일을 생성 합니다.</span><span class="sxs-lookup"><span data-stu-id="ccbc0-105">Generates a `.nuspec` file for a new package.</span></span> <span data-ttu-id="ccbc0-106">프로젝트`.csproj`파일 ( `.nuspec` , `.vbproj`, `.fsproj`)과 동일한 폴더에서 실행 되 `spec` 는 경우 토큰화 된 파일을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="ccbc0-106">If run in the same folder as a project file (`.csproj`, `.vbproj`, `.fsproj`), `spec` creates a tokenized `.nuspec` file.</span></span> <span data-ttu-id="ccbc0-107">자세한 내용은 [패키지 만들기](../../create-packages/creating-a-package.md)를 참조 하세요.</span><span class="sxs-lookup"><span data-stu-id="ccbc0-107">For additional information, see [Creating a Package](../../create-packages/creating-a-package.md).</span></span>

## <a name="usage"></a><span data-ttu-id="ccbc0-108">사용법</span><span class="sxs-lookup"><span data-stu-id="ccbc0-108">Usage</span></span>

```cli
nuget spec [<packageID>] [options]
```

<span data-ttu-id="ccbc0-109">여기서 `<packageID>` 은 `.nuspec` 파일에 저장할 선택적 패키지 식별자입니다.</span><span class="sxs-lookup"><span data-stu-id="ccbc0-109">where `<packageID>` is an optional package identifier to save in the `.nuspec` file.</span></span>

## <a name="options"></a><span data-ttu-id="ccbc0-110">변수</span><span class="sxs-lookup"><span data-stu-id="ccbc0-110">Options</span></span>

| <span data-ttu-id="ccbc0-111">옵션</span><span class="sxs-lookup"><span data-stu-id="ccbc0-111">Option</span></span> | <span data-ttu-id="ccbc0-112">Description</span><span class="sxs-lookup"><span data-stu-id="ccbc0-112">Description</span></span> |
| --- | --- |
| <span data-ttu-id="ccbc0-113">AssemblyPath</span><span class="sxs-lookup"><span data-stu-id="ccbc0-113">AssemblyPath</span></span> | <span data-ttu-id="ccbc0-114">메타 데이터에 사용할 어셈블리의 경로를 지정 합니다.</span><span class="sxs-lookup"><span data-stu-id="ccbc0-114">Specifies the path to the assembly to use for metadata.</span></span> |
| <span data-ttu-id="ccbc0-115">Force</span><span class="sxs-lookup"><span data-stu-id="ccbc0-115">Force</span></span> | <span data-ttu-id="ccbc0-116">기존 `.nuspec` 파일을 덮어씁니다.</span><span class="sxs-lookup"><span data-stu-id="ccbc0-116">Overwrites any existing `.nuspec` file.</span></span> |
| <span data-ttu-id="ccbc0-117">ForceEnglishOutput</span><span class="sxs-lookup"><span data-stu-id="ccbc0-117">ForceEnglishOutput</span></span> | <span data-ttu-id="ccbc0-118">*(3.5 이상)*  현재 언어 설정을 무시하고 영어를 기반으로 nuget.exe를 강제로 실행합니다.</span><span class="sxs-lookup"><span data-stu-id="ccbc0-118">*(3.5+)* Forces nuget.exe to run using an invariant, English-based culture.</span></span> |
| <span data-ttu-id="ccbc0-119">Help</span><span class="sxs-lookup"><span data-stu-id="ccbc0-119">Help</span></span> | <span data-ttu-id="ccbc0-120">명령어에 대한 도움말을 표시합니다.</span><span class="sxs-lookup"><span data-stu-id="ccbc0-120">Displays help information for the command.</span></span> |
| <span data-ttu-id="ccbc0-121">NonInteractive</span><span class="sxs-lookup"><span data-stu-id="ccbc0-121">NonInteractive</span></span> | <span data-ttu-id="ccbc0-122">사용자 입력이나 확인에 대한 프롬프트를 표시하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="ccbc0-122">Suppresses prompts for user input or confirmations.</span></span> |
| <span data-ttu-id="ccbc0-123">Verbosity</span><span class="sxs-lookup"><span data-stu-id="ccbc0-123">Verbosity</span></span> | <span data-ttu-id="ccbc0-124">출력에 표시되는 세부정보의 양을 지정합니다: *정상적인*, *조용한*, *자세한*합니다.</span><span class="sxs-lookup"><span data-stu-id="ccbc0-124">Specifies the amount of detail displayed in the output: *normal*, *quiet*, *detailed*.</span></span> |

<span data-ttu-id="ccbc0-125">또한 [환경 변수](cli-ref-environment-variables.md)에 대한 정보를 참조할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="ccbc0-125">Also see [Environment variables](cli-ref-environment-variables.md)</span></span>

## <a name="examples"></a><span data-ttu-id="ccbc0-126">예제</span><span class="sxs-lookup"><span data-stu-id="ccbc0-126">Examples</span></span>

```cli
nuget spec

nuget spec MyPackage

nuget spec -AssemblyPath MyAssembly.dll
```
