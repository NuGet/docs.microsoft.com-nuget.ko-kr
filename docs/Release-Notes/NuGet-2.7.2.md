---
title: "NuGet 2.7.2 릴리스 정보 | Microsoft Docs"
author: karann-msft
ms.author: karann-msft
manager: ghogen
ms.date: 11/11/2016
ms.topic: article
ms.prod: nuget
ms.technology: 
description: "NuGet 2.7.2 포함에 대 한 릴리스 정보는 문제, 버그 수정, 추가 된 기능 및 Dcr 알려져 있습니다."
keywords: "NuGet 2.7.2 릴리스 정보, 버그 수정, 알려진 문제, 추가 기능을 Dcr"
ms.reviewer:
- karann-msft
- unniravindranathan
ms.openlocfilehash: 8fe9acc3ad9c1c368fc750694ea523ac845995c5
ms.sourcegitcommit: 4651b16a3a08f6711669fc4577f5d63b600f8f58
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 02/02/2018
---
# <a name="nuget-272-release-notes"></a><span data-ttu-id="21569-104">NuGet 2.7.2 릴리스 정보</span><span class="sxs-lookup"><span data-stu-id="21569-104">NuGet 2.7.2 Release Notes</span></span>

<span data-ttu-id="21569-105">[NuGet 2.7.1 릴리스 정보](../release-notes/nuget-2.7.1.md) | [NuGet 2.8 릴리스 정보](../release-notes/nuget-2.8.md)</span><span class="sxs-lookup"><span data-stu-id="21569-105">[NuGet 2.7.1 Release Notes](../release-notes/nuget-2.7.1.md) | [NuGet 2.8 Release Notes](../release-notes/nuget-2.8.md)</span></span>

<span data-ttu-id="21569-106">2.7.2 NuGet는 2013 년 11 월 11 일에 출시 되었습니다.</span><span class="sxs-lookup"><span data-stu-id="21569-106">NuGet 2.7.2 was released on November 11, 2013.</span></span>

## <a name="noteworthy-bug-fixes-and-features"></a><span data-ttu-id="21569-107">주목할 만한 버그 수정 및 기능</span><span class="sxs-lookup"><span data-stu-id="21569-107">Noteworthy Bug Fixes and Features</span></span>

### <a name="license-text"></a><span data-ttu-id="21569-108">라이선스 텍스트</span><span class="sxs-lookup"><span data-stu-id="21569-108">License Text</span></span>
<span data-ttu-id="21569-109">상당한 기간 동안 Microsoft가 Visual Studio에서 웹 응용 프로그램 프로젝트에 대 한 기본 서식 파일의 일부로 여러 개의 인기 있는 오픈 소스 라이브러리에 대 한 NuGet 패키지를 포함 합니다.</span><span class="sxs-lookup"><span data-stu-id="21569-109">For quite some time, Microsoft has included the NuGet packages for several popular open-source libraries as a part of the default templates for Web application projects in Visual Studio.</span></span> <span data-ttu-id="21569-110">jQuery는 라이브러리에이 유형의 잘 알려진 예 때문일 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="21569-110">jQuery is probably the most well-known example of this type of library.</span></span> <span data-ttu-id="21569-111">제품을 함께 배달 되는 구성 요소와 관련 된 지원 계약으로 인해 패키지의 스크립트 파일이 동일한 패키지에는 공용 nuget.org 갤러리에서 확인할 스크립트 파일 보다 다른 라이선스 텍스트를 포함 합니다.</span><span class="sxs-lookup"><span data-stu-id="21569-111">Because of the support agreement associated with components that are delivered along with a product, the package's script file contains different license text than the script file found in the same package on the public nuget.org gallery.</span></span> <span data-ttu-id="21569-112">이러한 차이 텍스트에이 따라 다양 한 콘텐츠 해시 값을 스크립트 파일을 일으키는 다른 라이선스 텍스트 블록의 결과에서 패키지 업데이트를 방지할 수 (및 따라서 형태로 처리 되는 프로젝트 내에서 수정).</span><span class="sxs-lookup"><span data-stu-id="21569-112">This difference in text can prevent package updates from proceeding as a result of the different license text blocks causing the script files to have different content hash values (and therefore to be treated as modified within the project).</span></span>

