---
title: "NuGet 패키지의 멀티 타기팅 | Microsoft Docs"
author: kraigb
ms.author: kraigb
manager: ghogen
ms.date: 9/27/2017
ms.topic: article
ms.prod: nuget
ms.technology: 
ms.assetid: 2646ffcd-83ae-4086-8915-a7fba3f53e45
description: "단일 NuGet 패키지 내에서 여러 .NET Framework 버전을 대상으로 하는 다양한 방법에 대한 설명입니다."
keywords: "NuGet 패키지 타기팅, .NET Framework 버전, NuGet 및.NET, 여러 프레임워크 대상 지정, NuGet 패키지 만들기"
ms.reviewer:
- karann-msft
- unniravindranathan
ms.openlocfilehash: d23158c6dab838b723764994e94fc21cab52f553
ms.sourcegitcommit: d0ba99bfe019b779b75731bafdca8a37e35ef0d9
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 12/14/2017
---
# <a name="supporting-multiple-net-framework-versions"></a><span data-ttu-id="bcf83-104">여러 .NET Framework 버전 지원</span><span class="sxs-lookup"><span data-stu-id="bcf83-104">Supporting multiple .NET framework versions</span></span>

<span data-ttu-id="bcf83-105">*NuGet 4.0 이상을 사용하는 .NET Core 프로젝트에서 복수 대상 지정에 대한 자세한 내용은 [MSBuild 대상으로 NuGet 압축 및 복원](../schema/msbuild-targets.md)을 참조하세요.*</span><span class="sxs-lookup"><span data-stu-id="bcf83-105">*For .NET Core projects using NuGet 4.0+, see [NuGet pack and restore as MSBuild targets](../schema/msbuild-targets.md) for details on cross-targeting.*</span></span>

<span data-ttu-id="bcf83-106">많은 라이브러리는 특정 버전의 .NET Framework를 대상으로 지정합니다.</span><span class="sxs-lookup"><span data-stu-id="bcf83-106">Many libraries target a specific version of the .NET Framework.</span></span> <span data-ttu-id="bcf83-107">예를 들어 UWP에 관련된 한 버전의 라이브러리 및 .NET Framework 4.6에서 기능을 활용하는 다른 버전의 라이브러리가 있을 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="bcf83-107">For example, you might have one version of your library that's specific to UWP, and another version that takes advantage of features in .NET Framework 4.6.</span></span>

