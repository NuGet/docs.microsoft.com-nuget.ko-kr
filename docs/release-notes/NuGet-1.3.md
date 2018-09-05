---
title: NuGet 1.3 릴리스 정보
description: 알려진된 문제, 버그 수정, 추가 된 기능 및 Dcr 포함 하 여 NuGet 1.3에 대 한 릴리스 정보입니다.
author: karann-msft
ms.author: karann
ms.date: 11/11/2016
ms.topic: conceptual
ms.openlocfilehash: fa89af100096356c2ffb4d6c501c4a34296ad0ea
ms.sourcegitcommit: 1d1406764c6af5fb7801d462e0c4afc9092fa569
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 09/04/2018
ms.locfileid: "43551353"
---
# <a name="nuget-13-release-notes"></a><span data-ttu-id="ab197-103">NuGet 1.3 릴리스 정보</span><span class="sxs-lookup"><span data-stu-id="ab197-103">NuGet 1.3 Release Notes</span></span>

<span data-ttu-id="ab197-104">[NuGet 1.2 릴리스 정보](../release-notes/nuget-1.2.md) | [NuGet 1.4 릴리스 정보](../release-notes/nuget-1.4.md)</span><span class="sxs-lookup"><span data-stu-id="ab197-104">[NuGet 1.2 Release Notes](../release-notes/nuget-1.2.md) | [NuGet 1.4 Release Notes](../release-notes/nuget-1.4.md)</span></span>

<span data-ttu-id="ab197-105">NuGet 1.3은 2011 년 4 월 25 일에 출시 되었습니다.</span><span class="sxs-lookup"><span data-stu-id="ab197-105">NuGet 1.3 was released on April 25, 2011.</span></span>

## <a name="new-features"></a><span data-ttu-id="ab197-106">새 기능</span><span class="sxs-lookup"><span data-stu-id="ab197-106">New Features</span></span>

### <a name="streamlined-package-creation-with-symbol-server-integration"></a><span data-ttu-id="ab197-107">기호 서버 통합을 사용 하 여 간소화 된 패키지 만들기</span><span class="sxs-lookup"><span data-stu-id="ab197-107">Streamlined Package Creation with symbol server integration</span></span>

