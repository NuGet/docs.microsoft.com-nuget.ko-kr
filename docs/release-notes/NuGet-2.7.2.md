---
title: NuGet 2.7.2 릴리스 정보
description: 알려진 문제, 버그 수정, 추가 된 기능 및 2.7.2를 포함 하는 NuGet에 대 한 릴리스 정보입니다.
author: JonDouglas
ms.author: jodou
ms.date: 11/11/2016
ms.topic: conceptual
ms.openlocfilehash: 7643bf930bca39684eb626fe737001bc3e3ea769
ms.sourcegitcommit: ee6c3f203648a5561c809db54ebeb1d0f0598b68
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 01/26/2021
ms.locfileid: "98776775"
---
# <a name="nuget-272-release-notes"></a><span data-ttu-id="1c6c4-103">NuGet 2.7.2 릴리스 정보</span><span class="sxs-lookup"><span data-stu-id="1c6c4-103">NuGet 2.7.2 Release Notes</span></span>

<span data-ttu-id="1c6c4-104">[NuGet 2.7.1 릴리스 정보](../release-notes/nuget-2.7.1.md)  |  [NuGet 2.8 릴리스 정보](../release-notes/nuget-2.8.md)</span><span class="sxs-lookup"><span data-stu-id="1c6c4-104">[NuGet 2.7.1 Release Notes](../release-notes/nuget-2.7.1.md) | [NuGet 2.8 Release Notes](../release-notes/nuget-2.8.md)</span></span>

<span data-ttu-id="1c6c4-105">NuGet 2.7.2는 2013 년 11 월 11 일에 출시 되었습니다.</span><span class="sxs-lookup"><span data-stu-id="1c6c4-105">NuGet 2.7.2 was released on November 11, 2013.</span></span>

## <a name="noteworthy-bug-fixes-and-features"></a><span data-ttu-id="1c6c4-106">주목할 만한 버그 수정 및 기능</span><span class="sxs-lookup"><span data-stu-id="1c6c4-106">Noteworthy Bug Fixes and Features</span></span>

### <a name="license-text"></a><span data-ttu-id="1c6c4-107">라이선스 텍스트</span><span class="sxs-lookup"><span data-stu-id="1c6c4-107">License Text</span></span>
<span data-ttu-id="1c6c4-108">Microsoft는 상당한 시간 동안 널리 사용 되는 여러 오픈 소스 라이브러리에 대 한 NuGet 패키지를 Visual Studio의 웹 응용 프로그램 프로젝트에 대 한 기본 템플릿의 일부로 포함 했습니다.</span><span class="sxs-lookup"><span data-stu-id="1c6c4-108">For quite some time, Microsoft has included the NuGet packages for several popular open-source libraries as a part of the default templates for Web application projects in Visual Studio.</span></span> <span data-ttu-id="1c6c4-109">jQuery는 이러한 라이브러리 유형의 가장 잘 알려진 예입니다.</span><span class="sxs-lookup"><span data-stu-id="1c6c4-109">jQuery is probably the most well-known example of this type of library.</span></span> <span data-ttu-id="1c6c4-110">제품과 함께 제공 되는 구성 요소와 관련 된 지원 계약 때문에 패키지의 스크립트 파일에는 공용 nuget.org 갤러리의 동일한 패키지에 있는 스크립트 파일과 다른 라이선스 텍스트가 포함 됩니다.</span><span class="sxs-lookup"><span data-stu-id="1c6c4-110">Because of the support agreement associated with components that are delivered along with a product, the package's script file contains different license text than the script file found in the same package on the public nuget.org gallery.</span></span> <span data-ttu-id="1c6c4-111">이러한 텍스트의 차이로 인해 패키지 업데이트가 다른 라이선스 텍스트 블록의 결과로 진행 되는 것을 방지할 수 있습니다 .이로 인해 스크립트 파일에 다른 콘텐츠 해시 값이 있으므로 프로젝트 내에서 수정 된 것으로 처리 됩니다.</span><span class="sxs-lookup"><span data-stu-id="1c6c4-111">This difference in text can prevent package updates from proceeding as a result of the different license text blocks causing the script files to have different content hash values (and therefore to be treated as modified within the project).</span></span>