<span data-ttu-id="bcf83-108">이를 수용하기 위해 NuGet에서는 [패키지 만들기](../create-packages/creating-a-package.md#from-a-convention-based-working-directory)에 설명된 규칙 기반 작업 디렉터리 메서드를 사용할 때 단일 패키지에서 여러 버전의 동일한 라이브러리를 설정하도록 지원합니다.</span><span class="sxs-lookup"><span data-stu-id="bcf83-108">To accommodate this, NuGet supports putting multiple versions of the same library in a single package when using the convention-based working directory method described in [Creating a package](../create-packages/creating-a-package.md#from-a-convention-based-working-directory).</span></span>

<span data-ttu-id="bcf83-109">항목 내용:</span><span class="sxs-lookup"><span data-stu-id="bcf83-109">In this topic:</span></span>

- [<span data-ttu-id="bcf83-110">프레임워크 버전 폴더 구조</span><span class="sxs-lookup"><span data-stu-id="bcf83-110">Framework version folder structure</span></span>](#framework-version-folder-structure)
- [<span data-ttu-id="bcf83-111">프로젝트에서 어셈블리 버전 및 대상 프레임워크 일치</span><span class="sxs-lookup"><span data-stu-id="bcf83-111">Matching assembly versions and the target framework in a project</span></span>](#matching-assembly-versions-and-the-target-framework-in-a-project)
- [<span data-ttu-id="bcf83-112">프레임워크 버전에 따라 어셈블리 그룹화</span><span class="sxs-lookup"><span data-stu-id="bcf83-112">Grouping assemblies by framework version</span></span>](#grouping-assemblies-by-framework-version)
- [<span data-ttu-id="bcf83-113">사용할 NuGet 대상 결정</span><span class="sxs-lookup"><span data-stu-id="bcf83-113">Determining which NuGet target to use</span></span>](#determining-which-nuget-target-to-use)
- [<span data-ttu-id="bcf83-114">콘텐츠 파일 및 PowerShell 스크립트</span><span class="sxs-lookup"><span data-stu-id="bcf83-114">Content files and PowerShell scripts</span></span>](#content-files-and-powershell-scripts)


## <a name="framework-version-folder-structure"></a><span data-ttu-id="bcf83-115">프레임워크 버전 폴더 구조</span><span class="sxs-lookup"><span data-stu-id="bcf83-115">Framework version folder structure</span></span>

<span data-ttu-id="bcf83-116">하나의 라이브러리 버전을 포함하거나 여러 프레임워크를 대상으로 하는 패키지를 빌드하는 경우 항상 다음 규칙으로 다른 대/소문자 구분 프레임워크 이름을 사용하여 `lib` 아래에서 하위 폴더를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="bcf83-116">When building a package that contains only one version of a library or target multiple frameworks, you always make subfolders under `lib` using different case-sensitive framework names with the following convention:</span></span>

    lib\{framework name}[{version}]

<span data-ttu-id="bcf83-117">지원되는 이름의 전체 목록은 [대상 프레임워크 참조](../schema/target-frameworks.md#supported-frameworks)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="bcf83-117">For a complete list of supported names, see the [Target Frameworks reference](../schema/target-frameworks.md#supported-frameworks).</span></span>

<span data-ttu-id="bcf83-118">프레임워크에 관련되지 않는 버전의 라이브러리를 포함하거나 루트 `lib` 폴더에 배치하지 않아야 합니다.</span><span class="sxs-lookup"><span data-stu-id="bcf83-118">You should never have a version of the library that is not specific to a framework and placed directly in the root `lib` folder.</span></span> <span data-ttu-id="bcf83-119">(이 기능은 `packages.config`에만 지원됩니다.)</span><span class="sxs-lookup"><span data-stu-id="bcf83-119">(This capability was supported only with `packages.config`).</span></span> <span data-ttu-id="bcf83-120">그렇게 하면 모든 대상 프레임워크와 호환되도록 만들고 어디에나 설치할 수 있습니다. 따라서 예기치 않은 런타임 오류가 발생할 가능성이 높습니다.</span><span class="sxs-lookup"><span data-stu-id="bcf83-120">Doing so would make the compatible with any target framework and allow it to be installed anywhere, likely resulting in unexpected runtime errors.</span></span> <span data-ttu-id="bcf83-121">루트 폴더(예: `lib\abc.dll`) 또는 하위 폴더(예: `lib\abc\abc.dll`)에 어셈블리를 추가하는 작업은 사용되지 않으며 PackagesReference 형식을 사용할 때 무시됩니다.</span><span class="sxs-lookup"><span data-stu-id="bcf83-121">Adding assemblies in the root folder (such as `lib\abc.dll`) or subfolders (such as `lib\abc\abc.dll`) has been deprecated and is ignored when using the PackagesReference format.</span></span>

<span data-ttu-id="bcf83-122">예를 들어 다음 폴더 구조는 프레임워크에 관련된 4개 버전의 어셈블리를 지원합니다.</span><span class="sxs-lookup"><span data-stu-id="bcf83-122">For example, the following folder structure supports four versions of an assembly that are framework-specific:</span></span>

    \lib
        \net46
            \MyAssembly.dll
        \net461
            \MyAssembly.dll
        \uap
            \MyAssembly.dll
        \netcore
            \MyAssembly.dll

<span data-ttu-id="bcf83-123">패키지를 빌드할 때 이러한 파일 중 일부를 쉽게 포함하려면 `.nuspec`의 `<files>` 섹션에서 재귀 `**` 와일드 카드를 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="bcf83-123">To easily include all these files when building the package, use a recursive `**` wildcard in the `<files>` section of your `.nuspec`:</span></span>

```xml
<files>
    <file src="lib\**" target="lib/{framework name}[{version}]" />
</files>
```

### <a name="architecture-specific-folders"></a><span data-ttu-id="bcf83-124">아키텍처 관련 폴더</span><span class="sxs-lookup"><span data-stu-id="bcf83-124">Architecture-specific folders</span></span> 

<span data-ttu-id="bcf83-125">아키텍처 관련 어셈블리, 즉, ARM, x86 및 x64를 대상으로 하는 별도 어셈블리가 있는 경우 `{platform}-{architecture}\lib\{framework}` 또는 `{platform}-{architecture}\native`라는 하위 폴더 내에서 `runtimes`라는 폴더에 배치해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="bcf83-125">If you have architecture-specific assemblies, that is, separate assemblies that target ARM, x86, and x64, you must place them in a folder named `runtimes` within sub-folders named `{platform}-{architecture}\lib\{framework}` or `{platform}-{architecture}\native`.</span></span> <span data-ttu-id="bcf83-126">예를 들어 다음 폴더 구조는 Windows 10 및 `uap10.0` 프레임워크를 대상으로 하는 네이티브 및 관리 DLL을 모두 수용합니다.</span><span class="sxs-lookup"><span data-stu-id="bcf83-126">For example, the following folder structure would accommodate both native and managed DLLs targeting Windows 10 and the `uap10.0` framework:</span></span>

    \runtimes
        \win10-arm
            \native
            \lib\uap10.0
        \win10-x86
            \native
            \lib\uap10.0
        \win10-x64
            \native
            \lib\uap10.0

<span data-ttu-id="bcf83-127">`.nuspec` 매니페스트에서 이러한 파일을 참조하는 예제는 [UWP 패키지 만들기](../Guides/Create-UWP-Packages.md)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="bcf83-127">See [Create UWP Packages](../Guides/Create-UWP-Packages.md) for an example of referencing these files in the `.nuspec` manifest.</span></span>


## <a name="matching-assembly-versions-and-the-target-framework-in-a-project"></a><span data-ttu-id="bcf83-128">프로젝트에서 어셈블리 버전 및 대상 프레임워크 일치</span><span class="sxs-lookup"><span data-stu-id="bcf83-128">Matching assembly versions and the target framework in a project</span></span>

<span data-ttu-id="bcf83-129">NuGet이 여러 어셈블리 버전을 포함하는 패키지를 설치하면 프로젝트의 대상 프레임워크와 어셈블리의 프레임워크 이름을 일치하도록 합니다.</span><span class="sxs-lookup"><span data-stu-id="bcf83-129">When NuGet installs a package that has multiple assembly versions, it tries to match the framework name of the assembly with the target framework of the project.</span></span>

<span data-ttu-id="bcf83-130">일치 항목이 없으면 NuGet은 사용 가능한 경우 프로젝트의 대상 프레임워크 이전에 릴리스된 가장 높은 버전의 어셈블리를 복사합니다.</span><span class="sxs-lookup"><span data-stu-id="bcf83-130">If a match is not found, NuGet copies the assembly for the highest version that is less than or equal to the project's target framework, if available.</span></span> <span data-ttu-id="bcf83-131">호환 가능한 어셈블리를 찾는 경우 NuGet은 적절한 오류 메시지를 반환합니다.</span><span class="sxs-lookup"><span data-stu-id="bcf83-131">If no compatible assembly is found, NuGet returns an appropriate error message.</span></span>

<span data-ttu-id="bcf83-132">예를 들어 패키지에 다음과 같은 폴더 구조가 있다고 가정합니다.</span><span class="sxs-lookup"><span data-stu-id="bcf83-132">For example, consider the following folder structure in a package:</span></span>

    \lib
        \net45
            \MyAssembly.dll
        \net461
            \MyAssembly.dll


<span data-ttu-id="bcf83-133">.NET Framework 4.6을 대상으로 하는 프로젝트에서 이 패키지를 설치하는 경우 NuGet은 `net45` 폴더에 어셈블리를 설치합니다. 4.6 이전에 릴리스된 사용 가능한 가장 높은 버전이기 때문입니다.</span><span class="sxs-lookup"><span data-stu-id="bcf83-133">When installing this package in a project that targets .NET Framework 4.6, NuGet installs the assembly in the `net45` folder, because that's the highest available version that's less than or equal to 4.6.</span></span>

<span data-ttu-id="bcf83-134">반면 프로젝트가 .NET Framework 4.6.1을 대상으로 하는 경우 NuGet은 `net461` 폴더에 어셈블리를 설치합니다.</span><span class="sxs-lookup"><span data-stu-id="bcf83-134">If the project targets .NET Framework 4.6.1, on the other hand, NuGet installs the assembly in the `net461` folder.</span></span>

<span data-ttu-id="bcf83-135">프로젝트가 .NET framework 4.0 이전을 대상으로 하는 경우 NuGet은 호환 가능한 어셈블리를 찾을 수 없는 경우에 적절한 오류 메시지를 throw합니다.</span><span class="sxs-lookup"><span data-stu-id="bcf83-135">If the project targets .NET framework 4.0 and earlier, NuGet throws an appropriate error message for not finding the compatible assembly.</span></span>

## <a name="grouping-assemblies-by-framework-version"></a><span data-ttu-id="bcf83-136">프레임워크 버전에 따라 어셈블리 그룹화</span><span class="sxs-lookup"><span data-stu-id="bcf83-136">Grouping assemblies by framework version</span></span>

<span data-ttu-id="bcf83-137">NuGet은 패키지의 단일 라이브러리 폴더에서 어셈블리를 복사합니다.</span><span class="sxs-lookup"><span data-stu-id="bcf83-137">NuGet copies assemblies from only a single library folder in the package.</span></span> <span data-ttu-id="bcf83-138">예를 들어 패키지에 다음과 같은 폴더 구조가 있다고 가정합니다.</span><span class="sxs-lookup"><span data-stu-id="bcf83-138">For example, suppose a package has the following folder structure:</span></span>

    \lib
        \net40
            \MyAssembly.dll (v1.0)
            \MyAssembly.Core.dll (v1.0)
        \net45
            \MyAssembly.dll (v2.0)

<span data-ttu-id="bcf83-139">.NET Framework 4.5를 대상으로 하는 프로젝트에서 패키지를 설치할 때 `MyAssembly.dll`(v2.0)이 설치된 유일한 어셈블리입니다.</span><span class="sxs-lookup"><span data-stu-id="bcf83-139">When the package is installed in a project that targets .NET Framework 4.5, `MyAssembly.dll` (v2.0) is the only assembly installed.</span></span> <span data-ttu-id="bcf83-140">`MyAssembly.Core.dll`(v1.0)이 `net45` 폴더에 나열되지 않기 때문에 설치되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="bcf83-140">`MyAssembly.Core.dll` (v1.0) is not installed because it's not listed in the `net45` folder.</span></span> <span data-ttu-id="bcf83-141">`MyAssembly.Core.dll`이 2.0 버전의 `MyAssembly.dll`에 병합되기 때문에 NuGet은 이런 방식으로 작동합니다.</span><span class="sxs-lookup"><span data-stu-id="bcf83-141">NuGet behaves this way because `MyAssembly.Core.dll` might have merged into version 2.0 of `MyAssembly.dll`.</span></span>

<span data-ttu-id="bcf83-142">`MyAssembly.Core.dll`을 .NET Framework 4.5에 설치하려는 경우 복사본을 `net45` 폴더에 배치합니다.</span><span class="sxs-lookup"><span data-stu-id="bcf83-142">If you want `MyAssembly.Core.dll` to be installed for .NET Framework 4.5, place a copy in the `net45` folder.</span></span>

## <a name="grouping-assemblies-by-framework-profile"></a><span data-ttu-id="bcf83-143">프레임워크 프로필에 따라 어셈블리 그룹화</span><span class="sxs-lookup"><span data-stu-id="bcf83-143">Grouping assemblies by framework profile</span></span>

<span data-ttu-id="bcf83-144">또한 NuGet은 대시와 프로필 이름을 폴더의 끝에 추가하여 특정 프레임워크 프로필을 대상으로 하도록 지원합니다.</span><span class="sxs-lookup"><span data-stu-id="bcf83-144">NuGet also supports targeting a specific framework profile by appending a dash and the profile name to the end of the folder.</span></span>

    lib\{framework name}-{profile}

<span data-ttu-id="bcf83-145">지원되는 프로필은 다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="bcf83-145">The supported profiles are as follows:</span></span>

- <span data-ttu-id="bcf83-146">`client`: 클라이언트 프로필</span><span class="sxs-lookup"><span data-stu-id="bcf83-146">`client`: Client Profile</span></span>
- <span data-ttu-id="bcf83-147">`full`: 전체 프로필</span><span class="sxs-lookup"><span data-stu-id="bcf83-147">`full`: Full Profile</span></span>
- <span data-ttu-id="bcf83-148">`wp`: Windows Phone</span><span class="sxs-lookup"><span data-stu-id="bcf83-148">`wp`: Windows Phone</span></span>
- <span data-ttu-id="bcf83-149">`cf`: Compact Framework</span><span class="sxs-lookup"><span data-stu-id="bcf83-149">`cf`: Compact Framework</span></span>

## <a name="determining-which-nuget-target-to-use"></a><span data-ttu-id="bcf83-150">사용할 NuGet 대상 결정</span><span class="sxs-lookup"><span data-stu-id="bcf83-150">Determining which NuGet target to use</span></span>

<span data-ttu-id="bcf83-151">이식 가능한 클래스 라이브러리를 대상으로 하는 라이브러리를 패키지할 때 특히 PCL의 하위 집합만 대상으로 하는 경우 폴더 이름 및 `.nuspec` 파일에서 사용해야 하는 NuGet 대상을 결정하는 작업이 까다로울 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="bcf83-151">When packaging libraries targeting the Portable Class Library it can be tricky to determine which NuGet target you should use in your folder names and `.nuspec` file, especially if targeting only a subset of the PCL.</span></span> <span data-ttu-id="bcf83-152">다음 외부 리소스는 이런 기능에 도움이 됩니다.</span><span class="sxs-lookup"><span data-stu-id="bcf83-152">The following external resources will help you with this:</span></span>

- <span data-ttu-id="bcf83-153">[.NET의 프레임워크 프로필](http://blog.stephencleary.com/2012/05/framework-profiles-in-net.html)(stephenclearly.com)</span><span class="sxs-lookup"><span data-stu-id="bcf83-153">[Framework profiles in .NET](http://blog.stephencleary.com/2012/05/framework-profiles-in-net.html) (stephenclearly.com)</span></span>
- <span data-ttu-id="bcf83-154">[이식 가능한 클래스 라이브러리 프로필](http://embed.plnkr.co/03ck2dCtnJogBKHJ9EjY/preview)(plnkr.co): PCL 프로필 및 동등한 해당 NuGet 대상을 열거하는 표</span><span class="sxs-lookup"><span data-stu-id="bcf83-154">[Portable Class Library profiles](http://embed.plnkr.co/03ck2dCtnJogBKHJ9EjY/preview) (plnkr.co): Table enumerating PCL profiles and their equivalent NuGet targets</span></span>
- <span data-ttu-id="bcf83-155">[이식 가능한 클래스 라이브러리 프로필 도구](https://github.com/StephenCleary/PortableLibraryProfiles)(github.com): 시스템에서 사용할 수 있는 PCL 프로필을 결정하는 명령줄 도구</span><span class="sxs-lookup"><span data-stu-id="bcf83-155">[Portable Class Library profiles tool](https://github.com/StephenCleary/PortableLibraryProfiles) (github.com): command line tool for determining PCL profiles available on your system</span></span>

## <a name="content-files-and-powershell-scripts"></a><span data-ttu-id="bcf83-156">콘텐츠 파일 및 PowerShell 스크립트</span><span class="sxs-lookup"><span data-stu-id="bcf83-156">Content files and PowerShell scripts</span></span>

> [!Warning]
> <span data-ttu-id="bcf83-157">변경할 수 있는 콘텐츠 파일 및 스크립트 실행은 `packages.config` 형식에서만 제공됩니다. `project.json` 및 PackagesReference 형식을 사용할 때 제공되지 않고 새 패키지에서 사용하지 말아야 합니다.</span><span class="sxs-lookup"><span data-stu-id="bcf83-157">Mutable content files and script execution are available with the `packages.config` format only; they are deprecated when using `project.json` and PackagesReference formats and should should not be used for any new packages.</span></span>

<span data-ttu-id="bcf83-158">`packages.config`에서 `content` 및 `tools` 폴더 내의 동일한 폴더 규칙을 사용하는 대상 프레임워크에서 콘텐츠 파일 및 PowerShell 스크립트를 그룹화할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="bcf83-158">With `packages.config`, content files and PowerShell scripts can be grouped by target framework using the same folder convention inside the `content` and `tools` folders.</span></span> <span data-ttu-id="bcf83-159">예:</span><span class="sxs-lookup"><span data-stu-id="bcf83-159">For example:</span></span>

    \content
        \net46
            \MyContent.txt
        \net461
            \MyContent461.txt
        \uap
            \MyUWPContent.html
        \netcore
    \tools
        init.ps1
        \net46
            install.ps1
            uninstall.ps1
        \uap
            install.ps1
            uninstall.ps1

<span data-ttu-id="bcf83-160">프레임워크 폴더를 비워 두면 NuGet은 어셈블리 참조 또는 콘텐츠 파일을 추가하거나 해당 프레임워크에서 PowerShell 스크립트를 실행하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="bcf83-160">If a framework folder is left empty, NuGet doesn't add assembly references or content files or run the PowerShell scripts for that framework.</span></span>

> [!Note]
> <span data-ttu-id="bcf83-161">`init.ps1`은 솔루션 수준에서 실행되고 프로젝트를 사용하지 않기 때문에 `tools` 폴더 바로 아래에 배치되야 합니다.</span><span class="sxs-lookup"><span data-stu-id="bcf83-161">Because `init.ps1` is executed at the solution level and not dependent on project, it must be placed directly under the `tools` folder.</span></span> <span data-ttu-id="bcf83-162">프레임워크 폴더 아래에 있는 경우 무시됩니다.</span><span class="sxs-lookup"><span data-stu-id="bcf83-162">It's ignored if placed under a framework folder.</span></span>
