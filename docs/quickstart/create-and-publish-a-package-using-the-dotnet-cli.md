---
title: dotnet CLI를 사용하여 NuGet 패키지 만들기 및 게시
description: .NET Core CLI, dotnet을 사용하여 NuGet 패키지를 만들고 게시하는 방법에 대한 연습 자습서입니다.
author: karann-msft
ms.author: karann
ms.date: 05/24/2019
ms.topic: quickstart
ms.openlocfilehash: f663b1b2176a5f0ae5bc6d82873193638e0efdaa
ms.sourcegitcommit: ba8ad1bd13a4bba3df94374e34e20c425a05af2f
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/06/2019
ms.locfileid: "68833390"
---
# <a name="quickstart-create-and-publish-a-package-dotnet-cli"></a><span data-ttu-id="4e992-103">빠른 시작: 패키지 만들기 및 게시(dotnet CLI)</span><span class="sxs-lookup"><span data-stu-id="4e992-103">Quickstart: Create and publish a package (dotnet CLI)</span></span>

<span data-ttu-id="4e992-104">.NET 클래스 라이브러리에서 NuGet 패키지를 만들고 `dotnet` CLI(명령줄 인터페이스)를 사용하여 nuget.org에 게시하는 간단한 과정입니다.</span><span class="sxs-lookup"><span data-stu-id="4e992-104">It's a simple process to create a NuGet package from a .NET Class Library and publish it to nuget.org using the `dotnet` command-line interface (CLI).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="4e992-105">전제 조건</span><span class="sxs-lookup"><span data-stu-id="4e992-105">Prerequisites</span></span>

