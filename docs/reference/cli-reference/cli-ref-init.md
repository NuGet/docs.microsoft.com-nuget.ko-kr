---
title: NuGet CLI init 명령
description: nuget.exe init 명령에 대 한 참조
author: karann-msft
ms.author: karann
ms.date: 01/18/2018
ms.topic: reference
ms.openlocfilehash: 3b830d678a473c917b70bd46900bdb0206d3652e
ms.sourcegitcommit: cbc87fe51330cdd3eacaad3e8656eb4258882fc7
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/19/2020
ms.locfileid: "88623086"
---
# <a name="init-command-nuget-cli"></a><span data-ttu-id="67844-103">init 명령 (NuGet CLI)</span><span class="sxs-lookup"><span data-stu-id="67844-103">init command (NuGet CLI)</span></span>

<span data-ttu-id="67844-104">**적용 대상:** 패키지 만들기 &bullet; **지원 되는 버전:** 3.3 이상</span><span class="sxs-lookup"><span data-stu-id="67844-104">**Applies to:** package creation &bullet; **Supported versions:** 3.3+</span></span>

<span data-ttu-id="67844-105">[추가 명령](cli-ref-add.md)에 설명 된 대로 계층적 레이아웃을 사용 하 여 플랫 폴더의 모든 패키지를 대상 폴더에 복사 합니다.</span><span class="sxs-lookup"><span data-stu-id="67844-105">Copies all the packages from a flat folder to a destination folder using a hierarchical layout as described for the [add command](cli-ref-add.md).</span></span> <span data-ttu-id="67844-106">즉,를 사용 하는 것 `init` 은 `add` 폴더의 각 패키지에 대해 명령을 사용 하는 것과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="67844-106">That is, using `init` is equivalent to using the `add` command on each package in the folder.</span></span>

<span data-ttu-id="67844-107">와 마찬가지로 `add` 대상은 로컬 폴더 또는 UNC 경로 여야 합니다. Nuget.org 또는 private 서버와 같은 HTTP 패키지 리포지토리는 지원 되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="67844-107">As with `add`, the destination must be either a local folder or a UNC path; HTTP package repositories such as nuget.org or private servers are not supported.</span></span>

## <a name="usage"></a><span data-ttu-id="67844-108">사용량</span><span class="sxs-lookup"><span data-stu-id="67844-108">Usage</span></span>

```cli
nuget init <source> <destination> [options]
```

<span data-ttu-id="67844-109">여기서 `<source>` 는 패키지가 포함 된 폴더이 고 `<destination>` 은 패키지가 복사 되는 로컬 폴더 또는 UNC 경로 이름입니다.</span><span class="sxs-lookup"><span data-stu-id="67844-109">where `<source>` is the folder containing packages and `<destination>` is the local folder or UNC pathname to which the packages are copied.</span></span>

## <a name="options"></a><span data-ttu-id="67844-110">옵션</span><span class="sxs-lookup"><span data-stu-id="67844-110">Options</span></span>

- **`-ConfigFile`**

  <span data-ttu-id="67844-111">적용할 NuGet 구성 파일입니다.</span><span class="sxs-lookup"><span data-stu-id="67844-111">The NuGet configuration file to apply.</span></span> <span data-ttu-id="67844-112">지정 하지 않으면 `%AppData%\NuGet\NuGet.Config` (Windows) 또는 `~/.nuget/NuGet/NuGet.Config` 또는 `~/.config/NuGet/NuGet.Config` (Mac/Linux)가 사용 됩니다.</span><span class="sxs-lookup"><span data-stu-id="67844-112">If not specified, `%AppData%\NuGet\NuGet.Config` (Windows), or `~/.nuget/NuGet/NuGet.Config` or `~/.config/NuGet/NuGet.Config` (Mac/Linux) is used.</span></span>

- **`-Expand`**

  <span data-ttu-id="67844-113">패키지 소스에 추가 된 각 패키지의 모든 파일을 추가 합니다. `-Expand` 명령을 사용 하는 것과 같습니다 `add` .</span><span class="sxs-lookup"><span data-stu-id="67844-113">Adds all files in each package that's added to the package source; same as `-Expand` with the `add` command.</span></span>

- **`-ForceEnglishOutput`**

  <span data-ttu-id="67844-114">*(3.5 +)* 고정 된 영어 기반 문화권을 사용 하 여 nuget.exe을 강제로 실행 합니다.</span><span class="sxs-lookup"><span data-stu-id="67844-114">*(3.5+)* Forces nuget.exe to run using an invariant, English-based culture.</span></span>

- **`-?|-help`**

  <span data-ttu-id="67844-115">명령에 대 한 도움말 정보를 표시 합니다.</span><span class="sxs-lookup"><span data-stu-id="67844-115">Displays help information for the command.</span></span>

- **`-NonInteractive`**

  <span data-ttu-id="67844-116">사용자 입력 또는 확인에 대 한 프롬프트를 표시 하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="67844-116">Suppresses prompts for user input or confirmations.</span></span>

- **`-Verbosity [normal|quiet|detailed]`**

  <span data-ttu-id="67844-117">출력에 표시 되는 세부 정보의 양을 지정 합니다. `normal` (기본값), `quiet` 또는 `detailed` 입니다.</span><span class="sxs-lookup"><span data-stu-id="67844-117">Specifies the amount of detail displayed in the output: `normal` (the default), `quiet`, or `detailed`.</span></span>

<span data-ttu-id="67844-118">[환경 변수](cli-ref-environment-variables.md) 참조</span><span class="sxs-lookup"><span data-stu-id="67844-118">Also see [Environment variables](cli-ref-environment-variables.md)</span></span>

## <a name="examples"></a><span data-ttu-id="67844-119">예</span><span class="sxs-lookup"><span data-stu-id="67844-119">Examples</span></span>

```cli
nuget init c:\foo c:\bar
nuget init \\foo\packages \\bar\packages -Expand
```
