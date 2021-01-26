---
title: NuGet 2.1 릴리스 정보
description: 알려진 문제, 버그 수정, 추가 된 기능 및 Ecrs를 비롯 한 NuGet 2.1에 대 한 릴리스 정보입니다.
author: JonDouglas
ms.author: jodou
ms.date: 11/11/2016
ms.topic: conceptual
ms.openlocfilehash: c44ad32c8c4018ccb517b41bffda674eef1f11f3
ms.sourcegitcommit: ee6c3f203648a5561c809db54ebeb1d0f0598b68
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 01/26/2021
ms.locfileid: "98777034"
---
# <a name="nuget-21-release-notes"></a><span data-ttu-id="02a11-103">NuGet 2.1 릴리스 정보</span><span class="sxs-lookup"><span data-stu-id="02a11-103">NuGet 2.1 Release Notes</span></span>

<span data-ttu-id="02a11-104">[NuGet 2.0 릴리스 정보](../release-notes/nuget-2.0.md)  |  [NuGet 2.2 릴리스 정보](../release-notes/nuget-2.2.md)</span><span class="sxs-lookup"><span data-stu-id="02a11-104">[NuGet 2.0 Release Notes](../release-notes/nuget-2.0.md) | [NuGet 2.2 Release Notes](../release-notes/nuget-2.2.md)</span></span>

<span data-ttu-id="02a11-105">NuGet 2.1은 2012 년 10 월 4 일에 출시 되었습니다.</span><span class="sxs-lookup"><span data-stu-id="02a11-105">NuGet 2.1 was released on October 4, 2012.</span></span>

## <a name="hierarchical-nugetconfig"></a><span data-ttu-id="02a11-106">계층 구조 Nuget.Config</span><span class="sxs-lookup"><span data-stu-id="02a11-106">Hierarchical Nuget.Config</span></span>

<span data-ttu-id="02a11-107">NuGet 2.1은 `NuGet.Config` 파일을 찾은 다음, 검색 된 모든 파일 집합에서 구성을 빌드하여 폴더 구조를 재귀적으로 탐색 하는 방법으로 nuget 설정을 더욱 유연 하 게 제어할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="02a11-107">NuGet 2.1 gives you greater flexibility in controlling NuGet settings by way of recursively walking up the folder structure looking for `NuGet.Config` files and then building the configuration from the set of all found files.</span></span>  <span data-ttu-id="02a11-108">예를 들어 팀에 다른 내부 종속성의 CI 빌드에 대 한 내부 패키지 리포지토리가 있는 시나리오를 살펴보겠습니다.</span><span class="sxs-lookup"><span data-stu-id="02a11-108">As an example, consider the scenario where a team has an internal package repository for CI builds of other internal dependencies.</span></span> <span data-ttu-id="02a11-109">개별 프로젝트에 대 한 폴더 구조는 다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="02a11-109">The folder structure for an individual project might look like the following:</span></span>

```
C:\
C:\myteam\
C:\myteam\solution1
C:\myteam\solution1\project1
```

<span data-ttu-id="02a11-110">또한 솔루션에 대해 패키지 복원이 사용 되는 경우 다음 폴더도 존재 합니다.</span><span class="sxs-lookup"><span data-stu-id="02a11-110">Additionally, if package restore is enabled for the solution, the following folder will also exist:</span></span>

```
C:\myteam\solution1\.nuget
```

<span data-ttu-id="02a11-111">팀에서 작업 하는 모든 프로젝트에 대해 팀의 내부 패키지 리포지토리를 사용할 수 있도록 하 고, 컴퓨터의 모든 프로젝트에서 사용할 수 있도록 하는 것은 아니지만 새 Nuget.Config 파일을 만들어 c:\myteam 폴더에 저장할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="02a11-111">In order to have the team’s internal package repository available for all projects that the team works on, while not making it available for every project on the machine, we can create a new Nuget.Config file and place it in the c:\myteam folder.</span></span> <span data-ttu-id="02a11-112">프로젝트 마다 패키지 폴더를 변수와 방법이 없습니다.</span><span class="sxs-lookup"><span data-stu-id="02a11-112">There is no way to specificy a packages folder per project.</span></span>

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

