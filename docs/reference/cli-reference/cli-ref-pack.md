---
title: NuGet CLI pack 명령
description: Nuget.exe pack 명령에 대 한 참조
author: karann-msft
ms.author: karann
ms.date: 01/18/2018
ms.topic: reference
ms.openlocfilehash: 2358cedc05520a3ec82a39aef34b6d467e44460b
ms.sourcegitcommit: c81561e93a7be467c1983d639158d4e3dc25b93a
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 03/02/2020
ms.locfileid: "78231164"
---
# <a name="pack-command-nuget-cli"></a><span data-ttu-id="85c03-103">pack 명령(NuGet CLI)</span><span class="sxs-lookup"><span data-stu-id="85c03-103">pack command (NuGet CLI)</span></span>

<span data-ttu-id="85c03-104">**적용 대상:** 패키지 만들기 &bullet; **지원 되는 버전:** 2.7 이상</span><span class="sxs-lookup"><span data-stu-id="85c03-104">**Applies to:** package creation &bullet; **Supported versions:** 2.7+</span></span>

<span data-ttu-id="85c03-105">지정 된 [nuspec](../nuspec.md) 또는 프로젝트 파일을 기반으로 하는 NuGet 패키지를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="85c03-105">Creates a NuGet package based on the specified [.nuspec](../nuspec.md) or project file.</span></span> <span data-ttu-id="85c03-106">`dotnet pack` 명령 ( [Dotnet 명령](../dotnet-Commands.md)참조) 및 `msbuild -t:pack` ( [MSBuild 대상](../msbuild-targets.md)참조)를 대체 항목으로 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="85c03-106">The `dotnet pack` command (see [dotnet Commands](../dotnet-Commands.md)) and `msbuild -t:pack` (see [MSBuild targets](../msbuild-targets.md)) may be used as alternates.</span></span>

> [!Important]
> <span data-ttu-id="85c03-107">[PackageReference](../../consume-packages/package-references-in-project-files.md) 기반 프로젝트의 경우 [`dotnet pack`](../dotnet-Commands.md) 또는 [`msbuild -t:pack`](../msbuild-targets.md) 를 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="85c03-107">Use [`dotnet pack`](../dotnet-Commands.md) or [`msbuild -t:pack`](../msbuild-targets.md) for [PackageReference](../../consume-packages/package-references-in-project-files.md) based projects.</span></span>
> <span data-ttu-id="85c03-108">Mono에서는 프로젝트 파일에서 패키지를 만들 수 없습니다.</span><span class="sxs-lookup"><span data-stu-id="85c03-108">Under Mono, creating a package from a project file is not supported.</span></span> <span data-ttu-id="85c03-109">또한 nuget.exe는 Windows 경로 이름을 변환 하지 않으므로 `.nuspec` 파일의 비로컬 경로를 Unix 스타일 경로로 조정 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="85c03-109">You also need to adjust non-local paths in the `.nuspec` file to Unix-style paths, as nuget.exe doesn't convert Windows pathnames itself.</span></span>

## <a name="usage"></a><span data-ttu-id="85c03-110">사용</span><span class="sxs-lookup"><span data-stu-id="85c03-110">Usage</span></span>

```cli
nuget pack <nuspecPath | projectPath> [options] [-Properties ...]
```

<span data-ttu-id="85c03-111">여기서 `<nuspecPath>` 및 `<projectPath>`는 각각 `.nuspec` 또는 프로젝트 파일을 지정 합니다.</span><span class="sxs-lookup"><span data-stu-id="85c03-111">where `<nuspecPath>` and `<projectPath>` specify the `.nuspec` or project file, respectively.</span></span>

## <a name="options"></a><span data-ttu-id="85c03-112">옵션</span><span class="sxs-lookup"><span data-stu-id="85c03-112">Options</span></span>

