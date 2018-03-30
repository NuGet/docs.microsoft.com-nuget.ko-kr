---
title: Visual Studio를 사용하여 .NET Standard NuGet 패키지 만들기 및 게시에 대한 소개 가이드 | Microsoft Docs
author: kraigb
ms.author: kraigb
manager: ghogen
ms.date: 03/18/2018
ms.topic: quickstart
ms.prod: nuget
ms.technology: ''
description: Visual Studio 2017을 사용하여 .NET Standard NuGet 패키지를 만들고 게시하는 방법에 대한 연습 자습서입니다.
keywords: NuGet 패키지 만들기, NuGet 패키지 게시, NuGet 자습서, Visual Studio에서 NuGet 패키지 만들기, msbuild 팩
ms.reviewer:
- karann-msft
- unniravindranathan
ms.workload:
- dotnet
- aspnet
ms.openlocfilehash: cdfaf437b30f507f1227f9e6dbd8b039c5bf4402
ms.sourcegitcommit: beb229893559824e8abd6ab16707fd5fe1c6ac26
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 03/28/2018
---
# <a name="create-and-publish-a-package-using-visual-studio-net-standard"></a><span data-ttu-id="2673d-104">Visual Studio(.NET Standard)를 사용하여 패키지 만들기 및 게시</span><span class="sxs-lookup"><span data-stu-id="2673d-104">Create and publish a package using Visual Studio (.NET Standard)</span></span>

<span data-ttu-id="2673d-105">Visual Studio의 .NET Standard 클래스 라이브러리에서 NuGet 패키지를 만들고 CLI 도구를 사용하여 nuget.org에 게시하는 간단한 과정입니다.</span><span class="sxs-lookup"><span data-stu-id="2673d-105">It's a simple process to create a NuGet package from a .NET Standard Class Library in Visual Studio, and then publish it to nuget.org using a CLI tool.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="2673d-106">전제 조건</span><span class="sxs-lookup"><span data-stu-id="2673d-106">Prerequisites</span></span>

