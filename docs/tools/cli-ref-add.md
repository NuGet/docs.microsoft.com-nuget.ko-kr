---
title: NuGet CLI 명령 추가
description: Nuget.exe에 대 한 참조 추가 명령
author: karann-msft
ms.author: karann
ms.date: 01/18/2018
ms.topic: reference
ms.openlocfilehash: 7a72186e1dece082cd200a03849a0b12c751a645
ms.sourcegitcommit: 1d1406764c6af5fb7801d462e0c4afc9092fa569
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 09/04/2018
ms.locfileid: "43545836"
---
# <a name="add-command-nuget-cli"></a><span data-ttu-id="a6f7a-103">add 명령(NuGet CLI)</span><span class="sxs-lookup"><span data-stu-id="a6f7a-103">add command (NuGet CLI)</span></span>

<span data-ttu-id="a6f7a-104">**적용 대상**: 게시 패키지 &bullet; **지원 되는 버전**: 3.3 이상</span><span class="sxs-lookup"><span data-stu-id="a6f7a-104">**Applies to**: package publishing &bullet; **Supported versions**: 3.3+</span></span>

<span data-ttu-id="a6f7a-105">비 HTTP 패키지 원본 (폴더 또는 UNC 경로)에 패키지 ID와 버전 번호에 대 한 폴더가 만들어지고 여기서 계층형 레이아웃으로 지정 된 패키지를 추가 합니다.</span><span class="sxs-lookup"><span data-stu-id="a6f7a-105">Adds a specified package to a non-HTTP package source (a folder or UNC path) in a hierarchical layout, wherein folders are created for the package ID and version number.</span></span> <span data-ttu-id="a6f7a-106">예를 들어:</span><span class="sxs-lookup"><span data-stu-id="a6f7a-106">For example:</span></span>

    \\myserver\packages
      └─<packageID>
        └─<version>
          ├─<packageID>.<version>.nupkg
          ├─<packageID>.<version>.nupkg.sha512
          └─<packageID>.nuspec

<span data-ttu-id="a6f7a-107">복원 하거나 패키지 원본에 대 한 업데이트를 계층형 레이아웃 훨씬 더 나은 성능을 제공 합니다.</span><span class="sxs-lookup"><span data-stu-id="a6f7a-107">When restoring or updating against the package source, hierarchical layout provides significantly better performance.</span></span>

<span data-ttu-id="a6f7a-108">대상 패키지 원본에는 패키지의 모든 파일을 확장 하려면 사용 된 `-Expand` 전환 합니다.</span><span class="sxs-lookup"><span data-stu-id="a6f7a-108">To expand all the files in the package to the destination package source, use the `-Expand` switch.</span></span> <span data-ttu-id="a6f7a-109">일반적으로 이렇게 추가 하위 폴더와 같은 대상에 나타나는 `tools` 고 `lib`입니다.</span><span class="sxs-lookup"><span data-stu-id="a6f7a-109">This typically results in additional subfolders appearing in the destination, such as `tools` and `lib`.</span></span>

## <a name="usage"></a><span data-ttu-id="a6f7a-110">사용법</span><span class="sxs-lookup"><span data-stu-id="a6f7a-110">Usage</span></span>

```cli
nuget add <packagePath> -Source <sourcePath> [options]
```

<span data-ttu-id="a6f7a-111">여기서 `<packagePath>` 에 추가 하려면 패키지에 경로 이름 및 `<sourcePath>` 패키지를 추가할 폴더 기반 패키지 원본을 지정 합니다.</span><span class="sxs-lookup"><span data-stu-id="a6f7a-111">where `<packagePath>` is the pathname to the package to add, and `<sourcePath>` specifies the folder-based package source to which the package will be added.</span></span> <span data-ttu-id="a6f7a-112">HTTP 소스는 지원 되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="a6f7a-112">HTTP sources are not supported.</span></span>

## <a name="options"></a><span data-ttu-id="a6f7a-113">옵션</span><span class="sxs-lookup"><span data-stu-id="a6f7a-113">Options</span></span>

