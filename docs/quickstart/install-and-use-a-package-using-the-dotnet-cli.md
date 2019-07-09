---
title: dotnet CLI를 통한 NuGet 패키지 사용에 대한 소개 가이드
description: .NET Core 프로젝트에서 NuGet 패키지를 설치하고 사용하는 프로세스에 대한 연습 자습서입니다.
author: karann-msft
ms.author: karann
ms.date: 01/23/2018
ms.topic: quickstart
ms.openlocfilehash: 1060d98278fed89ac63ee17c1896ae8bdce72a9e
ms.sourcegitcommit: b6810860b77b2d50aab031040b047c20a333aca3
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 06/28/2019
ms.locfileid: "67426161"
---
# <a name="quickstart-install-and-use-a-package-using-the-dotnet-cli"></a><span data-ttu-id="a6ea9-103">빠른 시작: dotnet CLI를 사용하여 패키지 설치 및 사용</span><span class="sxs-lookup"><span data-stu-id="a6ea9-103">Quickstart: Install and use a package using the dotnet CLI</span></span>

<span data-ttu-id="a6ea9-104">NuGet 패키지는 다른 개발자가 프로젝트에서 사용하기 위해 제공하는 다시 사용할 수 있는 코드를 포함합니다.</span><span class="sxs-lookup"><span data-stu-id="a6ea9-104">NuGet packages contain reusable code that other developers make available to you for use in your projects.</span></span> <span data-ttu-id="a6ea9-105">배경 지식은 [NuGet이란?](../What-is-NuGet.md)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="a6ea9-105">See [What is NuGet?](../What-is-NuGet.md) for background.</span></span> <span data-ttu-id="a6ea9-106">패키지는 이 문서에 설명된 대로 널리 사용되는 [Newtonsoft.Json](https://www.nuget.org/packages/Newtonsoft.Json/) 패키지에 대해 `dotnet add package` 명령을 사용하여 .NET Core 프로젝트에 설치됩니다.</span><span class="sxs-lookup"><span data-stu-id="a6ea9-106">Packages are installed into a .NET Core project using the `dotnet add package` command as described in this article for the popular [Newtonsoft.Json](https://www.nuget.org/packages/Newtonsoft.Json/) package.</span></span>

<span data-ttu-id="a6ea9-107">패키지가 설치되면 `using <namespace>`를 사용하여 코드에서 패키지를 참조합니다. 여기서 \<네임스페이스\>는 사용 중인 패키지에 특정됩니다.</span><span class="sxs-lookup"><span data-stu-id="a6ea9-107">Once installed, refer to the package in code with `using <namespace>` where \<namespace\> is specific to the package you're using.</span></span> <span data-ttu-id="a6ea9-108">그런 다음, 패키지의 API를 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="a6ea9-108">You can then use the package's API.</span></span>

> [!Tip]
> <span data-ttu-id="a6ea9-109">**nuget.org 시작**: nuget.org 검색은 일반적으로 .NET 개발자가 고유의 애플리케이션에서 다시 사용할 수 있는 구성 요소를 찾는 방법입니다.</span><span class="sxs-lookup"><span data-stu-id="a6ea9-109">**Start with nuget.org**: Browsing nuget.org is how .NET developers typically find components they can reuse in their own applications.</span></span> <span data-ttu-id="a6ea9-110">nuget.org를 직접 검색하거나 이 문서에 표시된 대로 Visual Studio 내에서 패키지를 설치할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="a6ea9-110">You can search nuget.org directly or find and install packages within Visual Studio as shown in this article.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="a6ea9-111">전제 조건</span><span class="sxs-lookup"><span data-stu-id="a6ea9-111">Prerequisites</span></span>

- <span data-ttu-id="a6ea9-112">`dotnet` 명령줄 도구를 제공하는 [.NET Core SDK](https://www.microsoft.com/net/download/).</span><span class="sxs-lookup"><span data-stu-id="a6ea9-112">The [.NET Core SDK](https://www.microsoft.com/net/download/), which provides the `dotnet` command-line tool.</span></span>

## <a name="create-a-project"></a><span data-ttu-id="a6ea9-113">프로젝트 만들기</span><span class="sxs-lookup"><span data-stu-id="a6ea9-113">Create a project</span></span>

<span data-ttu-id="a6ea9-114">NuGet 패키지는 일종의 .NET 프로젝트에 설치할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="a6ea9-114">NuGet packages can be installed into a .NET project of some kind.</span></span> <span data-ttu-id="a6ea9-115">이 연습에서는 다음과 같이 간단한 .NET Core 콘솔 프로젝트를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="a6ea9-115">For this walkthrough, create a simple .NET Core console project as follows:</span></span>

1. <span data-ttu-id="a6ea9-116">프로젝트의 폴더를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="a6ea9-116">Create a folder for the project.</span></span>

1. <span data-ttu-id="a6ea9-117">다음 명령을 사용하여 프로젝트를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="a6ea9-117">Create the project using the following command:</span></span>

    ```cli
    dotnet new console
    ```

1. <span data-ttu-id="a6ea9-118">`dotnet run`을 사용하여 앱이 제대로 만들어졌는지 테스트합니다.</span><span class="sxs-lookup"><span data-stu-id="a6ea9-118">Use `dotnet run` to test that the app has been created properly.</span></span>

## <a name="add-the-newtonsoftjson-nuget-package"></a><span data-ttu-id="a6ea9-119">Newtonsoft.Json NuGet 패키지 추가</span><span class="sxs-lookup"><span data-stu-id="a6ea9-119">Add the Newtonsoft.Json NuGet package</span></span>

1. <span data-ttu-id="a6ea9-120">다음 명령을 사용하여 `Newtonsoft.json` 패키지를 설치합니다.</span><span class="sxs-lookup"><span data-stu-id="a6ea9-120">Use the following command to install the `Newtonsoft.json` package:</span></span>

    ```cli
    dotnet add package Newtonsoft.Json
    ```

2. <span data-ttu-id="a6ea9-121">명령이 완료된 후 `.csproj` 파일을 열어 추가된 참조를 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="a6ea9-121">After the command completes, open the `.csproj` file to see the added reference:</span></span>

    ```xml
   <ItemGroup>
    <PackageReference Include="Newtonsoft.Json" Version="12.0.1" />
   </ItemGroup>
    ```

## <a name="use-the-newtonsoftjson-api-in-the-app"></a><span data-ttu-id="a6ea9-122">앱에서 Newtonsoft.Json API 사용</span><span class="sxs-lookup"><span data-stu-id="a6ea9-122">Use the Newtonsoft.Json API in the app</span></span>

1. <span data-ttu-id="a6ea9-123">`Program.cs` 파일을 열고 파일 맨 위에 다음 줄을 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="a6ea9-123">Open the `Program.cs` file and add the following line at the top of the file:</span></span>

    ```cs
    using Newtonsoft.Json;
    ```

1. <span data-ttu-id="a6ea9-124">`class Program` 줄 앞에 다음 코드를 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="a6ea9-124">Add the following code before the `class Program` line:</span></span>

    ```cs
    public class Account
    {
        public string Name { get; set; }
        public string Email { get; set; }
        public DateTime DOB { get; set; }
    }
    ```

1. <span data-ttu-id="a6ea9-125">`Main` 함수를 다음과 같이 바꿉니다.</span><span class="sxs-lookup"><span data-stu-id="a6ea9-125">Replace the `Main` function with the following:</span></span>

    ```cs
    static void Main(string[] args)
    {
        Account account = new Account
        {
            Name = "John Doe",
            Email = "john@nuget.org",
            DOB = new DateTime(1980, 2, 20, 0, 0, 0, DateTimeKind.Utc),
        };

        string json = JsonConvert.SerializeObject(account, Formatting.Indented);
        Console.WriteLine(json);
    }
    ```

1. <span data-ttu-id="a6ea9-126">`dotnet run` 명령을 사용하여 앱을 빌드하고 실행합니다.</span><span class="sxs-lookup"><span data-stu-id="a6ea9-126">Build and run the app by using the `dotnet run` command.</span></span> <span data-ttu-id="a6ea9-127">출력은 코드에서 `Account` 개체의 JSON 표현이어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="a6ea9-127">The output should be the JSON representation of the `Account` object in the code:</span></span>

    ```output
    {
      "Name": "John Doe",
      "Email": "john@nuget.org",
      "DOB": "1980-02-20T00:00:00Z"
    }
    ```

## <a name="related-articles"></a><span data-ttu-id="a6ea9-128">관련 문서</span><span class="sxs-lookup"><span data-stu-id="a6ea9-128">Related articles</span></span>

- [<span data-ttu-id="a6ea9-129">dotnet CLI를 사용하여 패키지 설치 및 사용</span><span class="sxs-lookup"><span data-stu-id="a6ea9-129">Install and use packages using the dotnet CLI</span></span>](../consume-packages/install-use-packages-dotnet-cli.md)
- [<span data-ttu-id="a6ea9-130">패키지 사용 개요 및 워크플로</span><span class="sxs-lookup"><span data-stu-id="a6ea9-130">Overview and workflow of package consumption</span></span>](../consume-packages/overview-and-workflow.md)
- [<span data-ttu-id="a6ea9-131">패키지 찾기 및 선택</span><span class="sxs-lookup"><span data-stu-id="a6ea9-131">Finding and choosing packages</span></span>](../consume-packages/finding-and-choosing-packages.md)
- [<span data-ttu-id="a6ea9-132">일반적인 NuGet 구성</span><span class="sxs-lookup"><span data-stu-id="a6ea9-132">Common NuGet configurations</span></span>](../consume-packages/configuring-nuget-behavior.md)