<span data-ttu-id="21569-113">이 문제를 해결 하려면 NuGet 2.7.2 다음과 같이 표시 되는 특별히 표시 된 섹션 내에서 라이선스 텍스트 블록을 포함 하도록 스크립트 작성자를 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="21569-113">To mitigate this issue, NuGet 2.7.2 allows the script author to include the license text block within a specially marked section which looks as follows.</span></span>

    /************** NUGET: BEGIN LICENSE TEXT **************
     * The following code is licensed under the MIT license
     * Additional license information below is informational
     * only.
     ************** NUGET: END LICENSE TEXT ***************/

<span data-ttu-id="21569-114">패키지 내용으로 업데이트할 때이 블록을 포함 하는 파일 NuGet 않습니다 하지 블록의 내용을에 NuGet 갤러리에 있는 버전으로 비교 하 고 수 따라서 삭제 모아 놓은 원래 복사본 일치 인 것 처럼 콘텐츠 파일을 업데이트 합니다.</span><span class="sxs-lookup"><span data-stu-id="21569-114">When updating packages with content files containing this block, NuGet does not factor the contents of the block into the comparison with the version on the NuGet gallery, and can therefore delete and update the content file as though it matches the original copy.</span></span>

<span data-ttu-id="21569-115">이 블록은 텍스트 "NUGET:: BEGIN 라이선스 텍스트" 및 "NUGET:: 라이선스 텍스트 끝" 시작 부분에서 아무 곳 이나 발생 및 줄 끝으로 식별 됩니다.</span><span class="sxs-lookup"><span data-stu-id="21569-115">This block is identified by the text "NUGET: BEGIN LICENSE TEXT" and "NUGET: END LICENSE TEXT" occurring anywhere on the beginning and ending lines.</span></span>  <span data-ttu-id="21569-116">이 기능을 모든 종류의 언어에 관계 없이 텍스트 파일에 사용할 수 있도록 다른 서식 요구 존재 합니다.</span><span class="sxs-lookup"><span data-stu-id="21569-116">No other formatting requirements exist, allowing this feature to be used in any type of text file regardless of language.</span></span>

### <a name="add-binding-redirects-for-non-framework-assemblies"></a><span data-ttu-id="21569-117">프레임 워크 아닌 어셈블리에 대 한 바인딩 리디렉션을 추가합니다</span><span class="sxs-lookup"><span data-stu-id="21569-117">Add Binding Redirects for non-Framework Assemblies</span></span>
<span data-ttu-id="21569-118">어셈블리의.NET Framework의 일부인 경우 NuGet 패키지를 업데이트할 때 응용 프로그램의 구성 파일에 바인딩 리디렉션을 추가 건너뜁니다.</span><span class="sxs-lookup"><span data-stu-id="21569-118">For assemblies that are part of the .NET Framework, NuGet skips adding binding redirects into the application's configuration file when updating the package.</span></span> <span data-ttu-id="21569-119">이 수정 프로그램에서는 표현의 바인딩 리디렉션을 추가 되지 않았습니다 되 고 일부 어셈블리에 대 한 이러한 어셈블리 하지 않더라도 NuGet 2.7에서의 문제 재발에.NET Framework의 일부분으로 간주 합니다.</span><span class="sxs-lookup"><span data-stu-id="21569-119">This fix addresses a regression in NuGet 2.7 whereby binding redirects were not being added for some assemblies, even though those assemblies are not considered a part of the .NET Framework.</span></span> <span data-ttu-id="21569-120">NuGet 2.7.2 이전 NuGet 2.5 및 2.6 동작을 복원 하 고 바인딩 리디렉션을 추가 합니다.</span><span class="sxs-lookup"><span data-stu-id="21569-120">NuGet 2.7.2 restores the previous NuGet 2.5 and 2.6 behavior and adds the binding redirects.</span></span>

