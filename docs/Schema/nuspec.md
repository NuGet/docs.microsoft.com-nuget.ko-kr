---
title: "NuGet에 대한 .nuspec 파일 참조 | Microsoft Docs"
author: kraigb
ms.author: kraigb
manager: ghogen
ms.date: 08/29/2017
ms.topic: reference
ms.prod: nuget
ms.technology: 
description: ".nuspec 파일은 패키지를 빌드하고 패키지 소비자에게 정보를 제공하는 데 사용되는 패키지 메타데이터를 포함합니다."
keywords: "nuspec 참조, NuGet 패키지 메타데이터, NuGet 패키지 매니페스트, nuspec 스키마"
ms.reviewer:
- anangaur
- karann-msft
- unniravindranathan
ms.openlocfilehash: 95f86d8cd11bce8f0f1fed068370311f575601de
ms.sourcegitcommit: 24997b5345a997501fff846c9bd73610245ae0a6
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 01/31/2018
---
# <a name="nuspec-reference"></a><span data-ttu-id="c8f31-104">.nuspec 참조</span><span class="sxs-lookup"><span data-stu-id="c8f31-104">.nuspec reference</span></span>

<span data-ttu-id="c8f31-105">`.nuspec` 파일은 패키지 메타데이터가 포함된 XML 매니페스트입니다.</span><span class="sxs-lookup"><span data-stu-id="c8f31-105">A `.nuspec` file is an XML manifest that contains package metadata.</span></span> <span data-ttu-id="c8f31-106">이 매니페스트는 패키지를 빌드하고 소비자에게 정보를 제공하는 데 사용됩니다.</span><span class="sxs-lookup"><span data-stu-id="c8f31-106">This manifest is used both to build the package and to provide information to consumers.</span></span> <span data-ttu-id="c8f31-107">매니페스트는 항상 패키지에 포함됩니다.</span><span class="sxs-lookup"><span data-stu-id="c8f31-107">The manifest is always included in a package.</span></span>

<span data-ttu-id="c8f31-108">항목 내용:</span><span class="sxs-lookup"><span data-stu-id="c8f31-108">In this topic:</span></span>

