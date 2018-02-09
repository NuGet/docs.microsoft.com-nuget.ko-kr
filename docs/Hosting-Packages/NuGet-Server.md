---
title: "NuGet.Server를 사용하여 NuGet 피드 호스트 | Microsoft Docs"
author: kraigb
ms.author: kraigb
manager: ghogen
ms.date: 08/25/2017
ms.topic: article
ms.prod: nuget
ms.technology: 
description: "NuGet.Server를 사용하여 IIS를 실행하는 모든 서버에서 NuGet 패키지 피드를 만들고 호스트하는 방법입니다. OData 및 HTTP를 통해 패키지를 사용할 수 있습니다."
keywords: "NuGet 피드, NuGet 갤러리, 원격 패키지 피드, NuGet.Server"
ms.reviewer:
- karann-msft
- unniravindranathan
ms.openlocfilehash: 4cb3f04954fac1b4a39284be187776ab4a19b364
ms.sourcegitcommit: 4651b16a3a08f6711669fc4577f5d63b600f8f58
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 02/02/2018
---
# <a name="nugetserver"></a><span data-ttu-id="b55d4-104">NuGet.Server</span><span class="sxs-lookup"><span data-stu-id="b55d4-104">NuGet.Server</span></span>

<span data-ttu-id="b55d4-105">NuGet.Server는 IIS를 실행하는 모든 서버에서 패키지 피드를 호스트할 수 있는 ASP.NET 응용 프로그램을 만드는 .NET Foundation에서 제공하는 패키지입니다.</span><span class="sxs-lookup"><span data-stu-id="b55d4-105">NuGet.Server is a package provided by the .NET Foundation that creates an ASP.NET application that can host a package feed on any server that runs IIS.</span></span> <span data-ttu-id="b55d4-106">간단히 말해 NuGet.Server를 사용하면 HTTP(S)(특히 OData)를 통해 사용할 수 있는 서버에서 폴더를 만들 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="b55d4-106">Simply said, NuGet.Server makes a folder on the server available through HTTP(S) (specifically OData).</span></span> <span data-ttu-id="b55d4-107">쉽게 설정할 수 있고 간단한 시나리오에 가장 적합합니다.</span><span class="sxs-lookup"><span data-stu-id="b55d4-107">It's easy to set up and is best for simple scenarios.</span></span>

1. <span data-ttu-id="b55d4-108">Visual Studio에서 빈 ASP.NET 웹 응용 프로그램을 만들고 여기에 NuGet.Server 패키지를 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="b55d4-108">Create an empty ASP.NET Web application in Visual Studio and add the NuGet.Server package to it.</span></span>
1. <span data-ttu-id="b55d4-109">응용 프로그램에서 `Packages` 폴더를 구성하고 패키지를 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="b55d4-109">Configure the `Packages` folder in the application and add packages.</span></span>
1. <span data-ttu-id="b55d4-110">응용 프로그램을 적합한 서버에 배포합니다.</span><span class="sxs-lookup"><span data-stu-id="b55d4-110">Deploy the application to a suitable server.</span></span>

<span data-ttu-id="b55d4-111">다음 섹션에서는 C#을 사용하여 이 프로세스를 설명합니다.</span><span class="sxs-lookup"><span data-stu-id="b55d4-111">The following sections walk through this process in detail, using C#.</span></span>

## <a name="create-and-deploy-an-aspnet-web-application-with-nugetserver"></a><span data-ttu-id="b55d4-112">NuGet.Server를 사용하여 ASP.NET 웹 응용 프로그램 만들기 및 배포</span><span class="sxs-lookup"><span data-stu-id="b55d4-112">Create and deploy an ASP.NET Web application with NuGet.Server</span></span>

1. <span data-ttu-id="b55d4-113">Visual Studio에서 **파일 > 새로 만들기 > 프로젝트**를 선택하고, .NET Framework 4.6에 대한 대상 프레임워크를 설정하고(아래 참조), "ASP.NET"을 검색하고, C#에 대한 **ASP.NET 웹 응용 프로그램(.NET Framework)** 템플릿을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="b55d4-113">In Visual Studio, select **File > New > Project**, set the target framework for .NET Framework 4.6 (see below), search for "ASP.NET", and select the **ASP.NET Web Application (.NET Framework)** template for C#.</span></span>

    ![.NET Framework 대상을 4.6으로 설정](media/Hosting_01-NuGet.Server-Set4.6.png)

1. <span data-ttu-id="b55d4-115">응용 프로그램에 NuGet.Server가 *아닌* 적합한 이름을 입력하고, 확인을 선택하고, 다음 대화 상자에서 **빈** 템플릿을 선택하고, 확인을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="b55d4-115">Give the application a suitable name *other* than NuGet.Server, select OK, and in the next dialog select the **Empty** template and select OK.</span></span>

