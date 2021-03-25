---
title: 패키지 제작 모범 사례
description: 높은 품질의 NuGet 패키지를 생성하기 위한 모범 사례 일반 가이드입니다.
author: chgill-MSFT
ms.author: chgill
ms.date: 09/17/2020
ms.topic: conceptual
ms.openlocfilehash: 7475cf655876f2c127e79a16ccf67c0c723d164f
ms.sourcegitcommit: bb9560dcc7055bde84b4940c5eb0db402bf46a48
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 03/23/2021
ms.locfileid: "104859072"
---
# <a name="package-authoring-best-practices"></a><span data-ttu-id="0b36a-103">패키지 제작 모범 사례</span><span class="sxs-lookup"><span data-stu-id="0b36a-103">Package authoring best practices</span></span>

<span data-ttu-id="0b36a-104">이 지침은 NuGet 패키지 작성자가 높은 품질의 패키지를 만들고 게시할 수 있도록 간단한 참조 정보를 제공하기 위한 참고 자료입니다.</span><span class="sxs-lookup"><span data-stu-id="0b36a-104">This guidance is intended to give NuGet package authors a lightweight reference to create and publish high-quality packages.</span></span> <span data-ttu-id="0b36a-105">주로 메타데이터 및 압축과 같은 패키지 관련 모범 사례를 중점적으로 다룹니다.</span><span class="sxs-lookup"><span data-stu-id="0b36a-105">It will primarily focus on package-specific best practices such as metadata and packing.</span></span> <span data-ttu-id="0b36a-106">고품질 라이브러리 빌드에 대한 보다 심층적인 제안 사항은 .NET [오픈 소스 라이브러리 지침](https://docs.microsoft.com/dotnet/standard/library-guidance/)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="0b36a-106">For more in-depth suggestions for building high quality libraries, see the .NET [Open-source library guidance](https://docs.microsoft.com/dotnet/standard/library-guidance/).</span></span>

## <a name="types-of-recommendations"></a><span data-ttu-id="0b36a-107">권장 사항 유형</span><span class="sxs-lookup"><span data-stu-id="0b36a-107">Types of recommendations</span></span>

<span data-ttu-id="0b36a-108">각 문서에서는 **수행**, **고려**, **회피** 및 **금지** 의 네 가지 권장 사항 유형을 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="0b36a-108">Each article presents four types of recommendations: **Do**, **Consider**, **Avoid**, and **Do not**.</span></span> <span data-ttu-id="0b36a-109">각 권장 사항 유형은 수행해야 하는 필요성의 정도를 나타냅니다.</span><span class="sxs-lookup"><span data-stu-id="0b36a-109">The type of recommendation indicates how closely it should be followed.</span></span>

<span data-ttu-id="0b36a-110">**수행** 권장 사항은 거의 항상 따라야 합니다.</span><span class="sxs-lookup"><span data-stu-id="0b36a-110">You should almost always follow a **Do** recommendation.</span></span> <span data-ttu-id="0b36a-111">예:</span><span class="sxs-lookup"><span data-stu-id="0b36a-111">For example:</span></span>

<span data-ttu-id="0b36a-112">✔️ 패키지의 목적을 담은 간단한 설명을 포함합니다(수행).</span><span class="sxs-lookup"><span data-stu-id="0b36a-112">✔️ DO include a short description for your package that describes what it's for.</span></span>

<span data-ttu-id="0b36a-113">**고려** 권장 사항은 일반적으로 따라야 하지만 규칙에 따른 정당한 예외의 경우가 있습니다.</span><span class="sxs-lookup"><span data-stu-id="0b36a-113">On the other hand, **Consider** recommendations should generally be followed, but there are legitimate exceptions to the rule:</span></span>

<span data-ttu-id="0b36a-114">✔️ NuGet의 접두사 예약 [조건](https://docs.microsoft.com/nuget/reference/id-prefix-reservation)을 충족하는 접두사를 가진 NuGet 패키지 이름을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="0b36a-114">✔️ CONSIDER choosing a NuGet package name with a prefix that meets NuGet's prefix reservation [criteria](https://docs.microsoft.com/nuget/reference/id-prefix-reservation).</span></span>

<span data-ttu-id="0b36a-115">**회피** 권장 사항은 일반적으로 좋지는 않지만 규칙을 깨는 것이 적합한 경우를 언급합니다.</span><span class="sxs-lookup"><span data-stu-id="0b36a-115">**Avoid** recommendations mention things that are generally not a good idea, but breaking the rule sometimes makes sense:</span></span>

<span data-ttu-id="0b36a-116">❌ 정확한 버전을 요구하는 NuGet 패키지 참조는 사용하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="0b36a-116">❌ AVOID NuGet package references that demand an exact version.</span></span>

<span data-ttu-id="0b36a-117">마지막으로, **금지** 는 수행하지 않아야 하는 항목을 나타냅니다.</span><span class="sxs-lookup"><span data-stu-id="0b36a-117">And finally, **Do not** recommendations indicate something you should almost never do:</span></span>

<span data-ttu-id="0b36a-118">❌ `LicenseUrl` 메타데이터 속성은 사용하지 마세요(금지).</span><span class="sxs-lookup"><span data-stu-id="0b36a-118">❌ DO NOT use the `LicenseUrl` metadata property.</span></span>

## <a name="create-a-nuget-package"></a><span data-ttu-id="0b36a-119">NuGet 패키지 만들기</span><span class="sxs-lookup"><span data-stu-id="0b36a-119">Create a NuGet package</span></span>

<span data-ttu-id="0b36a-120">NuGet 패키지를 만드는 최신 권장 방법은 [SDK 스타일 프로젝트](https://docs.microsoft.com/nuget/resources/check-project-format)에서 만드는 것입니다.</span><span class="sxs-lookup"><span data-stu-id="0b36a-120">The latest recommended way to to create a NuGet package is from an [SDK-style project](https://docs.microsoft.com/nuget/resources/check-project-format).</span></span> <span data-ttu-id="0b36a-121">[대상 프레임워크](https://docs.microsoft.com/dotnet/standard/frameworks) 및 [패키지 메타데이터](#package-metadata)를 비롯한 SDK 스타일 프로젝트 속성은 [프로젝트 파일](https://docs.microsoft.com/visualstudio/ide/solutions-and-projects-in-visual-studio#project-file)에 정의되어 있습니다.</span><span class="sxs-lookup"><span data-stu-id="0b36a-121">SDK-style project properties, including [target framework](https://docs.microsoft.com/dotnet/standard/frameworks) and [package metadata](#package-metadata), are defined in the [project file](https://docs.microsoft.com/visualstudio/ide/solutions-and-projects-in-visual-studio#project-file).</span></span>

<span data-ttu-id="0b36a-122">[Visual Studio](https://docs.microsoft.com/nuget/quickstart/create-and-publish-a-package-using-visual-studio?tabs=netcore-cli) 또는 [dotnet CLI](https://docs.microsoft.com/nuget/quickstart/create-and-publish-a-package-using-the-dotnet-cli)에서 필수 속성과 압축을 정의하여 SDK 스타일 프로젝트에서 패키지를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="0b36a-122">Create a package from your SDK-style project by defining the required properties and packing in [Visual Studio](https://docs.microsoft.com/nuget/quickstart/create-and-publish-a-package-using-visual-studio?tabs=netcore-cli) or the [dotnet CLI](https://docs.microsoft.com/nuget/quickstart/create-and-publish-a-package-using-the-dotnet-cli).</span></span>

<span data-ttu-id="0b36a-123">✔️ SDK 스타일 프로젝트를 만들고 Visual Studio 또는 dotnet CLI를 사용하여 패키지를 생성(압축)합니다.</span><span class="sxs-lookup"><span data-stu-id="0b36a-123">✔️ DO create an SDK-style project and create (pack) your package using Visual Studio or the dotnet CLI.</span></span>

<span data-ttu-id="0b36a-124">필요한 클라이언트 도구, 프로젝트 파일 예제, 명령 등 패키지 생성에 관련된 보다 자세한 지침은 [dotnet CLI를 사용하여 NuGet 패키지 만들기](https://docs.microsoft.com/nuget/create-packages/creating-a-package-dotnet-cli)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="0b36a-124">For more detailed guidance regarding package creation including necessary client tools, project file example, and commands, see [Create a NuGet package using the dotnet CLI](https://docs.microsoft.com/nuget/create-packages/creating-a-package-dotnet-cli).</span></span>

<span data-ttu-id="0b36a-125">대상으로 지정할 .NET Framework를 결정하는 데 도움이 되도록 [플랫폼 간 대상 지정에 대한 최신 지침](https://docs.microsoft.com/dotnet/standard/library-guidance/cross-platform-targeting)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="0b36a-125">To help decide which .NET frameworks to target, see our [latest guidance for cross-platform targeting](https://docs.microsoft.com/dotnet/standard/library-guidance/cross-platform-targeting).</span></span>

## <a name="package-metadata"></a><span data-ttu-id="0b36a-126">패키지 메타데이터</span><span class="sxs-lookup"><span data-stu-id="0b36a-126">Package metadata</span></span>

<span data-ttu-id="0b36a-127">메타데이터는 모든 NuGet 패키지의 기본 구성 요소입니다.</span><span class="sxs-lookup"><span data-stu-id="0b36a-127">Metadata is a foundational component of any NuGet package.</span></span> <span data-ttu-id="0b36a-128">메타데이터의 품질은 패키지의 검색 가능성, 유용성 및 신뢰성에 크게 영향을 줄 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="0b36a-128">The quality of your metadata can vastly influence the discoverability, usability, and trustworthiness of your package.</span></span>

<span data-ttu-id="0b36a-129">Visual Studio에서 패키지 메타데이터 지정에 권장되는 방법은 프로젝트 > [프로젝트 이름] 속성 > 패키지로 이동하는 것입니다.</span><span class="sxs-lookup"><span data-stu-id="0b36a-129">In Visual Studio, the recommended way to specify package metadata is to go Project > [Project Name] Properties > Package.</span></span>

<span data-ttu-id="0b36a-130">패키지 메타데이터 요소는 [프로젝트 파일에서 직접 지정](https://docs.microsoft.com/nuget/create-packages/creating-a-package-msbuild#set-properties)할 수도 있습니다.</span><span class="sxs-lookup"><span data-stu-id="0b36a-130">Package metadata elements can also be [specified directly in the project file](https://docs.microsoft.com/nuget/create-packages/creating-a-package-msbuild#set-properties).</span></span>

<span data-ttu-id="0b36a-131">다음은 사용 가능한 패키지 메타데이터 요소를 매핑 및 설명하는 표입니다.</span><span class="sxs-lookup"><span data-stu-id="0b36a-131">Below is a table mapping and describing available package metadata elements:</span></span>

| <span data-ttu-id="0b36a-132">Visual Studio 속성 이름</span><span class="sxs-lookup"><span data-stu-id="0b36a-132">Visual Studio property name</span></span>                   | [<span data-ttu-id="0b36a-133">프로젝트 파일/MSBuild 속성 이름</span><span class="sxs-lookup"><span data-stu-id="0b36a-133">Project file/ MSBuild property name</span></span>](https://docs.microsoft.com/dotnet/core/tools/csproj#packagereleasenotes)                          | [<span data-ttu-id="0b36a-134">Nuspec 속성 이름</span><span class="sxs-lookup"><span data-stu-id="0b36a-134">Nuspec property name</span></span>](https://docs.microsoft.com/nuget/reference/nuspec#general-form-and-schema) | <span data-ttu-id="0b36a-135">Description</span><span class="sxs-lookup"><span data-stu-id="0b36a-135">Description</span></span>                                                                                                       |
|-----------------------------------------------|-----------------------------------------------------------------------------------------------------------------------------------------|---------------------------------------------------------------------------------------------------|-----------------------------------------------------------------------------------------------------------------|
| [`Package id`](#package-id)                   | [`PackageId`](https://docs.microsoft.com/dotnet/core/tools/csproj#packageid)                                                            | [`id`](https://docs.microsoft.com/nuget/reference/nuspec#id)                                      | <span data-ttu-id="0b36a-136">패키지 이름 또는 ID입니다.</span><span class="sxs-lookup"><span data-stu-id="0b36a-136">The package name or identifier.</span></span>                    |
| [`Package version`](#package-version)         | [`PackageVersion`](https://docs.microsoft.com/dotnet/core/tools/csproj#packageversion)                                                  | [`version`](https://docs.microsoft.com/nuget/reference/nuspec#version)                            | <span data-ttu-id="0b36a-137">NuGet 패키지 버전입니다.</span><span class="sxs-lookup"><span data-stu-id="0b36a-137">NuGet package version.</span></span>                                           |
| [`Authors`](#authors)                         | [`Authors`](https://docs.microsoft.com/dotnet/core/tools/csproj#authors)                                                                | [`authors`](https://docs.microsoft.com/nuget/reference/nuspec#authors)                            | <span data-ttu-id="0b36a-138">쉼표로 구분된 패키지 작성자 목록으로, 주로 개인 또는 조직의 특정 이름을 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="0b36a-138">A comma-separated list of package authors, often using the individual's or an organization's "pretty name."</span></span>                             |
| [`Description`](#description)                 | [`Description`](https://docs.microsoft.com/dotnet/core/tools/csproj#description)                                                        | [`description`](https://docs.microsoft.com/nuget/reference/nuspec#description)                    | <span data-ttu-id="0b36a-139">패키지에 대한 설명입니다.</span><span class="sxs-lookup"><span data-stu-id="0b36a-139">A description of the package.</span></span>                                                                |
| [`Copyright`](#copyright)                     | [`Copyright`](https://docs.microsoft.com/dotnet/core/tools/csproj#copyright)                                                            | [`copyright`](https://docs.microsoft.com/nuget/reference/nuspec#copyright)                        | <span data-ttu-id="0b36a-140">패키지에 대한 저작권 정보입니다.</span><span class="sxs-lookup"><span data-stu-id="0b36a-140">Copyright details for the package.</span></span>                                                                      |
| [`Licensing - Expression`](#licensing)        | [`PackageLicenseExpression`](https://docs.microsoft.com/nuget/reference/msbuild-targets#packing-a-license-expression-or-a-license-file) | [`license type="expression"`](https://docs.microsoft.com/nuget/reference/nuspec#license)          | <span data-ttu-id="0b36a-141">SPDX 라이선스 식입니다.</span><span class="sxs-lookup"><span data-stu-id="0b36a-141">An SPDX license expression.</span></span>       |
| [`Licensing - File`](#licensing)              | [`PackageLicenseFile`](https://docs.microsoft.com/nuget/reference/msbuild-targets#packing-a-license-expression-or-a-license-file)       | [`license type="file"`](https://docs.microsoft.com/nuget/reference/nuspec#license)                | <span data-ttu-id="0b36a-142">사용자 지정 라이선스 파일의 경로입니다.</span><span class="sxs-lookup"><span data-stu-id="0b36a-142">Path to a custom license file.</span></span>                                               |
| [`Project URL`](#project-url)                 | `PackageProjectUrl`                                                                                                                     | [`projectUrl`](https://docs.microsoft.com/nuget/reference/nuspec#projecturl)                      | <span data-ttu-id="0b36a-143">프로젝트 홈페이지의 URL입니다.</span><span class="sxs-lookup"><span data-stu-id="0b36a-143">A URL for the project homepage.</span></span>                                                                                   |
| [`Icon File`](#icon)                          | [`PackageIcon`](https://docs.microsoft.com/nuget/reference/msbuild-targets#packing-an-icon-image-file)                                  | [`icon`](https://docs.microsoft.com/nuget/reference/nuspec#icon)                                  | <span data-ttu-id="0b36a-144">패키지 아이콘 이미지 파일의 경로입니다.</span><span class="sxs-lookup"><span data-stu-id="0b36a-144">Path to the package icon image file.</span></span>                                                                      |
| [`Repository URL`](#repository-type-and-url)  | [`RepositoryUrl`](https://docs.microsoft.com/dotnet/core/tools/csproj#repositoryurl)                                                    | [`repository url`](https://docs.microsoft.com/nuget/reference/nuspec#repository)               | <span data-ttu-id="0b36a-145">패키지가 빌드된 리포지토리의 URL입니다.</span><span class="sxs-lookup"><span data-stu-id="0b36a-145">URL to the repository from which the package was built.</span></span>                                                           |
| [`Repository type`](#repository-type-and-url) | [`RepositoryType`](https://docs.microsoft.com/dotnet/core/tools/csproj#repositorytype)                                                 | [`repository type`](https://docs.microsoft.com/nuget/reference/nuspec#repository)              | <span data-ttu-id="0b36a-146">리포지토리 URL이 가리키는 리포지토리의 유형입니다(예: "git").</span><span class="sxs-lookup"><span data-stu-id="0b36a-146">Type of repository the repository URL is pointing to (i.e. "git").</span></span>                                                   |
| [`Tags`](#tags)                               | [`PackageTags`](https://docs.microsoft.com/dotnet/core/tools/csproj#packagetags)                                                        | [`tags`](https://docs.microsoft.com/nuget/reference/nuspec#tags)                                  | <span data-ttu-id="0b36a-147">패키지를 설명하는 태그 및 키워드의 공백으로 구분된 목록입니다.</span><span class="sxs-lookup"><span data-stu-id="0b36a-147">A space-delimited list of tags and keywords that describe the package.</span></span> <span data-ttu-id="0b36a-148">태그는 패키지를 검색할 때 사용됩니다.</span><span class="sxs-lookup"><span data-stu-id="0b36a-148">Tags are used when searching for packages.</span></span> |
| [`Release notes`](#release-notes)             | [`PackageReleaseNotes`](https://docs.microsoft.com/dotnet/core/tools/csproj#packagereleasenotes)                                          | [`releaseNotes`](https://docs.microsoft.com/nuget/reference/nuspec#releasenotes)                  | <span data-ttu-id="0b36a-149">이 패키지 릴리스의 변경 내용에 대한 설명입니다.</span><span class="sxs-lookup"><span data-stu-id="0b36a-149">A description of the changes made in this release of the package.</span></span>                                                 |

### <a name="package-id"></a><span data-ttu-id="0b36a-150">패키지 ID</span><span class="sxs-lookup"><span data-stu-id="0b36a-150">Package ID</span></span>

<span data-ttu-id="0b36a-151">완전히 새로운 패키지를 게시하는 경우 다음을 따르세요.</span><span class="sxs-lookup"><span data-stu-id="0b36a-151">If you're publishing a completely new package:</span></span>

<span data-ttu-id="0b36a-152">✔️ NuGet.org의 기존 패키지와 명확하게 구분되는 고유한 패키지 ID를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="0b36a-152">✔️ DO choose a package ID that is unique and clearly differentiated from existing packages on NuGet.org.</span></span>
> <span data-ttu-id="0b36a-153">NuGet.org에서 ID를 검색하거나 https://www.nuget.org/packages/<package 이름\> 링크가 존재하는지 확인하여 패키지 ID가 고유하고 구분 가능한지 여부를 확인할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="0b36a-153">You can check if a package ID is unique and differentiable by searching for the ID on NuGet.org or checking if the following link exists: https://www.nuget.org/packages/<package name\>.</span></span>

<span data-ttu-id="0b36a-154">✔️ NuGet 패키지 이름 선택 시 NuGet의 [접두사 예약 조건](https://docs.microsoft.com/nuget/nuget-org/id-prefix-reservation#id-prefix-reservation-criteria)을 충족하는 접두사를 가지도록 하는 것을 고려합니다.</span><span class="sxs-lookup"><span data-stu-id="0b36a-154">✔️ CONSIDER choosing a NuGet package name with a prefix that meets NuGet's [prefix reservation criteria](https://docs.microsoft.com/nuget/nuget-org/id-prefix-reservation#id-prefix-reservation-criteria).</span></span>
> <span data-ttu-id="0b36a-155">패키지에 접두사 ID를 예약하면 다음과 같은 검증 확인 표시를 가질 수 있습니다. ![이미지](media/Verified-check-mark.png)</span><span class="sxs-lookup"><span data-stu-id="0b36a-155">Reserving the prefix ID for your package will let you get the verified check mark: ![image](media/Verified-check-mark.png)</span></span>
> 
> <span data-ttu-id="0b36a-156">자세한 내용은 [패키지 ID 접두사 예약 문서](https://docs.microsoft.com/nuget/nuget-org/id-prefix-reservation)를 확인하세요.</span><span class="sxs-lookup"><span data-stu-id="0b36a-156">Check out the [Package ID prefix reservation docs](https://docs.microsoft.com/nuget/nuget-org/id-prefix-reservation) to learn more.</span></span>

### <a name="package-version"></a><span data-ttu-id="0b36a-157">패키지 버전</span><span class="sxs-lookup"><span data-stu-id="0b36a-157">Package Version</span></span>

<span data-ttu-id="0b36a-158">✔️ NuGet 패키지 버전을 관리하는 데 [SemVer](https://semver.org/)를 사용하는 것을 고려하세요.</span><span class="sxs-lookup"><span data-stu-id="0b36a-158">✔️ CONSIDER using [SemVer](https://semver.org/) to version your NuGet package.</span></span>
> <span data-ttu-id="0b36a-159">기본적으로 이는 Major.Minor.Patch[-prerelease] 형식을 사용한다는 의미입니다.</span><span class="sxs-lookup"><span data-stu-id="0b36a-159">Essentially, this means using the Major.Minor.Patch[-prerelease] format.</span></span>

<span data-ttu-id="0b36a-160">✔️ 안정적이지 않거나 미리 보기인 경우 패키지를 [시험판 패키지](https://docs.microsoft.com/nuget/create-packages/prerelease-packages)로 게시합니다.</span><span class="sxs-lookup"><span data-stu-id="0b36a-160">✔️ DO publish a package as a [pre-release package](https://docs.microsoft.com/nuget/create-packages/prerelease-packages) if it is non-stable or a preview.</span></span>

<span data-ttu-id="0b36a-161">고급 지침은 [.NET 라이브러리 버전 관리 가이드](https://docs.microsoft.com/dotnet/standard/library-guidance/versioning)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="0b36a-161">See the [.NET library versioning guide](https://docs.microsoft.com/dotnet/standard/library-guidance/versioning) for more advanced guidance.</span></span>

### <a name="authors"></a><span data-ttu-id="0b36a-162">Authors</span><span class="sxs-lookup"><span data-stu-id="0b36a-162">Authors</span></span>

<span data-ttu-id="0b36a-163">✔️ 작성자 필드에 개인 또는 조직의 특정 이름을 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="0b36a-163">✔️ DO use the author field for your or your organization's "pretty name."</span></span>
> <span data-ttu-id="0b36a-164">예를 들어 NuGet.org 사용자 이름이 "jdoe"인 경우 작성자 필드에 "Jane Doe"를 사용하면 소비자가 작성자를 알아보는 데 도움이 될 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="0b36a-164">For example, if my NuGet.org username is "jdoe" then using "Jane Doe" for the author field may help consumers recognize me as an author.</span></span> <span data-ttu-id="0b36a-165">조직의 NuGet.org 사용자 이름이 "ContosoToolkit"인 경우 "Contoso Corporation"을 사용하면 인식하기도 쉽고 소비자의 신뢰도가 높아질 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="0b36a-165">If my organization's NuGet.org username is "ContosoToolkit" then using "Contoso Corporation" may be more recognizable and inspire more consumer trust.</span></span>
### <a name="description"></a><span data-ttu-id="0b36a-166">Description</span><span class="sxs-lookup"><span data-stu-id="0b36a-166">Description</span></span>

<span data-ttu-id="0b36a-167">✔️ 패키지에 대한 간단한 설명(최대 4000자)을 포함합니다.</span><span class="sxs-lookup"><span data-stu-id="0b36a-167">✔️ DO include a short description (up to 4000 characters) to describe your package.</span></span>
> <span data-ttu-id="0b36a-168">패키지 설명은 NuGet 검색에 표시되는 가장 중요한 필드 중 하나이며, 잠재적 소비자가 패키지가 적합한지 여부를 결정할 때 가장 먼저 확인하는 것입니다.</span><span class="sxs-lookup"><span data-stu-id="0b36a-168">Package descriptions are one of the most prominent fields surfaced in NuGet search and will likely be the first thing potential consumers looks at to determine if a package is right for them.</span></span>

### <a name="copyright"></a><span data-ttu-id="0b36a-169">Copyright</span><span class="sxs-lookup"><span data-stu-id="0b36a-169">Copyright</span></span>

<span data-ttu-id="0b36a-170">✔️ "Copyright (c) <이름/회사\> <year\>" 형식으로 패키지의 저작권을 표시하는 걸 고려하세요.</span><span class="sxs-lookup"><span data-stu-id="0b36a-170">✔️ CONSIDER copyrighting your package with "Copyright (c) <name/company\> <year\>."</span></span>
><span data-ttu-id="0b36a-171">저작권 정보는 허가 없이 작업을 복사/복제할 수 없음을 나타냅니다.</span><span class="sxs-lookup"><span data-stu-id="0b36a-171">A copyright notice essentially indicates that your work cannot be copied without your permission.</span></span> <span data-ttu-id="0b36a-172">패키지에 저작권 표시를 포함하는 건 간단한 작업이며 손해 볼 것이 없습니다.</span><span class="sxs-lookup"><span data-stu-id="0b36a-172">Including a copyright notice in your package is easy and won't do any harm!</span></span>

<span data-ttu-id="0b36a-173">예: Copyright (c) Contoso 2020</span><span class="sxs-lookup"><span data-stu-id="0b36a-173">Example: Copyright (c) Contoso 2020</span></span>

### <a name="licensing"></a><span data-ttu-id="0b36a-174">라이선스</span><span class="sxs-lookup"><span data-stu-id="0b36a-174">Licensing</span></span>

<span data-ttu-id="0b36a-175">✔️ [패키지에 라이선스 식이나 라이선스 파일을 포함](https://docs.microsoft.com/nuget/reference/msbuild-targets#packing-a-license-expression-or-a-license-file)합니다.</span><span class="sxs-lookup"><span data-stu-id="0b36a-175">✔️ DO [include a license expression or license file in your package](https://docs.microsoft.com/nuget/reference/msbuild-targets#packing-a-license-expression-or-a-license-file).</span></span>
> [!IMPORTANT]
> <span data-ttu-id="0b36a-176">라이선스가 없는 프로젝트는 기본적으로 [배타적 저작권](https://choosealicense.com/no-permission/)을 사용하며, 이는 프로젝트를 사용할 권한을 누구에게도 부여하지 않았다는 것을 의미합니다.</span><span class="sxs-lookup"><span data-stu-id="0b36a-176">A project without a license defaults to [exclusive copyright](https://choosealicense.com/no-permission/), meaning that you have not granted anyone permission to use your project.</span></span>

<span data-ttu-id="0b36a-177">❌ 사용되지 않는 `LicenseUrl` 메타데이터 속성을 사용하지 마세요.</span><span class="sxs-lookup"><span data-stu-id="0b36a-177">❌ DO NOT use the deprecated `LicenseUrl` metadata property.</span></span>
> <span data-ttu-id="0b36a-178">URL에서 라이선스가 변경되면 이전 패키지 버전에 표시된 라이선스에 변경 내용이 소급 적용되므로 법적 모호성이 발생합니다.</span><span class="sxs-lookup"><span data-stu-id="0b36a-178">This presents legal ambiguity as license changes at the URL will retroactively change the displayed license for previous package versions.</span></span>

#### <a name="if-your-package-is-open-source"></a><span data-ttu-id="0b36a-179">패키지가 [오픈 소스](https://opensource.org/osd)인 경우</span><span class="sxs-lookup"><span data-stu-id="0b36a-179">If your package is [open source](https://opensource.org/osd)</span></span>

<span data-ttu-id="0b36a-180">✔️ [오픈 소스 라이선스를 선택](https://choosealicense.com/)하여 패키지를 오픈 소스로 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="0b36a-180">✔️ DO [choose an open source license](https://choosealicense.com/) to make your package open source.</span></span>
> <span data-ttu-id="0b36a-181">*"오픈 소스 라이선스는 오픈 소스 정의를 준수하는 라이선스입니다. 간단히 말하자면 소프트웨어를 자유롭게 사용, 수정 및 공유할 수 있도록 합니다."*</span><span class="sxs-lookup"><span data-stu-id="0b36a-181">*"Open source licenses are licenses that comply with the Open Source Definition — in brief, they allow software to be freely used, modified, and shared."*</span></span> <span data-ttu-id="0b36a-182">- Open Source Initiative.</span><span class="sxs-lookup"><span data-stu-id="0b36a-182">- Open Source Initiative.</span></span> <span data-ttu-id="0b36a-183">오픈 소스 소프트웨어 및 Open Source Initiative에 대해 자세히 알아보려면 https://opensource.org/ 를 확인하세요.</span><span class="sxs-lookup"><span data-stu-id="0b36a-183">To learn more about open source software and the Open Source Initiative, check out https://opensource.org/.</span></span>

<span data-ttu-id="0b36a-184">✔️ [패키지에 라이선스 식을 포함](https://docs.microsoft.com/nuget/reference/msbuild-targets#packing-a-license-expression-or-a-license-file)하는 것을 고려합니다.</span><span class="sxs-lookup"><span data-stu-id="0b36a-184">✔️ CONSIDER [including a license expression in your package](https://docs.microsoft.com/nuget/reference/msbuild-targets#packing-a-license-expression-or-a-license-file).</span></span>
> <span data-ttu-id="0b36a-185">라이선스 식은 가장 명확하게 표시되며 패키지를 사용할 수 있는지 또는 라이선스가 변경되었는지를 소비자에게 더 분명하게 알려줍니다.</span><span class="sxs-lookup"><span data-stu-id="0b36a-185">License expressions are surfaced the most clearly and make it more obvious to consumers if they can use your package or if the license has changed.</span></span> 
> [!Note]
> <span data-ttu-id="0b36a-186">NuGet.org는 Open Source Initiative 또는 Free Software Foundation에서 승인한 라이선스에 대한 라이선스 식만 허용합니다.</span><span class="sxs-lookup"><span data-stu-id="0b36a-186">NuGet.org only accepts license expressions for licenses that are approved by the Open Source Initiative or the Free Software Foundation.</span></span>

#### <a name="if-your-package-is-not-open-source"></a><span data-ttu-id="0b36a-187">패키지가 오픈 소스가 아닌 경우</span><span class="sxs-lookup"><span data-stu-id="0b36a-187">If your package is not open source</span></span>

<span data-ttu-id="0b36a-188">✔️ [패키지에 라이선스 파일을 포함](https://docs.microsoft.com/nuget/reference/msbuild-targets#packing-a-license-expression-or-a-license-file)합니다.</span><span class="sxs-lookup"><span data-stu-id="0b36a-188">✔️ DO [include a license file in your package](https://docs.microsoft.com/nuget/reference/msbuild-targets#packing-a-license-expression-or-a-license-file).</span></span>
> <span data-ttu-id="0b36a-189">비표준 라이선스를 포함하여 모든 라이선스 파일(.txt 또는 .md)을 패키지에 추가할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="0b36a-189">Any license file (.txt or .md) can be added to your package, including non-standard licenses.</span></span> 

### <a name="project-url"></a><span data-ttu-id="0b36a-190">프로젝트 URL</span><span class="sxs-lookup"><span data-stu-id="0b36a-190">Project URL</span></span>

<span data-ttu-id="0b36a-191">✔️ 관련 프로젝트, 리포지토리 또는 회사 웹 사이트로 연결되는 링크를 포함하는 것을 고려합니다.</span><span class="sxs-lookup"><span data-stu-id="0b36a-191">✔️ CONSIDER including a link to an associated project, repository, or company website.</span></span>
> <span data-ttu-id="0b36a-192">프로젝트 사이트에는 사용자가 패키지에 대해 알아야 하는 모든 정보가 있어야 하며 많은 경우 사용자가 설명서를 찾는 위치이기도 합니다.</span><span class="sxs-lookup"><span data-stu-id="0b36a-192">Your project site should have everything users need to know about your package and will likely be where users look for documentation.</span></span>

### <a name="icon"></a><span data-ttu-id="0b36a-193">아이콘</span><span class="sxs-lookup"><span data-stu-id="0b36a-193">Icon</span></span>

<span data-ttu-id="0b36a-194">✔️ 패키지를 시각적으로 구분할 수 있도록 [패키지에 아이콘을 포함](https://docs.microsoft.com/nuget/reference/msbuild-targets#packing-an-icon-image-file)하는 것을 고려합니다.</span><span class="sxs-lookup"><span data-stu-id="0b36a-194">✔️ CONSIDER [including an icon with your package](https://docs.microsoft.com/nuget/reference/msbuild-targets#packing-an-icon-image-file) to help visually differentiate it.</span></span> <span data-ttu-id="0b36a-195">이 같은 비교적 사소한 추가를 통해 패키지 인지도를 향상시킬 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="0b36a-195">It's a relatively small addition that can improve perception of package quality.</span></span>
> <span data-ttu-id="0b36a-196">아이콘은 개별 패키지에 특정될 수도 있고 브랜드 로고일 수도 있습니다.</span><span class="sxs-lookup"><span data-stu-id="0b36a-196">Icons can be specific to individual packages or be a brand logo.</span></span>

<span data-ttu-id="0b36a-197">✔️ 보기 결과를 최적화하기 위해 128x128이고 투명한 배경을 가진 이미지(PNG)를 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="0b36a-197">✔️ DO use an image that is 128x128 and has a transparent background (PNG) for best viewing results.</span></span>
> <span data-ttu-id="0b36a-198">NuGet은 이미지가 표시되는 클라이언트에 맞게 이미지 크기를 자동으로 조정합니다.</span><span class="sxs-lookup"><span data-stu-id="0b36a-198">NuGet will automatically scale your image to the client it is being displayed on.</span></span>

<span data-ttu-id="0b36a-199">❌사용되지 않는`IconUrl` 메타데이터 속성을 사용하지 마세요.</span><span class="sxs-lookup"><span data-stu-id="0b36a-199">❌ DO NOT use the deprecated `IconUrl` metadata property.</span></span>

### <a name="repository-type-and-url"></a><span data-ttu-id="0b36a-200">리포지토리 유형 및 URL</span><span class="sxs-lookup"><span data-stu-id="0b36a-200">Repository Type and URL</span></span>

<span data-ttu-id="0b36a-201">✔️ [소스 링크](https://docs.microsoft.com/dotnet/standard/library-guidance/sourcelink)를 설정하여 NuGet 패키지에 소스 제어 메타데이터를 자동으로 추가하고 라이브러리를 쉽게 디버그할 수 있도록 하는 것을 고려합니다.</span><span class="sxs-lookup"><span data-stu-id="0b36a-201">✔️ CONSIDER setting up [Source Link](https://docs.microsoft.com/dotnet/standard/library-guidance/sourcelink) to automatically add source control metadata to your NuGet package and make your library easier to debug.</span></span>
> <span data-ttu-id="0b36a-202">소스 링크는 `Repository URL` 및 `Repository Type`을 패키지 메타데이터에 자동으로 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="0b36a-202">Source Link automatically adds `Repository URL` and `Repository Type` to the package metadata.</span></span> <span data-ttu-id="0b36a-203">또한 패키지 버전과 연결된 특정 커밋을 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="0b36a-203">It also adds the specific commit associated with your package version.</span></span>

### <a name="tags"></a><span data-ttu-id="0b36a-204">태그</span><span class="sxs-lookup"><span data-stu-id="0b36a-204">Tags</span></span>

<span data-ttu-id="0b36a-205">✔️ 검색 가능성을 향상시키기 위해 패키지와 관련된 주요 용어를 사용해 여러 태그를 포함합니다.</span><span class="sxs-lookup"><span data-stu-id="0b36a-205">✔️ DO include several tags with key terms related to your package to enhance discoverability.</span></span>
> <span data-ttu-id="0b36a-206">NuGet.org의 검색 알고리즘은 태그를 고려합니다. 태그는 특히 패키지 ID에는 없지만 관련성 있는 용어에 특히 유용합니다.</span><span class="sxs-lookup"><span data-stu-id="0b36a-206">Tags are taken into account in NuGet.org's search algorithm and are especially helpful for terms that are not in the Package ID but are relevant.</span></span>

<span data-ttu-id="0b36a-207">예를 들어 콘솔에 문자열을 기록하는 패키지를 게시한 경우 "로깅, 로그, 콘솔, 문자열, 출력"을 포함합니다.</span><span class="sxs-lookup"><span data-stu-id="0b36a-207">For example, if I published a package to log strings to the console, I would include: "logging, log, console, string, output"</span></span>

### <a name="release-notes"></a><span data-ttu-id="0b36a-208">릴리스 정보</span><span class="sxs-lookup"><span data-stu-id="0b36a-208">Release notes</span></span>

<span data-ttu-id="0b36a-209">✔️ 업데이트가 있을 때마다 변경 내용에 대해 설명하는 릴리스 정보를 포함하는 것을 고려합니다.</span><span class="sxs-lookup"><span data-stu-id="0b36a-209">✔️ CONSIDER including release notes with each update describing what changes were made.</span></span>
> <span data-ttu-id="0b36a-210">릴리스 정보에 요구되는 특정 형식은 없지만 다음을 포함하는 것이 좋습니다.</span><span class="sxs-lookup"><span data-stu-id="0b36a-210">While there is no specific format required for release notes, we recommend including:</span></span>
>
> 1. <span data-ttu-id="0b36a-211">주요 변경 내용</span><span class="sxs-lookup"><span data-stu-id="0b36a-211">Breaking changes</span></span>
> 2. <span data-ttu-id="0b36a-212">새로운 기능</span><span class="sxs-lookup"><span data-stu-id="0b36a-212">New features</span></span>
> 3. <span data-ttu-id="0b36a-213">버그 수정</span><span class="sxs-lookup"><span data-stu-id="0b36a-213">Bug fixes</span></span>
> 
> <span data-ttu-id="0b36a-214">리포지토리에서 릴리스 정보 또는 변경 로그를 이미 추적하는 경우 관련 파일로 연결되는 링크를 포함할 수도 있습니다.</span><span class="sxs-lookup"><span data-stu-id="0b36a-214">If you already track release notes or a changelog in your repo, you can also include a link to the relevant file.</span></span>

## <a name="related-topics"></a><span data-ttu-id="0b36a-215">관련 항목</span><span class="sxs-lookup"><span data-stu-id="0b36a-215">Related topics</span></span>

- [<span data-ttu-id="0b36a-216">패키지 만들기 및 게시(dotnet CLI)</span><span class="sxs-lookup"><span data-stu-id="0b36a-216">Create and publish a package (dotnet CLI)</span></span>](https://docs.microsoft.com/nuget/quickstart/create-and-publish-a-package-using-the-dotnet-cli)
- [<span data-ttu-id="0b36a-217">패키지 만들기 및 게시(Visual Studio)</span><span class="sxs-lookup"><span data-stu-id="0b36a-217">Create and publish a package (Visual Studio)</span></span>](https://docs.microsoft.com/nuget/quickstart/create-and-publish-a-package-using-visual-studio?tabs=netcore-cli)
