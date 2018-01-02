---
title: "로컬 NuGet 피드 설정 | Microsoft Docs"
author: kraigb
ms.author: kraigb
manager: ghogen
ms.date: 12/06/2017
ms.topic: article
ms.prod: nuget
ms.technology: 
ms.assetid: 1354a527-d988-43d1-8dcf-6ce46ec5d3d4
description: "로컬 네트워크에서 폴더를 사용하여 NuGet 패키지에 로컬 피드를 만드는 방법"
keywords: "NuGet 피드, NuGet 갤러리, 로컬 패키지 피드"
ms.reviewer:
- karann-msft
- unniravindranathan
ms.openlocfilehash: 32217622077ff983abaf00b2e6e5baf3064fff56
ms.sourcegitcommit: d0ba99bfe019b779b75731bafdca8a37e35ef0d9
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 12/14/2017
---
# <a name="local-feeds"></a><span data-ttu-id="256e6-104">로컬 피드</span><span class="sxs-lookup"><span data-stu-id="256e6-104">Local feeds</span></span>

<span data-ttu-id="256e6-105">로컬 NuGet 패키지 피드는 패키지를 배치할 로컬 네트워크(또는 사용자 고유의 컴퓨터)의 단순한 계층적 폴더 구조입니다.</span><span class="sxs-lookup"><span data-stu-id="256e6-105">Local NuGet package feeds are simply hierarchical folder structures on your local network (or even just your own computer) in which you place packages.</span></span> <span data-ttu-id="256e6-106">CLI, 패키지 관리자 UI 및 패키지 관리자 콘솔을 사용하여 다른 모든 NuGet 작업에서 이러한 피드를 패키지 소스로 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="256e6-106">These feeds can then be used as package sources with all other NuGet operations using the CLI, the Package Manager UI, and the Package Manager Console.</span></span>

<span data-ttu-id="256e6-107">소스를 사용하려면 [패키지 관리자 UI](../tools/package-manager-ui.md#package-sources) 또는 [`nuget sources`](../tools/cli-ref-sources.md) 명령을 사용하여 원본 목록에 해당 경로 이름(예: `\\myserver\packages`)을 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="256e6-107">To enable the source, add its pathname (such as `\\myserver\packages`) to the list of sources using the [Package Manager UI](../tools/package-manager-ui.md#package-sources) or the [`nuget sources`](../tools/cli-ref-sources.md) command.</span></span>

> [!Note]
> <span data-ttu-id="256e6-108">계층적 폴더 구조는 NuGet 3.3+에서 지원됩니다.</span><span class="sxs-lookup"><span data-stu-id="256e6-108">Hierarchical folder structures are supported in NuGet 3.3+.</span></span> <span data-ttu-id="256e6-109">이전 버전의 NuGet은 성능이 계층적 구조보다 훨씬 낮은 패키지를 포함하는 단일 폴더만을 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="256e6-109">Older versions of NuGet use only a single folder containing packages, with which performance is much lower than the hierarchical structure.</span></span>

## <a name="initializing-and-maintaining-hierarchical-folders"></a><span data-ttu-id="256e6-110">계층적 폴더 초기화 및 유지 관리</span><span class="sxs-lookup"><span data-stu-id="256e6-110">Initializing and maintaining hierarchical folders</span></span>

<span data-ttu-id="256e6-111">계층적 버전이 있는 폴더 트리에는 다음과 같은 일반 구조가 있습니다.</span><span class="sxs-lookup"><span data-stu-id="256e6-111">The hierarchical versioned folder tree has the following general structure:</span></span>

    \\myserver\packages
      └─<packageID>
        └─<version>
          ├─<packageID>.<version>.nupkg
          └─<other files>

<span data-ttu-id="256e6-112">[`nuget add`](../tools/cli-ref-add.md) 명령을 사용하여 피드에 패키지를 복사할 때 NuGet이 이 구조를 자동으로 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="256e6-112">NuGet creates this structure automatically when you use the [`nuget add`](../tools/cli-ref-add.md) command to copy a package to the feed:</span></span>

```
nuget add new_package.1.0.0.nupkg -source \\myserver\packages
```

<span data-ttu-id="256e6-113">`nuget add` 명령은 한 번에 하나의 패키지에서 작동합니다. 그러면 여러 패키지가 포함된 피드를 설정할 때 편리할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="256e6-113">The `nuget add` command works with one package at a time, which can be inconvenient when setting up a feed with multiple packages.</span></span>

<span data-ttu-id="256e6-114">이러한 경우에 개별적으로 `nuget add`를 실행한 경우와 같이 피드에 폴더의 모든 패키지를 복사하는 [`nuget init`](../tools/cli-ref-init.md) 명령을 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="256e6-114">In such cases, use the [`nuget init`](../tools/cli-ref-init.md) command to copy all packages in a folder to the feed as if you ran `nuget add` on each one individually.</span></span> <span data-ttu-id="256e6-115">예를 들어 다음 명령은 `c:\packages`의 모든 패키지를 `\\myserver\packages`의 계층적 트리에 복사합니다.</span><span class="sxs-lookup"><span data-stu-id="256e6-115">For example, the following command copies all packages from `c:\packages` to a hierarchical tree on `\\myserver\packages`:</span></span>

```
nuget init c:\packages \\myserver\packages
```

<span data-ttu-id="256e6-116">`add` 명령과 마찬가지로 `init`는 각 패키지 식별자에 폴더를 만듭니다. 각각에는 적절한 패키지 내에 버전 번호 폴더가 포함됩니다.</span><span class="sxs-lookup"><span data-stu-id="256e6-116">As with the `add` command, `init` creates a folder for each package identifier, each of which contains a version number folder, within which is the appropriate package.</span></span>