<span data-ttu-id="02a11-113">이제 아래와 같이 c:\myteam 아래의 모든 폴더에서 ' nuget.exe sources ' 명령을 실행 하 여 소스가 추가 되었음을 확인할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="02a11-113">We can now see that the source was added by running the ‘nuget.exe sources’ command from any folder beneath c:\myteam as shown below:</span></span>

![부모 nuget 구성의 패키지 소스](./media/releasenotes-21-cfg-hierarchy.png)

<span data-ttu-id="02a11-115">`NuGet.Config` 파일은 다음 순서로 검색 됩니다.</span><span class="sxs-lookup"><span data-stu-id="02a11-115">`NuGet.Config` files are searched for in the following order:</span></span>

1. `.nuget\Nuget.Config`
2. <span data-ttu-id="02a11-116">프로젝트 폴더에서 루트로의 재귀 연습</span><span class="sxs-lookup"><span data-stu-id="02a11-116">Recursive walk from project folder to root</span></span>
3. <span data-ttu-id="02a11-117">Global `Nuget.Config` ( `%appdata%\NuGet\Nuget.Config` )</span><span class="sxs-lookup"><span data-stu-id="02a11-117">Global `Nuget.Config` (`%appdata%\NuGet\Nuget.Config`)</span></span>

<span data-ttu-id="02a11-118">이러한 구성은 *역순* 으로 적용 되는 것을 의미 합니다. 즉, 위의 순서에 따라 전역 Nuget.Config 먼저 적용 된 다음, 검색 된 Nuget.Config 파일의 루트에서 프로젝트 폴더로 차례로 적용 됩니다 `.nuget\Nuget.Config` .</span><span class="sxs-lookup"><span data-stu-id="02a11-118">The configurations are than applied in the *reverse order*, meaning that based on the above ordering, the global Nuget.Config would be applied first, followed by the discovered Nuget.Config files from root to project folder, followed by `.nuget\Nuget.Config`.</span></span>  <span data-ttu-id="02a11-119">요소를 사용 하 여 `<clear/>` 구성에서 항목 집합을 제거 하는 경우에 특히 중요 합니다.</span><span class="sxs-lookup"><span data-stu-id="02a11-119">This is particularly important if you’re using the `<clear/>` element to remove a set of items from config.</span></span>

## <a name="specify-packages-folder-location"></a><span data-ttu-id="02a11-120">' 패키지 ' 폴더 위치 지정</span><span class="sxs-lookup"><span data-stu-id="02a11-120">Specify ‘packages’ Folder Location</span></span>

<span data-ttu-id="02a11-121">이전에는 NuGet이 솔루션 루트 폴더 아래에 있는 알려진 ' 패키지 ' 폴더에서 솔루션 패키지를 관리 했습니다.</span><span class="sxs-lookup"><span data-stu-id="02a11-121">In the past, NuGet has managed a solution’s packages from a known ‘packages’ folder found beneath the solution root folder.</span></span>  <span data-ttu-id="02a11-122">NuGet 패키지를 설치 하는 다양 한 솔루션을 포함 하는 개발 팀의 경우 동일한 패키지가 파일 시스템의 여러 위치에 설치 될 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="02a11-122">For development teams that have many different solutions which have NuGet packages installed, this can result in the same package being installed in many different places on the file system.</span></span>

<span data-ttu-id="02a11-123">NuGet 2.1은 파일의 요소를 통해 패키지 폴더의 위치를 보다 세밀 하 게 제어 합니다 `repositoryPath` `NuGet.Config` .</span><span class="sxs-lookup"><span data-stu-id="02a11-123">NuGet 2.1 provides more granular control over the location of the packages folder via the `repositoryPath` element in the `NuGet.Config` file.</span></span>  <span data-ttu-id="02a11-124">계층 Nuget.Config 지원의 이전 예제를 기반으로 하 여 C:\myteam\의 모든 프로젝트가 동일한 패키지 폴더를 공유 한다고 가정 합니다.</span><span class="sxs-lookup"><span data-stu-id="02a11-124">Building on the previous example of hierarchical Nuget.Config support, assume that we wish to have all projects under C:\myteam\ share the same packages folder.</span></span>  <span data-ttu-id="02a11-125">이를 수행 하려면에 다음 항목을 추가 하면 됩니다 `c:\myteam\Nuget.Config` .</span><span class="sxs-lookup"><span data-stu-id="02a11-125">To accomplish this, simply add the following entry to `c:\myteam\Nuget.Config`.</span></span>