<span data-ttu-id="ab197-108">NuGet 팀 들 협력 [SymbolSource.org](http://www.symbolsource.org/) 소스 및 PDB의 패키지와 함께 게시 하는 간단한 방법을 제공 합니다.</span><span class="sxs-lookup"><span data-stu-id="ab197-108">The NuGet team partnered with the folks at [SymbolSource.org](http://www.symbolsource.org/) to offer a really simple way of publishing your sources and PDB’s along with your package.</span></span> <span data-ttu-id="ab197-109">이렇게 하면 패키지의 소비자가 디버거에서 패키지 소스를 한 단계씩 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="ab197-109">This allows consumers of your package to step into the source for your package in the debugger.</span></span> <span data-ttu-id="ab197-110">자세한 내용은 참조 하세요 [기호 패키지 만들기 및 게시](../create-packages/symbol-packages.md) 쉽게 소스를 사용 하 여 NuGet 패키지를 게시 하는 방법입니다.</span><span class="sxs-lookup"><span data-stu-id="ab197-110">For more details, read [Creating and Publishing a Symbol Package](../create-packages/symbol-packages.md) The easy way to publish NuGet packages with sources.</span></span> <span data-ttu-id="ab197-111">라이브 데모가 기능의 깊이에서 NuGet의 일부로 Mix11에서 이야기를 시청할 수도 있습니다.</span><span class="sxs-lookup"><span data-stu-id="ab197-111">You can also watch a live demonstration of this feature as part of the NuGet in Depth talk at Mix11.</span></span> <span data-ttu-id="ab197-112">이 기능은 비디오의 20 분 표시에서 시작 하는 완벽 하 게 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="ab197-112">This feature is fully demonstrated starting at the 20 minute mark of the video.</span></span>

### <a name="open-packagepage-command"></a><span data-ttu-id="ab197-113">`Open-PackagePage` 명령</span><span class="sxs-lookup"><span data-stu-id="ab197-113">`Open-PackagePage` Command</span></span>

<span data-ttu-id="ab197-114">이 명령은 쉽게 패키지 관리자 콘솔 내에서 패키지에 대 한 프로젝트 페이지를 표시 합니다.</span><span class="sxs-lookup"><span data-stu-id="ab197-114">This command makes it easy to get to the project page for a package from within the Package Manager Console.</span></span> <span data-ttu-id="ab197-115">또한 라이선스 URL 및 패키지에 대 한 보고서 남용 페이지를 열려면 옵션을 제공 합니다.</span><span class="sxs-lookup"><span data-stu-id="ab197-115">It also provides options to open the license URL and the report abuse page for the package.</span></span>
<span data-ttu-id="ab197-116">명령에 대 한 구문은 다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="ab197-116">The syntax for the command is:</span></span>

    Open-PackagePage -Id <string> [-Version] [-Source] [-License] [-ReportAbuse] [-PassThru]

<span data-ttu-id="ab197-117">`-PassThru` 옵션이 지정된 된 URL의 값을 반환 하는 데 사용 됩니다.</span><span class="sxs-lookup"><span data-stu-id="ab197-117">The `-PassThru` option is used to return the value of the specified URL.</span></span>

<span data-ttu-id="ab197-118">예를 들면 다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="ab197-118">Examples:</span></span>

    PM> Open-PackagePage Ninject

<span data-ttu-id="ab197-119">Ninject 패키지에 지정 된 프로젝트 URL로 브라우저를 엽니다.</span><span class="sxs-lookup"><span data-stu-id="ab197-119">Opens a browser to the project URL specified in the Ninject package.</span></span>

    PM> Open-PackagePage Ninject -License

<span data-ttu-id="ab197-120">패키지에 지정 된 Ninject 라이선스 URL로 브라우저를 엽니다.</span><span class="sxs-lookup"><span data-stu-id="ab197-120">Opens a browser to the license URL specified in the Ninject package.</span></span>

    PM> Open-PackagePage Ninject -ReportAbuse

<span data-ttu-id="ab197-121">지정된 된 패키지에 대 한 신고 하는 데 현재 패키지 소스의 URL로 브라우저를 엽니다.</span><span class="sxs-lookup"><span data-stu-id="ab197-121">Opens a browser to the URL at the current package source used to report abuse for the specified package.</span></span>

    PM> $url = Open-PackagePage Ninject -License -WhatIf -PassThru

<span data-ttu-id="ab197-122">라이선스 URL을 브라우저에서 URL을 열지 않고 $url, 변수에 할당 합니다.</span><span class="sxs-lookup"><span data-stu-id="ab197-122">Assigns the license URL to the variable, $url, without opening the URL in a browser.</span></span>

### <a name="performance-improvements"></a><span data-ttu-id="ab197-123">성능 향상</span><span class="sxs-lookup"><span data-stu-id="ab197-123">Performance Improvements</span></span>

<span data-ttu-id="ab197-124">NuGet 1.3 많은 성능 향상을 소개합니다.</span><span class="sxs-lookup"><span data-stu-id="ab197-124">NuGet 1.3 introduces a lot of performance improvements.</span></span> <span data-ttu-id="ab197-125">NuGet 1.3 사용자 당 로컬 캐시를 포함 하 여 동일한 버전의 패키지를 여러 번 다운로드를 방지 합니다.</span><span class="sxs-lookup"><span data-stu-id="ab197-125">NuGet 1.3 avoids downloading the same version of a package multiple times by including a local per-user cache.</span></span> <span data-ttu-id="ab197-126">캐시 액세스 하 고 패키지 관리자 설정 대화 상자를 통해 지워질 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="ab197-126">The cache can be accessed and cleared via the Package Manager Settings dialog:</span></span>

![패키지 캐시 설정 사용 하 여 NuGet 옵션 대화 상자](./media/nuget-options.png)

<span data-ttu-id="ab197-128">HTTP 압축에 대 한 지원을 추가 하 고 Visual Studio 내에서 패키지 설치 속도 향상 시키는 기타 성능 향상에 포함 됩니다.</span><span class="sxs-lookup"><span data-stu-id="ab197-128">Other performance improvements include adding support for HTTP compression and improving the package installation speed within Visual Studio.</span></span>

### <a name="visual-studio-and-nugetexe-uses-the-same-list-of-package-sources"></a><span data-ttu-id="ab197-129">Visual Studio 및 nuget.exe 동일한 패키지 소스 목록을 사용 하 여</span><span class="sxs-lookup"><span data-stu-id="ab197-129">Visual Studio and nuget.exe uses the same list of package sources</span></span>

<span data-ttu-id="ab197-130">NuGet 1.3 전에 nuget.exe와 NuGet Visual Studio 추가 기능에서 사용 하는 패키지 원본의 목록 같은 위치에 저장 되지 않았습니다.</span><span class="sxs-lookup"><span data-stu-id="ab197-130">Prior to NuGet 1.3, the list of package sources used by nuget.exe and the NuGet Visual Studio Add-In were not stored in the same place.</span></span> <span data-ttu-id="ab197-131">이제 NuGet 1.3 양쪽 모두에서 동일한 목록을 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="ab197-131">NuGet 1.3 now uses the same list in both places.</span></span> <span data-ttu-id="ab197-132">목록에 저장 됩니다 `NuGet.Config` AppData 폴더에 저장 합니다.</span><span class="sxs-lookup"><span data-stu-id="ab197-132">The list is stored in `NuGet.Config` and stored in the AppData folder.</span></span>

### <a name="nugetexe-ignores-files-and-folders-that-start-with--by-default"></a><span data-ttu-id="ab197-133">nuget.exe 무시 파일 및 폴더로 시작 하는 '.' 기본적으로</span><span class="sxs-lookup"><span data-stu-id="ab197-133">nuget.exe Ignores Files and Folders that start with '.' by default</span></span>

<span data-ttu-id="ab197-134">Subversion 및 Mercurial 같은 소스 제어 시스템에서 잘 작동 하는 NuGet을 만들려면 nuget.exe 무시로 시작 하는 파일과 폴더는 '.' 패키지를 만들 때 문자입니다.</span><span class="sxs-lookup"><span data-stu-id="ab197-134">In order to make NuGet work well with source control systems such Subversion and Mercurial, nuget.exe ignores folders and files that start with the '.' character when creating packages.</span></span> <span data-ttu-id="ab197-135">이 두 개의 새 플래그를 사용 하 여 재정의할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="ab197-135">This can be overridden using two new flags:</span></span>

* <span data-ttu-id="ab197-136">__-NoDefaultExcludes__ 이 설정을 무시 하 고 모든 파일을 포함 하는 데 사용 됩니다.</span><span class="sxs-lookup"><span data-stu-id="ab197-136">__-NoDefaultExcludes__ is used to override this setting and include all files.</span></span>
* <span data-ttu-id="ab197-137">__-제외__ 패턴을 사용 하 여 제외할 다른 파일/폴더를 추가 하는 데 사용 됩니다.</span><span class="sxs-lookup"><span data-stu-id="ab197-137">__-Exclude__ is used to add other files/folders to exclude using a pattern.</span></span> <span data-ttu-id="ab197-138">예를 들어 '_db_' 파일 확장명을 가진 모든 파일을 제외 하려면</span><span class="sxs-lookup"><span data-stu-id="ab197-138">For example, to exclude all files with the '.bak' file extension</span></span>

```
nuget Pack MyPackage.nuspec -Exclude **\*.bak
```  

<span data-ttu-id="ab197-139">_참고: 패턴은 기본적으로 재귀적 아닙니다._</span><span class="sxs-lookup"><span data-stu-id="ab197-139">_Note: the pattern is not recursive by default._</span></span>

### <a name="support-for-wix-projects-and-the-net-micro-framework"></a><span data-ttu-id="ab197-140">WiX 프로젝트와.NET Micro Framework에 대 한 지원</span><span class="sxs-lookup"><span data-stu-id="ab197-140">Support for WiX Projects and the .NET Micro Framework</span></span>

<span data-ttu-id="ab197-141">커뮤니티 기여를 통해 NuGet에는.NET Micro Framework 뿐만 아니라 WiX 프로젝트 형식에 대 한 지원이 포함 됩니다.</span><span class="sxs-lookup"><span data-stu-id="ab197-141">Thanks to community contributions, NuGet includes support for WiX project types as well as the .NET Micro Framework.</span></span>

## <a name="bug-fixes"></a><span data-ttu-id="ab197-142">버그 수정</span><span class="sxs-lookup"><span data-stu-id="ab197-142">Bug Fixes</span></span>

<span data-ttu-id="ab197-143">버그 수정 사항의 전체 목록을 참조 하십시오 합니다 [이 릴리스의 NuGet 문제 추적기](http://nuget.codeplex.com/workitem/list/advanced?keyword=&status=All&type=All&priority=All&release=NuGet%201.3&assignedTo=All&component=All&sortField=LastUpdatedDate&sortDirection=Descending&page=0)합니다.</span><span class="sxs-lookup"><span data-stu-id="ab197-143">For a full list of bug fixes, please view the [NuGet Issue Tracker for this release](http://nuget.codeplex.com/workitem/list/advanced?keyword=&status=All&type=All&priority=All&release=NuGet%201.3&assignedTo=All&component=All&sortField=LastUpdatedDate&sortDirection=Descending&page=0).</span></span>

## <a name="bug-fixes-worth-noting"></a><span data-ttu-id="ab197-144">주목할 만한 버그 수정</span><span class="sxs-lookup"><span data-stu-id="ab197-144">Bug fixes worth noting</span></span>

* <span data-ttu-id="ab197-145">소스 파일을 사용 하 여 패키지에는 두 웹 사이트에 웹 응용 프로그램 프로젝트에서 작동합니다.</span><span class="sxs-lookup"><span data-stu-id="ab197-145">Packages with source files work in both Websites and in Web Application Projects.</span></span>
<span data-ttu-id="ab197-146">웹 사이트에 대 한 소스 파일에 복사 됩니다는 `App_Code` 폴더</span><span class="sxs-lookup"><span data-stu-id="ab197-146">For Websites, source files are copied into the `App_Code` folder</span></span>
