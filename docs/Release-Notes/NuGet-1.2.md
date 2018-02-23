---
title: "NuGet 1.2 릴리스 정보 | Microsoft Docs"
author: karann-msft
ms.author: karann-msft
manager: ghogen
ms.date: 11/11/2016
ms.topic: article
ms.prod: nuget
ms.technology: 
description: "알려진된 문제, 버그 수정, 추가 된 기능 및 Dcr를 포함 하 여 NuGet 1.2에 대 한 릴리스 정보입니다."
keywords: "NuGet 1.2 릴리스 정보, 버그 수정, 알려진 문제, 추가 기능을 Dcr"
ms.reviewer:
- karann-msft
- unniravindranathan
ms.openlocfilehash: 9c8fff67eb61ab673eb62113e0cc46c0868be237
ms.sourcegitcommit: 7969f6cd94eccfee5b62031bb404422139ccc383
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 02/20/2018
---
# <a name="nuget-12-release-notes"></a><span data-ttu-id="1e5ec-104">NuGet 1.2 릴리스 정보</span><span class="sxs-lookup"><span data-stu-id="1e5ec-104">NuGet 1.2 Release Notes</span></span>

<span data-ttu-id="1e5ec-105">[NuGet 1.0 및 1.1 릴리스 정보](../release-notes/nuget-1.1.md) | [NuGet 1.3 릴리스 정보](../release-notes/nuget-1.3.md)</span><span class="sxs-lookup"><span data-stu-id="1e5ec-105">[NuGet 1.0 and 1.1 Release Notes](../release-notes/nuget-1.1.md) | [NuGet 1.3 Release Notes](../release-notes/nuget-1.3.md)</span></span>

<span data-ttu-id="1e5ec-106">NuGet 1.2 2011 년 3 월 30 일에 출시 되었습니다.</span><span class="sxs-lookup"><span data-stu-id="1e5ec-106">NuGet 1.2 was released on March 30, 2011.</span></span>

## <a name="new-features"></a><span data-ttu-id="1e5ec-107">새 기능</span><span class="sxs-lookup"><span data-stu-id="1e5ec-107">New Features</span></span>

### <a name="framework-profile-support"></a><span data-ttu-id="1e5ec-108">프레임 워크 프로필 지원</span><span class="sxs-lookup"><span data-stu-id="1e5ec-108">Framework Profile Support</span></span>

<span data-ttu-id="1e5ec-109">처음부터 NuGet 지원 해 다른 프레임 워크를 대상 하는 라이브러리입니다.</span><span class="sxs-lookup"><span data-stu-id="1e5ec-109">From the start, NuGet supported having libraries target different frameworks.</span></span> <span data-ttu-id="1e5ec-110">하지만 이제 패키지는 Windows Phone 프로필 같은 특정 프로필을 대상으로 하는 어셈블리를 포함 될 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="1e5ec-110">But now packages may contain assemblies that target specific profiles such as the Windows Phone profile.</span></span> <span data-ttu-id="1e5ec-111">특정 프레임 워크의 프로필을 대상으로 대시 프로필 약어에는 다음을 추가 합니다.</span><span class="sxs-lookup"><span data-stu-id="1e5ec-111">To target a specific profile of a framework, append a dash followed by the profile abbreviation.</span></span> <span data-ttu-id="1e5ec-112">예를 들어 Windows Phone (즉, Windows Phone 7)에서 실행 되는 SilverLight를 대상으로 다음 스크린샷에 표시 된 대로 sl3 wp 폴더에 어셈블리를 넣을 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="1e5ec-112">For example, to target SilverLight running on a Windows Phone (aka Windows Phone 7), you can put an assembly in the sl3-wp folder as demonstrated in the following screenshot.</span></span>

![프레임 워크 프로필 폴더 레이아웃](./media/framework-profile-support.png)

<span data-ttu-id="1e5ec-114">"Wp7" 모니커도 사용 하도록 방금 선택 하지 않은 이유를 요청할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="1e5ec-114">You might ask why we didn’t just choose to use “wp7” as the moniker.</span></span> <span data-ttu-id="1e5ec-115">부분적으로 Windows Phone 7은 최신 버전의 Silverlight 나중에 실행 될 수 있습니다, 대상으로 하는 경우에 프레임 워크 프로필에 대 한 더 정확 하 게 할 수를 예측 하는 것입니다.</span><span class="sxs-lookup"><span data-stu-id="1e5ec-115">In part, we’re anticipating that Windows Phone 7 might run a newer version of Silverlight in the future, in which case you may need to be more specific about which framework profile you’re targetting.</span></span>

