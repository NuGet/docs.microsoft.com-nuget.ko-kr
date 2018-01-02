---
title: "NuGet 패키지 만들기에 대한 개요 및 워크플로 | Microsoft Docs"
author: kraigb
ms.author: kraigb
manager: ghogen
ms.date: 07/26/2017
ms.topic: article
ms.prod: nuget
ms.technology: 
ms.assetid: feb7918c-4709-48a4-a106-8d65c41014dc
description: "NuGet 패키지를 만들고 게시하는 프로세스를 간략히 설명하며, 프로세스의 다른 특정 부분에 대한 링크가 포함되어 있습니다."
keywords: "NuGet 패키지 만들기, NuGet 만들기 개요, NuGet 만들기 워크플로, 패키지 만들기 워크플로, 패키지 만들기 개요."
ms.reviewer:
- karann-msft
- unniravindranathan
ms.openlocfilehash: 25822d22c53c07e4c1a2f4ab310c4a5da09b7661
ms.sourcegitcommit: 122bf7ce308365ea45da018b0768f0536de76a1f
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 12/14/2017
---
# <a name="package-creation-workflow"></a><span data-ttu-id="04f72-104">패키지 만들기 워크플로</span><span class="sxs-lookup"><span data-stu-id="04f72-104">Package creation workflow</span></span>

<span data-ttu-id="04f72-105">패키지를 만드는 작업은 공용 nuget.org 갤러리 또는 조직 내의 전용 갤러리를 통해 패키지하고 다른 사람들과 공유하려는 컴파일된 코드(일반적으로 .NET 어셈블리)로 시작합니다.</span><span class="sxs-lookup"><span data-stu-id="04f72-105">Creating a package starts with the compiled code (typically .NET assemblies) that you want to package and share with others, either through the public nuget.org gallery or a private gallery within your organization.</span></span> <span data-ttu-id="04f72-106">패키지에는 패키지를 설치할 때 표시되는 추가 정보와 같은 추가 파일이 포함될 수 있으며, 특정 프로젝트 파일에 대한 변환이 포함될 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="04f72-106">The package can also include additional files such as a readme that is displayed when the package is installed, and can include transformations to certain project files.</span></span>

<span data-ttu-id="04f72-107">또한 패키지는 자체의 코드를 포함하지 않고 임의 개수의 다른 종속성만 끌어올 수도 있습니다.</span><span class="sxs-lookup"><span data-stu-id="04f72-107">A package can also serve to only pull in any number of other dependencies, without containing any code of its own.</span></span> <span data-ttu-id="04f72-108">이러한 패키지는 여러 독립적인 패키지로 구성된 SDK를 제공하는 편리한 방법입니다.</span><span class="sxs-lookup"><span data-stu-id="04f72-108">Such a package is a convenient way to deliver an SDK that's composed of multiple independent packages.</span></span> <span data-ttu-id="04f72-109">다른 경우에는 디버깅을 지원하기 위해 기호(`.pdb`) 파일만 패키지에 포함될 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="04f72-109">In other cases, a package may contain only symbol (`.pdb`) files to aid debugging.</span></span>

> [!Note]
> <span data-ttu-id="04f72-110">다른 개발자가 사용할 패키지를 만드는 경우 개발자가 사용자의 작업에 의존하고 있음을 이해하는 것이 중요합니다.</span><span class="sxs-lookup"><span data-stu-id="04f72-110">When you create a package for use by other developers, it's important to understand that they are taking a dependency on your work.</span></span> <span data-ttu-id="04f72-111">이와 같이 패키지를 만들고 게시하는 것은 버그를 수정하고 다른 업데이트를 만들거나 최소한 패키지를 오픈 소스로 사용할 수 있게 하여 다른 사람들이 패키지를 유지 관리할 수 있도록 하기 위한 약속을 의미합니다.</span><span class="sxs-lookup"><span data-stu-id="04f72-111">As such, creating and publishing a package also implies a commitment to fixing bugs and making other updates, or at the very least making the package available as open source so others can help to maintain it.</span></span>

<span data-ttu-id="04f72-112">어떤 경우이든 패키지를 만드는 작업은 패키지할 어셈블리와 다른 파일을 결정하는 것으로 시작합니다.</span><span class="sxs-lookup"><span data-stu-id="04f72-112">Whatever the case, creating a package begins with deciding which assemblies and other files to package.</span></span> <span data-ttu-id="04f72-113">그런 다음 식별자, 버전 번호, 저작권 정보, MSBuild props 및 targets와 함께 패키지의 내용을 설명하는 `.nuspec` 파일이라고 하는 매니페스트 파일을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="04f72-113">You then create a manifest file, referred to as a `.nuspec` file, to describe the package's contents along with its identifer, version number, copyright information, MSBuild props and targets, and much more.</span></span>

<span data-ttu-id="04f72-114">적절한 폴더에 필요한 모든 파일을 준비하고 적절한 `.nuspec` 파일을 만들었으면 `nuget pack` 명령(또는 [MSBuild pack 대상](../Schema/msbuild-targets.md))을 사용하여 모든 파일을 함께 `.nupkg` 파일에 넣습니다.</span><span class="sxs-lookup"><span data-stu-id="04f72-114">When you've prepared all the necessary files in the appropriate folders and have created the appropriate `.nuspec` file, you then use the `nuget pack` command (or the [MSBuild pack target](../Schema/msbuild-targets.md)) to put everything together into a `.nupkg` file.</span></span> <span data-ttu-id="04f72-115">그러면 다른 개발자가 사용할 수 있는 모든 호스트에 패키지를 배포할 준비가 되었습니다.</span><span class="sxs-lookup"><span data-stu-id="04f72-115">You're then ready to deploy the package to whatever host makes it available to other developers.</span></span>