1. <span data-ttu-id="b55d4-116">.NET Framework 4.6을 대상으로 하는 경우 프로젝트를 마우스 오른쪽 단추로 클릭하고, **NuGet 패키지 관리**를 선택하고, 패키지 관리자 UI에서 최신 버전의 NuGet.Server 패키지를 검색하고 설치합니다.</span><span class="sxs-lookup"><span data-stu-id="b55d4-116">Right-click the project, select **Manage NuGet Packages**, and in the Package Manager UI search and install the latest version of the NuGet.Server package if you're targeting .NET Framework 4.6.</span></span> <span data-ttu-id="b55d4-117">(`Install-Package NuGet.Server`를 사용하여 패키지 관리자 콘솔에서 설치할 수도 있습니다.)</span><span class="sxs-lookup"><span data-stu-id="b55d4-117">(You can also install it from the Package Manager Console with `Install-Package NuGet.Server`.)</span></span>

    ![NuGet.Server 패키지 설치](media/Hosting_02-NuGet.Server-Package.png)

    > [!Important]
    > <span data-ttu-id="b55d4-119">웹 응용 프로그램이 .NET Framework 4.5.2를 대상으로 하는 경우 대신 NuGet Server **2.10.3**을 설치해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="b55d4-119">If your web application targets .NET Framework 4.5.2, you must install NuGet Server **2.10.3** instead.</span></span>

1. <span data-ttu-id="b55d4-120">NuGet.Server를 설치하면 빈 웹 응용 프로그램을 패키지 소스로 변환합니다.</span><span class="sxs-lookup"><span data-stu-id="b55d4-120">Installing NuGet.Server converts the empty Web application into a package source.</span></span> <span data-ttu-id="b55d4-121">응용 프로그램에서 `Packages` 폴더를 만들고 `web.config`를 덮어써서 추가 설정이 포함됩니다(자세한 내용은 해당 파일에 있는 설명 참조).</span><span class="sxs-lookup"><span data-stu-id="b55d4-121">It creates a `Packages` folder in the application and overwrites `web.config` to include additional settings (see the comments in that file for details).</span></span>

1. <span data-ttu-id="b55d4-122">서버에 응용 프로그램을 게시할 때 피드에서 패키지를 사용하려면 해당 `.nupkg` 파일을 Visual Studio의 `Packages` 폴더에 추가한 다음 **빌드 작업**을 **콘텐츠**로 설정하고, **출력 디렉터리로 복사**를 **항상 복사**로 설정합니다.</span><span class="sxs-lookup"><span data-stu-id="b55d4-122">To make packages available in the feed when you publish the application to a server, add their `.nupkg` files to the `Packages` folder in Visual Studio, then set their **Build Action** to **Content** and **Copy to Output Directory** to **Copy always**:</span></span>

    ![프로젝트의 패키지 폴더에 패키지 복사](media/Hosting_03-NuGet.Server-Package-Folder.png)

1. <span data-ttu-id="b55d4-124">Visual Studio에서 로컬로 사이트를 실행합니다(디버깅하지 않음, Ctrl+F5).</span><span class="sxs-lookup"><span data-stu-id="b55d4-124">Run the site locally in Visual Studio (without debugging, that is Ctrl+F5).</span></span> <span data-ttu-id="b55d4-125">홈페이지에서는 패키지 피드 URL을 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="b55d4-125">The home page provides the package feed URLs:</span></span>

    ![NuGet.Server에서 응용 프로그램의 기본 홈페이지](media/Hosting_04-NuGet.Server-FeedHomePage.png)

1. <span data-ttu-id="b55d4-127">위에서 설명한 영역의 **여기**를 클릭하여 패키지의 OData 피드를 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="b55d4-127">Click on **here** in the area outlined above to see the OData feed of packages.</span></span>

