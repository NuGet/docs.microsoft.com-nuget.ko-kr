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
# <a name="add-command-nuget-cli"></a><span data-ttu-id="b1bba-103">add 명령(NuGet CLI)</span><span class="sxs-lookup"><span data-stu-id="b1bba-103">add command (NuGet CLI)</span></span>

<span data-ttu-id="b1bba-104">**적용 대상**: 게시 패키지 &bullet; **지원 되는 버전**: 3.3 이상</span><span class="sxs-lookup"><span data-stu-id="b1bba-104">**Applies to**: package publishing &bullet; **Supported versions**: 3.3+</span></span>

<span data-ttu-id="b1bba-105">특정한 패키지를 폴더나 UNC 경로와 같은 비 HTTP 패키지 소스에 패키지 이름과 버전 번호로 된 폴더 내부에 계층 레이아웃으로 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="b1bba-105">Adds a specified package to a non-HTTP package source (a folder or UNC path) in a hierarchical layout, wherein folders are created for the package ID and version number.</span></span> <span data-ttu-id="b1bba-106">예를 들어:</span><span class="sxs-lookup"><span data-stu-id="b1bba-106">For example:</span></span>

    \\myserver\packages
      └─<packageID>
        └─<version>
          ├─<packageID>.<version>.nupkg
          ├─<packageID>.<version>.nupkg.sha512
          └─<packageID>.nuspec

<span data-ttu-id="b1bba-107">해당 패키지에 대한 복원이나 업데이트를 할 때, 위와 같은 계층 레이아웃은 더 나은 성능을 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="b1bba-107">When restoring or updating against the package source, hierarchical layout provides significantly better performance.</span></span>

<span data-ttu-id="b1bba-108">원하는 패키지 소스 폴더 내부의 모든 파일을 확장하려면 `-Expand`를 사용하여 전환합니다.</span><span class="sxs-lookup"><span data-stu-id="b1bba-108">To expand all the files in the package to the destination package source, use the `-Expand` switch.</span></span> <span data-ttu-id="b1bba-109">일반적으로 `tools` 와 `lib`이라는 추가적인 하위폴더가 목적지 폴더 내부에 보일 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="b1bba-109">This typically results in additional subfolders appearing in the destination, such as `tools` and `lib`.</span></span>

## <a name="usage"></a><span data-ttu-id="b1bba-110">사용법</span><span class="sxs-lookup"><span data-stu-id="b1bba-110">Usage</span></span>

```cli
nuget add <packagePath> -Source <sourcePath> [options]
```

<span data-ttu-id="b1bba-111">여기서 `<packagePath>`는 추가하고자 하는 패키지의 위치를, `<sourcePath>`는 추가할 패키지 소스의 위치를 의미합니다.</span><span class="sxs-lookup"><span data-stu-id="b1bba-111">where `<packagePath>` is the pathname to the package to add, and `<sourcePath>` specifies the folder-based package source to which the package will be added.</span></span> <span data-ttu-id="b1bba-112">HTTP 소스는 지원되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="b1bba-112">HTTP sources are not supported.</span></span>

## <a name="options"></a><span data-ttu-id="b1bba-113">옵션</span><span class="sxs-lookup"><span data-stu-id="b1bba-113">Options</span></span>

| <span data-ttu-id="b1bba-114">옵션</span><span class="sxs-lookup"><span data-stu-id="b1bba-114">Option</span></span> | <span data-ttu-id="b1bba-115">설명</span><span class="sxs-lookup"><span data-stu-id="b1bba-115">Description</span></span> |
| --- | --- |
| <span data-ttu-id="b1bba-116">ConfigFile</span><span class="sxs-lookup"><span data-stu-id="b1bba-116">ConfigFile</span></span> | <span data-ttu-id="b1bba-117">적용할 NuGet 설정 파일입니다.</span><span class="sxs-lookup"><span data-stu-id="b1bba-117">The NuGet configuration file to apply.</span></span> <span data-ttu-id="b1bba-118">지정하지 않으면 기본적으로 Windows에서는 `%AppData%\NuGet\NuGet.Config`, Mac이나 Linux에서는 `~/.nuget/NuGet/NuGet.Config`가 사용됩니다.</span><span class="sxs-lookup"><span data-stu-id="b1bba-118">If not specified, `%AppData%\NuGet\NuGet.Config` (Windows) or `~/.nuget/NuGet/NuGet.Config` (Mac/Linux) is used.</span></span>|
| <span data-ttu-id="b1bba-119">Expand</span><span class="sxs-lookup"><span data-stu-id="b1bba-119">Expand</span></span> | <span data-ttu-id="b1bba-120">패키지의 원본에 있는 모든 파일을 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="b1bba-120">Adds all the files in the package to the package source.</span></span> |
| <span data-ttu-id="b1bba-121">ForceEnglishOutput</span><span class="sxs-lookup"><span data-stu-id="b1bba-121">ForceEnglishOutput</span></span> | <span data-ttu-id="b1bba-122">*(3.5 이상)*  현재 언어 설정을 무시하고 영어를 기반으로 nuget.exe를 강제로 실행합니다.</span><span class="sxs-lookup"><span data-stu-id="b1bba-122">*(3.5+)* Forces nuget.exe to run using an invariant, English-based culture.</span></span> |
| <span data-ttu-id="b1bba-123">도움말</span><span class="sxs-lookup"><span data-stu-id="b1bba-123">Help</span></span> | <span data-ttu-id="b1bba-124">명령어에 대한 도움말을 표시합니다.</span><span class="sxs-lookup"><span data-stu-id="b1bba-124">Displays help information for the command.</span></span> |
| <span data-ttu-id="b1bba-125">NonInteractive</span><span class="sxs-lookup"><span data-stu-id="b1bba-125">NonInteractive</span></span> | <span data-ttu-id="b1bba-126">사용자 입력이나 확인에 대한 프롬프트를 표시하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="b1bba-126">Suppresses prompts for user input or confirmations.</span></span> |
| <span data-ttu-id="b1bba-127">자세한 정도</span><span class="sxs-lookup"><span data-stu-id="b1bba-127">Verbosity</span></span> | <span data-ttu-id="b1bba-128">출력에 표시되는 세부정보의 양을 지정합니다: *정상적인*, *조용한*, *자세한*합니다.</span><span class="sxs-lookup"><span data-stu-id="b1bba-128">Specifies the amount of detail displayed in the output: *normal*, *quiet*, *detailed*.</span></span> |

<span data-ttu-id="b1bba-129">또한 참조 [환경 변수](cli-ref-environment-variables.md)</span><span class="sxs-lookup"><span data-stu-id="b1bba-129">Also see [Environment variables](cli-ref-environment-variables.md)</span></span>

## <a name="examples"></a><span data-ttu-id="b1bba-130">예제</span><span class="sxs-lookup"><span data-stu-id="b1bba-130">Examples</span></span>

```cli
nuget add foo.nupkg -Source c:\bar\

nuget add foo.nupkg -Source \\bar\packages\
```
