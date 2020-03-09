---
title: Visual Studio에서 NuGet 패키지 설치 및 사용
description: Visual Studio 프로젝트에서 NuGet 패키지를 설치하고 사용하는 프로세스에 대한 연습 자습서입니다.
author: karann-msft
ms.author: karann
ms.date: 07/24/2018
ms.topic: quickstart
ms.openlocfilehash: 96e138561390984d9def495ba5e091c43023cc92
ms.sourcegitcommit: c81561e93a7be467c1983d639158d4e3dc25b93a
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 03/02/2020
ms.locfileid: "78231333"
---
# <a name="quickstart-install-and-use-a-package-in-visual-studio-windows-only"></a><span data-ttu-id="dd175-103">빠른 시작: Visual Studio에서 패키지 설치 및 사용(Windows만 해당)</span><span class="sxs-lookup"><span data-stu-id="dd175-103">Quickstart: Install and use a package in Visual Studio (Windows only)</span></span>

<span data-ttu-id="dd175-104">NuGet 패키지는 다른 개발자가 프로젝트에서 사용하기 위해 제공하는 다시 사용할 수 있는 코드를 포함합니다.</span><span class="sxs-lookup"><span data-stu-id="dd175-104">NuGet packages contain reusable code that other developers make available to you for use in your projects.</span></span> <span data-ttu-id="dd175-105">배경 지식은 [NuGet이란?](../What-is-NuGet.md)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="dd175-105">See [What is NuGet?](../What-is-NuGet.md) for background.</span></span> <span data-ttu-id="dd175-106">패키지는 NuGet 패키지 관리자 또는 패키지 관리자 콘솔을 사용하여 Visual Studio 프로젝트에 설치됩니다.</span><span class="sxs-lookup"><span data-stu-id="dd175-106">Packages are installed into a Visual Studio project using the NuGet Package Manager or the Package Manager Console.</span></span> <span data-ttu-id="dd175-107">이 문서에서는 널리 사용되는 [Newtonsoft.Json](https://www.nuget.org/packages/Newtonsoft.Json/) 패키지 및 WPF(Windows Presentation Foundation) 프로젝트를 사용하는 프로세스를 보여줍니다.</span><span class="sxs-lookup"><span data-stu-id="dd175-107">This article demonstrates the process using the popular [Newtonsoft.Json](https://www.nuget.org/packages/Newtonsoft.Json/) package and a Windows Presentation Foundation (WPF) project.</span></span> <span data-ttu-id="dd175-108">같은 프로세스가 다른 .NET 또는 .NET Core 프로젝트에 모두에 적용됩니다.</span><span class="sxs-lookup"><span data-stu-id="dd175-108">The same process applies to any other .NET or .NET Core project.</span></span>

<span data-ttu-id="dd175-109">패키지가 설치되면 `using <namespace>`를 사용하여 코드에서 패키지를 참조합니다. 여기서 \<네임스페이스\>는 사용 중인 패키지에 특정됩니다.</span><span class="sxs-lookup"><span data-stu-id="dd175-109">Once installed, refer to the package in code with `using <namespace>` where \<namespace\> is specific to the package you're using.</span></span> <span data-ttu-id="dd175-110">일단 참조를 만들면 해당 API를 통해 패키지를 호출할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="dd175-110">Once the reference is made, you can call the package through its API.</span></span>

> [!Tip]
> <span data-ttu-id="dd175-111">**nuget.org 시작**: *nuget.org* 검색은 일반적으로 .NET 개발자가 고유의 애플리케이션에서 다시 사용할 수 있는 구성 요소를 찾는 방법입니다.</span><span class="sxs-lookup"><span data-stu-id="dd175-111">**Start with nuget.org**: Browsing *nuget.org* is how .NET developers typically find components they can reuse in their own applications.</span></span> <span data-ttu-id="dd175-112">*nuget.org*를 직접 검색하거나 이 문서에 표시된 대로 Visual Studio 내에서 패키지를 설치할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="dd175-112">You can search *nuget.org* directly or find and install packages within Visual Studio as shown in this article.</span></span> <span data-ttu-id="dd175-113">일반 정보는 [NuGet 패키지 찾기 및 평가](../consume-packages/finding-and-choosing-packages.md)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="dd175-113">For general information, see [Find and evaluate NuGet packages](../consume-packages/finding-and-choosing-packages.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="dd175-114">사전 요구 사항</span><span class="sxs-lookup"><span data-stu-id="dd175-114">Prerequisites</span></span>

- <span data-ttu-id="dd175-115">Visual Studio 2019의 .NET 데스크톱 개발 워크로드.</span><span class="sxs-lookup"><span data-stu-id="dd175-115">Visual Studio 2019 with the .NET Desktop Development workload.</span></span>

<span data-ttu-id="dd175-116">[visualstudio.com](https://www.visualstudio.com/)에서 추가 비용 없이 2019 Community 버전을 설치하거나 Professional 또는 Enterprise 버전을 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="dd175-116">You can install the 2019 Community edition for free from [visualstudio.com](https://www.visualstudio.com/) or use the Professional or Enterprise editions.</span></span>

<span data-ttu-id="dd175-117">Mac용 Visual Studio를 사용하는 경우 [Mac용 Visual Studio에서 패키지 설치 및 사용](install-and-use-a-package-in-visual-studio-mac.md)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="dd175-117">If you're using Visual Studio for Mac, see [Install and use a package in Visual Studio for Mac](install-and-use-a-package-in-visual-studio-mac.md).</span></span>

## <a name="create-a-project"></a><span data-ttu-id="dd175-118">프로젝트 만들기</span><span class="sxs-lookup"><span data-stu-id="dd175-118">Create a project</span></span>

<span data-ttu-id="dd175-119">NuGet 패키지는 패키지가 프로젝트와 동일한 대상 프레임워크를 지원하는 경우 어느 .NET 프로젝트에나 설치할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="dd175-119">NuGet packages can be installed into any .NET project, provided that the package supports the same target framework as the project.</span></span>

<span data-ttu-id="dd175-120">이 연습에서는 단순 WPF 앱을 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="dd175-120">For this walkthrough, use a simple WPF app.</span></span> <span data-ttu-id="dd175-121">**파일** > **새 프로젝트**를 사용하고 검색 상자에 **.NET**을 입력한 후 **WPF 앱(.NET Framework)** 을 선택하여 Visual Studio에서 프로젝트를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="dd175-121">Create a project in Visual Studio using **File** > **New Project**, typing **.NET** in the search box, and then selecting the **WPF App (.NET Framework)**.</span></span> <span data-ttu-id="dd175-122">**다음**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="dd175-122">Click **Next**.</span></span> <span data-ttu-id="dd175-123">메시지가 표시되면 **프레임워크**의 기본값을 그대로 적용합니다.</span><span class="sxs-lookup"><span data-stu-id="dd175-123">Accept the default values for **Framework** when prompted.</span></span>

<span data-ttu-id="dd175-124">Visual Studio에서 프로젝트를 만들고 솔루션 탐색기에서 열립니다.</span><span class="sxs-lookup"><span data-stu-id="dd175-124">Visual Studio creates the project, which opens in Solution Explorer.</span></span>

## <a name="add-the-newtonsoftjson-nuget-package"></a><span data-ttu-id="dd175-125">Newtonsoft.Json NuGet 패키지 추가</span><span class="sxs-lookup"><span data-stu-id="dd175-125">Add the Newtonsoft.Json NuGet package</span></span>

<span data-ttu-id="dd175-126">패키지를 설치하는 데는 NuGet 패키지 관리자 또는 패키지 관리자 콘솔을 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="dd175-126">To install the package, you can use either the NuGet Package Manager or the Package Manager Console.</span></span> <span data-ttu-id="dd175-127">패키지를 설치하면 NuGet에서 프로젝트 파일 또는 `packages.config` 파일에 종속성을 기록합니다(프로젝트 형식에 따라).</span><span class="sxs-lookup"><span data-stu-id="dd175-127">When you install a package, NuGet records the dependency in either your project file or a `packages.config` file (depending on the project format).</span></span> <span data-ttu-id="dd175-128">자세한 내용은 [패키지 소비 개요 및 워크플로](../consume-packages/Overview-and-Workflow.md)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="dd175-128">For more information, see [Package consumption overview and workflow](../consume-packages/Overview-and-Workflow.md).</span></span>

### <a name="nuget-package-manager"></a><span data-ttu-id="dd175-129">NuGet 패키지 관리자</span><span class="sxs-lookup"><span data-stu-id="dd175-129">NuGet Package Manager</span></span>

1. <span data-ttu-id="dd175-130">솔루션 탐색기에서 **참조**를 마우스 오른쪽 단추로 클릭하고 **NuGet 패키지 관리**를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="dd175-130">In Solution Explorer, right-click **References** and choose **Manage NuGet Packages**.</span></span>

    ![프로젝트 참조에 대한 NuGet 패키지 관리 명령](media/QS_Use-02-ManageNuGetPackages.png)

1. <span data-ttu-id="dd175-132">"nuget.org"를 **패키지 원본**으로 선택하고, **찾아보기** 탭을 선택하고, **Newtonsoft.Json**을 검색하고, 목록에서 해당 패키지를 선택하고, **설치**를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="dd175-132">Choose "nuget.org" as the **Package source**, select the **Browse** tab, search for **Newtonsoft.Json**, select that package in the list, and select **Install**:</span></span>

    ![Newtonsoft.Json 패키지 찾기](media/QS_Use-03-NewtonsoftJson.png)

    <span data-ttu-id="dd175-134">NuGet 패키지 관리자에 대한 자세한 내용은 [Visual Studio를 사용하여 패키지 설치 및 관리](../consume-packages/install-use-packages-visual-studio.md)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="dd175-134">If you want more information on the NuGet Package Manager, see [Install and manage packages using Visual Studio](../consume-packages/install-use-packages-visual-studio.md).</span></span>

1. <span data-ttu-id="dd175-135">라이선스 프롬프트를 수락합니다.</span><span class="sxs-lookup"><span data-stu-id="dd175-135">Accept any license prompts.</span></span>

1. <span data-ttu-id="dd175-136">(Visual Studio 2017만 해당) 패키지 관리 형식을 선택하라는 메시지가 표시되면 **프로젝트 파일에서 PackageReference**를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="dd175-136">(Visual Studio 2017 only) If prompted to select a package management format, select **PackageReference in project file**:</span></span>

    ![패키지 관리 형식 선택](media/QS_Use-03b-SelectFormat.png)

1. <span data-ttu-id="dd175-138">변경 내용을 검토하라는 메시지가 표시되면 **확인**을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="dd175-138">If prompted to review changes, select **OK**.</span></span>

### <a name="package-manager-console"></a><span data-ttu-id="dd175-139">패키지 관리자 콘솔</span><span class="sxs-lookup"><span data-stu-id="dd175-139">Package Manager Console</span></span>

1. <span data-ttu-id="dd175-140">**도구** > **NuGet 패키지 관리자** > **패키지 관리자 콘솔** 메뉴 명령을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="dd175-140">Select the **Tools** > **NuGet Package Manager** > **Package Manager Console** menu command.</span></span>

1. <span data-ttu-id="dd175-141">콘솔이 열리면 **기본 프로젝트** 드롭다운 목록에 패키지를 설치할 프로젝트가 표시되는지 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="dd175-141">Once the console opens, check that the **Default project** drop-down list shows the project into which you want to install the package.</span></span> <span data-ttu-id="dd175-142">솔루션에 단일 프로젝트가 있는 경우 이미 선택되어 있습니다.</span><span class="sxs-lookup"><span data-stu-id="dd175-142">If you have a single project in the solution, it is already selected.</span></span>

    ![Newtonsoft.Json 패키지 찾기](media/QS_Use-08-Console1.png)

1. <span data-ttu-id="dd175-144">`Install-Package Newtonsoft.Json` 명령을 입력합니다([Install-Package](../reference/ps-reference/ps-ref-install-package.md) 참조).</span><span class="sxs-lookup"><span data-stu-id="dd175-144">Enter the command `Install-Package Newtonsoft.Json` (see [Install-Package](../reference/ps-reference/ps-ref-install-package.md)).</span></span> <span data-ttu-id="dd175-145">콘솔 창은 명령에 대한 출력을 표시합니다.</span><span class="sxs-lookup"><span data-stu-id="dd175-145">The console window shows output for the command.</span></span> <span data-ttu-id="dd175-146">일반적으로 오류는 패키지가 프로젝트의 대상 프레임워크와 호환되지 않음을 나타냅니다.</span><span class="sxs-lookup"><span data-stu-id="dd175-146">Errors typically indicate that the package isn't compatible with the project's target framework.</span></span>

   <span data-ttu-id="dd175-147">패키지 관리자 콘솔에 대한 자세한 내용은 [패키지 관리자 콘솔을 사용하여 패키지 설치 및 관리](../consume-packages/install-use-packages-powershell.md)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="dd175-147">If you want more information on the Package Manager Console, see [Install and manage packages using Package Manager Console](../consume-packages/install-use-packages-powershell.md).</span></span>

## <a name="use-the-newtonsoftjson-api-in-the-app"></a><span data-ttu-id="dd175-148">앱에서 Newtonsoft.Json API 사용</span><span class="sxs-lookup"><span data-stu-id="dd175-148">Use the Newtonsoft.Json API in the app</span></span>

<span data-ttu-id="dd175-149">프로젝트의 Newtonsoft.Json 패키지에서 해당 `JsonConvert.SerializeObject` 메서드를 호출하여 개체를 사람이 인식할 수 있는 문자열로 변환할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="dd175-149">With the Newtonsoft.Json package in the project, you can call its `JsonConvert.SerializeObject` method to convert an object to a human-readable string.</span></span>

1. <span data-ttu-id="dd175-150">`MainWindow.xaml`을 열고 기존 `Grid` 요소를 다음과 같이 바꿉니다.</span><span class="sxs-lookup"><span data-stu-id="dd175-150">Open `MainWindow.xaml` and replace the existing `Grid` element with the following:</span></span>

    ```xaml
    <Grid Background="White">
        <StackPanel VerticalAlignment="Center">
            <Button Click="Button_Click" Width="100px" HorizontalAlignment="Center" Content="Click Me" Margin="10"/>
            <TextBlock Name="TextBlock" HorizontalAlignment="Center" Text="TextBlock" Margin="10"/>
        </StackPanel>
    </Grid>
    ```

1. <span data-ttu-id="dd175-151">`MainWindow.xaml.cs` 파일(`MainWindow.xaml` 노드 아래의 솔루션 탐색기에 있음)을 열고 `MainWindow` 클래스 내부에 다음 코드를 삽입합니다.</span><span class="sxs-lookup"><span data-stu-id="dd175-151">Open the `MainWindow.xaml.cs` file (located in Solution Explorer under the `MainWindow.xaml` node), and insert the following code inside the `MainWindow` class:</span></span>

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

1. <span data-ttu-id="dd175-152">Newtonsoft.Json 패키지를 프로젝트에 추가했더라도 코드 파일 맨 위에 `using` 문이 필요한 경우 `JsonConvert` 아래에 빨간색 물결선이 나타납니다.</span><span class="sxs-lookup"><span data-stu-id="dd175-152">Even though you added the Newtonsoft.Json package to the project, red squiggles appears under `JsonConvert` because you need a `using` statement at the top of the code file:</span></span>

    ```cs
    using Newtonsoft.Json;
    ```

1. <span data-ttu-id="dd175-153">F5 키를 누르거나 **디버그** > **디버깅 시작**을 선택하여 앱을 빌드하고 실행합니다.</span><span class="sxs-lookup"><span data-stu-id="dd175-153">Build and run the app by pressing F5 or selecting **Debug** > **Start Debugging**:</span></span>

    ![WPF 앱의 초기 출력](media/QS_Use-06-AppStart.png)

1. <span data-ttu-id="dd175-155">JSON 텍스트로 바꾼 텍스트 블록의 내용을 보려면 단추를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="dd175-155">Select on the button to see the contents of the TextBlock replaced with some JSON text:</span></span>

    ![단추를 선택한 후 WPF 앱의 출력](media/QS_Use-07-AppEnd.png)

## <a name="related-video"></a><span data-ttu-id="dd175-157">관련 동영상</span><span class="sxs-lookup"><span data-stu-id="dd175-157">Related video</span></span>

> [!Video https://channel9.msdn.com/Series/NuGet-101/Install-and-Use-a-NuGet-Package-with-Visual-Studio-2-of-5/player]

<span data-ttu-id="dd175-158">[Channel 9](https://channel9.msdn.com/Series/NuGet-101) 및 [YouTube](https://www.youtube.com/playlist?list=PLdo4fOcmZ0oVLvfkFk8O9h6v2Dcdh2bh_)에서 더 많은 NuGet 비디오를 확인하세요.</span><span class="sxs-lookup"><span data-stu-id="dd175-158">Find more NuGet videos on [Channel 9](https://channel9.msdn.com/Series/NuGet-101) and [YouTube](https://www.youtube.com/playlist?list=PLdo4fOcmZ0oVLvfkFk8O9h6v2Dcdh2bh_).</span></span>

## <a name="next-steps"></a><span data-ttu-id="dd175-159">다음 단계</span><span class="sxs-lookup"><span data-stu-id="dd175-159">Next steps</span></span>

<span data-ttu-id="dd175-160">첫 번째 NuGet 패키지를 설치하고 사용하시게 된 것을 축하드립니다.</span><span class="sxs-lookup"><span data-stu-id="dd175-160">Congratulations on installing and using your first NuGet package!</span></span>

> [!div class="nextstepaction"]
> [<span data-ttu-id="dd175-161">Visual Studio를 사용하여 패키지 설치 및 관리</span><span class="sxs-lookup"><span data-stu-id="dd175-161">Install and manage packages using Visual Studio</span></span>](../consume-packages/install-use-packages-visual-studio.md)

> [!div class="nextstepaction"]
> [<span data-ttu-id="dd175-162">패키지 관리자 콘솔을 사용하여 패키지 설치 및 관리</span><span class="sxs-lookup"><span data-stu-id="dd175-162">Install and manage packages using Package Manager Console</span></span>](../consume-packages/install-use-packages-powershell.md)

<span data-ttu-id="dd175-163">NuGet에서 제공하는 다른 기능을 탐색하려면 아래 링크를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="dd175-163">To explore more that NuGet has to offer, select the links below.</span></span>

- [<span data-ttu-id="dd175-164">패키지 사용 개요 및 워크플로</span><span class="sxs-lookup"><span data-stu-id="dd175-164">Overview and workflow of package consumption</span></span>](../consume-packages/overview-and-workflow.md)
- [<span data-ttu-id="dd175-165">패키지 찾기 및 선택</span><span class="sxs-lookup"><span data-stu-id="dd175-165">Finding and choosing packages</span></span>](../consume-packages/finding-and-choosing-packages.md)
- [<span data-ttu-id="dd175-166">프로젝트 파일의 패키지 참조</span><span class="sxs-lookup"><span data-stu-id="dd175-166">Package references in project files</span></span>](../consume-packages/package-references-in-project-files.md)