1. <span data-ttu-id="2673d-107">.Net 관련 워크로드를 사용하여 [visualstudio.com](https://www.visualstudio.com/)에서 모든 버전의 Visual Studio 2017을 설치합니다.</span><span class="sxs-lookup"><span data-stu-id="2673d-107">Install any edition of Visual Studio 2017 from [visualstudio.com](https://www.visualstudio.com/) with any .NET-related workload.</span></span> <span data-ttu-id="2673d-108">.NET 워크로드가 설치될 때 Visual Studio 2017이 NuGet 기능을 자동으로 포함합니다.</span><span class="sxs-lookup"><span data-stu-id="2673d-108">Visual Studio 2017 automatically includes NuGet capabilities when a .NET workload is installed.</span></span>

1. <span data-ttu-id="2673d-109">`nuget.exe` CLI를 설치하려면 [nuget.org](https://dist.nuget.org/win-x86-commandline/latest/nuget.exe)에서 다운로드하고, 해당 `.exe` 파일을 적합한 폴더에 저장하고, 해당 폴더를 PATH 환경 변수에 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="2673d-109">Install the `nuget.exe` CLI by downloading it from [nuget.org](https://dist.nuget.org/win-x86-commandline/latest/nuget.exe), saving that `.exe` file to a suitable folder, and adding that folder to your PATH environment variable.</span></span>

    <span data-ttu-id="2673d-110">또는 [.NET Core SDK](https://www.microsoft.com/net/download/)를 설치한 경우에는 `dotnet` CLI를 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="2673d-110">Alternately, if you have the [.NET Core SDK](https://www.microsoft.com/net/download/) installed, you can use the `dotnet` CLI.</span></span>

1. <span data-ttu-id="2673d-111">아직 없는 경우 [nuget.org에 체험 계정을 등록](https://www.nuget.org/users/account/LogOn?returnUrl=%2F)합니다.</span><span class="sxs-lookup"><span data-stu-id="2673d-111">[Register for a free account on nuget.org](https://www.nuget.org/users/account/LogOn?returnUrl=%2F) if you don't have one already.</span></span> <span data-ttu-id="2673d-112">새 계정을 만들면 확인 전자 메일을 보냅니다.</span><span class="sxs-lookup"><span data-stu-id="2673d-112">Creating a new account sends a confirmation email.</span></span> <span data-ttu-id="2673d-113">패키지를 업로드하려면 먼저 계정을 확인해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="2673d-113">You must confirm the account before you can upload a package.</span></span>

## <a name="create-a-class-library-project"></a><span data-ttu-id="2673d-114">클래스 라이브러리 프로젝트 만들기</span><span class="sxs-lookup"><span data-stu-id="2673d-114">Create a class library project</span></span>

<span data-ttu-id="2673d-115">패키지할 코드에 대해 기존 .NET Standard 클래스 라이브러리 프로젝트를 사용하거나 다음과 같이 간단한 프로젝트를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="2673d-115">You can use an existing .NET Standard Class Library project for the code you want to package, or create a simple one as follows:</span></span>

1. <span data-ttu-id="2673d-116">Visual Studio에서 **파일 > 새로 만들기 > 프로젝트**를 차례로 선택하고, **Visual C# > .NET Standard** 노드를 펼치고, “클래스 라이브러리(.NET Standard)” 템플릿을 선택하고, 프로젝트 이름을 AppLogger로 지정한 다음, **확인**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="2673d-116">In Visual Studio, choose **File > New > Project**, expand the **Visual C# > .NET Standard** node, select the "Class Library (.NET Standard)" template, name the project AppLogger, and click **OK**.</span></span>

1. <span data-ttu-id="2673d-117">결과 프로젝트 파일을 마우스 오른쪽 단추로 클릭하고, **빌드**를 선택하여 프로젝트가 제대로 만들어졌는지 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="2673d-117">Right-click on the resulting project file and select **Build** to make sure the project was created properly.</span></span> <span data-ttu-id="2673d-118">DLL은 Debug(또는 해당 구성을 대신 빌드하는 경우 Release) 폴더 내에 있습니다.</span><span class="sxs-lookup"><span data-stu-id="2673d-118">The DLL is found within the Debug folder (or Release if you build that configuration instead).</span></span>

<span data-ttu-id="2673d-119">물론 실제 NuGet 패키지 내에서 다른 사람들이 응용 프로그램을 빌드할 수 있는 많은 유용한 기능을 구현할 것입니다.</span><span class="sxs-lookup"><span data-stu-id="2673d-119">Within a real NuGet package, of course, you implement many useful features with which others can build applications.</span></span> <span data-ttu-id="2673d-120">그러나 이 연습에서는 템플릿의 클래스 라이브러리가 패키지를 만드는 데 충분하므로 추가 코드를 작성하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="2673d-120">For this walkthrough, however, you won't write any additional code because a class library from the template is sufficient to create a package.</span></span> <span data-ttu-id="2673d-121">그러나 계속 패키지에 대한 함수형 코드를 원하는 경우 다음을 사용하세요.</span><span class="sxs-lookup"><span data-stu-id="2673d-121">Still, if you'd like some functional code for the package, use the following:</span></span>

```cs
namespace AppLogger
{
    public class Logger
    {
        public void Log(string text)
        {
            Console.WriteLine(text);
        }
    }
}
```

> [!Tip]
> <span data-ttu-id="2673d-122">별도로 선택하지 않는 한 .NET Standard는 가장 넓은 범위의 사용하는 프로젝트와 호환되기 때문에 NuGet 패키지의 기본 대상입니다.</span><span class="sxs-lookup"><span data-stu-id="2673d-122">Unless you have a reason to choose otherwise, .NET Standard is the preferred target for NuGet packages, as it provides compatibility with the widest range of consuming projects.</span></span>

## <a name="configure-package-properties"></a><span data-ttu-id="2673d-123">패키지 속성 구성</span><span class="sxs-lookup"><span data-stu-id="2673d-123">Configure package properties</span></span>

1. <span data-ttu-id="2673d-124">**프로젝트 > 속성** 메뉴 명령을 선택한 다음, **패키지** 탭을 선택합니다. (**패키지** 탭은 .NET Standard 클래스 라이브러리 프로젝트에만 표시됩니다. .NET Framework를 대상으로 하는 경우 [.NET Framework 패키지 만들기 및 게시](create-and-publish-a-package-using-visual-studio-net-framework.md)를 대신 참조하세요.)</span><span class="sxs-lookup"><span data-stu-id="2673d-124">Select the **Project > Properties** menu command, then select the **Package** tab. (The **Package** tab appears only for .NET Standard class library projects; if you are targeting .NET Framework, see [Create and publish a .NET Framework package](create-and-publish-a-package-using-visual-studio-net-framework.md) instead.)</span></span>

    ![Visual Studio 프로젝트의 NuGet 패키지 속성](media/qs_create-vs-01-package-properties.png)

    > [!Note]
    > <span data-ttu-id="2673d-126">공용으로 빌드된 패키지의 경우 **태그** 속성에 특히 주의하세요. 태그는 다른 사람들이 패키지를 찾고 그 기능을 이해하는 데 도움이 됩니다.</span><span class="sxs-lookup"><span data-stu-id="2673d-126">For packages built for public consumption, pay special attention to the **Tags** property, as tags help others find your package and understand what it does.</span></span>

1. <span data-ttu-id="2673d-127">패키지에 고유 식별자를 제공하고 원하는 다른 모든 속성을 채웁니다.</span><span class="sxs-lookup"><span data-stu-id="2673d-127">Give your package a unique identifier and fill out any other desired properties.</span></span> <span data-ttu-id="2673d-128">다른 속성에 대한 설명은 [.nuspec 파일 참조](../reference/nuspec.md)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="2673d-128">For a description of the different properties, see [.nuspec file reference](../reference/nuspec.md).</span></span> <span data-ttu-id="2673d-129">여기에 있는 모든 속성은 Visual Studio에서 프로젝트에 대해 만드는 `.nuspec` 매니페스트로 이동합니다.</span><span class="sxs-lookup"><span data-stu-id="2673d-129">All of the properties here go into the `.nuspec` manifest that Visual Studio creates for the project.</span></span>

    > [!Important]
    > <span data-ttu-id="2673d-130">nuget.org 또는 무엇이든 사용 중인 호스트에서 고유한 식별자를 패키지에 제공해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="2673d-130">You must give the package an identifier that's unique across nuget.org or whatever host you're using.</span></span> <span data-ttu-id="2673d-131">이 연습에서는 나중 게시 단계에서 패키지를 공개적으로 표시할 수 있도록 이름에 “샘플” 또는 “테스트”를 포함하는 것이 좋습니다(실제로 아무도 사용할 가능성이 없더라도).</span><span class="sxs-lookup"><span data-stu-id="2673d-131">For this walkthrough we recommend including "Sample" or "Test" in the name as the later publishing step does make the package publicly visible (though it's unlikely anyone will actually use it).</span></span>
    >
    > <span data-ttu-id="2673d-132">이미 존재하는 이름으로 패키지를 게시하려고 시도하면 오류가 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="2673d-132">If you attempt to publish a package with a name that already exists, you see an error.</span></span>

1. <span data-ttu-id="2673d-133">선택 사항: 프로젝트 파일에서 직접 속성을 보려면 솔루션 탐색기에서 프로젝트를 마우스 오른쪽 단추로 클릭하고 **AppLogger.csproj 편집**을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="2673d-133">Optional: to see the properties directly in the project file, right-click the project in Solution Explorer and select **Edit AppLogger.csproj**.</span></span>

## <a name="run-the-pack-command"></a><span data-ttu-id="2673d-134">pack 명령 실행</span><span class="sxs-lookup"><span data-stu-id="2673d-134">Run the pack command</span></span>

1. <span data-ttu-id="2673d-135">구성을 **해제**로 설정합니다.</span><span class="sxs-lookup"><span data-stu-id="2673d-135">Set the configuration to **Release**.</span></span>

1. <span data-ttu-id="2673d-136">**솔루션 탐색기**에서 프로젝트를 마우스 오른쪽 단추로 클릭하고 **Pack** 명령을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="2673d-136">Right click the project in **Solution Explorer** and select the **Pack** command:</span></span>

    ![Visual Studio 프로젝트 상황에 맞는 메뉴의 NuGet pack 명령](media/qs_create-vs-02-pack-command.png)

1. <span data-ttu-id="2673d-138">Visual Studio에서 프로젝트를 빌드하고 `.nupkg` 파일을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="2673d-138">Visual Studio builds the project and creates the `.nupkg` file.</span></span> <span data-ttu-id="2673d-139">**출력** 창에서 패키지 파일의 경로가 포함된 다음과 같은 세부 정보가 있는지 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="2673d-139">Examine the **Output** window for details (similar to the following), which contains the path to the package file.</span></span> <span data-ttu-id="2673d-140">또한 빌드된 어셈블리는 .NET Standard 2.0 대상에 맞게 `bin\Release\netstandard2.0`에 있습니다.</span><span class="sxs-lookup"><span data-stu-id="2673d-140">Note also that the built assembly is in `bin\Release\netstandard2.0` as befits the .NET Standard 2.0 target.</span></span>

    ```output
    1>------ Build started: Project: AppLogger, Configuration: Release Any CPU ------
    1>AppLogger -> d:\proj\AppLogger\AppLogger\bin\Release\netstandard2.0\AppLogger.dll
    1>Successfully created package 'd:\proj\AppLogger\AppLogger\bin\Release\AppLogger.1.0.0.nupkg'.
    ========== Build: 1 succeeded, 0 failed, 0 up-to-date, 0 skipped ==========
    ```

### <a name="alternate-option-pack-with-msbuild"></a><span data-ttu-id="2673d-141">대체 옵션: MSBuild로 압축</span><span class="sxs-lookup"><span data-stu-id="2673d-141">Alternate option: pack with MSBuild</span></span>

<span data-ttu-id="2673d-142">**Pack** 메뉴 명령을 사용하는 대신 프로젝트에 필요한 패키지 데이터가 포함된 경우 NuGet 4.x 이상 및 MSBuild 15.1 이상은 `pack` 대상을 지원합니다.</span><span class="sxs-lookup"><span data-stu-id="2673d-142">As an alternate to using the **Pack** menu command, NuGet 4.x+ and MSBuild 15.1+ supports a `pack` target when the project contains the necessary package data.</span></span> <span data-ttu-id="2673d-143">명령 프롬프트를 열고 프로젝트 폴더로 이동한 후 다음 명령을 실행합니다.</span><span class="sxs-lookup"><span data-stu-id="2673d-143">Open a command prompt, navigate to your project folder and run the following command.</span></span> <span data-ttu-id="2673d-144">(일반적으로 시작 메뉴에서 "Visual Studio용 개발자 명령 프롬프트"를 시작하는 것이 좋습니다. MSBuild에 필요한 모든 경로로 구성되기 때문입니다.)</span><span class="sxs-lookup"><span data-stu-id="2673d-144">(You typically want to start the "Developer Command Prompt for Visual Studio" from the Start menu, as it will be configured with all the necessary paths for MSBuild.)</span></span>

```cli
msbuild /t:pack /p:Configuration=Release
```

<span data-ttu-id="2673d-145">그러면 패키지를 `bin\Release` 폴더에서 찾을 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="2673d-145">The package can then be found in the `bin\Release` folder.</span></span>

<span data-ttu-id="2673d-146">`msbuild /t:pack`에 대한 추가 옵션은 [MSBuild 대상으로서의 NuGet pack 및 restore](../reference/msbuild-targets.md#pack-target)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="2673d-146">For additional options with `msbuild /t:pack`, see [NuGet pack and restore as MSBuild targets](../reference/msbuild-targets.md#pack-target).</span></span>

## <a name="publish-the-package"></a><span data-ttu-id="2673d-147">패키지 게시</span><span class="sxs-lookup"><span data-stu-id="2673d-147">Publish the package</span></span>

<span data-ttu-id="2673d-148">`.nupkg` 파일이 있으면 nuget.org에서 얻은 API 키와 함께 `nuget.exe` CLI 또는 `dotnet.exe` CLI를 사용하여 nuget.org에 게시합니다.</span><span class="sxs-lookup"><span data-stu-id="2673d-148">Once you have a `.nupkg` file, you publish it to nuget.org using either the `nuget.exe` CLI or the `dotnet.exe` CLI along with an API key acquired from nuget.org.</span></span>

[!INCLUDE[publish-notes](includes/publish-notes.md)]

### <a name="acquire-your-api-key"></a><span data-ttu-id="2673d-149">API 키 얻기</span><span class="sxs-lookup"><span data-stu-id="2673d-149">Acquire your API key</span></span>

[!INCLUDE[publish-api-key](includes/publish-api-key.md)]

### <a name="publish-with-nuget-push"></a><span data-ttu-id="2673d-150">nuget push로 게시</span><span class="sxs-lookup"><span data-stu-id="2673d-150">Publish with nuget push</span></span>

<span data-ttu-id="2673d-151">`dotnet.exe`를 사용하는 대신 다음 단계를 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="2673d-151">This step is an alternative to using `dotnet.exe`.</span></span>

1. <span data-ttu-id="2673d-152">`.nupkg` 파일을 포함하는 폴더로 변경합니다.</span><span class="sxs-lookup"><span data-stu-id="2673d-152">Change to the folder containing the `.nupkg` file.</span></span>

1. <span data-ttu-id="2673d-153">다음 명령을 실행하여 패키지 이름을 지정하고 키 값을 API 키로 바꿉니다.</span><span class="sxs-lookup"><span data-stu-id="2673d-153">Run the following command, specifying your package name and replacing the key value with your API key:</span></span>

    ```cli
    nuget push AppLogger.1.0.0.nupkg qz2jga8pl3dvn2akksyquwcs9ygggg4exypy3bhxy6w6x6 -Source https://api.nuget.org/v3/index.json
    ```

1. <span data-ttu-id="2673d-154">nuget.exe에서 게시 프로세스의 결과를 표시합니다.</span><span class="sxs-lookup"><span data-stu-id="2673d-154">nuget.exe displays the results of the publishing process:</span></span>

    ```output
    Pushing AppLogger.1.0.0.nupkg to 'https://www.nuget.org/api/v2/package'...
        PUT https://www.nuget.org/api/v2/package/
        Created https://www.nuget.org/api/v2/package/ 6829ms
    Your package was pushed.
    ```

<span data-ttu-id="2673d-155">[nuget push](../tools/cli-ref-push.md)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="2673d-155">See [nuget push](../tools/cli-ref-push.md).</span></span>

### <a name="publish-with-dotnet-nuget-push"></a><span data-ttu-id="2673d-156">dotnet nuget push로 게시</span><span class="sxs-lookup"><span data-stu-id="2673d-156">Publish with dotnet nuget push</span></span>

<span data-ttu-id="2673d-157">`nuget.exe`를 사용하는 대신 다음 단계를 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="2673d-157">This step is an alternative to using `nuget.exe`.</span></span>

[!INCLUDE[publish-dotnet](includes/publish-dotnet.md)]

### <a name="publish-errors"></a><span data-ttu-id="2673d-158">게시 오류</span><span class="sxs-lookup"><span data-stu-id="2673d-158">Publish errors</span></span>

[!INCLUDE[publish-errors](includes/publish-errors.md)]

### <a name="manage-the-published-package"></a><span data-ttu-id="2673d-159">게시된 패키지 관리</span><span class="sxs-lookup"><span data-stu-id="2673d-159">Manage the published package</span></span>

[!INCLUDE[publish-manage](includes/publish-manage.md)]

## <a name="related-topics"></a><span data-ttu-id="2673d-160">관련 항목</span><span class="sxs-lookup"><span data-stu-id="2673d-160">Related topics</span></span>

- [<span data-ttu-id="2673d-161">패키지 만들기</span><span class="sxs-lookup"><span data-stu-id="2673d-161">Create a Package</span></span>](../create-packages/creating-a-package.md)
- [<span data-ttu-id="2673d-162">패키지 게시</span><span class="sxs-lookup"><span data-stu-id="2673d-162">Publish a Package</span></span>](../create-packages/publish-a-package.md)
- [<span data-ttu-id="2673d-163">여러 대상 프레임워크 지원</span><span class="sxs-lookup"><span data-stu-id="2673d-163">Support multiple target frameworks</span></span>](../create-packages/supporting-multiple-target-frameworks.md)
- [<span data-ttu-id="2673d-164">패키지 버전 관리</span><span class="sxs-lookup"><span data-stu-id="2673d-164">Package versioning</span></span>](../reference/package-versioning.md)
- [<span data-ttu-id="2673d-165">지역화된 패키지 만들기</span><span class="sxs-lookup"><span data-stu-id="2673d-165">Creating localized packages</span></span>](../create-packages/creating-localized-packages.md)
- [<span data-ttu-id="2673d-166">.NET Standard 라이브러리 설명서</span><span class="sxs-lookup"><span data-stu-id="2673d-166">.NET Standard Library documentation</span></span>](/dotnet/articles/standard/library)
- [<span data-ttu-id="2673d-167">.NET Framework에서 .NET Core로 이식</span><span class="sxs-lookup"><span data-stu-id="2673d-167">Porting to .NET Core from .NET Framework</span></span>](/dotnet/articles/core/porting/index)