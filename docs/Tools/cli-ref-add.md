---
title: "NuGet CLI 명령을 추가 | Microsoft Docs"
author: kraigb
ms.author: kraigb
manager: ghogen
ms.date: 10/24/2017
ms.topic: reference
ms.prod: nuget
ms.technology: 
ms.assetid: 4f68a016-ad4e-41fc-b869-88910fc5121e
description: "nuget.exe에 대 한 참조 추가 명령"
keywords: "nuget 참조를 추가, 패키지 명령 추가"
ms.reviewer:
- karann-msft
- unniravindranathan
ms.openlocfilehash: bf9a6e51dfbf1716ba40273487b76ae04c18e948
ms.sourcegitcommit: d0ba99bfe019b779b75731bafdca8a37e35ef0d9
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 12/14/2017
---
# <a name="add-command-nuget-cli"></a><span data-ttu-id="25936-104">명령 (NuGet CLI)를 추가 합니다.</span><span class="sxs-lookup"><span data-stu-id="25936-104">add command (NuGet CLI)</span></span>

<span data-ttu-id="25936-105">**적용 대상**: 게시 패키지 &bullet; **지원 되는 버전**: 3.3 +</span><span class="sxs-lookup"><span data-stu-id="25936-105">**Applies to**: package publishing &bullet; **Supported versions**: 3.3+</span></span>

<span data-ttu-id="25936-106">패키지 ID 및 버전 번호에 대 한 폴더가 만들어지고 여기서 계층적 레이아웃에서 HTTP가 아닌 패키지 소스 (폴더 또는 UNC 경로)에 지정 된 패키지를 추가 합니다.</span><span class="sxs-lookup"><span data-stu-id="25936-106">Adds a specified package to a non-HTTP package source (a folder or UNC path) in a hierarchical layout, wherein folders are created for the package ID and version number.</span></span> <span data-ttu-id="25936-107">예:</span><span class="sxs-lookup"><span data-stu-id="25936-107">For example:</span></span>

    \\myserver\packages
      └─<packageID>
        └─<version>
          ├─<packageID>.<version>.nupkg
          ├─<packageID>.<version>.nupkg.sha512
          └─<packageID>.nuspec

<span data-ttu-id="25936-108">을 복원 하거나 패키지 소스에 대해 업데이트 하는 경우 계층 레이아웃 훨씬 더 나은 성능을 제공 합니다.</span><span class="sxs-lookup"><span data-stu-id="25936-108">When restoring or updating against the package source, hierarchical layout provides significantly better performance.</span></span>

<span data-ttu-id="25936-109">패키지에 있는 모든 파일을 확장 하 고 대상 패키지 원본에 사용 된 `-Expand` 전환 합니다.</span><span class="sxs-lookup"><span data-stu-id="25936-109">To expand all the files in the package to the destination package source, use the `-Expand` switch.</span></span> <span data-ttu-id="25936-110">일반적으로 추가 하위 폴더와 같은 대상에 나타나는 결과 `tools` 및 `lib`합니다.</span><span class="sxs-lookup"><span data-stu-id="25936-110">This typically results in additional subfolders appearing in the destination, such as `tools` and `lib`.</span></span>

## <a name="usage"></a><span data-ttu-id="25936-111">용도</span><span class="sxs-lookup"><span data-stu-id="25936-111">Usage</span></span>

```
nuget add <packagePath> -Source <sourcePath> [options]
```

<span data-ttu-id="25936-112">여기서 `<packagePath>` 를 추가 하려면 패키지에 경로 이름 및 `<sourcePath>` 패키지를 추가할 폴더 기반 패키지 소스를 지정 합니다.</span><span class="sxs-lookup"><span data-stu-id="25936-112">where `<packagePath>` is the pathname to the package to add, and `<sourcePath>` specifies the folder-based package source to which the package will be added.</span></span> <span data-ttu-id="25936-113">HTTP 원본은 지원 되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="25936-113">HTTP sources are not supported.</span></span>

## <a name="options"></a><span data-ttu-id="25936-114">옵션</span><span class="sxs-lookup"><span data-stu-id="25936-114">Options</span></span>

| <span data-ttu-id="25936-115">옵션</span><span class="sxs-lookup"><span data-stu-id="25936-115">Option</span></span> | <span data-ttu-id="25936-116">설명</span><span class="sxs-lookup"><span data-stu-id="25936-116">Description</span></span> |
| --- | --- |
| <span data-ttu-id="25936-117">ConfigFile</span><span class="sxs-lookup"><span data-stu-id="25936-117">ConfigFile</span></span> | <span data-ttu-id="25936-118">적용할 NuGet 구성 파일입니다.</span><span class="sxs-lookup"><span data-stu-id="25936-118">The NuGet configuration file to apply.</span></span> <span data-ttu-id="25936-119">지정 하지 않으면 *%AppData%\NuGet\NuGet.Config* 사용 됩니다.</span><span class="sxs-lookup"><span data-stu-id="25936-119">If not specified, *%AppData%\NuGet\NuGet.Config* is used.</span></span>| 
| <span data-ttu-id="25936-120">Expand</span><span class="sxs-lookup"><span data-stu-id="25936-120">Expand</span></span> | <span data-ttu-id="25936-121">패키지의 패키지 원본에 있는 모든 파일을 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="25936-121">Adds all the files in the package to the package source.</span></span> |
| <span data-ttu-id="25936-122">ForceEnglishOutput</span><span class="sxs-lookup"><span data-stu-id="25936-122">ForceEnglishOutput</span></span> | <span data-ttu-id="25936-123">*(3.5 +)*  고정, 영어 기반 문화권을 사용 하 여 실행할 nuget.exe를 강제로 수행 합니다.</span><span class="sxs-lookup"><span data-stu-id="25936-123">*(3.5+)* Forces nuget.exe to run using an invariant, English-based culture.</span></span> |
| <span data-ttu-id="25936-124">도움말</span><span class="sxs-lookup"><span data-stu-id="25936-124">Help</span></span> | <span data-ttu-id="25936-125">도움말의 명령에 대 한 정보를 표시 합니다.</span><span class="sxs-lookup"><span data-stu-id="25936-125">Displays help information for the command.</span></span> |
| <span data-ttu-id="25936-126">비 대화형</span><span class="sxs-lookup"><span data-stu-id="25936-126">NonInteractive</span></span> | <span data-ttu-id="25936-127">사용자 입력 또는 확인에 대 한 프롬프트를 표시 하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="25936-127">Suppresses prompts for user input or confirmations.</span></span> |
| <span data-ttu-id="25936-128">자세한 정도</span><span class="sxs-lookup"><span data-stu-id="25936-128">Verbosity</span></span> | <span data-ttu-id="25936-129">출력에 표시 되는 세부 정보 수준을 지정: *일반*, *quiet*, *자세한*합니다.</span><span class="sxs-lookup"><span data-stu-id="25936-129">Specifies the amount of detail displayed in the output: *normal*, *quiet*, *detailed*.</span></span> |

<span data-ttu-id="25936-130">또한 참조 [환경 변수](cli-ref-environment-variables.md)</span><span class="sxs-lookup"><span data-stu-id="25936-130">Also see [Environment variables](cli-ref-environment-variables.md)</span></span>

## <a name="examples"></a><span data-ttu-id="25936-131">예제</span><span class="sxs-lookup"><span data-stu-id="25936-131">Examples</span></span>

```
nuget add foo.nupkg -Source c:\bar\

nuget add foo.nupkg -Source \\bar\packages\
```
