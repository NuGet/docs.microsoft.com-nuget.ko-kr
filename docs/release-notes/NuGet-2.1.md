---
title: NuGet 2.1 릴리스 정보
description: 알려진된 문제, 버그 수정, 추가 된 기능 및 Dcr 포함 하 여 NuGet 2.1에 대 한 릴리스 정보입니다.
author: karann-msft
ms.author: karann
ms.date: 11/11/2016
ms.topic: conceptual
ms.openlocfilehash: fd6dadc7968991c77c1b06a6a261415355b2fd73
ms.sourcegitcommit: 1d1406764c6af5fb7801d462e0c4afc9092fa569
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 09/04/2018
ms.locfileid: "43548599"
---
# <a name="nuget-21-release-notes"></a><span data-ttu-id="cbfa8-103">NuGet 2.1 릴리스 정보</span><span class="sxs-lookup"><span data-stu-id="cbfa8-103">NuGet 2.1 Release Notes</span></span>

<span data-ttu-id="cbfa8-104">[NuGet 2.0 릴리스 정보](../release-notes/nuget-2.0.md) | [NuGet 2.2 릴리스 정보](../release-notes/nuget-2.2.md)</span><span class="sxs-lookup"><span data-stu-id="cbfa8-104">[NuGet 2.0 Release Notes](../release-notes/nuget-2.0.md) | [NuGet 2.2 Release Notes](../release-notes/nuget-2.2.md)</span></span>

<span data-ttu-id="cbfa8-105">NuGet 2.1은 2012 년 10 월 4 일에 출시 되었습니다.</span><span class="sxs-lookup"><span data-stu-id="cbfa8-105">NuGet 2.1 was released on October 4, 2012.</span></span>

## <a name="hierarchical-nugetconfig"></a><span data-ttu-id="cbfa8-106">계층적 Nuget.Config</span><span class="sxs-lookup"><span data-stu-id="cbfa8-106">Hierarchical Nuget.Config</span></span>

<span data-ttu-id="cbfa8-107">NuGet 2.1 하면 더욱 유연 하 게 찾고 폴더 구조를 탐색 하는 재귀적으로 통해 NuGet 설정을 제어 하 고 `NuGet.Config` 파일과 다음 모든 찾은 파일 집합에서 구성을 작성 합니다.</span><span class="sxs-lookup"><span data-stu-id="cbfa8-107">NuGet 2.1 gives you greater flexibility in controlling NuGet settings by way of recursively walking up the folder structure looking for `NuGet.Config` files and then building the configuration from the set of all found files.</span></span>  <span data-ttu-id="cbfa8-108">예를 들어 여기서 팀의 다른 내부 종속성의 CI 빌드에 대 한 내부 패키지 리포지토리를 시나리오를 고려 합니다.</span><span class="sxs-lookup"><span data-stu-id="cbfa8-108">As an example, consider the scenario where a team has an internal package repository for CI builds of other internal dependencies.</span></span> <span data-ttu-id="cbfa8-109">개별 프로젝트의 폴더 구조는 다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="cbfa8-109">The folder structure for an individual project might look like the following:</span></span>

    C:\
    C:\myteam\
    C:\myteam\solution1
    C:\myteam\solution1\project1

<span data-ttu-id="cbfa8-110">또한 패키지 복원 솔루션을 사용할 경우 다음 폴더 에서도 존재 합니다.</span><span class="sxs-lookup"><span data-stu-id="cbfa8-110">Additionally, if package restore is enabled for the solution, the following folder will also exist:</span></span>

    C:\myteam\solution1\.nuget

