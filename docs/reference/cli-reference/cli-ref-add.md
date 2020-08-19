---
title: NuGet CLI add 명령
description: nuget.exe add 명령에 대 한 참조
author: karann-msft
ms.author: karann
ms.date: 01/18/2018
ms.topic: reference
ms.openlocfilehash: 89d268946243e8eae07e482db48e809a15260c38
ms.sourcegitcommit: cbc87fe51330cdd3eacaad3e8656eb4258882fc7
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/19/2020
ms.locfileid: "88622904"
---
# <a name="add-command-nuget-cli"></a><span data-ttu-id="a6a2a-103">add 명령 (NuGet CLI)</span><span class="sxs-lookup"><span data-stu-id="a6a2a-103">add command (NuGet CLI)</span></span>

<span data-ttu-id="a6a2a-104">**적용 대상**: 패키지 게시 &bullet; **지원 버전**: 3.3 이상</span><span class="sxs-lookup"><span data-stu-id="a6a2a-104">**Applies to**: package publishing &bullet; **Supported versions**: 3.3+</span></span>

<span data-ttu-id="a6a2a-105">패키지 ID 및 버전 번호에 대 한 폴더를 만드는 계층적 레이아웃에서 HTTP가 아닌 패키지 원본 (폴더 또는 UNC 경로)에 지정 된 패키지를 추가 합니다.</span><span class="sxs-lookup"><span data-stu-id="a6a2a-105">Adds a specified package to a non-HTTP package source (a folder or UNC path) in a hierarchical layout, wherein folders are created for the package ID and version number.</span></span> <span data-ttu-id="a6a2a-106">다음은 그 예입니다. </span><span class="sxs-lookup"><span data-stu-id="a6a2a-106">For example:</span></span>

```
\\myserver\packages
  └─<packageID>
    └─<version>
      ├─<packageID>.<version>.nupkg
      ├─<packageID>.<version>.nupkg.sha512
      └─<packageID>.nuspec
```

<span data-ttu-id="a6a2a-107">패키지 원본에 대해 복원 하거나 업데이트 하는 경우 계층적 레이아웃을 통해 성능이 크게 향상 됩니다.</span><span class="sxs-lookup"><span data-stu-id="a6a2a-107">When restoring or updating against the package source, hierarchical layout provides significantly better performance.</span></span>

<span data-ttu-id="a6a2a-108">패키지의 모든 파일을 대상 패키지 원본으로 확장 하려면 스위치를 사용 `-Expand` 합니다.</span><span class="sxs-lookup"><span data-stu-id="a6a2a-108">To expand all the files in the package to the destination package source, use the `-Expand` switch.</span></span> <span data-ttu-id="a6a2a-109">이 경우 일반적으로 및와 같은 추가 하위 폴더가 대상에 나타납니다 `tools` `lib` .</span><span class="sxs-lookup"><span data-stu-id="a6a2a-109">This typically results in additional subfolders appearing in the destination, such as `tools` and `lib`.</span></span>

## <a name="usage"></a><span data-ttu-id="a6a2a-110">사용량</span><span class="sxs-lookup"><span data-stu-id="a6a2a-110">Usage</span></span>

```cli
nuget add <packagePath> -Source <sourcePath> [options]
```

<span data-ttu-id="a6a2a-111">여기서 `<packagePath>` 는 추가할 패키지의 경로 이름 이며,는 `<sourcePath>` 패키지를 추가할 폴더 기반 패키지 원본을 지정 합니다.</span><span class="sxs-lookup"><span data-stu-id="a6a2a-111">where `<packagePath>` is the pathname to the package to add, and `<sourcePath>` specifies the folder-based package source to which the package will be added.</span></span> <span data-ttu-id="a6a2a-112">HTTP 원본은 지원 되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="a6a2a-112">HTTP sources are not supported.</span></span>

