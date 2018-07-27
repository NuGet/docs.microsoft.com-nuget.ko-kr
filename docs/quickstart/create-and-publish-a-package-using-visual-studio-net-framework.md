---
title: Windows에서 Visual Studio를 사용하여 .NET Framework 패키지 만들기 및 게시
description: Windows에서 Visual Studio 2017을 사용하여 .NET Framework NuGet 패키지를 만들고 게시하는 방법에 대한 연습 자습서입니다.
author: karann-msft
ms.author: karann
manager: unnir
ms.date: 05/13/2018
ms.topic: quickstart
ms.openlocfilehash: ffa2128b577673e980f4115f37f8685858c36250
ms.sourcegitcommit: 6cffa6ef59b922df2d87aa9c24034d00542983cd
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/10/2018
ms.locfileid: "37963161"
---
# <a name="quickstart-create-and-publish-a-package-using-visual-studio-net-framework-windows"></a><span data-ttu-id="c247a-103">빠른 시작: Visual Studio(.NET Framework, Windows)를 사용하여 패키지 만들기 및 게시</span><span class="sxs-lookup"><span data-stu-id="c247a-103">Quickstart: Create and publish a package using Visual Studio (.NET Framework, Windows)</span></span>

<span data-ttu-id="c247a-104">.NET Framework 클래스 라이브러리로 NuGet 패키지를 만들려면 Windows의 Visual Studio에서 DLL을 만든 후 nuget.exe 명령줄 도구를 사용하여 패키지를 만들고 게시해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="c247a-104">Creating a NuGet package from a .NET Framework Class Library involves creating the DLL in Visual Studio on Windows, then using the nuget.exe command line tool to create and publish the package.</span></span>

> [!Note]
> <span data-ttu-id="c247a-105">이 빠른 시작은 Windows용 Visual Studio 2017에만 적용됩니다.</span><span class="sxs-lookup"><span data-stu-id="c247a-105">This Quickstart applies to Visual Studio 2017 for Windows only.</span></span> <span data-ttu-id="c247a-106">Mac용 Visual Studio에는 여기에 설명된 기능이 포함되어 있지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="c247a-106">Visual Studio for Mac does not include the capabilities described here.</span></span> <span data-ttu-id="c247a-107">대신 [dotnet CLI 도구](create-and-publish-a-package-using-the-dotnet-cli.md)를 사용하세요.</span><span class="sxs-lookup"><span data-stu-id="c247a-107">Use the [dotnet CLI tools](create-and-publish-a-package-using-the-dotnet-cli.md) instead.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="c247a-108">전제 조건</span><span class="sxs-lookup"><span data-stu-id="c247a-108">Prerequisites</span></span>