> [!Tip]
> <span data-ttu-id="04f72-116">`.nupkg` 확장명이 있는 NuGet 패키지는 단순히 ZIP 파일입니다.</span><span class="sxs-lookup"><span data-stu-id="04f72-116">A NuGet package with the `.nupkg` extension is simply a ZIP file.</span></span> <span data-ttu-id="04f72-117">패키지의 내용을 쉽게 검사하려면 확장명을 `.zip`으로 변경하고 평소와 같이 해당 내용을 펼쳐봅니다.</span><span class="sxs-lookup"><span data-stu-id="04f72-117">To easily examine any package's contents, change the extension to `.zip` and expand its contents as usual.</span></span> <span data-ttu-id="04f72-118">호스트에 업로드하기 전에 확장명을 `.nupkg`로 다시 변경해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="04f72-118">Just be sure to change the extension back to `.nupkg` before attempting to upload it to a host.</span></span>

<span data-ttu-id="04f72-119">만들기 프로세스를 알아보고 이해하려면 [패키지 만들기](../create-packages/creating-a-package.md)부터 시작하여 모든 패키지에 공통적인 핵심 프로세스를 안내합니다.</span><span class="sxs-lookup"><span data-stu-id="04f72-119">To learn and understand the creation process, start with [Creating a package](../create-packages/creating-a-package.md) which guides you through the core processes common to all packages.</span></span> 

<span data-ttu-id="04f72-120">이러한 프로세스에서 패키지에 대한 여러 가지 다른 옵션을 고려할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="04f72-120">From there, you can consider a number of other options for your package:</span></span>

-  <span data-ttu-id="04f72-121">[여러 대상 프레임워크 지원](../create-packages/supporting-multiple-target-frameworks.md)에서는 다양한 .NET Framework에 대해 여러 변형을 사용하여 패키지를 만드는 방법에 대해 설명합니다.</span><span class="sxs-lookup"><span data-stu-id="04f72-121">[Supporting Multiple Target Frameworks](../create-packages/supporting-multiple-target-frameworks.md) describes how to create a package with multiple variants for different .NET Frameworks.</span></span>
-  <span data-ttu-id="04f72-122">[지역화된 패키지 만들기](../create-packages/creating-localized-packages.md)에서는 여러 언어 리소스가 있는 패키지를 구성하는 방법과 별도의 지역화된 위성 패키지를 사용하는 방법에 대해 설명합니다.</span><span class="sxs-lookup"><span data-stu-id="04f72-122">[Creating Localized Packages](../create-packages/creating-localized-packages.md) describes how to structure a package with multiple language resources and how to use separate localized satellite packages.</span></span>
-  <span data-ttu-id="04f72-123">[시험판 패키지](../create-packages/prerelease-packages.md)는 알파, 베타 및 RC 패키지를 관심 있는 고객에게 공개하는 방법을 보여줍니다.</span><span class="sxs-lookup"><span data-stu-id="04f72-123">[Pre-release Packages](../create-packages/prerelease-packages.md) demonstrates how to release alpha, beta, and rc packages to those customers who are interested.</span></span>
-  <span data-ttu-id="04f72-124">[원본 및 구성 파일 변환](../create-packages/source-and-config-file-transformations.md)은 프로젝트에 추가된 파일에서 단방향 토큰 대체를 수행하는 방법과 패키지가 제거될 때 취소되는 설정으로 `web.config` 및 `app.config`를 수정하는 방법에 대해 설명합니다.</span><span class="sxs-lookup"><span data-stu-id="04f72-124">[Source and Config File Transformations](../create-packages/source-and-config-file-transformations.md) describes how you can do both one-way token replacements in files that are added to a project, and modify `web.config` and `app.config` with settings that are also backed out when the package is uninstalled.</span></span>
-  <span data-ttu-id="04f72-125">[기호 패키지](../create-packages/symbol-packages.md)는 사용자가 코드를 단계별로 실행하면서 디버그할 수 있도록 라이브러리에 대한 기호를 제공하기 위한 지침을 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="04f72-125">[Symbol Packages](../create-packages/symbol-packages.md) offers guidance for supplying symbols for your library that allow consumers to step into your code while debugging.</span></span>
-  <span data-ttu-id="04f72-126">[패키지 버전 관리](../reference/package-versioning.md)에서는 종속성을 허용하는 정확한 버전(패키지에서 사용하는 다른 패키지)을 식별하는 방법에 대해 설명합니다.</span><span class="sxs-lookup"><span data-stu-id="04f72-126">[Package versioning](../reference/package-versioning.md) discusses how to identify the exact versions that you allow for your dependencies (other packages that you consume from your package).</span></span>
-  <span data-ttu-id="04f72-127">[네이티브 패키지](../create-packages/native-packages.md)는 C++ 소비자용 패키지를 만드는 프로세스를 설명합니다.</span><span class="sxs-lookup"><span data-stu-id="04f72-127">[Native Packages](../create-packages/native-packages.md) describes the process for creating a package for C++ consumers.</span></span>

<span data-ttu-id="04f72-128">다음으로 nuget.org에 패키지를 게시할 준비가 되면 [패키지 게시](../create-packages/publish-a-package.md)의 간단한 프로세스를 수행합니다.</span><span class="sxs-lookup"><span data-stu-id="04f72-128">When you're then ready to publish a package to nuget.org, follow the simple process in [Publish a package](../create-packages/publish-a-package.md).</span></span>

<span data-ttu-id="04f72-129">nuget.org 대신 개인 피드를 사용하려면 [패키지 호스팅 개요](../hosting-packages/overview.md)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="04f72-129">If you want to use a private feed instead of nuget.org, see the [Hosting Packages Overview](../hosting-packages/overview.md)</span></span>