1. <span data-ttu-id="b55d4-128">처음으로 응용 프로그램을 실행하면 NuGet.Server에서는 각 패키지에 대한 폴더를 포함하도록 `Packages` 폴더를 다시 구성합니다.</span><span class="sxs-lookup"><span data-stu-id="b55d4-128">The first time you run the application, NuGet.Server restructures the `Packages` folder to contain a folder for each package.</span></span> <span data-ttu-id="b55d4-129">이렇게 하면 NuGet 3.3에서 도입한 [로컬 저장소 레이아웃](http://blog.nuget.org/20151118/nuget-3.3.html#folder-based-repository-commands)과 일치하여 성능을 향상시킵니다.</span><span class="sxs-lookup"><span data-stu-id="b55d4-129">This matches the [local storage layout](http://blog.nuget.org/20151118/nuget-3.3.html#folder-based-repository-commands) introduced with NuGet 3.3 to improve performance.</span></span> <span data-ttu-id="b55d4-130">패키지를 추가하는 경우 이 구조를 계속 진행합니다.</span><span class="sxs-lookup"><span data-stu-id="b55d4-130">When adding more packages, continue to follow this structure.</span></span>

1. <span data-ttu-id="b55d4-131">로컬 배포를 테스트하면 필요에 따라 다른 내부 또는 외부 사이트에 응용 프로그램을 배포합니다.</span><span class="sxs-lookup"><span data-stu-id="b55d4-131">Once you've tested your local deployment, deploy the application to any other internal or external site as needed.</span></span>
1. <span data-ttu-id="b55d4-132">`http://<domain>`에 배포되면 패키지 원본에 사용하는 URL은 `http://<domain>/nuget`입니다.</span><span class="sxs-lookup"><span data-stu-id="b55d4-132">Once deployed to `http://<domain>`, the URL that you use for the package source will be `http://<domain>/nuget`.</span></span>

## <a name="configuring-the-packages-folder"></a><span data-ttu-id="b55d4-133">패키지 폴더 구성</span><span class="sxs-lookup"><span data-stu-id="b55d4-133">Configuring the Packages folder</span></span>

<span data-ttu-id="b55d4-134">`NuGet.Server` 1.5 이상에서 `web.config`의 `appSetting/packagesPath` 값을 사용하여 패키지 폴더를 구체적으로 구성할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="b55d4-134">With `NuGet.Server` 1.5 and later, you can more specifically configure the package folder using the `appSetting/packagesPath` value in `web.config`:</span></span>

```xml
<appSettings>
    <!-- Set the value here to specify your custom packages folder. -->
    <add key="packagesPath" value="C:\MyPackages" />
</appSettings>
```

<span data-ttu-id="b55d4-135">`packagesPath`는 절대 또는 가상 경로일 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="b55d4-135">`packagesPath` can be an absolute or virtual path.</span></span>

<span data-ttu-id="b55d4-136">`packagesPath`를 생략하거나 비워 두면 패키지 폴더는 기본적으로 `~/Packages`입니다.</span><span class="sxs-lookup"><span data-stu-id="b55d4-136">When `packagesPath` is omitted or left blank, the packages folder is the default `~/Packages`.</span></span>

## <a name="adding-packages-to-the-feed-externally"></a><span data-ttu-id="b55d4-137">외부에서 피드에 패키지 추가</span><span class="sxs-lookup"><span data-stu-id="b55d4-137">Adding packages to the feed externally</span></span>

<span data-ttu-id="b55d4-138">NuGet.Server 사이트를 실행하면 `web.config`에서 API 키 값을 설정하기 위해 제공된 nuget.exe를 사용하여 패키지를 추가하거나 삭제할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="b55d4-138">Once a NuGet.Server site is running, you can add or delete packages using nuget.exe provided that you set an API key value in `web.config`.</span></span>

<span data-ttu-id="b55d4-139">NuGet.Server 패키지를 설치한 후에 `web.config`에는 빈 `appSetting/apiKey` 값이 포함됩니다.</span><span class="sxs-lookup"><span data-stu-id="b55d4-139">After installing the NuGet.Server package, `web.config` contains an empty `appSetting/apiKey` value:</span></span>

```xml
<appSettings>
    <add key="apiKey" value="" />
</appSettings>
```

<span data-ttu-id="b55d4-140">`apiKey`를 생략하거나 비워 두면 피드에 패키지를 푸시하는 작업이 비활성화됩니다.</span><span class="sxs-lookup"><span data-stu-id="b55d4-140">When `apiKey` is omitted or blank, pushing packages to the feed is disabled.</span></span>

<span data-ttu-id="b55d4-141">이 기능을 사용하려면 `apiKey`를 값(이상적으로 강력한 암호)으로 설정하고 `true` 값을 포함한 `appSettings/requireApiKey`라는 키를 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="b55d4-141">To enable this capability, set the `apiKey` to a value (ideally a strong password) and add a key called `appSettings/requireApiKey` with the value of `true`:</span></span>

```xml
<appSettings>
        <!-- Sets whether an API Key is required to push/delete packages -->
    <add key="requireApiKey" value="true" />

    <!-- Set a shared password (for all users) to push/delete packages -->
    <add key="apiKey" value="" />
</appSettings>
```

<span data-ttu-id="b55d4-142">서버가 이미 보호되거나 그렇지 않은 경우 API 키가 필요하지 않는 경우(예: 로컬 팀 네트워크에서 개인 서버를 사용하는 경우) `requireApiKey`를 `false`로 설정할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="b55d4-142">If your server is already secured or you do not otherwise require an API key (for example, when using a private server on a local team network), you can set `requireApiKey` to `false`.</span></span> <span data-ttu-id="b55d4-143">서버에 액세스할 수 있는 모든 사용자는 패키지를 푸시하거나 삭제할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="b55d4-143">All users with access to the server can then push or delete packages.</span></span>