<span data-ttu-id="1c6c4-112">이 문제를 완화 하기 위해 NuGet 2.7.2는 스크립트 작성자가 다음과 같이 특수 하 게 표시 된 섹션 내에 라이선스 텍스트 블록을 포함할 수 있도록 허용 합니다.</span><span class="sxs-lookup"><span data-stu-id="1c6c4-112">To mitigate this issue, NuGet 2.7.2 allows the script author to include the license text block within a specially marked section which looks as follows.</span></span>

```
/************** NUGET: BEGIN LICENSE TEXT **************
    * The following code is licensed under the MIT license
    * Additional license information below is informational
    * only.
    ************** NUGET: END LICENSE TEXT ***************/
```

<span data-ttu-id="1c6c4-113">이 블록을 포함 하는 콘텐츠 파일을 사용 하 여 패키지를 업데이트 하는 경우 NuGet은 NuGet 갤러리의 버전과 비교 하 여 블록의 내용을 비교 하지 않으며, 따라서 원본 복사본과 일치 하는 것 처럼 콘텐츠 파일을 삭제 및 업데이트할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="1c6c4-113">When updating packages with content files containing this block, NuGet does not factor the contents of the block into the comparison with the version on the NuGet gallery, and can therefore delete and update the content file as though it matches the original copy.</span></span>

<span data-ttu-id="1c6c4-114">이 블록은 시작 및 끝 줄 어디에서 나 "NUGET: BEGIN 라이선스 텍스트" 및 "NUGET: END 라이선스 텍스트"로 식별 됩니다.</span><span class="sxs-lookup"><span data-stu-id="1c6c4-114">This block is identified by the text "NUGET: BEGIN LICENSE TEXT" and "NUGET: END LICENSE TEXT" occurring anywhere on the beginning and ending lines.</span></span>  <span data-ttu-id="1c6c4-115">언어에 관계 없이 모든 형식의 텍스트 파일에서이 기능을 사용할 수 있도록 하는 다른 형식 지정 요구 사항은 없습니다.</span><span class="sxs-lookup"><span data-stu-id="1c6c4-115">No other formatting requirements exist, allowing this feature to be used in any type of text file regardless of language.</span></span>

### <a name="add-binding-redirects-for-non-framework-assemblies"></a><span data-ttu-id="1c6c4-116">비 프레임 워크 어셈블리에 대 한 바인딩 리디렉션 추가</span><span class="sxs-lookup"><span data-stu-id="1c6c4-116">Add Binding Redirects for non-Framework Assemblies</span></span>
<span data-ttu-id="1c6c4-117">.NET Framework의 일부인 어셈블리의 경우 NuGet은 패키지를 업데이트할 때 응용 프로그램의 구성 파일에 바인딩 리디렉션을 추가 하는 것을 건너뜁니다.</span><span class="sxs-lookup"><span data-stu-id="1c6c4-117">For assemblies that are part of the .NET Framework, NuGet skips adding binding redirects into the application's configuration file when updating the package.</span></span> <span data-ttu-id="1c6c4-118">이 수정은 일부 어셈블리에 대 한 바인딩 리디렉션이 추가 되지 않는 경우에도 NuGet 2.7의 회귀를 해결 합니다. 이러한 어셈블리는 .NET Framework 일부로 간주 되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="1c6c4-118">This fix addresses a regression in NuGet 2.7 whereby binding redirects were not being added for some assemblies, even though those assemblies are not considered a part of the .NET Framework.</span></span> <span data-ttu-id="1c6c4-119">NuGet 2.7.2 이전 NuGet 2.5 및 2.6 동작을 복원 하 고 바인딩 리디렉션을 추가 합니다.</span><span class="sxs-lookup"><span data-stu-id="1c6c4-119">NuGet 2.7.2 restores the previous NuGet 2.5 and 2.6 behavior and adds the binding redirects.</span></span>