### <a name="automatically-add-binding-redirects"></a><span data-ttu-id="1e5ec-116">바인딩 리디렉션을 자동으로 추가</span><span class="sxs-lookup"><span data-stu-id="1e5ec-116">Automatically Add Binding Redirects</span></span>

<span data-ttu-id="1e5ec-117">강력한 이름의 어셈블리와 패키지를 설치할 때 NuGet에 프로젝트에 필요한 바인딩 리디렉션을 컴파일하고 자동으로 추가 하려면 프로젝트에 대 한 순서 대로 구성 파일에 추가 될 경우를 이제 감지할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="1e5ec-117">When installing a package with strong named assemblies, NuGet can now detect cases where the project requires binding redirects to be added to the configuration file in order for the project to compile and add them automatically.</span></span> <span data-ttu-id="1e5ec-118">NuGet 버전 관리 권한을 부여 받은 David Ebbo 블로그 게시물 시리즈의 일부 3 "[리디렉션합니다 바인딩을 통해 통합](http://blog.davidebbo.com/2011/01/nuget-versioning-part-3-unification-via.html)"에서 자세한 내용을 보려면이 기능의 용도 설명 합니다.</span><span class="sxs-lookup"><span data-stu-id="1e5ec-118">Part 3 of David Ebbo’s blog post series on NuGet Versioning entitled “[Unification via Binding Redirects](http://blog.davidebbo.com/2011/01/nuget-versioning-part-3-unification-via.html)” covers the purpose of this feature in more details.</span></span>

<a name="framework-assembly-refs"></a>

### <a name="specifying-framework-assembly-references-gac"></a><span data-ttu-id="1e5ec-119">프레임 워크 어셈블리 참조 (GAC)를 지정합니다.</span><span class="sxs-lookup"><span data-stu-id="1e5ec-119">Specifying Framework Assembly References (GAC)</span></span>

<span data-ttu-id="1e5ec-120">경우에 따라 패키지는.NET Framework에 있는 어셈블리에 따라 달라질 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="1e5ec-120">In some cases, a package may depend on an assembly that’s in the .NET Framework.</span></span> <span data-ttu-id="1e5ec-121">엄격히 말해서, 항상 필요 없는 패키지의 소비자의 프레임 워크 어셈블리를 참조 합니다.</span><span class="sxs-lookup"><span data-stu-id="1e5ec-121">Strictly speaking, it’s not always necessary that the consumer of your package reference the framework assembly.</span></span> <span data-ttu-id="1e5ec-122">하지만 일부 경우에는 개발자가 패키지를 사용 하려면 해당 어셈블리의 형식에 대해 코딩 해야 하는 경우 같은 중요 한 쉽습니다.</span><span class="sxs-lookup"><span data-stu-id="1e5ec-122">But in some cases, it's important, such as when the developer needs to code against types in that assembly in order to use your package.</span></span> <span data-ttu-id="1e5ec-123">새 `frameworkAssemblies` 요소, 메타 데이터 요소의 자식 요소 집합을 지정할 수 있습니다 `frameworkAssembly` GAC에 프레임 워크 어셈블리를 가리키는 요소입니다.</span><span class="sxs-lookup"><span data-stu-id="1e5ec-123">The new `frameworkAssemblies` element, a child element of the metadata element, allows you to specify a set of `frameworkAssembly` elements pointing to a Framework assembly in the GAC.</span></span> <span data-ttu-id="1e5ec-124">프레임 워크 어셈블리에 중점을 두를 note 합니다.</span><span class="sxs-lookup"><span data-stu-id="1e5ec-124">Note the emphasis on Framework assembly.</span></span>
<span data-ttu-id="1e5ec-125">이러한 어셈블리.NET Framework의 일부로 모든 컴퓨터에 있는 것으로 간주 됩니다 대로 패키지에 포함 되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="1e5ec-125">These assemblies are not included in your package as they are assumed to be on every machine  as part of the .NET Framework.</span></span> <span data-ttu-id="1e5ec-126">다음 표에서 특성을 나열는 `frameworkAssembly` 요소입니다.</span><span class="sxs-lookup"><span data-stu-id="1e5ec-126">The following table lists attributes of the `frameworkAssembly` element.</span></span>


|<span data-ttu-id="1e5ec-127">특성</span><span class="sxs-lookup"><span data-stu-id="1e5ec-127">Attribute</span></span> |<span data-ttu-id="1e5ec-128">설명</span><span class="sxs-lookup"><span data-stu-id="1e5ec-128">Description</span></span>|
|----------------|-----------|
|<span data-ttu-id="1e5ec-129">**assemblyName**</span><span class="sxs-lookup"><span data-stu-id="1e5ec-129">**assemblyName**</span></span>|<span data-ttu-id="1e5ec-130">*필요한*합니다.</span><span class="sxs-lookup"><span data-stu-id="1e5ec-130">*Required*.</span></span> <span data-ttu-id="1e5ec-131">와 같은 어셈블리의 이름 `System.Net`합니다.</span><span class="sxs-lookup"><span data-stu-id="1e5ec-131">Name of the assembly such as `System.Net`.</span></span>|
|<span data-ttu-id="1e5ec-132">**targetFramework**</span><span class="sxs-lookup"><span data-stu-id="1e5ec-132">**targetFramework**</span></span>|<span data-ttu-id="1e5ec-133">*선택적*합니다.</span><span class="sxs-lookup"><span data-stu-id="1e5ec-133">*Optional*.</span></span> <span data-ttu-id="1e5ec-134">프레임 워크 및 프로필 이름 (또는 별칭)을 지정할 수 있도록 "net40" 또는 "sl4" 등이 프레임 워크 어셈블리에 적용 되는 합니다.</span><span class="sxs-lookup"><span data-stu-id="1e5ec-134">Allows specifying a framework and profile name (or alias) that this framework assembly applies to such as "net40" or "sl4".</span></span> <span data-ttu-id="1e5ec-135">에 설명 된 동일한 형식을 사용 하 여 [여러 대상 프레임 워크를 지 원하는](../create-packages/supporting-multiple-target-frameworks.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="1e5ec-135">Uses the same format described in [Supporting Multiple Target Frameworks](../create-packages/supporting-multiple-target-frameworks.md).</span></span>|

```xml
  <frameworkAssemblies>
    <frameworkAssembly assemblyName="System.ComponentModel.DataAnnotations" targetFramework="net40" />
    <frameworkAssembly assemblyName="System.ServiceModel" targetFramework="net40" />
  </frameworkAssemblies>
```

### <a name="nugetexe-now-is-able-to-store-api-key-credentials"></a><span data-ttu-id="1e5ec-136">nuget.exe 이제 API 키 자격 증명을 저장할 수는</span><span class="sxs-lookup"><span data-stu-id="1e5ec-136">nuget.exe now is able to store API Key credentials</span></span>

<span data-ttu-id="1e5ec-137">Nuget.exe 명령줄 도구를 사용할 때는 API 키를 저장할 SetApiKey 명령 이제 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="1e5ec-137">When using the nuget.exe command line tool, you can now use the SetApiKey command to store your API key.</span></span> <span data-ttu-id="1e5ec-138">이런 방식으로 패키지를 누를 때마다 지정할 필요가 없습니다.</span><span class="sxs-lookup"><span data-stu-id="1e5ec-138">That way, you won’t need to specify it every time you push a package.</span></span> <span data-ttu-id="1e5ec-139">Nuget.exe를 사용 하 여 API 키를 저장 하는 대 한 자세한 내용은 [는 패키지를 게시 하는 데에 대 한 설명서를 읽을](../create-packages/publish-a-package.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="1e5ec-139">For more details on saving your API key with nuget.exe, [read the documentation on publishing a package](../create-packages/publish-a-package.md).</span></span>

### <a name="package-explorer"></a><span data-ttu-id="1e5ec-140">패키지 탐색기</span><span class="sxs-lookup"><span data-stu-id="1e5ec-140">Package Explorer</span></span>
<span data-ttu-id="1e5ec-141">패키지 탐색기 NuGet 1.2를 지원 하도록 업데이트 되었습니다.</span><span class="sxs-lookup"><span data-stu-id="1e5ec-141">Package Explorer has been updated to support NuGet 1.2.</span></span> <span data-ttu-id="1e5ec-142">자세한 내용은 참조는 [패키지 탐색기 릴리스 정보](http://nuget.codeplex.com/wikipage?title=New%20features%20in%20NuGet%20Package%20Explorer%201.0)합니다.</span><span class="sxs-lookup"><span data-stu-id="1e5ec-142">For more information, check out the [Package Explorer release notes](http://nuget.codeplex.com/wikipage?title=New%20features%20in%20NuGet%20Package%20Explorer%201.0).</span></span>

## <a name="other-featuresfixes"></a><span data-ttu-id="1e5ec-143">다른 기능/수정</span><span class="sxs-lookup"><span data-stu-id="1e5ec-143">Other features/fixes</span></span>

<span data-ttu-id="1e5ec-144">이전 목록에서 가장 눈에 띄는 많은 기능을 구현 했습니다 및 버그를 해결 했습니다.</span><span class="sxs-lookup"><span data-stu-id="1e5ec-144">The previous list were the most noticeable of the many features we implemented and bugs we fixed.</span></span> <span data-ttu-id="1e5ec-145">무엇 보다도 구현/해결 [59 작업 항목](http://nuget.codeplex.com/workitem/list/advanced?keyword=&status=All&type=All&priority=All&release=NuGet%201.2&assignedTo=All&component=All&sortField=Votes&sortDirection=Descending&page=0) 이 릴리스에서 합니다.</span><span class="sxs-lookup"><span data-stu-id="1e5ec-145">All in all, we implemented/fixed [59 work items](http://nuget.codeplex.com/workitem/list/advanced?keyword=&status=All&type=All&priority=All&release=NuGet%201.2&assignedTo=All&component=All&sortField=Votes&sortDirection=Descending&page=0) in this release.</span></span>

## <a name="known-issues"></a><span data-ttu-id="1e5ec-146">알려진 문제</span><span class="sxs-lookup"><span data-stu-id="1e5ec-146">Known Issues</span></span>

* <span data-ttu-id="1e5ec-147">**1.2 패키지의 비 호환성**: 최신 버전의 명령줄 도구를 사용 하 여 패키지 작성, nuget.exe (> 1.2) 이전 버전의 NuGet VS에서 추가 기능 (예: 1.1)와 작동 하지 것입니다.</span><span class="sxs-lookup"><span data-stu-id="1e5ec-147">**1.2 Package incompatibility**: Packages built with the latest version of the command line tool, nuget.exe (> 1.2) will not work with older versions of the NuGet VS Add-in (such as 1.1).</span></span> <span data-ttu-id="1e5ec-148">호환 되지 않는 스키마에 대 한 정보를 나타내는 오류 메시지를 실행 하면이 오류를 실행 합니다.</span><span class="sxs-lookup"><span data-stu-id="1e5ec-148">If you run into an error message stating something about incompatible schema, you are running into this error.</span></span> <span data-ttu-id="1e5ec-149">NuGet을 최신 버전으로 업데이트 하세요.</span><span class="sxs-lookup"><span data-stu-id="1e5ec-149">Please update NuGet to the latest version.</span></span>
* <span data-ttu-id="1e5ec-150">**NuGet.Server 비 호환성**:는 내부 NuGet NuGet.Server 프로젝트를 사용 하 여 피드를 호스팅하는 경우 NuGet.Server의 최신 버전으로 해당 프로젝트를 업데이트 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="1e5ec-150">**NuGet.Server incompatibility**: If you’re hosting an internal NuGet feed using the NuGet.Server project, you’ll need to update that project with the latest version of NuGet.Server.</span></span>
* <span data-ttu-id="1e5ec-151">**서명 불일치 오류**: 서명 불일치 하는 방법에 대 한 메시지와 함께 업그레이드 하는 동안 오류가 발생 하면, NuGet를 먼저 제거한 다음 설치 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="1e5ec-151">**Signature Mismatch Error**: If you run into an error during an upgrade with a message about a Signature Mismatch, you need to uninstall NuGet first and then install it.</span></span> <span data-ttu-id="1e5ec-152">이 테이블은 표시에 우리의 [알려진 문제 페이지](../release-notes/known-issues.md) 추가 정보가 제공 됩니다.</span><span class="sxs-lookup"><span data-stu-id="1e5ec-152">This is listed in our [Known Issues page](../release-notes/known-issues.md) which provides more details.</span></span> <span data-ttu-id="1e5ec-153">문제만 Visual Studio 2010 s p 1을 실행 하는 것 미치며 잘못 서명 설치 된 NuGet 1.0이 설치 되어 있습니다.</span><span class="sxs-lookup"><span data-stu-id="1e5ec-153">The issue only affects those running Visual Studio 2010 SP1 and have a version of NuGet 1.0 installed that was incorrectly signed.</span></span> <span data-ttu-id="1e5ec-154">이 버전만으로 제공 된 CodePlex 웹 사이트에서 짧은 기간 동안이 문제에 너무 많은 사람들이 영향을 하지 않아야 합니다.</span><span class="sxs-lookup"><span data-stu-id="1e5ec-154">This version was only made available from the CodePlex website for a brief period so this issue shouldn't affect too many people.</span></span>