## <a name="options"></a><span data-ttu-id="a6a2a-113">옵션</span><span class="sxs-lookup"><span data-stu-id="a6a2a-113">Options</span></span>

- **`-ConfigFile`**

  <span data-ttu-id="a6a2a-114">적용할 NuGet 구성 파일입니다.</span><span class="sxs-lookup"><span data-stu-id="a6a2a-114">The NuGet configuration file to apply.</span></span> <span data-ttu-id="a6a2a-115">지정 하지 않으면 `%AppData%\NuGet\NuGet.Config` (Windows) 또는 `~/.nuget/NuGet/NuGet.Config` 또는 `~/.config/NuGet/NuGet.Config` (Mac/Linux)가 사용 됩니다.</span><span class="sxs-lookup"><span data-stu-id="a6a2a-115">If not specified, `%AppData%\NuGet\NuGet.Config` (Windows), or `~/.nuget/NuGet/NuGet.Config` or `~/.config/NuGet/NuGet.Config` (Mac/Linux) is used.</span></span>

- **`-Expand`**

  <span data-ttu-id="a6a2a-116">패키지 소스에 패키지의 모든 파일을 추가 합니다.</span><span class="sxs-lookup"><span data-stu-id="a6a2a-116">Adds all the files in the package to the package source.</span></span>

- **`-ForceEnglishOutput`**

  <span data-ttu-id="a6a2a-117">*(3.5 +)* 고정 된 영어 기반 문화권을 사용 하 여 nuget.exe을 강제로 실행 합니다.</span><span class="sxs-lookup"><span data-stu-id="a6a2a-117">*(3.5+)* Forces nuget.exe to run using an invariant, English-based culture.</span></span>
<span data-ttu-id="a6a2a-118">고정 된 영어 기반 문화권을 사용 하 여 nuget.exe을 강제로 실행 합니다.</span><span class="sxs-lookup"><span data-stu-id="a6a2a-118">Forces nuget.exe to run using an invariant, English-based culture.</span></span>

- **`-?|-help`**

  <span data-ttu-id="a6a2a-119">명령에 대 한 도움말 정보를 표시 합니다.</span><span class="sxs-lookup"><span data-stu-id="a6a2a-119">Displays help information for the command.</span></span>

- **`-NonInteractive`**

  <span data-ttu-id="a6a2a-120">사용자 입력 또는 확인에 대 한 프롬프트를 표시 하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="a6a2a-120">Suppresses prompts for user input or confirmations.</span></span>

- **`-src|-Source`**

   <span data-ttu-id="a6a2a-121">Nupkg이 추가 될 폴더 또는 UNC 공유 인 패키지 원본을 지정 합니다.</span><span class="sxs-lookup"><span data-stu-id="a6a2a-121">Specifies the package source, which is a folder or UNC share, to which the nupkg will be added.</span></span> <span data-ttu-id="a6a2a-122">Http 원본은 지원 되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="a6a2a-122">Http sources are not supported.</span></span>

- **`-Verbosity [normal|quiet|detailed]`**

  <span data-ttu-id="a6a2a-123">출력에 표시 되는 세부 정보의 양을 지정 합니다. `normal` (기본값), `quiet` 또는 `detailed` 입니다.</span><span class="sxs-lookup"><span data-stu-id="a6a2a-123">Specifies the amount of detail displayed in the output: `normal` (the default), `quiet`, or `detailed`.</span></span>

<span data-ttu-id="a6a2a-124">[환경 변수](cli-ref-environment-variables.md) 참조</span><span class="sxs-lookup"><span data-stu-id="a6a2a-124">Also see [Environment variables](cli-ref-environment-variables.md)</span></span>

## <a name="examples"></a><span data-ttu-id="a6a2a-125">예</span><span class="sxs-lookup"><span data-stu-id="a6a2a-125">Examples</span></span>

```cli
nuget add foo.nupkg -Source c:\bar\

nuget add foo.nupkg -Source \\bar\packages\
```