### <a name="installing-portable-libraries-with-xamarin-tools-installed"></a><span data-ttu-id="1c6c4-120">Xamarin 도구가 설치 된 이식 가능한 라이브러리 설치</span><span class="sxs-lookup"><span data-stu-id="1c6c4-120">Installing portable libraries with Xamarin Tools installed</span></span>
<span data-ttu-id="1c6c4-121">Xamarin의 개발 도구가 컴퓨터에 설치 되어 있는 경우에는 지원 되는 프레임 워크 구성 데이터를 수정 하 여 기존 대상 프레임 워크 조합과 Xamarin framework 간의 호환성을 지정 합니다.</span><span class="sxs-lookup"><span data-stu-id="1c6c4-121">When Xamarin's development tools are installed on a machine, they modify the supported frameworks configuration data to specify compatibility between existing target framework combinations and Xamarin frameworks.</span></span> <span data-ttu-id="1c6c4-122">버전 2.7.2에서 NuGet은 이제 이러한 암시적 호환성 규칙을 인식 하므로 Xamarin 플랫폼을 대상으로 하는 개발자는 Xamarin 호환 이지만 패키지 메타 데이터 자체에서 명시적으로 표시 되지 않은 이식 가능한 라이브러리를 쉽게 설치할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="1c6c4-122">With version 2.7.2, NuGet is now aware of these implicit compatibility rules, and therefore makes it easy for developers targeting Xamarin platforms to install portable libraries that are Xamarin-compatible but not explicitly marked as such in the package metadata itself.</span></span>

### <a name="machine-wide-configuration-settings-honored"></a><span data-ttu-id="1c6c4-123">시스템 수준 구성 설정 적용</span><span class="sxs-lookup"><span data-stu-id="1c6c4-123">Machine-wide configuration settings honored</span></span>
<span data-ttu-id="1c6c4-124">계층적 Nuget.Config 파일을 사용 하는 경우 솔루션 루트와 가장 가까운 Nuget.Config 파일에 대해 repositoryPath 키를 적용 하지 않았습니다.</span><span class="sxs-lookup"><span data-stu-id="1c6c4-124">When using hierarchical Nuget.Config files, the repositoryPath key was not being honored for Nuget.Config files closest to the solution root.</span></span> <span data-ttu-id="1c6c4-125">Visual Studio 2013에서 NuGet은 "Microsoft 및 .NET" 패키지 원본을 추가 하기 위해% ProgramData% \NuGet\Config\VisualStudio\12.0\Microsoft.VisualStudio.config에 사용자 지정 Nuget.Config 파일을 설치 합니다.</span><span class="sxs-lookup"><span data-stu-id="1c6c4-125">In Visual Studio 2013, NuGet installs a custom Nuget.Config file at %ProgramData%\NuGet\Config\VisualStudio\12.0\Microsoft.VisualStudio.config in order to add the "Microsoft and .NET" package source.</span></span> <span data-ttu-id="1c6c4-126">따라서 솔루션에서 사용자 지정 repositoryPath를 사용 하기 위한 해결 방법은 컴퓨터 수준 Nuget.Config를 삭제 하는 것입니다 .이는 "Microsoft 및 .NET" 패키지 원본도 제거 하는 것입니다.</span><span class="sxs-lookup"><span data-stu-id="1c6c4-126">As a result, the work-around for using a custom repositoryPath in a solution was to delete the machine-level Nuget.Config - which also meant removing the "Microsoft and .NET" package source.</span></span> <span data-ttu-id="1c6c4-127">이제 NuGet 2.7.2는 계층적 Nuget.Config 파일을 사용 하는 경우 repositoryPath에 대 한 우선 순위 규칙을 따릅니다.</span><span class="sxs-lookup"><span data-stu-id="1c6c4-127">NuGet 2.7.2 now honors the precedence rules for repositoryPath when using hierarchical Nuget.Config files.</span></span>

## <a name="all-changes"></a><span data-ttu-id="1c6c4-128">모든 변경 내용</span><span class="sxs-lookup"><span data-stu-id="1c6c4-128">All Changes</span></span>
<span data-ttu-id="1c6c4-129">NuGet 2.7.2에서 수정 된 작업 항목의 전체 목록은 [이 릴리스에 대 한 Nuget 문제 추적기](https://nuget.codeplex.com/workitem/list/advanced?keyword=&status=All&type=All&priority=All&release=NuGet%202.7.2&assignedTo=All&component=All&sortField=LastUpdatedDate&sortDirection=Descending&page=0&reasonClosed=Fixed)를 확인 하세요.</span><span class="sxs-lookup"><span data-stu-id="1c6c4-129">For a full list of work items fixed in NuGet 2.7.2, please view the [NuGet Issue Tracker for this release](https://nuget.codeplex.com/workitem/list/advanced?keyword=&status=All&type=All&priority=All&release=NuGet%202.7.2&assignedTo=All&component=All&sortField=LastUpdatedDate&sortDirection=Descending&page=0&reasonClosed=Fixed).</span></span>
