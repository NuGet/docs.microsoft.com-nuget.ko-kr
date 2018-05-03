---
title: NuGet 1.3 릴리스 정보
description: 알려진된 문제, 버그 수정, 추가 된 기능 및 Dcr를 포함 하 여 NuGet 1.3에 대 한 릴리스 정보입니다.
author: karann-msft
ms.author: karann
manager: unnir
ms.date: 11/11/2016
ms.topic: conceptual
ms.openlocfilehash: c0284fe0afb11bf6465897132cccd160674ea3e1
ms.sourcegitcommit: 3eab9c4dd41ea7ccd2c28bb5ab16f6fbbec13708
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/26/2018
---
# <a name="nuget-13-release-notes"></a><span data-ttu-id="4a924-103">NuGet 1.3 릴리스 정보</span><span class="sxs-lookup"><span data-stu-id="4a924-103">NuGet 1.3 Release Notes</span></span>

<span data-ttu-id="4a924-104">[NuGet 1.2 릴리스 정보](../release-notes/nuget-1.2.md) | [NuGet 1.4 릴리스 정보](../release-notes/nuget-1.4.md)</span><span class="sxs-lookup"><span data-stu-id="4a924-104">[NuGet 1.2 Release Notes](../release-notes/nuget-1.2.md) | [NuGet 1.4 Release Notes](../release-notes/nuget-1.4.md)</span></span>

<span data-ttu-id="4a924-105">NuGet 1.3 2011 년 4 월 25 일에 출시 되었습니다.</span><span class="sxs-lookup"><span data-stu-id="4a924-105">NuGet 1.3 was released on April 25, 2011.</span></span>

## <a name="new-features"></a><span data-ttu-id="4a924-106">새 기능</span><span class="sxs-lookup"><span data-stu-id="4a924-106">New Features</span></span>

### <a name="streamlined-package-creation-with-symbol-server-integration"></a><span data-ttu-id="4a924-107">기호 서버 통합 된 간편한 패키지 만들기</span><span class="sxs-lookup"><span data-stu-id="4a924-107">Streamlined Package Creation with symbol server integration</span></span>

