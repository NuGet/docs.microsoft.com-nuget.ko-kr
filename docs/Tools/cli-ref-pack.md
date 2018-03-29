---
title: NuGet CLI 팩 명령을 | Microsoft Docs
author: kraigb
ms.author: kraigb
manager: ghogen
ms.date: 01/18/2018
ms.topic: reference
ms.prod: nuget
ms.technology: ''
description: Nuget.exe 팩 명령에 대 한 참조
keywords: nuget 팩 참조 팩 명령
ms.reviewer:
- karann-msft
- unniravindranathan
ms.workload:
- dotnet
- aspnet
ms.openlocfilehash: 14ecf724477f652275eb68a090bb57b8640d4a8a
ms.sourcegitcommit: beb229893559824e8abd6ab16707fd5fe1c6ac26
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 03/28/2018
---
# <a name="pack-command-nuget-cli"></a><span data-ttu-id="4fa1e-104">팩 명령 (NuGet CLI)</span><span class="sxs-lookup"><span data-stu-id="4fa1e-104">pack command (NuGet CLI)</span></span>

<span data-ttu-id="4fa1e-105">**적용 대상:** 패키지 만들기가 &bullet; **지원 되는 버전:** 2.7 +</span><span class="sxs-lookup"><span data-stu-id="4fa1e-105">**Applies to:** package creation &bullet; **Supported versions:** 2.7+</span></span>

<span data-ttu-id="4fa1e-106">지정 된 기준 NuGet 패키지를 만들어 `.nuspec` 또는 프로젝트 파일입니다.</span><span class="sxs-lookup"><span data-stu-id="4fa1e-106">Creates a NuGet package based on the specified `.nuspec` or project file.</span></span> <span data-ttu-id="4fa1e-107">`dotnet pack` 명령 (참조 [dotnet 명령을](dotnet-Commands.md)) 및 `msbuild /t:pack` (참조 [MSBuild 대상](../reference/msbuild-targets.md)) 안으로 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="4fa1e-107">The `dotnet pack` command (see [dotnet Commands](dotnet-Commands.md)) and `msbuild /t:pack` (see [MSBuild targets](../reference/msbuild-targets.md)) may be used as alternates.</span></span>

> [!Important]
> <span data-ttu-id="4fa1e-108">모노, 아래에서 프로젝트 파일에서 패키지를 만드는 지원 되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="4fa1e-108">Under Mono, creating a package from a project file is not supported.</span></span> <span data-ttu-id="4fa1e-109">로컬이 아닌 경로 조정 해야 할 수도 있습니다는 `.nuspec` Unix 스타일 경로 파일 nuget.exe Windows 경로 이름 자체를 변환 하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="4fa1e-109">You also need to adjust non-local paths in the `.nuspec` file to Unix-style paths, as nuget.exe doesn't convert Windows pathnames itself.</span></span>

## <a name="usage"></a><span data-ttu-id="4fa1e-110">사용법</span><span class="sxs-lookup"><span data-stu-id="4fa1e-110">Usage</span></span>

```cli
nuget pack <nuspecPath | projectPath> [options]
```

<span data-ttu-id="4fa1e-111">여기서 `<nuspecPath>` 및 `<projectPath>` 지정는 `.nuspec` 또는 프로젝트 파일을 각각.</span><span class="sxs-lookup"><span data-stu-id="4fa1e-111">where `<nuspecPath>` and `<projectPath>` specify the `.nuspec` or project file, respectively.</span></span>

## <a name="options"></a><span data-ttu-id="4fa1e-112">옵션</span><span class="sxs-lookup"><span data-stu-id="4fa1e-112">Options</span></span>

