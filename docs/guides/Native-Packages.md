---
title: 네이티브 NuGet 패키지 만들기
description: 관리 코드 대신 C++ 프로젝트에서 사용할 C++ 코드가 포함된 네이티브 NuGet 패키지를 만드는 방법에 대한 세부 정보입니다.
author: karann-msft
ms.author: karann
ms.date: 01/09/2017
ms.topic: conceptual
ms.openlocfilehash: e0ec5323f7be53bef6637ad69540a66abbf22711
ms.sourcegitcommit: 2b50c450cca521681a384aa466ab666679a40213
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/07/2020
ms.locfileid: "69520523"
---
# <a name="creating-native-packages"></a><span data-ttu-id="778f3-103">네이티브 패키지 만들기</span><span class="sxs-lookup"><span data-stu-id="778f3-103">Creating native packages</span></span>

<span data-ttu-id="778f3-104">네이티브 패키지에는 관리형 어셈블리 대신 C++(또는 유사한) 프로젝트 내에서 사용할 수 있도록 하는 네이티브 이진 파일이 포함됩니다.</span><span class="sxs-lookup"><span data-stu-id="778f3-104">A native package contains native binaries instead of managed assemblies, allowing it to be used within C++ (or similar) projects.</span></span> <span data-ttu-id="778f3-105">(사용 섹션에서 [네이티브 C++ 패키지](../consume-packages/finding-and-choosing-packages.md#native-c-packages)를 참조하세요.)</span><span class="sxs-lookup"><span data-stu-id="778f3-105">(See [Native C++ Packages](../consume-packages/finding-and-choosing-packages.md#native-c-packages) in the Consume section.)</span></span>

<span data-ttu-id="778f3-106">C++ 프로젝트에서 사용할 수 있으려면 패키지는 `native` 프레임워크를 대상으로 지정해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="778f3-106">To be consumable in a C++ project, a package must target the `native` framework.</span></span> <span data-ttu-id="778f3-107">NuGet이 모든 C++ 프로젝트를 동일하게 처리하므로 현재 이 프레임워크와 연결된 버전 번호가 없습니다.</span><span class="sxs-lookup"><span data-stu-id="778f3-107">At present there are not any version numbers associated with this framework as NuGet treats all C++ projects the same.</span></span>

> [!Note]
> <span data-ttu-id="778f3-108">다른 개발자가 해당 태그를 검색하여 패키지를 찾을 수 있도록 *의*  섹션에 `<tags>`네이티브`.nuspec`를 포함해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="778f3-108">Be sure to include *native* in the `<tags>` section of your `.nuspec` to help other developers find your package by searching on that tag.</span></span>

<span data-ttu-id="778f3-109">그러면 `native`를 대상으로 지정한 네이티브 NuGet 패키지는 `\build`, `\content` 및 `\tools` 폴더에 파일을 제공합니다. `\lib`은 이 경우에 사용되지 않습니다(NuGet은 C++ 프로젝트에 직접 참조를 추가할 수 없음).</span><span class="sxs-lookup"><span data-stu-id="778f3-109">Native NuGet packages targeting `native` then provide files in `\build`, `\content`, and `\tools` folders; `\lib` is not used in this case (NuGet cannot directly add references to a C++ project).</span></span> <span data-ttu-id="778f3-110">NuGet에서 패키지를 사용하는 프로젝트에 자동으로 가져오는 `\build`의 대상 및 props 파일이 패키지에 포함될 수도 있습니다.</span><span class="sxs-lookup"><span data-stu-id="778f3-110">A package may also include targets and props files in `\build` that NuGet will automatically import into projects that consume the package.</span></span> <span data-ttu-id="778f3-111">`.targets` 및/또는 `.props` 확장명으로 패키지 ID와 동일하게 해당 파일의 이름을 지정해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="778f3-111">Those files must be named the same as the package ID with the `.targets` and/or `.props` extensions.</span></span> <span data-ttu-id="778f3-112">예를 들어 [cpprestsdk](https://nuget.org/packages/cpprestsdk/) 패키지에는 해당 `cpprestsdk.targets` 폴더에 있는 `\build` 파일이 포함됩니다.</span><span class="sxs-lookup"><span data-stu-id="778f3-112">For example, the [cpprestsdk](https://nuget.org/packages/cpprestsdk/) package includes a `cpprestsdk.targets` file in its `\build` folder.</span></span>

<span data-ttu-id="778f3-113">네이티브 패키지뿐만 아니라 모든 NuGet 패키지에 `\build` 폴더를 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="778f3-113">The `\build` folder can be used for all NuGet packages and not just native packages.</span></span> <span data-ttu-id="778f3-114">`\build` 폴더는 `\content`, `\lib` 및 `\tools` 폴더와 같은 대상 프레임워크를 그대로 보존합니다.</span><span class="sxs-lookup"><span data-stu-id="778f3-114">The `\build` folder respects target frameworks just like the `\content`, `\lib`, and `\tools` folders.</span></span> <span data-ttu-id="778f3-115">즉, `\build\net40` 폴더 및 `\build\net45` 폴더를 만들 수 있습니다. 또한 NuGet에서는 적절한 props 및 대상 파일을 프로젝트로 가져옵니다.</span><span class="sxs-lookup"><span data-stu-id="778f3-115">This means you can create a `\build\net40` folder and a `\build\net45` folder and NuGet will import the appropriate props and targets files into the project.</span></span> <span data-ttu-id="778f3-116">(MSBuild 대상을 가져오기 위해 PowerShell 스크립트를 사용하지 않아도 됩니다.)</span><span class="sxs-lookup"><span data-stu-id="778f3-116">(Use of PowerShell scripts to import MSBuild targets is not needed.)</span></span>