```xml
<configuration>
    <config>
    <add key="repositoryPath" value="C:\myteam\teampackages" />
    </config>
    ...
</configuration>
```

<span data-ttu-id="02a11-126">이 예에서 공유 `Nuget.Config` 파일은 깊이에 관계 없이 C:\myteam 아래에 생성 되는 모든 프로젝트에 대 한 공유 패키지 폴더를 지정 합니다.</span><span class="sxs-lookup"><span data-stu-id="02a11-126">In this example, the shared `Nuget.Config` file specifies a shared packages folder for every project that is created beneath C:\myteam, regardless of depth.</span></span> <span data-ttu-id="02a11-127">솔루션 루트 아래에 기존 패키지 폴더가 있는 경우 NuGet이 새 위치에 패키지를 배치 하기 전에 삭제 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="02a11-127">Note that if you have an existing packages folder underneath your solution root, you need to delete it before NuGet will place packages in the new location.</span></span>

## <a name="support-for-portable-libraries"></a><span data-ttu-id="02a11-128">이식 가능한 라이브러리에 대 한 지원</span><span class="sxs-lookup"><span data-stu-id="02a11-128">Support for Portable Libraries</span></span>

<span data-ttu-id="02a11-129">[이식 가능한 라이브러리](/dotnet/standard/cross-platform/cross-platform-development-with-the-portable-class-library) 는 .net 4에서 처음 도입 된 기능으로,이 기능을 사용 하면 the.NET Framework 버전에서 Silverlight로 Windows Phone 및 xbox 360에 이르기까지 다양 한 Microsoft 플랫폼에서 수정 하지 않고도 작업할 수 있는 어셈블리를 빌드할 수 있습니다. 그러나 이번에는 NuGet이 xbox 이식 가능한 라이브러리 대상을 지원 하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="02a11-129">[Portable libraries](/dotnet/standard/cross-platform/cross-platform-development-with-the-portable-class-library) is a feature first introduced with .NET 4 that enables you to build assemblies that can work without modification on different Microsoft platforms, from versions of the.NET Framework to Silverlight to Windows Phone and even Xbox 360 (though at this time, NuGet does not support the Xbox portable library target).</span></span>  <span data-ttu-id="02a11-130">이제 NuGet 2.1은 프레임 워크 버전 및 프로필에 대 한 [패키지 규칙](../create-packages/supporting-multiple-target-frameworks.md) 을 확장 하 여 복합 프레임 워크 및 프로필 대상 폴더를 포함 하는 패키지를 만들 수 있도록 하 여 이식 가능한 라이브러리를 지원 합니다 `lib` .</span><span class="sxs-lookup"><span data-stu-id="02a11-130">By extending the [package conventions](../create-packages/supporting-multiple-target-frameworks.md) for framework versions and profiles, NuGet 2.1 now supports portable libraries by enabling you to create packages that have compound framework and profile target `lib` folders.</span></span>

<span data-ttu-id="02a11-131">예를 들어 다음과 같은 이식 가능한 클래스 라이브러리의 사용 가능한 대상 플랫폼을 살펴보겠습니다.</span><span class="sxs-lookup"><span data-stu-id="02a11-131">As an example, consider the following portable class library’s available target platforms.</span></span>

![이식 가능한 라이브러리 만들기 대화 상자](./media/releasenotes-21-plib.png)

<span data-ttu-id="02a11-133">라이브러리가 빌드되고 명령이 실행 된 후에는 `nuget.exe pack MyPortableProject.csproj` 생성 된 NuGet 패키지의 콘텐츠를 검사 하 여 새 이식 가능한 라이브러리 패키지 폴더 구조를 볼 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="02a11-133">After the library is built and the command `nuget.exe pack MyPortableProject.csproj` is run, the new portable library package folder structure can be seen by examining the contents of the generated NuGet package.</span></span>

![이식 가능한 라이브러리 패키지 레이아웃](./media/releasenotes-21-plib-layout.png)

