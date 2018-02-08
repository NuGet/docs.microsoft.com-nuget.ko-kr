---
title: "UWP 프로젝트가 있는 NuGet project.json 파일 | Microsoft Docs"
author: kraigb
ms.author: kraigb
manager: ghogen
ms.date: 07/17/2017
ms.topic: article
ms.prod: nuget
ms.technology: 
description: "project.json 파일을 사용하여 UWP(유니버설 Windows 플랫폼) 프로젝트에서 NuGet 종속성을 추적하는 방법을 설명합니다."
keywords: "NuGet 종속성, NuGet 및 UWP, UWP 및 project.json, NuGet project.json 파일"
ms.reviewer:
- karann-msft
- unniravindranathan
ms.openlocfilehash: f1ec086d6404c441ca5ad53028af2265a2344905
ms.sourcegitcommit: 4651b16a3a08f6711669fc4577f5d63b600f8f58
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 02/01/2018
---
# <a name="projectjson-and-uwp"></a><span data-ttu-id="e31bf-104">project.json 및 UWP</span><span class="sxs-lookup"><span data-stu-id="e31bf-104">project.json and UWP</span></span>

> [!Important]
> <span data-ttu-id="e31bf-105">이 콘텐츠는 더 이상 사용되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="e31bf-105">This content is deprecated.</span></span> <span data-ttu-id="e31bf-106">프로젝트는 `packages.config` 또는 PackageReference 형식을 사용해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="e31bf-106">Projects should use either the `packages.config` or PackageReference formats.</span></span>

<span data-ttu-id="e31bf-107">이 문서에서는 NuGet 3 이상(Visual Studio 2015 이상)의 기능을 사용하는 패키지 구조에 대해 설명합니다.</span><span class="sxs-lookup"><span data-stu-id="e31bf-107">This document describes the package structure that employs features in NuGet 3+ (Visual Studio 2015 and later).</span></span> <span data-ttu-id="e31bf-108">`.nuspec`의 `minClientVersion` 속성은 3.1로 설정하여 여기서 설명하는 기능이 필요하다고 명시하는 데 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="e31bf-108">The `minClientVersion` property of your `.nuspec` can be used to state that you require the features described here by setting it to 3.1.</span></span>

## <a name="adding-uwp-support-to-an-existing-package"></a><span data-ttu-id="e31bf-109">기존 패키지에 UWP 지원 추가</span><span class="sxs-lookup"><span data-stu-id="e31bf-109">Adding UWP support to an existing package</span></span>

<span data-ttu-id="e31bf-110">기존 패키지가 있고 UWP 응용 프로그램에 대한 지원을 추가하려는 경우 여기서 설명하는 패키징 형식을 사용할 필요가 없습니다.</span><span class="sxs-lookup"><span data-stu-id="e31bf-110">If you have an existing package and you want to add support for UWP applications, then you don’t need to adopt the  packaging format described here.</span></span> <span data-ttu-id="e31bf-111">여기서 설명하는 기능이 필요하고 NuGet 클라이언트 버전 3 이상으로 업데이트된 클라이언트에서만 작동하도록 하려면 이 형식을 채택하면 됩니다.</span><span class="sxs-lookup"><span data-stu-id="e31bf-111">You only need to adopt this format if you require the features it describes and are willing to  work only with clients that have updated to version 3+ of the NuGet client.</span></span>

## <a name="i-already-target-netcore45"></a><span data-ttu-id="e31bf-112">이미 netcore45를 대상으로 하고 있는 경우</span><span class="sxs-lookup"><span data-stu-id="e31bf-112">I already target netcore45</span></span>

<span data-ttu-id="e31bf-113">이미 `netcore45`를 대상으로 지정하고 있고 여기서 설명하는 기능을 활용할 필요가 없는 경우 아무 작업도 필요하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="e31bf-113">If you target `netcore45` already, and you don’t need to take advantage of the features here, no action is needed.</span></span> <span data-ttu-id="e31bf-114">`netcore45` 패키지는 UWP 응용 프로그램에서 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="e31bf-114">`netcore45` packages can be consumed by UWP applications.</span></span>

## <a name="i-want-to-take-advantage-of-windows-10-specific-apis"></a><span data-ttu-id="e31bf-115">Windows 10 특정 API를 활용하려는 경우</span><span class="sxs-lookup"><span data-stu-id="e31bf-115">I want to take advantage of Windows 10 specific APIs</span></span>

