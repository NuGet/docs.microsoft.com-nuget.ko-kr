---
title: "NuGet 1.5 릴리스 정보 | Microsoft Docs"
author: karann-msft
ms.author: karann-msft
manager: ghogen
ms.date: 11/11/2016
ms.topic: article
ms.prod: nuget
ms.technology: 
description: "알려진된 문제, 버그 수정, 추가 된 기능 및 Dcr를 포함 하 여 NuGet 1.5에 대 한 릴리스 정보입니다."
keywords: "NuGet 1.5 릴리스 정보, 버그 수정, 알려진 문제, 추가 기능을 Dcr"
ms.reviewer:
- karann-msft
- unniravindranathan
ms.openlocfilehash: 261cfbbd262bad28f142b0c3dff8a541641d9fda
ms.sourcegitcommit: 262d026beeffd4f3b6fc47d780a2f701451663a8
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 01/25/2018
---
# <a name="nuget-15-release-notes"></a><span data-ttu-id="b1805-104">NuGet 1.5 릴리스 정보</span><span class="sxs-lookup"><span data-stu-id="b1805-104">NuGet 1.5 Release Notes</span></span>

<span data-ttu-id="b1805-105">[NuGet 1.4 릴리스 정보](../release-notes/nuget-1.4.md) | [NuGet 1.6 릴리스 정보](../release-notes/nuget-1.6.md)</span><span class="sxs-lookup"><span data-stu-id="b1805-105">[NuGet 1.4 Release Notes](../release-notes/nuget-1.4.md) | [NuGet 1.6 Release Notes](../release-notes/nuget-1.6.md)</span></span>

<span data-ttu-id="b1805-106">NuGet 1.5 2011 년 8 월 30 일에 출시 되었습니다.</span><span class="sxs-lookup"><span data-stu-id="b1805-106">NuGet 1.5 was released on August 30, 2011.</span></span>

## <a name="features"></a><span data-ttu-id="b1805-107">기능</span><span class="sxs-lookup"><span data-stu-id="b1805-107">Features</span></span>

### <a name="project-templates-with-preinstalled-nuget-packages"></a><span data-ttu-id="b1805-108">사전 설치 된 NuGet 패키지와 프로젝트 템플릿</span><span class="sxs-lookup"><span data-stu-id="b1805-108">Project Templates with Preinstalled NuGet Packages</span></span>
<span data-ttu-id="b1805-109">새 ASP.NET MVC 3 프로젝트 서식 파일을 만들 때 프로젝트에 포함 된 jQuery 스크립트 라이브러리 NuGet 패키지를 설치 하 여 있습니다 배치 실제로 됩니다.</span><span class="sxs-lookup"><span data-stu-id="b1805-109">When creating a new ASP.NET MVC 3 project template, the jQuery script libraries included in the project are actually placed there by installing NuGet packages.</span></span>

<span data-ttu-id="b1805-110">ASP.NET MVC 3 프로젝트 템플릿은 프로젝트 템플릿은 호출 될 때 설치 하는 NuGet 패키지의 집합을 가집니다.</span><span class="sxs-lookup"><span data-stu-id="b1805-110">The ASP.NET MVC 3 project template includes a set of NuGet packages that get installed when the project template is invoked.</span></span> <span data-ttu-id="b1805-111">프로젝트 템플릿 사용 하 여 NuGet 패키지를 포함 하는이 기능은 NuGet의 기능은 이제는 _모든_ 프로젝트 템플릿은 이제 활용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="b1805-111">This ability to include NuGet packages with a project template is now a feature of NuGet that _any_ project template can now take advantage of.</span></span>