| <span data-ttu-id="85c03-113">옵션</span><span class="sxs-lookup"><span data-stu-id="85c03-113">Option</span></span> | <span data-ttu-id="85c03-114">Description</span><span class="sxs-lookup"><span data-stu-id="85c03-114">Description</span></span> |
| --- | --- |
| <span data-ttu-id="85c03-115">BasePath</span><span class="sxs-lookup"><span data-stu-id="85c03-115">BasePath</span></span> | <span data-ttu-id="85c03-116">[Nuspec](../nuspec.md) 파일에 정의 된 파일의 기본 경로를 설정 합니다.</span><span class="sxs-lookup"><span data-stu-id="85c03-116">Sets the base path of the files defined in the [.nuspec](../nuspec.md) file.</span></span> |
| <span data-ttu-id="85c03-117">빌드</span><span class="sxs-lookup"><span data-stu-id="85c03-117">Build</span></span> | <span data-ttu-id="85c03-118">패키지를 빌드하기 전에 프로젝트를 빌드해야 함을 지정 합니다.</span><span class="sxs-lookup"><span data-stu-id="85c03-118">Specifies that the project should be built before building the package.</span></span> |
| <span data-ttu-id="85c03-119">제외</span><span class="sxs-lookup"><span data-stu-id="85c03-119">Exclude</span></span> | <span data-ttu-id="85c03-120">패키지를 만들 때 제외할 와일드 카드 패턴을 하나 이상 지정 합니다.</span><span class="sxs-lookup"><span data-stu-id="85c03-120">Specifies one or more wildcard patterns to exclude when creating a package.</span></span> <span data-ttu-id="85c03-121">둘 이상의 패턴을 지정 하려면-Exclude 플래그를 반복 합니다.</span><span class="sxs-lookup"><span data-stu-id="85c03-121">To specify more than one pattern, repeat the -Exclude flag.</span></span> <span data-ttu-id="85c03-122">아래 예제를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="85c03-122">See example below.</span></span> |
| <span data-ttu-id="85c03-123">ExcludeEmptyDirectories</span><span class="sxs-lookup"><span data-stu-id="85c03-123">ExcludeEmptyDirectories</span></span> | <span data-ttu-id="85c03-124">패키지를 빌드할 때 빈 디렉터리가 포함 되지 않도록 합니다.</span><span class="sxs-lookup"><span data-stu-id="85c03-124">Prevents inclusion of empty directories when building the package.</span></span> |
| <span data-ttu-id="85c03-125">ForceEnglishOutput</span><span class="sxs-lookup"><span data-stu-id="85c03-125">ForceEnglishOutput</span></span> | <span data-ttu-id="85c03-126">*(3.5 +)* 고정 영어 기반 문화권을 사용 하 여 nuget.exe를 실행 합니다.</span><span class="sxs-lookup"><span data-stu-id="85c03-126">*(3.5+)* Forces nuget.exe to run using an invariant, English-based culture.</span></span> |
| <span data-ttu-id="85c03-127">ConfigFile</span><span class="sxs-lookup"><span data-stu-id="85c03-127">ConfigFile</span></span> | <span data-ttu-id="85c03-128">Pack 명령의 구성 파일을 지정 합니다.</span><span class="sxs-lookup"><span data-stu-id="85c03-128">Specify the configuration file for the pack command.</span></span> |
| <span data-ttu-id="85c03-129">도움말</span><span class="sxs-lookup"><span data-stu-id="85c03-129">Help</span></span> | <span data-ttu-id="85c03-130">명령어에 대한 도움말을 표시합니다.</span><span class="sxs-lookup"><span data-stu-id="85c03-130">Displays help information for the command.</span></span> |
| <span data-ttu-id="85c03-131">IncludeReferencedProjects</span><span class="sxs-lookup"><span data-stu-id="85c03-131">IncludeReferencedProjects</span></span> | <span data-ttu-id="85c03-132">빌드된 패키지에 종속성 또는 패키지의 일부로 참조 된 프로젝트를 포함 해야 함을 나타냅니다.</span><span class="sxs-lookup"><span data-stu-id="85c03-132">Indicates that the built package should include referenced projects either as dependencies or as part of the package.</span></span> <span data-ttu-id="85c03-133">참조 된 프로젝트에 프로젝트와 동일한 이름을 가진 해당 `.nuspec` 파일이 있는 경우 참조 된 프로젝트가 종속성으로 추가 됩니다.</span><span class="sxs-lookup"><span data-stu-id="85c03-133">If a referenced project has a corresponding `.nuspec` file that has the same name as the project, then that referenced project is added as a dependency.</span></span> <span data-ttu-id="85c03-134">그렇지 않으면 참조 된 프로젝트가 패키지의 일부로 추가 됩니다.</span><span class="sxs-lookup"><span data-stu-id="85c03-134">Otherwise, the referenced project is added as part of the package.</span></span> |
| <span data-ttu-id="85c03-135">MinClientVersion</span><span class="sxs-lookup"><span data-stu-id="85c03-135">MinClientVersion</span></span> | <span data-ttu-id="85c03-136">만든 패키지에 대 한 *minClientVersion* 특성을 설정 합니다.</span><span class="sxs-lookup"><span data-stu-id="85c03-136">Set the *minClientVersion* attribute for the created package.</span></span> <span data-ttu-id="85c03-137">이 값은 `.nuspec` 파일에서 기존 *minClientVersion* 특성 (있는 경우)의 값을 재정의 합니다.</span><span class="sxs-lookup"><span data-stu-id="85c03-137">This value will override the value of the existing *minClientVersion* attribute (if any) in the `.nuspec` file.</span></span> |
| <span data-ttu-id="85c03-138">MSBuildPath</span><span class="sxs-lookup"><span data-stu-id="85c03-138">MSBuildPath</span></span> | <span data-ttu-id="85c03-139">*(4.0 이상)* 명령에 사용할 MSBuild의 경로를 지정 합니다. `-MSBuildVersion`보다 우선 합니다.</span><span class="sxs-lookup"><span data-stu-id="85c03-139">*(4.0+)* Specifies the path of MSBuild to use with the command, taking precedence over `-MSBuildVersion`.</span></span> |
| <span data-ttu-id="85c03-140">MSBuildVersion</span><span class="sxs-lookup"><span data-stu-id="85c03-140">MSBuildVersion</span></span> | <span data-ttu-id="85c03-141">*(3.2 이상)* 이 명령에 사용할 MSBuild의 버전을 지정 합니다.</span><span class="sxs-lookup"><span data-stu-id="85c03-141">*(3.2+)* Specifies the version of MSBuild to be used with this command.</span></span> <span data-ttu-id="85c03-142">지원 되는 값은 4, 12, 14, 15.1, 15.3, 15.4, 15.5, 15.6, 15.7, 15.8, 15.9입니다.</span><span class="sxs-lookup"><span data-stu-id="85c03-142">Supported values are 4, 12, 14, 15.1, 15.3, 15.4, 15.5, 15.6, 15.7, 15.8, 15.9.</span></span> <span data-ttu-id="85c03-143">기본적으로 경로에 MSBuild가 선택 되어 있으며, 그렇지 않은 경우 기본적으로 설치 되어 있는 MSBuild의 가장 높은 버전으로 설정 됩니다.</span><span class="sxs-lookup"><span data-stu-id="85c03-143">By default the MSBuild in your path is picked, otherwise it defaults to the highest installed version of MSBuild.</span></span> |
| <span data-ttu-id="85c03-144">NoDefaultExcludes</span><span class="sxs-lookup"><span data-stu-id="85c03-144">NoDefaultExcludes</span></span> | <span data-ttu-id="85c03-145">`.svn` 및 `.gitignore`와 같이 점으로 시작 하는 NuGet 패키지 파일 및 파일 및 폴더의 기본 제외를 방지 합니다.</span><span class="sxs-lookup"><span data-stu-id="85c03-145">Prevents default exclusion of NuGet package files and files and folders starting with a dot, such as `.svn` and `.gitignore`.</span></span> |
| <span data-ttu-id="85c03-146">NoPackageAnalysis</span><span class="sxs-lookup"><span data-stu-id="85c03-146">NoPackageAnalysis</span></span> | <span data-ttu-id="85c03-147">패키지를 빌드한 후 팩에서 패키지 분석을 실행하지 않아야 함을 지정합니다.</span><span class="sxs-lookup"><span data-stu-id="85c03-147">Specifies that pack should not run package analysis after building the package.</span></span> |
| <span data-ttu-id="85c03-148">OutputDirectory</span><span class="sxs-lookup"><span data-stu-id="85c03-148">OutputDirectory</span></span> | <span data-ttu-id="85c03-149">만들어진 패키지가 저장 되는 폴더를 지정 합니다.</span><span class="sxs-lookup"><span data-stu-id="85c03-149">Specifies the folder in which the created package is stored.</span></span> <span data-ttu-id="85c03-150">폴더를 지정 하지 않으면 현재 폴더가 사용 됩니다.</span><span class="sxs-lookup"><span data-stu-id="85c03-150">If no folder is specified, the current folder is used.</span></span> |
| <span data-ttu-id="85c03-151">속성</span><span class="sxs-lookup"><span data-stu-id="85c03-151">Properties</span></span> | <span data-ttu-id="85c03-152">다른 옵션 다음에 오는 명령줄에서 마지막에 표시 되어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="85c03-152">Should appear last on the command line after other options.</span></span> <span data-ttu-id="85c03-153">프로젝트 파일의 값을 재정의 하는 속성의 목록을 지정 합니다. 속성 이름에 대 한 [일반적인 MSBuild 프로젝트 속성](/visualstudio/msbuild/common-msbuild-project-properties) 을 참조 하세요.</span><span class="sxs-lookup"><span data-stu-id="85c03-153">Specifies a list of properties that override values in the project file; see [Common MSBuild Project Properties](/visualstudio/msbuild/common-msbuild-project-properties) for property names.</span></span> <span data-ttu-id="85c03-154">여기에 있는 Properties 인수는 세미콜론으로 구분 된 토큰 = 값 쌍의 목록이 며,이 목록은 `.nuspec` 파일의 각 `$token$` 발생이 지정 된 값으로 바뀝니다.</span><span class="sxs-lookup"><span data-stu-id="85c03-154">The Properties argument here is a list of token=value pairs, separated by semicolons, where each occurrence of `$token$` in the `.nuspec` file will be replaced with the given value.</span></span> <span data-ttu-id="85c03-155">값은 따옴표로 묶인 문자열일 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="85c03-155">Values can be strings in quotation marks.</span></span> <span data-ttu-id="85c03-156">"구성" 속성의 경우 기본값은 "Debug"입니다.</span><span class="sxs-lookup"><span data-stu-id="85c03-156">Note that for the "Configuration" property, the default is "Debug".</span></span> <span data-ttu-id="85c03-157">릴리스 구성으로 변경 하려면 `-Properties Configuration=Release`을 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="85c03-157">To change to a Release configuration, use `-Properties Configuration=Release`.</span></span> <span data-ttu-id="85c03-158">**일반적**으로 이러한 속성은 비정상적인 동작을 방지 하기 위해 해당 `nuget build`중에 사용 된 것과 동일 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="85c03-158">**In general**, Properties should be the same that were used during the corresponding `nuget build`, in order to avoid potentially strange behavior.</span></span> |
| <span data-ttu-id="85c03-159">접미사</span><span class="sxs-lookup"><span data-stu-id="85c03-159">Suffix</span></span> | <span data-ttu-id="85c03-160">*(3.4.4 +)* 일반적으로 빌드 또는 기타 시험판 식별자를 추가 하는 데 사용 되는 내부적으로 생성 된 버전 번호에 접미사를 추가 합니다.</span><span class="sxs-lookup"><span data-stu-id="85c03-160">*(3.4.4+)* Appends a suffix to the internally generated version number, typically used for appending build or other pre-release identifiers.</span></span> <span data-ttu-id="85c03-161">예를 들어 `-suffix nightly`를 사용 하면 `1.2.3-nightly`같은 버전 번호를 사용 하 여 패키지를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="85c03-161">For example, using `-suffix nightly` will create a package with a version number like `1.2.3-nightly`.</span></span> <span data-ttu-id="85c03-162">서로 다른 버전의 NuGet 및 NuGet 패키지 관리자와의 경고, 오류 및 잠재적 비 호환성을 방지 하려면 접미사를 문자로 시작 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="85c03-162">Suffixes must start with a letter to avoid warnings, errors, and potential incompatibilities with different versions of NuGet and the NuGet Package Manager.</span></span> |
| <span data-ttu-id="85c03-163">Symbols</span><span class="sxs-lookup"><span data-stu-id="85c03-163">Symbols</span></span> | <span data-ttu-id="85c03-164">패키지에 원본 및 기호가 포함 되도록 지정 합니다.</span><span class="sxs-lookup"><span data-stu-id="85c03-164">Specifies that the package contains sources and symbols.</span></span> <span data-ttu-id="85c03-165">`.nuspec` 파일에서 사용 하는 경우 일반 NuGet 패키지 파일 및 해당 기호 패키지를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="85c03-165">When used with a `.nuspec` file, this creates a regular NuGet package file and the corresponding symbols package.</span></span> <span data-ttu-id="85c03-166">기본적으로 [레거시 기호 패키지](../../create-packages/Symbol-Packages.md)를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="85c03-166">By default it creates a [legacy symbol package](../../create-packages/Symbol-Packages.md).</span></span> <span data-ttu-id="85c03-167">기호 패키지에 대한 새 권장 형식은 .snupkg입니다.</span><span class="sxs-lookup"><span data-stu-id="85c03-167">The new recommended format for symbol packages is .snupkg.</span></span> <span data-ttu-id="85c03-168">[기호 패키지(.snupkg) 만들기](../../create-packages/Symbol-Packages-snupkg.md)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="85c03-168">See [Creating symbol packages (.snupkg)](../../create-packages/Symbol-Packages-snupkg.md).</span></span> |
| <span data-ttu-id="85c03-169">도구</span><span class="sxs-lookup"><span data-stu-id="85c03-169">Tool</span></span> | <span data-ttu-id="85c03-170">프로젝트의 출력 파일을 `tool` 폴더에 배치 하도록 지정 합니다.</span><span class="sxs-lookup"><span data-stu-id="85c03-170">Specifies that the output files of the project should be placed in the `tool` folder.</span></span> |
| <span data-ttu-id="85c03-171">자세한 정도</span><span class="sxs-lookup"><span data-stu-id="85c03-171">Verbosity</span></span> | <span data-ttu-id="85c03-172">출력에 표시 되는 세부 정보의 양을 지정 합니다. *보통*, *자동*, *자세히*입니다.</span><span class="sxs-lookup"><span data-stu-id="85c03-172">Specifies the amount of detail displayed in the output: *normal*, *quiet*, *detailed*.</span></span> |
| <span data-ttu-id="85c03-173">버전</span><span class="sxs-lookup"><span data-stu-id="85c03-173">Version</span></span> | <span data-ttu-id="85c03-174">`.nuspec` 파일에서 버전 번호를 재정의 합니다.</span><span class="sxs-lookup"><span data-stu-id="85c03-174">Overrides the version number from the `.nuspec` file.</span></span> |