- [<span data-ttu-id="c8f31-109">일반 형식 및 스키마</span><span class="sxs-lookup"><span data-stu-id="c8f31-109">General form and schema</span></span>](#general-form-and-schema)
- <span data-ttu-id="c8f31-110">[대체 토큰](#replacement-tokens)(Visual Studio 프로젝트에서 사용하는 경우)</span><span class="sxs-lookup"><span data-stu-id="c8f31-110">[Replacement tokens](#replacement-tokens) (when used with a Visual Studio project)</span></span>
- [<span data-ttu-id="c8f31-111">종속성</span><span class="sxs-lookup"><span data-stu-id="c8f31-111">Dependencies</span></span>](#dependencies)
- [<span data-ttu-id="c8f31-112">명시적 어셈블리 참조</span><span class="sxs-lookup"><span data-stu-id="c8f31-112">Explicit assembly references</span></span>](#explicit-assembly-references)
- [<span data-ttu-id="c8f31-113">프레임워크 어셈블리 참조</span><span class="sxs-lookup"><span data-stu-id="c8f31-113">Framework assembly references</span></span>](#framework-assembly-references)
- [<span data-ttu-id="c8f31-114">어셈블리 파일 포함</span><span class="sxs-lookup"><span data-stu-id="c8f31-114">Including assembly files</span></span>](#including-assembly-files)
- [<span data-ttu-id="c8f31-115">콘텐츠 파일 포함</span><span class="sxs-lookup"><span data-stu-id="c8f31-115">Including content files</span></span>](#including-content-files)
- [<span data-ttu-id="c8f31-116">예제</span><span class="sxs-lookup"><span data-stu-id="c8f31-116">Examples</span></span>](#examples)

## <a name="general-form-and-schema"></a><span data-ttu-id="c8f31-117">일반 형식 및 스키마</span><span class="sxs-lookup"><span data-stu-id="c8f31-117">General form and schema</span></span>

<span data-ttu-id="c8f31-118">현재 `nuspec.xsd` 스키마 파일은 [NuGet GitHub 리포지토리](https://github.com/NuGet/NuGet.Client/blob/dev/src/NuGet.Core/NuGet.Packaging/compiler/resources/nuspec.xsd)에 있습니다.</span><span class="sxs-lookup"><span data-stu-id="c8f31-118">The current `nuspec.xsd` schema file can be found in the [NuGet GitHub repository](https://github.com/NuGet/NuGet.Client/blob/dev/src/NuGet.Core/NuGet.Packaging/compiler/resources/nuspec.xsd).</span></span>

<span data-ttu-id="c8f31-119">이 스키마 내에서 `.nuspec` 파일의 일반 형식은 다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="c8f31-119">Within this schema, a `.nuspec` file has the following general form:</span></span>

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

<span data-ttu-id="c8f31-120">스키마를 시각적으로 명확하게 표시하려면, Visual Studio에서 디자인 모드로 스키마 파일을 열고 **XML 스키마 탐색기** 링크를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="c8f31-120">For a clear visual representation of the schema, open the schema file in Visual Studio in Design mode and click on the **XML Schema Explorer** link.</span></span> <span data-ttu-id="c8f31-121">또는 파일을 코드로 열고, 편집기에서 마우스 오른쪽 단추를 클릭한 다음, **XML 스키마 탐색기 표시**를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="c8f31-121">Alternately, open the file as code, right-click in the editor, and select **Show XML Schema Explorer**.</span></span> <span data-ttu-id="c8f31-122">어느 방법이든 아래와 같은 보기가 표시됩니다(대부분의 경우 펼쳐져 있음).</span><span class="sxs-lookup"><span data-stu-id="c8f31-122">Either way you get a view like the one below (when mostly expanded):</span></span>

![nuspec.xsd가 열려 있는 Visual Studio 스키마 탐색기](media/SchemaExplorer.png)

### <a name="metadata-attributes"></a><span data-ttu-id="c8f31-124">metadata 특성</span><span class="sxs-lookup"><span data-stu-id="c8f31-124">Metadata attributes</span></span>

<span data-ttu-id="c8f31-125">`<metadata>` 요소는 다음 표에서 설명하는 특성을 지원합니다.</span><span class="sxs-lookup"><span data-stu-id="c8f31-125">The `<metadata>` element supports the attributes described in the following table.</span></span>

| <span data-ttu-id="c8f31-126">특성</span><span class="sxs-lookup"><span data-stu-id="c8f31-126">Attribute</span></span> | <span data-ttu-id="c8f31-127">필수</span><span class="sxs-lookup"><span data-stu-id="c8f31-127">Required</span></span> | <span data-ttu-id="c8f31-128">설명</span><span class="sxs-lookup"><span data-stu-id="c8f31-128">Description</span></span> |
| --- | --- | --- | 
| <span data-ttu-id="c8f31-129">**minClientVersion**</span><span class="sxs-lookup"><span data-stu-id="c8f31-129">**minClientVersion**</span></span> | <span data-ttu-id="c8f31-130">아니요</span><span class="sxs-lookup"><span data-stu-id="c8f31-130">No</span></span> | <span data-ttu-id="c8f31-131">nuget.exe 및 Visual Studio 패키지 관리자에 의해 적용되는, 이 패키지를 설치할 수 있는 NuGet 클라이언트의 최소 버전을 지정합니다.</span><span class="sxs-lookup"><span data-stu-id="c8f31-131">Specifies the minimum version of the NuGet client that can install this package, enforced by nuget.exe and the Visual Studio Package Manager.</span></span> <span data-ttu-id="c8f31-132">패키지가 특정 버전의 NuGet 클라이언트에 추가된 `.nuspec` 파일의 특정 기능에 종속될 때마다 이 특성이 사용됩니다.</span><span class="sxs-lookup"><span data-stu-id="c8f31-132">This is used whenever the package depends on specific features of the `.nuspec` file that were added in a particular version of the NuGet client.</span></span> <span data-ttu-id="c8f31-133">예를 들어 `developmentDependency` 특성을 사용하는 패키지는 `minClientVersion`에 대해 "2.8"을 지정해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="c8f31-133">For example, a package using the `developmentDependency` attribute should specify "2.8" for `minClientVersion`.</span></span> <span data-ttu-id="c8f31-134">마찬가지로 `contentFiles` 요소(다음 섹션 참조)를 사용하는 패키지는 `minClientVersion`을 "3.3"으로 설정해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="c8f31-134">Similarly, a package using the `contentFiles` element (see the next section) should set `minClientVersion` to "3.3".</span></span> <span data-ttu-id="c8f31-135">또한 2.5 이전의 NuGet 클라이언트에서는 이 플래그를 인식하지 못하기 때문에 `minClientVersion`에 포함된 내용에 관계없이 *항상* 패키지 설치를 거부합니다.</span><span class="sxs-lookup"><span data-stu-id="c8f31-135">Note also that because NuGet clients prior to 2.5 do not recognize this flag, they *always* refuse to install the package no matter what `minClientVersion` contains.</span></span> |

### <a name="required-metadata-elements"></a><span data-ttu-id="c8f31-136">필수 metadata 요소</span><span class="sxs-lookup"><span data-stu-id="c8f31-136">Required metadata elements</span></span>

<span data-ttu-id="c8f31-137">다음 요소는 패키지에 대한 최소 요구 사항이지만, [선택적 metadata 요소](#optional-metadata-elements)를 추가하여 개발자가 사용하는 패키지에 대한 전반적인 환경을 향상시키는 것이 좋습니다.</span><span class="sxs-lookup"><span data-stu-id="c8f31-137">Although the following elements are the minimum requirements for a package, you should consider adding the [optional metadata elements](#optional-metadata-elements) to improve the overall experience developers have with your package.</span></span>

<span data-ttu-id="c8f31-138">이러한 요소는 `<metadata>` 요소 내에 나타나야 합니다.</span><span class="sxs-lookup"><span data-stu-id="c8f31-138">These elements must appear within a `<metadata>` element.</span></span>

| <span data-ttu-id="c8f31-139">요소</span><span class="sxs-lookup"><span data-stu-id="c8f31-139">Element</span></span> | <span data-ttu-id="c8f31-140">설명</span><span class="sxs-lookup"><span data-stu-id="c8f31-140">Description</span></span> |
| --- | --- |
| <span data-ttu-id="c8f31-141">**ID**</span><span class="sxs-lookup"><span data-stu-id="c8f31-141">**id**</span></span> | <span data-ttu-id="c8f31-142">대/소문자를 구분하지 않는 패키지 식별자이며, nuget.org 또는 패키지가 상주하는 모든 갤러리에서 고유해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="c8f31-142">The case-insensitive package identifier, which must be unique across nuget.org or whatever gallery the package resides in.</span></span> <span data-ttu-id="c8f31-143">ID는 URL에 유효하지 않은 공백 또는 문자를 포함할 수 없고, 일반적으로 .NET 네임스페이스 규칙을 따릅니다.</span><span class="sxs-lookup"><span data-stu-id="c8f31-143">IDs may not contain spaces or characters that are not valid for a URL, and generally follow .NET namespace rules.</span></span> <span data-ttu-id="c8f31-144">지침은 [고유한 패키지 식별자 선택](../create-packages/creating-a-package.md#choosing-a-unique-package-identifier-and-setting-the-version-number)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="c8f31-144">See [Choosing a unique package identifier](../create-packages/creating-a-package.md#choosing-a-unique-package-identifier-and-setting-the-version-number) for guidance.</span></span> |
| <span data-ttu-id="c8f31-145">**version**</span><span class="sxs-lookup"><span data-stu-id="c8f31-145">**version**</span></span> | <span data-ttu-id="c8f31-146">*major.minor.patch* 패턴을 따르는 패키지의 버전입니다.</span><span class="sxs-lookup"><span data-stu-id="c8f31-146">The version of the package, following the *major.minor.patch* pattern.</span></span> <span data-ttu-id="c8f31-147">버전 번호는 [패키지 버전 관리](../reference/package-versioning.md#pre-release-versions)에서 설명한 대로 시험판 접미사를 포함할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="c8f31-147">Version numbers may include a pre-release suffix as described in [Package versioning](../reference/package-versioning.md#pre-release-versions).</span></span> |
| <span data-ttu-id="c8f31-148">**description**</span><span class="sxs-lookup"><span data-stu-id="c8f31-148">**description**</span></span> | <span data-ttu-id="c8f31-149">UI 표시를 위한 패키지에 대한 자세한 설명입니다.</span><span class="sxs-lookup"><span data-stu-id="c8f31-149">A long description of the package for UI display.</span></span> |
| <span data-ttu-id="c8f31-150">**authors**</span><span class="sxs-lookup"><span data-stu-id="c8f31-150">**authors**</span></span> | <span data-ttu-id="c8f31-151">nuget.org에서 프로필 이름과 일치하는, 쉼표로 구분된 패키지 작성자 목록입니다. 이러한 목록은 nuget.org의 NuGet 갤러리에 표시되고 동일한 작성자가 패키지를 상호 참조하는 데 사용됩니다.</span><span class="sxs-lookup"><span data-stu-id="c8f31-151">A comma-separated list of packages authors, matching the profile names on nuget.org. These are displayed in the NuGet Gallery on nuget.org and are used to cross-reference packages by the same authors.</span></span> |

### <a name="optional-metadata-elements"></a><span data-ttu-id="c8f31-152">선택적 metadata 요소</span><span class="sxs-lookup"><span data-stu-id="c8f31-152">Optional metadata elements</span></span>

<span data-ttu-id="c8f31-153">이러한 요소는 `<metadata>` 요소 내에 나타날 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="c8f31-153">These elements may appear within a `<metadata>` element.</span></span>

#### <a name="single-elements"></a><span data-ttu-id="c8f31-154">단일 요소</span><span class="sxs-lookup"><span data-stu-id="c8f31-154">Single elements</span></span>

| <span data-ttu-id="c8f31-155">요소</span><span class="sxs-lookup"><span data-stu-id="c8f31-155">Element</span></span> | <span data-ttu-id="c8f31-156">설명</span><span class="sxs-lookup"><span data-stu-id="c8f31-156">Description</span></span> |
| --- | --- |
| <span data-ttu-id="c8f31-157">**title**</span><span class="sxs-lookup"><span data-stu-id="c8f31-157">**title**</span></span> | <span data-ttu-id="c8f31-158">사람들에게 친숙한 패키지 제목이며 보통 nuget.org 및 Visual Studio의 패키지 관리자에서 UI 표시에 사용됩니다.</span><span class="sxs-lookup"><span data-stu-id="c8f31-158">A human-friendly title of the package, typically used in UI displays as on nuget.org and the Package Manager in Visual Studio.</span></span> <span data-ttu-id="c8f31-159">지정하지 않으면 패키지 ID가 사용됩니다.</span><span class="sxs-lookup"><span data-stu-id="c8f31-159">If not specified, the package ID is used.</span></span> |
| <span data-ttu-id="c8f31-160">**owners**</span><span class="sxs-lookup"><span data-stu-id="c8f31-160">**owners**</span></span> | <span data-ttu-id="c8f31-161">nuget.org에서 프로필 이름을 사용하는 패키지 작성자에 대한 쉼표로 구분된 목록입니다. 이는 종종 `authors`에 있는 것과 동일한 목록이며, 패키지를 nuget.org에 업로드할 때 무시됩니다. [nuget.org에서 패키지 소유자 관리](../create-packages/publish-a-package.md#managing-package-owners-on-nugetorg)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="c8f31-161">A comma-separated list of the package creators using profile names on nuget.org. This is often the same list as in `authors`, and is ignored when uploading the package to nuget.org. See [Managing package owners on nuget.org](../create-packages/publish-a-package.md#managing-package-owners-on-nugetorg).</span></span> |
| <span data-ttu-id="c8f31-162">**projectUrl**</span><span class="sxs-lookup"><span data-stu-id="c8f31-162">**projectUrl**</span></span> | <span data-ttu-id="c8f31-163">nuget.org뿐만 아니라 종종 UI 표시에 표시되는 패키지의 홈페이지에 대한 URL입니다.</span><span class="sxs-lookup"><span data-stu-id="c8f31-163">A URL for the package's home page, often shown in UI displays as well as nuget.org.</span></span> |
| <span data-ttu-id="c8f31-164">**licenseUrl**</span><span class="sxs-lookup"><span data-stu-id="c8f31-164">**licenseUrl**</span></span> | <span data-ttu-id="c8f31-165">nuget.org뿐만 아니라 UI 표시에도 종종 표시되는 패키지의 라이선스에 대한 URL입니다.</span><span class="sxs-lookup"><span data-stu-id="c8f31-165">A URL for the package's license, often shown in UI displays as well as nuget.org.</span></span> |
| <span data-ttu-id="c8f31-166">**iconUrl**</span><span class="sxs-lookup"><span data-stu-id="c8f31-166">**iconUrl**</span></span> | <span data-ttu-id="c8f31-167">UI 표시에서 패키지에 대한 아이콘으로 사용하는 투명한 배경이 있는 64x64 이미지에 대한 URL입니다.</span><span class="sxs-lookup"><span data-stu-id="c8f31-167">A URL for a 64x64 image with transparency background to use as the icon for the package in UI display.</span></span> <span data-ttu-id="c8f31-168">이 요소에는 이미지가 포함된 웹 페이지의 URL이 아니라 *직접 이미지 URL*이 포함되어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="c8f31-168">Be sure this element contains the *direct image URL* and not the URL of a web page containing the image.</span></span> <span data-ttu-id="c8f31-169">예를 들어 GitHub의 이미지를 사용하려면 `https://github.com/<username>/<repository>/raw/<branch>/<logo.png>`와 같은 원시 파일 URL을 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="c8f31-169">For example, to use an image from GitHub, use the raw file URL like `https://github.com/<username>/<repository>/raw/<branch>/<logo.png>`.</span></span> |
| <span data-ttu-id="c8f31-170">**requireLicenseAcceptance**</span><span class="sxs-lookup"><span data-stu-id="c8f31-170">**requireLicenseAcceptance**</span></span> | <span data-ttu-id="c8f31-171">패키지를 설치하기 전에 클라이언트에서 소비자가 패키지 라이선스에 동의하도록 요구하는 메시지를 표시해야 할지 여부를 지정하는 부울 값입니다.</span><span class="sxs-lookup"><span data-stu-id="c8f31-171">A Boolean value specifying whether the client must prompt the consumer to accept the package license before installing the package.</span></span> |
| <span data-ttu-id="c8f31-172">**developmentDependency**</span><span class="sxs-lookup"><span data-stu-id="c8f31-172">**developmentDependency**</span></span> | <span data-ttu-id="c8f31-173">*(2.8 이상)* 패키지가 다른 패키지의 종속성으로 포함되지 않도록 패키지를 개발 전용 종속성으로 표시할지 여부를 지정 하는 부울 값입니다.</span><span class="sxs-lookup"><span data-stu-id="c8f31-173">*(2.8+)* A Boolean value specifying whether the package is be marked as a development-only-dependency, which prevents the package from being included as a dependency in other packages.</span></span> |
| <span data-ttu-id="c8f31-174">**요약**</span><span class="sxs-lookup"><span data-stu-id="c8f31-174">**summary**</span></span> | <span data-ttu-id="c8f31-175">UI 표시를 위한 패키지에 대한 간단한 설명입니다.</span><span class="sxs-lookup"><span data-stu-id="c8f31-175">A short description of the package for UI display.</span></span> <span data-ttu-id="c8f31-176">생략하면 `description`의 잘린 버전이 사용됩니다.</span><span class="sxs-lookup"><span data-stu-id="c8f31-176">If omitted, a truncated version of `description` is used.</span></span> |
| <span data-ttu-id="c8f31-177">**releaseNotes**</span><span class="sxs-lookup"><span data-stu-id="c8f31-177">**releaseNotes**</span></span> | <span data-ttu-id="c8f31-178">*(1.5 이상)* 패키지 설명 대신 Visual Studio 패키지 관리자의 **업데이트** 탭처럼 UI에서 자주 사용되는 이 패키지 릴리스의 변경 내용에 대한 설명입니다.</span><span class="sxs-lookup"><span data-stu-id="c8f31-178">*(1.5+)* A description of the changes made in this release of the package, often used in UI like the **Updates** tab of the Visual Studio Package Manager in place of the package description.</span></span> |
| <span data-ttu-id="c8f31-179">**copyright**</span><span class="sxs-lookup"><span data-stu-id="c8f31-179">**copyright**</span></span> | <span data-ttu-id="c8f31-180">*(1.5 이상)* 패키지에 대한 저작권 세부 정보입니다.</span><span class="sxs-lookup"><span data-stu-id="c8f31-180">*(1.5+)* Copyright details for the package.</span></span> |
| <span data-ttu-id="c8f31-181">**language**</span><span class="sxs-lookup"><span data-stu-id="c8f31-181">**language**</span></span> | <span data-ttu-id="c8f31-182">패키지에 대한 로캘 ID입니다.</span><span class="sxs-lookup"><span data-stu-id="c8f31-182">The locale ID for the package.</span></span> <span data-ttu-id="c8f31-183">[지역화된 패키지 만들기](../create-packages/creating-localized-packages.md)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="c8f31-183">See [Creating localized packages](../create-packages/creating-localized-packages.md).</span></span> |
| <span data-ttu-id="c8f31-184">**tags**</span><span class="sxs-lookup"><span data-stu-id="c8f31-184">**tags**</span></span> | <span data-ttu-id="c8f31-185">패키지를 설명하고 검색 및 필터링을 통해 패키지의 검색 기능을 지원하는 태그 및 키워드에 대한 공백으로 구분된 목록입니다.</span><span class="sxs-lookup"><span data-stu-id="c8f31-185">A space-delimited list of tags and keywords that describe the package and aid discoverability of packages through search and filtering.</span></span> |
| <span data-ttu-id="c8f31-186">**serviceable**</span><span class="sxs-lookup"><span data-stu-id="c8f31-186">**serviceable**</span></span> | <span data-ttu-id="c8f31-187">*(3.3 이상)* NuGet 내부 전용입니다.</span><span class="sxs-lookup"><span data-stu-id="c8f31-187">*(3.3+)* For internal NuGet use only.</span></span> |

#### <a name="collection-elements"></a><span data-ttu-id="c8f31-188">컬렉션 요소</span><span class="sxs-lookup"><span data-stu-id="c8f31-188">Collection elements</span></span>

| <span data-ttu-id="c8f31-189">요소</span><span class="sxs-lookup"><span data-stu-id="c8f31-189">Element</span></span> | <span data-ttu-id="c8f31-190">설명</span><span class="sxs-lookup"><span data-stu-id="c8f31-190">Description</span></span> |
| --- | --- |
<span data-ttu-id="c8f31-191">**packageTypes**</span><span class="sxs-lookup"><span data-stu-id="c8f31-191">**packageTypes**</span></span> | <span data-ttu-id="c8f31-192">*(3.5 이상)* 기존 종속 패키지가 아닌 경우 패키지의 유형을 지정하는 0개 이상의 `<packageType>` 요소 컬렉션입니다.</span><span class="sxs-lookup"><span data-stu-id="c8f31-192">*(3.5+)* A collection of zero or more `<packageType>` elements specifying the type of the package if other than a traditional dependency package.</span></span> <span data-ttu-id="c8f31-193">각 packageType에는 *name* 및 *version* 특성이 있습니다.</span><span class="sxs-lookup"><span data-stu-id="c8f31-193">Each packageType has attributes of *name* and *version*.</span></span> <span data-ttu-id="c8f31-194">[패키지 유형 설정](../create-packages/creating-a-package.md#setting-a-package-type)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="c8f31-194">See [Setting a package type](../create-packages/creating-a-package.md#setting-a-package-type).</span></span> |
| <span data-ttu-id="c8f31-195">**dependencies**</span><span class="sxs-lookup"><span data-stu-id="c8f31-195">**dependencies**</span></span> | <span data-ttu-id="c8f31-196">패키지에 대한 종속성을 지정하는 0개 이상의 `<dependency>` 요소 컬렉션입니다.</span><span class="sxs-lookup"><span data-stu-id="c8f31-196">A collection of zero or more `<dependency>` elements specifying the dependencies for the package.</span></span> <span data-ttu-id="c8f31-197">각 종속성에는 *id*, *version*, *include*(3.x 이상) 및 *exclude*(3.x 이상) 특성이 있습니다.</span><span class="sxs-lookup"><span data-stu-id="c8f31-197">Each dependency has attributes of *id*, *version*, *include* (3.x+), and *exclude* (3.x+).</span></span> <span data-ttu-id="c8f31-198">아래의 [종속성](#dependencies)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="c8f31-198">See [Dependencies](#dependencies) below.</span></span> |
| <span data-ttu-id="c8f31-199">**frameworkAssemblies**</span><span class="sxs-lookup"><span data-stu-id="c8f31-199">**frameworkAssemblies**</span></span> | <span data-ttu-id="c8f31-200">*(1.2 이상)* 이 패키지에 필요한 .NET Framework 어셈블리 참조를 식별하는 0개 이상의 `<frameworkAssembly>` 요소 컬렉션이며, 패키지를 사용하는 프로젝트에 참조가 추가되도록 합니다.</span><span class="sxs-lookup"><span data-stu-id="c8f31-200">*(1.2+)* A collection of zero or more `<frameworkAssembly>` elements identifying .NET Framework assembly references that this package requires, which ensures that references are added to projects consuming the package.</span></span> <span data-ttu-id="c8f31-201">각 frameworkAssembly에는 *assemblyName* 및 *targetFramework* 특성이 있습니다.</span><span class="sxs-lookup"><span data-stu-id="c8f31-201">Each frameworkAssembly has *assemblyName* and *targetFramework* attributes.</span></span> <span data-ttu-id="c8f31-202">아래의 [프레임워크 어셈블리 참조 GAC 지정](#specifying-framework-assembly-references-gac)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="c8f31-202">See [Specifying framework assembly references GAC](#specifying-framework-assembly-references-gac) below.</span></span> |
| <span data-ttu-id="c8f31-203">**references**</span><span class="sxs-lookup"><span data-stu-id="c8f31-203">**references**</span></span> | <span data-ttu-id="c8f31-204">*(1.5 이상)* 프로젝트 참조로 추가된 패키지의 `lib` 폴더에 있는 어셈블리를 명명하는 0개 이상의 `<reference>` 요소 컬렉션입니다.</span><span class="sxs-lookup"><span data-stu-id="c8f31-204">*(1.5+)* A collection of zero or more `<reference>` elements naming assemblies in the package's `lib` folder that are added as project references.</span></span> <span data-ttu-id="c8f31-205">각 참조에는 *file* 특성이 있습니다.</span><span class="sxs-lookup"><span data-stu-id="c8f31-205">Each reference has a *file* attribute.</span></span> <span data-ttu-id="c8f31-206">또한 `<references>`에는 *targetFramework* 특성이 있는 `<group>` 요소도 포함될 수 있으며, 그런 다음 `<reference>` 요소가 포함됩니다.</span><span class="sxs-lookup"><span data-stu-id="c8f31-206">`<references>` can also contain a `<group>` element with a *targetFramework* attribute, that then contains `<reference>` elements.</span></span> <span data-ttu-id="c8f31-207">생략하면 `lib`의 모든 참조가 포함됩니다.</span><span class="sxs-lookup"><span data-stu-id="c8f31-207">If omitted, all references in `lib` are included.</span></span> <span data-ttu-id="c8f31-208">아래의 [명시적 어셈블리 참조 지정](#specifying-explicit-assembly-references)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="c8f31-208">See [Specifying explicit assembly references](#specifying-explicit-assembly-references) below.</span></span> |
| <span data-ttu-id="c8f31-209">**contentFiles**</span><span class="sxs-lookup"><span data-stu-id="c8f31-209">**contentFiles**</span></span> | <span data-ttu-id="c8f31-210">*(3.3 이상)* 사용하는 프로젝트에 포함할 콘텐츠 파일을 식별하는 `<files>` 요소 컬렉션입니다.</span><span class="sxs-lookup"><span data-stu-id="c8f31-210">*(3.3+)* A collection of `<files>` elements that identify content files to include in the consuming project.</span></span> <span data-ttu-id="c8f31-211">이러한 파일은 프로젝트 시스템 내에서 사용되는 방법을 설명하는 일단의 특성으로 지정됩니다.</span><span class="sxs-lookup"><span data-stu-id="c8f31-211">These files are specified with a set of attributes that describe how they should be used within the project system.</span></span> <span data-ttu-id="c8f31-212">아래의 [패키지에 포함할 파일 지정](#specifying-files-to-include-in-the-package)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="c8f31-212">See [Specifying files to include in the package](#specifying-files-to-include-in-the-package) below.</span></span> |

### <a name="files-element"></a><span data-ttu-id="c8f31-213">Files 요소</span><span class="sxs-lookup"><span data-stu-id="c8f31-213">Files element</span></span>

<span data-ttu-id="c8f31-214">`<package>` 노드는 패키지에 포함할 어셈블리 및 콘텐츠 파일을 지정하기 위해 `<files>` 노드를 `<metadata>`에 대한 형제로 포함하고 a 또는 `<contentFiles>` 자식을 `<metadata>` 아래에 포함할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="c8f31-214">The `<package>` node may contain a `<files>` node as a sibling to `<metadata>`, and a or `<contentFiles>` child under `<metadata>`, to specify which assembly and content files to include in the package.</span></span> <span data-ttu-id="c8f31-215">자세한 내용은 이 항목의 뒷부분에 있는 [어셈블리 파일 포함](#including-assembly-files) 및 [콘텐츠 파일 포함](#including-content-files)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="c8f31-215">See [Including assembly files](#including-assembly-files) and [Including content files](#including-content-files) later in this topic for details.</span></span>

## <a name="replacement-tokens"></a><span data-ttu-id="c8f31-216">대체 토큰</span><span class="sxs-lookup"><span data-stu-id="c8f31-216">Replacement tokens</span></span>

<span data-ttu-id="c8f31-217">패키지를 만들 때 [`nuget pack` 명령](../tools/cli-ref-pack.md)은 `.nuspec` 파일의 `<metadata>` 노드에 있는 $로 구분된 토큰을 프로젝트 파일 또는 `pack` 명령의 `-properties` 스위치에서 제공하는 값으로 바꿉니다 .</span><span class="sxs-lookup"><span data-stu-id="c8f31-217">When creating a package, the [`nuget pack` command](../tools/cli-ref-pack.md) replaces $-delimited tokens in the `.nuspec` file's `<metadata>` node with values that come from either a project file or the `pack` command's `-properties` switch.</span></span>

<span data-ttu-id="c8f31-218">명령줄에서 `nuget pack -properties <name>=<value>;<name>=<value>`를 사용하여 토큰 값을 지정합니다.</span><span class="sxs-lookup"><span data-stu-id="c8f31-218">On the command line, you specify token values with `nuget pack -properties <name>=<value>;<name>=<value>`.</span></span> <span data-ttu-id="c8f31-219">예를 들어 `.nuspec`에서 `$owners$` 및 `$desc$`와 같은 토큰을 사용하고 다음과 같이 압축 시간에 값을 제공할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="c8f31-219">For example, you can use a token such as `$owners$` and `$desc$` in the `.nuspec` and provide the values at packing time as follows:</span></span>

```ps
nuget pack MyProject.csproj -properties
    owners=janedoe,harikm,kimo,xiaop;desc="Awesome app logger utility"
```

<span data-ttu-id="c8f31-220">프로젝트의 값을 사용하려면 아래 표에서 설명한 토큰을 지정합니다(AssemblyInfo는 `AssemblyInfo.cs` 또는 `AssemblyInfo.vb`과 같이 `Properties`의 파일을 나타냄).</span><span class="sxs-lookup"><span data-stu-id="c8f31-220">To use values from a project, specify the tokens described in the table below (AssemblyInfo refers to the file in `Properties` such as `AssemblyInfo.cs` or `AssemblyInfo.vb`).</span></span>

<span data-ttu-id="c8f31-221">이러한 토큰을 사용하려면 `.nuspec` 대신 프로젝트 파일이 있는 `nuget pack`을 실행합니다.</span><span class="sxs-lookup"><span data-stu-id="c8f31-221">To use these tokens, run `nuget pack` with the project file rather than just the `.nuspec`.</span></span> <span data-ttu-id="c8f31-222">예를 들어 다음 명령을 사용하는 경우 `.nuspec` 파일의 `$id$` 및 `$version$` 토큰을 프로젝트의 `AssemblyName` 및 `AssemblyVersion` 값으로 바꿉니다.</span><span class="sxs-lookup"><span data-stu-id="c8f31-222">For example, when using the following command, the `$id$` and `$version$` tokens in a `.nuspec` file are replaced with the project's `AssemblyName` and `AssemblyVersion` values:</span></span>

```ps
nuget pack MyProject.csproj
```

<span data-ttu-id="c8f31-223">일반적으로 프로젝트가 있는 경우 처음에는 이러한 표준 토큰 중 일부가 자동으로 포함되는 `nuget spec MyProject.csproj`를 사용하여 `.nuspec`을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="c8f31-223">Typically, when you have a project, you create the `.nuspec` initially using `nuget spec MyProject.csproj` which automatically includes some of these standard tokens.</span></span> <span data-ttu-id="c8f31-224">그러나 프로젝트에 필요한 `.nuspec` 요소 값이 부족하면 `nuget pack`이 실패합니다.</span><span class="sxs-lookup"><span data-stu-id="c8f31-224">However, if a project lacks values for required `.nuspec` elements, then `nuget pack` fails.</span></span> <span data-ttu-id="c8f31-225">또한 프로젝트 값을 변경하는 경우 패키지를 만들기 전에 다시 빌드해야 합니다. 이 경우 pack 명령의 `build` 스위치를 사용하여 편리하게 수행할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="c8f31-225">Furthermore, if you change project values, be sure to rebuild before creating the package; this can be done conveniently with the pack command's `build` switch.</span></span>

<span data-ttu-id="c8f31-226">`$configuration$`을 제외하고는 프로젝트의 값이 명령줄에서 동일한 토큰에 할당된 값보다 우선적으로 사용됩니다.</span><span class="sxs-lookup"><span data-stu-id="c8f31-226">With the exception of `$configuration$`, values in the project are used in preference to any assigned to the same token on the command line.</span></span>

| <span data-ttu-id="c8f31-227">토큰</span><span class="sxs-lookup"><span data-stu-id="c8f31-227">Token</span></span> | <span data-ttu-id="c8f31-228">값 원본</span><span class="sxs-lookup"><span data-stu-id="c8f31-228">Value source</span></span> | <span data-ttu-id="c8f31-229">값</span><span class="sxs-lookup"><span data-stu-id="c8f31-229">Value</span></span>
| --- | --- | ---
| <span data-ttu-id="c8f31-230">**$id$**</span><span class="sxs-lookup"><span data-stu-id="c8f31-230">**$id$**</span></span> | <span data-ttu-id="c8f31-231">프로젝트 파일</span><span class="sxs-lookup"><span data-stu-id="c8f31-231">Project file</span></span> | <span data-ttu-id="c8f31-232">프로젝트 파일의 AssemblyName</span><span class="sxs-lookup"><span data-stu-id="c8f31-232">AssemblyName from the project file</span></span> |
| <span data-ttu-id="c8f31-233">**$version$**</span><span class="sxs-lookup"><span data-stu-id="c8f31-233">**$version$**</span></span> | <span data-ttu-id="c8f31-234">AssemblyInfo</span><span class="sxs-lookup"><span data-stu-id="c8f31-234">AssemblyInfo</span></span> | <span data-ttu-id="c8f31-235">있는 경우 AssemblyInformationalVersion, 그렇지 않으면 AssemblyVersion</span><span class="sxs-lookup"><span data-stu-id="c8f31-235">AssemblyInformationalVersion if present, otherwise AssemblyVersion</span></span> |
| <span data-ttu-id="c8f31-236">**$author$**</span><span class="sxs-lookup"><span data-stu-id="c8f31-236">**$author$**</span></span> | <span data-ttu-id="c8f31-237">AssemblyInfo</span><span class="sxs-lookup"><span data-stu-id="c8f31-237">AssemblyInfo</span></span> | <span data-ttu-id="c8f31-238">AssemblyCompany</span><span class="sxs-lookup"><span data-stu-id="c8f31-238">AssemblyCompany</span></span> |
| <span data-ttu-id="c8f31-239">**$description$**</span><span class="sxs-lookup"><span data-stu-id="c8f31-239">**$description$**</span></span> | <span data-ttu-id="c8f31-240">AssemblyInfo</span><span class="sxs-lookup"><span data-stu-id="c8f31-240">AssemblyInfo</span></span> | <span data-ttu-id="c8f31-241">AssemblyDescription</span><span class="sxs-lookup"><span data-stu-id="c8f31-241">AssemblyDescription</span></span> |
| <span data-ttu-id="c8f31-242">**$copyright$**</span><span class="sxs-lookup"><span data-stu-id="c8f31-242">**$copyright$**</span></span> | <span data-ttu-id="c8f31-243">AssemblyInfo</span><span class="sxs-lookup"><span data-stu-id="c8f31-243">AssemblyInfo</span></span> | <span data-ttu-id="c8f31-244">AssemblyCopyright</span><span class="sxs-lookup"><span data-stu-id="c8f31-244">AssemblyCopyright</span></span> |
| <span data-ttu-id="c8f31-245">**$configuration$**</span><span class="sxs-lookup"><span data-stu-id="c8f31-245">**$configuration$**</span></span> | <span data-ttu-id="c8f31-246">어셈블리 DLL</span><span class="sxs-lookup"><span data-stu-id="c8f31-246">Assembly DLL</span></span> | <span data-ttu-id="c8f31-247">어셈블리를 빌드하는 데 사용되는 구성이며, 기본값은 Debug입니다.</span><span class="sxs-lookup"><span data-stu-id="c8f31-247">Configuration used to build the assembly, defaulting to Debug.</span></span> <span data-ttu-id="c8f31-248">Release 구성을 사용하여 패키지를 만들려면 항상 명령줄에서 `-properties Configuration=Release`를 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="c8f31-248">Note that to create a package using a Release configuration, you always use `-properties Configuration=Release` on the command line.</span></span> |

<span data-ttu-id="c8f31-249">또한 토큰은 [어셈블리 파일](#including-assembly-files) 및 [콘텐츠 파일](#including-content-files)을 포함할 때 경로를 확인하는 데 사용할 수도 있습니다.</span><span class="sxs-lookup"><span data-stu-id="c8f31-249">Tokens can also be used to resolve paths when you include [assembly files](#including-assembly-files) and [content files](#including-content-files).</span></span> <span data-ttu-id="c8f31-250">토큰의 이름은 MSBuild 속성과 동일하므로 현재 빌드 구성에 따라 포함할 파일을 선택할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="c8f31-250">The tokens have the same names as the MSBuild properties, making it possible to select files to be included depending on the current build configuration.</span></span> <span data-ttu-id="c8f31-251">예를 들어 `.nuspec` 파일에서 다음 토큰을 사용하는 경우가 있습니다.</span><span class="sxs-lookup"><span data-stu-id="c8f31-251">For example, if you use the following tokens in the `.nuspec` file:</span></span>

```xml
<files>
    <file src="bin\$configuration$\$id$.pdb" target="lib\net40" />
</files>
```

<span data-ttu-id="c8f31-252">그리고 MSBuild의 `Release` 구성을 사용하여 `AssemblyName`이 `LoggingLibrary`인 어셈블리를 빌드합니다. 이 경우 패키지에 있는 `.nuspec` 파일의 결과 줄은 다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="c8f31-252">And you build an assembly whose `AssemblyName` is `LoggingLibrary` with the `Release` configuration in MSBuild, the resulting lines in the `.nuspec` file in the package is as follows:</span></span>

```xml
<files>
    <file src="bin\Release\LoggingLibrary.pdb" target="lib\net40" />
</files>
```

## <a name="dependencies"></a><span data-ttu-id="c8f31-253">종속성</span><span class="sxs-lookup"><span data-stu-id="c8f31-253">Dependencies</span></span>

<span data-ttu-id="c8f31-254">`<metadata>` 내의 `<dependencies>` 요소에는 최상위 패키지가 종속되는 다른 패키지를 식별하는 임의 개수의 `<dependency>` 요소가 포함됩니다.</span><span class="sxs-lookup"><span data-stu-id="c8f31-254">The `<dependencies>` element within `<metadata>` contains any number of `<dependency>` elements that identify other packages upon which the top-level package depends.</span></span> <span data-ttu-id="c8f31-255">각 `<dependency>`에 대한 특성은 다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="c8f31-255">The attributes for each `<dependency>` are as follows:</span></span>

| <span data-ttu-id="c8f31-256">특성</span><span class="sxs-lookup"><span data-stu-id="c8f31-256">Attribute</span></span> | <span data-ttu-id="c8f31-257">설명</span><span class="sxs-lookup"><span data-stu-id="c8f31-257">Description</span></span> |
| --- | --- |
| `id` | <span data-ttu-id="c8f31-258">(필수) 패키지 페이지에서 “EntityFramework” 및 “NUnit” 패키지 nuget.org의 이름인 같은 종속성의 패키지 ID를 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="c8f31-258">(Required) The package ID of the dependency, such as "EntityFramework" and "NUnit", which is the name of the package nuget.org shows on a package page.</span></span> |
| `version` | <span data-ttu-id="c8f31-259">(필수) 종속성으로 허용되는 버전 범위입니다.</span><span class="sxs-lookup"><span data-stu-id="c8f31-259">(Required) The range of versions acceptable as a dependency.</span></span> <span data-ttu-id="c8f31-260">정확한 구문은 [패키지 버전 관리](../reference/package-versioning.md#version-ranges-and-wildcards)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="c8f31-260">See [Package versioning](../reference/package-versioning.md#version-ranges-and-wildcards) for exact syntax.</span></span> |
| <span data-ttu-id="c8f31-261">include</span><span class="sxs-lookup"><span data-stu-id="c8f31-261">include</span></span> | <span data-ttu-id="c8f31-262">최종 패키지에 포함할 종속성을 나타내는 include/exclude 태그(아래 참조)에 대한 쉼표로 구분된 목록입니다.</span><span class="sxs-lookup"><span data-stu-id="c8f31-262">A comma-delimited list of include/exclude tags (see below) indicating of the dependency to include in the final package.</span></span> <span data-ttu-id="c8f31-263">기본값은 `none`입니다.</span><span class="sxs-lookup"><span data-stu-id="c8f31-263">The default value is `none`.</span></span> |
| <span data-ttu-id="c8f31-264">Exclude</span><span class="sxs-lookup"><span data-stu-id="c8f31-264">exclude</span></span> | <span data-ttu-id="c8f31-265">최종 패키지에서 제외할 종속성을 나타내는 include/exclude 태그(아래 참조)에 대한 쉼표로 구분된 목록입니다.</span><span class="sxs-lookup"><span data-stu-id="c8f31-265">A comma-delimited list of include/exclude tags (see below) indicating of the dependency to exclude in the final package.</span></span> <span data-ttu-id="c8f31-266">기본값은 `all`입니다.</span><span class="sxs-lookup"><span data-stu-id="c8f31-266">The  default value is `all`.</span></span> <span data-ttu-id="c8f31-267">`exclude`로 지정된 태그는 `include`로 지정된 태그보다 우선 순위가 높습니다.</span><span class="sxs-lookup"><span data-stu-id="c8f31-267">Tags specified with `exclude` take precedence over those specified with `include`.</span></span> <span data-ttu-id="c8f31-268">예를 들어 `include="runtime, compile" exclude="compile"`은 `include="runtime"`과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="c8f31-268">For example, `include="runtime, compile" exclude="compile"` is the same as `include="runtime"`.</span></span> |

| <span data-ttu-id="c8f31-269">include/exclude 태그</span><span class="sxs-lookup"><span data-stu-id="c8f31-269">Include/Exclude tag</span></span> | <span data-ttu-id="c8f31-270">영향을 받는 대상 폴더</span><span class="sxs-lookup"><span data-stu-id="c8f31-270">Affected folders of the target</span></span> |
| --- | --- |
| <span data-ttu-id="c8f31-271">contentFiles</span><span class="sxs-lookup"><span data-stu-id="c8f31-271">contentFiles</span></span> | <span data-ttu-id="c8f31-272">콘텐츠</span><span class="sxs-lookup"><span data-stu-id="c8f31-272">Content</span></span>  |
| <span data-ttu-id="c8f31-273">런타임(runtime)</span><span class="sxs-lookup"><span data-stu-id="c8f31-273">runtime</span></span> | <span data-ttu-id="c8f31-274">Runtime, Resources 및 FrameworkAssemblies</span><span class="sxs-lookup"><span data-stu-id="c8f31-274">Runtime, Resources, and FrameworkAssemblies</span></span>  |
| <span data-ttu-id="c8f31-275">compile</span><span class="sxs-lookup"><span data-stu-id="c8f31-275">compile</span></span> | <span data-ttu-id="c8f31-276">lib</span><span class="sxs-lookup"><span data-stu-id="c8f31-276">lib</span></span> |
| <span data-ttu-id="c8f31-277">빌드</span><span class="sxs-lookup"><span data-stu-id="c8f31-277">build</span></span> | <span data-ttu-id="c8f31-278">build(MSBuild props 및 targets)</span><span class="sxs-lookup"><span data-stu-id="c8f31-278">build (MSBuild props and targets)</span></span> |
| <span data-ttu-id="c8f31-279">native</span><span class="sxs-lookup"><span data-stu-id="c8f31-279">native</span></span> | <span data-ttu-id="c8f31-280">native</span><span class="sxs-lookup"><span data-stu-id="c8f31-280">native</span></span> |
| <span data-ttu-id="c8f31-281">없음</span><span class="sxs-lookup"><span data-stu-id="c8f31-281">none</span></span> | <span data-ttu-id="c8f31-282">영향을 받는 폴더 없음</span><span class="sxs-lookup"><span data-stu-id="c8f31-282">No folders</span></span> |
| <span data-ttu-id="c8f31-283">모두</span><span class="sxs-lookup"><span data-stu-id="c8f31-283">all</span></span> | <span data-ttu-id="c8f31-284">모든 폴더</span><span class="sxs-lookup"><span data-stu-id="c8f31-284">All folders</span></span> |

<span data-ttu-id="c8f31-285">예를 들어 다음 줄은 `PackageA` 버전 1.1.0 이상 및 `PackageB` 버전 1.x에 대한 종속성을 나타냅니다.</span><span class="sxs-lookup"><span data-stu-id="c8f31-285">For example, the following lines indicate dependencies on `PackageA` version 1.1.0 or higher, and `PackageB` version 1.x.</span></span>

```xml
<dependencies>
    <dependency id="PackageA" version="1.1.0" />
    <dependency id="PackageB" version="[1,2)" />
</dependencies>
```

<span data-ttu-id="c8f31-286">다음 줄은 동일한 패키지에 대한 종속성을 나타내지만, `PackageA`의 `contentFiles` 및 `build` 폴더와 `PackageB`의 `native` 및 `compile` 폴더 이외의 모든 폴더를 포함하도록 지정합니다.</span><span class="sxs-lookup"><span data-stu-id="c8f31-286">The following lines indicate dependencies on the same packages, but specify to include the `contentFiles` and `build` folders of `PackageA` and everything but the `native` and `compile` folders of `PackageB`"</span></span>

```xml
<dependencies>
    <dependency id="PackageA" version="1.1.0" include="contentFiles, build" />
    <dependency id="PackageB" version="[1,2)" exclude="native, compile" />
</dependencies>
```

<span data-ttu-id="c8f31-287">참고: `nuget spec`을 사용하여 프로젝트에서 `.nuspec`을 만드는 경우 해당 프로젝트에 있는 종속성이 결과 `.nuspec` 파일에 자동으로 포함됩니다.</span><span class="sxs-lookup"><span data-stu-id="c8f31-287">Note: When creating a `.nuspec` from a project using `nuget spec`, dependencies that exist in that project are automatically included in the resulting `.nuspec` file.</span></span>

### <a name="dependency-groups"></a><span data-ttu-id="c8f31-288">종속성 그룹</span><span class="sxs-lookup"><span data-stu-id="c8f31-288">Dependency groups</span></span>

<span data-ttu-id="c8f31-289">*버전 2.0 이상*</span><span class="sxs-lookup"><span data-stu-id="c8f31-289">*Version 2.0+*</span></span>

<span data-ttu-id="c8f31-290">단일 단순 목록의 대안으로, `<dependencies>` 내에서 `<group>` 요소를 사용하여 대상 프로젝트의 프레임워크 프로필에 따라 종속성을 지정할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="c8f31-290">As an alternative to a single flat list, dependencies can be specified according to the framework profile of the target project using `<group>` elements within `<dependencies>`.</span></span>

<span data-ttu-id="c8f31-291">각 그룹에는 `targetFramework`라는 특성이 있으며 0개 이상의 `<dependency>` 요소가 포함됩니다.</span><span class="sxs-lookup"><span data-stu-id="c8f31-291">Each group has an attribute named `targetFramework` and contains zero or more `<dependency>` elements.</span></span> <span data-ttu-id="c8f31-292">이러한 종속성은 대상 프레임워크가 프로젝트의 프레임워크 프로필과 호환될 때 함께 설치됩니다.</span><span class="sxs-lookup"><span data-stu-id="c8f31-292">Those dependencies are installed together when  the target framework is compatible with the project's framework profile.</span></span>

<span data-ttu-id="c8f31-293">`targetFramework` 특성이 없는 `<group>` 요소는 종속성의 기본 또는 대체(fallback) 목록으로 사용됩니다.</span><span class="sxs-lookup"><span data-stu-id="c8f31-293">The `<group>` element without a `targetFramework` attribute is used as the default or fallback list of dependencies.</span></span> <span data-ttu-id="c8f31-294">정확한 프레임워크 식별자는 [대상 프레임워크](../schema/target-frameworks.md)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="c8f31-294">See [Target frameworks](../schema/target-frameworks.md) for the exact framework identifiers.</span></span>

> [!Important]
> <span data-ttu-id="c8f31-295">그룹 형식은 단순 목록과 섞일 수 없습니다.</span><span class="sxs-lookup"><span data-stu-id="c8f31-295">The group format cannot be intermixed with a flat list.</span></span>

<span data-ttu-id="c8f31-296">다음 예제에서는 `<group>` 요소의 여러 변형을 보여줍니다.</span><span class="sxs-lookup"><span data-stu-id="c8f31-296">The following example shows different variations of the `<group>` element:</span></span>

```xml
<dependencies>
    <group>
        <dependency id="RouteMagic" version="1.1.0" />
    </group>

    <group targetFramework="net40">
        <dependency id="jQuery" />
        <dependency id="WebActivator" />
    </group>

    <group targetFramework="sl30">
    </group>
</dependencies>
```

<a name="specifying-explicit-assembly-references"></a>

## <a name="explicit-assembly-references"></a><span data-ttu-id="c8f31-297">명시적 어셈블리 참조</span><span class="sxs-lookup"><span data-stu-id="c8f31-297">Explicit assembly references</span></span>

<span data-ttu-id="c8f31-298">`<references>` 요소는 패키지를 사용할 때 대상 프로젝트에서 참조해야 하는 어셈블리를 명시적으로 지정합니다.</span><span class="sxs-lookup"><span data-stu-id="c8f31-298">The `<references>` element explicitly specifies the assemblies that the target project should reference when using the package.</span></span> <span data-ttu-id="c8f31-299">이 요소가 있으면 NuGet은 나열된 어셈블리에 대한 참조만 추가합니다. 패키지의 `lib` 폴더에 있는 다른 어셈블리에 대한 참조는 추가하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="c8f31-299">When this element is present, NuGet add references to only the listed assemblies; it does not add references for any other assemblies in the package's `lib` folder.</span></span>

<span data-ttu-id="c8f31-300">예를 들어 다음 `<references>` 요소는 패키지에 추가 어셈블리가 있는 경우에도 `xunit.dll` 및 `xunit.extensions.dll`에 대한 참조만 추가하도록 NuGet에 지시합니다.</span><span class="sxs-lookup"><span data-stu-id="c8f31-300">For example, the following `<references>` element instructs NuGet to add references to only `xunit.dll` and `xunit.extensions.dll` even if there are additional assemblies in the package:</span></span>

```xml
<references>
    <reference file="xunit.dll" />
    <reference file="xunit.extensions.dll" />
</references>
```

<span data-ttu-id="c8f31-301">명시적 참조는 일반적으로 디자인 타임 전용 어셈블리에만 사용됩니다.</span><span class="sxs-lookup"><span data-stu-id="c8f31-301">Explicit references are typically used for design-time only assemblies.</span></span> <span data-ttu-id="c8f31-302">예를 들어 [코드 계약](/dotnet/framework/debug-trace-profile/code-contracts)을 사용하는 경우 계약 어셈블리는 확장하는 런타임 어셈블리 옆에 있어야 Visual Studio에서 찾을 수 있습니다. 그러나 계약 어셈블리는 프로젝트에서 참조하거나 프로젝트의 `bin` 폴더에 복사할 필요가 없습니다.</span><span class="sxs-lookup"><span data-stu-id="c8f31-302">When using [Code Contracts](/dotnet/framework/debug-trace-profile/code-contracts), for example, contract assemblies need to be next to the runtime assemblies that they augment so that Visual Studio can find them, but the contract assemblies need not be referenced by the project or copied into the project's `bin` folder.</span></span>

<span data-ttu-id="c8f31-303">마찬가지로 명시적 참조는 런타임 어셈블리 옆에 있는 도구 어셈블리가 필요하지만 프로젝트 참조로 포함될 필요가 없는 XUnit과 같은 단위 테스트 프레임워크에 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="c8f31-303">Similarly, explicit references can be used for unit test frameworks, such as XUnit, which needs its tools assemblies located next to the runtime assemblies, but does not need them included as project references.</span></span>

### <a name="reference-groups"></a><span data-ttu-id="c8f31-304">참조 그룹</span><span class="sxs-lookup"><span data-stu-id="c8f31-304">Reference groups</span></span>

<span data-ttu-id="c8f31-305">단일 단순 목록의 대안으로, `<references>` 내에서 `<group>` 요소를 사용하여 대상 프로젝트의 프레임워크 프로필에 따라 참조를 지정할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="c8f31-305">As an alternative to a single flat list, references can be specified according to the framework profile of the target project using `<group>` elements within `<references>`.</span></span>

<span data-ttu-id="c8f31-306">각 그룹에는 `targetFramework`라는 특성이 있으며 0개 이상의 `<reference>` 요소가 포함됩니다.</span><span class="sxs-lookup"><span data-stu-id="c8f31-306">Each group has an attribute named `targetFramework` and contains zero or more `<reference>` elements.</span></span> <span data-ttu-id="c8f31-307">이러한 참조는 대상 프레임워크가 프로젝트의 프레임워크 프로필과 호환될 때 프로젝트에 추가 됩니다.</span><span class="sxs-lookup"><span data-stu-id="c8f31-307">Those references are added to a project when the target framework is compatible with the project's framework profile.</span></span>

<span data-ttu-id="c8f31-308">`targetFramework` 특성이 없는 `<group>` 요소는 참조의 기본 또는 대체(fallback) 목록으로 사용됩니다.</span><span class="sxs-lookup"><span data-stu-id="c8f31-308">The `<group>` element without a `targetFramework` attribute is used as the default or fallback list of references.</span></span> <span data-ttu-id="c8f31-309">정확한 프레임워크 식별자는 [대상 프레임워크](../schema/target-frameworks.md)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="c8f31-309">See [Target frameworks](../schema/target-frameworks.md) for the exact framework identifiers.</span></span>

> [!Important]
> <span data-ttu-id="c8f31-310">그룹 형식은 단순 목록과 섞일 수 없습니다.</span><span class="sxs-lookup"><span data-stu-id="c8f31-310">The group format cannot be intermixed with a flat list.</span></span>

<span data-ttu-id="c8f31-311">다음 예제에서는 `<group>` 요소의 여러 변형을 보여줍니다.</span><span class="sxs-lookup"><span data-stu-id="c8f31-311">The following example shows different variations of the `<group>` element:</span></span>

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

## <a name="framework-assembly-references"></a><span data-ttu-id="c8f31-312">프레임워크 어셈블리 참조</span><span class="sxs-lookup"><span data-stu-id="c8f31-312">Framework assembly references</span></span>

<span data-ttu-id="c8f31-313">프레임워크 어셈블리는 .NET Framework의 일부이며, 지정된 컴퓨터에 대한 GAC(전역 어셈블리 캐시)에 이미 있어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="c8f31-313">Framework assemblies are those that are part of the .NET framework and should already be in the global assembly cache (GAC) for any given machine.</span></span> <span data-ttu-id="c8f31-314">패키지는 `<frameworkAssemblies>` 요소 내에서 이러한 어셈블리를 식별하여 프로젝트에 해당 참조가 아직 없는 경우 필요한 참조가 프로젝트에 추가되도록 할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="c8f31-314">By identifying those assemblies within the `<frameworkAssemblies>` element, a package can ensure that required references are added to a project in the event that the project doesn't have such references already.</span></span> <span data-ttu-id="c8f31-315">물론 이러한 어셈블리는 패키지에 직접 포함되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="c8f31-315">Such assemblies, of course, are not included in a package directly.</span></span>

<span data-ttu-id="c8f31-316">`<frameworkAssemblies>` 요소는 0개 이상의 `<frameworkAssembly>` 요소를 포함하며, 각 요소마다 다음 특성을 지정합니다.</span><span class="sxs-lookup"><span data-stu-id="c8f31-316">The `<frameworkAssemblies>` element contains zero or more `<frameworkAssembly>` elements, each of which specifies the following attributes:</span></span>

| <span data-ttu-id="c8f31-317">특성</span><span class="sxs-lookup"><span data-stu-id="c8f31-317">Attribute</span></span> | <span data-ttu-id="c8f31-318">설명</span><span class="sxs-lookup"><span data-stu-id="c8f31-318">Description</span></span> |
| --- | --- |
| <span data-ttu-id="c8f31-319">**assemblyName**</span><span class="sxs-lookup"><span data-stu-id="c8f31-319">**assemblyName**</span></span> | <span data-ttu-id="c8f31-320">(필수) 정규화된 어셈블리 이름입니다.</span><span class="sxs-lookup"><span data-stu-id="c8f31-320">(Required) The fully qualified assembly name.</span></span> |
| <span data-ttu-id="c8f31-321">**targetFramework**</span><span class="sxs-lookup"><span data-stu-id="c8f31-321">**targetFramework**</span></span> | <span data-ttu-id="c8f31-322">(선택) 이 참조가 적용되는 대상 프레임워크를 지정합니다.</span><span class="sxs-lookup"><span data-stu-id="c8f31-322">(Optional) Specifies the target framework to which this reference applies.</span></span> <span data-ttu-id="c8f31-323">생략하면 참조가 모든 프레임워크에 적용됨을 나타냅니다.</span><span class="sxs-lookup"><span data-stu-id="c8f31-323">If omitted, indicates that the reference applies to all frameworks.</span></span> <span data-ttu-id="c8f31-324">정확한 프레임워크 식별자는 [대상 프레임워크](../schema/target-frameworks.md)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="c8f31-324">See [Target frameworks](../schema/target-frameworks.md) for the exact framework identifiers.</span></span> |

<span data-ttu-id="c8f31-325">다음 예제에서는 모든 대상 프레임워크의 `System.Net`에 대한 참조와 .NET Framework 4.0 전용의 `System.ServiceModel`에 대한 참조를 보여줍니다.</span><span class="sxs-lookup"><span data-stu-id="c8f31-325">The following example shows a reference to `System.Net` for all target frameworks, and a reference to `System.ServiceModel` for .NET Framework 4.0 only:</span></span>

```xml
<frameworkAssemblies>
    <frameworkAssembly assemblyName="System.Net"  />

    <frameworkAssembly assemblyName="System.ServiceModel" targetFramework="net40" />
</frameworkAssemblies>
```

<a name="specifying-files-to-include-in-the-package"></a>

## <a name="including-assembly-files"></a><span data-ttu-id="c8f31-326">어셈블리 파일 포함</span><span class="sxs-lookup"><span data-stu-id="c8f31-326">Including assembly files</span></span>

<span data-ttu-id="c8f31-327">[패키지 만들기](../create-packages/creating-a-package.md)에서 설명한 규칙을 따르면 파일 목록을 `.nuspec` 파일에 명시적으로 지정할 필요가 없습니다.</span><span class="sxs-lookup"><span data-stu-id="c8f31-327">If you follow the conventions described in [Creating a Package](../create-packages/creating-a-package.md), you do not have to explicitly specify a list of files in the `.nuspec` file.</span></span> <span data-ttu-id="c8f31-328">`nuget pack` 명령은 필요한 파일을 자동으로 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="c8f31-328">The `nuget pack` command automatically picks up the necessary files.</span></span>

> [!Important]
> <span data-ttu-id="c8f31-329">패키지가 프로젝트에 설치되면 어셈블리 참조가 지역화된 위성 어셈블리로 간주되므로 NuGet은 `.resources.dll`이라는 DLL을 *제외한* 패키지의 DLL에 해당 어셈블리 참조를 자동으로 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="c8f31-329">When a package is installed into a project, NuGet automatically adds assembly references to the package's DLLs, *excluding* those that are named `.resources.dll` because they are assumed to be localized satellite assemblies.</span></span> <span data-ttu-id="c8f31-330">이러한 이유로 다른 경우에 필수 패키지 코드가 포함되는 파일에는 `.resources.dll`을 사용하지 마세요.</span><span class="sxs-lookup"><span data-stu-id="c8f31-330">For this reason, avoid using `.resources.dll` for files that otherwise contain essential package code.</span></span>

<span data-ttu-id="c8f31-331">이러한 자동 동작을 무시하고 패키지에 포함되는 파일을 명시적으로 제어하려면 `<files>` 요소를 `<package>`의 자식(및 `<metadata>`의 형제)으로 배치하고 각 파일을 별도의 `<file>` 요소로 식별합니다.</span><span class="sxs-lookup"><span data-stu-id="c8f31-331">To bypass this automatic behavior and explicitly control which files are included in a package, place a `<files>` element as a child of `<package>` (and a sibling of `<metadata>`), identifying each file with a separate `<file>` element.</span></span> <span data-ttu-id="c8f31-332">예:</span><span class="sxs-lookup"><span data-stu-id="c8f31-332">For example:</span></span>

```xml
<files>
    <file src="bin\Debug\*.dll" target="lib" />
    <file src="bin\Debug\*.pdb" target="lib" />
    <file src="tools\**\*.*" exclude="**\*.log" />
</files>
```

<span data-ttu-id="c8f31-333">NuGet 2.x 및 이전 버전과 `packages.config`를 사용하는 프로젝트의 경우 `<files>` 요소는 패키지를 설치할 때 변경할 수 없는 콘텐츠 파일을 포함하는 데에도 사용됩니다.</span><span class="sxs-lookup"><span data-stu-id="c8f31-333">With NuGet 2.x and earlier, and projects using `packages.config`, the `<files>` element is also used to include immutable content files when a package is installed.</span></span> <span data-ttu-id="c8f31-334">NuGet 3.3 이상 및 프로젝트 PackageReference에서는 `<contentFiles>` 요소가 대신 사용됩니다.</span><span class="sxs-lookup"><span data-stu-id="c8f31-334">With NuGet 3.3+ and projects PackageReference, the `<contentFiles>` element is used instead.</span></span> <span data-ttu-id="c8f31-335">자세한 내용은 아래의 [콘텐츠 파일 포함](#including-content-files)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="c8f31-335">See [Including content files](#including-content-files) below for details.</span></span>

### <a name="file-element-attributes"></a><span data-ttu-id="c8f31-336">파일 요소 특성</span><span class="sxs-lookup"><span data-stu-id="c8f31-336">File element attributes</span></span>

<span data-ttu-id="c8f31-337">각 `<file>` 요소는 다음과 같은 특성을 지정합니다.</span><span class="sxs-lookup"><span data-stu-id="c8f31-337">Each `<file>` element specifies the following attributes:</span></span>

| <span data-ttu-id="c8f31-338">특성</span><span class="sxs-lookup"><span data-stu-id="c8f31-338">Attribute</span></span> | <span data-ttu-id="c8f31-339">설명</span><span class="sxs-lookup"><span data-stu-id="c8f31-339">Description</span></span> |
| --- | --- |
| <span data-ttu-id="c8f31-340">**src**</span><span class="sxs-lookup"><span data-stu-id="c8f31-340">**src**</span></span> | <span data-ttu-id="c8f31-341">`exclude` 특성으로 지정된 제외에 따라 포함할 파일의 위치입니다.</span><span class="sxs-lookup"><span data-stu-id="c8f31-341">The location of the file or files to include, subject to exclusions specified by the `exclude` attribute.</span></span> <span data-ttu-id="c8f31-342">절대 경로가 지정되지 않으면 경로는 `.nuspec` 파일에 대한 상대 경로입니다.</span><span class="sxs-lookup"><span data-stu-id="c8f31-342">The path is relative to the `.nuspec` file unless an absolute path is specified.</span></span> <span data-ttu-id="c8f31-343">`*` 와일드카드 문자가 허용되고, `**` 이중 와일드카드는 재귀적 폴더 검색을 의미합니다.</span><span class="sxs-lookup"><span data-stu-id="c8f31-343">The wildcard character `*` is allowed, and the double wildcard `**` implies a recursive folder search.</span></span> |
| <span data-ttu-id="c8f31-344">**target**</span><span class="sxs-lookup"><span data-stu-id="c8f31-344">**target**</span></span> | <span data-ttu-id="c8f31-345">원본 파일이 있는 패키지 내의 폴더에 대한 상대 경로이며, `lib`, `content`, `build` 또는 `tools`로 시작해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="c8f31-345">The relative path to the folder within the package where the source files are placed, which must begin with `lib`, `content`, `build`, or `tools`.</span></span> <span data-ttu-id="c8f31-346">[규칙 기반 작업 디렉터리에서 .nuspec 만들기](../Create-Packages/Creating-a-Package.md#from-a-convention-based-working-directory)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="c8f31-346">See [Creating a .nuspec from a convention-based working directory](../Create-Packages/Creating-a-Package.md#from-a-convention-based-working-directory).</span></span> |
| <span data-ttu-id="c8f31-347">**exclude**</span><span class="sxs-lookup"><span data-stu-id="c8f31-347">**exclude**</span></span> | <span data-ttu-id="c8f31-348">`src` 위치에서 제외할 파일 또는 파일 패턴에 대한 세미콜론으로 구분된 목록입니다.</span><span class="sxs-lookup"><span data-stu-id="c8f31-348">A semicolon-delimited list of files or file patterns to exclude from the `src` location.</span></span> <span data-ttu-id="c8f31-349">`*` 와일드카드 문자가 허용되고, `**` 이중 와일드카드는 재귀적 폴더 검색을 의미합니다.</span><span class="sxs-lookup"><span data-stu-id="c8f31-349">The wildcard character `*` is allowed, and the double wildcard `**` implies a recursive folder search.</span></span> |

### <a name="examples"></a><span data-ttu-id="c8f31-350">예제</span><span class="sxs-lookup"><span data-stu-id="c8f31-350">Examples</span></span>

<span data-ttu-id="c8f31-351">**단일 어셈블리**</span><span class="sxs-lookup"><span data-stu-id="c8f31-351">**Single assembly**</span></span>

    Source file:
        library.dll

    .nuspec entry:
        <file src="library.dll" target="lib" />

    Packaged result:
        lib\library.dll

<span data-ttu-id="c8f31-352">**특정 대상 프레임워크에 대한 단일 어셈블리**</span><span class="sxs-lookup"><span data-stu-id="c8f31-352">**Single assembly specific to a target framework**</span></span>

    Source file:
        library.dll

    .nuspec entry:
        <file src="assemblies\net40\library.dll" target="lib\net40" />

    Packaged result:
        lib\net40\library.dll

<span data-ttu-id="c8f31-353">**와일드카드를 사용하는 DLL 집합**</span><span class="sxs-lookup"><span data-stu-id="c8f31-353">**Set of DLLs using a wildcard**</span></span>

    Source files:
        bin\release\libraryA.dll
        bin\release\libraryB.dll

    .nuspec entry:
        <file src="bin\release\*.dll" target="lib" />

    Packaged result:
        lib\libraryA.dll
        lib\libraryB.dll

<span data-ttu-id="c8f31-354">**여러 프레임워크에 대한 DLL**</span><span class="sxs-lookup"><span data-stu-id="c8f31-354">**DLLs for different frameworks**</span></span>

    Source files:
        lib\net40\library.dll
        lib\net20\library.dll

    .nuspec entry (using ** recursive search):
        <file src="lib\**" target="lib" />

    Packaged result:
        lib\net40\library.dll
        lib\net20\library.dll

<span data-ttu-id="c8f31-355">**파일 제외**</span><span class="sxs-lookup"><span data-stu-id="c8f31-355">**Excluding files**</span></span>

    Source files:
        \tools\*.bak
        \tools\*.log
        \tools\build\*.log

    .nuspec entries:
        <file src="tools\*.*" target="tools" exclude="tools\*.bak" />
        <file src="tools\**\*.*" target="tools" exclude="**\*.log" />

    Package result:
        (no files)

## <a name="including-content-files"></a><span data-ttu-id="c8f31-356">콘텐츠 파일 포함</span><span class="sxs-lookup"><span data-stu-id="c8f31-356">Including content files</span></span>

<span data-ttu-id="c8f31-357">콘텐츠 파일은 패키지에서 프로젝트에 포함해야 하는 변경할 수 없는 파일입니다.</span><span class="sxs-lookup"><span data-stu-id="c8f31-357">Content files are immutable files that a package needs to include in a project.</span></span> <span data-ttu-id="c8f31-358">변경할 수 없으므로 사용하는 프로젝트에서 수정되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="c8f31-358">Being immutable, they are not intended to be modified by the consuming project.</span></span> <span data-ttu-id="c8f31-359">콘텐츠 파일의 예는 다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="c8f31-359">Example content files include:</span></span>

- <span data-ttu-id="c8f31-360">리소스로 포함된 이미지</span><span class="sxs-lookup"><span data-stu-id="c8f31-360">Images that are embedded as resources</span></span>
- <span data-ttu-id="c8f31-361">이미 컴파일된 원본 파일</span><span class="sxs-lookup"><span data-stu-id="c8f31-361">Source files that are already compiled</span></span>
- <span data-ttu-id="c8f31-362">프로젝트의 빌드 출력에 포함되어야 하는 스크립트</span><span class="sxs-lookup"><span data-stu-id="c8f31-362">Scripts that need to be included with the build output of the project</span></span>
- <span data-ttu-id="c8f31-363">프로젝트에 포함되어야 하지만 프로젝트별 변경이 필요하지 않은 패키지에 대한 구성 파일</span><span class="sxs-lookup"><span data-stu-id="c8f31-363">Configuration files for the package that need to be included in the project but don't need any project-specific changes</span></span>

<span data-ttu-id="c8f31-364">콘텐츠 파일은 `<files>` 요소를 사용하고 `target` 특성에서 `content` 폴더를 지정하여 패키지에 포함됩니다.</span><span class="sxs-lookup"><span data-stu-id="c8f31-364">Content files are included in a package using the `<files>` element, specifying the `content` folder in the `target` attribute.</span></span> <span data-ttu-id="c8f31-365">그러나 `<contentFiles>` 요소를 대신 사용하는 PackageReference를 사용하여 프로젝트에 패키지를 설치하는 경우 이러한 파일은 무시됩니다.</span><span class="sxs-lookup"><span data-stu-id="c8f31-365">However, such files are ignored when the package is installed in a project using PackageReference, which instead uses the `<contentFiles>` element.</span></span>

<span data-ttu-id="c8f31-366">사용하는 프로젝트와의 호환성을 최대화하기 위해 패키지는 두 요소 모두에 콘텐츠 파일을 이상적으로 지정합니다.</span><span class="sxs-lookup"><span data-stu-id="c8f31-366">For maximum compatibility with consuming projects, a package ideally specifies the content files in both elements.</span></span>

### <a name="using-the-files-element-for-content-files"></a><span data-ttu-id="c8f31-367">콘텐츠 파일에 대한 files 요소 사용</span><span class="sxs-lookup"><span data-stu-id="c8f31-367">Using the files element for content files</span></span>

<span data-ttu-id="c8f31-368">콘텐츠 파일의 경우 단순히 어셈블리 파일과 동일한 형식을 사용하고 다음 예제와 같이 `content`를 `target` 특성의 기본 폴더로 지정합니다.</span><span class="sxs-lookup"><span data-stu-id="c8f31-368">For content files, simply use the same format as for assembly files, but specify `content` as the base folder in the `target` attribute as shown in the following examples.</span></span>

<span data-ttu-id="c8f31-369">**기본 콘텐츠 파일**</span><span class="sxs-lookup"><span data-stu-id="c8f31-369">**Basic content files**</span></span>

    Source files:
        css\mobile\style1.css
        css\mobile\style2.css

    .nuspec entry:
        <file src="css\mobile\*.css" target="content\css\mobile" />

    Packaged result:
        content\css\mobile\style1.css
        content\css\mobile\style2.css

<span data-ttu-id="c8f31-370">**디렉터리 구조가 포함된 콘텐츠 파일**</span><span class="sxs-lookup"><span data-stu-id="c8f31-370">**Content files with directory structure**</span></span>

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

<span data-ttu-id="c8f31-371">**특정 대상 프레임워크에 대한 콘텐츠 파일**</span><span class="sxs-lookup"><span data-stu-id="c8f31-371">**Content file specific to a target framework**</span></span>

    Source file:
        css\cool\style.css

    .nuspec entry
        <file src="css\cool\style.css" target="Content" />

    Packaged result:
        content\style.css

<span data-ttu-id="c8f31-372">**이름에 점이 있는 폴더에 복사되는 콘텐츠 파일**</span><span class="sxs-lookup"><span data-stu-id="c8f31-372">**Content file copied to a folder with dot in name**</span></span>

<span data-ttu-id="c8f31-373">이 경우 NuGet은 `target`과 `src`의 확장명이 일치하지 않는지 확인하여 `target`의 이름 중 해당 부분을 폴더로 처리합니다.</span><span class="sxs-lookup"><span data-stu-id="c8f31-373">In this case, NuGet sees that the extension in `target` does not match the extension in `src` and thus treats that part of the name in `target` as a folder:</span></span>

    Source file:
        images\picture.png

    .nuspec entry:
        <file src="images\picture.png" target="Content\images\package.icons" />

    Packaged result:
        content\images\package.icons\picture.png

<span data-ttu-id="c8f31-374">**확장명이 없는 콘텐츠 파일**</span><span class="sxs-lookup"><span data-stu-id="c8f31-374">**Content files without extensions**</span></span>

<span data-ttu-id="c8f31-375">확장명이 없는 파일을 포함하려면 `*` 또는 `**` 와일드카드를 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="c8f31-375">To include files without an extension, use the `*` or `**` wildcards:</span></span>

    Source file:
        flags\installed

    .nuspec entry:
        <file src="flags\**" target="flags" />

    Packaged result:
        flags\installed

<span data-ttu-id="c8f31-376">**전체 경로와 전체 대상이 포함된 콘텐츠 파일**</span><span class="sxs-lookup"><span data-stu-id="c8f31-376">**Content files with deep path and deep target**</span></span>

<span data-ttu-id="c8f31-377">이 경우 원본과 대상의 파일 확장명이 일치하므로 NuGet은 대상이 폴더가 아니라 파일 이름이라고 가정합니다.</span><span class="sxs-lookup"><span data-stu-id="c8f31-377">In this case, because the file extensions of the source and target match, NuGet assumes that the target is a file name and not a folder:</span></span>

    Source file:
        css\cool\style.css

    .nuspec entry:
        <file src="css\cool\style.css" target="Content\css\cool" />
        or:
        <file src="css\cool\style.css" target="Content\css\cool\style.css" />

    Packaged result:
        content\css\cool\style.css

<span data-ttu-id="c8f31-378">**패키지의 콘텐츠 파일 이름 바꾸기**</span><span class="sxs-lookup"><span data-stu-id="c8f31-378">**Renaming a content file in the package**</span></span>

    Source file:
        ie\css\style.css

    .nuspec entry:
        <file src="ie\css\style.css" target="Content\css\ie.css" />

    Packaged result:
        content\css\ie.css

<span data-ttu-id="c8f31-379">**파일 제외**</span><span class="sxs-lookup"><span data-stu-id="c8f31-379">**Excluding files**</span></span>

    Source file:
        docs\*.txt (multiple files)

    .nuspec entry:
        <file src="docs\*.txt" target="content\docs" exclude="docs\admin.txt" />
        or
        <file src="*.txt" target="content\docs" exclude="admin.txt;log.txt" />

    Packaged result:
        All .txt files from docs except admin.txt (first example)
        All .txt files from docs except admin.txt and log.txt (second example)

<a name="using-contentfiles-element-for-content-files"></a>

### <a name="using-the-contentfiles-element-for-content-files"></a><span data-ttu-id="c8f31-380">콘텐츠 파일에 대한 contentFiles 요소 사용</span><span class="sxs-lookup"><span data-stu-id="c8f31-380">Using the contentFiles element for content files</span></span>

<span data-ttu-id="c8f31-381">*NuGet 4.0 이상(PackageReference 사용)*</span><span class="sxs-lookup"><span data-stu-id="c8f31-381">*NuGet 4.0+ with PackageReference*</span></span>

<span data-ttu-id="c8f31-382">기본적으로 패키지는 `contentFiles` 폴더(아래 참조) 및 기본 특성을 사용하여 해당 폴더의 모든 파일이 포함되는 `nuget pack`에 콘텐츠 파일을 배치합니다.</span><span class="sxs-lookup"><span data-stu-id="c8f31-382">By default, a package places content in a `contentFiles` folder (see below) and `nuget pack` included all files in that folder using default attributes.</span></span> <span data-ttu-id="c8f31-383">이 경우 `.nuspec`에 `contentFiles` 노드를 포함할 필요가 없습니다.</span><span class="sxs-lookup"><span data-stu-id="c8f31-383">In this case it's not necessary to include a `contentFiles` node in the `.nuspec` at all.</span></span>

<span data-ttu-id="c8f31-384">포함되는 파일을 제어하려면 `<contentFiles>` 요소에서 포함할 파일을 정확히 식별하는 `<files>` 요소 컬렉션을 지정합니다.</span><span class="sxs-lookup"><span data-stu-id="c8f31-384">To control which files are included, the `<contentFiles>` element specifies is a collection of `<files>` elements that identify the exact files include.</span></span>

<span data-ttu-id="c8f31-385">이러한 파일은 프로젝트 시스템 내에서 사용되는 방법을 설명하는 일단의 특성으로 지정됩니다.</span><span class="sxs-lookup"><span data-stu-id="c8f31-385">These files are specified with a set of attributes that describe how they should be used within the project system:</span></span>

| <span data-ttu-id="c8f31-386">특성</span><span class="sxs-lookup"><span data-stu-id="c8f31-386">Attribute</span></span> | <span data-ttu-id="c8f31-387">설명</span><span class="sxs-lookup"><span data-stu-id="c8f31-387">Description</span></span> |
| --- | --- |
| <span data-ttu-id="c8f31-388">**include**</span><span class="sxs-lookup"><span data-stu-id="c8f31-388">**include**</span></span> | <span data-ttu-id="c8f31-389">(필수) `exclude` 특성으로 지정된 제외에 따라 포함할 파일의 위치입니다.</span><span class="sxs-lookup"><span data-stu-id="c8f31-389">(Required) The location of the file or files to include, subject to exclusions specified by the `exclude` attribute.</span></span> <span data-ttu-id="c8f31-390">절대 경로가 지정되지 않으면 경로는 `.nuspec` 파일에 대한 상대 경로입니다.</span><span class="sxs-lookup"><span data-stu-id="c8f31-390">The path is relative to the `.nuspec` file unless an absolute path is specified.</span></span> <span data-ttu-id="c8f31-391">`*` 와일드카드 문자가 허용되고, `**` 이중 와일드카드는 재귀적 폴더 검색을 의미합니다.</span><span class="sxs-lookup"><span data-stu-id="c8f31-391">The wildcard character `*` is allowed, and the double wildcard `**` implies a recursive folder search.</span></span> |
| <span data-ttu-id="c8f31-392">**exclude**</span><span class="sxs-lookup"><span data-stu-id="c8f31-392">**exclude**</span></span> | <span data-ttu-id="c8f31-393">`src` 위치에서 제외할 파일 또는 파일 패턴에 대한 세미콜론으로 구분된 목록입니다.</span><span class="sxs-lookup"><span data-stu-id="c8f31-393">A semicolon-delimited list of files or file patterns to exclude from the `src` location.</span></span> <span data-ttu-id="c8f31-394">`*` 와일드카드 문자가 허용되고, `**` 이중 와일드카드는 재귀적 폴더 검색을 의미합니다.</span><span class="sxs-lookup"><span data-stu-id="c8f31-394">The wildcard character `*` is allowed, and the double wildcard `**` implies a recursive folder search.</span></span> |
| <span data-ttu-id="c8f31-395">**buildAction**</span><span class="sxs-lookup"><span data-stu-id="c8f31-395">**buildAction**</span></span> | <span data-ttu-id="c8f31-396">`Content`, `None`, `Embedded Resource`, `Compile` 등과 같이 MSBuild의 콘텐츠 항목에 할당할 빌드 작업입니다. 기본값은 `Compile`입니다.</span><span class="sxs-lookup"><span data-stu-id="c8f31-396">The build action to assign to the content item for MSBuild, such as `Content`, `None`, `Embedded Resource`, `Compile`, etc. The default is `Compile`.</span></span> |
| <span data-ttu-id="c8f31-397">**copyToOutput**</span><span class="sxs-lookup"><span data-stu-id="c8f31-397">**copyToOutput**</span></span> | <span data-ttu-id="c8f31-398">콘텐츠 항목을 빌드 출력 폴더에 복사할지 여부를 나타내는 부울 값입니다.</span><span class="sxs-lookup"><span data-stu-id="c8f31-398">A Boolean indicating whether to copy content items to the build output folder.</span></span> <span data-ttu-id="c8f31-399">기본값은 false입니다.</span><span class="sxs-lookup"><span data-stu-id="c8f31-399">The default is false.</span></span> |
| <span data-ttu-id="c8f31-400">**flatten**</span><span class="sxs-lookup"><span data-stu-id="c8f31-400">**flatten**</span></span> | <span data-ttu-id="c8f31-401">빌드 출력의 단일 폴더에 콘텐츠 항목을 복사할지(true), 아니면 패키지의 폴더 구조를 유지할지(false) 여부를 나타내는 부울 값입니다.</span><span class="sxs-lookup"><span data-stu-id="c8f31-401">A Boolean indicating whether to copy content items to a single folder in the build output (true), or to preserve the folder structure in the package (false).</span></span> <span data-ttu-id="c8f31-402">이 플래그는 copyToOutput 플래그가 true로 설정된 경우에만 작동합니다.</span><span class="sxs-lookup"><span data-stu-id="c8f31-402">This flag only works when copyToOutput flag is set to true.</span></span> <span data-ttu-id="c8f31-403">기본값은 false입니다.</span><span class="sxs-lookup"><span data-stu-id="c8f31-403">The default is false.</span></span> |

<span data-ttu-id="c8f31-404">패키지를 설치할 때 NuGet에서 `<contentFiles>`의 자식 요소를 위쪽에서 아래쪽으로 적용합니다.</span><span class="sxs-lookup"><span data-stu-id="c8f31-404">When installing a package, NuGet applies the child elements of `<contentFiles>` from top to bottom.</span></span> <span data-ttu-id="c8f31-405">여러 항목이 동일한 파일과 일치하면 모든 항목이 적용됩니다.</span><span class="sxs-lookup"><span data-stu-id="c8f31-405">If multiple entries match the same file then all entries are applied.</span></span> <span data-ttu-id="c8f31-406">동일한 특성에 대한 충돌이 있는 경우 최상위 항목이 하위 항목을 재정의합니다.</span><span class="sxs-lookup"><span data-stu-id="c8f31-406">The top-most entry overrides the lower entries if there is a conflict for the same attribute.</span></span>

#### <a name="package-folder-structure"></a><span data-ttu-id="c8f31-407">패키지 폴더 구조</span><span class="sxs-lookup"><span data-stu-id="c8f31-407">Package folder structure</span></span>

<span data-ttu-id="c8f31-408">패키지 프로젝트는 다음 패턴을 사용하여 콘텐츠를 구성해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="c8f31-408">The package project should structure content using the following pattern:</span></span>

    /contentFiles/{codeLanguage}/{TxM}/{any?}

- <span data-ttu-id="c8f31-409">`codeLanguages`는 `cs`, `vb`, `fs`, `any` 또는 지정된 `$(ProjectLanguage)`에 해당하는 소문자일 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="c8f31-409">`codeLanguages` may be `cs`, `vb`, `fs`, `any`, or the lowercase equivalent of a given `$(ProjectLanguage)`</span></span>
- <span data-ttu-id="c8f31-410">`TxM`은 NuGet에서 지원하는 모든 법적 대상 프레임워크 모니커입니다([대상 프레임워크](../schema/target-frameworks.md) 참조).</span><span class="sxs-lookup"><span data-stu-id="c8f31-410">`TxM` is any legal target framework moniker that NuGet supports (see [Target frameworks](../schema/target-frameworks.md)).</span></span>
- <span data-ttu-id="c8f31-411">모든 폴더 구조는 이 구문의 끝에 추가될 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="c8f31-411">Any folder structure may be appended to the end of this syntax.</span></span>

<span data-ttu-id="c8f31-412">예:</span><span class="sxs-lookup"><span data-stu-id="c8f31-412">For example:</span></span>

    Language- and framework-agnostic:
        /contentFiles/any/any/config.xml

    net45 content for all languages
        /contentFiles/any/net45/config.xml

    C#-specific content for net45 and up
        /contentFiles/cs/net45/sample.cs

<span data-ttu-id="c8f31-413">빈 폴더는 `.`을 사용하여 언어 및 TxM의 특정 조합에 대한 콘텐츠 제공을 거부할 수 있습니다. 예를 들어 다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="c8f31-413">Empty folders can use `.` to opt out of providing content for certain combinations of language and TxM, for example:</span></span>

    /contentFiles/vb/any/code.vb
    /contentFiles/cs/any/.

#### <a name="example-contentfiles-section"></a><span data-ttu-id="c8f31-414">contentFiles 섹션 예제</span><span class="sxs-lookup"><span data-stu-id="c8f31-414">Example contentFiles section</span></span>

```xml
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
```

## <a name="example-nuspec-files"></a><span data-ttu-id="c8f31-415">.nuspec 파일 예제</span><span class="sxs-lookup"><span data-stu-id="c8f31-415">Example .nuspec files</span></span>

<span data-ttu-id="c8f31-416">**dependencies 또는 files를 지정하지 않은 간단한 `.nuspec`**</span><span class="sxs-lookup"><span data-stu-id="c8f31-416">**A simple `.nuspec` that does not specify dependencies or files**</span></span>

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
    <licenseUrl>http://xunit.codeplex.com/license</licenseUrl>
    </metadata>
</package>
```

<span data-ttu-id="c8f31-417">**dependencies가 있는 `.nuspec`**</span><span class="sxs-lookup"><span data-stu-id="c8f31-417">**A `.nuspec` with dependencies**</span></span>

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

<span data-ttu-id="c8f31-418">**files가 있는 `.nuspec`**</span><span class="sxs-lookup"><span data-stu-id="c8f31-418">**A `.nuspec` with files**</span></span>

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

<span data-ttu-id="c8f31-419">**프레임워크 어셈블리가 있는 `.nuspec`**</span><span class="sxs-lookup"><span data-stu-id="c8f31-419">**A `.nuspec` with framework assemblies**</span></span>

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

<span data-ttu-id="c8f31-420">이 예제에서는 특정 프로젝트 대상에 대해 다음이 설치됩니다.</span><span class="sxs-lookup"><span data-stu-id="c8f31-420">In this example, the following are installed for specific project targets:</span></span>

- <span data-ttu-id="c8f31-421">.NET4 -> `System.Web`, `System.Net`</span><span class="sxs-lookup"><span data-stu-id="c8f31-421">.NET4 -> `System.Web`, `System.Net`</span></span>
- <span data-ttu-id="c8f31-422">.NET4 클라이언트 프로필 -> `System.Net`</span><span class="sxs-lookup"><span data-stu-id="c8f31-422">.NET4 Client Profile -> `System.Net`</span></span>
- <span data-ttu-id="c8f31-423">Silverlight 3 -> `System.Json`</span><span class="sxs-lookup"><span data-stu-id="c8f31-423">Silverlight 3 -> `System.Json`</span></span>
- <span data-ttu-id="c8f31-424">Silverlight 4 -> `System.Windows.Controls.DomainServices`</span><span class="sxs-lookup"><span data-stu-id="c8f31-424">Silverlight 4 -> `System.Windows.Controls.DomainServices`</span></span>
- <span data-ttu-id="c8f31-425">WindowsPhone -> `Microsoft.Devices.Sensors`</span><span class="sxs-lookup"><span data-stu-id="c8f31-425">WindowsPhone -> `Microsoft.Devices.Sensors`</span></span>