<span data-ttu-id="b1805-112">이 기능에 대 한 자세한 내용은이 내용을 읽고 [기능의 개발자가 블로그 게시물](http://blogs.msdn.com/b/marcinon/archive/2011/07/08/project-templates-and-preinstalled-nuget-packages.aspx)합니다.</span><span class="sxs-lookup"><span data-stu-id="b1805-112">For more details about this feature, read this [blog post by the developer of the feature](http://blogs.msdn.com/b/marcinon/archive/2011/07/08/project-templates-and-preinstalled-nuget-packages.aspx).</span></span>

### <a name="explicit-assembly-references"></a><span data-ttu-id="b1805-113">명시적 어셈블리 참조</span><span class="sxs-lookup"><span data-stu-id="b1805-113">Explicit Assembly References</span></span>

<span data-ttu-id="b1805-114">새 추가 `<references />` 내에서 어셈블리를 명시적으로 지정 하는 데 사용 되는 요소는 패키지를 참조 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="b1805-114">Added a new `<references />` element used to explicitly specify which assemblies within the the package should be referenced.</span></span>

<span data-ttu-id="b1805-115">예를 들어, 다음을 추가 하는 경우:</span><span class="sxs-lookup"><span data-stu-id="b1805-115">For example, if you add the following:</span></span>

```xml
<references>
    <reference file="xunit.dll" />
    <reference file="xunit.extensions.dll" />
</references>
```

<span data-ttu-id="b1805-116">그런 다음만 `xunit.dll` 및 `xunit.extensions.dll` 적절 한 참조할 수 [프레임 워크/프로필 하위 폴더](../schema/nuspec.md#explicit-assembly-references) 의 `lib` 폴더에에서 있는 경우 다른 어셈블리 폴더에도 합니다.</span><span class="sxs-lookup"><span data-stu-id="b1805-116">Then only the `xunit.dll` and `xunit.extensions.dll` will be referenced from the appropriate [framework/profile subfolder](../schema/nuspec.md#explicit-assembly-references) of the `lib` folder even if there are other assemblies in the folder.</span></span>

<span data-ttu-id="b1805-117">이 요소를 생략 하면 경우 일반적으로 삭제 적용에서 모든 어셈블리를 참조 하는 것입니다는 `lib` 폴더입니다.</span><span class="sxs-lookup"><span data-stu-id="b1805-117">If this element is omitted, then the usual behavior applies, which is to reference every assembly in the `lib` folder.</span></span>

<span data-ttu-id="b1805-118">__이 기능은 용도 무엇입니까?__</span><span class="sxs-lookup"><span data-stu-id="b1805-118">__What is this feature used for?__</span></span>

<span data-ttu-id="b1805-119">이 기능은 디자인 타임 전용 어셈블리를 지원합니다.</span><span class="sxs-lookup"><span data-stu-id="b1805-119">This feature supports design-time only assemblies.</span></span> <span data-ttu-id="b1805-120">예를 들어, 코드 계약을 사용할 경우 계약 어셈블리 해야 Visual Studio를 찾을 수 있습니다 하지만 계약 어셈블리 실제로 프로젝트에서 참조 되지 하도록 및에 복사 되지 않도록를 확장 하는 런타임 어셈블리 옆에 있습니다 `bin` 폴더입니다.</span><span class="sxs-lookup"><span data-stu-id="b1805-120">For example, when using Code Contracts, the contract assemblies need to be next to the runtime assemblies that they augment so that Visual Studio can find them, but the contract assemblies should not actually be referenced by the project and should not be copied into the `bin` folder.</span></span>

<span data-ttu-id="b1805-121">마찬가지로,을 런타임에서 어셈블리 옆에 있는 수는 있지만 프로젝트 참조에서 제외 도구 어셈블리 필요한 XUnit 등 단위 테스트 프레임 워크에 대 한 하는 기능은 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="b1805-121">Likewise, the feature can be used to for unit test frameworks such as XUnit which need its tools assemblies to be located next to the runtime assemblies, but excluded from project references.</span></span>

### <a name="added-ability-to-exclude-files-in-the-nuspec"></a><span data-ttu-id="b1805-122">추가 기능에는.nuspec 파일을 제외 하려면</span><span class="sxs-lookup"><span data-stu-id="b1805-122">Added ability to exclude files in the .nuspec</span></span>
<span data-ttu-id="b1805-123">`<file>` 내의 요소는 `.nuspec` 특정 파일 또는 와일드 카드를 사용 하 여 파일 집합을 포함 하도록 파일을 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="b1805-123">The `<file>` element within a `.nuspec` file can be used to include a specific file or a set of files using a wildcard.</span></span> <span data-ttu-id="b1805-124">와일드 카드를 사용할 경우에 포함 된 파일의 특정 하위 집합을 제외 하려면 방법은.</span><span class="sxs-lookup"><span data-stu-id="b1805-124">When using a wildcard, there's no way to exclude a specific subset of the included files.</span></span> <span data-ttu-id="b1805-125">예를 들어 특정 제외 하 고 폴더 내의 모든 텍스트 파일을 한다고 가정 합니다.</span><span class="sxs-lookup"><span data-stu-id="b1805-125">For example, suppose you want all text files within a folder except a specific one.</span></span>

```xml
<files>
    <file src="*.txt" target="content\docs" exclude="admin.txt" />
</files>
```

<span data-ttu-id="b1805-126">세미콜론을 사용 하 여 여러 파일을 지정 합니다.</span><span class="sxs-lookup"><span data-stu-id="b1805-126">Use semicolons to specify multiple files.</span></span>

```xml
<files>
    <file src="*.txt" target="content\docs" exclude="admin.txt;log.txt" />
</files>
```

<span data-ttu-id="b1805-127">와일드 카드를 사용 하 여 백업 파일을 모두 같은 파일의 집합을 제외할 또는</span><span class="sxs-lookup"><span data-stu-id="b1805-127">Or use a wild card to exclude a set of files such as all backup files</span></span>

```xml
<files>
    <file src="tools\*.*" target="tools" exclude="*.bak" />
</files>
```

### <a name="removing-packages-using-the-dialog-prompts-to-remove-dependencies"></a><span data-ttu-id="b1805-128">종속성을 제거 하 라는 메시지를 표시 대화 상자를 사용 하 여 패키지를 제거 합니다.</span><span class="sxs-lookup"><span data-stu-id="b1805-128">Removing packages using the dialog prompts to remove dependencies</span></span>
<span data-ttu-id="b1805-129">NuGet 프롬프트 종속성을 사용 하 여 패키지를 제거할 때 해당 패키지와 함께 패키지의 종속성을 제거 하 고 허용 합니다.</span><span class="sxs-lookup"><span data-stu-id="b1805-129">When uninstalling a package with dependencies, NuGet prompts, allowing the removal of a package's dependencies along with the package.</span></span>

![종속 패키지를 제거합니다.](./media/remove-dependent-packages.png)


### <a name="get-package-command-improvement"></a><span data-ttu-id="b1805-131">`Get-Package`명령 개선</span><span class="sxs-lookup"><span data-stu-id="b1805-131">`Get-Package` command improvement</span></span>
<span data-ttu-id="b1805-132">`Get-Package` 명령에서는 이제는 `-ProjectName` 매개 변수입니다.</span><span class="sxs-lookup"><span data-stu-id="b1805-132">The `Get-Package` command now supports a `-ProjectName` parameter.</span></span> <span data-ttu-id="b1805-133">따라서 명령</span><span class="sxs-lookup"><span data-stu-id="b1805-133">So the command</span></span>

    Get-Package –ProjectName A

<span data-ttu-id="b1805-134">1. 프로젝트에 설치 된 모든 패키지를 나열 합니다.</span><span class="sxs-lookup"><span data-stu-id="b1805-134">will list all packages installed in project A.</span></span>

### <a name="support-for-proxies-that-require-authentication"></a><span data-ttu-id="b1805-135">인증이 필요한 프록시에 대 한 지원</span><span class="sxs-lookup"><span data-stu-id="b1805-135">Support for Proxies that require authentication</span></span>
<span data-ttu-id="b1805-136">NuGet을 사용 하 여 인증이 필요한 프록시 뒤, 프록시 자격 증명에 대 한 NuGet 이제 묻습니다.</span><span class="sxs-lookup"><span data-stu-id="b1805-136">When using NuGet behind a proxy that requires authentication, NuGet will now prompt for proxy credentials.</span></span> <span data-ttu-id="b1805-137">자격 증명을 입력 NuGet을 원격 저장소에 연결할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="b1805-137">Entering credentials allows NuGet to connect to the remote repository.</span></span>

### <a name="support-for-repositories-that-require-authentication"></a><span data-ttu-id="b1805-138">인증을 요구 하는 저장소에 대 한 지원</span><span class="sxs-lookup"><span data-stu-id="b1805-138">Support for Repositories that require authentication</span></span>
<span data-ttu-id="b1805-139">NuGet 연결을 이제 지원 [개인 저장소](../hosting-packages/local-feeds.md) 기본 또는 NTLM 인증을 해야 하는 합니다.</span><span class="sxs-lookup"><span data-stu-id="b1805-139">NuGet now supports connecting to [private repositories](../hosting-packages/local-feeds.md) that require basic or NTLM authentication.</span></span>

<span data-ttu-id="b1805-140">이후 릴리스에서 다이제스트 인증에 대 한 지원이 추가 됩니다.</span><span class="sxs-lookup"><span data-stu-id="b1805-140">Support for Digest authentication will be added in a future release.</span></span>

### <a name="performance-improvements-to-the-nugetorg-repository"></a><span data-ttu-id="b1805-141">Nuget.org 리포지토리에 성능 향상</span><span class="sxs-lookup"><span data-stu-id="b1805-141">Performance improvements to the nuget.org repository</span></span>
<span data-ttu-id="b1805-142">패키지를 나열 하 고 더 빠르게 검색할 수 있도록 nuget.org 갤러리에 몇 가지 성능 개선 되었습니다.</span><span class="sxs-lookup"><span data-stu-id="b1805-142">We've made several performance improvements to the nuget.org gallery to make package listing and searching faster.</span></span>

### <a name="solution-dialog-project-filtering"></a><span data-ttu-id="b1805-143">솔루션 프로젝트 필터링 대화 상자</span><span class="sxs-lookup"><span data-stu-id="b1805-143">Solution dialog project filtering</span></span>
<span data-ttu-id="b1805-144">솔루션 수준 대화 상자에서 설치 하려면 프로젝트에 대 한 메시지를 표시 하는 경우, 선택 된 패키지와 호환 되는 프로젝트만 보여줍니다.</span><span class="sxs-lookup"><span data-stu-id="b1805-144">In the Solution-level dialog, when prompting for what projects to install, we only show projects that are compatible with the selected package.</span></span>

### <a name="package-release-notes"></a><span data-ttu-id="b1805-145">패키지 릴리스 정보</span><span class="sxs-lookup"><span data-stu-id="b1805-145">Package Release Notes</span></span>
<span data-ttu-id="b1805-146">NuGet 패키지에는 이제 릴리스 정보에 대 한 지원이 포함 됩니다.</span><span class="sxs-lookup"><span data-stu-id="b1805-146">NuGet packages now include support for release notes.</span></span> <span data-ttu-id="b1805-147">이 릴리스 정보에 표시를 볼 때 _업데이트_ 는 패키지에 대 한 하므로 바람직하지 않습니다 첫 번째 릴리스에서 추가 합니다.</span><span class="sxs-lookup"><span data-stu-id="b1805-147">The release notes only show up when viewing _Updates_ for a package, so it doesn't make sense to add them to your first release.</span></span>

![업데이트 탭 내에서 릴리스 정보](./media/manage-nuget-packages-release-notes.png)

<span data-ttu-id="b1805-149">릴리스 정보에는 패키지를 추가 하려면 사용 하 여 새 `<releaseNotes />` NuSpec 파일에서 메타 데이터 요소입니다.</span><span class="sxs-lookup"><span data-stu-id="b1805-149">To add release notes to a package, use the new `<releaseNotes />` metadata element in your NuSpec file.</span></span>

### <a name="nuspec-ltfiles-gt-improvement"></a><span data-ttu-id="b1805-150">.nuspec & ltfiles /&gt; 개선</span><span class="sxs-lookup"><span data-stu-id="b1805-150">.nuspec &ltfiles /&gt; improvement</span></span>
<span data-ttu-id="b1805-151">`.nuspec` 파일 이제을 사용 하면 빈 `<files />` nuget.exe를 패키지의 모든 파일을 포함 하지 않도록 지시 하는 요소입니다.</span><span class="sxs-lookup"><span data-stu-id="b1805-151">The `.nuspec` file now allows empty `<files />` element, which tells nuget.exe not to include any file in the package.</span></span>

## <a name="bug-fixes"></a><span data-ttu-id="b1805-152">버그 수정</span><span class="sxs-lookup"><span data-stu-id="b1805-152">Bug Fixes</span></span>
<span data-ttu-id="b1805-153">NuGet 1.5 107의 총 작업 항목을 고정 했습니다.</span><span class="sxs-lookup"><span data-stu-id="b1805-153">NuGet 1.5 had a total of 107 work items fixed.</span></span> <span data-ttu-id="b1805-154">그 중 103 버그로 표시 되었습니다.</span><span class="sxs-lookup"><span data-stu-id="b1805-154">103 of those were marked as bugs.</span></span>

<span data-ttu-id="b1805-155">작업의 전체 목록은 항목에서에서 수정 된 NuGet 1.5 하십시오 보기는 [이 릴리스에 대 한 NuGet 문제 추적기](http://nuget.codeplex.com/workitem/list/advanced?keyword=&status=All&type=All&priority=All&release=NuGet%201.5&assignedTo=All&component=All&sortField=Summary&sortDirection=Descending&page=0)합니다.</span><span class="sxs-lookup"><span data-stu-id="b1805-155">For a full list of work items fixed in NuGet 1.5, please view the [NuGet Issue Tracker for this release](http://nuget.codeplex.com/workitem/list/advanced?keyword=&status=All&type=All&priority=All&release=NuGet%201.5&assignedTo=All&component=All&sortField=Summary&sortDirection=Descending&page=0).</span></span>

## <a name="bug-fixes-worth-noting"></a><span data-ttu-id="b1805-156">주목할 만한 버그가 수정 되었습니다.</span><span class="sxs-lookup"><span data-stu-id="b1805-156">Bug fixes worth noting:</span></span>

* <span data-ttu-id="b1805-157">[문제 1273](http://nuget.codeplex.com/workitem/1273): 만든 `packages.config` 패키지를 사전순으로 정렬 하 고 추가 공백을 제거 하 여 친숙 한 버전 제어를 강화 합니다.</span><span class="sxs-lookup"><span data-stu-id="b1805-157">[Issue 1273](http://nuget.codeplex.com/workitem/1273): Made `packages.config` more version control friendly by sorting packages alphabetically and removing extra whitespace.</span></span>
* <span data-ttu-id="b1805-158">[문제 844](http://nuget.codeplex.com/workitem/844): 버전 번호를 표준화 이제 있도록 `Install-Package 1.0` 버전을 사용 하 여 패키지에서 작동 하는 `1.0.0`합니다.</span><span class="sxs-lookup"><span data-stu-id="b1805-158">[Issue 844](http://nuget.codeplex.com/workitem/844): Version numbers are now normalized so that `Install-Package 1.0` works on a package with the version `1.0.0`.</span></span>
* <span data-ttu-id="b1805-159">[문제 1060](http://nuget.codeplex.com/workitem/1060): nuget.exe를 사용 하 여 패키지를 만들 때의 `-Version` 재정의 플래그는 `<version />` 요소입니다.</span><span class="sxs-lookup"><span data-stu-id="b1805-159">[Issue 1060](http://nuget.codeplex.com/workitem/1060): When creating a package using nuget.exe, the `-Version` flag overrides the `<version />` element.</span></span>
