---
title: NuGet 1.5 릴리스 정보
description: 알려진 문제, 버그 수정, 추가 된 기능 및 Ecrs를 비롯 한 NuGet 1.5에 대 한 릴리스 정보입니다.
author: karann-msft
ms.author: karann
ms.date: 11/11/2016
ms.topic: conceptual
ms.openlocfilehash: 940a19cdc485d611d03b52ee3102bc95a78a36bb
ms.sourcegitcommit: 26a8eae00af2d4be581171e7a73009f94534c336
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 12/25/2019
ms.locfileid: "75383351"
---
# <a name="nuget-15-release-notes"></a><span data-ttu-id="34236-103">NuGet 1.5 릴리스 정보</span><span class="sxs-lookup"><span data-stu-id="34236-103">NuGet 1.5 Release Notes</span></span>

<span data-ttu-id="34236-104">Nuget [1.4 릴리스 정보](../release-notes/nuget-1.4.md) | [Nuget 1.6 릴리스 정보](../release-notes/nuget-1.6.md)</span><span class="sxs-lookup"><span data-stu-id="34236-104">[NuGet 1.4 Release Notes](../release-notes/nuget-1.4.md) | [NuGet 1.6 Release Notes](../release-notes/nuget-1.6.md)</span></span>

<span data-ttu-id="34236-105">NuGet 1.5은 2011 년 8 월 30 일에 출시 되었습니다.</span><span class="sxs-lookup"><span data-stu-id="34236-105">NuGet 1.5 was released on August 30, 2011.</span></span>

## <a name="features"></a><span data-ttu-id="34236-106">기능</span><span class="sxs-lookup"><span data-stu-id="34236-106">Features</span></span>

### <a name="project-templates-with-preinstalled-nuget-packages"></a><span data-ttu-id="34236-107">사전 설치 된 NuGet 패키지를 사용 하는 프로젝트 템플릿</span><span class="sxs-lookup"><span data-stu-id="34236-107">Project Templates with Preinstalled NuGet Packages</span></span>
<span data-ttu-id="34236-108">새 ASP.NET MVC 3 프로젝트 템플릿을 만들 때 프로젝트에 포함 된 jQuery 스크립트 라이브러리는 NuGet 패키지를 설치 하 여 실제로 배치 됩니다.</span><span class="sxs-lookup"><span data-stu-id="34236-108">When creating a new ASP.NET MVC 3 project template, the jQuery script libraries included in the project are actually placed there by installing NuGet packages.</span></span>

<span data-ttu-id="34236-109">ASP.NET MVC 3 프로젝트 템플릿에는 프로젝트 템플릿이 호출 될 때 설치 되는 NuGet 패키지 집합이 포함 되어 있습니다.</span><span class="sxs-lookup"><span data-stu-id="34236-109">The ASP.NET MVC 3 project template includes a set of NuGet packages that get installed when the project template is invoked.</span></span> <span data-ttu-id="34236-110">프로젝트 템플릿에 NuGet 패키지를 포함 하는이 기능은 이제 _모든_ 프로젝트 템플릿이 활용할 수 있는 nuget의 기능입니다.</span><span class="sxs-lookup"><span data-stu-id="34236-110">This ability to include NuGet packages with a project template is now a feature of NuGet that _any_ project template can now take advantage of.</span></span>