<span data-ttu-id="e31bf-116">이 경우에는 `uap10.0` 대상 프레임워크 모니커(TFM 또는 TxM)를 패키지에 추가해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="e31bf-116">In this case you need to add the `uap10.0` target framework moniker (TFM or TxM) to your package.</span></span> <span data-ttu-id="e31bf-117">패키지에 새 폴더를 만들고 Windows 10에서 작동하도록 컴파일된 어셈블리를 해당 폴더에 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="e31bf-117">Create a new folder in your package and add the assembly that has been compiled to work with Windows 10 to that folder.</span></span>

## <a name="i-dont-need-windows-10-specific-apis-but-want-new-net-features-or-dont-have-netcore45-already"></a><span data-ttu-id="e31bf-118">Windows 10 특정 API는 필요하지 않지만 새 .NET 기능을 원하거나 netcore45가 아직 없는 경우</span><span class="sxs-lookup"><span data-stu-id="e31bf-118">I don’t need Windows 10 specific APIs, but want new .NET features or don’t have netcore45 already</span></span>

<span data-ttu-id="e31bf-119">이 경우에는 `dotnet` TxM을 패키지에 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="e31bf-119">In this case you would add the `dotnet` TxM to your package.</span></span> <span data-ttu-id="e31bf-120">다른 TxM과 달리 `dotnet`은 노출 영역 또는 플랫폼을 의미하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="e31bf-120">Unlike other TxMs, `dotnet` doesn't imply a surface area or platform.</span></span> <span data-ttu-id="e31bf-121">이는 종속성이 작동하는 모든 플랫폼에서 패키지가 작동한다는 것을 나타냅니다.</span><span class="sxs-lookup"><span data-stu-id="e31bf-121">It is stating that your package works on any platform that your dependencies work on.</span></span> <span data-ttu-id="e31bf-122">`dotnet` TxM을 사용하여 패키지를 빌드하는 경우 사용자에게 필요한 BCL 패키지(예: `System.Text`, `System.Xml` 등)를 정의해야 하므로 `.nuspec`에 더 많은 TxM 특정 종속성이 있을 수 있습니다. 이러한 종속성이 작동하는 위치는 패키지가 작동하는 위치를 정의합니다.</span><span class="sxs-lookup"><span data-stu-id="e31bf-122">When building a package with the `dotnet` TxM, you are likely to have many more TxM-specific dependencies in your `.nuspec`, as you need to define the BCL packages you depend on, such `System.Text`, `System.Xml`, etc. The locations that those dependencies work on define where your package works.</span></span>

### <a name="how-do-i-find-out-my-dependencies"></a><span data-ttu-id="e31bf-123">내 종속성을 찾으려면 어떻게 할까요?</span><span class="sxs-lookup"><span data-stu-id="e31bf-123">How do I find out my dependencies</span></span>

<span data-ttu-id="e31bf-124">나열할 종속성을 파악하는 데에는 다음 두 가지 방법이 있습니다.</span><span class="sxs-lookup"><span data-stu-id="e31bf-124">There are two ways to figure out which dependencies to list:</span></span>

