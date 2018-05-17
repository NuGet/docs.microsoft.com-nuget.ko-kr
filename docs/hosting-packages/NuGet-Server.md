---
title: NuGet.Server를 사용하여 NuGet 피드 호스트
description: NuGet.Server를 사용하여 IIS를 실행하는 모든 서버에서 NuGet 패키지 피드를 만들고 호스트하는 방법입니다. OData 및 HTTP를 통해 패키지를 사용할 수 있습니다.
author: kraigb
ms.author: kraigb
manager: douge
ms.date: 03/13/2018
ms.topic: conceptual
ms.openlocfilehash: 55501eedf6c5fdf054a602536ee8c03e7048d5d5
ms.sourcegitcommit: 3eab9c4dd41ea7ccd2c28bb5ab16f6fbbec13708
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/26/2018
---
# <a name="nugetserver"></a><span data-ttu-id="a1761-103">NuGet.Server</span><span class="sxs-lookup"><span data-stu-id="a1761-103">NuGet.Server</span></span>

<span data-ttu-id="a1761-104">NuGet.Server는 IIS를 실행하는 모든 서버에서 패키지 피드를 호스트할 수 있는 ASP.NET 응용 프로그램을 만드는 .NET Foundation에서 제공하는 패키지입니다.</span><span class="sxs-lookup"><span data-stu-id="a1761-104">NuGet.Server is a package provided by the .NET Foundation that creates an ASP.NET application that can host a package feed on any server that runs IIS.</span></span> <span data-ttu-id="a1761-105">간단히 말해 NuGet.Server를 사용하면 HTTP(S)(특히 OData)를 통해 사용할 수 있는 서버에서 폴더를 만들 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="a1761-105">Simply said, NuGet.Server makes a folder on the server available through HTTP(S) (specifically OData).</span></span> <span data-ttu-id="a1761-106">쉽게 설정할 수 있고 간단한 시나리오에 가장 적합합니다.</span><span class="sxs-lookup"><span data-stu-id="a1761-106">It's easy to set up and is best for simple scenarios.</span></span>

1. <span data-ttu-id="a1761-107">Visual Studio에서 빈 ASP.NET 웹 응용 프로그램을 만들고 여기에 NuGet.Server 패키지를 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="a1761-107">Create an empty ASP.NET Web application in Visual Studio and add the NuGet.Server package to it.</span></span>
1. <span data-ttu-id="a1761-108">응용 프로그램에서 `Packages` 폴더를 구성하고 패키지를 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="a1761-108">Configure the `Packages` folder in the application and add packages.</span></span>
1. <span data-ttu-id="a1761-109">응용 프로그램을 적합한 서버에 배포합니다.</span><span class="sxs-lookup"><span data-stu-id="a1761-109">Deploy the application to a suitable server.</span></span>

<span data-ttu-id="a1761-110">다음 섹션에서는 C#을 사용하여 이 프로세스를 설명합니다.</span><span class="sxs-lookup"><span data-stu-id="a1761-110">The following sections walk through this process in detail, using C#.</span></span>

