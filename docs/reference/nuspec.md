---
title: NuGet에 대 한 nuspec 파일 참조
description: .nuspec 파일은 패키지를 빌드하고 패키지 소비자에게 정보를 제공하는 데 사용되는 패키지 메타데이터를 포함합니다.
author: JonDouglas
ms.author: jodou
ms.date: 05/24/2019
ms.topic: reference
ms.reviewer: anangaur
ms.openlocfilehash: 6a68b07c42e6abf4ad57d0129fa76d7dd620145f
ms.sourcegitcommit: ee6c3f203648a5561c809db54ebeb1d0f0598b68
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 01/26/2021
ms.locfileid: "98777674"
---
# <a name="nuspec-reference"></a><span data-ttu-id="700d8-103">.nuspec 참조</span><span class="sxs-lookup"><span data-stu-id="700d8-103">.nuspec reference</span></span>

<span data-ttu-id="700d8-104">`.nuspec` 파일은 패키지 메타데이터가 포함된 XML 매니페스트입니다.</span><span class="sxs-lookup"><span data-stu-id="700d8-104">A `.nuspec` file is an XML manifest that contains package metadata.</span></span> <span data-ttu-id="700d8-105">이 매니페스트는 패키지를 빌드하고 소비자에게 정보를 제공하는 데 사용됩니다.</span><span class="sxs-lookup"><span data-stu-id="700d8-105">This manifest is used both to build the package and to provide information to consumers.</span></span> <span data-ttu-id="700d8-106">매니페스트는 항상 패키지에 포함됩니다.</span><span class="sxs-lookup"><span data-stu-id="700d8-106">The manifest is always included in a package.</span></span>

<span data-ttu-id="700d8-107">이 항목의 내용:</span><span class="sxs-lookup"><span data-stu-id="700d8-107">In this topic:</span></span>