| <span data-ttu-id="4fa1e-113">옵션</span><span class="sxs-lookup"><span data-stu-id="4fa1e-113">Option</span></span> | <span data-ttu-id="4fa1e-114">설명</span><span class="sxs-lookup"><span data-stu-id="4fa1e-114">Description</span></span> |
| --- | --- |
| <span data-ttu-id="4fa1e-115">BasePath</span><span class="sxs-lookup"><span data-stu-id="4fa1e-115">BasePath</span></span> | <span data-ttu-id="4fa1e-116">에 정의 된 파일의 기본 경로 설정의 `.nuspec` 파일입니다.</span><span class="sxs-lookup"><span data-stu-id="4fa1e-116">Sets the base path of the files defined in the `.nuspec` file.</span></span> |
| <span data-ttu-id="4fa1e-117">빌드</span><span class="sxs-lookup"><span data-stu-id="4fa1e-117">Build</span></span> | <span data-ttu-id="4fa1e-118">패키지를 빌드하기 전에 프로젝트를 빌드해야 함을 지정 합니다.</span><span class="sxs-lookup"><span data-stu-id="4fa1e-118">Specifies that the project should be built before building the package.</span></span> |
| <span data-ttu-id="4fa1e-119">제외</span><span class="sxs-lookup"><span data-stu-id="4fa1e-119">Exclude</span></span> | <span data-ttu-id="4fa1e-120">패키지를 만들 때를 제외 하려면 와일드 카드 패턴을 하나 이상 지정 합니다.</span><span class="sxs-lookup"><span data-stu-id="4fa1e-120">Specifies one or more wildcard patterns to exclude when creating a package.</span></span> <span data-ttu-id="4fa1e-121">둘 이상의 패턴을 지정 하려면 반복-Exclude 플래그입니다.</span><span class="sxs-lookup"><span data-stu-id="4fa1e-121">To specify more than one pattern, repeat the -Exclude flag.</span></span> <span data-ttu-id="4fa1e-122">아래 예제를 참조 하십시오.</span><span class="sxs-lookup"><span data-stu-id="4fa1e-122">See example below.</span></span> |
| <span data-ttu-id="4fa1e-123">ExcludeEmptyDirectories</span><span class="sxs-lookup"><span data-stu-id="4fa1e-123">ExcludeEmptyDirectories</span></span> | <span data-ttu-id="4fa1e-124">패키지를 작성 하는 경우 빈 디렉터리를 포함을 하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="4fa1e-124">Prevents inclusion of empty directories when building the package.</span></span> |
| <span data-ttu-id="4fa1e-125">ForceEnglishOutput</span><span class="sxs-lookup"><span data-stu-id="4fa1e-125">ForceEnglishOutput</span></span> | <span data-ttu-id="4fa1e-126">*(3.5 +)*  고정, 영어 기반 문화권을 사용 하 여 실행할 nuget.exe를 강제로 수행 합니다.</span><span class="sxs-lookup"><span data-stu-id="4fa1e-126">*(3.5+)* Forces nuget.exe to run using an invariant, English-based culture.</span></span> |
| <span data-ttu-id="4fa1e-127">도움말</span><span class="sxs-lookup"><span data-stu-id="4fa1e-127">Help</span></span> | <span data-ttu-id="4fa1e-128">도움말의 명령에 대 한 정보를 표시 합니다.</span><span class="sxs-lookup"><span data-stu-id="4fa1e-128">Displays help information for the command.</span></span> |
| <span data-ttu-id="4fa1e-129">IncludeReferencedProjects</span><span class="sxs-lookup"><span data-stu-id="4fa1e-129">IncludeReferencedProjects</span></span> | <span data-ttu-id="4fa1e-130">종속성으로 또는 패키지의 일부로 서 빌드된 패키지에서 참조 된 프로젝트를 포함 해야 함을 나타냅니다.</span><span class="sxs-lookup"><span data-stu-id="4fa1e-130">Indicates that the built package should include referenced projects either as dependencies or as part of the package.</span></span> <span data-ttu-id="4fa1e-131">참조 된 프로젝트에 해당 하는 경우 `.nuspec` 참조 된 프로젝트는 종속성으로 추가 됩니다 한 다음 프로젝트와 동일한 이름을 가진 파일을 합니다.</span><span class="sxs-lookup"><span data-stu-id="4fa1e-131">If a referenced project has a corresponding `.nuspec` file that has the same name as the project, then that referenced project is added as a dependency.</span></span> <span data-ttu-id="4fa1e-132">그렇지 않은 경우 참조 된 프로젝트는 패키지의 일부로 추가 됩니다.</span><span class="sxs-lookup"><span data-stu-id="4fa1e-132">Otherwise, the referenced project is added as part of the package.</span></span> |
| <span data-ttu-id="4fa1e-133">MinClientVersion</span><span class="sxs-lookup"><span data-stu-id="4fa1e-133">MinClientVersion</span></span> | <span data-ttu-id="4fa1e-134">설정의 *minClientVersion* 생성된 된 패키지에 대 한 특성입니다.</span><span class="sxs-lookup"><span data-stu-id="4fa1e-134">Set the *minClientVersion* attribute for the created package.</span></span> <span data-ttu-id="4fa1e-135">이 값은 기존 값을 재정의 하는 것 *minClientVersion* 특성 (있는 경우)에 `.nuspec` 파일입니다.</span><span class="sxs-lookup"><span data-stu-id="4fa1e-135">This value will override the value of the existing *minClientVersion* attribute (if any) in the `.nuspec` file.</span></span> |
| <span data-ttu-id="4fa1e-136">MSBuildPath</span><span class="sxs-lookup"><span data-stu-id="4fa1e-136">MSBuildPath</span></span> | <span data-ttu-id="4fa1e-137">*(4.0 이상)*  우선 순위를 차지 명령으로 사용 하는 MSBuild의 경로 지정 `-MSBuildVersion`합니다.</span><span class="sxs-lookup"><span data-stu-id="4fa1e-137">*(4.0+)* Specifies the path of MSBuild to use with the command, taking precedence over `-MSBuildVersion`.</span></span> |
| <span data-ttu-id="4fa1e-138">MSBuildVersion</span><span class="sxs-lookup"><span data-stu-id="4fa1e-138">MSBuildVersion</span></span> | <span data-ttu-id="4fa1e-139">*(3.2 +)*  이 명령과 함께 사용할 MSBuild의 버전을 지정 합니다.</span><span class="sxs-lookup"><span data-stu-id="4fa1e-139">*(3.2+)* Specifies the version of MSBuild to be used with this command.</span></span> <span data-ttu-id="4fa1e-140">지원 되는 값은 4, 12, 14, 15입니다.</span><span class="sxs-lookup"><span data-stu-id="4fa1e-140">Supported values are 4, 12, 14, 15.</span></span> <span data-ttu-id="4fa1e-141">경로에 MSBuild 선택은 기본적으로 그렇지 않은 경우 기본값이 가장 높은 설치 된 버전의 MSBuild 됩니다.</span><span class="sxs-lookup"><span data-stu-id="4fa1e-141">By default the MSBuild in your path is picked, otherwise it defaults to the highest installed version of MSBuild.</span></span> |
| <span data-ttu-id="4fa1e-142">NoDefaultExcludes</span><span class="sxs-lookup"><span data-stu-id="4fa1e-142">NoDefaultExcludes</span></span> | <span data-ttu-id="4fa1e-143">NuGet의 기본 예외 방지 패키지 파일 및 파일 및 폴더와 같은 점으로 시작 `.svn` 및 `.gitignore`합니다.</span><span class="sxs-lookup"><span data-stu-id="4fa1e-143">Prevents default exclusion of NuGet package files and files and folders starting with a dot, such as `.svn` and `.gitignore`.</span></span> |
| <span data-ttu-id="4fa1e-144">NoPackageAnalysis</span><span class="sxs-lookup"><span data-stu-id="4fa1e-144">NoPackageAnalysis</span></span> | <span data-ttu-id="4fa1e-145">패키지를 빌드한 후 팩에서 패키지 분석을 실행하지 않아야 함을 지정합니다.</span><span class="sxs-lookup"><span data-stu-id="4fa1e-145">Specifies that pack should not run package analysis after building the package.</span></span> |
| <span data-ttu-id="4fa1e-146">OutputDirectory</span><span class="sxs-lookup"><span data-stu-id="4fa1e-146">OutputDirectory</span></span> | <span data-ttu-id="4fa1e-147">생성된 된 패키지 저장 된 폴더를 지정 합니다.</span><span class="sxs-lookup"><span data-stu-id="4fa1e-147">Specifies the folder in which the created package is stored.</span></span> <span data-ttu-id="4fa1e-148">없는 폴더를 지정 하는 경우 현재 폴더가 사용 됩니다.</span><span class="sxs-lookup"><span data-stu-id="4fa1e-148">If no folder is specified, the current folder is used.</span></span> |
| <span data-ttu-id="4fa1e-149">속성</span><span class="sxs-lookup"><span data-stu-id="4fa1e-149">Properties</span></span> | <span data-ttu-id="4fa1e-150">프로젝트 파일;의 값을 재정의 하는 속성의 목록을 지정 합니다. 참조 [일반적인 MSBuild 프로젝트 속성](/visualstudio/msbuild/common-msbuild-project-properties) 속성 이름에 대 한 합니다.</span><span class="sxs-lookup"><span data-stu-id="4fa1e-150">Specifies a list of properties that override values in the project file; see [Common MSBuild Project Properties](/visualstudio/msbuild/common-msbuild-project-properties) for property names.</span></span> <span data-ttu-id="4fa1e-151">여기에 속성 인수는 토큰의 목록 = 값 쌍을 세미콜론으로 구분 하 여기서 발생할 때마다 `$token$` 에 `.nuspec` 파일이 지정된 된 값으로 바뀝니다.</span><span class="sxs-lookup"><span data-stu-id="4fa1e-151">The Properties argument here is a list of token=value pairs, separated by semicolons, where each occurrence of `$token$` in the `.nuspec` file will be replaced with the given value.</span></span> <span data-ttu-id="4fa1e-152">따옴표로 문자열 일 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="4fa1e-152">Values can be strings in quotation marks.</span></span> <span data-ttu-id="4fa1e-153">"구성" 속성에 대 한 기본값은 "Debug" note 합니다.</span><span class="sxs-lookup"><span data-stu-id="4fa1e-153">Note that for the "Configuration" property, the default is "Debug".</span></span> <span data-ttu-id="4fa1e-154">릴리스 구성으로 변경 하려면 사용 `-Properties Configuration=Release`합니다.</span><span class="sxs-lookup"><span data-stu-id="4fa1e-154">To change to a Release configuration, use `-Properties Configuration=Release`.</span></span> |
| <span data-ttu-id="4fa1e-155">접미사</span><span class="sxs-lookup"><span data-stu-id="4fa1e-155">Suffix</span></span> | <span data-ttu-id="4fa1e-156">*(3.4.4+)*  빌드 또는 기타 시험판 버전 식별자를 추가 하기 위한 일반적으로 사용 되는 내부적으로 생성 된 버전 번호에 접미사를 추가 합니다.</span><span class="sxs-lookup"><span data-stu-id="4fa1e-156">*(3.4.4+)* Appends a suffix to the internally generated version number, typically used for appending build or other pre-release identifiers.</span></span> <span data-ttu-id="4fa1e-157">예를 들어,를 사용 하 여 `-suffix nightly` 버전 번호 like 패키지를 만듭니다 `1.2.3-nightly`합니다.</span><span class="sxs-lookup"><span data-stu-id="4fa1e-157">For example, using `-suffix nightly` will create a package with a version number like `1.2.3-nightly`.</span></span> <span data-ttu-id="4fa1e-158">접미사는 경고, 오류 및 다른 버전의 NuGet과 NuGet 패키지 관리자 잠재적인 호환성 문제를 방지 하기 위해 문자로 시작 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="4fa1e-158">Suffixes must start with a letter to avoid warnings, errors, and potential incompatibilities with different versions of NuGet and the NuGet Package Manager.</span></span> |
| <span data-ttu-id="4fa1e-159">기호</span><span class="sxs-lookup"><span data-stu-id="4fa1e-159">Symbols</span></span> | <span data-ttu-id="4fa1e-160">소스 및 기호 패키지에 포함 되도록 지정 합니다.</span><span class="sxs-lookup"><span data-stu-id="4fa1e-160">Specifies that the package contains sources and symbols.</span></span> <span data-ttu-id="4fa1e-161">와 함께 사용할 경우는 `.nuspec` 해당 기호 패키지 하 고 파일을 일반 NuGet 패키지 파일이 만들어집니다.</span><span class="sxs-lookup"><span data-stu-id="4fa1e-161">When used with a `.nuspec` file, this creates a regular NuGet package file and the corresponding symbols package.</span></span> |
| <span data-ttu-id="4fa1e-162">도구</span><span class="sxs-lookup"><span data-stu-id="4fa1e-162">Tool</span></span> | <span data-ttu-id="4fa1e-163">프로젝트의 출력 파일에 배치할를 지정 된 `tool` 폴더입니다.</span><span class="sxs-lookup"><span data-stu-id="4fa1e-163">Specifies that the output files of the project should be placed in the `tool` folder.</span></span> |
| <span data-ttu-id="4fa1e-164">자세한 정도</span><span class="sxs-lookup"><span data-stu-id="4fa1e-164">Verbosity</span></span> | <span data-ttu-id="4fa1e-165">출력에 표시 되는 세부 정보 수준을 지정: *일반*, *quiet*, *자세한*합니다.</span><span class="sxs-lookup"><span data-stu-id="4fa1e-165">Specifies the amount of detail displayed in the output: *normal*, *quiet*, *detailed*.</span></span> |
| <span data-ttu-id="4fa1e-166">버전</span><span class="sxs-lookup"><span data-stu-id="4fa1e-166">Version</span></span> | <span data-ttu-id="4fa1e-167">버전 번호를 재정의 `.nuspec` 파일입니다.</span><span class="sxs-lookup"><span data-stu-id="4fa1e-167">Overrides the version number from the `.nuspec` file.</span></span> |