| <span data-ttu-id="a6f7a-114">옵션</span><span class="sxs-lookup"><span data-stu-id="a6f7a-114">Option</span></span> | <span data-ttu-id="a6f7a-115">설명</span><span class="sxs-lookup"><span data-stu-id="a6f7a-115">Description</span></span> |
| --- | --- |
| <span data-ttu-id="a6f7a-116">ConfigFile</span><span class="sxs-lookup"><span data-stu-id="a6f7a-116">ConfigFile</span></span> | <span data-ttu-id="a6f7a-117">NuGet 구성 파일을 적용 합니다.</span><span class="sxs-lookup"><span data-stu-id="a6f7a-117">The NuGet configuration file to apply.</span></span> <span data-ttu-id="a6f7a-118">지정 하지 않으면 `%AppData%\NuGet\NuGet.Config` (Windows) 또는 `~/.nuget/NuGet/NuGet.Config` (Mac/Linux)가 사용 됩니다.</span><span class="sxs-lookup"><span data-stu-id="a6f7a-118">If not specified, `%AppData%\NuGet\NuGet.Config` (Windows) or `~/.nuget/NuGet/NuGet.Config` (Mac/Linux) is used.</span></span>|
| <span data-ttu-id="a6f7a-119">Expand</span><span class="sxs-lookup"><span data-stu-id="a6f7a-119">Expand</span></span> | <span data-ttu-id="a6f7a-120">패키지의 패키지 원본에 있는 모든 파일을 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="a6f7a-120">Adds all the files in the package to the package source.</span></span> |
| <span data-ttu-id="a6f7a-121">ForceEnglishOutput</span><span class="sxs-lookup"><span data-stu-id="a6f7a-121">ForceEnglishOutput</span></span> | <span data-ttu-id="a6f7a-122">*(3.5 이상)*  고정 영어 기반 문화권을 사용 하 여 실행할 nuget.exe를 강제로 수행 합니다.</span><span class="sxs-lookup"><span data-stu-id="a6f7a-122">*(3.5+)* Forces nuget.exe to run using an invariant, English-based culture.</span></span> |
| <span data-ttu-id="a6f7a-123">도움말</span><span class="sxs-lookup"><span data-stu-id="a6f7a-123">Help</span></span> | <span data-ttu-id="a6f7a-124">도움말의 명령에 대 한 정보를 표시 합니다.</span><span class="sxs-lookup"><span data-stu-id="a6f7a-124">Displays help information for the command.</span></span> |
| <span data-ttu-id="a6f7a-125">NonInteractive</span><span class="sxs-lookup"><span data-stu-id="a6f7a-125">NonInteractive</span></span> | <span data-ttu-id="a6f7a-126">사용자 입력 또는 확인에 대 한 프롬프트를 표시 하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="a6f7a-126">Suppresses prompts for user input or confirmations.</span></span> |
| <span data-ttu-id="a6f7a-127">자세한 정도</span><span class="sxs-lookup"><span data-stu-id="a6f7a-127">Verbosity</span></span> | <span data-ttu-id="a6f7a-128">출력에 표시 되는 세부 정보의 양을 지정: *정상적인*, *quiet*, *자세한*합니다.</span><span class="sxs-lookup"><span data-stu-id="a6f7a-128">Specifies the amount of detail displayed in the output: *normal*, *quiet*, *detailed*.</span></span> |

<span data-ttu-id="a6f7a-129">또한 참조 [환경 변수](cli-ref-environment-variables.md)</span><span class="sxs-lookup"><span data-stu-id="a6f7a-129">Also see [Environment variables](cli-ref-environment-variables.md)</span></span>

## <a name="examples"></a><span data-ttu-id="a6f7a-130">예제</span><span class="sxs-lookup"><span data-stu-id="a6f7a-130">Examples</span></span>

```cli
nuget add foo.nupkg -Source c:\bar\

nuget add foo.nupkg -Source \\bar\packages\
```