<span data-ttu-id="4a924-108">NuGet 팀에서 협력 [SymbolSource.org](http://www.symbolsource.org/) 원본과 PDB의 패키지와 함께 게시 하는 매우 간단한 방법을 제공 합니다.</span><span class="sxs-lookup"><span data-stu-id="4a924-108">The NuGet team partnered with the folks at [SymbolSource.org](http://www.symbolsource.org/) to offer a really simple way of publishing your sources and PDB’s along with your package.</span></span> <span data-ttu-id="4a924-109">그러면 디버거에서 패키지에 대 한 소스 한 단계씩 패키지의 소비자가 있습니다.</span><span class="sxs-lookup"><span data-stu-id="4a924-109">This allows consumers of your package to step into the source for your package in the debugger.</span></span> <span data-ttu-id="4a924-110">자세한 내용은 참조 하세요 [만들기 및 게시 기호 패키지](../create-packages/symbol-packages.md) 소스와 NuGet 패키지를 게시 하는 쉬운 방법입니다.</span><span class="sxs-lookup"><span data-stu-id="4a924-110">For more details, read [Creating and Publishing a Symbol Package](../create-packages/symbol-packages.md) The easy way to publish NuGet packages with sources.</span></span> <span data-ttu-id="4a924-111">라이브 데모는이 기능의 심층에서 NuGet의 일부로 Mix11에 통신도 볼 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="4a924-111">You can also watch a live demonstration of this feature as part of the NuGet in Depth talk at Mix11.</span></span> <span data-ttu-id="4a924-112">이 기능을 완벽 하 게 비디오의 20 분 지점부터 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="4a924-112">This feature is fully demonstrated starting at the 20 minute mark of the video.</span></span>

### <a name="open-packagepage-command"></a><span data-ttu-id="4a924-113">`Open-PackagePage` 명령</span><span class="sxs-lookup"><span data-stu-id="4a924-113">`Open-PackagePage` Command</span></span>

<span data-ttu-id="4a924-114">이 명령을 사용 하면 쉽게 패키지 관리자 콘솔 내에서 패키지에 대 한 프로젝트 페이지에 액세스할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="4a924-114">This command makes it easy to get to the project page for a package from within the Package Manager Console.</span></span> <span data-ttu-id="4a924-115">또한 라이선스 URL 및 패키지에 대 한 보고서 남용 페이지를 열려면 옵션을 제공 합니다.</span><span class="sxs-lookup"><span data-stu-id="4a924-115">It also provides options to open the license URL and the report abuse page for the package.</span></span>
<span data-ttu-id="4a924-116">명령 구문은 다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="4a924-116">The syntax for the command is:</span></span>

    Open-PackagePage -Id <string> [-Version] [-Source] [-License] [-ReportAbuse] [-PassThru]

<span data-ttu-id="4a924-117">`-PassThru` 옵션이 지정된 된 URL의 값을 반환 하는 데 사용 됩니다.</span><span class="sxs-lookup"><span data-stu-id="4a924-117">The `-PassThru` option is used to return the value of the specified URL.</span></span>

<span data-ttu-id="4a924-118">예를 들면 다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="4a924-118">Examples:</span></span>

    PM> Open-PackagePage Ninject

<span data-ttu-id="4a924-119">Ninject 패키지에 지정 된 프로젝트 URL로 브라우저를 엽니다.</span><span class="sxs-lookup"><span data-stu-id="4a924-119">Opens a browser to the project URL specified in the Ninject package.</span></span>

    PM> Open-PackagePage Ninject -License

<span data-ttu-id="4a924-120">Ninject 패키지에 지정 된 라이선스 URL에 대 한 브라우저를 엽니다.</span><span class="sxs-lookup"><span data-stu-id="4a924-120">Opens a browser to the license URL specified in the Ninject package.</span></span>

    PM> Open-PackagePage Ninject -ReportAbuse

<span data-ttu-id="4a924-121">지정된 된 패키지에 대 한 신고 하는 데 사용 되는 현재 패키지 소스에서 URL로 브라우저를 엽니다.</span><span class="sxs-lookup"><span data-stu-id="4a924-121">Opens a browser to the URL at the current package source used to report abuse for the specified package.</span></span>

    PM> $url = Open-PackagePage Ninject -License -WhatIf -PassThru

<span data-ttu-id="4a924-122">변수에 $url, 브라우저에서 URL을 열지 않고 라이선스 URL을 할당 합니다.</span><span class="sxs-lookup"><span data-stu-id="4a924-122">Assigns the license URL to the variable, $url, without opening the URL in a browser.</span></span>

### <a name="performance-improvements"></a><span data-ttu-id="4a924-123">성능 향상</span><span class="sxs-lookup"><span data-stu-id="4a924-123">Performance Improvements</span></span>

<span data-ttu-id="4a924-124">NuGet 1.3 많은 성능 향상을 소개합니다.</span><span class="sxs-lookup"><span data-stu-id="4a924-124">NuGet 1.3 introduces a lot of performance improvements.</span></span> <span data-ttu-id="4a924-125">NuGet 1.3 사용자 단위 로컬 캐시를 포함 하 여 동일한 버전의 패키지를 여러 번 다운로드를 방지 합니다.</span><span class="sxs-lookup"><span data-stu-id="4a924-125">NuGet 1.3 avoids downloading the same version of a package multiple times by including a local per-user cache.</span></span> <span data-ttu-id="4a924-126">캐시를 액세스 하 고 패키지 관리자 설정 대화 상자를 통해 지울 수 있습니다.:</span><span class="sxs-lookup"><span data-stu-id="4a924-126">The cache can be accessed and cleared via the Package Manager Settings dialog:</span></span>

![패키지 캐시 설정 사용 하 여 NuGet 옵션 대화 상자](./media/nuget-options.png)

<span data-ttu-id="4a924-128">기타 성능 향상 등이 HTTP 압축에 대 한 지원을 추가 하기 위한 Visual Studio 내에서 패키지 설치 속도 향상 합니다.</span><span class="sxs-lookup"><span data-stu-id="4a924-128">Other performance improvements include adding support for HTTP compression and improving the package installation speed within Visual Studio.</span></span>

### <a name="visual-studio-and-nugetexe-uses-the-same-list-of-package-sources"></a><span data-ttu-id="4a924-129">Visual Studio 및 nuget.exe 같은 패키지 소스 목록을 사용 하 여</span><span class="sxs-lookup"><span data-stu-id="4a924-129">Visual Studio and nuget.exe uses the same list of package sources</span></span>

<span data-ttu-id="4a924-130">NuGet 1.3 전에 nuget.exe와 NuGet Visual Studio 추가 기능에서 사용 하는 패키지 소스 목록 같은 위치에 저장 되지 않았습니다.</span><span class="sxs-lookup"><span data-stu-id="4a924-130">Prior to NuGet 1.3, the list of package sources used by nuget.exe and the NuGet Visual Studio Add-In were not stored in the same place.</span></span> <span data-ttu-id="4a924-131">이제 NuGet 1.3 양쪽 모두에서 동일한 목록을 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="4a924-131">NuGet 1.3 now uses the same list in both places.</span></span> <span data-ttu-id="4a924-132">목록에 저장 됩니다 `NuGet.Config` 응용 프로그램 데이터 폴더에 저장 합니다.</span><span class="sxs-lookup"><span data-stu-id="4a924-132">The list is stored in `NuGet.Config` and stored in the AppData folder.</span></span>

### <a name="nugetexe-ignores-files-and-folders-that-start-with--by-default"></a><span data-ttu-id="4a924-133">nuget.exe 무시 파일 및 폴더로 시작 하는 '.' 기본적으로</span><span class="sxs-lookup"><span data-stu-id="4a924-133">nuget.exe Ignores Files and Folders that start with '.' by default</span></span>

<span data-ttu-id="4a924-134">NuGet Subversion, Mercurial 등의 소스 제어 시스템에서 제대로 작동 하려면 nuget.exe 무시로 시작 하는 파일과 폴더는 '.' 패키지를 만들 때 문자입니다.</span><span class="sxs-lookup"><span data-stu-id="4a924-134">In order to make NuGet work well with source control systems such Subversion and Mercurial, nuget.exe ignores folders and files that start with the '.' character when creating packages.</span></span> <span data-ttu-id="4a924-135">두 개의 새로운 플래그를 사용 하 여 재정의할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="4a924-135">This can be overridden using two new flags:</span></span>

* <span data-ttu-id="4a924-136">__-NoDefaultExcludes__ 이 설정을 무시 하 고 모든 파일을 포함 하는 데 사용 됩니다.</span><span class="sxs-lookup"><span data-stu-id="4a924-136">__-NoDefaultExcludes__ is used to override this setting and include all files.</span></span>
* <span data-ttu-id="4a924-137">__-제외__ 패턴을 사용 하 여 제외할 다른 파일/폴더를 추가 하는 데 사용 됩니다.</span><span class="sxs-lookup"><span data-stu-id="4a924-137">__-Exclude__ is used to add other files/folders to exclude using a pattern.</span></span> <span data-ttu-id="4a924-138">예를 들어, '_db_' 파일 확장명을 가진 모든 파일을 제외 하려면</span><span class="sxs-lookup"><span data-stu-id="4a924-138">For example, to exclude all files with the '.bak' file extension</span></span>

```
nuget Pack MyPackage.nuspec -Exclude **\*.bak
```  

<span data-ttu-id="4a924-139">_참고: 패턴은 기본적으로 재귀적입니다._</span><span class="sxs-lookup"><span data-stu-id="4a924-139">_Note: the pattern is not recursive by default._</span></span>

### <a name="support-for-wix-projects-and-the-net-micro-framework"></a><span data-ttu-id="4a924-140">WiX 프로젝트 및.NET 마이크로 프레임 워크에 대 한 지원</span><span class="sxs-lookup"><span data-stu-id="4a924-140">Support for WiX Projects and the .NET Micro Framework</span></span>

<span data-ttu-id="4a924-141">커뮤니티 기여 덕분에 NuGet에 WiX 프로젝트 형식 뿐만 아니라.NET 마이크로 프레임 워크에 대 한 지원이 포함 됩니다.</span><span class="sxs-lookup"><span data-stu-id="4a924-141">Thanks to community contributions, NuGet includes support for WiX project types as well as the .NET Micro Framework.</span></span>

## <a name="bug-fixes"></a><span data-ttu-id="4a924-142">버그 수정</span><span class="sxs-lookup"><span data-stu-id="4a924-142">Bug Fixes</span></span>

<span data-ttu-id="4a924-143">버그 수정 사항의 전체 목록을 보십시오는 [이 릴리스에 대 한 NuGet 문제 추적기](http://nuget.codeplex.com/workitem/list/advanced?keyword=&status=All&type=All&priority=All&release=NuGet%201.3&assignedTo=All&component=All&sortField=LastUpdatedDate&sortDirection=Descending&page=0)합니다.</span><span class="sxs-lookup"><span data-stu-id="4a924-143">For a full list of bug fixes, please view the [NuGet Issue Tracker for this release](http://nuget.codeplex.com/workitem/list/advanced?keyword=&status=All&type=All&priority=All&release=NuGet%201.3&assignedTo=All&component=All&sortField=LastUpdatedDate&sortDirection=Descending&page=0).</span></span>

## <a name="bug-fixes-worth-noting"></a><span data-ttu-id="4a924-144">주목할 만한 버그 수정</span><span class="sxs-lookup"><span data-stu-id="4a924-144">Bug fixes worth noting</span></span>

* <span data-ttu-id="4a924-145">소스 파일을 사용 하 여 패키지에 두 웹 사이트 및 웹 응용 프로그램 프로젝트에서 작업합니다.</span><span class="sxs-lookup"><span data-stu-id="4a924-145">Packages with source files work in both Websites and in Web Application Projects.</span></span>
<span data-ttu-id="4a924-146">웹 사이트의 경우 소스 파일에 복사 되는 `App_Code` 폴더</span><span class="sxs-lookup"><span data-stu-id="4a924-146">For Websites, source files are copied into the `App_Code` folder</span></span>