1. <span data-ttu-id="c247a-109">.Net 관련 워크로드를 사용하여 [visualstudio.com](https://www.visualstudio.com/)에서 모든 버전의 Visual Studio 2017을 설치합니다.</span><span class="sxs-lookup"><span data-stu-id="c247a-109">Install any edition of Visual Studio 2017 from [visualstudio.com](https://www.visualstudio.com/) with any .NET-related workload.</span></span> <span data-ttu-id="c247a-110">.NET 워크로드가 설치될 때 Visual Studio 2017이 NuGet 기능을 자동으로 포함합니다.</span><span class="sxs-lookup"><span data-stu-id="c247a-110">Visual Studio 2017 automatically includes NuGet capabilities when a .NET workload is installed.</span></span>

1. <span data-ttu-id="c247a-111">`nuget.exe` CLI를 설치하려면 [nuget.org](https://dist.nuget.org/win-x86-commandline/latest/nuget.exe)에서 다운로드하고, 해당 `.exe` 파일을 적합한 폴더에 저장하고, 해당 폴더를 PATH 환경 변수에 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="c247a-111">Install the `nuget.exe` CLI by downloading it from [nuget.org](https://dist.nuget.org/win-x86-commandline/latest/nuget.exe), saving that `.exe` file to a suitable folder, and adding that folder to your PATH environment variable.</span></span>

1. <span data-ttu-id="c247a-112">아직 없는 경우 [nuget.org에 체험 계정을 등록](https://www.nuget.org/users/account/LogOn?returnUrl=%2F)합니다.</span><span class="sxs-lookup"><span data-stu-id="c247a-112">[Register for a free account on nuget.org](https://www.nuget.org/users/account/LogOn?returnUrl=%2F) if you don't have one already.</span></span> <span data-ttu-id="c247a-113">새 계정을 만들면 확인 전자 메일을 보냅니다.</span><span class="sxs-lookup"><span data-stu-id="c247a-113">Creating a new account sends a confirmation email.</span></span> <span data-ttu-id="c247a-114">패키지를 업로드하려면 먼저 계정을 확인해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="c247a-114">You must confirm the account before you can upload a package.</span></span>

## <a name="create-a-class-library-project"></a><span data-ttu-id="c247a-115">클래스 라이브러리 프로젝트 만들기</span><span class="sxs-lookup"><span data-stu-id="c247a-115">Create a class library project</span></span>

<span data-ttu-id="c247a-116">패키지할 코드에 대해 기존 .NET Framework 클래스 라이브러리 프로젝트를 사용하거나 다음과 같이 간단한 프로젝트를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="c247a-116">You can use an existing .NET Framework Class Library project for the code you want to package, or create a simple one as follows:</span></span>

1. <span data-ttu-id="c247a-117">Visual Studio에서 **파일 > 새로 만들기 > 프로젝트**를 차례로 선택하고, **Visual C#** 노드를 선택하고, "클래스 라이브러리(.NET Framework)" 템플릿을 선택하고, 프로젝트 이름을 AppLogger로 지정한 다음, **확인**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="c247a-117">In Visual Studio, choose **File > New > Project**, select the **Visual C#** node, select the "Class Library (.NET Framework)" template, name the project AppLogger, and click **OK**.</span></span>

1. <span data-ttu-id="c247a-118">결과 프로젝트 파일을 마우스 오른쪽 단추로 클릭하고, **빌드**를 선택하여 프로젝트가 제대로 만들어졌는지 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="c247a-118">Right-click on the resulting project file and select **Build** to make sure the project was created properly.</span></span> <span data-ttu-id="c247a-119">DLL은 Debug(또는 해당 구성을 대신 빌드하는 경우 Release) 폴더 내에 있습니다.</span><span class="sxs-lookup"><span data-stu-id="c247a-119">The DLL is found within the Debug folder (or Release if you build that configuration instead).</span></span>

<span data-ttu-id="c247a-120">물론 실제 NuGet 패키지 내에서 다른 사람들이 응용 프로그램을 빌드할 수 있는 많은 유용한 기능을 구현할 것입니다.</span><span class="sxs-lookup"><span data-stu-id="c247a-120">Within a real NuGet package, of course, you implement many useful features with which others can build applications.</span></span> <span data-ttu-id="c247a-121">원하는 대상 프레임워크를 설정할 수도 있습니다.</span><span class="sxs-lookup"><span data-stu-id="c247a-121">You can also set the target frameworks however you like.</span></span> <span data-ttu-id="c247a-122">예를 들어 [UWP](../guides/create-uwp-packages.md) 및 [Xamarin](../guides/create-packages-for-xamarin.md)에 대한 가이드를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="c247a-122">For example, see the guides for [UWP](../guides/create-uwp-packages.md) and [Xamarin](../guides/create-packages-for-xamarin.md).</span></span>

<span data-ttu-id="c247a-123">그러나 이 연습에서는 템플릿의 클래스 라이브러리가 패키지를 만드는 데 충분하므로 추가 코드를 작성하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="c247a-123">For this walkthrough, however, you won't write any additional code because a class library from the template is sufficient to create a package.</span></span> <span data-ttu-id="c247a-124">그러나 계속 패키지에 대한 함수형 코드를 원하는 경우 다음을 사용하세요.</span><span class="sxs-lookup"><span data-stu-id="c247a-124">Still, if you'd like some functional code for the package, use the following:</span></span>

```cs
using System;

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
> <span data-ttu-id="c247a-125">별도로 선택하지 않는 한 .NET Standard는 가장 넓은 범위의 사용하는 프로젝트와 호환되기 때문에 NuGet 패키지의 기본 대상입니다.</span><span class="sxs-lookup"><span data-stu-id="c247a-125">Unless you have a reason to choose otherwise, .NET Standard is the preferred target for NuGet packages, as it provides compatibility with the widest range of consuming projects.</span></span> <span data-ttu-id="c247a-126">[Visual Studio(.NET Standard)를 사용하여 패키지 만들기 및 게시](create-and-publish-a-package-using-visual-studio.md)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="c247a-126">See [Create and publish a package using Visual Studio (.NET Standard)](create-and-publish-a-package-using-visual-studio.md).</span></span>

## <a name="configure-project-properties-for-the-package"></a><span data-ttu-id="c247a-127">패키지의 프로젝트 속성 구성</span><span class="sxs-lookup"><span data-stu-id="c247a-127">Configure project properties for the package</span></span>

<span data-ttu-id="c247a-128">패키지 식별자, 버전 번호, 설명 등과 같은 관련 메타데이터를 포함하는 매니페스트(`.nuspec` 파일)가 들어 있는 NuGet 패키지입니다.</span><span class="sxs-lookup"><span data-stu-id="c247a-128">A NuGet package contains a manifest (a `.nuspec` file), that contains relevant metadata such as the package identifier, version number, description, and more.</span></span> <span data-ttu-id="c247a-129">이 중 일부는 프로젝트 속성에서 바로 가져올 수 있습니다. 그러면 프로젝트와 매니페스트에서 개별적으로 업데이트할 필요가 없습니다.</span><span class="sxs-lookup"><span data-stu-id="c247a-129">Some of these can be drawn from the project properties directly, which avoids having to separately update them in both the project and the manifest.</span></span> <span data-ttu-id="c247a-130">이 섹션에서는 해당 속성을 설정하는 위치를 설명합니다.</span><span class="sxs-lookup"><span data-stu-id="c247a-130">This section describes where to set the applicable properties.</span></span>

1. <span data-ttu-id="c247a-131">**프로젝트 > 속성** 메뉴 명령을 선택한 다음, **응용 프로그램** 탭을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="c247a-131">Select the **Project > Properties** menu command, then select the **Application** tab.</span></span>

1. <span data-ttu-id="c247a-132">**어셈블리 이름** 필드에서 패키지에 고유 식별자를 지정합니다.</span><span class="sxs-lookup"><span data-stu-id="c247a-132">In the **Assembly name** field, give your package a unique identifier.</span></span>

    > [!Important]
    > <span data-ttu-id="c247a-133">nuget.org 또는 무엇이든 사용 중인 호스트에서 고유한 식별자를 패키지에 제공해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="c247a-133">You must give the package an identifier that's unique across nuget.org or whatever host you're using.</span></span> <span data-ttu-id="c247a-134">이 연습에서는 나중 게시 단계에서 패키지를 공개적으로 표시할 수 있도록 이름에 “샘플” 또는 “테스트”를 포함하는 것이 좋습니다(실제로 아무도 사용할 가능성이 없더라도).</span><span class="sxs-lookup"><span data-stu-id="c247a-134">For this walkthrough we recommend including "Sample" or "Test" in the name as the later publishing step does make the package publicly visible (though it's unlikely anyone will actually use it).</span></span>
    >
    > <span data-ttu-id="c247a-135">이미 존재하는 이름으로 패키지를 게시하려고 시도하면 오류가 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="c247a-135">If you attempt to publish a package with a name that already exists, you see an error.</span></span>

1. <span data-ttu-id="c247a-136">**어셈블리 정보...** 단추를 선택합니다. 그러면 매니페스트에 전달되는 다른 속성을 입력할 수 있는 대화 상자가 표시됩니다([.nuspec 파일 - 교체 토큰 참조](../reference/nuspec.md#replacement-tokens)).</span><span class="sxs-lookup"><span data-stu-id="c247a-136">Select the **Assembly Information...** button, which brings up a dialog box in which you can enter other properties that carry into the manifest (see [.nuspec file reference - replacement tokens](../reference/nuspec.md#replacement-tokens)).</span></span> <span data-ttu-id="c247a-137">가장 일반적으로 사용되는 필드는 **제목**, **설명**, **회사**, **저작권** 및 **어셈블리 버전**입니다.</span><span class="sxs-lookup"><span data-stu-id="c247a-137">The most commonly used fields are **Title**, **Description**, **Company**, **Copyright**, and **Assembly version**.</span></span> <span data-ttu-id="c247a-138">이러한 속성은 최종적으로 nuget.org 같은 호스트에서 패키지와 함께 표시되므로 자세한 설명을 제공하는지 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="c247a-138">These properties ultimately appear with your package on a host like nuget.org, so make sure they're fully descriptive.</span></span>

    ![Visual Studio에서 .NET Framework 프로젝트의 어셈블리 정보](media/qs_create-vs-01b-project-properties.png)

1. <span data-ttu-id="c247a-140">옵션: 속성을 직접 보고 편집하려면 프로젝트의 `Properties/AssemblyInfo.cs` 파일을 엽니다.</span><span class="sxs-lookup"><span data-stu-id="c247a-140">Optional: to see and edit the properties directly, open the `Properties/AssemblyInfo.cs` file in the project.</span></span>

1. <span data-ttu-id="c247a-141">속성이 설정되면 프로젝트 구성을 **릴리스**로 설정하고 프로젝트를 다시 빌드하여 업데이트된 DLL을 생성합니다.</span><span class="sxs-lookup"><span data-stu-id="c247a-141">When the properties are set, set the project configuration to **Release** and rebuild the project to generate the updated DLL.</span></span>

## <a name="generate-the-initial-manifest"></a><span data-ttu-id="c247a-142">초기 매니페스트 생성</span><span class="sxs-lookup"><span data-stu-id="c247a-142">Generate the initial manifest</span></span>

<span data-ttu-id="c247a-143">DLL이 생성되고 프로젝트 속성이 설정되면 이제 `nuget spec` 명령을 사용하여 프로젝트에서 초기 `.nuspec` 파일을 생성합니다.</span><span class="sxs-lookup"><span data-stu-id="c247a-143">With a DLL in hand and project properties set, you now use the `nuget spec` command to generate an initial `.nuspec` file from the project.</span></span> <span data-ttu-id="c247a-144">이 단계에는 프로젝트 파일에서 정보를 가져오기 위한 관련 교체 토큰이 포함됩니다.</span><span class="sxs-lookup"><span data-stu-id="c247a-144">This step includes the relevant replacement tokens to draw information from the project file.</span></span>

<span data-ttu-id="c247a-145">`nuget spec`을 한 번만 실행하여 초기 매니페스트를 생성합니다.</span><span class="sxs-lookup"><span data-stu-id="c247a-145">You run `nuget spec` only once to generate the initial manifest.</span></span> <span data-ttu-id="c247a-146">패키지를 업데이트할 때는 프로젝트에서 값을 변경하거나 매니페스트를 직접 편집하세요.</span><span class="sxs-lookup"><span data-stu-id="c247a-146">When updating the package, you either change values in your project or edit the manifest directly.</span></span>

1. <span data-ttu-id="c247a-147">명령 프롬프트를 열고 `AppLogger.csproj` 파일이 있는 프로젝트 폴더로 이동합니다.</span><span class="sxs-lookup"><span data-stu-id="c247a-147">Open a command prompt and navigate to the project folder containing `AppLogger.csproj` file.</span></span>

1. <span data-ttu-id="c247a-148">`nuget spec AppLogger.csproj` 명령을 실행합니다.</span><span class="sxs-lookup"><span data-stu-id="c247a-148">Run the following command: `nuget spec AppLogger.csproj`.</span></span> <span data-ttu-id="c247a-149">프로젝트를 지정하면 NuGet이 프로젝트의 이름과 일치하는 매니페스트를 만듭니다(이 경우 `AppLogger.nuspec`).</span><span class="sxs-lookup"><span data-stu-id="c247a-149">By specifying a project, NuGet creates a manifest that matches the name of the project, in this case `AppLogger.nuspec`.</span></span> <span data-ttu-id="c247a-150">또한 매니페스트에는 교체 토큰도 포함되어 있습니다.</span><span class="sxs-lookup"><span data-stu-id="c247a-150">It also include replacement tokens in the manifest.</span></span>

1. <span data-ttu-id="c247a-151">텍스트 편집기에서 `AppLogger.nuspec`을 열어 해당 내용을 살펴봅니다. 이는 다음과 같아야 합니다.</span><span class="sxs-lookup"><span data-stu-id="c247a-151">Open `AppLogger.nuspec` in a text editor to examine its contents, which should appear as follows:</span></span>

    ```xml
    <?xml version="1.0"?>
    <package >
      <metadata>
        <id>$id$</id>
        <version>$version$</version>
        <title>$title$</title>
        <authors>$author$</authors>
        <owners>$author$</owners>
        <licenseUrl>http://LICENSE_URL_HERE_OR_DELETE_THIS_LINE</licenseUrl>
        <projectUrl>http://PROJECT_URL_HERE_OR_DELETE_THIS_LINE</projectUrl>
        <iconUrl>http://ICON_URL_HERE_OR_DELETE_THIS_LINE</iconUrl>
        <requireLicenseAcceptance>false</requireLicenseAcceptance>
        <description>$description$</description>
        <releaseNotes>Summary of changes made in this release of the package.</releaseNotes>
        <copyright>Copyright 2018</copyright>
        <tags>Tag1 Tag2</tags>
      </metadata>
    </package>
    ```

## <a name="edit-the-manifest"></a><span data-ttu-id="c247a-152">매니페스트 편집</span><span class="sxs-lookup"><span data-stu-id="c247a-152">Edit the manifest</span></span>

1. <span data-ttu-id="c247a-153">`.nuspec` 파일의 기본값을 사용하여 패키지를 만들려고 하면 NuGet에서 오류를 표시하므로 계속하기 전에 다음 필드를 편집해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="c247a-153">NuGet produces an error if you try to create a package with default values in your `.nuspec` file, so you must edit the following fields before proceeding.</span></span> <span data-ttu-id="c247a-154">이를 사용하는 방법에 대한 자세한 내용은 [.nuspec 파일 참조 - 단일 요소](../reference/nuspec.md#single-elements)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="c247a-154">See [.nuspec file reference - single elements](../reference/nuspec.md#single-elements) for a description of how these are used.</span></span>

    - <span data-ttu-id="c247a-155">licenseUrl</span><span class="sxs-lookup"><span data-stu-id="c247a-155">licenseUrl</span></span>
    - <span data-ttu-id="c247a-156">projectUrl</span><span class="sxs-lookup"><span data-stu-id="c247a-156">projectUrl</span></span>
    - <span data-ttu-id="c247a-157">iconUrl</span><span class="sxs-lookup"><span data-stu-id="c247a-157">iconUrl</span></span>
    - <span data-ttu-id="c247a-158">releaseNotes</span><span class="sxs-lookup"><span data-stu-id="c247a-158">releaseNotes</span></span>
    - <span data-ttu-id="c247a-159">태그</span><span class="sxs-lookup"><span data-stu-id="c247a-159">tags</span></span>

1. <span data-ttu-id="c247a-160">공용으로 빌드된 패키지의 경우 **태그** 속성에 특히 주의하세요. 태그는 다른 사람들이 nuget.org 같은 소스에서 패키지를 찾고 그 기능을 이해하는 데 도움이 됩니다.</span><span class="sxs-lookup"><span data-stu-id="c247a-160">For packages built for public consumption, pay special attention to the **Tags** property, as tags help others find your package on sources like nuget.org and understand what it does.</span></span>

1. <span data-ttu-id="c247a-161">또한 이때 [.nuspec 파일 참조](../reference/nuspec.md)에 설명된 대로 매니페스트에 다른 요소를 추가할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="c247a-161">You can also add any other elements to the manifest at this time, as described on [.nuspec file reference](../reference/nuspec.md).</span></span>

1. <span data-ttu-id="c247a-162">계속하기 전에 파일을 저장하세요.</span><span class="sxs-lookup"><span data-stu-id="c247a-162">Save the file before proceeding.</span></span>

## <a name="run-the-pack-command"></a><span data-ttu-id="c247a-163">pack 명령 실행</span><span class="sxs-lookup"><span data-stu-id="c247a-163">Run the pack command</span></span>

1. <span data-ttu-id="c247a-164">명령 프롬프트에서 `.nuspec` 파일이 포함된 폴더에 `nuget pack` 명령을 실행합니다.</span><span class="sxs-lookup"><span data-stu-id="c247a-164">From a command prompt in the folder containing your `.nuspec` file, run the command `nuget pack`.</span></span>

1. <span data-ttu-id="c247a-165">NuGet은 *식별자-버전.nupkg* 형태의 `.nupkg` 파일을 생성하며, 이는 현재 폴더에서 볼 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="c247a-165">NuGet generates a `.nupkg` file in the form of *identifier-version.nupkg*, which you'll find in the current folder.</span></span>

## <a name="publish-the-package"></a><span data-ttu-id="c247a-166">패키지 게시</span><span class="sxs-lookup"><span data-stu-id="c247a-166">Publish the package</span></span>

<span data-ttu-id="c247a-167">`.nupkg` 파일이 생성되면 nuget.org에서 얻은 API 키와 함께 `nuget.exe`를 사용하여 nuget.org에 게시합니다. nuget.org의 경우 `nuget.exe` 4.1.0 이상을 사용해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="c247a-167">Once you have a `.nupkg` file, you publish it to nuget.org using `nuget.exe` with an API key acquired from nuget.org. For nuget.org you must use `nuget.exe` 4.1.0 or higher.</span></span>

[!INCLUDE [publish-notes](includes/publish-notes.md)]

### <a name="acquire-your-api-key"></a><span data-ttu-id="c247a-168">API 키 얻기</span><span class="sxs-lookup"><span data-stu-id="c247a-168">Acquire your API key</span></span>

[!INCLUDE [publish-api-key](includes/publish-api-key.md)]

### <a name="publish-with-nuget-push"></a><span data-ttu-id="c247a-169">nuget push로 게시</span><span class="sxs-lookup"><span data-stu-id="c247a-169">Publish with nuget push</span></span>

1. <span data-ttu-id="c247a-170">`.nupkg` 파일을 포함하는 폴더로 변경합니다.</span><span class="sxs-lookup"><span data-stu-id="c247a-170">Change to the folder containing the `.nupkg` file.</span></span>

1. <span data-ttu-id="c247a-171">다음 명령을 실행하여 패키지 이름을 지정하고 키 값을 API 키로 바꿉니다.</span><span class="sxs-lookup"><span data-stu-id="c247a-171">Run the following command, specifying your package name and replacing the key value with your API key:</span></span>

    ```cli
    nuget push AppLogger.1.0.0.nupkg qz2jga8pl3dvn2akksyquwcs9ygggg4exypy3bhxy6w6x6 -Source https://api.nuget.org/v3/index.json
    ```

1. <span data-ttu-id="c247a-172">nuget.exe에서 게시 프로세스의 결과를 표시합니다.</span><span class="sxs-lookup"><span data-stu-id="c247a-172">nuget.exe displays the results of the publishing process:</span></span>

    ```output
    Pushing AppLogger.1.0.0.nupkg to 'https://www.nuget.org/api/v2/package'...
        PUT https://www.nuget.org/api/v2/package/
        Created https://www.nuget.org/api/v2/package/ 6829ms
    Your package was pushed.
    ```

<span data-ttu-id="c247a-173">[nuget push](../tools/cli-ref-push.md)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="c247a-173">See [nuget push](../tools/cli-ref-push.md).</span></span>

### <a name="publish-errors"></a><span data-ttu-id="c247a-174">게시 오류</span><span class="sxs-lookup"><span data-stu-id="c247a-174">Publish errors</span></span>

[!INCLUDE [publish-errors](includes/publish-errors.md)]

### <a name="manage-the-published-package"></a><span data-ttu-id="c247a-175">게시된 패키지 관리</span><span class="sxs-lookup"><span data-stu-id="c247a-175">Manage the published package</span></span>

[!INCLUDE [publish-manage](includes/publish-manage.md)]

## <a name="related-topics"></a><span data-ttu-id="c247a-176">관련 항목</span><span class="sxs-lookup"><span data-stu-id="c247a-176">Related topics</span></span>

- [<span data-ttu-id="c247a-177">패키지 만들기</span><span class="sxs-lookup"><span data-stu-id="c247a-177">Create a Package</span></span>](../create-packages/creating-a-package.md)
- [<span data-ttu-id="c247a-178">패키지 게시</span><span class="sxs-lookup"><span data-stu-id="c247a-178">Publish a Package</span></span>](../create-packages/publish-a-package.md)
- [<span data-ttu-id="c247a-179">시험판 패키지</span><span class="sxs-lookup"><span data-stu-id="c247a-179">Pre-release Packages</span></span>](../create-packages/Prerelease-Packages.md)
- [<span data-ttu-id="c247a-180">여러 대상 프레임워크 지원</span><span class="sxs-lookup"><span data-stu-id="c247a-180">Support multiple target frameworks</span></span>](../create-packages/supporting-multiple-target-frameworks.md)
- [<span data-ttu-id="c247a-181">패키지 버전 관리</span><span class="sxs-lookup"><span data-stu-id="c247a-181">Package versioning</span></span>](../reference/package-versioning.md)
- [<span data-ttu-id="c247a-182">지역화된 패키지 만들기</span><span class="sxs-lookup"><span data-stu-id="c247a-182">Creating localized packages</span></span>](../create-packages/creating-localized-packages.md)