<span data-ttu-id="02a11-135">여기에서 볼 수 있듯이 이식 가능한 라이브러리 폴더 이름 규칙은 프레임 워크 식별자가 기존 [프레임 워크 이름 및 버전 규칙](../reference/target-frameworks.md)을 따르는 ' 이식 가능한-{framework 1} + {framework n} ' 패턴을 따릅니다.</span><span class="sxs-lookup"><span data-stu-id="02a11-135">As you can see, the portable library folder name convention follows the pattern ‘portable-{framework 1}+{framework n}’ where the framework identifiers follow the existing [framework name and version conventions](../reference/target-frameworks.md).</span></span> <span data-ttu-id="02a11-136">이름 및 버전 표기 규칙에 대 한 한 가지 예외는 Windows Phone에 사용 되는 프레임 워크 식별자에 있습니다.</span><span class="sxs-lookup"><span data-stu-id="02a11-136">One exception to the name and version conventions is found in the framework identifier used for Windows Phone.</span></span>  <span data-ttu-id="02a11-137">이 모니커는 프레임 워크 이름 ' wp ' (wp7, wp71 또는 wp8)를 사용 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="02a11-137">This moniker should use the framework name ‘wp’ (wp7, wp71 or wp8).</span></span> <span data-ttu-id="02a11-138">예를 들어 ' wp7 '를 사용 하면 오류가 발생 합니다.</span><span class="sxs-lookup"><span data-stu-id="02a11-138">Using ‘silverlight-wp7’, for example, will result in an error.</span></span>

<span data-ttu-id="02a11-139">이 폴더 구조에서 만들어진 패키지를 설치할 때 NuGet은 이제 폴더 이름에 지정 된 대로 여러 대상에 프레임 워크 및 프로필 규칙을 적용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="02a11-139">When installing the package that is created from this folder structure, NuGet can now apply its framework and profile rules to multiple targets, as specified in the folder name.</span></span>  <span data-ttu-id="02a11-140">NuGet의 일치 규칙을 사용 하는 경우 "보다 구체적인" 대상이 "less"의 대상 보다 우선적으로 적용 됩니다.</span><span class="sxs-lookup"><span data-stu-id="02a11-140">Behind NuGet’s matching rules is the principle that “more specific” targets will take precedence over “less specific” ones.</span></span>  <span data-ttu-id="02a11-141">즉, 특정 플랫폼을 대상으로 하는 모니커는 모두 프로젝트와 호환 되는 경우 항상 이식 가능한 것 보다 우선적으로 적용 됩니다.</span><span class="sxs-lookup"><span data-stu-id="02a11-141">This means that monikers targeting a specific platform will always be preferred over portable ones if they are both compatible with a project.</span></span>  <span data-ttu-id="02a11-142">또한 여러 휴대용 대상이 프로젝트와 호환 되는 경우 NuGet은 지원 되는 플랫폼 집합이 패키지를 참조 하는 프로젝트에 "가장 가까운" 것을 선호 합니다.</span><span class="sxs-lookup"><span data-stu-id="02a11-142">Additionally, if multiple portable targets are compatible with a project, NuGet will prefer the one where the set of platforms supported is “closest” to the project referencing the package.</span></span>

## <a name="targeting-windows-8-and-windows-phone-8-projects"></a><span data-ttu-id="02a11-143">Windows 8 및 Windows Phone 8 프로젝트를 대상으로 지정</span><span class="sxs-lookup"><span data-stu-id="02a11-143">Targeting Windows 8 and Windows Phone 8 Projects</span></span>

<span data-ttu-id="02a11-144">NuGet 2.1은 이식 가능한 라이브러리 프로젝트를 대상으로 하는 지원을 추가 하는 것 외에도 Windows 8 스토어 및 Windows Phone 8 프로젝트에 대 한 새로운 프레임 워크 모니커와 각 플랫폼의 이후 버전에서 보다 쉽게 관리할 수 있는 Windows 스토어 및 Windows Phone 프로젝트에 대 한 새로운 일반 모니커를 제공 합니다.</span><span class="sxs-lookup"><span data-stu-id="02a11-144">In addition to adding support for targeting portable library projects, NuGet 2.1 provides new framework monikers for both Windows 8 Store and Windows Phone 8 projects, as well as some new general monikers for Windows Store and Windows Phone projects that will be easier to manage across future versions of the respective platforms.</span></span>

<span data-ttu-id="02a11-145">Windows 8 스토어 응용 프로그램의 경우 식별자는 다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="02a11-145">For Windows 8 Store applications, the identifiers look as follows:</span></span>

