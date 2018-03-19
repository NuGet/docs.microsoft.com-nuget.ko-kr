---
title: "Visual Studio 내에서 NuGet 패키지 사용에 대한 소개 가이드 | Microsoft Docs"
author: kraigb
ms.author: kraigb
manager: ghogen
ms.date: 01/23/2018
ms.topic: get-started-article
ms.prod: nuget
ms.technology: 
description: "Visual Studio 프로젝트에서 NuGet 패키지를 설치하고 사용하는 프로세스에 대한 연습 자습서입니다."
keywords: "NuGet 설치, NuGet 패키지 사용, NuGet 패키지 설치, NuGet 패키지 참조, NuGet 패키지 사용"
ms.reviewer:
- karann-msft
- unniravindranathan
ms.openlocfilehash: ff905fec6d6af4fa40fd4331cb970121b6eb0879
ms.sourcegitcommit: 74c21b406302288c158e8ae26057132b12960be8
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 03/15/2018
---
# <a name="install-and-use-a-package-in-visual-studio"></a><span data-ttu-id="17495-104">Visual Studio에서 패키지 설치 및 사용</span><span class="sxs-lookup"><span data-stu-id="17495-104">Install and use a package in Visual Studio</span></span>

<span data-ttu-id="17495-105">NuGet 패키지는 다른 개발자가 프로젝트에서 사용하기 위해 제공하는 다시 사용할 수 있는 코드를 포함합니다.</span><span class="sxs-lookup"><span data-stu-id="17495-105">NuGet packages contain reusable code that other developers make available to you for use in your projects.</span></span> <span data-ttu-id="17495-106">배경 지식은 [NuGet이란?](../What-is-NuGet.md)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="17495-106">See [What is NuGet?](../What-is-NuGet.md) for background.</span></span> <span data-ttu-id="17495-107">패키지는 이 문서에 설명된 대로 널리 사용되는 [Newtonsoft.Json](https://www.nuget.org/packages/Newtonsoft.Json/) 패키지 및 UWP(유니버설 Windows 플랫폼) 프로젝트에 대해 패키지 관리자 UI 또는 패키지 관리자 콘솔을 사용하여 Visual Studio 프로젝트에 설치됩니다.</span><span class="sxs-lookup"><span data-stu-id="17495-107">Packages are installed into a Visual Studio project using the Package Manager UI or the Package Manager Console, as described in this article for the popular [Newtonsoft.Json](https://www.nuget.org/packages/Newtonsoft.Json/) package and a Universal Windows Platform (UWP) project.</span></span>

<span data-ttu-id="17495-108">패키지가 설치되면 `using <namespace>`를 사용하여 코드에서 패키지를 참조합니다. 여기서 \<네임스페이스\>는 사용 중인 패키지에 특정됩니다.</span><span class="sxs-lookup"><span data-stu-id="17495-108">Once installed, refer to the package in code with `using <namespace>` where \<namespace\> is specific to the package you're using.</span></span> <span data-ttu-id="17495-109">일단 참조를 만들면 해당 API를 통해 패키지를 호출할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="17495-109">Once the reference is made, you can call the package through its API.</span></span>

> [!Tip]
> <span data-ttu-id="17495-110">**nuget.org 시작**: nuget.org 검색은 일반적으로 .NET 개발자가 고유의 응용 프로그램에서 다시 사용할 수 있는 구성 요소를 찾는 방법입니다.</span><span class="sxs-lookup"><span data-stu-id="17495-110">**Start with nuget.org**: Browsing nuget.org is how .NET developers typically find components they can reuse in their own applications.</span></span> <span data-ttu-id="17495-111">nuget.org를 직접 검색하거나 이 문서에 표시된 대로 Visual Studio 내에서 패키지를 설치할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="17495-111">You can search nuget.org directly or find and install packages within Visual Studio as shown in this article.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="17495-112">전제 조건</span><span class="sxs-lookup"><span data-stu-id="17495-112">Prerequisites</span></span>

- <span data-ttu-id="17495-113">Visual Studio 2017(유니버설 Windows 플랫폼 개발 워크로드 포함) 또는</span><span class="sxs-lookup"><span data-stu-id="17495-113">Visual Studio 2017 with the Universal Windows Platform development workload, or</span></span>
- <span data-ttu-id="17495-114">Visual Studio 2015 업데이트 3(유니버설 Windows 앱용 도구 포함).</span><span class="sxs-lookup"><span data-stu-id="17495-114">Visual Studio 2015 Update 3 with Tools for Universal Windows Apps.</span></span>

<span data-ttu-id="17495-115">[visualstudio.com](https://www.visualstudio.com/)에서 추가 비용 없이 2017 Community 버전을 설치하거나 Professional 또는 Enterprise 버전을 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="17495-115">You can install the 2017 Community edition for free from [visualstudio.com](https://www.visualstudio.com/) or use the Professional or Enterprise editions.</span></span>

## <a name="create-a-project"></a><span data-ttu-id="17495-116">프로젝트 만들기</span><span class="sxs-lookup"><span data-stu-id="17495-116">Create a project</span></span>

<span data-ttu-id="17495-117">NuGet 패키지는 일종의 .NET 프로젝트에 설치할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="17495-117">NuGet packages can be installed into a .NET project of some kind.</span></span> <span data-ttu-id="17495-118">이 연습에서는 간단한 유니버설 Windows(UWP) 앱을 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="17495-118">For this walkthrough, you use a simple Universal Windows (UWP) app.</span></span> <span data-ttu-id="17495-119">**파일 > 새 프로젝트...**를 사용하고 **Windows 유니버설 > 빈 앱(유니버설 Windows)**을 선택하여 Visual Studio에서 프로젝트를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="17495-119">Create a project in Visual Studio using **File > New Project...** and selecting the **Windows Universal > Blank App (Universal Windows)**.</span></span> <span data-ttu-id="17495-120">메시지가 표시되면 대상 버전 및 최소 버전에 대한 기본값을 적용합니다.</span><span class="sxs-lookup"><span data-stu-id="17495-120">Accept the default values for Target Version and Minimum Version when prompted.</span></span>

## <a name="add-the-newtonsoftjson-nuget-package"></a><span data-ttu-id="17495-121">Newtonsoft.Json NuGet 패키지 추가</span><span class="sxs-lookup"><span data-stu-id="17495-121">Add the Newtonsoft.Json NuGet package</span></span>

<span data-ttu-id="17495-122">패키지를 설치하는 데는 패키지 관리자 UI 또는 패키지 관리자 콘솔을 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="17495-122">To install the package, you can use either the Package Manager UI or the Package Manager Console.</span></span> <span data-ttu-id="17495-123">패키지를 설치하면 NuGet에서 프로젝트 파일 또는 `packages.config` 파일에 종속성을 기록합니다.</span><span class="sxs-lookup"><span data-stu-id="17495-123">When you install a package, NuGet records the dependency in either your project file or a `packages.config` file.</span></span> <span data-ttu-id="17495-124">자세한 내용은 [패키지 소비 개요 및 워크플로](../consume-packages/Overview-and-Workflow.md)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="17495-124">For more information, see [Package consumption overview and workflow](../consume-packages/Overview-and-Workflow.md).</span></span>

### <a name="package-manager-ui"></a><span data-ttu-id="17495-125">패키지 관리자 UI</span><span class="sxs-lookup"><span data-stu-id="17495-125">Package Manager UI</span></span>

1. <span data-ttu-id="17495-126">솔루션 탐색기에서 **참조**를 마우스 오른쪽 단추로 클릭하고 **NuGet 패키지 관리**를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="17495-126">In Solution Explorer, right-click **References** and choose **Manage NuGet Packages**.</span></span>

    ![프로젝트 참조에 대한 NuGet 패키지 관리 명령](media/QS_Use-02-ManageNuGetPackages.png)

1. <span data-ttu-id="17495-128">"nuget.org"를 **패키지 원본**으로 선택하고, **찾아보기** 탭을 선택하고, **Newtonsoft.Json**을 검색하고, 목록에서 해당 패키지를 선택하고, **설치**를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="17495-128">Choose "nuget.org" as the **Package source**, select the **Browse** tab, search for **Newtonsoft.Json**, select that package in the list, and select **Install**:</span></span>

    ![Newtonsoft.Json 패키지 찾기](media/QS_Use-03-NewtonsoftJson.png)

1. <span data-ttu-id="17495-130">라이선스 프롬프트를 수락합니다.</span><span class="sxs-lookup"><span data-stu-id="17495-130">Accept any license prompts.</span></span>

1. <span data-ttu-id="17495-131">(Visual Studio 2017) 패키지 관리 형식을 선택하라는 메시지가 표시되면 **프로젝트 파일에서 PackageReference**를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="17495-131">(Visual Studio 2017) If prompted to select a package management format, select **PackageReference in project file**:</span></span>

    ![패키지 참조 형식 선택](media/QS_Use-03b-SelectFormat.png)

1. <span data-ttu-id="17495-133">변경 내용을 검토하라는 메시지가 표시되면 **확인**을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="17495-133">If prompted to review changes, select **OK**.</span></span>

### <a name="package-manager-console"></a><span data-ttu-id="17495-134">패키지 관리자 콘솔</span><span class="sxs-lookup"><span data-stu-id="17495-134">Package Manager Console</span></span>

1. <span data-ttu-id="17495-135">**도구 > NuGet 패키지 관리자 > 패키지 관리자 콘솔** 메뉴 명령을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="17495-135">Select the **Tools > NuGet Package Manager > Package Manager Console** menu command.</span></span>

1. <span data-ttu-id="17495-136">콘솔이 열리면 **기본 프로젝트** 드롭다운 목록에 패키지를 설치할 프로젝트가 표시되는지 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="17495-136">Once the console opens, check that the **Default project** drop-down list shows the project into which you want to install the package.</span></span> <span data-ttu-id="17495-137">솔루션에 단일 프로젝트가 있는 경우 이미 선택되어 있습니다.</span><span class="sxs-lookup"><span data-stu-id="17495-137">If you have a single project in the solution, it is already selected.</span></span>

    ![Newtonsoft.Json 패키지 찾기](media/QS_Use-08-Console1.png)

1. <span data-ttu-id="17495-139">`Install-Package Newtonsoft.json` 명령을 입력합니다([Install-Package](../tools/ps-ref-install-package.md) 참조).</span><span class="sxs-lookup"><span data-stu-id="17495-139">Enter the command `Install-Package Newtonsoft.json` (see [Install-Package](../tools/ps-ref-install-package.md)).</span></span> <span data-ttu-id="17495-140">콘솔 창은 명령에 대한 출력을 표시합니다.</span><span class="sxs-lookup"><span data-stu-id="17495-140">The console window shows output for the command.</span></span> <span data-ttu-id="17495-141">일반적으로 오류는 패키지가 프로젝트의 대상 프레임워크와 호환되지 않음을 나타냅니다.</span><span class="sxs-lookup"><span data-stu-id="17495-141">Errors typically indicate that the package isn't compatible with the project's target framework.</span></span>

## <a name="use-the-newtonsoftjson-api-in-the-app"></a><span data-ttu-id="17495-142">앱에서 Newtonsoft.Json API 사용</span><span class="sxs-lookup"><span data-stu-id="17495-142">Use the Newtonsoft.Json API in the app</span></span>

<span data-ttu-id="17495-143">프로젝트의 Newtonsoft.Json 패키지에서 해당 `JsonConvert.SerializeObject` 메서드를 호출하여 개체를 사람이 인식할 수 있는 문자열로 변환할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="17495-143">With the Newtonsoft.Json package in the project, you can call its `JsonConvert.SerializeObject` method to convert an object to a human-readable string.</span></span>

1. <span data-ttu-id="17495-144">`MainPage.xaml`을 열고 기존 `Grid` 요소를 다음과 같이 바꿉니다.</span><span class="sxs-lookup"><span data-stu-id="17495-144">Open `MainPage.xaml` and replace the existing `Grid` element with the following:</span></span>

    ```xaml
    <Grid Background="{ThemeResource ApplicationPageBackgroundThemeBrush}">
        <StackPanel VerticalAlignment="Center">
            <Button Click="Button_Click" Content="Click Me" Margin="10"/>
            <TextBlock Name="TextBlock" Text="TextBlock" Margin="10"/>
        </StackPanel>
    </Grid>
    ```

1. <span data-ttu-id="17495-145">`MainPage.xaml.cs` 파일(`MainPage.xaml` 노드 아래의 솔루션 탐색기에 있음)을 열고 `MainPage` 생성자 내부에 다음 코드를 삽입합니다.</span><span class="sxs-lookup"><span data-stu-id="17495-145">Open the `MainPage.xaml.cs` file (located in Solution Explorer under the `MainPage.xaml` node), and insert the following code inside the `MainPage` constructor:</span></span>

    ```cs
    public class Account
    {
        public string Name { get; set; }
        public string Email { get; set; }
        public DateTime DOB { get; set; }
    }

    private void Button_Click(object sender, RoutedEventArgs e)
    {
        Account account = new Account
        {
            Name = "John Doe",
            Email = "john@microsoft.com",
            DOB = new DateTime(1980, 2, 20, 0, 0, 0, DateTimeKind.Utc),
        };
        string json = JsonConvert.SerializeObject(account, Formatting.Indented);
        TextBlock.Text = json;
    }
    ```

1. <span data-ttu-id="17495-146">Newtonsoft.Json 패키지를 프로젝트에 추가했더라도 코드 파일 맨 위에 `using` 문이 필요한 경우 `JsonConvert` 아래에 빨간색 물결선이 나타납니다.</span><span class="sxs-lookup"><span data-stu-id="17495-146">Even though you added the Newtonsoft.Json package to the project, red squiggles appears under `JsonConvert` because you need a `using` statement at the top of the code file:</span></span>

    ```cs
    using Newtonsoft.json;
    ```

1. <span data-ttu-id="17495-147">F5 키를 누르거나 **디버그 > 디버깅 시작**을 선택하여 앱을 빌드하고 실행합니다.</span><span class="sxs-lookup"><span data-stu-id="17495-147">Build and run the app by pressing F5 or selecting **Debug > Start Debugging**:</span></span>

    ![UWP 앱의 초기 출력](media/QS_Use-06-AppStart.png)

1. <span data-ttu-id="17495-149">JSON 텍스트로 바꾼 텍스트 블록의 내용을 보려면 단추를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="17495-149">Select on the button to see the contents of the TextBlock replaced with some JSON text:</span></span>

    ![단추를 선택한 후 UWP 앱의 출력](media/QS_Use-07-AppEnd.png)

## <a name="related-articles"></a><span data-ttu-id="17495-151">관련 문서</span><span class="sxs-lookup"><span data-stu-id="17495-151">Related articles</span></span>

- [<span data-ttu-id="17495-152">패키지 사용 개요 및 워크플로</span><span class="sxs-lookup"><span data-stu-id="17495-152">Overview and workflow of package consumption</span></span>](../consume-packages/overview-and-workflow.md)
- [<span data-ttu-id="17495-153">패키지 찾기 및 선택</span><span class="sxs-lookup"><span data-stu-id="17495-153">Finding and choosing packages</span></span>](../consume-packages/finding-and-choosing-packages.md)
- [<span data-ttu-id="17495-154">패키지 설치 방법</span><span class="sxs-lookup"><span data-stu-id="17495-154">Ways to install a package</span></span>](../consume-packages/ways-to-install-a-package.md)
- [<span data-ttu-id="17495-155">NuGet 동작 구성</span><span class="sxs-lookup"><span data-stu-id="17495-155">Configuring NuGet Behavior</span></span>](../consume-packages/configuring-nuget-behavior.md)