<span data-ttu-id="cbfa8-111">팀의 내부 패키지 리포지토리를 팀이 없습니다 사용할 수 있도록 모든 프로젝트에 대 한 컴퓨터에서 하는 동안에 작동 하는 모든 프로젝트에 사용할 수 있는 권한을 가지려면 수 새 Nuget.Config 파일을 만들고 c:\myteam 폴더에 넣습니다.</span><span class="sxs-lookup"><span data-stu-id="cbfa8-111">In order to have the team’s internal package repository available for all projects that the team works on, while not making it available for every project on the machine, we can create a new Nuget.Config file and place it in the c:\myteam folder.</span></span> <span data-ttu-id="cbfa8-112">방법이 없기에 지정 된 프로젝트 / 패키지 폴더.</span><span class="sxs-lookup"><span data-stu-id="cbfa8-112">There is no way to specificy a packages folder per project.</span></span>

```xml
<configuration>
    <packageSources>
    <add key="Official project team source" value="http://teamserver/api/v2/" />
    </packageSources>
    <disabledPackageSources />
    <activePackageSource>
    <add key="Official project team source" value="http://teamserver/api/v2/" />
    </activePackageSource>
</configuration>
```

<span data-ttu-id="cbfa8-113">이제 아래와 같이 c:\myteam 아래에 있는 모든 폴더에서 'nuget.exe 소스' 명령을 실행 하 여 원본 추가 되었는지 볼 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="cbfa8-113">We can now see that the source was added by running the ‘nuget.exe sources’ command from any folder beneath c:\myteam as shown below:</span></span>

![부모 nuget config 파일에서 패키지 원본](./media/releasenotes-21-cfg-hierarchy.png)

<span data-ttu-id="cbfa8-115">`NuGet.Config` 파일에 대 한 다음과 같은 순서로 검색 됩니다.</span><span class="sxs-lookup"><span data-stu-id="cbfa8-115">`NuGet.Config` files are searched for in the following order:</span></span>

1. `.nuget\Nuget.Config`
2. <span data-ttu-id="cbfa8-116">루트 프로젝트 폴더에서 재귀적 탐색</span><span class="sxs-lookup"><span data-stu-id="cbfa8-116">Recursive walk from project folder to root</span></span>
3. <span data-ttu-id="cbfa8-117">전역 `Nuget.Config` (`%appdata%\NuGet\Nuget.Config`)</span><span class="sxs-lookup"><span data-stu-id="cbfa8-117">Global `Nuget.Config` (`%appdata%\NuGet\Nuget.Config`)</span></span>

<span data-ttu-id="cbfa8-118">구성을 적용 하는 것은 *역순*, 즉 위의 순서에 따라 전역 Nuget.Config는 수 먼저 적용 뒤에 검색 된 Nuget.Config 파일에서 루트 프로젝트 폴더에, `.nuget\Nuget.Config`합니다.</span><span class="sxs-lookup"><span data-stu-id="cbfa8-118">The configurations are than applied in the *reverse order*, meaning that based on the above ordering, the global Nuget.Config would be applied first, followed by the discovered Nuget.Config files from root to project folder, followed by `.nuget\Nuget.Config`.</span></span>  <span data-ttu-id="cbfa8-119">이 사용 중인 경우에 특히 중요 합니다 `<clear/>` 항목 집합이 구성에서 제거할 요소입니다.</span><span class="sxs-lookup"><span data-stu-id="cbfa8-119">This is particularly important if you’re using the `<clear/>` element to remove a set of items from config.</span></span>

## <a name="specify-packages-folder-location"></a><span data-ttu-id="cbfa8-120">'패키지' 폴더 위치를 지정 합니다.</span><span class="sxs-lookup"><span data-stu-id="cbfa8-120">Specify ‘packages’ Folder Location</span></span>

<span data-ttu-id="cbfa8-121">과거에는 NuGet에 솔루션 루트 폴더 아래에 찾이 알려진된 '패키지' 폴더에서 솔루션의 패키지를 관리 합니다.</span><span class="sxs-lookup"><span data-stu-id="cbfa8-121">In the past, NuGet has managed a solution’s packages from a known ‘packages’ folder found beneath the solution root folder.</span></span>  <span data-ttu-id="cbfa8-122">NuGet 패키지를 설치 하는 다양 한 솔루션이 있는 개발 팀은이 파일 시스템의 여러 곳에 설치 되는 동일한 패키지에서 발생할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="cbfa8-122">For development teams that have many different solutions which have NuGet packages installed, this can result in the same package being installed in many different places on the file system.</span></span>