<span data-ttu-id="4fa1e-168">또한 참조 [환경 변수](cli-ref-environment-variables.md)</span><span class="sxs-lookup"><span data-stu-id="4fa1e-168">Also see [Environment variables](cli-ref-environment-variables.md)</span></span>

## <a name="excluding-development-dependencies"></a><span data-ttu-id="4fa1e-169">개발 종속성을 제외</span><span class="sxs-lookup"><span data-stu-id="4fa1e-169">Excluding development dependencies</span></span>

<span data-ttu-id="4fa1e-170">일부 NuGet 패키지가 라이브러리를 작성 하는 데 도움이 되지만 반드시 실제 패키지 종속성으로 필요 하지 않은 개발 종속 항목으로 유용 합니다.</span><span class="sxs-lookup"><span data-stu-id="4fa1e-170">Some NuGet packages are useful as development dependencies, which help you author your own library, but aren't necessarily needed as actual package dependencies.</span></span>

<span data-ttu-id="4fa1e-171">`pack` 명령에서 무시 `package` 항목 `packages.config` 있는 `developmentDependency` 특성이로 설정 `true`합니다.</span><span class="sxs-lookup"><span data-stu-id="4fa1e-171">The `pack` command will ignore `package` entries in `packages.config` that have the `developmentDependency` attribute set to `true`.</span></span> <span data-ttu-id="4fa1e-172">이러한 항목을 만든된 패키지에서 종속성으로 포함 되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="4fa1e-172">These entries will not be include as a dependencies in the created package.</span></span>

