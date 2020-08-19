---
title: NuGet CLI 사양 명령
description: nuget.exe spec 명령에 대 한 참조
author: karann-msft
ms.author: karann
ms.date: 01/18/2018
ms.topic: reference
ms.openlocfilehash: 17603fa30a75c7906f867c96c5d77f31732eaa59
ms.sourcegitcommit: cbc87fe51330cdd3eacaad3e8656eb4258882fc7
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/19/2020
ms.locfileid: "88622566"
---
# <a name="spec-command-nuget-cli"></a><span data-ttu-id="119f7-103">spec 명령 (NuGet CLI)</span><span class="sxs-lookup"><span data-stu-id="119f7-103">spec command (NuGet CLI)</span></span>

<span data-ttu-id="119f7-104">**적용 대상:** 패키지 만들기 &bullet; **지원 되는 버전:** 모두</span><span class="sxs-lookup"><span data-stu-id="119f7-104">**Applies to:** package creation &bullet; **Supported versions:** all</span></span>

<span data-ttu-id="119f7-105">`.nuspec`새 패키지에 대 한 파일을 생성 합니다.</span><span class="sxs-lookup"><span data-stu-id="119f7-105">Generates a `.nuspec` file for a new package.</span></span> <span data-ttu-id="119f7-106">프로젝트 파일 (,,)과 동일한 폴더에서 실행 `.csproj` 되는 경우 `.vbproj` `.fsproj` `spec` 토큰화 된 파일을 만듭니다 `.nuspec` .</span><span class="sxs-lookup"><span data-stu-id="119f7-106">If run in the same folder as a project file (`.csproj`, `.vbproj`, `.fsproj`), `spec` creates a tokenized `.nuspec` file.</span></span> <span data-ttu-id="119f7-107">자세한 내용은 [패키지 만들기](../../create-packages/creating-a-package.md)를 참조 하세요.</span><span class="sxs-lookup"><span data-stu-id="119f7-107">For additional information, see [Creating a Package](../../create-packages/creating-a-package.md).</span></span>

## <a name="usage"></a><span data-ttu-id="119f7-108">사용량</span><span class="sxs-lookup"><span data-stu-id="119f7-108">Usage</span></span>

```cli
nuget spec [<packageID>] [options]
```

<span data-ttu-id="119f7-109">여기서 `<packageID>` 은 파일에 저장할 선택적 패키지 식별자입니다 `.nuspec` .</span><span class="sxs-lookup"><span data-stu-id="119f7-109">where `<packageID>` is an optional package identifier to save in the `.nuspec` file.</span></span>

## <a name="options"></a><span data-ttu-id="119f7-110">옵션</span><span class="sxs-lookup"><span data-stu-id="119f7-110">Options</span></span>

- **`-AssemblyPath`**

  <span data-ttu-id="119f7-111">메타 데이터에 사용할 어셈블리의 경로를 지정 합니다.</span><span class="sxs-lookup"><span data-stu-id="119f7-111">Specifies the path to the assembly to use for metadata.</span></span>

- **`-Force`**

  <span data-ttu-id="119f7-112">기존 `.nuspec` 파일을 덮어씁니다.</span><span class="sxs-lookup"><span data-stu-id="119f7-112">Overwrites any existing `.nuspec` file.</span></span>


- **`-ForceEnglishOutput`**

  <span data-ttu-id="119f7-113">*(3.5 +)* 고정 된 영어 기반 문화권을 사용 하 여 nuget.exe을 강제로 실행 합니다.</span><span class="sxs-lookup"><span data-stu-id="119f7-113">*(3.5+)* Forces nuget.exe to run using an invariant, English-based culture.</span></span>

- **`-?|-help`**

  <span data-ttu-id="119f7-114">명령에 대 한 도움말 정보를 표시 합니다.</span><span class="sxs-lookup"><span data-stu-id="119f7-114">Displays help information for the command.</span></span>

- **`-NonInteractive`**

  <span data-ttu-id="119f7-115">사용자 입력 또는 확인에 대 한 프롬프트를 표시 하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="119f7-115">Suppresses prompts for user input or confirmations.</span></span>

- **`-Verbosity [normal|quiet|detailed]`**

  <span data-ttu-id="119f7-116">출력에 표시 되는 세부 정보의 양을 지정 합니다. `normal` (기본값), `quiet` 또는 `detailed` 입니다.</span><span class="sxs-lookup"><span data-stu-id="119f7-116">Specifies the amount of detail displayed in the output: `normal` (the default), `quiet`, or `detailed`.</span></span>

<span data-ttu-id="119f7-117">[환경 변수](cli-ref-environment-variables.md) 참조</span><span class="sxs-lookup"><span data-stu-id="119f7-117">Also see [Environment variables](cli-ref-environment-variables.md)</span></span>

## <a name="examples"></a><span data-ttu-id="119f7-118">예</span><span class="sxs-lookup"><span data-stu-id="119f7-118">Examples</span></span>

```cli
nuget spec

nuget spec MyPackage

nuget spec -AssemblyPath MyAssembly.dll
```
