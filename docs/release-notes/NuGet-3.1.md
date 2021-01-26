---
title: NuGet 3.1 릴리스 정보
description: 알려진 문제, 버그 수정, 추가 된 기능 및 Ecrs를 비롯 한 NuGet 3.1에 대 한 릴리스 정보입니다.
author: JonDouglas
ms.author: jodou
ms.date: 11/11/2016
ms.topic: conceptual
ms.openlocfilehash: e1dc31e2543610b1da395f77fd2424bd85d985ef
ms.sourcegitcommit: ee6c3f203648a5561c809db54ebeb1d0f0598b68
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 01/26/2021
ms.locfileid: "98776539"
---
# <a name="nuget-31-release-notes"></a><span data-ttu-id="b4ba9-103">NuGet 3.1 릴리스 정보</span><span class="sxs-lookup"><span data-stu-id="b4ba9-103">NuGet 3.1 Release Notes</span></span>

<span data-ttu-id="b4ba9-104">[NuGet 3.0 릴리스 정보](../release-notes/nuget-3.0.0.md)  |  [NuGet 3.1.1 릴리스 정보](../release-notes/nuget-3.1.1.md)</span><span class="sxs-lookup"><span data-stu-id="b4ba9-104">[NuGet 3.0 Release Notes](../release-notes/nuget-3.0.0.md) | [NuGet 3.1.1 Release Notes](../release-notes/nuget-3.1.1.md)</span></span>

<span data-ttu-id="b4ba9-105">NuGet 3.1는 Visual Studio 2015 용 유니버설 Windows 플랫폼 SDK에 대 한 번들로 제공 되는 확장으로, 2015 7 월 27 일에 출시 되었습니다.</span><span class="sxs-lookup"><span data-stu-id="b4ba9-105">NuGet 3.1 was released on July 27, 2015 as a bundled extension to the Universal Windows Platform SDK for Visual Studio 2015.</span></span> <span data-ttu-id="b4ba9-106">Windows 개발 환경에서 이전에 시작 된 NuGet 플랫폼 간 작업을 활용할 수 있도록 Windows Platform SDK를 사용 하 여이 릴리스를 제공 했습니다.</span><span class="sxs-lookup"><span data-stu-id="b4ba9-106">We delivered this release with the Windows Platform SDK so that the Windows development experience could take advantage of the NuGet cross-platform work that had been previously started.</span></span> <span data-ttu-id="b4ba9-107">이 NuGet 확장 버전은 Visual Studio 2015 에서만 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="b4ba9-107">This NuGet extension version is only available for Visual Studio 2015.</span></span>

<span data-ttu-id="b4ba9-108">항상 버그 수정과 새로운 기능을 사용 하 여 업데이트를 게시 하므로 사용 가능한 최신 버전에 대 한 Visual Studio 갤러리 업데이트에 액세스할 수 있는 개발자를 사용 하는 것이 좋습니다.</span><span class="sxs-lookup"><span data-stu-id="b4ba9-108">We recommend those developers that have access to the Visual Studio gallery update to the latest version that is available, as we are always publishing updates with bug fixes and new features.</span></span>

## <a name="nuget-visual-studio-extension"></a><span data-ttu-id="b4ba9-109">NuGet Visual Studio 확장</span><span class="sxs-lookup"><span data-stu-id="b4ba9-109">NuGet Visual Studio Extension</span></span>