<span data-ttu-id="cbfa8-123">NuGet 2.1을 통해 패키지 폴더의 위치 보다 세부적인 제어를 제공 합니다 `repositoryPath` 요소에는 `NuGet.Config` 파일입니다.</span><span class="sxs-lookup"><span data-stu-id="cbfa8-123">NuGet 2.1 provides more granular control over the location of the packages folder via the `repositoryPath` element in the `NuGet.Config` file.</span></span>  <span data-ttu-id="cbfa8-124">계층적 Nuget.Config 지원, 이전 예제에서 빌드 C:\myteam\ 공유 같은 패키지 폴더에서 모든 프로젝트가 하려는 것을 가정 합니다.</span><span class="sxs-lookup"><span data-stu-id="cbfa8-124">Building on the previous example of hierarchical Nuget.Config support, assume that we wish to have all projects under C:\myteam\ share the same packages folder.</span></span>  <span data-ttu-id="cbfa8-125">이렇게 하려면 다음 항목을 간단히 추가 `c:\myteam\Nuget.Config`합니다.</span><span class="sxs-lookup"><span data-stu-id="cbfa8-125">To accomplish this, simply add the following entry to `c:\myteam\Nuget.Config`.</span></span>

```xml
<configuration>
    <config>
    <add key="repositoryPath" value="C:\myteam\teampackages" />
    </config>
    ...
</configuration>
```

<span data-ttu-id="cbfa8-126">이 예제에서는 공유 `Nuget.Config` 파일 수준에 관계 없이 C:\myteam, 아래에 만들어진 모든 프로젝트에 대 한 공유 패키지 폴더를 지정 합니다.</span><span class="sxs-lookup"><span data-stu-id="cbfa8-126">In this example, the shared `Nuget.Config` file specifies a shared packages folder for every project that is created beneath C:\myteam, regardless of depth.</span></span> <span data-ttu-id="cbfa8-127">참고는 솔루션 루트 아래에 있는 기존 패키지 폴더에 있는 경우 삭제 해야 하기 전에 NuGet 패키지를 새 위치에 배치 됩니다.</span><span class="sxs-lookup"><span data-stu-id="cbfa8-127">Note that if you have an existing packages folder underneath your solution root, you need to delete it before NuGet will place packages in the new location.</span></span>

## <a name="support-for-portable-libraries"></a><span data-ttu-id="cbfa8-128">이식 가능한 라이브러리에 대 한 지원</span><span class="sxs-lookup"><span data-stu-id="cbfa8-128">Support for Portable Libraries</span></span>

<span data-ttu-id="cbfa8-129">[이식 가능한 라이브러리](/dotnet/standard/cross-platform/cross-platform-development-with-the-portable-class-library) 는.NET 4 버전의.net Framework에도 Xbox 및 Windows Phone silverlight에서 다른 Microsoft 플랫폼에서 수정 없이 사용할 수 있는 어셈블리를 빌드할 수 있도록 처음 도입 된 기능 360 (하지만 지금은 NuGet에는 Xbox 이식 가능한 라이브러리 대상을 지원 하지 않습니다).</span><span class="sxs-lookup"><span data-stu-id="cbfa8-129">[Portable libraries](/dotnet/standard/cross-platform/cross-platform-development-with-the-portable-class-library) is a feature first introduced with .NET 4 that enables you to build assemblies that can work without modification on different Microsoft platforms, from versions of the.NET Framework to Silverlight to Windows Phone and even Xbox 360 (though at this time, NuGet does not support the Xbox portable library target).</span></span>  <span data-ttu-id="cbfa8-130">확장 하 여 합니다 [규칙 패키지](../create-packages/supporting-multiple-target-frameworks.md) framework 버전 및 프로필에 대 한 NuGet 2.1 이제 이식 가능한 라이브러리 복합 프레임 워크 및 프로필 대상 있는 패키지를 만들 수 있도록 하 여 `lib` 폴더입니다.</span><span class="sxs-lookup"><span data-stu-id="cbfa8-130">By extending the [package conventions](../create-packages/supporting-multiple-target-frameworks.md) for framework versions and profiles, NuGet 2.1 now supports portable libraries by enabling you to create packages that have compound framework and profile target `lib` folders.</span></span>