<span data-ttu-id="34236-111">이 기능에 대 한 자세한 내용은 [기능 개발자가이 블로그 게시물](https://blogs.msdn.com/b/marcinon/archive/2011/07/08/project-templates-and-preinstalled-nuget-packages.aspx)을 참조 하세요.</span><span class="sxs-lookup"><span data-stu-id="34236-111">For more details about this feature, read this [blog post by the developer of the feature](https://blogs.msdn.com/b/marcinon/archive/2011/07/08/project-templates-and-preinstalled-nuget-packages.aspx).</span></span>

### <a name="explicit-assembly-references"></a><span data-ttu-id="34236-112">명시적 어셈블리 참조</span><span class="sxs-lookup"><span data-stu-id="34236-112">Explicit Assembly References</span></span>

<span data-ttu-id="34236-113">패키지 내에서 참조할 어셈블리를 명시적으로 지정 하는 데 사용 되는 새로운 `<references />` 요소를 추가 했습니다.</span><span class="sxs-lookup"><span data-stu-id="34236-113">Added a new `<references />` element used to explicitly specify which assemblies within the the package should be referenced.</span></span>

<span data-ttu-id="34236-114">예를 들어 다음을 추가 합니다.</span><span class="sxs-lookup"><span data-stu-id="34236-114">For example, if you add the following:</span></span>

```xml
<references>
    <reference file="xunit.dll" />
    <reference file="xunit.extensions.dll" />
</references>
```

<span data-ttu-id="34236-115">그런 다음 폴더에 다른 어셈블리가 있는 경우에도 `xunit.dll` 및 `xunit.extensions.dll` `lib` 폴더의 해당 [프레임 워크/프로필 하위 폴더](../reference/nuspec.md#explicit-assembly-references) 에서 참조 됩니다.</span><span class="sxs-lookup"><span data-stu-id="34236-115">Then only the `xunit.dll` and `xunit.extensions.dll` will be referenced from the appropriate [framework/profile subfolder](../reference/nuspec.md#explicit-assembly-references) of the `lib` folder even if there are other assemblies in the folder.</span></span>

<span data-ttu-id="34236-116">이 요소를 생략 하면 `lib` 폴더의 모든 어셈블리를 참조 하는 일반적인 동작이 적용 됩니다.</span><span class="sxs-lookup"><span data-stu-id="34236-116">If this element is omitted, then the usual behavior applies, which is to reference every assembly in the `lib` folder.</span></span>

<span data-ttu-id="34236-117">__이 기능은 어떻게 사용 되나요?__</span><span class="sxs-lookup"><span data-stu-id="34236-117">__What is this feature used for?__</span></span>

<span data-ttu-id="34236-118">이 기능은 디자인 타임 전용 어셈블리를 지원 합니다.</span><span class="sxs-lookup"><span data-stu-id="34236-118">This feature supports design-time only assemblies.</span></span> <span data-ttu-id="34236-119">예를 들어 코드 계약을 사용 하는 경우 Visual Studio에서 해당 계약 어셈블리를 찾을 수 있도록 확장 하는 런타임 어셈블리 옆에 계약 어셈블리가 있어야 하지만, 계약 어셈블리는 실제로 프로젝트에서 참조 되지 않으므로 `bin` 폴더에 복사 하면 안 됩니다.</span><span class="sxs-lookup"><span data-stu-id="34236-119">For example, when using Code Contracts, the contract assemblies need to be next to the runtime assemblies that they augment so that Visual Studio can find them, but the contract assemblies should not actually be referenced by the project and should not be copied into the `bin` folder.</span></span>

<span data-ttu-id="34236-120">마찬가지로, 기능을 XUnit과 같은 단위 테스트 프레임 워크에 사용할 수 있습니다 .이 경우 도구 어셈블리는 런타임 어셈블리 옆에 배치 해야 하지만 프로젝트 참조에서는 제외 됩니다.</span><span class="sxs-lookup"><span data-stu-id="34236-120">Likewise, the feature can be used to for unit test frameworks such as XUnit which need its tools assemblies to be located next to the runtime assemblies, but excluded from project references.</span></span>

### <a name="added-ability-to-exclude-files-in-the-nuspec"></a><span data-ttu-id="34236-121">Nuspec에서 파일을 제외 하는 기능이 추가 되었습니다.</span><span class="sxs-lookup"><span data-stu-id="34236-121">Added ability to exclude files in the .nuspec</span></span>
<span data-ttu-id="34236-122">`.nuspec` 파일 내의 `<file>` 요소는 와일드 카드를 사용 하 여 특정 파일이 나 파일 집합을 포함 하는 데 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="34236-122">The `<file>` element within a `.nuspec` file can be used to include a specific file or a set of files using a wildcard.</span></span> <span data-ttu-id="34236-123">와일드 카드를 사용 하는 경우 포함 된 파일의 특정 하위 집합을 제외할 수 있는 방법이 없습니다.</span><span class="sxs-lookup"><span data-stu-id="34236-123">When using a wildcard, there's no way to exclude a specific subset of the included files.</span></span> <span data-ttu-id="34236-124">예를 들어 특정 폴더에 있는 모든 텍스트 파일을 제외 하 고 모든 텍스트 파일을 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="34236-124">For example, suppose you want all text files within a folder except a specific one.</span></span>

```xml
<files>
    <file src="*.txt" target="content\docs" exclude="admin.txt" />
</files>
```

<span data-ttu-id="34236-125">여러 파일을 지정 하려면 세미콜론을 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="34236-125">Use semicolons to specify multiple files.</span></span>

```xml
<files>
    <file src="*.txt" target="content\docs" exclude="admin.txt;log.txt" />
</files>
```

<span data-ttu-id="34236-126">또는 와일드 카드를 사용 하 여 모든 백업 파일과 같은 파일 집합을 제외 합니다.</span><span class="sxs-lookup"><span data-stu-id="34236-126">Or use a wild card to exclude a set of files such as all backup files</span></span>

```xml
<files>
    <file src="tools\*.*" target="tools" exclude="*.bak" />
</files>
```

### <a name="removing-packages-using-the-dialog-prompts-to-remove-dependencies"></a><span data-ttu-id="34236-127">종속성을 제거 하 라는 대화 상자를 사용 하 여 패키지 제거</span><span class="sxs-lookup"><span data-stu-id="34236-127">Removing packages using the dialog prompts to remove dependencies</span></span>
<span data-ttu-id="34236-128">종속성이 포함 된 패키지를 제거 하면 NuGet 프롬프트가 표시 되어 패키지와 함께 패키지의 종속성을 제거할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="34236-128">When uninstalling a package with dependencies, NuGet prompts, allowing the removal of a package's dependencies along with the package.</span></span>

![종속 패키지 제거](./media/remove-dependent-packages.png)


### <a name="get-package-command-improvement"></a><span data-ttu-id="34236-130">`Get-Package` 명령 향상</span><span class="sxs-lookup"><span data-stu-id="34236-130">`Get-Package` command improvement</span></span>
<span data-ttu-id="34236-131">`Get-Package` 명령은 이제 `-ProjectName` 매개 변수를 지원 합니다.</span><span class="sxs-lookup"><span data-stu-id="34236-131">The `Get-Package` command now supports a `-ProjectName` parameter.</span></span> <span data-ttu-id="34236-132">따라서 명령</span><span class="sxs-lookup"><span data-stu-id="34236-132">So the command</span></span>

    Get-Package –ProjectName A

<span data-ttu-id="34236-133">프로젝트 A에 설치 된 모든 패키지를 나열 합니다.</span><span class="sxs-lookup"><span data-stu-id="34236-133">will list all packages installed in project A.</span></span>

### <a name="support-for-proxies-that-require-authentication"></a><span data-ttu-id="34236-134">인증이 필요한 프록시에 대 한 지원</span><span class="sxs-lookup"><span data-stu-id="34236-134">Support for Proxies that require authentication</span></span>
<span data-ttu-id="34236-135">인증을 필요로 하는 프록시 뒤에 NuGet을 사용할 때 NuGet은 이제 프록시 자격 증명을 묻는 메시지를 표시 합니다.</span><span class="sxs-lookup"><span data-stu-id="34236-135">When using NuGet behind a proxy that requires authentication, NuGet will now prompt for proxy credentials.</span></span> <span data-ttu-id="34236-136">자격 증명을 입력 하면 NuGet에서 원격 리포지토리에 연결할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="34236-136">Entering credentials allows NuGet to connect to the remote repository.</span></span>

### <a name="support-for-repositories-that-require-authentication"></a><span data-ttu-id="34236-137">인증을 요구 하는 리포지토리에 대 한 지원</span><span class="sxs-lookup"><span data-stu-id="34236-137">Support for Repositories that require authentication</span></span>
<span data-ttu-id="34236-138">이제 NuGet에서 기본 또는 NTLM 인증을 요구 하는 [개인 리포지토리에](../hosting-packages/local-feeds.md) 연결할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="34236-138">NuGet now supports connecting to [private repositories](../hosting-packages/local-feeds.md) that require basic or NTLM authentication.</span></span>

<span data-ttu-id="34236-139">다이제스트 인증에 대 한 지원은 향후 릴리스에 추가 될 예정입니다.</span><span class="sxs-lookup"><span data-stu-id="34236-139">Support for Digest authentication will be added in a future release.</span></span>

### <a name="performance-improvements-to-the-nugetorg-repository"></a><span data-ttu-id="34236-140">Nuget.org 리포지토리의 성능 향상</span><span class="sxs-lookup"><span data-stu-id="34236-140">Performance improvements to the nuget.org repository</span></span>
<span data-ttu-id="34236-141">Nuget.org 갤러리에 대 한 몇 가지 성능 향상으로 패키지 목록 및 검색을 더 빠르게 수행할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="34236-141">We've made several performance improvements to the nuget.org gallery to make package listing and searching faster.</span></span>

### <a name="solution-dialog-project-filtering"></a><span data-ttu-id="34236-142">솔루션 대화 상자 프로젝트 필터링</span><span class="sxs-lookup"><span data-stu-id="34236-142">Solution dialog project filtering</span></span>
<span data-ttu-id="34236-143">솔루션 수준 대화 상자에서 설치할 프로젝트를 묻는 메시지가 표시 되 면 선택한 패키지와 호환 되는 프로젝트만 표시 됩니다.</span><span class="sxs-lookup"><span data-stu-id="34236-143">In the Solution-level dialog, when prompting for what projects to install, we only show projects that are compatible with the selected package.</span></span>

### <a name="package-release-notes"></a><span data-ttu-id="34236-144">패키지 릴리스 정보</span><span class="sxs-lookup"><span data-stu-id="34236-144">Package Release Notes</span></span>
<span data-ttu-id="34236-145">이제 NuGet 패키지에 릴리스 정보에 대 한 지원이 포함 됩니다.</span><span class="sxs-lookup"><span data-stu-id="34236-145">NuGet packages now include support for release notes.</span></span> <span data-ttu-id="34236-146">릴리스 정보는 패키지에 대 한 _업데이트_ 를 볼 때만 표시 되므로 첫 번째 릴리스에 추가 하는 것은 적합 하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="34236-146">The release notes only show up when viewing _Updates_ for a package, so it doesn't make sense to add them to your first release.</span></span>

![업데이트 탭 내 릴리스 정보](./media/manage-nuget-packages-release-notes.png)

<span data-ttu-id="34236-148">패키지에 릴리스 정보를 추가 하려면 NuSpec 파일에 새 `<releaseNotes />` metadata 요소를 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="34236-148">To add release notes to a package, use the new `<releaseNotes />` metadata element in your NuSpec file.</span></span>

### <a name="nuspec-ltfiles-gt-improvement"></a><span data-ttu-id="34236-149">. nuspec & ltfiles/&gt; 개선</span><span class="sxs-lookup"><span data-stu-id="34236-149">.nuspec &ltfiles /&gt; improvement</span></span>
<span data-ttu-id="34236-150">이제 `.nuspec` 파일에 빈 `<files />` 요소가 허용 됩니다. 그러면 nuget.exe는 패키지에 파일을 포함 하지 않도록 합니다.</span><span class="sxs-lookup"><span data-stu-id="34236-150">The `.nuspec` file now allows empty `<files />` element, which tells nuget.exe not to include any file in the package.</span></span>

## <a name="bug-fixes"></a><span data-ttu-id="34236-151">버그 수정</span><span class="sxs-lookup"><span data-stu-id="34236-151">Bug Fixes</span></span>
<span data-ttu-id="34236-152">NuGet 1.5에는 총 107 개의 작업 항목이 수정 되었습니다.</span><span class="sxs-lookup"><span data-stu-id="34236-152">NuGet 1.5 had a total of 107 work items fixed.</span></span> <span data-ttu-id="34236-153">103는 버그로 표시 되어 있습니다.</span><span class="sxs-lookup"><span data-stu-id="34236-153">103 of those were marked as bugs.</span></span>

<span data-ttu-id="34236-154">NuGet 1.5에서 수정 된 작업 항목의 전체 목록은 [이 릴리스에 대 한 Nuget 문제 추적기](http://nuget.codeplex.com/workitem/list/advanced?keyword=&status=All&type=All&priority=All&release=NuGet%201.5&assignedTo=All&component=All&sortField=Summary&sortDirection=Descending&page=0)를 확인 하세요.</span><span class="sxs-lookup"><span data-stu-id="34236-154">For a full list of work items fixed in NuGet 1.5, please view the [NuGet Issue Tracker for this release](http://nuget.codeplex.com/workitem/list/advanced?keyword=&status=All&type=All&priority=All&release=NuGet%201.5&assignedTo=All&component=All&sortField=Summary&sortDirection=Descending&page=0).</span></span>

## <a name="bug-fixes-worth-noting"></a><span data-ttu-id="34236-155">버그가 수정 될 만한 문제:</span><span class="sxs-lookup"><span data-stu-id="34236-155">Bug fixes worth noting:</span></span>

* <span data-ttu-id="34236-156">[문제 1273](http://nuget.codeplex.com/workitem/1273): 패키지를 사전순으로 정렬 하 고 추가 공백을 제거 하 여 더 많은 버전 제어를 `packages.config` 했습니다.</span><span class="sxs-lookup"><span data-stu-id="34236-156">[Issue 1273](http://nuget.codeplex.com/workitem/1273): Made `packages.config` more version control friendly by sorting packages alphabetically and removing extra whitespace.</span></span>
* <span data-ttu-id="34236-157">[문제 844](http://nuget.codeplex.com/workitem/844): 버전이 `1.0.0`인 패키지에서 `Install-Package 1.0` 작동 하도록 버전 번호가 정규화 되었습니다.</span><span class="sxs-lookup"><span data-stu-id="34236-157">[Issue 844](http://nuget.codeplex.com/workitem/844): Version numbers are now normalized so that `Install-Package 1.0` works on a package with the version `1.0.0`.</span></span>
* <span data-ttu-id="34236-158">[문제 1060](http://nuget.codeplex.com/workitem/1060): nuget.exe를 사용 하 여 패키지를 만들 때 `-Version` 플래그가 `<version />` 요소를 재정의 합니다.</span><span class="sxs-lookup"><span data-stu-id="34236-158">[Issue 1060](http://nuget.codeplex.com/workitem/1060): When creating a package using nuget.exe, the `-Version` flag overrides the `<version />` element.</span></span>