1. <span data-ttu-id="e31bf-125">[NuSpec 종속성 생성기](https://github.com/onovotny/ReferenceGenerator) **타사** 도구를 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="e31bf-125">Use the [NuSpec Dependency Generator](https://github.com/onovotny/ReferenceGenerator) **3rd party** tool.</span></span> <span data-ttu-id="e31bf-126">이 도구는 프로세스를 자동화하고 빌드 시 `.nuspec` 파일을 종속 패키지로 업데이트합니다.</span><span class="sxs-lookup"><span data-stu-id="e31bf-126">The tool automates the process and updates your `.nuspec` file with the dependant packages on build.</span></span> <span data-ttu-id="e31bf-127">[NuSpec.ReferenceGenerator](https://www.nuget.org/packages/NuSpec.ReferenceGenerator/) NuGet 패키지를 통해 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="e31bf-127">It is available via a NuGet package, [NuSpec.ReferenceGenerator](https://www.nuget.org/packages/NuSpec.ReferenceGenerator/).</span></span>

1. <span data-ttu-id="e31bf-128">(어려운 방법) 런타임에 실제로 필요한 어셈블리를 확인하려면 `ILDasm`을 사용하여 `.dll`을 살펴봅니다.</span><span class="sxs-lookup"><span data-stu-id="e31bf-128">(The hard way) Use `ILDasm` to look at your `.dll` to see what assemblies are actually needed at runtime.</span></span> <span data-ttu-id="e31bf-129">그런 다음 각각에서 제공하는 NuGet 패키지를 결정합니다.</span><span class="sxs-lookup"><span data-stu-id="e31bf-129">Then determine which NuGet package they each come from.</span></span>

<span data-ttu-id="e31bf-130">`dotnet` TxM을 지원하는 패키지를 만드는 데 도움이 되는 기능에 대한 자세한 내용은 [`project.json`](project-json.md) 항목을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="e31bf-130">See the [`project.json`](project-json.md) topic for details on features that help in the creation of a package that supports the `dotnet` TxM.</span></span>

> [!Important]
> <span data-ttu-id="e31bf-131">패키지가 PCL 프로젝트에서 작동하도록 만들어진 경우 경고 및 잠재적인 호환성 문제를 방지하기 위해 `dotnet` 폴더를 만드는 것이 좋습니다.</span><span class="sxs-lookup"><span data-stu-id="e31bf-131">If your package is intended to work with PCL projects, we highly recommend to create a `dotnet` folder, to avoid warnings and potential compatibility issues.</span></span>

## <a name="directory-structure"></a><span data-ttu-id="e31bf-132">디렉터리 구조</span><span class="sxs-lookup"><span data-stu-id="e31bf-132">Directory structure</span></span>

<span data-ttu-id="e31bf-133">이 형식을 사용하는 NuGet 패키지에는 다음과 같은 잘 알려진 폴더와 동작이 있습니다.</span><span class="sxs-lookup"><span data-stu-id="e31bf-133">NuGet packages using this format have the following well-known folder and behaviors:</span></span>

| <span data-ttu-id="e31bf-134">폴더</span><span class="sxs-lookup"><span data-stu-id="e31bf-134">Folder</span></span> | <span data-ttu-id="e31bf-135">동작</span><span class="sxs-lookup"><span data-stu-id="e31bf-135">Behaviors</span></span> |
| --- | --- |
| <span data-ttu-id="e31bf-136">빌드</span><span class="sxs-lookup"><span data-stu-id="e31bf-136">Build</span></span> | <span data-ttu-id="e31bf-137">프로젝트에 다르게 통합되어 있지만 그렇지 않은 경우 변경되지 않은 MSBuild targets 및 props 파일을 포함합니다.</span><span class="sxs-lookup"><span data-stu-id="e31bf-137">Contains MSBuild targets and props files in this folder are integrated differently into the project, but otherwise there is no change.</span></span> |
| <span data-ttu-id="e31bf-138">도구</span><span class="sxs-lookup"><span data-stu-id="e31bf-138">Tools</span></span> | <span data-ttu-id="e31bf-139">`install.ps1` 및 `uninstall.ps1`은 실행되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="e31bf-139">`install.ps1` and `uninstall.ps1` are not run.</span></span> <span data-ttu-id="e31bf-140">`init.ps1`은 항상 있는 그대로 작동합니다.</span><span class="sxs-lookup"><span data-stu-id="e31bf-140">`init.ps1` works as it always has.</span></span> |
| <span data-ttu-id="e31bf-141">콘텐츠</span><span class="sxs-lookup"><span data-stu-id="e31bf-141">Content</span></span> | <span data-ttu-id="e31bf-142">사용자의 프로젝트에 자동으로 복사되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="e31bf-142">Content is not copied automatically into a user's project.</span></span> <span data-ttu-id="e31bf-143">프로젝트의 콘텐츠 포함에 대한 지원은 이후 릴리스에 예정되어 있습니다.</span><span class="sxs-lookup"><span data-stu-id="e31bf-143">Support for content inclusion in the project is planned for a later release.</span></span> |
| <span data-ttu-id="e31bf-144">Lib</span><span class="sxs-lookup"><span data-stu-id="e31bf-144">Lib</span></span> | <span data-ttu-id="e31bf-145">`lib`는 많은 패키지에 대해 NuGet 2.x에서 작동하는 것과 동일한 방식으로 작동하지만, 패키지를 사용할 때 패키지 내부에서 사용할 수 있는 이름에 대한 확장된 옵션 및 올바른 하위 폴더를 선택하기 위한 더 나은 논리를 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="e31bf-145">For many packages the `lib` works the same way it does in NuGet 2.x, but with expanded options for what names can be used inside it and better logic for picking the correct sub-folder when consuming packages.</span></span> <span data-ttu-id="e31bf-146">그러나 `ref`와 함께 사용하는 경우 `lib` 폴더에는 `ref` 폴더의 어셈블리에서 정의한 노출 영역을 구현하는 어셈블리가 포함됩니다.</span><span class="sxs-lookup"><span data-stu-id="e31bf-146">However, when used in conjunction with `ref`, the `lib` folder contains assemblies that implement the surface area defined by the assemblies in the `ref` folder.</span></span> |
| <span data-ttu-id="e31bf-147">Ref</span><span class="sxs-lookup"><span data-stu-id="e31bf-147">Ref</span></span> | <span data-ttu-id="e31bf-148">`ref`는 컴파일할 응용 프로그램에 대한 공용 노출 영역(공용 형식 및 메서드)을 정의하는 .NET 어셈블리가 포함되는 선택적 폴더입니다.</span><span class="sxs-lookup"><span data-stu-id="e31bf-148">`ref` is an optional folder that contains .NET assemblies defining the public surface (public types and methods) for an application to compile against.</span></span> <span data-ttu-id="e31bf-149">이 폴더에 있는 어셈블리는 구현이 없어도 컴파일러에 대한 노출 영역을 전적으로 정의하는 데 사용됩니다.</span><span class="sxs-lookup"><span data-stu-id="e31bf-149">The assemblies in this folder may have no implementation, they are purely used to define surface area for the compiler.</span></span> <span data-ttu-id="e31bf-150">패키지에 `ref` 폴더가 없으면 `lib`는 참조 어셈블리와 구현 어셈블리입니다.</span><span class="sxs-lookup"><span data-stu-id="e31bf-150">If the package has no `ref` folder, then the `lib` is both the reference assembly and the implementation assembly.</span></span> |
| <span data-ttu-id="e31bf-151">runtimes</span><span class="sxs-lookup"><span data-stu-id="e31bf-151">Runtimes</span></span> | <span data-ttu-id="e31bf-152">`runtimes`는 OS 특정 코드(예: CPU 아키텍처 및 OS 특정 이진 파일 또는 플랫폼에 종속된 이진 파일)가 포함된 선택적 폴더입니다.</span><span class="sxs-lookup"><span data-stu-id="e31bf-152">`runtimes` is an optional folder that contains OS specific code, such as CPU architecture and OS specific or otherwise platform-dependent binaries.</span></span> |

## <a name="msbuild-targets-and-props-files-in-packages"></a><span data-ttu-id="e31bf-153">패키지의 MSBuild targets 및 props 파일</span><span class="sxs-lookup"><span data-stu-id="e31bf-153">MSBuild targets and props files in packages</span></span>

<span data-ttu-id="e31bf-154">NuGet 패키지에는 패키지가 설치된 MSBuild 프로젝트에 가져오는 `.targets` 및 `.props` 파일이 포함될 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="e31bf-154">NuGet packages can contain `.targets` and `.props` files which are imported into any MSBuild project that the package is installed into.</span></span> <span data-ttu-id="e31bf-155">NuGet 2.x에서는 `<Import>` 문을 `.csproj` 파일에 삽입하여 수행했지만, NuGet 3.0에서는 특정 "프로젝트에 설치" 작업이 없습니다.</span><span class="sxs-lookup"><span data-stu-id="e31bf-155">In NuGet 2.x, this was done by injecting `<Import>` statements into the `.csproj` file, in NuGet 3.0 there is no specific "installation to project" action.</span></span> <span data-ttu-id="e31bf-156">대신 패키지 복원 프로세스는 두 파일, `[projectname].nuget.props`과 `[projectname].NuGet.targets`를 씁니다.</span><span class="sxs-lookup"><span data-stu-id="e31bf-156">Instead the package restore process writes two files `[projectname].nuget.props` and `[projectname].NuGet.targets`.</span></span>

<span data-ttu-id="e31bf-157">MSBuild는 이러한 두 파일을 찾고 프로젝트 빌드 프로세스의 시작과 끝 무렵에 자동으로 해당 파일을 가져옵니다.</span><span class="sxs-lookup"><span data-stu-id="e31bf-157">MSBuild knows to look for these two files and automatically imports them near the beginning and near the end of the project build process.</span></span> <span data-ttu-id="e31bf-158">이는 NuGet 2.x와 매우 비슷한 동작을 제공하지만, 주요 차이점 중 하나는 *이 경우 targets/props 파일의 순서가 보장되지 않는다*는 것입니다.</span><span class="sxs-lookup"><span data-stu-id="e31bf-158">This provides very similar behavior to NuGet 2.x, but with one major difference: *there is no guaranteed order of targets/props files in this case*.</span></span> <span data-ttu-id="e31bf-159">그러나 MSBuild는 `<Target>` 정의의 `BeforeTargets` 및 `AfterTargets` 특성을 통해 대상의 순서를 지정하는 방법을 제공합니다([Target 요소(MSBuild)](/visualstudio/msbuild/target-element-msbuild) 참조).</span><span class="sxs-lookup"><span data-stu-id="e31bf-159">However, MSBuild does provide ways to order targets through the `BeforeTargets` and `AfterTargets` attributes of the `<Target>` definition (see [Target Element (MSBuild)](/visualstudio/msbuild/target-element-msbuild).</span></span>

## <a name="lib-and-ref"></a><span data-ttu-id="e31bf-160">Lib 및 Ref</span><span class="sxs-lookup"><span data-stu-id="e31bf-160">Lib and Ref</span></span>

<span data-ttu-id="e31bf-161">NuGet v3에서는 `lib` 폴더의 동작이 크게 변경되지 않았습니다.</span><span class="sxs-lookup"><span data-stu-id="e31bf-161">The behavior of the `lib` folder hasn't changed significantly in NuGet v3.</span></span> <span data-ttu-id="e31bf-162">그러나 모든 어셈블리는 TxM이라는 하위 폴더 내에 있어야 하며 더 이상 `lib` 폴더 바로 아래에 배치할 수 없습니다.</span><span class="sxs-lookup"><span data-stu-id="e31bf-162">However, all assemblies must be within sub-folders named after a TxM, and can no longer be placed directly under the `lib` folder.</span></span> <span data-ttu-id="e31bf-163">TxM은 패키지에 지정된 특정 자산이 작동해야 하는 플랫폼의 이름입니다.</span><span class="sxs-lookup"><span data-stu-id="e31bf-163">A TxM is the name of a platform that a given asset in a package is supposed to work for.</span></span> <span data-ttu-id="e31bf-164">이러한 이름은 논리적으로 TFM(Target Framework Monikers)의 확장입니다. 예를 들어 `net45`, `net46`, `netcore50` 및 `dnxcore50`는 모두 TxM의 예입니다([대상 프레임워크](../reference/target-frameworks.md) 참조).</span><span class="sxs-lookup"><span data-stu-id="e31bf-164">Logically these are an extension of the Target Framework Monikers (TFM) e.g. `net45`, `net46`, `netcore50`, and `dnxcore50` are all examples of TxMs (see [Target Frameworks](../reference/target-frameworks.md).</span></span> <span data-ttu-id="e31bf-165">TxM은 다른 플랫폼 특정 노출 영역뿐만 아니라 프레임워크(TFM)도 참조할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="e31bf-165">TxM can refer to a framework (TFM) as well as other platform-specific surface areas.</span></span> <span data-ttu-id="e31bf-166">예를 들어 UWP TxM(`uap10.0`)은 .NET 노출 영역과 UWP 응용 프로그램에 대한 Windows 노출 영역을 나타냅니다.</span><span class="sxs-lookup"><span data-stu-id="e31bf-166">For example the UWP TxM (`uap10.0`) represents the .NET surface area as well as the Windows surface area for UWP applications.</span></span>

<span data-ttu-id="e31bf-167">lib 구조의 예:</span><span class="sxs-lookup"><span data-stu-id="e31bf-167">An example lib structure:</span></span>

    lib
    ├───net40
    │       MyLibrary.dll
    └───wp81
            MyLibrary.dll

<span data-ttu-id="e31bf-168">`lib` 폴더에는 런타임에 사용되는 어셈블리가 포함되어 있습니다.</span><span class="sxs-lookup"><span data-stu-id="e31bf-168">The `lib` folder contains assemblies that are used at runtime.</span></span> <span data-ttu-id="e31bf-169">대부분의 패키지에는 각 대상 TxM에 대한 `lib` 아래의 폴더만 있으면 됩니다.</span><span class="sxs-lookup"><span data-stu-id="e31bf-169">For most packages a folder under `lib` for each of the target TxMs is all that is required.</span></span>

## <a name="ref"></a><span data-ttu-id="e31bf-170">Ref</span><span class="sxs-lookup"><span data-stu-id="e31bf-170">Ref</span></span>

<span data-ttu-id="e31bf-171">컴파일하는 동안 다른 어셈블리를 사용해야 하는 경우도 있습니다(이 작업은 현재 .NET 참조 어셈블리에서 수행함).</span><span class="sxs-lookup"><span data-stu-id="e31bf-171">There are sometimes cases where a different assembly should be used during compilation (.NET Reference Assemblies do this today).</span></span> <span data-ttu-id="e31bf-172">이러한 경우 `ref`("Reference Assemblies(참조 어셈블리)" 약어)라는 최상위 폴더를 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="e31bf-172">For those cases, use a top-level folder called `ref` (short for "Reference Assemblies").</span></span>

<span data-ttu-id="e31bf-173">대부분의 패키지 작성자에게는 `ref` 폴더가 필요하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="e31bf-173">Most package authors don't require the `ref` folder.</span></span> <span data-ttu-id="e31bf-174">이 폴더는 컴파일 및 IntelliSense에 일관된 노출 영역을 제공해야 하지만 다른 TxM에 대해 별도의 구현이 필요한 패키지에 유용합니다.</span><span class="sxs-lookup"><span data-stu-id="e31bf-174">It is useful for packages that need to provide a consistent surface area for compilation and IntelliSense but then have different implementation for different TxMs.</span></span> <span data-ttu-id="e31bf-175">이 폴더에 대한 가장 큰 사용 사례는 NuGet에 대한 .NET Core 제공의 일환으로 생성되는 `System.*` 패키지입니다.</span><span class="sxs-lookup"><span data-stu-id="e31bf-175">The biggest use case of this are the `System.*` packages that are being produced as part of shipping .NET Core on NuGet.</span></span> <span data-ttu-id="e31bf-176">이러한 패키지에는 일관된 참조 어셈블리 집합으로 통합되는 다양한 구현이 있습니다.</span><span class="sxs-lookup"><span data-stu-id="e31bf-176">These packages have various implementations that are being unified by a consistent set of ref assemblies.</span></span>

<span data-ttu-id="e31bf-177">`ref` 폴더에 포함된 어셈블리는 컴파일러에 기계적으로 전달되는 참조 어셈블리입니다.</span><span class="sxs-lookup"><span data-stu-id="e31bf-177">Mechanically, the assemblies included in the `ref` folder are the reference assemblies being passed to the compiler.</span></span> <span data-ttu-id="e31bf-178">csc.exe를 사용한 사용자의 어셈블리는 [C# /reference 옵션](/dotnet/articles/csharp/language-reference/compiler-options/reference-compiler-option) 스위치에 전달할 어셈블리입니다.</span><span class="sxs-lookup"><span data-stu-id="e31bf-178">For those of you who have used csc.exe these are the assemblies we are passing to the [C# /reference option](/dotnet/articles/csharp/language-reference/compiler-options/reference-compiler-option) switch.</span></span>

<span data-ttu-id="e31bf-179">`ref` 폴더의 구조는 `lib`와 같습니다. 예를 들어 다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="e31bf-179">The structure of the `ref` folder is the same as `lib`, for example:</span></span>

    └───MyImageProcessingLib
         ├───lib
         │   ├───net40
         │   │       MyImageProcessingLibrary.dll
         │   │
         │   ├───net451
         │   │       MyImageProcessingLibrary.dll
         │   │
         │   └───win81
         │           MyImageProcessingLibrary.dll
         │
         └───ref
             ├───net40
             │       MyImageProcessingLibrary.dll
             │
             └───portable-net451-win81
                     MyImageProcessingLibrary.dll

<span data-ttu-id="e31bf-180">이 예에서 `ref` 디렉터리의 어셈블리는 모두 동일합니다.</span><span class="sxs-lookup"><span data-stu-id="e31bf-180">In this example the assemblies in the `ref` directories would all be identical.</span></span>

## <a name="runtimes"></a><span data-ttu-id="e31bf-181">runtimes</span><span class="sxs-lookup"><span data-stu-id="e31bf-181">Runtimes</span></span>

<span data-ttu-id="e31bf-182">runtimes 폴더는 일반적으로 운영 체제 및 CPU 아키텍처에서 정의되는 특정 "런타임"에서 실행하는 데 필요한 어셈블리 및 네이티브 라이브러리를 포함합니다.</span><span class="sxs-lookup"><span data-stu-id="e31bf-182">The runtimes folder contains assemblies and native libraries required to run on specific "runtimes", which are generally defined by Operating System and CPU architecture.</span></span> <span data-ttu-id="e31bf-183">이러한 런타임은 `win`, `win-x86`, `win7-x86`, `win8-64` 등과 같이 [RID(런타임 식별자)](/dotnet/core/rid-catalog)를 사용하여 식별됩니다.</span><span class="sxs-lookup"><span data-stu-id="e31bf-183">These runtimes are identified using [Runtime Identifiers (RIDs)](/dotnet/core/rid-catalog) such as `win`, `win-x86`, `win7-x86`, `win8-64`, etc.</span></span>

## <a name="native-light-up"></a><span data-ttu-id="e31bf-184">네이티브 폴더에 대한 설명</span><span class="sxs-lookup"><span data-stu-id="e31bf-184">Native light-up</span></span>

<span data-ttu-id="e31bf-185">다음 예에서는 여러 플랫폼에 대해 전적으로 관리되는 구현이 있지만 Windows 8 특정 네이티브 API를 호출할 수 있는 네이티브 도우미를 Windows 8에서 사용하는 패키지를 보여줍니다.</span><span class="sxs-lookup"><span data-stu-id="e31bf-185">The following example shows a package that has a purely managed implementation for several platforms, but uses native helpers on Windows 8 where it can call into Windows 8-specific native APIs.</span></span>

    └───MyLibrary
         ├───lib
         │   └───net40
         │           MyLibrary.dll
         │
         └───runtimes
             ├───win8-x64
             │   ├───lib
             │   │   └───net40
             │   │           MyLibrary.dll
             │   │
             │   └───native
             │           MyNativeLibrary.dll
             │
             └───win8-x86
                 ├───lib
                 │   └───net40
                 │           MyLibrary.dll
                 │
                 └───native
                         MyNativeLibrary.dll

<span data-ttu-id="e31bf-186">위 패키지가 제공되면 다음과 같은 상황이 발생합니다.</span><span class="sxs-lookup"><span data-stu-id="e31bf-186">Given the above package the following things happen:</span></span>

- <span data-ttu-id="e31bf-187">Windows 8이 아닌 경우 `lib/net40/MyLibrary.dll` 어셈블리가 사용됩니다.</span><span class="sxs-lookup"><span data-stu-id="e31bf-187">When not on Windows 8 the `lib/net40/MyLibrary.dll` assembly is used.</span></span>

- <span data-ttu-id="e31bf-188">Windows 8인 경우 `runtimes/win8-<architecture>/lib/MyLibrary.dll`이 사용되고 `native/MyNativeHelper.dll`이 빌드 출력에 복사됩니다.</span><span class="sxs-lookup"><span data-stu-id="e31bf-188">When on Windows 8 the `runtimes/win8-<architecture>/lib/MyLibrary.dll` is used and the `native/MyNativeHelper.dll` is copied to the output of your build.</span></span>

<span data-ttu-id="e31bf-189">위의 예에서 `lib/net40` 어셈블리는 전적으로 관리되는 코드이지만, runtimes 폴더에 있는 어셈블리는 네이티브 도우미 어셈블리를 호출하여 Windows 8 특정 API를 호출합니다.</span><span class="sxs-lookup"><span data-stu-id="e31bf-189">In the example above the `lib/net40` assembly is purely managed code, whilst the assemblies in the runtimes folder will p/invoke into the native helper assembly to call APIs specific to Windows 8.</span></span>

<span data-ttu-id="e31bf-190">단일 `lib` 폴더만 선택되므로 런타임 특정 폴더가 있으면 해당 폴더가 런타임 이외의 특정 `lib`를 통해 선택됩니다.</span><span class="sxs-lookup"><span data-stu-id="e31bf-190">Only a single `lib` folder is ever be picked, so if there is a runtime specific folder it's chosen over non-runtime specific `lib`.</span></span> <span data-ttu-id="e31bf-191">네이티브 폴더는 추가 항목이며, 존재하는 경우 빌드 출력에 복사됩니다.</span><span class="sxs-lookup"><span data-stu-id="e31bf-191">The native folder is additive, if it exists it's copied to the output of the build.</span></span>

## <a name="managed-wrapper"></a><span data-ttu-id="e31bf-192">관리되는 래퍼</span><span class="sxs-lookup"><span data-stu-id="e31bf-192">Managed wrapper</span></span>

<span data-ttu-id="e31bf-193">런타임을 사용하는 또 다른 방법은 전적으로 관리되는 래퍼인 패키지를 네이티브 어셈블리를 통해 제공하는 것입니다.</span><span class="sxs-lookup"><span data-stu-id="e31bf-193">Another way to use runtimes is to ship a package that is purely a managed wrapper over a native assembly.</span></span> <span data-ttu-id="e31bf-194">이 시나리오에서는 다음과 같은 패키지를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="e31bf-194">In this scenario you create a package like the following:</span></span>

    └───MyLibrary
         └───runtimes
             ├───win8-x64
             │   ├───lib
             │   │   └───net451
             │   │           MyLibrary.dll
             │   │
             │   └───native
             │           MyImplementation.dll
             │
             └───win8-x86
                 ├───lib
                 │   └───net451
                 │           MyLibrary.dll
                 │
                 └───native
                         MyImplementation.dll

<span data-ttu-id="e31bf-195">이 경우 해당 네이티브 어셈블리에 종속되지 않는 이 패키지의 구현이 없으므로 해당 폴더와 같은 최상위 `lib` 폴더가 없습니다.</span><span class="sxs-lookup"><span data-stu-id="e31bf-195">In this case there is no top-level `lib` folder as that folder as there is no implementation of this package that doesn't rely on the corresponding native assembly.</span></span> <span data-ttu-id="e31bf-196">두 경우 모두에서 `MyLibrary.dll` 관리되는 어셈블리가 정확히 동일한 경우 최상위 `lib` 폴더에 넣을 수 있습니다. 그러나 win-x86 또는 win-x64가 아닌 플랫폼에 설치되어 있으면, 네이티브 어셈블리의 부족으로 인해 패키지 설치가 실패하지 않으며, 최상위 lib가 사용되지만 네이티브 어셈블리는 복사되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="e31bf-196">If the managed assembly, `MyLibrary.dll`, was exactly the same in both of these cases then we could put it in a top level `lib` folder, but because the lack of a native assembly doesn't cause the package to fail installing if it was installed on a platform that wasn't win-x86 or win-x64 then the top level lib would be used but no native assembly would be copied.</span></span>

## <a name="authoring-packages-for-nuget-2-and-nuget-3"></a><span data-ttu-id="e31bf-197">NuGet 2 및 NuGet 3 패키지 제작</span><span class="sxs-lookup"><span data-stu-id="e31bf-197">Authoring packages for NuGet 2 and NuGet 3</span></span>

<span data-ttu-id="e31bf-198">`packages.config`를 사용하는 프로젝트와 `project.json`을 사용하는 패키지에서 사용할 수 있는 패키지를 만들려는 경우 다음이 적용됩니다.</span><span class="sxs-lookup"><span data-stu-id="e31bf-198">If you want to create a package that can be consumed by projects using `packages.config` as well as packages using `project.json` then the following apply:</span></span>

- <span data-ttu-id="e31bf-199">Ref 및 runtimes는 NuGet 3에서만 작동하며,</span><span class="sxs-lookup"><span data-stu-id="e31bf-199">Ref and runtimes only work on NuGet 3.</span></span> <span data-ttu-id="e31bf-200">NuGet 2에서는 모두 무시됩니다.</span><span class="sxs-lookup"><span data-stu-id="e31bf-200">They are both ignored by NuGet 2.</span></span>

- <span data-ttu-id="e31bf-201">`install.ps1` 또는 `uninstall.ps1`을 사용하여 작동할 수 없습니다.</span><span class="sxs-lookup"><span data-stu-id="e31bf-201">You cannot rely on `install.ps1` or `uninstall.ps1` to function.</span></span> <span data-ttu-id="e31bf-202">이러한 파일은 `packages.config`를 사용하면 실행되지만 `project.json`에서는 무시됩니다.</span><span class="sxs-lookup"><span data-stu-id="e31bf-202">These files execute when using `packages.config`, but are ignored with `project.json`.</span></span> <span data-ttu-id="e31bf-203">따라서 패키지는 실행하지 않고도 사용할 수 있어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="e31bf-203">So your package needs to be usable without them running.</span></span> <span data-ttu-id="e31bf-204">`init.ps1`은 NuGet 3에서 계속 실행됩니다.</span><span class="sxs-lookup"><span data-stu-id="e31bf-204">`init.ps1` still runs on NuGet 3.</span></span>

- <span data-ttu-id="e31bf-205">Targets 및 Props 설치가 서로 다르므로 패키지가 두 클라이언트 모두에서 예상대로 작동하는지 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="e31bf-205">Targets and Props installation is different, so make sure that your package works as expected on both clients.</span></span>

- <span data-ttu-id="e31bf-206">lib의 하위 디렉터리는 NuGet 3에서 TxM이어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="e31bf-206">Subdirectories of lib must be a TxM in NuGet 3.</span></span> <span data-ttu-id="e31bf-207">`lib` 폴더의 루트에 라이브러리를 배치할 수 없습니다.</span><span class="sxs-lookup"><span data-stu-id="e31bf-207">You cannot place libraries at the root of the `lib` folder.</span></span>

- <span data-ttu-id="e31bf-208">Content는 NuGet 3과 함께 자동으로 복사되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="e31bf-208">Content is not copied automatically with NuGet 3.</span></span> <span data-ttu-id="e31bf-209">패키지 소비자가 파일을 직접 복사하거나 작업 실행기와 같은 도구를 사용하여 파일의 복사를 자동화할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="e31bf-209">Consumers of your package could copy the files themselves or use a tool like a task runner to automate copying the files.</span></span>

- <span data-ttu-id="e31bf-210">원본 및 config 파일 변환은 NuGet 3에서 실행되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="e31bf-210">Source and config file transforms are not run by NuGet 3.</span></span>

<span data-ttu-id="e31bf-211">NuGet 2 및 NuGet 3을 지원하는 경우 `minClientVersion`은 패키지가 작동하는 NuGet 2 클라이언트의 가장 낮은 버전이어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="e31bf-211">If you are supporting NuGet 2 and 3 then your `minClientVersion` should be the lowest version of NuGet 2 client that your package works on.</span></span> <span data-ttu-id="e31bf-212">기존 패키지의 경우 변경할 필요가 없습니다.</span><span class="sxs-lookup"><span data-stu-id="e31bf-212">In the case of an existing package it shouldn't need to change.</span></span>