<span data-ttu-id="cbfa8-131">예를 들어 다음 이식 가능한 클래스 라이브러리의 사용 가능한 대상 플랫폼을 고려 합니다.</span><span class="sxs-lookup"><span data-stu-id="cbfa8-131">As an example, consider the following portable class library’s available target platforms.</span></span>

![이식 가능한 라이브러리 만들기 대화 상자](./media/releasenotes-21-plib.png)

<span data-ttu-id="cbfa8-133">라이브러리를 빌드한 후 명령과 `nuget.exe pack MyPortableProject.csproj` 를 실행할 새 이식 가능한 라이브러리 패키지 폴더 구조는 생성 된 NuGet 패키지의 내용을 검사 하 여 볼 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="cbfa8-133">After the library is built and the command `nuget.exe pack MyPortableProject.csproj` is run, the new portable library package folder structure can be seen by examining the contents of the generated NuGet package.</span></span>

![이식 가능한 라이브러리 패키지 레이아웃](./media/releasenotes-21-plib-layout.png)

<span data-ttu-id="cbfa8-135">알 수 있듯이 이식 가능한 라이브러리 폴더 이름 규칙 패턴을 따릅니다. 'portable-{framework 1} + {framework n}'는 프레임 워크 식별자에 따라 기존 [프레임 워크 이름 및 버전 규칙](../reference/target-frameworks.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="cbfa8-135">As you can see, the portable library folder name convention follows the pattern ‘portable-{framework 1}+{framework n}’ where the framework identifiers follow the existing [framework name and version conventions](../reference/target-frameworks.md).</span></span> <span data-ttu-id="cbfa8-136">이름 및 버전 규칙의 한 가지 예외는 Windows Phone 사용 되는 프레임 워크 식별자에 있습니다.</span><span class="sxs-lookup"><span data-stu-id="cbfa8-136">One exception to the name and version conventions is found in the framework identifier used for Windows Phone.</span></span>  <span data-ttu-id="cbfa8-137">이 모니커 'wp' (wp7, wp71 wp8) 프레임 워크 이름을 사용 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="cbfa8-137">This moniker should use the framework name ‘wp’ (wp7, wp71 or wp8).</span></span> <span data-ttu-id="cbfa8-138">오류가 발생 하면 예를 들어, ' silverlight-wp7'를 사용 하 여 합니다.</span><span class="sxs-lookup"><span data-stu-id="cbfa8-138">Using ‘silverlight-wp7’, for example, will result in an error.</span></span>

<span data-ttu-id="cbfa8-139">이 폴더 구조에서 만든 패키지를 설치할 때 NuGet 폴더 이름에 지정 된 대로 여러 대상에 해당 프레임 워크 및 프로필 규칙을 이제 적용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="cbfa8-139">When installing the package that is created from this folder structure, NuGet can now apply its framework and profile rules to multiple targets, as specified in the folder name.</span></span>  <span data-ttu-id="cbfa8-140">NuGet의 일치 규칙 숨김은 "보다 구체적인" 대상 "작은" 구체적인 우선적으로 적용 됩니다는 원칙이입니다.</span><span class="sxs-lookup"><span data-stu-id="cbfa8-140">Behind NuGet’s matching rules is the principle that “more specific” targets will take precedence over “less specific” ones.</span></span>  <span data-ttu-id="cbfa8-141">이 특정 플랫폼을 대상으로 하는 모니커는 항상 기본 이식 가능한 항목 위에 둘 다는 프로젝트와 호환 되는 경우를 의미 합니다.</span><span class="sxs-lookup"><span data-stu-id="cbfa8-141">This means that monikers targeting a specific platform will always be preferred over portable ones if they are both compatible with a project.</span></span>  <span data-ttu-id="cbfa8-142">또한 여러 휴대용 대상 프로젝트와 호환 되는 경우 NuGet는 지원 되는 플랫폼 집합 패키지 참조를 프로젝트에 "가장 가까운" 인 것을 선호 합니다.</span><span class="sxs-lookup"><span data-stu-id="cbfa8-142">Additionally, if multiple portable targets are compatible with a project, NuGet will prefer the one where the set of platforms supported is “closest” to the project referencing the package.</span></span>

## <a name="targeting-windows-8-and-windows-phone-8-projects"></a><span data-ttu-id="cbfa8-143">대상 Windows 8 및 Windows Phone 8 프로젝트</span><span class="sxs-lookup"><span data-stu-id="cbfa8-143">Targeting Windows 8 and Windows Phone 8 Projects</span></span>

<span data-ttu-id="cbfa8-144">이식 가능한 라이브러리 프로젝트를 대상으로 하는 것에 대 한 지원에 추가 하는 것 외에도 NuGet 2.1 일부 새 일반 모니커 Windows 스토어 및 Windows Phone 프로젝트 될 뿐만 아니라 Windows 8 스토어 및 Windows Phone 8 프로젝트에 대 한 새 프레임 워크 모니커를 제공 각 플랫폼의 이후 버전에서 관리 하기가 더 쉽습니다.</span><span class="sxs-lookup"><span data-stu-id="cbfa8-144">In addition to adding support for targeting portable library projects, NuGet 2.1 provides new framework monikers for both Windows 8 Store and Windows Phone 8 projects, as well as some new general monikers for Windows Store and Windows Phone projects that will be easier to manage across future versions of the respective platforms.</span></span>

<span data-ttu-id="cbfa8-145">Windows 8 스토어 응용 프로그램에 대 한 식별자를 다음과 같이 표시 합니다.</span><span class="sxs-lookup"><span data-stu-id="cbfa8-145">For Windows 8 Store applications, the identifiers look as follows:</span></span>

| <span data-ttu-id="cbfa8-146">2.0 및 이전 버전의 NuGet</span><span class="sxs-lookup"><span data-stu-id="cbfa8-146">NuGet 2.0 and earlier</span></span> | <span data-ttu-id="cbfa8-147">NuGet 2.1</span><span class="sxs-lookup"><span data-stu-id="cbfa8-147">NuGet 2.1</span></span> |
| ---------------- | ----------- |
| <span data-ttu-id="cbfa8-148">winRT45, .NETCore45</span><span class="sxs-lookup"><span data-stu-id="cbfa8-148">winRT45, .NETCore45</span></span> | <span data-ttu-id="cbfa8-149">Windows, Windows8, win, win8</span><span class="sxs-lookup"><span data-stu-id="cbfa8-149">Windows, Windows8, win, win8</span></span> |

<br/>
<span data-ttu-id="cbfa8-150">Windows Phone 프로젝트에 대 한 식별자를 다음과 같이 표시 합니다.</span><span class="sxs-lookup"><span data-stu-id="cbfa8-150">For Windows Phone projects, the identifiers look as follows:</span></span>

| <span data-ttu-id="cbfa8-151">Phone OS</span><span class="sxs-lookup"><span data-stu-id="cbfa8-151">Phone OS</span></span> | <span data-ttu-id="cbfa8-152">2.0 및 이전 버전의 NuGet</span><span class="sxs-lookup"><span data-stu-id="cbfa8-152">NuGet 2.0 and earlier</span></span> | <span data-ttu-id="cbfa8-153">NuGet 2.1</span><span class="sxs-lookup"><span data-stu-id="cbfa8-153">NuGet 2.1</span></span> |
| --- | --- | --- |
| <span data-ttu-id="cbfa8-154">Windows Phone 7</span><span class="sxs-lookup"><span data-stu-id="cbfa8-154">Windows Phone 7</span></span> | <span data-ttu-id="cbfa8-155">silverlight3-wp</span><span class="sxs-lookup"><span data-stu-id="cbfa8-155">silverlight3-wp</span></span> | <span data-ttu-id="cbfa8-156">wp, wp7, WindowsPhone, WindowsPhone7</span><span class="sxs-lookup"><span data-stu-id="cbfa8-156">wp, wp7, WindowsPhone, WindowsPhone7</span></span> |
| <span data-ttu-id="cbfa8-157">Windows Phone 7.5(mango)</span><span class="sxs-lookup"><span data-stu-id="cbfa8-157">Windows Phone 7.5 (Mango)</span></span> | <span data-ttu-id="cbfa8-158">silverlight4 wp71</span><span class="sxs-lookup"><span data-stu-id="cbfa8-158">silverlight4-wp71</span></span> | <span data-ttu-id="cbfa8-159">wp71, WindowsPhone71</span><span class="sxs-lookup"><span data-stu-id="cbfa8-159">wp71, WindowsPhone71</span></span> |
| <span data-ttu-id="cbfa8-160">Windows Phone 8</span><span class="sxs-lookup"><span data-stu-id="cbfa8-160">Windows Phone 8</span></span> | <span data-ttu-id="cbfa8-161">(지원 되지 않음)</span><span class="sxs-lookup"><span data-stu-id="cbfa8-161">(not supported)</span></span> | <span data-ttu-id="cbfa8-162">wp8, WindowsPhone8</span><span class="sxs-lookup"><span data-stu-id="cbfa8-162">wp8, WindowsPhone8</span></span> |

<br/>
<span data-ttu-id="cbfa8-163">모든 변경에서 NuGet 2.1에서 완전히 지원 되는 이전 프레임 워크 이름을 계속 합니다.</span><span class="sxs-lookup"><span data-stu-id="cbfa8-163">In all of the above changes, the old framework names will continue to be fully supported by NuGet 2.1.</span></span>  <span data-ttu-id="cbfa8-164">앞으로 새 이름은 사용 해야 하므로 더 안정적인 각 플랫폼의 이후 버전에서 합니다.</span><span class="sxs-lookup"><span data-stu-id="cbfa8-164">Moving forward, the new names should be used as they will be more stable across future versions of the respective platforms.</span></span> <span data-ttu-id="cbfa8-165">새 이름이 됩니다 *되지* 수 2.1 이전 버전의 NuGet에서 지 원하는 반면 계획 적절 하 게 전환 하는 경우에 대 한 합니다.</span><span class="sxs-lookup"><span data-stu-id="cbfa8-165">The new names will *not* be supported in versions of NuGet prior to 2.1, however, so plan accordingly for when to make the switch.</span></span>

## <a name="improved-search-in-package-manager-dialog"></a><span data-ttu-id="cbfa8-166">패키지 관리자 대화 상자에서 향상 된 검색</span><span class="sxs-lookup"><span data-stu-id="cbfa8-166">Improved Search in Package Manager Dialog</span></span>

<span data-ttu-id="cbfa8-167">지난 몇 가지 반복 변경 속도 및 패키지 검색 관련성을 크게 향상 하는 NuGet 갤러리에 도입 되었습니다.</span><span class="sxs-lookup"><span data-stu-id="cbfa8-167">Over the past several iterations, changes have been introduced to the NuGet gallery that greatly improved the speed and relevance of package searches.</span></span>  <span data-ttu-id="cbfa8-168">그러나 이러한 향상 된이 기능 nuget.org 웹 사이트 수 있었습니다.</span><span class="sxs-lookup"><span data-stu-id="cbfa8-168">However, these improvements were limited to the nuget.org Web site.</span></span>  <span data-ttu-id="cbfa8-169">NuGet 2.1 NuGet 패키지 관리자 대화 상자를 통해 사용 가능한 환경을 향상 된 검색을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="cbfa8-169">NuGet 2.1 makes the improved search experience available through the NuGet package manager dialog.</span></span>  <span data-ttu-id="cbfa8-170">예를 들어 Windows Azure Caching 미리 보기 패키지를 검색 하려고 한다고 가정해 보겠습니다.</span><span class="sxs-lookup"><span data-stu-id="cbfa8-170">As an example, imagine that you wanted to find the Windows Azure Caching Preview package.</span></span>  <span data-ttu-id="cbfa8-171">이 패키지에 대 한 적절 한 검색 쿼리는 "Azure Cache" 될 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="cbfa8-171">A reasonable search query for this package may be “Azure Cache”.</span></span>  <span data-ttu-id="cbfa8-172">이전 버전의 패키지 관리자 대화 상자에서 원하는 패키지가 나열 되지 않습니다도 결과의 첫 번째 페이지에서.</span><span class="sxs-lookup"><span data-stu-id="cbfa8-172">In previous versions of the package manager dialog, the desired package would not even be listed on the first page of results.</span></span>  <span data-ttu-id="cbfa8-173">그러나 NuGet 2.1에서 원하는 패키지가 이제 표시 검색 결과의 맨 위에 있는 됩니다.</span><span class="sxs-lookup"><span data-stu-id="cbfa8-173">However, in NuGet 2.1, the desired package now shows up at the top of the search results.</span></span>

![패키지 관리자 대화 검색](./media/releasenotes-21-vsdlg-search.png)

## <a name="force-package-update"></a><span data-ttu-id="cbfa8-175">패키지 업데이트 적용</span><span class="sxs-lookup"><span data-stu-id="cbfa8-175">Force Package Update</span></span>

<span data-ttu-id="cbfa8-176">NuGet 2.1 이전 NuGet 패키지 업데이트는 아닌 경우 건너 뛸 높은 버전 번호입니다.</span><span class="sxs-lookup"><span data-stu-id="cbfa8-176">Prior to NuGet 2.1, NuGet would skip updating a package when there was a not a high version number.</span></span>  <span data-ttu-id="cbfa8-177">이 팀 패키지 버전 번호를 각 빌드를 사용 하 여 증가 하지 않은 빌드 또는 CI 시나리오의 경우 특히 특정 시나리오에 대 한 마찰을 도입 했습니다.</span><span class="sxs-lookup"><span data-stu-id="cbfa8-177">This introduced friction for certain scenarios – particularly in the case of build or CI scenarios where the team did not want to increment the package version number with each build.</span></span>  <span data-ttu-id="cbfa8-178">원하는 동작 관계 없이 강제로 업데이트 하는 것 이었습니다.</span><span class="sxs-lookup"><span data-stu-id="cbfa8-178">The desired behavior was to force an update regardless.</span></span>  <span data-ttu-id="cbfa8-179">NuGet 2.1 '다시 설치' 플래그를 사용 하 여이 문제를 해결 합니다.</span><span class="sxs-lookup"><span data-stu-id="cbfa8-179">NuGet 2.1 addresses this with the ‘reinstall’ flag.</span></span>  <span data-ttu-id="cbfa8-180">예를 들어, 이전 버전의 NuGet 최신 패키지 버전 없는 패키지를 업데이트 하려고 할 때 다음에서 결과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="cbfa8-180">For example, previous versions of NuGet would result in the following when attempting to update a package that did not have a more recent package version:</span></span>

    PM> Update-Package Moq
    No updates available for 'Moq' in project 'MySolution.MyConsole'.

<span data-ttu-id="cbfa8-181">다시 설치 플래그를 사용 하 여 패키지 업데이트될지 여부에 관계 없이 최신 버전이 있습니다.</span><span class="sxs-lookup"><span data-stu-id="cbfa8-181">With the reinstall flag, the package will be updated regardless of whether there is a newer version.</span></span>

    PM> Update-Package Moq -Reinstall
    Successfully removed 'Moq 4.0.10827' from MySolution.MyConsole.
    Successfully uninstalled 'Moq 4.0.10827'.
    Successfully installed 'Moq 4.0.10827'.
    Successfully added 'Moq 4.0.10827' to MySolution.MyConsole.

<span data-ttu-id="cbfa8-182">여기서 다시 설치 플래그를 입증 유용한 다른 시나리오의 프레임 워크 대상 다시 지정 됩니다.</span><span class="sxs-lookup"><span data-stu-id="cbfa8-182">Another scenario where the reinstall flag proves beneficial is that of framework re-targeting.</span></span> <span data-ttu-id="cbfa8-183">(예를 들어.NET 4에서.NET 4.5로), 프로젝트의 대상 프레임 워크를 변경 하는 경우 Update-package-다시 설치 프로젝트에 설치 된 모든 NuGet 패키지에 대 한 올바른 어셈블리에 대 한 참조를 업데이트할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="cbfa8-183">When changing the target framework of a project (for example, from .NET 4 to .NET 4.5), Update-Package -Reinstall can update references to the correct assemblies for all NuGet packages installed in the project.</span></span>

## <a name="edit-package-sources-within-visual-studio"></a><span data-ttu-id="cbfa8-184">Visual Studio 내에서 패키지 소스 편집</span><span class="sxs-lookup"><span data-stu-id="cbfa8-184">Edit Package Sources Within Visual Studio</span></span>

<span data-ttu-id="cbfa8-185">이전 버전의 NuGet에서 다시 패키지 소스를 추가 및 삭제 하는 데 필요한 Visual Studio 옵션 대화 상자 내에서 패키지 원본을 업데이트 합니다.</span><span class="sxs-lookup"><span data-stu-id="cbfa8-185">In previous versions of NuGet, updating a package source from within the Visual Studio options dialog required deleting and re-adding the package source.</span></span>  <span data-ttu-id="cbfa8-186">NuGet 2.1 구성 사용자 인터페이스의 첫 번째 클래스 함수로 서 업데이트를 지원 하 여이 워크플로 개선 합니다.</span><span class="sxs-lookup"><span data-stu-id="cbfa8-186">NuGet 2.1 improves this workflow by supporting update as a first class function of the configuration user interface.</span></span>

![패키지 관리자 구성 대화 상자](./media/releasenotes-21-edit-pkg-source.png)

## <a name="bug-fixes"></a><span data-ttu-id="cbfa8-188">버그 수정</span><span class="sxs-lookup"><span data-stu-id="cbfa8-188">Bug Fixes</span></span>

<span data-ttu-id="cbfa8-189">NuGet 2.1에는 여러 버그 수정을 포함 합니다.</span><span class="sxs-lookup"><span data-stu-id="cbfa8-189">NuGet 2.1 includes many bug fixes.</span></span> <span data-ttu-id="cbfa8-190">작업의 전체 목록은 항목 고정 NuGet 2.0에서 하세요 보기는 [이 릴리스의 NuGet 문제 추적기](http://nuget.codeplex.com/workitem/list/advanced?keyword=&status=Fixed&type=All&priority=All&release=NuGet%202.1&assignedTo=All&component=All&sortField=LastUpdatedDate&sortDirection=Descending&page=0)합니다.</span><span class="sxs-lookup"><span data-stu-id="cbfa8-190">For a full list of work items fixed in NuGet 2.0, please view the [NuGet Issue Tracker for this release](http://nuget.codeplex.com/workitem/list/advanced?keyword=&status=Fixed&type=All&priority=All&release=NuGet%202.1&assignedTo=All&component=All&sortField=LastUpdatedDate&sortDirection=Descending&page=0).</span></span>