<span data-ttu-id="b4ba9-110">이 릴리스의 문제 및 기능에는 ["3.1 RTM UWP 전이적 지원" 마일스 톤](https://github.com/NuGet/Home/issues?utf8=%E2%9C%93&q=is%3Aclosed+milestone%3A%223.1+RTM+UWP+transitive+support%22+)  이 포함 된 GitHub에 태그가 지정 되어 있습니다. 3.1 릴리스에서 67 문제가 종결 되었습니다.</span><span class="sxs-lookup"><span data-stu-id="b4ba9-110">Issues and features in this release are tagged on GitHub with the ["3.1 RTM UWP transitive support" milestone](https://github.com/NuGet/Home/issues?utf8=%E2%9C%93&q=is%3Aclosed+milestone%3A%223.1+RTM+UWP+transitive+support%22+)  In total, we closed 67 issues in the 3.1 release.</span></span>

### <a name="new-features"></a><span data-ttu-id="b4ba9-111">새로운 기능</span><span class="sxs-lookup"><span data-stu-id="b4ba9-111">New Features</span></span>

* <span data-ttu-id="b4ba9-112">`project.json` Windows UWP 및 ASP.NET 5 지원 지원</span><span class="sxs-lookup"><span data-stu-id="b4ba9-112">`project.json` support for Windows UWP and ASP.NET 5 support</span></span>
* <span data-ttu-id="b4ba9-113">전이적 패키지 설치</span><span class="sxs-lookup"><span data-stu-id="b4ba9-113">Transitive package installation</span></span>

<span data-ttu-id="b4ba9-114">이러한 기능의 설명 및 정의는 설명서의 다른 위치에서 찾을 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="b4ba9-114">Description and definition of these features can be found elsewhere in the documentation.</span></span>

### <a name="deprecated"></a><span data-ttu-id="b4ba9-115">사용되지 않음</span><span class="sxs-lookup"><span data-stu-id="b4ba9-115">Deprecated</span></span>

<span data-ttu-id="b4ba9-116">Visual Studio 2015에는 다음 기능을 더 이상 사용할 수 없습니다.</span><span class="sxs-lookup"><span data-stu-id="b4ba9-116">The following features are no longer available for Visual Studio 2015:</span></span>

* <span data-ttu-id="b4ba9-117">솔루션 수준 패키지는 더 이상 설치할 수 없습니다.</span><span class="sxs-lookup"><span data-stu-id="b4ba9-117">Solution level packages can no longer be installed</span></span>

<span data-ttu-id="b4ba9-118">다음 기능은 Visual Studio 2015 및 해당 사양을 사용 하는 프로젝트에서 더 이상 사용할 수 없습니다. `project.json`</span><span class="sxs-lookup"><span data-stu-id="b4ba9-118">The following features are no longer available for Visual Studio 2015 and projects that use the `project.json` specification</span></span>

* <span data-ttu-id="b4ba9-119">`install.ps1` 및 `uninstall.ps1` -이러한 스크립트는 패키지 설치, 복원, 업데이트 및 제거 중에 무시 됩니다.</span><span class="sxs-lookup"><span data-stu-id="b4ba9-119">`install.ps1` and `uninstall.ps1` - These scripts will be ignored during package install, restore, update, and uninstall</span></span>
* <span data-ttu-id="b4ba9-120">구성 변환이 무시 됩니다.</span><span class="sxs-lookup"><span data-stu-id="b4ba9-120">Configuration transforms will be ignored</span></span>
* <span data-ttu-id="b4ba9-121">콘텐츠는 전달 되지만 프로젝트에는 복사 되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="b4ba9-121">Content will be carried, but not copied into a project.</span></span>
    * <span data-ttu-id="b4ba9-122">팀에서이 기능을 다시 구현 하기 위해 작업 하 고 있습니다. 다음의 설명 및 진행률을 따르세요. [https://github.com/NuGet/Home/issues/627](https://github.com/NuGet/Home/issues/627)</span><span class="sxs-lookup"><span data-stu-id="b4ba9-122">The team is working to re-implement this feature, follow the discussion and progress at: [https://github.com/NuGet/Home/issues/627](https://github.com/NuGet/Home/issues/627)</span></span>


### <a name="known-issues"></a><span data-ttu-id="b4ba9-123">알려진 문제</span><span class="sxs-lookup"><span data-stu-id="b4ba9-123">Known Issues</span></span>

<span data-ttu-id="b4ba9-124">이 릴리스와 함께 제공 되는 알려진 문제에는 여러 가지가 있습니다.</span><span class="sxs-lookup"><span data-stu-id="b4ba9-124">There were a number of known issues delivered with this release.</span></span>

* <span data-ttu-id="b4ba9-125">Windows 10 SDK를 사용 하 여 3.1 릴리스를 설치 하면 이전에 설치 된 NuGet 확장 버전이 다운 그레이드 됩니다.</span><span class="sxs-lookup"><span data-stu-id="b4ba9-125">Installation of the 3.1 release with the Windows 10 SDK will downgrade any version of NuGet extension that was previously installed</span></span>

## <a name="nuget-command-line"></a><span data-ttu-id="b4ba9-126">NuGet 명령줄</span><span class="sxs-lookup"><span data-stu-id="b4ba9-126">NuGet Command-line</span></span>

<span data-ttu-id="b4ba9-127">NuGet 명령줄 실행 파일을 업데이트 하 고 새 배포 가능한 위치로 이동 했으므로 nuget.exe의 기록 버전을 계속 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="b4ba9-127">The NuGet command-line executable was updated and moved to a new distributable location so that historical versions of nuget.exe can continue to be made available.</span></span>  <span data-ttu-id="b4ba9-128">Windows 용 nuget.exe의 3.1 베타 버전은 다음 위치에서 다운로드할 수 있습니다. [http://dist.nuget.org/win-x86-commandline/v3.1.0-beta/nuget.exe](http://dist.nuget.org/win-x86-commandline/v3.1.0-beta/nuget.exe)</span><span class="sxs-lookup"><span data-stu-id="b4ba9-128">You can download the 3.1 beta version of nuget.exe for Windows at: [http://dist.nuget.org/win-x86-commandline/v3.1.0-beta/nuget.exe](http://dist.nuget.org/win-x86-commandline/v3.1.0-beta/nuget.exe)</span></span>

<span data-ttu-id="b4ba9-129">새 배포 가능한 위치는이 템플릿 뒤에 오는 폴더 구조를 사용 하 여 dist.nuget.org 호스트에 있습니다.</span><span class="sxs-lookup"><span data-stu-id="b4ba9-129">The new distributable location resides on the dist.nuget.org host, with a folder structure that follows this template:</span></span>

```
{platform supported}/{version}/nuget.exe
```

### <a name="new-features"></a><span data-ttu-id="b4ba9-130">새로운 기능</span><span class="sxs-lookup"><span data-stu-id="b4ba9-130">New Features</span></span>

* <span data-ttu-id="b4ba9-131">nuget.exe 파일을 사용 하는 프로젝트에 패키지를 복원 하 고 설치할 수 있습니다 `project.json` .</span><span class="sxs-lookup"><span data-stu-id="b4ba9-131">nuget.exe can restore and install packages into projects that use a `project.json` file.</span></span>
* <span data-ttu-id="b4ba9-132">nuget.exe에서 NuGet v3 프로토콜에 연결 하 고 사용할 수 있습니다. [https://api.nuget.org/v3/index.json](https://api.nuget.org/v3/index.json)</span><span class="sxs-lookup"><span data-stu-id="b4ba9-132">nuget.exe can connect to and consume the NuGet v3 protocol at: [https://api.nuget.org/v3/index.json](https://api.nuget.org/v3/index.json)</span></span>

## <a name="known-issues"></a><span data-ttu-id="b4ba9-133">알려진 문제</span><span class="sxs-lookup"><span data-stu-id="b4ba9-133">Known Issues</span></span> ##

1.    <span data-ttu-id="b4ba9-134">파일에 대해 pack을 실행할 수 없습니다. `project.json` - [928](https://github.com/NuGet/Home/issues/928)</span><span class="sxs-lookup"><span data-stu-id="b4ba9-134">Cannot execute pack against a `project.json` file - [928](https://github.com/NuGet/Home/issues/928)</span></span>
2.    <span data-ttu-id="b4ba9-135">Mono- [1059](https://github.com/NuGet/Home/issues/1059) 에서는 지원 되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="b4ba9-135">Is not supported on Mono - [1059](https://github.com/NuGet/Home/issues/1059)</span></span>
3.    <span data-ttu-id="b4ba9-136">지역화 되지 않음- [1058](https://github.com/NuGet/Home/issues/1058),   [1057](https://github.com/NuGet/Home/issues/1057)</span><span class="sxs-lookup"><span data-stu-id="b4ba9-136">Is not localized - [1058](https://github.com/NuGet/Home/issues/1058),   [1057](https://github.com/NuGet/Home/issues/1057)</span></span>
4.    <span data-ttu-id="b4ba9-137">은 (는) 기존 1073와 마찬가지로 서명 되지 않습니다. http://nuget.org/nuget.exe  -  [](https://github.com/NuGet/Home/issues/1073)</span><span class="sxs-lookup"><span data-stu-id="b4ba9-137">Is not signed, just like the existing http://nuget.org/nuget.exe - [1073](https://github.com/NuGet/Home/issues/1073)</span></span>