- [<span data-ttu-id="700d8-108">일반 형식 및 스키마</span><span class="sxs-lookup"><span data-stu-id="700d8-108">General form and schema</span></span>](#general-form-and-schema)
- <span data-ttu-id="700d8-109">[대체 토큰](#replacement-tokens)(Visual Studio 프로젝트에서 사용하는 경우)</span><span class="sxs-lookup"><span data-stu-id="700d8-109">[Replacement tokens](#replacement-tokens) (when used with a Visual Studio project)</span></span>
- [<span data-ttu-id="700d8-110">종속성</span><span class="sxs-lookup"><span data-stu-id="700d8-110">Dependencies</span></span>](#dependencies)
- [<span data-ttu-id="700d8-111">명시적 어셈블리 참조</span><span class="sxs-lookup"><span data-stu-id="700d8-111">Explicit assembly references</span></span>](#explicit-assembly-references)
- [<span data-ttu-id="700d8-112">프레임워크 어셈블리 참조</span><span class="sxs-lookup"><span data-stu-id="700d8-112">Framework assembly references</span></span>](#framework-assembly-references)
- [<span data-ttu-id="700d8-113">어셈블리 파일 포함</span><span class="sxs-lookup"><span data-stu-id="700d8-113">Including assembly files</span></span>](#including-assembly-files)
- [<span data-ttu-id="700d8-114">콘텐츠 파일 포함</span><span class="sxs-lookup"><span data-stu-id="700d8-114">Including content files</span></span>](#including-content-files)
- [<span data-ttu-id="700d8-115">예제 nuspec 파일</span><span class="sxs-lookup"><span data-stu-id="700d8-115">Example nuspec files</span></span>](#example-nuspec-files)

## <a name="project-type-compatibility"></a><span data-ttu-id="700d8-116">프로젝트 형식 호환성</span><span class="sxs-lookup"><span data-stu-id="700d8-116">Project type compatibility</span></span>

- <span data-ttu-id="700d8-117">`.nuspec`를 `nuget.exe pack` 사용 하는 비 SDK 스타일 프로젝트의 경우를 사용 `packages.config` 합니다.</span><span class="sxs-lookup"><span data-stu-id="700d8-117">Use `.nuspec` with `nuget.exe pack` for non-SDK-style projects that use `packages.config`.</span></span>

- <span data-ttu-id="700d8-118">`.nuspec` [Sdk 스타일 프로젝트](../resources/check-project-format.md) 에 대 한 패키지를 만드는 데는 파일이 필요 하지 않습니다 (일반적으로 .Net Core 및 [sdk 특성](/dotnet/core/tools/csproj#additions)을 사용 하는 .NET Standard 프로젝트).</span><span class="sxs-lookup"><span data-stu-id="700d8-118">A `.nuspec` file is not required to create packages for [SDK-style projects](../resources/check-project-format.md) (typically .NET Core and .NET Standard projects that use the [SDK attribute](/dotnet/core/tools/csproj#additions)).</span></span> <span data-ttu-id="700d8-119">`.nuspec`패키지를 만들 때이 생성 됩니다.</span><span class="sxs-lookup"><span data-stu-id="700d8-119">(Note that a `.nuspec` is generated when you create the package.)</span></span>

   <span data-ttu-id="700d8-120">또는를 사용 하 여 패키지를 만드는 경우 `dotnet.exe pack` `msbuild pack target` 일반적으로 파일에 있는 [모든 속성](../reference/msbuild-targets.md#pack-target) 을 `.nuspec` 프로젝트 파일에 포함 하는 것이 좋습니다.</span><span class="sxs-lookup"><span data-stu-id="700d8-120">If you are creating a package using `dotnet.exe pack` or `msbuild pack target`, we recommend that you [include all the properties](../reference/msbuild-targets.md#pack-target) that are usually in the `.nuspec` file in the project file instead.</span></span> <span data-ttu-id="700d8-121">그러나 대신 [파일을 사용 하 여 `.nuspec` `dotnet.exe` 또는 `msbuild pack target` 를 사용 하 여 압축할 ](../reference/msbuild-targets.md#packing-using-a-nuspec)수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="700d8-121">However, you can instead choose to [use a `.nuspec` file to pack using `dotnet.exe` or `msbuild pack target`](../reference/msbuild-targets.md#packing-using-a-nuspec).</span></span>

- <span data-ttu-id="700d8-122">에서 PackageReference로 마이그레이션된 프로젝트의 경우에는 `packages.config` 패키지를 [](../consume-packages/package-references-in-project-files.md) `.nuspec` 만들 때 파일이 필요 하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="700d8-122">For projects migrated from `packages.config` to [PackageReference](../consume-packages/package-references-in-project-files.md), a `.nuspec` file is not required to create the package.</span></span> <span data-ttu-id="700d8-123">대신 [msbuild-t:pack](../consume-packages/migrate-packages-config-to-package-reference.md#create-a-package-after-migration)를 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="700d8-123">Instead, use [msbuild -t:pack](../consume-packages/migrate-packages-config-to-package-reference.md#create-a-package-after-migration).</span></span>

## <a name="general-form-and-schema"></a><span data-ttu-id="700d8-124">일반 형식 및 스키마</span><span class="sxs-lookup"><span data-stu-id="700d8-124">General form and schema</span></span>

<span data-ttu-id="700d8-125">현재 `nuspec.xsd` 스키마 파일은 [NuGet GitHub 리포지토리](https://github.com/NuGet/NuGet.Client/blob/dev/src/NuGet.Core/NuGet.Packaging/compiler/resources/nuspec.xsd)에 있습니다.</span><span class="sxs-lookup"><span data-stu-id="700d8-125">The current `nuspec.xsd` schema file can be found in the [NuGet GitHub repository](https://github.com/NuGet/NuGet.Client/blob/dev/src/NuGet.Core/NuGet.Packaging/compiler/resources/nuspec.xsd).</span></span>

<span data-ttu-id="700d8-126">이 스키마 내에서 `.nuspec` 파일의 일반 형식은 다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="700d8-126">Within this schema, a `.nuspec` file has the following general form:</span></span>

```xml
<?xml version="1.0" encoding="utf-8"?>
<package xmlns="http://schemas.microsoft.com/packaging/2010/07/nuspec.xsd">
    <metadata>
        <!-- Required elements-->
        <id></id>
        <version></version>
        <description></description>
        <authors></authors>

        <!-- Optional elements -->
        <!-- ... -->
    </metadata>
    <!-- Optional 'files' node -->
</package>
```

<span data-ttu-id="700d8-127">스키마를 시각적으로 명확하게 표시하려면, Visual Studio에서 디자인 모드로 스키마 파일을 열고 **XML 스키마 탐색기** 링크를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="700d8-127">For a clear visual representation of the schema, open the schema file in Visual Studio in Design mode and click on the **XML Schema Explorer** link.</span></span> <span data-ttu-id="700d8-128">또는 파일을 코드로 열고, 편집기에서 마우스 오른쪽 단추를 클릭한 다음, **XML 스키마 탐색기 표시** 를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="700d8-128">Alternately, open the file as code, right-click in the editor, and select **Show XML Schema Explorer**.</span></span> <span data-ttu-id="700d8-129">어느 방법이든 아래와 같은 보기가 표시됩니다(대부분의 경우 펼쳐져 있음).</span><span class="sxs-lookup"><span data-stu-id="700d8-129">Either way you get a view like the one below (when mostly expanded):</span></span>

![nuspec.xsd가 열려 있는 Visual Studio 스키마 탐색기](media/SchemaExplorer.png)

<span data-ttu-id="700d8-131">일반적으로 XML의 경우와 마찬가지로 nuspec 파일의 모든 XML 요소 이름은 대/소문자를 구분 합니다.</span><span class="sxs-lookup"><span data-stu-id="700d8-131">All XML element names in the .nuspec file are case-sensitive, as is the case for XML in general.</span></span> <span data-ttu-id="700d8-132">예를 들어 메타 데이터 요소를 사용 하는 `<description>` 것은 올바르지만 `<Description>` 올바르지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="700d8-132">For example, using the metadata element `<description>` is correct and `<Description>` is not correct.</span></span> <span data-ttu-id="700d8-133">각 요소 이름에 대 한 적절 한 대/소문자는 아래에 설명 되어 있습니다.</span><span class="sxs-lookup"><span data-stu-id="700d8-133">The proper casing for each element name is documented below.</span></span>

### <a name="required-metadata-elements"></a><span data-ttu-id="700d8-134">필수 metadata 요소</span><span class="sxs-lookup"><span data-stu-id="700d8-134">Required metadata elements</span></span>

<span data-ttu-id="700d8-135">다음 요소는 패키지에 대한 최소 요구 사항이지만, [선택적 metadata 요소](#optional-metadata-elements)를 추가하여 개발자가 사용하는 패키지에 대한 전반적인 환경을 향상시키는 것이 좋습니다.</span><span class="sxs-lookup"><span data-stu-id="700d8-135">Although the following elements are the minimum requirements for a package, you should consider adding the [optional metadata elements](#optional-metadata-elements) to improve the overall experience developers have with your package.</span></span> 

<span data-ttu-id="700d8-136">이러한 요소는 `<metadata>` 요소 내에 나타나야 합니다.</span><span class="sxs-lookup"><span data-stu-id="700d8-136">These elements must appear within a `<metadata>` element.</span></span>

#### <a name="id"></a><span data-ttu-id="700d8-137">id</span><span class="sxs-lookup"><span data-stu-id="700d8-137">id</span></span> 
<span data-ttu-id="700d8-138">대/소문자를 구분하지 않는 패키지 식별자이며, nuget.org 또는 패키지가 상주하는 모든 갤러리에서 고유해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="700d8-138">The case-insensitive package identifier, which must be unique across nuget.org or whatever gallery the package resides in.</span></span> <span data-ttu-id="700d8-139">ID는 URL에 유효하지 않은 공백 또는 문자를 포함할 수 없고, 일반적으로 .NET 네임스페이스 규칙을 따릅니다.</span><span class="sxs-lookup"><span data-stu-id="700d8-139">IDs may not contain spaces or characters that are not valid for a URL, and generally follow .NET namespace rules.</span></span> <span data-ttu-id="700d8-140">지침은 [고유한 패키지 식별자 선택](../create-packages/creating-a-package.md#choose-a-unique-package-identifier-and-setting-the-version-number)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="700d8-140">See [Choosing a unique package identifier](../create-packages/creating-a-package.md#choose-a-unique-package-identifier-and-setting-the-version-number) for guidance.</span></span>

<span data-ttu-id="700d8-141">Nuget.org에 패키지를 업로드 하는 경우 `id` 이 필드는 128 자로 제한 됩니다.</span><span class="sxs-lookup"><span data-stu-id="700d8-141">When uploading a package to nuget.org, the `id` field is limited to 128 characters.</span></span>

#### <a name="version"></a><span data-ttu-id="700d8-142">버전</span><span class="sxs-lookup"><span data-stu-id="700d8-142">version</span></span>
<span data-ttu-id="700d8-143">*major.minor.patch* 패턴을 따르는 패키지의 버전입니다.</span><span class="sxs-lookup"><span data-stu-id="700d8-143">The version of the package, following the *major.minor.patch* pattern.</span></span> <span data-ttu-id="700d8-144">버전 번호는 [패키지 버전 관리](../concepts/package-versioning.md#pre-release-versions)에서 설명한 대로 시험판 접미사를 포함할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="700d8-144">Version numbers may include a pre-release suffix as described in [Package versioning](../concepts/package-versioning.md#pre-release-versions).</span></span> 

<span data-ttu-id="700d8-145">Nuget.org에 패키지를 업로드 하는 경우 `version` 이 필드는 64 자로 제한 됩니다.</span><span class="sxs-lookup"><span data-stu-id="700d8-145">When uploading a package to nuget.org, the `version` field is limited to 64 characters.</span></span>

#### <a name="description"></a><span data-ttu-id="700d8-146">description</span><span class="sxs-lookup"><span data-stu-id="700d8-146">description</span></span>
<span data-ttu-id="700d8-147">UI 표시를 위한 패키지에 대 한 설명입니다.</span><span class="sxs-lookup"><span data-stu-id="700d8-147">A description of the package for UI display.</span></span>

<span data-ttu-id="700d8-148">Nuget.org에 패키지를 업로드 하는 경우 `description` 이 필드는 4000 자로 제한 됩니다.</span><span class="sxs-lookup"><span data-stu-id="700d8-148">When uploading a package to nuget.org, the `description` field is limited to 4000 characters.</span></span>

#### <a name="authors"></a><span data-ttu-id="700d8-149">authors</span><span class="sxs-lookup"><span data-stu-id="700d8-149">authors</span></span>
<span data-ttu-id="700d8-150">Nuget.org의 프로필 이름과 일치 하는 쉼표로 구분 된 패키지 작성자 목록입니다. 이러한는 nuget.org의 NuGet 갤러리에 표시 되 고 동일한 작성자가 패키지를 상호 참조 하는 데 사용 됩니다.</span><span class="sxs-lookup"><span data-stu-id="700d8-150">A comma-separated list of packages authors, matching the profile names on nuget.org. These are displayed in the NuGet Gallery on nuget.org and are used to cross-reference packages by the same authors.</span></span> 

<span data-ttu-id="700d8-151">Nuget.org에 패키지를 업로드 하는 경우 `authors` 이 필드는 4000 자로 제한 됩니다.</span><span class="sxs-lookup"><span data-stu-id="700d8-151">When uploading a package to nuget.org, the `authors` field is limited to 4000 characters.</span></span>

### <a name="optional-metadata-elements"></a><span data-ttu-id="700d8-152">선택적 metadata 요소</span><span class="sxs-lookup"><span data-stu-id="700d8-152">Optional metadata elements</span></span>

#### <a name="owners"></a><span data-ttu-id="700d8-153">owners</span><span class="sxs-lookup"><span data-stu-id="700d8-153">owners</span></span>
> [!Important]
> <span data-ttu-id="700d8-154">소유자는 사용 되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="700d8-154">owners is deprecated.</span></span> <span data-ttu-id="700d8-155">작성자를 대신 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="700d8-155">Use authors instead.</span></span>

<span data-ttu-id="700d8-156">Nuget.org에서 프로필 이름을 사용 하 여 쉼표로 구분 된 패키지 작성자 목록입니다. 이는 일반적으로와 동일한 목록 이며 `authors` nuget.org에 패키지를 업로드할 때 무시 됩니다. [Nuget.org에서 패키지 소유자 관리](../nuget-org/publish-a-package.md#managing-package-owners-on-nugetorg)를 참조 하세요.</span><span class="sxs-lookup"><span data-stu-id="700d8-156">A comma-separated list of the package creators using profile names on nuget.org. This is often the same list as in `authors`, and is ignored when uploading the package to nuget.org. See [Managing package owners on nuget.org](../nuget-org/publish-a-package.md#managing-package-owners-on-nugetorg).</span></span> 

#### <a name="projecturl"></a><span data-ttu-id="700d8-157">projectUrl</span><span class="sxs-lookup"><span data-stu-id="700d8-157">projectUrl</span></span>
<span data-ttu-id="700d8-158">nuget.org뿐만 아니라 종종 UI 표시에 표시되는 패키지의 홈페이지에 대한 URL입니다.</span><span class="sxs-lookup"><span data-stu-id="700d8-158">A URL for the package's home page, often shown in UI displays as well as nuget.org.</span></span> 

<span data-ttu-id="700d8-159">Nuget.org에 패키지를 업로드 하는 경우 `projectUrl` 이 필드는 4000 자로 제한 됩니다.</span><span class="sxs-lookup"><span data-stu-id="700d8-159">When uploading a package to nuget.org, the `projectUrl` field is limited to 4000 characters.</span></span>

#### <a name="licenseurl"></a><span data-ttu-id="700d8-160">licenseUrl</span><span class="sxs-lookup"><span data-stu-id="700d8-160">licenseUrl</span></span>
> [!Important]
> <span data-ttu-id="700d8-161">licenseUrl는 사용 되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="700d8-161">licenseUrl is deprecated.</span></span> <span data-ttu-id="700d8-162">대신 라이선스를 사용 하십시오.</span><span class="sxs-lookup"><span data-stu-id="700d8-162">Use license instead.</span></span>

<span data-ttu-id="700d8-163">Nuget.org와 같은 Ui에 표시 되는 패키지의 라이선스에 대 한 URL입니다.</span><span class="sxs-lookup"><span data-stu-id="700d8-163">A URL for the package's license, often shown in UIs like nuget.org.</span></span>

<span data-ttu-id="700d8-164">Nuget.org에 패키지를 업로드 하는 경우 `licenseUrl` 이 필드는 4000 자로 제한 됩니다.</span><span class="sxs-lookup"><span data-stu-id="700d8-164">When uploading a package to nuget.org, the `licenseUrl` field is limited to 4000 characters.</span></span>

#### <a name="license"></a><span data-ttu-id="700d8-165">license</span><span class="sxs-lookup"><span data-stu-id="700d8-165">license</span></span>

<span data-ttu-id="700d8-166">***NuGet 4.9.0** 이상에서 지원 됨*</span><span class="sxs-lookup"><span data-stu-id="700d8-166">*Supported with **NuGet 4.9.0** and above*</span></span>

<span data-ttu-id="700d8-167">Nuget.org와 같은 Ui에 표시 되는 패키지 내 라이선스 파일의 SPDX 라이선스 식 또는 경로입니다. MIT 또는 BSD-2 절과 같은 일반적인 라이선스를 사용 하 여 패키지에 라이선스를 부여 하는 경우 연결 된 [Spdx 라이선스 식별자](https://spdx.org/licenses/)를 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="700d8-167">An SPDX license expression or path to a license file within the package, often shown in UIs like nuget.org. If you're licensing the package under a common license, like MIT or BSD-2-Clause, use the associated [SPDX license identifier](https://spdx.org/licenses/).</span></span> <span data-ttu-id="700d8-168">예를 들면 다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="700d8-168">For example:</span></span>

`<license type="expression">MIT</license>`

> [!Note]
> <span data-ttu-id="700d8-169">NuGet.org는 오픈 소스 이니셔티브 또는 무료 Software Foundation에서 승인한 라이선스 식만 허용 합니다.</span><span class="sxs-lookup"><span data-stu-id="700d8-169">NuGet.org only accepts license expressions that are approved by the Open Source Initiative or the Free Software Foundation.</span></span>

<span data-ttu-id="700d8-170">패키지가 여러 일반적인 라이선스에서 사용이 허가 된 경우 [Spdx 식 구문 버전 2.0](https://spdx.org/spdx-specification-21-web-version#h.jxpfx0ykyb60)을 사용 하 여 복합 라이선스를 지정할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="700d8-170">If your package is licensed under multiple common licenses, you can specify a composite license using the [SPDX expression syntax version 2.0](https://spdx.org/spdx-specification-21-web-version#h.jxpfx0ykyb60).</span></span> <span data-ttu-id="700d8-171">예를 들면 다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="700d8-171">For example:</span></span>

`<license type="expression">BSD-2-Clause OR MIT</license>`

<span data-ttu-id="700d8-172">라이선스 식에서 지원 하지 않는 사용자 지정 라이선스를 사용 하는 경우 `.txt` 라이선스의 텍스트를 사용 하 여 또는 파일을 패키지할 수 있습니다 `.md` .</span><span class="sxs-lookup"><span data-stu-id="700d8-172">If you use a custom license that isn't supported by license expressions, you can package a `.txt` or `.md` file with the license's text.</span></span> <span data-ttu-id="700d8-173">예를 들면 다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="700d8-173">For example:</span></span>

```xml
<package>
  <metadata>
    ...
    <license type="file">LICENSE.txt</license>
    ...
  </metadata>
  <files>
    ...
    <file src="licenses\LICENSE.txt" target="" />
    ...
  </files>
</package>
```

<span data-ttu-id="700d8-174">MSBuild에 해당 하는 경우 [라이선스 식 또는 라이선스 파일 압축](msbuild-targets.md#packing-a-license-expression-or-a-license-file)을 참조 하세요.</span><span class="sxs-lookup"><span data-stu-id="700d8-174">For the MSBuild equivalent, take a look at [Packing a license expression or a license file](msbuild-targets.md#packing-a-license-expression-or-a-license-file).</span></span>

<span data-ttu-id="700d8-175">NuGet 라이선스 식의 정확한 구문은 아래 [ABNF](https://tools.ietf.org/html/rfc5234)에 설명 되어 있습니다.</span><span class="sxs-lookup"><span data-stu-id="700d8-175">The exact syntax of NuGet's license expressions is described below in [ABNF](https://tools.ietf.org/html/rfc5234).</span></span>

```cli
license-id            = <short form license identifier from https://spdx.org/spdx-specification-21-web-version#h.luq9dgcle9mo>

license-exception-id  = <short form license exception identifier from https://spdx.org/spdx-specification-21-web-version#h.ruv3yl8g6czd>

simple-expression = license-id / license-id”+”

compound-expression =  1*1(simple-expression /
                simple-expression "WITH" license-exception-id /
                compound-expression "AND" compound-expression /
                compound-expression "OR" compound-expression ) /                
                "(" compound-expression ")" )

license-expression =  1*1(simple-expression / compound-expression / UNLICENSED)
```

#### <a name="iconurl"></a><span data-ttu-id="700d8-176">iconUrl</span><span class="sxs-lookup"><span data-stu-id="700d8-176">iconUrl</span></span>

> [!Important]
> <span data-ttu-id="700d8-177">iconUrl은 더 이상 사용 되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="700d8-177">iconUrl is deprecated.</span></span> <span data-ttu-id="700d8-178">대신 아이콘을 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="700d8-178">Use icon instead.</span></span>

<span data-ttu-id="700d8-179">UI 표시에서 패키지에 대 한 아이콘으로 사용할 투명도 배경을 포함 하는 128x128 이미지의 URL입니다.</span><span class="sxs-lookup"><span data-stu-id="700d8-179">A URL for a 128x128 image with transparency background to use as the icon for the package in UI display.</span></span> <span data-ttu-id="700d8-180">이 요소에는 이미지가 포함된 웹 페이지의 URL이 아니라 *직접 이미지 URL* 이 포함되어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="700d8-180">Be sure this element contains the *direct image URL* and not the URL of a web page containing the image.</span></span> <span data-ttu-id="700d8-181">예를 들어 GitHub의 이미지를 사용 하려면 <em> https://github.com/ \<username\> / \<repository\> /raw/ \<branch\> / \<logo.png\> </em>와 같은 원시 파일 URL을 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="700d8-181">For example, to use an image from GitHub, use the raw file URL like <em>https://github.com/\<username\>/\<repository\>/raw/\<branch\>/\<logo.png\></em>.</span></span> 

<span data-ttu-id="700d8-182">Nuget.org에 패키지를 업로드 하는 경우 `iconUrl` 이 필드는 4000 자로 제한 됩니다.</span><span class="sxs-lookup"><span data-stu-id="700d8-182">When uploading a package to nuget.org, the `iconUrl` field is limited to 4000 characters.</span></span>

#### <a name="icon"></a><span data-ttu-id="700d8-183">icon</span><span class="sxs-lookup"><span data-stu-id="700d8-183">icon</span></span>

<span data-ttu-id="700d8-184">***NuGet 5.3.0** 이상에서 지원 됨*</span><span class="sxs-lookup"><span data-stu-id="700d8-184">*Supported with **NuGet 5.3.0** and above*</span></span>

<span data-ttu-id="700d8-185">패키지 내 이미지 파일에 대 한 경로입니다. 종종 nuget.org와 같은 Ui에서 패키지 아이콘으로 표시 됩니다.</span><span class="sxs-lookup"><span data-stu-id="700d8-185">It is a path to an image file within the package, often shown in UIs like nuget.org as the package icon.</span></span> <span data-ttu-id="700d8-186">이미지 파일 크기는 1mb로 제한 됩니다.</span><span class="sxs-lookup"><span data-stu-id="700d8-186">Image file size is limited to 1 MB.</span></span> <span data-ttu-id="700d8-187">지원 되는 파일 형식에는 JPEG 및 PNG가 있습니다.</span><span class="sxs-lookup"><span data-stu-id="700d8-187">Supported file formats include JPEG and PNG.</span></span> <span data-ttu-id="700d8-188">128x128 이미지를 확인 하는 것이 좋습니다.</span><span class="sxs-lookup"><span data-stu-id="700d8-188">We recommend an image resolution of 128x128.</span></span>

<span data-ttu-id="700d8-189">예를 들어 nuget.exe를 사용 하 여 패키지를 만들 때 nuspec에 다음을 추가 합니다.</span><span class="sxs-lookup"><span data-stu-id="700d8-189">For example, you would add the following to your nuspec when creating a package using nuget.exe:</span></span>

```xml
<package>
  <metadata>
    ...
    <icon>images\icon.png</icon>
    ...
  </metadata>
  <files>
    ...
    <file src="..\icon.png" target="images\" />
    ...
  </files>
</package>
```

[<span data-ttu-id="700d8-190">패키지 아이콘 nuspec 샘플.</span><span class="sxs-lookup"><span data-stu-id="700d8-190">Package Icon nuspec sample.</span></span>](https://github.com/NuGet/Samples/tree/master/PackageIconNuspecExample)

<span data-ttu-id="700d8-191">MSBuild에 해당 하는 경우 [아이콘 이미지 파일 압축](msbuild-targets.md#packing-an-icon-image-file)을 참조 하세요.</span><span class="sxs-lookup"><span data-stu-id="700d8-191">For the MSBuild equivalent, take a look at [Packing an icon image file](msbuild-targets.md#packing-an-icon-image-file).</span></span>

> [!Tip]
> <span data-ttu-id="700d8-192">및를 모두 지정 `icon` 하 여를 `iconUrl` 지원 하지 않는 소스와의 호환성을 유지할 수 있습니다 `icon` .</span><span class="sxs-lookup"><span data-stu-id="700d8-192">You can specify both `icon` and `iconUrl` to maintain backward compatibility with sources that do not support `icon`.</span></span> <span data-ttu-id="700d8-193">Visual Studio는 `icon` 이후 릴리스에서 폴더 기반 소스에서 가져온 패키지를 지원 합니다.</span><span class="sxs-lookup"><span data-stu-id="700d8-193">Visual Studio will support `icon` for packages coming from a folder-based source in a future release.</span></span>

#### <a name="requirelicenseacceptance"></a><span data-ttu-id="700d8-194">requireLicenseAcceptance</span><span class="sxs-lookup"><span data-stu-id="700d8-194">requireLicenseAcceptance</span></span>
<span data-ttu-id="700d8-195">패키지를 설치하기 전에 클라이언트에서 소비자가 패키지 라이선스에 동의하도록 요구하는 메시지를 표시해야 할지 여부를 지정하는 부울 값입니다.</span><span class="sxs-lookup"><span data-stu-id="700d8-195">A Boolean value specifying whether the client must prompt the consumer to accept the package license before installing the package.</span></span>

#### <a name="developmentdependency"></a><span data-ttu-id="700d8-196">developmentDependency</span><span class="sxs-lookup"><span data-stu-id="700d8-196">developmentDependency</span></span>
<span data-ttu-id="700d8-197">*(2.8 이상)* 패키지가 다른 패키지의 종속성으로 포함되지 않도록 패키지를 개발 전용 종속성으로 표시할지 여부를 지정 하는 부울 값입니다.</span><span class="sxs-lookup"><span data-stu-id="700d8-197">*(2.8+)* A Boolean value specifying whether the package is be marked as a development-only-dependency, which prevents the package from being included as a dependency in other packages.</span></span> <span data-ttu-id="700d8-198">PackageReference (NuGet 4.8 이상) 를 사용하는 경우 이 플래그는 컴파일 시간 자산을 컴파일에서 제외한다는 의미이기도 합니다.</span><span class="sxs-lookup"><span data-stu-id="700d8-198">With PackageReference (NuGet 4.8+), this flag also means that it will exclude compile-time assets from compilation.</span></span> <span data-ttu-id="700d8-199">[PackageReference에 대 한 DevelopmentDependency 지원을](https://github.com/NuGet/Home/wiki/DevelopmentDependency-support-for-PackageReference) 참조 하세요.</span><span class="sxs-lookup"><span data-stu-id="700d8-199">See [DevelopmentDependency support for PackageReference](https://github.com/NuGet/Home/wiki/DevelopmentDependency-support-for-PackageReference)</span></span>

#### <a name="summary"></a><span data-ttu-id="700d8-200">요약</span><span class="sxs-lookup"><span data-stu-id="700d8-200">summary</span></span>
> [!Important]
> <span data-ttu-id="700d8-201">`summary` 는 사용 되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="700d8-201">`summary` is being deprecated.</span></span> <span data-ttu-id="700d8-202">대신 `description`를 사용하세요.</span><span class="sxs-lookup"><span data-stu-id="700d8-202">Use `description` instead.</span></span>

<span data-ttu-id="700d8-203">UI 표시를 위한 패키지에 대한 간단한 설명입니다.</span><span class="sxs-lookup"><span data-stu-id="700d8-203">A short description of the package for UI display.</span></span> <span data-ttu-id="700d8-204">생략하면 `description`의 잘린 버전이 사용됩니다.</span><span class="sxs-lookup"><span data-stu-id="700d8-204">If omitted, a truncated version of `description` is used.</span></span>

<span data-ttu-id="700d8-205">Nuget.org에 패키지를 업로드 하는 경우 `summary` 이 필드는 4000 자로 제한 됩니다.</span><span class="sxs-lookup"><span data-stu-id="700d8-205">When uploading a package to nuget.org, the `summary` field is limited to 4000 characters.</span></span>

#### <a name="releasenotes"></a><span data-ttu-id="700d8-206">releaseNotes</span><span class="sxs-lookup"><span data-stu-id="700d8-206">releaseNotes</span></span>
<span data-ttu-id="700d8-207">*(1.5 이상)* 패키지 설명 대신 Visual Studio 패키지 관리자의 **업데이트** 탭처럼 UI에서 자주 사용되는 이 패키지 릴리스의 변경 내용에 대한 설명입니다.</span><span class="sxs-lookup"><span data-stu-id="700d8-207">*(1.5+)* A description of the changes made in this release of the package, often used in UI like the **Updates** tab of the Visual Studio Package Manager in place of the package description.</span></span>

<span data-ttu-id="700d8-208">Nuget.org에 패키지를 업로드 하는 경우 `releaseNotes` 이 필드는 35000 자로 제한 됩니다.</span><span class="sxs-lookup"><span data-stu-id="700d8-208">When uploading a package to nuget.org, the `releaseNotes` field is limited to 35,000 characters.</span></span>

#### <a name="copyright"></a><span data-ttu-id="700d8-209">저작권</span><span class="sxs-lookup"><span data-stu-id="700d8-209">copyright</span></span>
<span data-ttu-id="700d8-210">*(1.5 이상)* 패키지에 대한 저작권 세부 정보입니다.</span><span class="sxs-lookup"><span data-stu-id="700d8-210">*(1.5+)* Copyright details for the package.</span></span>

<span data-ttu-id="700d8-211">Nuget.org에 패키지를 업로드 하는 경우 `copyright` 이 필드는 4000 자로 제한 됩니다.</span><span class="sxs-lookup"><span data-stu-id="700d8-211">When uploading a package to nuget.org, the `copyright` field is limited to 4000 characters.</span></span>

#### <a name="language"></a><span data-ttu-id="700d8-212">language</span><span class="sxs-lookup"><span data-stu-id="700d8-212">language</span></span>
<span data-ttu-id="700d8-213">패키지에 대한 로캘 ID입니다.</span><span class="sxs-lookup"><span data-stu-id="700d8-213">The locale ID for the package.</span></span> <span data-ttu-id="700d8-214">[지역화된 패키지 만들기](../create-packages/creating-localized-packages.md)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="700d8-214">See [Creating localized packages](../create-packages/creating-localized-packages.md).</span></span>

#### <a name="tags"></a><span data-ttu-id="700d8-215">tags</span><span class="sxs-lookup"><span data-stu-id="700d8-215">tags</span></span>
<span data-ttu-id="700d8-216">패키지를 설명하고 검색 및 필터링을 통해 패키지의 검색 기능을 지원하는 태그 및 키워드에 대한 공백으로 구분된 목록입니다.</span><span class="sxs-lookup"><span data-stu-id="700d8-216">A space-delimited list of tags and keywords that describe the package and aid discoverability of packages through search and filtering.</span></span> 

<span data-ttu-id="700d8-217">Nuget.org에 패키지를 업로드 하는 경우 `tags` 이 필드는 4000 자로 제한 됩니다.</span><span class="sxs-lookup"><span data-stu-id="700d8-217">When uploading a package to nuget.org, the `tags` field is limited to 4000 characters.</span></span>

#### <a name="serviceable"></a><span data-ttu-id="700d8-218">serviceable</span><span class="sxs-lookup"><span data-stu-id="700d8-218">serviceable</span></span> 
<span data-ttu-id="700d8-219">*(3.3 이상)* NuGet 내부 전용입니다.</span><span class="sxs-lookup"><span data-stu-id="700d8-219">*(3.3+)* For internal NuGet use only.</span></span>

#### <a name="repository"></a><span data-ttu-id="700d8-220">리포지토리</span><span class="sxs-lookup"><span data-stu-id="700d8-220">repository</span></span>
<span data-ttu-id="700d8-221">저장소 메타 데이터는 `type` 및 `url` *(4.0 +)*, 및 `branch` 및 `commit` *(4.6 +)* 의 네 가지 선택적 특성으로 구성 됩니다.</span><span class="sxs-lookup"><span data-stu-id="700d8-221">Repository metadata, consisting of four optional attributes: `type` and `url` *(4.0+)*, and `branch` and `commit` *(4.6+)*.</span></span> <span data-ttu-id="700d8-222">이러한 특성을 사용 하 여를 `.nupkg` 빌드한 리포지토리에 매핑할 수 있으며, 패키지를 작성 하는 개별 분기 이름 또는 커밋 sha-1 해시를 자세히 파악할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="700d8-222">These attributes allow you to map the `.nupkg` to the repository that built it, with the potential to get as detailed as the individual branch name and / or commit SHA-1 hash that built the package.</span></span> <span data-ttu-id="700d8-223">이 url은 버전 제어 소프트웨어에서 직접 호출할 수 있는 공개적으로 사용할 수 있는 url 이어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="700d8-223">This should be a publicly available url that can be invoked directly by a version control software.</span></span> <span data-ttu-id="700d8-224">이는 컴퓨터에 대 한 것 이므로 html 페이지가 되어서는 안 됩니다.</span><span class="sxs-lookup"><span data-stu-id="700d8-224">It should not be an html page as this is meant for the computer.</span></span> <span data-ttu-id="700d8-225">프로젝트 페이지에 연결 하려면 `projectUrl` 필드를 대신 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="700d8-225">For linking to project page, use the `projectUrl` field, instead.</span></span>

<span data-ttu-id="700d8-226">예를 들면 다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="700d8-226">For example:</span></span>
```xml
<?xml version="1.0"?>
<package xmlns="http://schemas.microsoft.com/packaging/2010/07/nuspec.xsd">
    <metadata>
        ...
        <repository type="git" url="https://github.com/NuGet/NuGet.Client.git" branch="dev" commit="e1c65e4524cd70ee6e22abe33e6cb6ec73938cb3" />
        ...
    </metadata>
</package>
```

<span data-ttu-id="700d8-227">Nuget.org에 패키지를 업로드 하는 경우 `type` 특성은 100 자로 제한 되며 특성은 `url` 4000 자로 제한 됩니다.</span><span class="sxs-lookup"><span data-stu-id="700d8-227">When uploading a package to nuget.org, the `type` attribute is limited to 100 characters and the `url` attribute is limited to 4000 characters.</span></span>

#### <a name="title"></a><span data-ttu-id="700d8-228">title</span><span class="sxs-lookup"><span data-stu-id="700d8-228">title</span></span>
<span data-ttu-id="700d8-229">일부 UI 표시에서 사용할 수 있는 사용자에 게 친숙 한 패키지의 제목입니다.</span><span class="sxs-lookup"><span data-stu-id="700d8-229">A human-friendly title of the package which may be used in some UI displays.</span></span> <span data-ttu-id="700d8-230">(nuget.org 및 Visual Studio의 패키지 관리자는 제목을 표시 하지 않음)</span><span class="sxs-lookup"><span data-stu-id="700d8-230">(nuget.org and the Package Manager in Visual Studio do not show title)</span></span>

<span data-ttu-id="700d8-231">Nuget.org에 패키지를 업로드 하는 경우이 `title` 필드는 256 자로 제한 되지만 표시 목적으로는 사용 되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="700d8-231">When uploading a package to nuget.org, the `title` field is limited to 256 characters but is not used for any display purposes.</span></span>

#### <a name="collection-elements"></a><span data-ttu-id="700d8-232">컬렉션 요소</span><span class="sxs-lookup"><span data-stu-id="700d8-232">Collection elements</span></span>

#### <a name="packagetypes"></a><span data-ttu-id="700d8-233">packageTypes</span><span class="sxs-lookup"><span data-stu-id="700d8-233">packageTypes</span></span>
<span data-ttu-id="700d8-234">*(3.5 이상)* 기존 종속 패키지가 아닌 경우 패키지의 유형을 지정하는 0개 이상의 `<packageType>` 요소 컬렉션입니다.</span><span class="sxs-lookup"><span data-stu-id="700d8-234">*(3.5+)* A collection of zero or more `<packageType>` elements specifying the type of the package if other than a traditional dependency package.</span></span> <span data-ttu-id="700d8-235">각 packageType에는 *name* 및 *version* 특성이 있습니다.</span><span class="sxs-lookup"><span data-stu-id="700d8-235">Each packageType has attributes of *name* and *version*.</span></span> <span data-ttu-id="700d8-236">[패키지 유형 설정](../create-packages/set-package-type.md)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="700d8-236">See [Setting a package type](../create-packages/set-package-type.md).</span></span>

#### <a name="dependencies"></a><span data-ttu-id="700d8-237">종속성</span><span class="sxs-lookup"><span data-stu-id="700d8-237">dependencies</span></span>
<span data-ttu-id="700d8-238">패키지에 대한 종속성을 지정하는 0개 이상의 `<dependency>` 요소 컬렉션입니다.</span><span class="sxs-lookup"><span data-stu-id="700d8-238">A collection of zero or more `<dependency>` elements specifying the dependencies for the package.</span></span> <span data-ttu-id="700d8-239">각 종속성에는 *id*, *version*, *include*(3.x 이상) 및 *exclude*(3.x 이상) 특성이 있습니다.</span><span class="sxs-lookup"><span data-stu-id="700d8-239">Each dependency has attributes of *id*, *version*, *include* (3.x+), and *exclude* (3.x+).</span></span> <span data-ttu-id="700d8-240">아래의 [종속성](#dependencies-element)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="700d8-240">See [Dependencies](#dependencies-element) below.</span></span>

#### <a name="frameworkassemblies"></a><span data-ttu-id="700d8-241">frameworkAssemblies</span><span class="sxs-lookup"><span data-stu-id="700d8-241">frameworkAssemblies</span></span>
<span data-ttu-id="700d8-242">*(1.2 이상)* 이 패키지에 필요한 .NET Framework 어셈블리 참조를 식별하는 0개 이상의 `<frameworkAssembly>` 요소 컬렉션이며, 패키지를 사용하는 프로젝트에 참조가 추가되도록 합니다.</span><span class="sxs-lookup"><span data-stu-id="700d8-242">*(1.2+)* A collection of zero or more `<frameworkAssembly>` elements identifying .NET Framework assembly references that this package requires, which ensures that references are added to projects consuming the package.</span></span> <span data-ttu-id="700d8-243">각 frameworkAssembly에는 *assemblyName* 및 *targetFramework* 특성이 있습니다.</span><span class="sxs-lookup"><span data-stu-id="700d8-243">Each frameworkAssembly has *assemblyName* and *targetFramework* attributes.</span></span> <span data-ttu-id="700d8-244">아래의 [프레임워크 어셈블리 참조 GAC 지정](#specifying-framework-assembly-references-gac)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="700d8-244">See [Specifying framework assembly references GAC](#specifying-framework-assembly-references-gac) below.</span></span>

#### <a name="references"></a><span data-ttu-id="700d8-245">references</span><span class="sxs-lookup"><span data-stu-id="700d8-245">references</span></span>
<span data-ttu-id="700d8-246">*(1.5 이상)* 프로젝트 참조로 추가된 패키지의 `lib` 폴더에 있는 어셈블리를 명명하는 0개 이상의 `<reference>` 요소 컬렉션입니다.</span><span class="sxs-lookup"><span data-stu-id="700d8-246">*(1.5+)* A collection of zero or more `<reference>` elements naming assemblies in the package's `lib` folder that are added as project references.</span></span> <span data-ttu-id="700d8-247">각 참조에는 *file* 특성이 있습니다.</span><span class="sxs-lookup"><span data-stu-id="700d8-247">Each reference has a *file* attribute.</span></span> <span data-ttu-id="700d8-248">또한 `<references>`에는 *targetFramework* 특성이 있는 `<group>` 요소도 포함될 수 있으며, 그런 다음 `<reference>` 요소가 포함됩니다.</span><span class="sxs-lookup"><span data-stu-id="700d8-248">`<references>` can also contain a `<group>` element with a *targetFramework* attribute, that then contains `<reference>` elements.</span></span> <span data-ttu-id="700d8-249">생략하면 `lib`의 모든 참조가 포함됩니다.</span><span class="sxs-lookup"><span data-stu-id="700d8-249">If omitted, all references in `lib` are included.</span></span> <span data-ttu-id="700d8-250">아래의 [명시적 어셈블리 참조 지정](#specifying-explicit-assembly-references)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="700d8-250">See [Specifying explicit assembly references](#specifying-explicit-assembly-references) below.</span></span>

#### <a name="contentfiles"></a><span data-ttu-id="700d8-251">contentFiles</span><span class="sxs-lookup"><span data-stu-id="700d8-251">contentFiles</span></span>
<span data-ttu-id="700d8-252">*(3.3 이상)* 사용하는 프로젝트에 포함할 콘텐츠 파일을 식별하는 `<files>` 요소 컬렉션입니다.</span><span class="sxs-lookup"><span data-stu-id="700d8-252">*(3.3+)* A collection of `<files>` elements that identify content files to include in the consuming project.</span></span> <span data-ttu-id="700d8-253">이러한 파일은 프로젝트 시스템 내에서 사용되는 방법을 설명하는 일단의 특성으로 지정됩니다.</span><span class="sxs-lookup"><span data-stu-id="700d8-253">These files are specified with a set of attributes that describe how they should be used within the project system.</span></span> <span data-ttu-id="700d8-254">아래의 [패키지에 포함할 파일 지정](#specifying-files-to-include-in-the-package)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="700d8-254">See [Specifying files to include in the package](#specifying-files-to-include-in-the-package) below.</span></span>

#### <a name="files"></a><span data-ttu-id="700d8-255">파일</span><span class="sxs-lookup"><span data-stu-id="700d8-255">files</span></span> 
<span data-ttu-id="700d8-256">`<package>`노드에는에 대 한 형제로 노드가 포함 될 수 있으며 `<files>` `<metadata>` `<contentFiles>` ,이에 따라 `<metadata>` 패키지에 포함할 어셈블리 및 콘텐츠 파일을 지정할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="700d8-256">The `<package>` node may contain a `<files>` node as a sibling to `<metadata>`, and a `<contentFiles>` child under `<metadata>`, to specify which assembly and content files to include in the package.</span></span> <span data-ttu-id="700d8-257">자세한 내용은 이 항목의 뒷부분에 있는 [어셈블리 파일 포함](#including-assembly-files) 및 [콘텐츠 파일 포함](#including-content-files)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="700d8-257">See [Including assembly files](#including-assembly-files) and [Including content files](#including-content-files) later in this topic for details.</span></span>

### <a name="metadata-attributes"></a><span data-ttu-id="700d8-258">메타 데이터 특성</span><span class="sxs-lookup"><span data-stu-id="700d8-258">metadata attributes</span></span>

#### <a name="minclientversion"></a><span data-ttu-id="700d8-259">minClientVersion</span><span class="sxs-lookup"><span data-stu-id="700d8-259">minClientVersion</span></span>
<span data-ttu-id="700d8-260">nuget.exe 및 Visual Studio 패키지 관리자에 의해 적용되는, 이 패키지를 설치할 수 있는 NuGet 클라이언트의 최소 버전을 지정합니다.</span><span class="sxs-lookup"><span data-stu-id="700d8-260">Specifies the minimum version of the NuGet client that can install this package, enforced by nuget.exe and the Visual Studio Package Manager.</span></span> <span data-ttu-id="700d8-261">패키지가 특정 버전의 NuGet 클라이언트에 추가된 `.nuspec` 파일의 특정 기능에 종속될 때마다 이 특성이 사용됩니다.</span><span class="sxs-lookup"><span data-stu-id="700d8-261">This is used whenever the package depends on specific features of the `.nuspec` file that were added in a particular version of the NuGet client.</span></span> <span data-ttu-id="700d8-262">예를 들어 `developmentDependency` 특성을 사용하는 패키지는 `minClientVersion`에 대해 "2.8"을 지정해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="700d8-262">For example, a package using the `developmentDependency` attribute should specify "2.8" for `minClientVersion`.</span></span> <span data-ttu-id="700d8-263">마찬가지로 `contentFiles` 요소(다음 섹션 참조)를 사용하는 패키지는 `minClientVersion`을 "3.3"으로 설정해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="700d8-263">Similarly, a package using the `contentFiles` element (see the next section) should set `minClientVersion` to "3.3".</span></span> <span data-ttu-id="700d8-264">또한 2.5 이전의 NuGet 클라이언트에서는 이 플래그를 인식하지 못하기 때문에 `minClientVersion`에 포함된 내용에 관계없이 *항상* 패키지 설치를 거부합니다.</span><span class="sxs-lookup"><span data-stu-id="700d8-264">Note also that because NuGet clients prior to 2.5 do not recognize this flag, they *always* refuse to install the package no matter what `minClientVersion` contains.</span></span>

```xml
<?xml version="1.0" encoding="utf-8"?>
<package xmlns="http://schemas.microsoft.com/packaging/2010/07/nuspec.xsd">
    <metadata minClientVersion="100.0.0.1">
        <id>dasdas</id>
        <version>2.0.0</version>
        <title />
        <authors>dsadas</authors>
        <owners />
        <requireLicenseAcceptance>false</requireLicenseAcceptance>
        <description>My package description.</description>
    </metadata>
    <files>
        <file src="content\one.txt" target="content\one.txt" />
    </files>
</package>
```

## <a name="replacement-tokens"></a><span data-ttu-id="700d8-265">대체 토큰</span><span class="sxs-lookup"><span data-stu-id="700d8-265">Replacement tokens</span></span>

<span data-ttu-id="700d8-266">패키지를 만들 때 [ `nuget pack` 명령은](../reference/cli-reference/cli-ref-pack.md) 파일 노드의 $ 구분 된 토큰을 `.nuspec` `<metadata>` 프로젝트 파일이 나 명령의 스위치에서 제공 하는 값으로 바꿉니다 `pack` `-properties` .</span><span class="sxs-lookup"><span data-stu-id="700d8-266">When creating a package, the [`nuget pack` command](../reference/cli-reference/cli-ref-pack.md) replaces $-delimited tokens in the `.nuspec` file's `<metadata>` node with values that come from either a project file or the `pack` command's `-properties` switch.</span></span>

<span data-ttu-id="700d8-267">명령줄에서 `nuget pack -properties <name>=<value>;<name>=<value>`를 사용하여 토큰 값을 지정합니다.</span><span class="sxs-lookup"><span data-stu-id="700d8-267">On the command line, you specify token values with `nuget pack -properties <name>=<value>;<name>=<value>`.</span></span> <span data-ttu-id="700d8-268">예를 들어 `.nuspec`에서 `$owners$` 및 `$desc$`와 같은 토큰을 사용하고 다음과 같이 압축 시간에 값을 제공할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="700d8-268">For example, you can use a token such as `$owners$` and `$desc$` in the `.nuspec` and provide the values at packing time as follows:</span></span>

```ps
nuget pack MyProject.csproj -properties
    owners=janedoe,harikm,kimo,xiaop;desc="Awesome app logger utility"
```

<span data-ttu-id="700d8-269">프로젝트의 값을 사용하려면 아래 표에서 설명한 토큰을 지정합니다(AssemblyInfo는 `AssemblyInfo.cs` 또는 `AssemblyInfo.vb`과 같이 `Properties`의 파일을 나타냄).</span><span class="sxs-lookup"><span data-stu-id="700d8-269">To use values from a project, specify the tokens described in the table below (AssemblyInfo refers to the file in `Properties` such as `AssemblyInfo.cs` or `AssemblyInfo.vb`).</span></span>

<span data-ttu-id="700d8-270">이러한 토큰을 사용하려면 `.nuspec` 대신 프로젝트 파일이 있는 `nuget pack`을 실행합니다.</span><span class="sxs-lookup"><span data-stu-id="700d8-270">To use these tokens, run `nuget pack` with the project file rather than just the `.nuspec`.</span></span> <span data-ttu-id="700d8-271">예를 들어 다음 명령을 사용하는 경우 `.nuspec` 파일의 `$id$` 및 `$version$` 토큰을 프로젝트의 `AssemblyName` 및 `AssemblyVersion` 값으로 바꿉니다.</span><span class="sxs-lookup"><span data-stu-id="700d8-271">For example, when using the following command, the `$id$` and `$version$` tokens in a `.nuspec` file are replaced with the project's `AssemblyName` and `AssemblyVersion` values:</span></span>

```ps
nuget pack MyProject.csproj
```

<span data-ttu-id="700d8-272">일반적으로 프로젝트가 있는 경우 처음에는 이러한 표준 토큰 중 일부가 자동으로 포함되는 `nuget spec MyProject.csproj`를 사용하여 `.nuspec`을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="700d8-272">Typically, when you have a project, you create the `.nuspec` initially using `nuget spec MyProject.csproj` which automatically includes some of these standard tokens.</span></span> <span data-ttu-id="700d8-273">그러나 프로젝트에 필요한 `.nuspec` 요소 값이 부족하면 `nuget pack`이 실패합니다.</span><span class="sxs-lookup"><span data-stu-id="700d8-273">However, if a project lacks values for required `.nuspec` elements, then `nuget pack` fails.</span></span> <span data-ttu-id="700d8-274">또한 프로젝트 값을 변경하는 경우 패키지를 만들기 전에 다시 빌드해야 합니다. 이 경우 pack 명령의 `build` 스위치를 사용하여 편리하게 수행할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="700d8-274">Furthermore, if you change project values, be sure to rebuild before creating the package; this can be done conveniently with the pack command's `build` switch.</span></span>

<span data-ttu-id="700d8-275">`$configuration$`을 제외하고는 프로젝트의 값이 명령줄에서 동일한 토큰에 할당된 값보다 우선적으로 사용됩니다.</span><span class="sxs-lookup"><span data-stu-id="700d8-275">With the exception of `$configuration$`, values in the project are used in preference to any assigned to the same token on the command line.</span></span>

| <span data-ttu-id="700d8-276">토큰</span><span class="sxs-lookup"><span data-stu-id="700d8-276">Token</span></span> | <span data-ttu-id="700d8-277">값 원본</span><span class="sxs-lookup"><span data-stu-id="700d8-277">Value source</span></span> | <span data-ttu-id="700d8-278">값</span><span class="sxs-lookup"><span data-stu-id="700d8-278">Value</span></span>
| --- | --- | ---
| <span data-ttu-id="700d8-279">**$id $**</span><span class="sxs-lookup"><span data-stu-id="700d8-279">**$id$**</span></span> | <span data-ttu-id="700d8-280">프로젝트 파일</span><span class="sxs-lookup"><span data-stu-id="700d8-280">Project file</span></span> | <span data-ttu-id="700d8-281">프로젝트 파일의 AssemblyName (title)</span><span class="sxs-lookup"><span data-stu-id="700d8-281">AssemblyName (title) from the project file</span></span> |
| <span data-ttu-id="700d8-282">**$version $**</span><span class="sxs-lookup"><span data-stu-id="700d8-282">**$version$**</span></span> | <span data-ttu-id="700d8-283">AssemblyInfo</span><span class="sxs-lookup"><span data-stu-id="700d8-283">AssemblyInfo</span></span> | <span data-ttu-id="700d8-284">있는 경우 AssemblyInformationalVersion, 그렇지 않으면 AssemblyVersion</span><span class="sxs-lookup"><span data-stu-id="700d8-284">AssemblyInformationalVersion if present, otherwise AssemblyVersion</span></span> |
| <span data-ttu-id="700d8-285">**$author $**</span><span class="sxs-lookup"><span data-stu-id="700d8-285">**$author$**</span></span> | <span data-ttu-id="700d8-286">AssemblyInfo</span><span class="sxs-lookup"><span data-stu-id="700d8-286">AssemblyInfo</span></span> | <span data-ttu-id="700d8-287">AssemblyCompany</span><span class="sxs-lookup"><span data-stu-id="700d8-287">AssemblyCompany</span></span> |
| <span data-ttu-id="700d8-288">**$title $**</span><span class="sxs-lookup"><span data-stu-id="700d8-288">**$title$**</span></span> | <span data-ttu-id="700d8-289">AssemblyInfo</span><span class="sxs-lookup"><span data-stu-id="700d8-289">AssemblyInfo</span></span> | <span data-ttu-id="700d8-290">AssemblyTitle</span><span class="sxs-lookup"><span data-stu-id="700d8-290">AssemblyTitle</span></span> |
| <span data-ttu-id="700d8-291">**$description $**</span><span class="sxs-lookup"><span data-stu-id="700d8-291">**$description$**</span></span> | <span data-ttu-id="700d8-292">AssemblyInfo</span><span class="sxs-lookup"><span data-stu-id="700d8-292">AssemblyInfo</span></span> | <span data-ttu-id="700d8-293">AssemblyDescription</span><span class="sxs-lookup"><span data-stu-id="700d8-293">AssemblyDescription</span></span> |
| <span data-ttu-id="700d8-294">**$copyright $**</span><span class="sxs-lookup"><span data-stu-id="700d8-294">**$copyright$**</span></span> | <span data-ttu-id="700d8-295">AssemblyInfo</span><span class="sxs-lookup"><span data-stu-id="700d8-295">AssemblyInfo</span></span> | <span data-ttu-id="700d8-296">AssemblyCopyright</span><span class="sxs-lookup"><span data-stu-id="700d8-296">AssemblyCopyright</span></span> |
| <span data-ttu-id="700d8-297">**$configuration $**</span><span class="sxs-lookup"><span data-stu-id="700d8-297">**$configuration$**</span></span> | <span data-ttu-id="700d8-298">어셈블리 DLL</span><span class="sxs-lookup"><span data-stu-id="700d8-298">Assembly DLL</span></span> | <span data-ttu-id="700d8-299">어셈블리를 빌드하는 데 사용되는 구성이며, 기본값은 Debug입니다.</span><span class="sxs-lookup"><span data-stu-id="700d8-299">Configuration used to build the assembly, defaulting to Debug.</span></span> <span data-ttu-id="700d8-300">Release 구성을 사용하여 패키지를 만들려면 항상 명령줄에서 `-properties Configuration=Release`를 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="700d8-300">Note that to create a package using a Release configuration, you always use `-properties Configuration=Release` on the command line.</span></span> |

<span data-ttu-id="700d8-301">또한 토큰은 [어셈블리 파일](#including-assembly-files) 및 [콘텐츠 파일](#including-content-files)을 포함할 때 경로를 확인하는 데 사용할 수도 있습니다.</span><span class="sxs-lookup"><span data-stu-id="700d8-301">Tokens can also be used to resolve paths when you include [assembly files](#including-assembly-files) and [content files](#including-content-files).</span></span> <span data-ttu-id="700d8-302">토큰의 이름은 MSBuild 속성과 동일하므로 현재 빌드 구성에 따라 포함할 파일을 선택할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="700d8-302">The tokens have the same names as the MSBuild properties, making it possible to select files to be included depending on the current build configuration.</span></span> <span data-ttu-id="700d8-303">예를 들어 `.nuspec` 파일에서 다음 토큰을 사용하는 경우가 있습니다.</span><span class="sxs-lookup"><span data-stu-id="700d8-303">For example, if you use the following tokens in the `.nuspec` file:</span></span>

```xml
<files>
    <file src="bin\$configuration$\$id$.pdb" target="lib\net40" />
</files>
```

<span data-ttu-id="700d8-304">그리고 MSBuild의 `Release` 구성을 사용하여 `AssemblyName`이 `LoggingLibrary`인 어셈블리를 빌드합니다. 이 경우 패키지에 있는 `.nuspec` 파일의 결과 줄은 다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="700d8-304">And you build an assembly whose `AssemblyName` is `LoggingLibrary` with the `Release` configuration in MSBuild, the resulting lines in the `.nuspec` file in the package is as follows:</span></span>

```xml
<files>
    <file src="bin\Release\LoggingLibrary.pdb" target="lib\net40" />
</files>
```

## <a name="dependencies-element"></a><span data-ttu-id="700d8-305">종속성 요소</span><span class="sxs-lookup"><span data-stu-id="700d8-305">Dependencies element</span></span>

<span data-ttu-id="700d8-306">`<metadata>` 내의 `<dependencies>` 요소에는 최상위 패키지가 종속되는 다른 패키지를 식별하는 임의 개수의 `<dependency>` 요소가 포함됩니다.</span><span class="sxs-lookup"><span data-stu-id="700d8-306">The `<dependencies>` element within `<metadata>` contains any number of `<dependency>` elements that identify other packages upon which the top-level package depends.</span></span> <span data-ttu-id="700d8-307">각 `<dependency>`에 대한 특성은 다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="700d8-307">The attributes for each `<dependency>` are as follows:</span></span>

| <span data-ttu-id="700d8-308">attribute</span><span class="sxs-lookup"><span data-stu-id="700d8-308">Attribute</span></span> | <span data-ttu-id="700d8-309">Description</span><span class="sxs-lookup"><span data-stu-id="700d8-309">Description</span></span> |
| --- | --- |
| `id` | <span data-ttu-id="700d8-310">(필수) 패키지 페이지에서 “EntityFramework” 및 “NUnit” 패키지 nuget.org의 이름인 같은 종속성의 패키지 ID를 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="700d8-310">(Required) The package ID of the dependency, such as "EntityFramework" and "NUnit", which is the name of the package nuget.org shows on a package page.</span></span> |
| `version` | <span data-ttu-id="700d8-311">(필수) 종속성으로 허용되는 버전 범위입니다.</span><span class="sxs-lookup"><span data-stu-id="700d8-311">(Required) The range of versions acceptable as a dependency.</span></span> <span data-ttu-id="700d8-312">정확한 구문은 [패키지 버전 관리](../concepts/package-versioning.md#version-ranges)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="700d8-312">See [Package versioning](../concepts/package-versioning.md#version-ranges) for exact syntax.</span></span> <span data-ttu-id="700d8-313">부동 버전은 지원 되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="700d8-313">Floating versions are not supported.</span></span> |
| <span data-ttu-id="700d8-314">include</span><span class="sxs-lookup"><span data-stu-id="700d8-314">include</span></span> | <span data-ttu-id="700d8-315">최종 패키지에 포함할 종속성을 나타내는 include/exclude 태그(아래 참조)에 대한 쉼표로 구분된 목록입니다.</span><span class="sxs-lookup"><span data-stu-id="700d8-315">A comma-delimited list of include/exclude tags (see below) indicating of the dependency to include in the final package.</span></span> <span data-ttu-id="700d8-316">기본값은 `all`입니다.</span><span class="sxs-lookup"><span data-stu-id="700d8-316">The default value is `all`.</span></span> |
| <span data-ttu-id="700d8-317">제외</span><span class="sxs-lookup"><span data-stu-id="700d8-317">exclude</span></span> | <span data-ttu-id="700d8-318">최종 패키지에서 제외할 종속성을 나타내는 include/exclude 태그(아래 참조)에 대한 쉼표로 구분된 목록입니다.</span><span class="sxs-lookup"><span data-stu-id="700d8-318">A comma-delimited list of include/exclude tags (see below) indicating of the dependency to exclude in the final package.</span></span> <span data-ttu-id="700d8-319">기본값은 과도 하 `build,analyzers` 게 쓸 수 있는 값입니다.</span><span class="sxs-lookup"><span data-stu-id="700d8-319">The  default value is `build,analyzers` which can be over-written.</span></span> <span data-ttu-id="700d8-320">그러나 `content/ ContentFiles` 는 과도 하 게 작성할 수 없는 최종 패키지에서 암시적으로 제외 됩니다.</span><span class="sxs-lookup"><span data-stu-id="700d8-320">But `content/ ContentFiles` are also implicitly excluded in the final package which can't be over-written.</span></span> <span data-ttu-id="700d8-321">`exclude`로 지정된 태그는 `include`로 지정된 태그보다 우선 순위가 높습니다.</span><span class="sxs-lookup"><span data-stu-id="700d8-321">Tags specified with `exclude` take precedence over those specified with `include`.</span></span> <span data-ttu-id="700d8-322">예를 들어 `include="runtime, compile" exclude="compile"`은 `include="runtime"`과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="700d8-322">For example, `include="runtime, compile" exclude="compile"` is the same as `include="runtime"`.</span></span> |

<span data-ttu-id="700d8-323">Nuget.org에 패키지를 업로드 하는 경우 각 종속성의 `id` 특성은 128 자로 제한 되며 `version` 특성은 256 자로 제한 됩니다.</span><span class="sxs-lookup"><span data-stu-id="700d8-323">When uploading a package to nuget.org, each dependency's `id` attribute is limited to 128 characters and the `version` attribute is limited to 256 characters.</span></span>

| <span data-ttu-id="700d8-324">include/exclude 태그</span><span class="sxs-lookup"><span data-stu-id="700d8-324">Include/Exclude tag</span></span> | <span data-ttu-id="700d8-325">영향을 받는 대상 폴더</span><span class="sxs-lookup"><span data-stu-id="700d8-325">Affected folders of the target</span></span> |
| --- | --- |
| <span data-ttu-id="700d8-326">contentFiles</span><span class="sxs-lookup"><span data-stu-id="700d8-326">contentFiles</span></span> | <span data-ttu-id="700d8-327">Content</span><span class="sxs-lookup"><span data-stu-id="700d8-327">Content</span></span> |
| <span data-ttu-id="700d8-328">런타임</span><span class="sxs-lookup"><span data-stu-id="700d8-328">runtime</span></span> | <span data-ttu-id="700d8-329">Runtime, Resources 및 FrameworkAssemblies</span><span class="sxs-lookup"><span data-stu-id="700d8-329">Runtime, Resources, and FrameworkAssemblies</span></span> |
| <span data-ttu-id="700d8-330">compile</span><span class="sxs-lookup"><span data-stu-id="700d8-330">compile</span></span> | <span data-ttu-id="700d8-331">lib</span><span class="sxs-lookup"><span data-stu-id="700d8-331">lib</span></span> |
| <span data-ttu-id="700d8-332">빌드</span><span class="sxs-lookup"><span data-stu-id="700d8-332">build</span></span> | <span data-ttu-id="700d8-333">build(MSBuild props 및 targets)</span><span class="sxs-lookup"><span data-stu-id="700d8-333">build (MSBuild props and targets)</span></span> |
| <span data-ttu-id="700d8-334">native</span><span class="sxs-lookup"><span data-stu-id="700d8-334">native</span></span> | <span data-ttu-id="700d8-335">native</span><span class="sxs-lookup"><span data-stu-id="700d8-335">native</span></span> |
| <span data-ttu-id="700d8-336">없음</span><span class="sxs-lookup"><span data-stu-id="700d8-336">none</span></span> | <span data-ttu-id="700d8-337">영향을 받는 폴더 없음</span><span class="sxs-lookup"><span data-stu-id="700d8-337">No folders</span></span> |
| <span data-ttu-id="700d8-338">모두</span><span class="sxs-lookup"><span data-stu-id="700d8-338">all</span></span> | <span data-ttu-id="700d8-339">모든 폴더</span><span class="sxs-lookup"><span data-stu-id="700d8-339">All folders</span></span> |

<span data-ttu-id="700d8-340">예를 들어 다음 줄은 `PackageA` 버전 1.1.0 이상 및 `PackageB` 버전 1.x에 대한 종속성을 나타냅니다.</span><span class="sxs-lookup"><span data-stu-id="700d8-340">For example, the following lines indicate dependencies on `PackageA` version 1.1.0 or higher, and `PackageB` version 1.x.</span></span>

```xml
<dependencies>
    <dependency id="PackageA" version="1.1.0" />
    <dependency id="PackageB" version="[1,2)" />
</dependencies>
```

<span data-ttu-id="700d8-341">다음 줄은 동일한 패키지에 대한 종속성을 나타내지만, `PackageA`의 `contentFiles` 및 `build` 폴더와 `PackageB`의 `native` 및 `compile` 폴더 이외의 모든 폴더를 포함하도록 지정합니다.</span><span class="sxs-lookup"><span data-stu-id="700d8-341">The following lines indicate dependencies on the same packages, but specify to include the `contentFiles` and `build` folders of `PackageA` and everything but the `native` and `compile` folders of `PackageB`"</span></span>

```xml
<dependencies>
    <dependency id="PackageA" version="1.1.0" include="contentFiles, build" />
    <dependency id="PackageB" version="[1,2)" exclude="native, compile" />
</dependencies>
```

> [!Important]
> <span data-ttu-id="700d8-342">를 `.nuspec` 사용 하 여 프로젝트에서을 만드는 경우 `nuget spec` 해당 프로젝트에 존재 하는 종속성은 결과 파일에 자동으로 포함 되지 않습니다 `.nuspec` .</span><span class="sxs-lookup"><span data-stu-id="700d8-342">When creating a `.nuspec` from a project using `nuget spec`, dependencies that exist in that project are not automatically included in the resulting `.nuspec` file.</span></span> <span data-ttu-id="700d8-343">대신를 사용 하 여 `nuget pack myproject.csproj` 생성 된 *nupkg* 파일 내에서 *nuspec* 파일을 가져옵니다.</span><span class="sxs-lookup"><span data-stu-id="700d8-343">Instead, use `nuget pack myproject.csproj`, and get the *.nuspec* file from within the generated *.nupkg* file.</span></span> <span data-ttu-id="700d8-344">*Nuspec* 는 종속성을 포함 합니다.</span><span class="sxs-lookup"><span data-stu-id="700d8-344">This *.nuspec* contains the dependencies.</span></span>

### <a name="dependency-groups"></a><span data-ttu-id="700d8-345">종속성 그룹</span><span class="sxs-lookup"><span data-stu-id="700d8-345">Dependency groups</span></span>

<span data-ttu-id="700d8-346">*버전 2.0 이상*</span><span class="sxs-lookup"><span data-stu-id="700d8-346">*Version 2.0+*</span></span>

<span data-ttu-id="700d8-347">단일 단순 목록의 대안으로, `<dependencies>` 내에서 `<group>` 요소를 사용하여 대상 프로젝트의 프레임워크 프로필에 따라 종속성을 지정할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="700d8-347">As an alternative to a single flat list, dependencies can be specified according to the framework profile of the target project using `<group>` elements within `<dependencies>`.</span></span>

<span data-ttu-id="700d8-348">각 그룹에는 `targetFramework`라는 특성이 있으며 0개 이상의 `<dependency>` 요소가 포함됩니다.</span><span class="sxs-lookup"><span data-stu-id="700d8-348">Each group has an attribute named `targetFramework` and contains zero or more `<dependency>` elements.</span></span> <span data-ttu-id="700d8-349">이러한 종속성은 대상 프레임워크가 프로젝트의 프레임워크 프로필과 호환될 때 함께 설치됩니다.</span><span class="sxs-lookup"><span data-stu-id="700d8-349">Those dependencies are installed together when  the target framework is compatible with the project's framework profile.</span></span>

<span data-ttu-id="700d8-350">`targetFramework` 특성이 없는 `<group>` 요소는 종속성의 기본 또는 대체(fallback) 목록으로 사용됩니다.</span><span class="sxs-lookup"><span data-stu-id="700d8-350">The `<group>` element without a `targetFramework` attribute is used as the default or fallback list of dependencies.</span></span> <span data-ttu-id="700d8-351">정확한 프레임워크 식별자는 [대상 프레임워크](../reference/target-frameworks.md)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="700d8-351">See [Target frameworks](../reference/target-frameworks.md) for the exact framework identifiers.</span></span>

> [!Important]
> <span data-ttu-id="700d8-352">그룹 형식은 단순 목록과 섞일 수 없습니다.</span><span class="sxs-lookup"><span data-stu-id="700d8-352">The group format cannot be intermixed with a flat list.</span></span>

> [!Note]
> <span data-ttu-id="700d8-353">폴더에 사용 되는 [TFM (대상 프레임 워크 모니커)](../reference/target-frameworks.md) 의 형식은 `lib/ref` 에서 사용 되는 TFM 비교할 때 다릅니다 `dependency groups` .</span><span class="sxs-lookup"><span data-stu-id="700d8-353">The format of [Target Framework Moniker (TFM)](../reference/target-frameworks.md) used in `lib/ref` folder is different when compared to the TFM used in `dependency groups`.</span></span> <span data-ttu-id="700d8-354">에 선언 된 대상 프레임 워크 `dependencies group` 와 `lib/ref` 파일의 폴더에 `.nuspec` 정확히 일치 하는 항목이 없으면 `pack` 명령이 [NuGet 경고 NU5128](../reference/errors-and-warnings/nu5128.md)를 발생 시킵니다.</span><span class="sxs-lookup"><span data-stu-id="700d8-354">If the target frameworks declared in the `dependencies group` and the `lib/ref` folder of `.nuspec` file do not have exact matches then `pack` command will raise [NuGet Warning NU5128](../reference/errors-and-warnings/nu5128.md).</span></span>

<span data-ttu-id="700d8-355">다음 예제에서는 `<group>` 요소의 여러 변형을 보여줍니다.</span><span class="sxs-lookup"><span data-stu-id="700d8-355">The following example shows different variations of the `<group>` element:</span></span>

```xml
<dependencies>
    <group>
        <dependency id="RouteMagic" version="1.1.0" />
    </group>

    <group targetFramework=".NETFramework4.7.2">
        <dependency id="jQuery" version="1.6.2" />
        <dependency id="WebActivator" version="1.4.4" />
    </group>

    <group targetFramework="netcoreapp3.1">
    </group>
</dependencies>
```

<a name="specifying-explicit-assembly-references"></a>

## <a name="explicit-assembly-references"></a><span data-ttu-id="700d8-356">명시적 어셈블리 참조</span><span class="sxs-lookup"><span data-stu-id="700d8-356">Explicit assembly references</span></span>

<span data-ttu-id="700d8-357">`<references>`요소는를 사용 하 여 프로젝트에서 `packages.config` 패키지를 사용할 때 대상 프로젝트에서 참조 해야 하는 어셈블리를 명시적으로 지정 하는 데 사용 됩니다.</span><span class="sxs-lookup"><span data-stu-id="700d8-357">The `<references>` element is used by projects using `packages.config` to explicitly specify the assemblies that the target project should reference when using the package.</span></span> <span data-ttu-id="700d8-358">명시적 참조는 일반적으로 디자인 타임 전용 어셈블리에만 사용됩니다.</span><span class="sxs-lookup"><span data-stu-id="700d8-358">Explicit references are typically used for design-time only assemblies.</span></span> <span data-ttu-id="700d8-359">자세한 내용은 프로젝트에서 참조 하는 [어셈블리를 선택](../create-packages/select-assemblies-referenced-by-projects.md) 하는 방법에 대 한 페이지를 참조 하세요.</span><span class="sxs-lookup"><span data-stu-id="700d8-359">For more information, see the page on [selecting assemblies referenced by projects](../create-packages/select-assemblies-referenced-by-projects.md) for more information.</span></span>

<span data-ttu-id="700d8-360">예를 들어 다음 `<references>` 요소는 패키지에 추가 어셈블리가 있는 경우에도 `xunit.dll` 및 `xunit.extensions.dll`에 대한 참조만 추가하도록 NuGet에 지시합니다.</span><span class="sxs-lookup"><span data-stu-id="700d8-360">For example, the following `<references>` element instructs NuGet to add references to only `xunit.dll` and `xunit.extensions.dll` even if there are additional assemblies in the package:</span></span>

```xml
<references>
    <reference file="xunit.dll" />
    <reference file="xunit.extensions.dll" />
</references>
```

### <a name="reference-groups"></a><span data-ttu-id="700d8-361">참조 그룹</span><span class="sxs-lookup"><span data-stu-id="700d8-361">Reference groups</span></span>

<span data-ttu-id="700d8-362">단일 단순 목록의 대안으로, `<references>` 내에서 `<group>` 요소를 사용하여 대상 프로젝트의 프레임워크 프로필에 따라 참조를 지정할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="700d8-362">As an alternative to a single flat list, references can be specified according to the framework profile of the target project using `<group>` elements within `<references>`.</span></span>

<span data-ttu-id="700d8-363">각 그룹에는 `targetFramework`라는 특성이 있으며 0개 이상의 `<reference>` 요소가 포함됩니다.</span><span class="sxs-lookup"><span data-stu-id="700d8-363">Each group has an attribute named `targetFramework` and contains zero or more `<reference>` elements.</span></span> <span data-ttu-id="700d8-364">이러한 참조는 대상 프레임워크가 프로젝트의 프레임워크 프로필과 호환될 때 프로젝트에 추가 됩니다.</span><span class="sxs-lookup"><span data-stu-id="700d8-364">Those references are added to a project when the target framework is compatible with the project's framework profile.</span></span>

<span data-ttu-id="700d8-365">`targetFramework` 특성이 없는 `<group>` 요소는 참조의 기본 또는 대체(fallback) 목록으로 사용됩니다.</span><span class="sxs-lookup"><span data-stu-id="700d8-365">The `<group>` element without a `targetFramework` attribute is used as the default or fallback list of references.</span></span> <span data-ttu-id="700d8-366">정확한 프레임워크 식별자는 [대상 프레임워크](../reference/target-frameworks.md)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="700d8-366">See [Target frameworks](../reference/target-frameworks.md) for the exact framework identifiers.</span></span>

> [!Important]
> <span data-ttu-id="700d8-367">그룹 형식은 단순 목록과 섞일 수 없습니다.</span><span class="sxs-lookup"><span data-stu-id="700d8-367">The group format cannot be intermixed with a flat list.</span></span>

<span data-ttu-id="700d8-368">다음 예제에서는 `<group>` 요소의 여러 변형을 보여줍니다.</span><span class="sxs-lookup"><span data-stu-id="700d8-368">The following example shows different variations of the `<group>` element:</span></span>

```xml
<references>
    <group>
        <reference file="a.dll" />
    </group>

    <group targetFramework="net45">
        <reference file="b45.dll" />
    </group>

    <group targetFramework="netcore45">
        <reference file="bcore45.dll" />
    </group>
</references>
```

<a name="specifying-framework-assembly-references-gac"></a>

## <a name="framework-assembly-references"></a><span data-ttu-id="700d8-369">프레임워크 어셈블리 참조</span><span class="sxs-lookup"><span data-stu-id="700d8-369">Framework assembly references</span></span>

<span data-ttu-id="700d8-370">프레임워크 어셈블리는 .NET Framework의 일부이며, 지정된 컴퓨터에 대한 GAC(전역 어셈블리 캐시)에 이미 있어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="700d8-370">Framework assemblies are those that are part of the .NET framework and should already be in the global assembly cache (GAC) for any given machine.</span></span> <span data-ttu-id="700d8-371">패키지는 `<frameworkAssemblies>` 요소 내에서 이러한 어셈블리를 식별하여 프로젝트에 해당 참조가 아직 없는 경우 필요한 참조가 프로젝트에 추가되도록 할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="700d8-371">By identifying those assemblies within the `<frameworkAssemblies>` element, a package can ensure that required references are added to a project in the event that the project doesn't have such references already.</span></span> <span data-ttu-id="700d8-372">물론 이러한 어셈블리는 패키지에 직접 포함되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="700d8-372">Such assemblies, of course, are not included in a package directly.</span></span>

<span data-ttu-id="700d8-373">`<frameworkAssemblies>` 요소는 0개 이상의 `<frameworkAssembly>` 요소를 포함하며, 각 요소마다 다음 특성을 지정합니다.</span><span class="sxs-lookup"><span data-stu-id="700d8-373">The `<frameworkAssemblies>` element contains zero or more `<frameworkAssembly>` elements, each of which specifies the following attributes:</span></span>

| <span data-ttu-id="700d8-374">attribute</span><span class="sxs-lookup"><span data-stu-id="700d8-374">Attribute</span></span> | <span data-ttu-id="700d8-375">설명</span><span class="sxs-lookup"><span data-stu-id="700d8-375">Description</span></span> |
| --- | --- |
| <span data-ttu-id="700d8-376">**assemblyName**</span><span class="sxs-lookup"><span data-stu-id="700d8-376">**assemblyName**</span></span> | <span data-ttu-id="700d8-377">(필수) 정규화된 어셈블리 이름입니다.</span><span class="sxs-lookup"><span data-stu-id="700d8-377">(Required) The fully qualified assembly name.</span></span> |
| <span data-ttu-id="700d8-378">**targetFramework**</span><span class="sxs-lookup"><span data-stu-id="700d8-378">**targetFramework**</span></span> | <span data-ttu-id="700d8-379">(선택) 이 참조가 적용되는 대상 프레임워크를 지정합니다.</span><span class="sxs-lookup"><span data-stu-id="700d8-379">(Optional) Specifies the target framework to which this reference applies.</span></span> <span data-ttu-id="700d8-380">생략하면 참조가 모든 프레임워크에 적용됨을 나타냅니다.</span><span class="sxs-lookup"><span data-stu-id="700d8-380">If omitted, indicates that the reference applies to all frameworks.</span></span> <span data-ttu-id="700d8-381">정확한 프레임워크 식별자는 [대상 프레임워크](../reference/target-frameworks.md)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="700d8-381">See [Target frameworks](../reference/target-frameworks.md) for the exact framework identifiers.</span></span> |

<span data-ttu-id="700d8-382">다음 예제에서는 모든 대상 프레임워크의 `System.Net`에 대한 참조와 .NET Framework 4.0 전용의 `System.ServiceModel`에 대한 참조를 보여줍니다.</span><span class="sxs-lookup"><span data-stu-id="700d8-382">The following example shows a reference to `System.Net` for all target frameworks, and a reference to `System.ServiceModel` for .NET Framework 4.0 only:</span></span>

```xml
<frameworkAssemblies>
    <frameworkAssembly assemblyName="System.Net"  />

    <frameworkAssembly assemblyName="System.ServiceModel" targetFramework="net40" />
</frameworkAssemblies>
```

<a name="specifying-files-to-include-in-the-package"></a>

## <a name="including-assembly-files"></a><span data-ttu-id="700d8-383">어셈블리 파일 포함</span><span class="sxs-lookup"><span data-stu-id="700d8-383">Including assembly files</span></span>

<span data-ttu-id="700d8-384">[패키지 만들기](../create-packages/creating-a-package.md)에서 설명한 규칙을 따르면 파일 목록을 `.nuspec` 파일에 명시적으로 지정할 필요가 없습니다.</span><span class="sxs-lookup"><span data-stu-id="700d8-384">If you follow the conventions described in [Creating a Package](../create-packages/creating-a-package.md), you do not have to explicitly specify a list of files in the `.nuspec` file.</span></span> <span data-ttu-id="700d8-385">`nuget pack` 명령은 필요한 파일을 자동으로 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="700d8-385">The `nuget pack` command automatically picks up the necessary files.</span></span>

> [!Important]
> <span data-ttu-id="700d8-386">패키지가 프로젝트에 설치되면 어셈블리 참조가 지역화된 위성 어셈블리로 간주되므로 NuGet은 `.resources.dll`이라는 DLL을 *제외한* 패키지의 DLL에 해당 어셈블리 참조를 자동으로 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="700d8-386">When a package is installed into a project, NuGet automatically adds assembly references to the package's DLLs, *excluding* those that are named `.resources.dll` because they are assumed to be localized satellite assemblies.</span></span> <span data-ttu-id="700d8-387">이러한 이유로 다른 경우에 필수 패키지 코드가 포함되는 파일에는 `.resources.dll`을 사용하지 마세요.</span><span class="sxs-lookup"><span data-stu-id="700d8-387">For this reason, avoid using `.resources.dll` for files that otherwise contain essential package code.</span></span>

<span data-ttu-id="700d8-388">이러한 자동 동작을 무시하고 패키지에 포함되는 파일을 명시적으로 제어하려면 `<files>` 요소를 `<package>`의 자식(및 `<metadata>`의 형제)으로 배치하고 각 파일을 별도의 `<file>` 요소로 식별합니다.</span><span class="sxs-lookup"><span data-stu-id="700d8-388">To bypass this automatic behavior and explicitly control which files are included in a package, place a `<files>` element as a child of `<package>` (and a sibling of `<metadata>`), identifying each file with a separate `<file>` element.</span></span> <span data-ttu-id="700d8-389">예를 들면 다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="700d8-389">For example:</span></span>

```xml
<files>
    <file src="bin\Debug\*.dll" target="lib" />
    <file src="bin\Debug\*.pdb" target="lib" />
    <file src="tools\**\*.*" exclude="**\*.log" />
</files>
```

<span data-ttu-id="700d8-390">NuGet 2.x 및 이전 버전과 `packages.config`를 사용하는 프로젝트의 경우 `<files>` 요소는 패키지를 설치할 때 변경할 수 없는 콘텐츠 파일을 포함하는 데에도 사용됩니다.</span><span class="sxs-lookup"><span data-stu-id="700d8-390">With NuGet 2.x and earlier, and projects using `packages.config`, the `<files>` element is also used to include immutable content files when a package is installed.</span></span> <span data-ttu-id="700d8-391">NuGet 3.3 이상 및 프로젝트 PackageReference에서는 `<contentFiles>` 요소가 대신 사용됩니다.</span><span class="sxs-lookup"><span data-stu-id="700d8-391">With NuGet 3.3+ and projects PackageReference, the `<contentFiles>` element is used instead.</span></span> <span data-ttu-id="700d8-392">자세한 내용은 아래의 [콘텐츠 파일 포함](#including-content-files)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="700d8-392">See [Including content files](#including-content-files) below for details.</span></span>

### <a name="file-element-attributes"></a><span data-ttu-id="700d8-393">파일 요소 특성</span><span class="sxs-lookup"><span data-stu-id="700d8-393">File element attributes</span></span>

<span data-ttu-id="700d8-394">각 `<file>` 요소는 다음과 같은 특성을 지정합니다.</span><span class="sxs-lookup"><span data-stu-id="700d8-394">Each `<file>` element specifies the following attributes:</span></span>

| <span data-ttu-id="700d8-395">attribute</span><span class="sxs-lookup"><span data-stu-id="700d8-395">Attribute</span></span> | <span data-ttu-id="700d8-396">Description</span><span class="sxs-lookup"><span data-stu-id="700d8-396">Description</span></span> |
| --- | --- |
| <span data-ttu-id="700d8-397">**src**</span><span class="sxs-lookup"><span data-stu-id="700d8-397">**src**</span></span> | <span data-ttu-id="700d8-398">`exclude` 특성으로 지정된 제외에 따라 포함할 파일의 위치입니다.</span><span class="sxs-lookup"><span data-stu-id="700d8-398">The location of the file or files to include, subject to exclusions specified by the `exclude` attribute.</span></span> <span data-ttu-id="700d8-399">절대 경로가 지정되지 않으면 경로는 `.nuspec` 파일에 대한 상대 경로입니다.</span><span class="sxs-lookup"><span data-stu-id="700d8-399">The path is relative to the `.nuspec` file unless an absolute path is specified.</span></span> <span data-ttu-id="700d8-400">`*` 와일드카드 문자가 허용되고, `**` 이중 와일드카드는 재귀적 폴더 검색을 의미합니다.</span><span class="sxs-lookup"><span data-stu-id="700d8-400">The wildcard character `*` is allowed, and the double wildcard `**` implies a recursive folder search.</span></span> |
| <span data-ttu-id="700d8-401">**대상**</span><span class="sxs-lookup"><span data-stu-id="700d8-401">**target**</span></span> | <span data-ttu-id="700d8-402">원본 파일이 있는 패키지 내의 폴더에 대한 상대 경로이며, `lib`, `content`, `build` 또는 `tools`로 시작해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="700d8-402">The relative path to the folder within the package where the source files are placed, which must begin with `lib`, `content`, `build`, or `tools`.</span></span> <span data-ttu-id="700d8-403">[규칙 기반 작업 디렉터리에서 .nuspec 만들기](../create-packages/creating-a-package.md#from-a-convention-based-working-directory)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="700d8-403">See [Creating a .nuspec from a convention-based working directory](../create-packages/creating-a-package.md#from-a-convention-based-working-directory).</span></span> |
| <span data-ttu-id="700d8-404">**제외**</span><span class="sxs-lookup"><span data-stu-id="700d8-404">**exclude**</span></span> | <span data-ttu-id="700d8-405">`src` 위치에서 제외할 파일 또는 파일 패턴에 대한 세미콜론으로 구분된 목록입니다.</span><span class="sxs-lookup"><span data-stu-id="700d8-405">A semicolon-delimited list of files or file patterns to exclude from the `src` location.</span></span> <span data-ttu-id="700d8-406">`*` 와일드카드 문자가 허용되고, `**` 이중 와일드카드는 재귀적 폴더 검색을 의미합니다.</span><span class="sxs-lookup"><span data-stu-id="700d8-406">The wildcard character `*` is allowed, and the double wildcard `**` implies a recursive folder search.</span></span> |

### <a name="examples"></a><span data-ttu-id="700d8-407">예제</span><span class="sxs-lookup"><span data-stu-id="700d8-407">Examples</span></span>

<span data-ttu-id="700d8-408">**단일 어셈블리**</span><span class="sxs-lookup"><span data-stu-id="700d8-408">**Single assembly**</span></span>

```
Source file:
    library.dll

.nuspec entry:
    <file src="library.dll" target="lib" />

Packaged result:
    lib\library.dll
```

<span data-ttu-id="700d8-409">**특정 대상 프레임워크에 대한 단일 어셈블리**</span><span class="sxs-lookup"><span data-stu-id="700d8-409">**Single assembly specific to a target framework**</span></span>

```
Source file:
    library.dll

.nuspec entry:
    <file src="assemblies\net40\library.dll" target="lib\net40" />

Packaged result:
    lib\net40\library.dll
```

<span data-ttu-id="700d8-410">**와일드카드를 사용하는 DLL 집합**</span><span class="sxs-lookup"><span data-stu-id="700d8-410">**Set of DLLs using a wildcard**</span></span>

```
Source files:
    bin\release\libraryA.dll
    bin\release\libraryB.dll

.nuspec entry:
    <file src="bin\release\*.dll" target="lib" />

Packaged result:
    lib\libraryA.dll
    lib\libraryB.dll
```

<span data-ttu-id="700d8-411">**여러 프레임워크에 대한 DLL**</span><span class="sxs-lookup"><span data-stu-id="700d8-411">**DLLs for different frameworks**</span></span>

```
Source files:
    lib\net40\library.dll
    lib\net20\library.dll

.nuspec entry (using ** recursive search):
    <file src="lib\**" target="lib" />

Packaged result:
    lib\net40\library.dll
    lib\net20\library.dll
```

<span data-ttu-id="700d8-412">**파일 제외**</span><span class="sxs-lookup"><span data-stu-id="700d8-412">**Excluding files**</span></span>

```
Source files:
    \tools\fileA.bak
    \tools\fileB.bak
    \tools\fileA.log
    \tools\build\fileB.log

.nuspec entries:
    <file src="tools\*.*" target="tools" exclude="tools\*.bak" />
    <file src="tools\**\*.*" target="tools" exclude="**\*.log" />

Package result:
    (no files)
```

## <a name="including-content-files"></a><span data-ttu-id="700d8-413">콘텐츠 파일 포함</span><span class="sxs-lookup"><span data-stu-id="700d8-413">Including content files</span></span>

<span data-ttu-id="700d8-414">콘텐츠 파일은 패키지에서 프로젝트에 포함해야 하는 변경할 수 없는 파일입니다.</span><span class="sxs-lookup"><span data-stu-id="700d8-414">Content files are immutable files that a package needs to include in a project.</span></span> <span data-ttu-id="700d8-415">변경할 수 없으므로 사용하는 프로젝트에서 수정되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="700d8-415">Being immutable, they are not intended to be modified by the consuming project.</span></span> <span data-ttu-id="700d8-416">콘텐츠 파일의 예는 다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="700d8-416">Example content files include:</span></span>

- <span data-ttu-id="700d8-417">리소스로 포함된 이미지</span><span class="sxs-lookup"><span data-stu-id="700d8-417">Images that are embedded as resources</span></span>
- <span data-ttu-id="700d8-418">이미 컴파일된 원본 파일</span><span class="sxs-lookup"><span data-stu-id="700d8-418">Source files that are already compiled</span></span>
- <span data-ttu-id="700d8-419">프로젝트의 빌드 출력에 포함되어야 하는 스크립트</span><span class="sxs-lookup"><span data-stu-id="700d8-419">Scripts that need to be included with the build output of the project</span></span>
- <span data-ttu-id="700d8-420">프로젝트에 포함되어야 하지만 프로젝트별 변경이 필요하지 않은 패키지에 대한 구성 파일</span><span class="sxs-lookup"><span data-stu-id="700d8-420">Configuration files for the package that need to be included in the project but don't need any project-specific changes</span></span>

<span data-ttu-id="700d8-421">콘텐츠 파일은 `<files>` 요소를 사용하고 `target` 특성에서 `content` 폴더를 지정하여 패키지에 포함됩니다.</span><span class="sxs-lookup"><span data-stu-id="700d8-421">Content files are included in a package using the `<files>` element, specifying the `content` folder in the `target` attribute.</span></span> <span data-ttu-id="700d8-422">그러나 `<contentFiles>` 요소를 대신 사용하는 PackageReference를 사용하여 프로젝트에 패키지를 설치하는 경우 이러한 파일은 무시됩니다.</span><span class="sxs-lookup"><span data-stu-id="700d8-422">However, such files are ignored when the package is installed in a project using PackageReference, which instead uses the `<contentFiles>` element.</span></span>

<span data-ttu-id="700d8-423">사용하는 프로젝트와의 호환성을 최대화하기 위해 패키지는 두 요소 모두에 콘텐츠 파일을 이상적으로 지정합니다.</span><span class="sxs-lookup"><span data-stu-id="700d8-423">For maximum compatibility with consuming projects, a package ideally specifies the content files in both elements.</span></span>

### <a name="using-the-files-element-for-content-files"></a><span data-ttu-id="700d8-424">콘텐츠 파일에 대한 files 요소 사용</span><span class="sxs-lookup"><span data-stu-id="700d8-424">Using the files element for content files</span></span>

<span data-ttu-id="700d8-425">콘텐츠 파일의 경우 단순히 어셈블리 파일과 동일한 형식을 사용하고 다음 예제와 같이 `content`를 `target` 특성의 기본 폴더로 지정합니다.</span><span class="sxs-lookup"><span data-stu-id="700d8-425">For content files, simply use the same format as for assembly files, but specify `content` as the base folder in the `target` attribute as shown in the following examples.</span></span>

<span data-ttu-id="700d8-426">**기본 콘텐츠 파일**</span><span class="sxs-lookup"><span data-stu-id="700d8-426">**Basic content files**</span></span>

```
Source files:
    css\mobile\style1.css
    css\mobile\style2.css

.nuspec entry:
    <file src="css\mobile\*.css" target="content\css\mobile" />

Packaged result:
    content\css\mobile\style1.css
    content\css\mobile\style2.css
```

<span data-ttu-id="700d8-427">**디렉터리 구조가 포함된 콘텐츠 파일**</span><span class="sxs-lookup"><span data-stu-id="700d8-427">**Content files with directory structure**</span></span>

```
Source files:
    css\mobile\style.css
    css\mobile\wp7\style.css
    css\browser\style.css

.nuspec entry:
    <file src="css\**\*.css" target="content\css" />

Packaged result:
    content\css\mobile\style.css
    content\css\mobile\wp7\style.css
    content\css\browser\style.css
```

<span data-ttu-id="700d8-428">**특정 대상 프레임워크에 대한 콘텐츠 파일**</span><span class="sxs-lookup"><span data-stu-id="700d8-428">**Content file specific to a target framework**</span></span>

```
Source file:
    css\cool\style.css

.nuspec entry
    <file src="css\cool\style.css" target="Content" />

Packaged result:
    content\style.css
```

<span data-ttu-id="700d8-429">**이름에 점이 있는 폴더에 복사되는 콘텐츠 파일**</span><span class="sxs-lookup"><span data-stu-id="700d8-429">**Content file copied to a folder with dot in name**</span></span>

<span data-ttu-id="700d8-430">이 경우 NuGet은 `target`과 `src`의 확장명이 일치하지 않는지 확인하여 `target`의 이름 중 해당 부분을 폴더로 처리합니다.</span><span class="sxs-lookup"><span data-stu-id="700d8-430">In this case, NuGet sees that the extension in `target` does not match the extension in `src` and thus treats that part of the name in `target` as a folder:</span></span>

```
Source file:
    images\picture.png

.nuspec entry:
    <file src="images\picture.png" target="Content\images\package.icons" />

Packaged result:
    content\images\package.icons\picture.png
```

<span data-ttu-id="700d8-431">**확장명이 없는 콘텐츠 파일**</span><span class="sxs-lookup"><span data-stu-id="700d8-431">**Content files without extensions**</span></span>

<span data-ttu-id="700d8-432">확장명이 없는 파일을 포함하려면 `*` 또는 `**` 와일드카드를 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="700d8-432">To include files without an extension, use the `*` or `**` wildcards:</span></span>

```
Source file:
    flags\installed

.nuspec entry:
    <file src="flags\**" target="flags" />

Packaged result:
    flags\installed
```

<span data-ttu-id="700d8-433">**전체 경로와 전체 대상이 포함된 콘텐츠 파일**</span><span class="sxs-lookup"><span data-stu-id="700d8-433">**Content files with deep path and deep target**</span></span>

<span data-ttu-id="700d8-434">이 경우 원본과 대상의 파일 확장명이 일치하므로 NuGet은 대상이 폴더가 아니라 파일 이름이라고 가정합니다.</span><span class="sxs-lookup"><span data-stu-id="700d8-434">In this case, because the file extensions of the source and target match, NuGet assumes that the target is a file name and not a folder:</span></span>

```
Source file:
    css\cool\style.css

.nuspec entry:
    <file src="css\cool\style.css" target="Content\css\cool" />
    or:
    <file src="css\cool\style.css" target="Content\css\cool\style.css" />

Packaged result:
    content\css\cool\style.css
```

<span data-ttu-id="700d8-435">**패키지의 콘텐츠 파일 이름 바꾸기**</span><span class="sxs-lookup"><span data-stu-id="700d8-435">**Renaming a content file in the package**</span></span>

```
Source file:
    ie\css\style.css

.nuspec entry:
    <file src="ie\css\style.css" target="Content\css\ie.css" />

Packaged result:
    content\css\ie.css
```

<span data-ttu-id="700d8-436">**파일 제외**</span><span class="sxs-lookup"><span data-stu-id="700d8-436">**Excluding files**</span></span>

```
Source file:
    docs\*.txt (multiple files)

.nuspec entry:
    <file src="docs\*.txt" target="content\docs" exclude="docs\admin.txt" />
    or
    <file src="*.txt" target="content\docs" exclude="admin.txt;log.txt" />

Packaged result:
    All .txt files from docs except admin.txt (first example)
    All .txt files from docs except admin.txt and log.txt (second example)
```

<a name="using-contentfiles-element-for-content-files"></a>

### <a name="using-the-contentfiles-element-for-content-files"></a><span data-ttu-id="700d8-437">콘텐츠 파일에 대한 contentFiles 요소 사용</span><span class="sxs-lookup"><span data-stu-id="700d8-437">Using the contentFiles element for content files</span></span>

<span data-ttu-id="700d8-438">*NuGet 4.0 이상(PackageReference 사용)*</span><span class="sxs-lookup"><span data-stu-id="700d8-438">*NuGet 4.0+ with PackageReference*</span></span>

<span data-ttu-id="700d8-439">기본적으로 패키지는 `contentFiles` 폴더(아래 참조) 및 기본 특성을 사용하여 해당 폴더의 모든 파일이 포함되는 `nuget pack`에 콘텐츠 파일을 배치합니다.</span><span class="sxs-lookup"><span data-stu-id="700d8-439">By default, a package places content in a `contentFiles` folder (see below) and `nuget pack` included all files in that folder using default attributes.</span></span> <span data-ttu-id="700d8-440">이 경우 `.nuspec`에 `contentFiles` 노드를 포함할 필요가 없습니다.</span><span class="sxs-lookup"><span data-stu-id="700d8-440">In this case it's not necessary to include a `contentFiles` node in the `.nuspec` at all.</span></span>

<span data-ttu-id="700d8-441">포함되는 파일을 제어하려면 `<contentFiles>` 요소에서 포함할 파일을 정확히 식별하는 `<files>` 요소 컬렉션을 지정합니다.</span><span class="sxs-lookup"><span data-stu-id="700d8-441">To control which files are included, the `<contentFiles>` element specifies is a collection of `<files>` elements that identify the exact files include.</span></span>

<span data-ttu-id="700d8-442">이러한 파일은 프로젝트 시스템 내에서 사용되는 방법을 설명하는 일단의 특성으로 지정됩니다.</span><span class="sxs-lookup"><span data-stu-id="700d8-442">These files are specified with a set of attributes that describe how they should be used within the project system:</span></span>

| <span data-ttu-id="700d8-443">attribute</span><span class="sxs-lookup"><span data-stu-id="700d8-443">Attribute</span></span> | <span data-ttu-id="700d8-444">Description</span><span class="sxs-lookup"><span data-stu-id="700d8-444">Description</span></span> |
| --- | --- |
| <span data-ttu-id="700d8-445">**되어야**</span><span class="sxs-lookup"><span data-stu-id="700d8-445">**include**</span></span> | <span data-ttu-id="700d8-446">(필수) `exclude` 특성으로 지정된 제외에 따라 포함할 파일의 위치입니다.</span><span class="sxs-lookup"><span data-stu-id="700d8-446">(Required) The location of the file or files to include, subject to exclusions specified by the `exclude` attribute.</span></span> <span data-ttu-id="700d8-447">`contentFiles`절대 경로를 지정 하지 않으면 폴더에 대 한 상대 경로입니다.</span><span class="sxs-lookup"><span data-stu-id="700d8-447">The path is relative to the `contentFiles` folder unless an absolute path is specified.</span></span> <span data-ttu-id="700d8-448">`*` 와일드카드 문자가 허용되고, `**` 이중 와일드카드는 재귀적 폴더 검색을 의미합니다.</span><span class="sxs-lookup"><span data-stu-id="700d8-448">The wildcard character `*` is allowed, and the double wildcard `**` implies a recursive folder search.</span></span> |
| <span data-ttu-id="700d8-449">**제외**</span><span class="sxs-lookup"><span data-stu-id="700d8-449">**exclude**</span></span> | <span data-ttu-id="700d8-450">`src` 위치에서 제외할 파일 또는 파일 패턴에 대한 세미콜론으로 구분된 목록입니다.</span><span class="sxs-lookup"><span data-stu-id="700d8-450">A semicolon-delimited list of files or file patterns to exclude from the `src` location.</span></span> <span data-ttu-id="700d8-451">`*` 와일드카드 문자가 허용되고, `**` 이중 와일드카드는 재귀적 폴더 검색을 의미합니다.</span><span class="sxs-lookup"><span data-stu-id="700d8-451">The wildcard character `*` is allowed, and the double wildcard `**` implies a recursive folder search.</span></span> |
| <span data-ttu-id="700d8-452">**buildAction**</span><span class="sxs-lookup"><span data-stu-id="700d8-452">**buildAction**</span></span> | <span data-ttu-id="700d8-453">,,, 등의 MSBuild에 대 한 콘텐츠 항목에 할당할 빌드 `Content` 작업 `None` `Embedded Resource` `Compile` 입니다. 기본값은 `Compile` 입니다.</span><span class="sxs-lookup"><span data-stu-id="700d8-453">The build action to assign to the content item for MSBuild, such as `Content`, `None`, `Embedded Resource`, `Compile`, etc. The default is `Compile`.</span></span> |
| <span data-ttu-id="700d8-454">**copyToOutput**</span><span class="sxs-lookup"><span data-stu-id="700d8-454">**copyToOutput**</span></span> | <span data-ttu-id="700d8-455">콘텐츠 항목을 빌드 (또는 게시) 출력 폴더에 복사할지 여부를 나타내는 부울 값입니다.</span><span class="sxs-lookup"><span data-stu-id="700d8-455">A Boolean indicating whether to copy content items to the build (or publish) output folder.</span></span> <span data-ttu-id="700d8-456">기본값은 false입니다.</span><span class="sxs-lookup"><span data-stu-id="700d8-456">The default is false.</span></span> |
| <span data-ttu-id="700d8-457">**flatten**</span><span class="sxs-lookup"><span data-stu-id="700d8-457">**flatten**</span></span> | <span data-ttu-id="700d8-458">빌드 출력의 단일 폴더에 콘텐츠 항목을 복사할지(true), 아니면 패키지의 폴더 구조를 유지할지(false) 여부를 나타내는 부울 값입니다.</span><span class="sxs-lookup"><span data-stu-id="700d8-458">A Boolean indicating whether to copy content items to a single folder in the build output (true), or to preserve the folder structure in the package (false).</span></span> <span data-ttu-id="700d8-459">이 플래그는 copyToOutput 플래그가 true로 설정된 경우에만 작동합니다.</span><span class="sxs-lookup"><span data-stu-id="700d8-459">This flag only works when copyToOutput flag is set to true.</span></span> <span data-ttu-id="700d8-460">기본값은 false입니다.</span><span class="sxs-lookup"><span data-stu-id="700d8-460">The default is false.</span></span> |

<span data-ttu-id="700d8-461">패키지를 설치할 때 NuGet에서 `<contentFiles>`의 자식 요소를 위쪽에서 아래쪽으로 적용합니다.</span><span class="sxs-lookup"><span data-stu-id="700d8-461">When installing a package, NuGet applies the child elements of `<contentFiles>` from top to bottom.</span></span> <span data-ttu-id="700d8-462">여러 항목이 동일한 파일과 일치하면 모든 항목이 적용됩니다.</span><span class="sxs-lookup"><span data-stu-id="700d8-462">If multiple entries match the same file then all entries are applied.</span></span> <span data-ttu-id="700d8-463">동일한 특성에 대한 충돌이 있는 경우 최상위 항목이 하위 항목을 재정의합니다.</span><span class="sxs-lookup"><span data-stu-id="700d8-463">The top-most entry overrides the lower entries if there is a conflict for the same attribute.</span></span>

#### <a name="package-folder-structure"></a><span data-ttu-id="700d8-464">패키지 폴더 구조</span><span class="sxs-lookup"><span data-stu-id="700d8-464">Package folder structure</span></span>

<span data-ttu-id="700d8-465">패키지 프로젝트는 다음 패턴을 사용하여 콘텐츠를 구성해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="700d8-465">The package project should structure content using the following pattern:</span></span>

```
/contentFiles/{codeLanguage}/{TxM}/{any?}
```

- <span data-ttu-id="700d8-466">`codeLanguages`는 `cs`, `vb`, `fs`, `any` 또는 지정된 `$(ProjectLanguage)`에 해당하는 소문자일 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="700d8-466">`codeLanguages` may be `cs`, `vb`, `fs`, `any`, or the lowercase equivalent of a given `$(ProjectLanguage)`</span></span>
- <span data-ttu-id="700d8-467">`TxM`은 NuGet에서 지원하는 모든 법적 대상 프레임워크 모니커입니다([대상 프레임워크](../reference/target-frameworks.md) 참조).</span><span class="sxs-lookup"><span data-stu-id="700d8-467">`TxM` is any legal target framework moniker that NuGet supports (see [Target frameworks](../reference/target-frameworks.md)).</span></span>
- <span data-ttu-id="700d8-468">모든 폴더 구조는 이 구문의 끝에 추가될 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="700d8-468">Any folder structure may be appended to the end of this syntax.</span></span>

<span data-ttu-id="700d8-469">예를 들면 다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="700d8-469">For example:</span></span>

```
Language- and framework-agnostic:
    /contentFiles/any/any/config.xml

net45 content for all languages
    /contentFiles/any/net45/config.xml

C#-specific content for net45 and up
    /contentFiles/cs/net45/sample.cs
```

<span data-ttu-id="700d8-470">빈 폴더는 `.`을 사용하여 언어 및 TxM의 특정 조합에 대한 콘텐츠 제공을 거부할 수 있습니다. 예를 들어 다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="700d8-470">Empty folders can use `.` to opt out of providing content for certain combinations of language and TxM, for example:</span></span>

```
/contentFiles/vb/any/code.vb
/contentFiles/cs/any/.
```

#### <a name="example-contentfiles-section"></a><span data-ttu-id="700d8-471">contentFiles 섹션 예제</span><span class="sxs-lookup"><span data-stu-id="700d8-471">Example contentFiles section</span></span>

```xml
<?xml version="1.0" encoding="utf-8"?>
<package xmlns="http://schemas.microsoft.com/packaging/2010/07/nuspec.xsd">
    <metadata>
        ...
        <contentFiles>
            <!-- Embed image resources -->
            <files include="any/any/images/dnf.png" buildAction="EmbeddedResource" />
            <files include="any/any/images/ui.png" buildAction="EmbeddedResource" />

            <!-- Embed all image resources under contentFiles/cs/ -->
            <files include="cs/**/*.png" buildAction="EmbeddedResource" />

            <!-- Copy config.xml to the root of the output folder -->
            <files include="cs/uap/config/config.xml" buildAction="None" copyToOutput="true" flatten="true" />

            <!-- Copy run.cmd to the output folder and keep the directory structure -->
            <files include="cs/commands/run.cmd" buildAction="None" copyToOutput="true" flatten="false" />

            <!-- Include everything in the scripts folder except exe files -->
            <files include="cs/net45/scripts/*" exclude="**/*.exe"  buildAction="None" copyToOutput="true" />
        </contentFiles>
        </metadata>
</package>
```

## <a name="framework-reference-groups"></a><span data-ttu-id="700d8-472">프레임 워크 참조 그룹</span><span class="sxs-lookup"><span data-stu-id="700d8-472">Framework reference groups</span></span>

<span data-ttu-id="700d8-473">*버전 5.1 + 붙일 PackageReference only*</span><span class="sxs-lookup"><span data-stu-id="700d8-473">*Version 5.1+ wih PackageReference only*</span></span>

<span data-ttu-id="700d8-474">프레임 워크 참조는 WPF 또는 Windows Forms와 같은 공유 프레임 워크를 나타내는 .NET Core 개념입니다.</span><span class="sxs-lookup"><span data-stu-id="700d8-474">Framework References are a .NET Core concept representing shared frameworks such as WPF or Windows Forms.</span></span>
<span data-ttu-id="700d8-475">패키지는 공유 프레임 워크를 지정 하 여 모든 프레임 워크 종속성이 참조 하는 프로젝트에 포함 되도록 합니다.</span><span class="sxs-lookup"><span data-stu-id="700d8-475">By specifying a shared framework, the package ensures that all its framework dependencies are included in the referencing project.</span></span>

<span data-ttu-id="700d8-476">각 `<group>` 요소에는 `targetFramework` 특성과 0 개 이상의 `<frameworkReference>` 요소가 필요 합니다.</span><span class="sxs-lookup"><span data-stu-id="700d8-476">Each `<group>` element requires a `targetFramework` attribute and zero or more `<frameworkReference>` elements.</span></span>

<span data-ttu-id="700d8-477">다음 예제에서는 .NET Core WPF 프로젝트에 대해 생성 되는 nuspec를 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="700d8-477">The following example shows a nuspec generated for a .NET Core WPF project.</span></span>
<span data-ttu-id="700d8-478">프레임 워크 참조를 포함 하는 nuspecs를 직접 작성 하는 것은 권장 되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="700d8-478">Note that hand authoring nuspecs that contain framework references is not recommended.</span></span> <span data-ttu-id="700d8-479">대신 [대상](msbuild-targets.md) 팩을 사용 하는 것이 좋습니다. 이렇게 하면 프로젝트에서 자동으로 유추 됩니다.</span><span class="sxs-lookup"><span data-stu-id="700d8-479">Consider using the [targets](msbuild-targets.md) pack instead, which will automatically infer them from the project.</span></span>

```xml
<package xmlns="http://schemas.microsoft.com/packaging/2012/06/nuspec.xsd">
  <metadata>
    <dependencies>
      <group targetFramework=".NETCoreApp3.1" />
    </dependencies>
    <frameworkReferences>
      <group targetFramework=".NETCoreApp3.1">
        <frameworkReference name="Microsoft.WindowsDesktop.App.WPF" />
      </group>
    </frameworkReferences>
  </metadata>
</package>
```

## <a name="example-nuspec-files"></a><span data-ttu-id="700d8-480">예제 nuspec 파일</span><span class="sxs-lookup"><span data-stu-id="700d8-480">Example nuspec files</span></span>

<span data-ttu-id="700d8-481">**dependencies 또는 files를 지정하지 않은 간단한 `.nuspec`**</span><span class="sxs-lookup"><span data-stu-id="700d8-481">**A simple `.nuspec` that does not specify dependencies or files**</span></span>

```xml
<?xml version="1.0" encoding="utf-8"?>
<package xmlns="http://schemas.microsoft.com/packaging/2010/07/nuspec.xsd">
    <metadata>
        <id>sample</id>
        <version>1.2.3</version>
        <authors>Kim Abercrombie, Franck Halmaert</authors>
        <description>Sample exists only to show a sample .nuspec file.</description>
        <language>en-US</language>
        <projectUrl>http://xunit.codeplex.com/</projectUrl>
        <license type="expression">MIT</license>
    </metadata>
</package>
```

<span data-ttu-id="700d8-482">**dependencies가 있는 `.nuspec`**</span><span class="sxs-lookup"><span data-stu-id="700d8-482">**A `.nuspec` with dependencies**</span></span>

```xml
<?xml version="1.0" encoding="utf-8"?>
<package xmlns="http://schemas.microsoft.com/packaging/2010/07/nuspec.xsd">
    <metadata>
        <id>sample</id>
        <version>1.0.0</version>
        <authors>Microsoft</authors>
        <dependencies>
            <dependency id="another-package" version="3.0.0" />
            <dependency id="yet-another-package" version="1.0.0" />
        </dependencies>
    </metadata>
</package>
```

<span data-ttu-id="700d8-483">**files가 있는 `.nuspec`**</span><span class="sxs-lookup"><span data-stu-id="700d8-483">**A `.nuspec` with files**</span></span>

```xml
<?xml version="1.0"?>
<package xmlns="http://schemas.microsoft.com/packaging/2010/07/nuspec.xsd">
    <metadata>
        <id>routedebugger</id>
        <version>1.0.0</version>
        <authors>Jay Hamlin</authors>
        <requireLicenseAcceptance>false</requireLicenseAcceptance>
        <description>Route Debugger is a little utility I wrote...</description>
    </metadata>
    <files>
        <file src="bin\Debug\*.dll" target="lib" />
    </files>
</package>
```

<span data-ttu-id="700d8-484">**프레임워크 어셈블리가 있는 `.nuspec`**</span><span class="sxs-lookup"><span data-stu-id="700d8-484">**A `.nuspec` with framework assemblies**</span></span>

```xml
<?xml version="1.0"?>
<package xmlns="http://schemas.microsoft.com/packaging/2010/07/nuspec.xsd">
    <metadata>
        <id>PackageWithGacReferences</id>
        <version>1.0</version>
        <authors>Author here</authors>
        <requireLicenseAcceptance>false</requireLicenseAcceptance>
        <description>
            A package that has framework assemblyReferences depending
            on the target framework.
        </description>
        <frameworkAssemblies>
            <frameworkAssembly assemblyName="System.Web" targetFramework="net40" />
            <frameworkAssembly assemblyName="System.Net" targetFramework="net40-client, net40" />
            <frameworkAssembly assemblyName="Microsoft.Devices.Sensors" targetFramework="sl4-wp" />
            <frameworkAssembly assemblyName="System.Json" targetFramework="sl3" />
        </frameworkAssemblies>
    </metadata>
</package>
```

<span data-ttu-id="700d8-485">이 예제에서는 특정 프로젝트 대상에 대해 다음이 설치됩니다.</span><span class="sxs-lookup"><span data-stu-id="700d8-485">In this example, the following are installed for specific project targets:</span></span>

- <span data-ttu-id="700d8-486">.NET4 -> `System.Web`, `System.Net`</span><span class="sxs-lookup"><span data-stu-id="700d8-486">.NET4 -> `System.Web`, `System.Net`</span></span>
- <span data-ttu-id="700d8-487">.NET4 클라이언트 프로필 -> `System.Net`</span><span class="sxs-lookup"><span data-stu-id="700d8-487">.NET4 Client Profile -> `System.Net`</span></span>
- <span data-ttu-id="700d8-488">Silverlight 3 -> `System.Json`</span><span class="sxs-lookup"><span data-stu-id="700d8-488">Silverlight 3 -> `System.Json`</span></span>
- <span data-ttu-id="700d8-489">WindowsPhone -> `Microsoft.Devices.Sensors`</span><span class="sxs-lookup"><span data-stu-id="700d8-489">WindowsPhone -> `Microsoft.Devices.Sensors`</span></span>