### <a name="installing-portable-libraries-with-xamarin-tools-installed"></a><span data-ttu-id="21569-121">Xamarin 도구가 설치 된 휴대용 라이브러리 설치</span><span class="sxs-lookup"><span data-stu-id="21569-121">Installing portable libraries with Xamarin Tools installed</span></span>
<span data-ttu-id="21569-122">Xamarin 개발 도구는 컴퓨터에 설치 되 면 기존 대상 프레임 워크 조합 및 Xamarin 프레임 워크 간의 호환성을 지정 하려면 지원 되는 프레임 워크 구성 데이터 수정 합니다.</span><span class="sxs-lookup"><span data-stu-id="21569-122">When Xamarin's development tools are installed on a machine, they modify the supported frameworks configuration data to specify compatibility between existing target framework combinations and Xamarin frameworks.</span></span> <span data-ttu-id="21569-123">2.7.2 버전으로 NuGet은 이러한 암시적 호환성 규칙을 알고 이제 있으며 따라서 쉽게 패키지에 따라서 Xamarin 호환 되는 하지만 명시적으로 표시 하는 이식 가능한 라이브러리를 설치 하려면 Xamarin 플랫폼을 대상으로 하는 개발자를 위한 자체 메타 데이터입니다.</span><span class="sxs-lookup"><span data-stu-id="21569-123">With version 2.7.2, NuGet is now aware of these implicit compatibility rules, and therefore makes it easy for developers targeting Xamarin platforms to install portable libraries that are Xamarin-compatible but not explicitly marked as such in the package metadata itself.</span></span>

### <a name="machine-wide-configuration-settings-honored"></a><span data-ttu-id="21569-124">시스템 수준의 구성 설정 적용</span><span class="sxs-lookup"><span data-stu-id="21569-124">Machine-wide configuration settings honored</span></span>
<span data-ttu-id="21569-125">Nuget.Config 파일 계층을 사용할 경우 repositoryPath 키 적용 되지 않은 것 되 고 솔루션의 루트에 가장 가까운 Nuget.Config 파일에 대 한 합니다.</span><span class="sxs-lookup"><span data-stu-id="21569-125">When using hierarchical Nuget.Config files, the repositoryPath key was not being honored for Nuget.Config files closest to the solution root.</span></span> <span data-ttu-id="21569-126">Visual Studio 2013에서 NuGet "Microsoft 및.NET" 패키지 소스를 추가 하기 위해 %ProgramData%\NuGet\Config\VisualStudio\12.0\Microsoft.VisualStudio.config에 사용자 지정 Nuget.Config 파일을 설치 합니다.</span><span class="sxs-lookup"><span data-stu-id="21569-126">In Visual Studio 2013, NuGet installs a custom Nuget.Config file at %ProgramData%\NuGet\Config\VisualStudio\12.0\Microsoft.VisualStudio.config in order to add the "Microsoft and .NET" package source.</span></span> <span data-ttu-id="21569-127">결과적으로, 해결 하는 솔루션에서 사용자 지정 repositoryPath 사용에 대 한도 제거 하는 "Microsoft 및.NET" 패키지 소스를 의미 하는 컴퓨터 수준 Nuget.Config-삭제할 했습니다.</span><span class="sxs-lookup"><span data-stu-id="21569-127">As a result, the work-around for using a custom repositoryPath in a solution was to delete the machine-level Nuget.Config - which also meant removing the "Microsoft and .NET" package source.</span></span> <span data-ttu-id="21569-128">Nuget.Config 파일 계층 구조를 사용 하는 경우 NuGet 2.7.2 이제 repositoryPath에 대 한 우선 순위 규칙을 준수 합니다.</span><span class="sxs-lookup"><span data-stu-id="21569-128">NuGet 2.7.2 now honors the precedence rules for repositoryPath when using hierarchical Nuget.Config files.</span></span>

## <a name="all-changes"></a><span data-ttu-id="21569-129">모든 변경 내용</span><span class="sxs-lookup"><span data-stu-id="21569-129">All Changes</span></span>
<span data-ttu-id="21569-130">작업의 전체 목록은 항목에서에서 수정 된 NuGet 2.7.2, 하십시오 보기는 [이 릴리스에 대 한 NuGet 문제 추적기](https://nuget.codeplex.com/workitem/list/advanced?keyword=&status=All&type=All&priority=All&release=NuGet%202.7.2&assignedTo=All&component=All&sortField=LastUpdatedDate&sortDirection=Descending&page=0&reasonClosed=Fixed)합니다.</span><span class="sxs-lookup"><span data-stu-id="21569-130">For a full list of work items fixed in NuGet 2.7.2, please view the [NuGet Issue Tracker for this release](https://nuget.codeplex.com/workitem/list/advanced?keyword=&status=All&type=All&priority=All&release=NuGet%202.7.2&assignedTo=All&component=All&sortField=LastUpdatedDate&sortDirection=Descending&page=0&reasonClosed=Fixed).</span></span>