1. <span data-ttu-id="4e992-106">`dotnet` CLI를 포함하는 [.NET Core SDK](https://www.microsoft.com/net/download/)를 설치합니다.</span><span class="sxs-lookup"><span data-stu-id="4e992-106">Install the [.NET Core SDK](https://www.microsoft.com/net/download/), which includes the `dotnet` CLI.</span></span> <span data-ttu-id="4e992-107">Visual Studio 2017부터 dotnet CLI는 모든 .NET Core 관련 워크로드와 함께 자동으로 설치됩니다.</span><span class="sxs-lookup"><span data-stu-id="4e992-107">Starting in Visual Studio 2017, the dotnet CLI is automatically installed with any .NET Core related workloads.</span></span>

1. <span data-ttu-id="4e992-108">아직 없는 경우 [nuget.org에 체험 계정을 등록](https://www.nuget.org/users/account/LogOn?returnUrl=%2F)합니다.</span><span class="sxs-lookup"><span data-stu-id="4e992-108">[Register for a free account on nuget.org](https://www.nuget.org/users/account/LogOn?returnUrl=%2F) if you don't have one already.</span></span> <span data-ttu-id="4e992-109">새 계정을 만들면 확인 전자 메일을 보냅니다.</span><span class="sxs-lookup"><span data-stu-id="4e992-109">Creating a new account sends a confirmation email.</span></span> <span data-ttu-id="4e992-110">패키지를 업로드하려면 먼저 계정을 확인해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="4e992-110">You must confirm the account before you can upload a package.</span></span>

## <a name="create-a-class-library-project"></a><span data-ttu-id="4e992-111">클래스 라이브러리 프로젝트 만들기</span><span class="sxs-lookup"><span data-stu-id="4e992-111">Create a class library project</span></span>

<span data-ttu-id="4e992-112">패키지할 코드에 대해 기존 .NET 클래스 라이브러리 프로젝트를 사용하거나 다음과 같이 간단한 프로젝트를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="4e992-112">You can use an existing .NET Class Library project for the code you want to package, or create a simple one as follows:</span></span>

1. <span data-ttu-id="4e992-113">`AppLogger`라는 폴더를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="4e992-113">Create a folder called `AppLogger`.</span></span>

1. <span data-ttu-id="4e992-114">명령 프롬프트를 열고 `AppLogger` 폴더로 전환합니다.</span><span class="sxs-lookup"><span data-stu-id="4e992-114">Open a command prompt and switch to the `AppLogger` folder.</span></span>

1. <span data-ttu-id="4e992-115">프로젝트의 현재 폴더 이름을 사용하는 `dotnet new classlib`를 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="4e992-115">Type `dotnet new classlib`, which uses the name of the current folder for the project.</span></span>

   <span data-ttu-id="4e992-116">이렇게 하면 새 프로젝트가 생성됩니다.</span><span class="sxs-lookup"><span data-stu-id="4e992-116">This creates the new project.</span></span>

1. <span data-ttu-id="4e992-117">`dotnet run`을 사용하여 앱이 제대로 만들어졌는지 테스트합니다.</span><span class="sxs-lookup"><span data-stu-id="4e992-117">Use `dotnet run` to test that the app has been created properly.</span></span>

## <a name="add-package-metadata-to-the-project-file"></a><span data-ttu-id="4e992-118">프로젝트 파일에 패키지 메타데이터 추가</span><span class="sxs-lookup"><span data-stu-id="4e992-118">Add package metadata to the project file</span></span>

<span data-ttu-id="4e992-119">모든 NuGet 패키지에는 패키지의 콘텐츠와 종속성을 설명하는 매니페스트가 필요합니다.</span><span class="sxs-lookup"><span data-stu-id="4e992-119">Every NuGet package needs a manifest that describes the package's contents and dependencies.</span></span> <span data-ttu-id="4e992-120">마지막 패키지에서 매니페스트는 프로젝트 파일에 포함하는 NuGet 메타데이터 속성에서 생성되는 `.nuspec` 파일입니다.</span><span class="sxs-lookup"><span data-stu-id="4e992-120">In a final package, the manifest is a `.nuspec` file that is generated from the NuGet metadata properties that you include in the project file.</span></span>

1. <span data-ttu-id="4e992-121">프로젝트 파일(`.csproj`)을 열고 종료 `<PropertyGroup>` 태그 내부에 다음 최소 속성을 추가하여 값을 적절하게 변경합니다.</span><span class="sxs-lookup"><span data-stu-id="4e992-121">Open your project file (`.csproj`) and add the following minimal properties inside the existing `<PropertyGroup>` tag, changing the values as appropriate:</span></span>

    ```xml
    <PackageId>AppLogger</PackageId>
    <Version>1.0.0</Version>
    <Authors>your_name</Authors>
    <Company>your_company</Company>
    ```

    > [!Important]
    > <span data-ttu-id="4e992-122">nuget.org 또는 무엇이든 사용 중인 호스트에서 고유한 식별자를 패키지에 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="4e992-122">Give the package an identifier that's unique across nuget.org or whatever host you're using.</span></span> <span data-ttu-id="4e992-123">이 연습에서는 나중 게시 단계에서 패키지를 공개적으로 표시할 수 있도록 이름에 “샘플” 또는 “테스트”를 포함하는 것이 좋습니다(실제로 아무도 사용할 가능성이 없더라도).</span><span class="sxs-lookup"><span data-stu-id="4e992-123">For this walkthrough we recommend including "Sample" or "Test" in the name as the later publishing step does make the package publicly visible (though it's unlikely anyone will actually use it).</span></span>

1. <span data-ttu-id="4e992-124">[NuGet 메타데이터 속성](/dotnet/core/tools/csproj#nuget-metadata-properties)에 설명된 선택적 속성을 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="4e992-124">Add any optional properties described on [NuGet metadata properties](/dotnet/core/tools/csproj#nuget-metadata-properties).</span></span>

    > [!Note]
    > <span data-ttu-id="4e992-125">공용으로 빌드된 패키지의 경우 **PackageTags** 속성에 특히 주의하세요. 이러한 태그는 다른 사람들이 패키지를 찾고 그 기능을 이해하는 데 도움이 됩니다.</span><span class="sxs-lookup"><span data-stu-id="4e992-125">For packages built for public consumption, pay special attention to the **PackageTags** property, as tags help others find your package and understand what it does.</span></span>

## <a name="run-the-pack-command"></a><span data-ttu-id="4e992-126">pack 명령 실행</span><span class="sxs-lookup"><span data-stu-id="4e992-126">Run the pack command</span></span>

<span data-ttu-id="4e992-127">프로젝트에서 NuGet 패키지(`.nupkg` 파일)를 빌드하려면 `dotnet pack` 명령을 실행합니다. 이 명령은 프로젝트도 자동으로 빌드합니다.</span><span class="sxs-lookup"><span data-stu-id="4e992-127">To build a NuGet package (a `.nupkg` file) from the project, run the `dotnet pack` command, which also builds the project automatically:</span></span>

```cli
# Uses the project file in the current folder by default
dotnet pack
```

<span data-ttu-id="4e992-128">출력에는 `.nupkg` 파일의 경로가 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="4e992-128">The output shows the path to the `.nupkg` file:</span></span>

```output
Microsoft (R) Build Engine version 15.5.180.51428 for .NET Core
Copyright (C) Microsoft Corporation. All rights reserved.

  Restore completed in 29.91 ms for D:\proj\AppLoggerNet\AppLogger\AppLogger.csproj.
  AppLogger -> D:\proj\AppLoggerNet\AppLogger\bin\Debug\netstandard2.0\AppLogger.dll
  Successfully created package 'D:\proj\AppLoggerNet\AppLogger\bin\Debug\AppLogger.1.0.0.nupkg'.
```

### <a name="automatically-generate-package-on-build"></a><span data-ttu-id="4e992-129">빌드 시 패키지를 자동으로 생성</span><span class="sxs-lookup"><span data-stu-id="4e992-129">Automatically generate package on build</span></span>

<span data-ttu-id="4e992-130">`dotnet build`를 실행할 때 `dotnet pack`을 자동으로 실행하려면 프로젝트 파일의 `<PropertyGroup>` 내에 다음 줄을 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="4e992-130">To automatically run `dotnet pack` when you run `dotnet build`, add the following line to your project file within `<PropertyGroup>`:</span></span>

```xml
<GeneratePackageOnBuild>true</GeneratePackageOnBuild>
```

## <a name="publish-the-package"></a><span data-ttu-id="4e992-131">패키지 게시</span><span class="sxs-lookup"><span data-stu-id="4e992-131">Publish the package</span></span>

<span data-ttu-id="4e992-132">`.nupkg` 파일이 있으면 nuget.org에서 얻은 API 키와 함께 `dotnet nuget push` 명령을 사용하여 nuget.org에 게시합니다.</span><span class="sxs-lookup"><span data-stu-id="4e992-132">Once you have a `.nupkg` file, you publish it to nuget.org using the `dotnet nuget push` command along with an API key acquired from nuget.org.</span></span>

[!INCLUDE [publish-notes](includes/publish-notes.md)]

### <a name="acquire-your-api-key"></a><span data-ttu-id="4e992-133">API 키 얻기</span><span class="sxs-lookup"><span data-stu-id="4e992-133">Acquire your API key</span></span>

[!INCLUDE [publish-api-key](includes/publish-api-key.md)]

### <a name="publish-with-dotnet-nuget-push"></a><span data-ttu-id="4e992-134">dotnet nuget push로 게시</span><span class="sxs-lookup"><span data-stu-id="4e992-134">Publish with dotnet nuget push</span></span>

[!INCLUDE [publish-dotnet](includes/publish-dotnet.md)]

### <a name="publish-errors"></a><span data-ttu-id="4e992-135">게시 오류</span><span class="sxs-lookup"><span data-stu-id="4e992-135">Publish errors</span></span>

[!INCLUDE [publish-errors](includes/publish-errors.md)]

### <a name="manage-the-published-package"></a><span data-ttu-id="4e992-136">게시된 패키지 관리</span><span class="sxs-lookup"><span data-stu-id="4e992-136">Manage the published package</span></span>

[!INCLUDE [publish-manage](includes/publish-manage.md)]

## <a name="next-steps"></a><span data-ttu-id="4e992-137">다음 단계</span><span class="sxs-lookup"><span data-stu-id="4e992-137">Next steps</span></span>

<span data-ttu-id="4e992-138">첫 번째 NuGet 패키지 만들기를 진행하시게 된 것을 축하드립니다.</span><span class="sxs-lookup"><span data-stu-id="4e992-138">Congratulations on creating your first NuGet package!</span></span>

> [!div class="nextstepaction"]
> [<span data-ttu-id="4e992-139">패키지 만들기</span><span class="sxs-lookup"><span data-stu-id="4e992-139">Create a Package</span></span>](../create-packages/creating-a-package-dotnet-cli.md)

<span data-ttu-id="4e992-140">NuGet에서 제공하는 다른 기능을 탐색하려면 아래 링크를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="4e992-140">To explore more that NuGet has to offer, select the links below.</span></span>

- [<span data-ttu-id="4e992-141">패키지 게시</span><span class="sxs-lookup"><span data-stu-id="4e992-141">Publish a Package</span></span>](../nuget-org/publish-a-package.md)
- [<span data-ttu-id="4e992-142">시험판 패키지</span><span class="sxs-lookup"><span data-stu-id="4e992-142">Pre-release Packages</span></span>](../create-packages/Prerelease-Packages.md)
- [<span data-ttu-id="4e992-143">여러 대상 프레임워크 지원</span><span class="sxs-lookup"><span data-stu-id="4e992-143">Support multiple target frameworks</span></span>](../create-packages/multiple-target-frameworks-project-file.md)
- [<span data-ttu-id="4e992-144">패키지 버전 관리</span><span class="sxs-lookup"><span data-stu-id="4e992-144">Package versioning</span></span>](../reference/package-versioning.md)
- [<span data-ttu-id="4e992-145">지역화된 패키지 만들기</span><span class="sxs-lookup"><span data-stu-id="4e992-145">Creating localized packages</span></span>](../create-packages/creating-localized-packages.md)
- [<span data-ttu-id="4e992-146">기호 패키지 만들기</span><span class="sxs-lookup"><span data-stu-id="4e992-146">Creating symbol packages</span></span>](../create-packages/symbol-packages-snupkg.md)
- [<span data-ttu-id="4e992-147">패키지 서명</span><span class="sxs-lookup"><span data-stu-id="4e992-147">Signing packages</span></span>](../create-packages/Sign-a-package.md)