| <span data-ttu-id="02a11-146">NuGet 2.0 및 이전 버전</span><span class="sxs-lookup"><span data-stu-id="02a11-146">NuGet 2.0 and earlier</span></span> | <span data-ttu-id="02a11-147">NuGet 2.1</span><span class="sxs-lookup"><span data-stu-id="02a11-147">NuGet 2.1</span></span> |
| ---------------- | ----------- |
| <span data-ttu-id="02a11-148">W i n,. NETCore45</span><span class="sxs-lookup"><span data-stu-id="02a11-148">winRT45, .NETCore45</span></span> | <span data-ttu-id="02a11-149">Windows, Windows8, win, win8</span><span class="sxs-lookup"><span data-stu-id="02a11-149">Windows, Windows8, win, win8</span></span> |

<br/>
<span data-ttu-id="02a11-150">Windows Phone 프로젝트의 경우 식별자는 다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="02a11-150">For Windows Phone projects, the identifiers look as follows:</span></span>

| <span data-ttu-id="02a11-151">전화 OS</span><span class="sxs-lookup"><span data-stu-id="02a11-151">Phone OS</span></span> | <span data-ttu-id="02a11-152">NuGet 2.0 및 이전 버전</span><span class="sxs-lookup"><span data-stu-id="02a11-152">NuGet 2.0 and earlier</span></span> | <span data-ttu-id="02a11-153">NuGet 2.1</span><span class="sxs-lookup"><span data-stu-id="02a11-153">NuGet 2.1</span></span> |
| --- | --- | --- |
| <span data-ttu-id="02a11-154">Windows Phone 7</span><span class="sxs-lookup"><span data-stu-id="02a11-154">Windows Phone 7</span></span> | <span data-ttu-id="02a11-155">silverlight3-wp</span><span class="sxs-lookup"><span data-stu-id="02a11-155">silverlight3-wp</span></span> | <span data-ttu-id="02a11-156">wp, wp7, Appname.windowsphone, WindowsPhone7</span><span class="sxs-lookup"><span data-stu-id="02a11-156">wp, wp7, WindowsPhone, WindowsPhone7</span></span> |
| <span data-ttu-id="02a11-157">Windows Phone 7.5 (망고)</span><span class="sxs-lookup"><span data-stu-id="02a11-157">Windows Phone 7.5 (Mango)</span></span> | <span data-ttu-id="02a11-158">silverlight4-wp71</span><span class="sxs-lookup"><span data-stu-id="02a11-158">silverlight4-wp71</span></span> | <span data-ttu-id="02a11-159">wp71, WindowsPhone71</span><span class="sxs-lookup"><span data-stu-id="02a11-159">wp71, WindowsPhone71</span></span> |
| <span data-ttu-id="02a11-160">Windows Phone 8</span><span class="sxs-lookup"><span data-stu-id="02a11-160">Windows Phone 8</span></span> | <span data-ttu-id="02a11-161">(지원되지 않음)</span><span class="sxs-lookup"><span data-stu-id="02a11-161">(not supported)</span></span> | <span data-ttu-id="02a11-162">wp8, WindowsPhone8</span><span class="sxs-lookup"><span data-stu-id="02a11-162">wp8, WindowsPhone8</span></span> |

<br/>
<span data-ttu-id="02a11-163">위의 모든 변경 내용에서 이전 프레임 워크 이름은 NuGet 2.1에서 계속 완벽 하 게 지원 됩니다.</span><span class="sxs-lookup"><span data-stu-id="02a11-163">In all of the above changes, the old framework names will continue to be fully supported by NuGet 2.1.</span></span>  <span data-ttu-id="02a11-164">앞으로 새 이름을 사용 하면 이후 버전의 해당 플랫폼에서 더 안정적으로 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="02a11-164">Moving forward, the new names should be used as they will be more stable across future versions of the respective platforms.</span></span> <span data-ttu-id="02a11-165">그러나 2.1 이전 버전에서는 새 이름이 지원 *되지* 않으므로 스위치를 만들 때 적절 하 게 계획 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="02a11-165">The new names will *not* be supported in versions of NuGet prior to 2.1, however, so plan accordingly for when to make the switch.</span></span>