<span data-ttu-id="4fa1e-173">예를 들어, 다음 사항을 고려 `packages.config` 소스 프로젝트 파일에에서:</span><span class="sxs-lookup"><span data-stu-id="4fa1e-173">For example, consider the following `packages.config` file in the source project:</span></span>

```xml
<?xml version="1.0" encoding="utf-8"?>
<packages>
    <package id="jQuery" version="1.5.2" />
    <package id="netfx-Guard" version="1.3.3.2" developmentDependency="true" />
    <package id="microsoft-web-helpers" version="1.15" />
</packages>
```

<span data-ttu-id="4fa1e-174">이 프로젝트에 대 한 패키지에서 만든 `nuget pack` 한 종속성을 설정한 `jQuery` 및 `microsoft-web-helpers` 아닌 `netfx-Guard`합니다.</span><span class="sxs-lookup"><span data-stu-id="4fa1e-174">For this project, the package created by `nuget pack` will have a dependency on `jQuery` and `microsoft-web-helpers` but not `netfx-Guard`.</span></span>

## <a name="examples"></a><span data-ttu-id="4fa1e-175">예제</span><span class="sxs-lookup"><span data-stu-id="4fa1e-175">Examples</span></span>

```cli
nuget pack

nuget pack foo.nuspec

nuget pack foo.csproj

nuget pack foo.csproj -Properties Configuration=Release

nuget pack foo.csproj -Build -Symbols -Properties owners=janedoe,xiaop;version="1.0.5"

# create a package from project foo.csproj, using MSBuild version 12 to build the project
nuget pack foo.csproj -Build -Symbols -Properties owners=janedoe,xiaop;version="1.0.5" -MSBuildVersion 12

nuget pack foo.nuspec -Version 2.1.0

nuget pack foo.nuspec -Version 1.0.0 -MinClientVersion 2.5

nuget pack Package.nuspec -exclude "*.exe" -exclude "*.bat"
```