<span data-ttu-id="85c03-175">[환경 변수](cli-ref-environment-variables.md) 참조</span><span class="sxs-lookup"><span data-stu-id="85c03-175">Also see [Environment variables](cli-ref-environment-variables.md)</span></span>

## <a name="excluding-development-dependencies"></a><span data-ttu-id="85c03-176">개발 종속성 제외</span><span class="sxs-lookup"><span data-stu-id="85c03-176">Excluding development dependencies</span></span>

<span data-ttu-id="85c03-177">일부 NuGet 패키지는 사용자 고유의 라이브러리를 작성 하는 데 도움이 되는 개발 종속성으로 유용 하지만 실제 패키지 종속성으로 반드시 필요한 것은 아닙니다.</span><span class="sxs-lookup"><span data-stu-id="85c03-177">Some NuGet packages are useful as development dependencies, which help you author your own library, but aren't necessarily needed as actual package dependencies.</span></span>

<span data-ttu-id="85c03-178">`pack` 명령은 `developmentDependency` 특성이 `true`로 설정 된 `packages.config`의 `package` 항목을 무시 합니다.</span><span class="sxs-lookup"><span data-stu-id="85c03-178">The `pack` command will ignore `package` entries in `packages.config` that have the `developmentDependency` attribute set to `true`.</span></span> <span data-ttu-id="85c03-179">이러한 항목은 생성 된 패키지에 종속성으로 포함 되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="85c03-179">These entries will not be include as a dependencies in the created package.</span></span>