## <a name="improved-search-in-package-manager-dialog"></a><span data-ttu-id="02a11-166">패키지 관리자 대화 상자에서 향상 된 검색 기능</span><span class="sxs-lookup"><span data-stu-id="02a11-166">Improved Search in Package Manager Dialog</span></span>

<span data-ttu-id="02a11-167">지난 몇 번의 반복을 통해 패키지 검색의 속도와 관련성이 크게 향상 된 NuGet 갤러리에 대 한 변경 내용이 도입 되었습니다.</span><span class="sxs-lookup"><span data-stu-id="02a11-167">Over the past several iterations, changes have been introduced to the NuGet gallery that greatly improved the speed and relevance of package searches.</span></span>  <span data-ttu-id="02a11-168">그러나 이러한 향상 된 기능은 nuget.org 웹 사이트로 제한 되었습니다.</span><span class="sxs-lookup"><span data-stu-id="02a11-168">However, these improvements were limited to the nuget.org Web site.</span></span>  <span data-ttu-id="02a11-169">NuGet 2.1은 NuGet 패키지 관리자 대화 상자를 통해 향상 된 검색 환경을 제공 합니다.</span><span class="sxs-lookup"><span data-stu-id="02a11-169">NuGet 2.1 makes the improved search experience available through the NuGet package manager dialog.</span></span>  <span data-ttu-id="02a11-170">예를 들어 Windows Azure 캐싱 미리 보기 패키지를 찾으려고 한다고 가정 합니다.</span><span class="sxs-lookup"><span data-stu-id="02a11-170">As an example, imagine that you wanted to find the Windows Azure Caching Preview package.</span></span>  <span data-ttu-id="02a11-171">이 패키지에 대 한 적절 한 검색 쿼리는 "Azure Cache" 일 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="02a11-171">A reasonable search query for this package may be “Azure Cache”.</span></span>  <span data-ttu-id="02a11-172">이전 버전의 패키지 관리자 대화 상자에서 원하는 패키지는 결과의 첫 번째 페이지에도 나열 되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="02a11-172">In previous versions of the package manager dialog, the desired package would not even be listed on the first page of results.</span></span>  <span data-ttu-id="02a11-173">그러나 NuGet 2.1에서는 원하는 패키지가 검색 결과의 맨 위에 표시 됩니다.</span><span class="sxs-lookup"><span data-stu-id="02a11-173">However, in NuGet 2.1, the desired package now shows up at the top of the search results.</span></span>

![패키지 관리자 대화 상자 검색](./media/releasenotes-21-vsdlg-search.png)

## <a name="force-package-update"></a><span data-ttu-id="02a11-175">패키지 강제 업데이트</span><span class="sxs-lookup"><span data-stu-id="02a11-175">Force Package Update</span></span>

<span data-ttu-id="02a11-176">NuGet 2.1 이전 버전에서는 NuGet이 패키지 업데이트를 건너뜁니다.</span><span class="sxs-lookup"><span data-stu-id="02a11-176">Prior to NuGet 2.1, NuGet would skip updating a package when there was a not a high version number.</span></span>  <span data-ttu-id="02a11-177">이는 특정 시나리오에 대 한 마찰을 도입 했습니다. 특히 팀에서 각 빌드와 함께 패키지 버전 번호를 증분 하지 않으려는 빌드 또는 CI 시나리오의 경우에는 특히 그렇습니다.</span><span class="sxs-lookup"><span data-stu-id="02a11-177">This introduced friction for certain scenarios – particularly in the case of build or CI scenarios where the team did not want to increment the package version number with each build.</span></span>  <span data-ttu-id="02a11-178">필요한 동작은에 관계 없이 업데이트를 적용 하는 것입니다.</span><span class="sxs-lookup"><span data-stu-id="02a11-178">The desired behavior was to force an update regardless.</span></span>  <span data-ttu-id="02a11-179">NuGet 2.1은 ' 다시 설치 ' 플래그를 사용 하 여이를 해결 합니다.</span><span class="sxs-lookup"><span data-stu-id="02a11-179">NuGet 2.1 addresses this with the ‘reinstall’ flag.</span></span>  <span data-ttu-id="02a11-180">예를 들어 이전 버전의 NuGet은 최신 패키지 버전이 없는 패키지를 업데이트 하려고 할 때 다음과 같은 결과가 발생 합니다.</span><span class="sxs-lookup"><span data-stu-id="02a11-180">For example, previous versions of NuGet would result in the following when attempting to update a package that did not have a more recent package version:</span></span>