<span data-ttu-id="a1761-111">NuGet.Server에 대해 추가 질문이 있으면 [https://github.com/nuget/NuGetGallery/issues](https://github.com/nuget/NuGetGallery/issues)에서 문제를 제출하세요.</span><span class="sxs-lookup"><span data-stu-id="a1761-111">If you have further questions about NuGet.Server, create an issue on [https://github.com/nuget/NuGetGallery/issues](https://github.com/nuget/NuGetGallery/issues).</span></span>

## <a name="create-and-deploy-an-aspnet-web-application-with-nugetserver"></a><span data-ttu-id="a1761-112">NuGet.Server를 사용하여 ASP.NET 웹 응용 프로그램 만들기 및 배포</span><span class="sxs-lookup"><span data-stu-id="a1761-112">Create and deploy an ASP.NET Web application with NuGet.Server</span></span>

1. <span data-ttu-id="a1761-113">Visual Studio에서 **파일 > 새로 만들기 > 프로젝트**를 선택하고, "ASP.NET"을 검색하고, C#에 대한 **ASP.NET 웹 응용 프로그램(.NET Framework)** 템플릿을 선택하고, **프레임워크**를 ".NET Framework 4.6"으로 설정합니다.</span><span class="sxs-lookup"><span data-stu-id="a1761-113">In Visual Studio, select **File > New > Project**, search for "ASP.NET", select the **ASP.NET Web Application (.NET Framework)** template for C#, and set **Framework** to ".NET Framework 4.6":</span></span>

    ![새 프로젝트의 대상 프레임워크 설정](media/Hosting_01-NuGet.Server-Set4.6.png)

1. <span data-ttu-id="a1761-115">응용 프로그램에 NuGet.Server가 *아닌* 적합한 이름을 입력하고, 확인을 선택하고, 다음 대화 상자에서 **빈** 템플릿을 선택한 다음, **확인**을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="a1761-115">Give the application a suitable name *other* than NuGet.Server, select OK, and in the next dialog select the **Empty** template, then select **OK**.</span></span>

1. <span data-ttu-id="a1761-116">프로젝트를 마우스 오른쪽 단추로 클릭하고 **NuGet 패키지 관리**를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="a1761-116">Right-click the project, select **Manage NuGet Packages**.</span></span>

1. <span data-ttu-id="a1761-117">.NET Framework 4.6을 대상으로 하는 경우 패키지 관리자 UI에서 **찾아보기** 탭을 선택한 후, 최신 버전의 NuGet.Server 패키지를 검색하고 설치합니다.</span><span class="sxs-lookup"><span data-stu-id="a1761-117">In the Package Manager UI, select the **Browse** tab, then search and install the latest version of the NuGet.Server package if you're targeting .NET Framework 4.6.</span></span> <span data-ttu-id="a1761-118">(`Install-Package NuGet.Server`를 사용하여 패키지 관리자 콘솔에서 설치할 수도 있습니다.) 메시지가 표시되면 사용 약관에 동의합니다.</span><span class="sxs-lookup"><span data-stu-id="a1761-118">(You can also install it from the Package Manager Console with `Install-Package NuGet.Server`.) Accept the license terms if prompted.</span></span>

    ![NuGet.Server 패키지 설치](media/Hosting_02-NuGet.Server-Package.png)

1. <span data-ttu-id="a1761-120">NuGet.Server를 설치하면 빈 웹 응용 프로그램을 패키지 소스로 변환합니다.</span><span class="sxs-lookup"><span data-stu-id="a1761-120">Installing NuGet.Server converts the empty Web application into a package source.</span></span> <span data-ttu-id="a1761-121">응용 프로그램에서 다양한 기타 패키지를 설치하고, `Packages` 폴더를 만들고, `web.config`를 수정하여 추가 설정이 포함됩니다(자세한 내용은 해당 파일에 있는 설명 참조).</span><span class="sxs-lookup"><span data-stu-id="a1761-121">It installs a variety of other packages, creates a `Packages` folder in the application, and modifies `web.config` to include additional settings (see the comments in that file for details).</span></span>

    > [!Important]
    > <span data-ttu-id="a1761-122">NuGet.Server 패키지가 해당 파일에 대한 수정을 완료한 후에는 `web.config`를 자세히 살펴봅니다.</span><span class="sxs-lookup"><span data-stu-id="a1761-122">Carefully inspect `web.config` after the NuGet.Server package has completed its modifications to that file.</span></span> <span data-ttu-id="a1761-123">NuGet.Server는 기존 요소를 덮어쓰지 않는 대신 중복 요소를 만들 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="a1761-123">NuGet.Server may not overwrite existing elements but instead create duplicate elements.</span></span> <span data-ttu-id="a1761-124">나중에 프로젝트를 실행하려고 할 때 이러한 중복 요소로 인해 "내부 서버 오류"가 발생합니다.</span><span class="sxs-lookup"><span data-stu-id="a1761-124">Those duplicates will cause an "Internal Server Error" when you later try to run the project.</span></span> <span data-ttu-id="a1761-125">예를 들어 NuGet.Server를 설치하기 전에 `web.config`에 `<compilation debug="true" targetFramework="4.5.2" />`가 포함된 경우 패키지에서 이를 덮어쓰는 대신 두 번째 `<compilation debug="true" targetFramework="4.6" />`을 삽입합니다.</span><span class="sxs-lookup"><span data-stu-id="a1761-125">For example, if your `web.config` contains `<compilation debug="true" targetFramework="4.5.2" />` before installing NuGet.Server, the package doesn't overwrite it but inserts a second `<compilation debug="true" targetFramework="4.6" />`.</span></span> <span data-ttu-id="a1761-126">이 경우 이전 프레임워크 버전을 사용하여 요소를 삭제합니다.</span><span class="sxs-lookup"><span data-stu-id="a1761-126">In that case, delete the element with the older framework version.</span></span>

1. <span data-ttu-id="a1761-127">서버에 응용 프로그램을 게시할 때 피드에서 패키지를 사용하려면 각 `.nupkg` 파일을 Visual Studio의 `Packages` 폴더에 추가한 다음, **빌드 작업**을 **콘텐츠**로 설정하고, **출력 디렉터리로 복사**를 **항상 복사**로 설정합니다.</span><span class="sxs-lookup"><span data-stu-id="a1761-127">To make packages available in the feed when you publish the application to a server, add each `.nupkg` files to the `Packages` folder in Visual Studio, then set each one's **Build Action** to **Content** and **Copy to Output Directory** to **Copy always**:</span></span>

    ![프로젝트의 패키지 폴더에 패키지 복사](media/Hosting_03-NuGet.Server-Package-Folder.png)

1. <span data-ttu-id="a1761-129">Visual Studio에서 로컬로 사이트를 실행합니다(**디버그 > 디버깅 없이 시작** 또는 Ctrl+F5 사용).</span><span class="sxs-lookup"><span data-stu-id="a1761-129">Run the site locally in Visual Studio (using **Debug > Start Without Debugging** or Ctrl+F5).</span></span> <span data-ttu-id="a1761-130">홈 페이지에서는 아래 표시된 것처럼 패키지 피드 URL을 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="a1761-130">The home page provides the package feed URLs as shown below.</span></span> <span data-ttu-id="a1761-131">오류가 표시될 경우 앞서 5단계에서 설명한 것처럼 중복 요소가 있는지 `web.config`를 자세히 살펴보세요.</span><span class="sxs-lookup"><span data-stu-id="a1761-131">If you see errors, carefully inspect your `web.config` for duplicate elements are noted earlier with step 5.</span></span>

    ![NuGet.Server에서 응용 프로그램의 기본 홈페이지](media/Hosting_04-NuGet.Server-FeedHomePage.png)

1. <span data-ttu-id="a1761-133">위에서 설명한 영역의 **여기**를 클릭하여 패키지의 OData 피드를 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="a1761-133">Click on **here** in the area outlined above to see the OData feed of packages.</span></span>

1. <span data-ttu-id="a1761-134">처음으로 응용 프로그램을 실행하면 NuGet.Server에서는 각 패키지에 대한 폴더를 포함하도록 `Packages` 폴더를 다시 구성합니다.</span><span class="sxs-lookup"><span data-stu-id="a1761-134">The first time you run the application, NuGet.Server restructures the `Packages` folder to contain a folder for each package.</span></span> <span data-ttu-id="a1761-135">이렇게 하면 NuGet 3.3에서 도입한 [로컬 저장소 레이아웃](http://blog.nuget.org/20151118/nuget-3.3.html#folder-based-repository-commands)과 일치하여 성능을 향상시킵니다.</span><span class="sxs-lookup"><span data-stu-id="a1761-135">This matches the [local storage layout](http://blog.nuget.org/20151118/nuget-3.3.html#folder-based-repository-commands) introduced with NuGet 3.3 to improve performance.</span></span> <span data-ttu-id="a1761-136">패키지를 추가하는 경우 이 구조를 계속 진행합니다.</span><span class="sxs-lookup"><span data-stu-id="a1761-136">When adding more packages, continue to follow this structure.</span></span>

1. <span data-ttu-id="a1761-137">로컬 배포를 테스트하면 필요에 따라 다른 내부 또는 외부 사이트에 응용 프로그램을 배포합니다.</span><span class="sxs-lookup"><span data-stu-id="a1761-137">Once you've tested your local deployment, deploy the application to any other internal or external site as needed.</span></span>

1. <span data-ttu-id="a1761-138">`http://<domain>`에 배포되면 패키지 원본에 사용하는 URL은 `http://<domain>/nuget`입니다.</span><span class="sxs-lookup"><span data-stu-id="a1761-138">Once deployed to `http://<domain>`, the URL that you use for the package source will be `http://<domain>/nuget`.</span></span>

## <a name="configuring-the-packages-folder"></a><span data-ttu-id="a1761-139">패키지 폴더 구성</span><span class="sxs-lookup"><span data-stu-id="a1761-139">Configuring the Packages folder</span></span>

<span data-ttu-id="a1761-140">`NuGet.Server` 1.5 이상에서 `web.config`의 `appSetting/packagesPath` 값을 사용하여 패키지 폴더를 구체적으로 구성할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="a1761-140">With `NuGet.Server` 1.5 and later, you can more specifically configure the package folder using the `appSetting/packagesPath` value in `web.config`:</span></span>

```xml
<appSettings>
    <!-- Set the value here to specify your custom packages folder. -->
    <add key="packagesPath" value="C:\MyPackages" />
</appSettings>
```

<span data-ttu-id="a1761-141">`packagesPath`는 절대 또는 가상 경로일 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="a1761-141">`packagesPath` can be an absolute or virtual path.</span></span>

<span data-ttu-id="a1761-142">`packagesPath`를 생략하거나 비워 두면 패키지 폴더는 기본적으로 `~/Packages`입니다.</span><span class="sxs-lookup"><span data-stu-id="a1761-142">When `packagesPath` is omitted or left blank, the packages folder is the default `~/Packages`.</span></span>

## <a name="adding-packages-to-the-feed-externally"></a><span data-ttu-id="a1761-143">외부에서 피드에 패키지 추가</span><span class="sxs-lookup"><span data-stu-id="a1761-143">Adding packages to the feed externally</span></span>

<span data-ttu-id="a1761-144">NuGet.Server 사이트를 실행하면 `web.config`에서 API 키 값을 설정하기 위해 제공된 [nuget push](../tools/cli-ref-push.md)를 사용하여 패키지를 추가할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="a1761-144">Once a NuGet.Server site is running, you can add packages using [nuget push](../tools/cli-ref-push.md) provided that you set an API key value in `web.config`.</span></span>

<span data-ttu-id="a1761-145">NuGet.Server 패키지를 설치한 후에 `web.config`에는 빈 `appSetting/apiKey` 값이 포함됩니다.</span><span class="sxs-lookup"><span data-stu-id="a1761-145">After installing the NuGet.Server package, `web.config` contains an empty `appSetting/apiKey` value:</span></span>

```xml
<appSettings>
    <add key="apiKey" value="" />
</appSettings>
```

<span data-ttu-id="a1761-146">`apiKey`를 생략하거나 비워 두면 피드에 패키지를 푸시하는 작업이 비활성화됩니다.</span><span class="sxs-lookup"><span data-stu-id="a1761-146">When `apiKey` is omitted or blank, pushing packages to the feed is disabled.</span></span>

<span data-ttu-id="a1761-147">이 기능을 사용하려면 `apiKey`를 값(이상적으로 강력한 암호)으로 설정하고 `true` 값을 포함한 `appSettings/requireApiKey`라는 키를 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="a1761-147">To enable this capability, set the `apiKey` to a value (ideally a strong password) and add a key called `appSettings/requireApiKey` with the value of `true`:</span></span>

```xml
<appSettings>
        <!-- Sets whether an API Key is required to push/delete packages -->
    <add key="requireApiKey" value="true" />

    <!-- Set a shared password (for all users) to push/delete packages -->
    <add key="apiKey" value="" />
</appSettings>
```

<span data-ttu-id="a1761-148">서버가 이미 보호되거나 그렇지 않은 경우 API 키가 필요하지 않는 경우(예: 로컬 팀 네트워크에서 개인 서버를 사용하는 경우) `requireApiKey`를 `false`로 설정할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="a1761-148">If your server is already secured or you do not otherwise require an API key (for example, when using a private server on a local team network), you can set `requireApiKey` to `false`.</span></span> <span data-ttu-id="a1761-149">서버에 액세스할 수 있는 모든 사용자는 패키지를 푸시할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="a1761-149">All users with access to the server can then push packages.</span></span>

## <a name="removing-packages-from-the-feed"></a><span data-ttu-id="a1761-150">피드에서 패키지 제거</span><span class="sxs-lookup"><span data-stu-id="a1761-150">Removing packages from the feed</span></span>

<span data-ttu-id="a1761-151">NuGet.Server에서 [nuget delete](../tools/cli-ref-delete.md) 명령은 주석과 API 키를 포함한 경우 리포지토리에서 패키지를 제거합니다.</span><span class="sxs-lookup"><span data-stu-id="a1761-151">With NuGet.Server, the [nuget delete](../tools/cli-ref-delete.md) command removes a package from the repository provided that you include the API key with the comment.</span></span>

<span data-ttu-id="a1761-152">이 동작을 패키지 목록을 해제하는 것으로 변경하려면(패키지 복원에 사용할 수 있게 유지) `web.config`의 `enableDelisting` 키를 true로 변경하세요.</span><span class="sxs-lookup"><span data-stu-id="a1761-152">If you want to change the behavior to delist the package instead (leaving it available for package restore), change the `enableDelisting` key in `web.config` to true.</span></span>

## <a name="nugetserver-support"></a><span data-ttu-id="a1761-153">NuGet.Server 지원</span><span class="sxs-lookup"><span data-stu-id="a1761-153">NuGet.Server support</span></span>

<span data-ttu-id="a1761-154">NuGet.Server 사용 시 추가 도움이 필요할 경우 [https://github.com/nuget/NuGetGallery/issues](https://github.com/nuget/NuGetGallery/issues)에서 문제를 제출하세요.</span><span class="sxs-lookup"><span data-stu-id="a1761-154">For additional help using NuGet.Server, create an issue on [https://github.com/nuget/NuGetGallery/issues](https://github.com/nuget/NuGetGallery/issues).</span></span>