<span data-ttu-id="85c03-180">예를 들어 소스 프로젝트에서 다음 `packages.config` 파일을 고려 합니다.</span><span class="sxs-lookup"><span data-stu-id="85c03-180">For example, consider the following `packages.config` file in the source project:</span></span>

```xml
<?xml version="1.0" encoding="utf-8"?>
<packages>
    <package id="jQuery" version="1.5.2" />
    <package id="netfx-Guard" version="1.3.3.2" developmentDependency="true" />
    <package id="microsoft-web-helpers" version="1.15" />
</packages>
```

<span data-ttu-id="85c03-181">이 프로젝트의 `nuget pack`에 의해 만들어진 패키지는 `jQuery` 및 `microsoft-web-helpers`에 대 한 종속성을 가지 지만 `netfx-Guard`하지는 않습니다.</span><span class="sxs-lookup"><span data-stu-id="85c03-181">For this project, the package created by `nuget pack` will have a dependency on `jQuery` and `microsoft-web-helpers` but not `netfx-Guard`.</span></span>

## <a name="suppressing-pack-warnings"></a><span data-ttu-id="85c03-182">Pack 경고 표시 안 함</span><span class="sxs-lookup"><span data-stu-id="85c03-182">Suppressing pack warnings</span></span>

<span data-ttu-id="85c03-183">Pack 작업 중에 모든 NuGet 경고를 해결 하는 것이 좋지만 특정 한 경우에는이를 억제 하는 것이 좋습니다.</span><span class="sxs-lookup"><span data-stu-id="85c03-183">While it is recommended that you resolve all NuGet warnings during your pack operations, in certain situations suppressing them is warranted.</span></span>