```
PM> Update-Package Moq
No updates available for 'Moq' in project 'MySolution.MyConsole'.
```

<span data-ttu-id="02a11-181">다시 설치 플래그를 사용 하면 최신 버전이 있는지 여부에 관계 없이 패키지가 업데이트 됩니다.</span><span class="sxs-lookup"><span data-stu-id="02a11-181">With the reinstall flag, the package will be updated regardless of whether there is a newer version.</span></span>

```
PM> Update-Package Moq -Reinstall
Successfully removed 'Moq 4.0.10827' from MySolution.MyConsole.
Successfully uninstalled 'Moq 4.0.10827'.
Successfully installed 'Moq 4.0.10827'.
Successfully added 'Moq 4.0.10827' to MySolution.MyConsole.
```

<span data-ttu-id="02a11-182">다시 설치 플래그가 도움이 되는 또 다른 시나리오는 프레임 워크를 다시 대상으로 하는 것입니다.</span><span class="sxs-lookup"><span data-stu-id="02a11-182">Another scenario where the reinstall flag proves beneficial is that of framework re-targeting.</span></span> <span data-ttu-id="02a11-183">프로젝트의 대상 프레임 워크를 변경 하는 경우 (예: .NET 4에서 .NET 4.5으로) Update-Package-다시 설치는 프로젝트에 설치 된 모든 NuGet 패키지에 대 한 올바른 어셈블리에 대 한 참조를 업데이트할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="02a11-183">When changing the target framework of a project (for example, from .NET 4 to .NET 4.5), Update-Package -Reinstall can update references to the correct assemblies for all NuGet packages installed in the project.</span></span>

## <a name="edit-package-sources-within-visual-studio"></a><span data-ttu-id="02a11-184">Visual Studio 내에서 패키지 소스 편집</span><span class="sxs-lookup"><span data-stu-id="02a11-184">Edit Package Sources Within Visual Studio</span></span>

<span data-ttu-id="02a11-185">이전 버전의 NuGet에서 Visual Studio 옵션 대화 상자 내에서 패키지 소스를 업데이트 하려면 패키지 원본을 삭제 하 고 다시 추가 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="02a11-185">In previous versions of NuGet, updating a package source from within the Visual Studio options dialog required deleting and re-adding the package source.</span></span>  <span data-ttu-id="02a11-186">NuGet 2.1은 업데이트를 구성 사용자 인터페이스의 첫 번째 클래스 함수로 지원 하 여이 워크플로를 개선 합니다.</span><span class="sxs-lookup"><span data-stu-id="02a11-186">NuGet 2.1 improves this workflow by supporting update as a first class function of the configuration user interface.</span></span>

![패키지 관리자 구성 대화 상자](./media/releasenotes-21-edit-pkg-source.png)

## <a name="bug-fixes"></a><span data-ttu-id="02a11-188">버그 픽스</span><span class="sxs-lookup"><span data-stu-id="02a11-188">Bug Fixes</span></span>

<span data-ttu-id="02a11-189">NuGet 2.1에는 많은 버그 수정이 포함 되어 있습니다.</span><span class="sxs-lookup"><span data-stu-id="02a11-189">NuGet 2.1 includes many bug fixes.</span></span> <span data-ttu-id="02a11-190">NuGet 2.0에서 수정 된 작업 항목의 전체 목록은 [이 릴리스에 대 한 Nuget 문제 추적기](http://nuget.codeplex.com/workitem/list/advanced?keyword=&status=Fixed&type=All&priority=All&release=NuGet%202.1&assignedTo=All&component=All&sortField=LastUpdatedDate&sortDirection=Descending&page=0)를 확인 하세요.</span><span class="sxs-lookup"><span data-stu-id="02a11-190">For a full list of work items fixed in NuGet 2.0, please view the [NuGet Issue Tracker for this release](http://nuget.codeplex.com/workitem/list/advanced?keyword=&status=Fixed&type=All&priority=All&release=NuGet%202.1&assignedTo=All&component=All&sortField=LastUpdatedDate&sortDirection=Descending&page=0).</span></span>