<span data-ttu-id="85c03-184">이렇게 하려면 다음과 같은 방법을 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="85c03-184">You can achieve that in the following way:</span></span> 

> <span data-ttu-id="85c03-185">nuget.exe 팩 패키지. nuspec-Properties NoWarn = NU5104</span><span class="sxs-lookup"><span data-stu-id="85c03-185">nuget.exe pack package.nuspec -Properties NoWarn=NU5104</span></span>

## <a name="examples"></a><span data-ttu-id="85c03-186">예</span><span class="sxs-lookup"><span data-stu-id="85c03-186">Examples</span></span>

```cli
nuget pack

nuget pack foo.nuspec

nuget pack foo.csproj

nuget pack foo.csproj -Properties Configuration=Release

nuget pack foo.csproj -Build -Symbols -Properties owners=janedoe,xiaop;version="1.0.5"

# Create a package from project foo.csproj, using MSBuild version 12 to build the project
nuget pack foo.csproj -Build -Symbols -MSBuildVersion 12 -Properties owners=janedoe,xiaop;version="1.0.5"

# Create a package from project foo.nuspec and the corresponding symbol package using the new recommended format .snupkg
nuget pack foo.nuspec -Symbols -SymbolPackageFormat snupkg

nuget pack foo.nuspec -Version 2.1.0

nuget pack foo.nuspec -Version 1.0.0 -MinClientVersion 2.5

nuget pack Package.nuspec -exclude "*.exe" -exclude "*.bat"
```
