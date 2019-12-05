---
title: dotnet CLI를 사용하여 NuGet 패키지 설치 및 관리
description: dotnet CLI를 사용하여 NuGet 패키지를 작업하기 위한 지침입니다.
author: mikejo5000
ms.author: mikejo
ms.date: 06/03/2019
ms.topic: conceptual
ms.openlocfilehash: 67cca81c48970c7f2e2cf0a64ee5ba57704a31e2
ms.sourcegitcommit: fe34b1fc79d6a9b2943a951f70b820037d2dd72d
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 12/04/2019
ms.locfileid: "74825168"
---
# <a name="install-and-manage-packages-using-the-dotnet-cli"></a><span data-ttu-id="f2cd3-103">dotnet CLI를 사용하여 패키지 설치 및 관리</span><span class="sxs-lookup"><span data-stu-id="f2cd3-103">Install and manage packages using the dotnet CLI</span></span>

<span data-ttu-id="f2cd3-104">CLI 도구를 사용하면 프로젝트 및 솔루션에서 NuGet 패키지를 쉽게 설치, 제거 및 업데이트할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="f2cd3-104">The CLI tool allows you to easily install, uninstall, and update NuGet packages in projects and solutions.</span></span> <span data-ttu-id="f2cd3-105">Windows, Mac OS X 및 Linux에서 실행됩니다.</span><span class="sxs-lookup"><span data-stu-id="f2cd3-105">It runs on Windows, Mac OS X, and Linux.</span></span>

<span data-ttu-id="f2cd3-106">dotnet CLI는 .NET Core, .NET Standard 프로젝트(SDK 스타일 프로젝트 형식) 및 기타 모든 SDK 스타일 프로젝트(예: .NET Framework를 대상으로 하는 SDK 스타일 프로젝트)에서 사용하기 위한 것입니다.</span><span class="sxs-lookup"><span data-stu-id="f2cd3-106">The dotnet CLI is for use in your .NET Core and .NET Standard project (SDK-style project types), and for any other SDK-style projects (for example, an SDK-style project that targets .NET Framework).</span></span> <span data-ttu-id="f2cd3-107">자세한 내용은 [SDK 특성](/dotnet/core/tools/csproj#additions)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="f2cd3-107">For more information, see [SDK attribute](/dotnet/core/tools/csproj#additions).</span></span>

<span data-ttu-id="f2cd3-108">이 문서에서는 가장 일반적인 몇 가지 dotnet CLI 명령에 대한 기본 사용법을 보여줍니다.</span><span class="sxs-lookup"><span data-stu-id="f2cd3-108">This article shows you basic usage for a few of the most common dotnet CLI commands.</span></span> <span data-ttu-id="f2cd3-109">이러한 명령의 대부분의 경우 CLI 도구는 프로젝트 파일이 명령에 지정되지 않는 한 현재 디렉터리에서 프로젝트 파일을 찾습니다(프로젝트 파일은 선택적 스위치임).</span><span class="sxs-lookup"><span data-stu-id="f2cd3-109">For most of these commands, the CLI tool looks for a project file in the current directory, unless a project file is specified in the command (the project file is an optional switch).</span></span> <span data-ttu-id="f2cd3-110">사용할 수 있는 명령 및 인수의 전체 목록은 [.NET Core CLI (명령줄 인터페이스) 도구](../reference/dotnet-commands.md)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="f2cd3-110">For a complete list of commands and the arguments you may use, see the [.NET Core command-line interface (CLI) tools](../reference/dotnet-commands.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="f2cd3-111">전제 조건</span><span class="sxs-lookup"><span data-stu-id="f2cd3-111">Prerequisites</span></span>

- <span data-ttu-id="f2cd3-112">`dotnet` 명령줄 도구를 제공하는 [.NET Core SDK](https://www.microsoft.com/net/download/).</span><span class="sxs-lookup"><span data-stu-id="f2cd3-112">The [.NET Core SDK](https://www.microsoft.com/net/download/), which provides the `dotnet` command-line tool.</span></span> <span data-ttu-id="f2cd3-113">Visual Studio 2017부터 dotnet CLI는 모든 .NET Core 관련 워크로드와 함께 자동으로 설치됩니다.</span><span class="sxs-lookup"><span data-stu-id="f2cd3-113">Starting in Visual Studio 2017, the dotnet CLI is automatically installed with any .NET Core related workloads.</span></span>

## <a name="install-a-package"></a><span data-ttu-id="f2cd3-114">패키지 설치</span><span class="sxs-lookup"><span data-stu-id="f2cd3-114">Install a package</span></span>

<span data-ttu-id="f2cd3-115">[dotnet add package](/dotnet/core/tools/dotnet-add-package?tabs=netcore2x)는 패키지 참조를 프로젝트 파일에 추가한 다음, `dotnet restore`를 추가하여 패키지를 설치합니다.</span><span class="sxs-lookup"><span data-stu-id="f2cd3-115">[dotnet add package](/dotnet/core/tools/dotnet-add-package?tabs=netcore2x) adds a package reference to the project file, then runs `dotnet restore` to install the package.</span></span>

1. <span data-ttu-id="f2cd3-116">명령줄을 열고 프로젝트 파일이 포함된 디렉터리로 전환합니다.</span><span class="sxs-lookup"><span data-stu-id="f2cd3-116">Open a command line and switch to the directory that contains your project file.</span></span>

2. <span data-ttu-id="f2cd3-117">다음 명령을 사용하여 Nuget 패키지를 설치합니다.</span><span class="sxs-lookup"><span data-stu-id="f2cd3-117">Use the following command to install a Nuget package:</span></span>

    ```dotnetcli
    dotnet add package <PACKAGE_NAME>
    ```

    <span data-ttu-id="f2cd3-118">예를 들어 `Newtonsoft.Json` 패키지를 설치하려면 다음 명령을 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="f2cd3-118">For example, to install the `Newtonsoft.Json` package, use the following command</span></span>

    ```dotnetcli
    dotnet add package Newtonsoft.Json
    ```

3. <span data-ttu-id="f2cd3-119">명령이 완료된 후 프로젝트 파일을 보고 패키지가 설치되었는지 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="f2cd3-119">After the command completes, look at the project file to make sure the package was installed.</span></span>

   <span data-ttu-id="f2cd3-120">`.csproj` 파일을 열어 추가된 참조를 볼 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="f2cd3-120">You can open the `.csproj` file to see the added reference:</span></span>

    ```xml
   <ItemGroup>
    <PackageReference Include="Newtonsoft.Json" Version="12.0.1" />
   </ItemGroup>
    ```

## <a name="install-a-specific-version-of-a-package"></a><span data-ttu-id="f2cd3-121">특정 버전의 패키지 설치</span><span class="sxs-lookup"><span data-stu-id="f2cd3-121">Install a specific version of a package</span></span>

<span data-ttu-id="f2cd3-122">버전이 지정되지 않은 경우 NuGet은 패키지의 최신 버전을 설치합니다.</span><span class="sxs-lookup"><span data-stu-id="f2cd3-122">If the version is not specified, NuGet installs the latest version of the package.</span></span> <span data-ttu-id="f2cd3-123">[dotnet add package](/dotnet/core/tools/dotnet-add-package?tabs=netcore2x) 명령을 사용하여 특정 버전의 Nuget 패키지를 설치할 수도 있습니다.</span><span class="sxs-lookup"><span data-stu-id="f2cd3-123">You can also use the [dotnet add package](/dotnet/core/tools/dotnet-add-package?tabs=netcore2x) command to install a specific version of a Nuget package:</span></span>

```dotnetcli
dotnet add package <PACKAGE_NAME> -v <VERSION>
```

<span data-ttu-id="f2cd3-124">예를 들어 `Newtonsoft.Json` 패키지의 버전 12.0.1을 추가하려면 다음 명령을 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="f2cd3-124">For example, to add version 12.0.1 of the `Newtonsoft.Json` package, use this command:</span></span>

```dotnetcli
dotnet add package Newtonsoft.Json -v 12.0.1
```

## <a name="list-package-references"></a><span data-ttu-id="f2cd3-125">패키지 참조 나열</span><span class="sxs-lookup"><span data-stu-id="f2cd3-125">List package references</span></span>

<span data-ttu-id="f2cd3-126">[dotnet 목록 패키지](/dotnet/core/tools/dotnet-list-package?tabs=netcore2x) 명령을 사용하여 프로젝트의 패키지 참조를 나열할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="f2cd3-126">You can list the package references for your project using the [dotnet list package](/dotnet/core/tools/dotnet-list-package?tabs=netcore2x) command.</span></span>

```dotnetcli
dotnet list package
```

## <a name="remove-a-package"></a><span data-ttu-id="f2cd3-127">패키지 제거</span><span class="sxs-lookup"><span data-stu-id="f2cd3-127">Remove a package</span></span>

<span data-ttu-id="f2cd3-128">[dotnet remove package](/dotnet/core/tools/dotnet-remove-package?tabs=netcore2x) 명령을 사용하여 프로젝트 파일에서 패키지 참조를 제거합니다.</span><span class="sxs-lookup"><span data-stu-id="f2cd3-128">Use the [dotnet remove package](/dotnet/core/tools/dotnet-remove-package?tabs=netcore2x) command to remove a package reference from the project file.</span></span>

```dotnetcli
dotnet remove package <PACKAGE_NAME>
```

<span data-ttu-id="f2cd3-129">예를 들어 `Newtonsoft.Json` 패키지를 제거하려면 다음 명령을 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="f2cd3-129">For example, to remove the `Newtonsoft.Json` package, use the following command</span></span>

```dotnetcli
dotnet remove package Newtonsoft.Json
```

## <a name="update-a-package"></a><span data-ttu-id="f2cd3-130">패키지 업데이트</span><span class="sxs-lookup"><span data-stu-id="f2cd3-130">Update a package</span></span>

<span data-ttu-id="f2cd3-131">패키지 버전을 지정하지 않는 한 `dotnet add package` 명령을 사용할 때 NuGet은 패키지의 최신 버전을 설치합니다(`-v` 스위치).</span><span class="sxs-lookup"><span data-stu-id="f2cd3-131">NuGet installs the latest version of the package when you use the `dotnet add package` command unless you specify the package version (`-v` switch).</span></span>

## <a name="restore-packages"></a><span data-ttu-id="f2cd3-132">패키지 복원</span><span class="sxs-lookup"><span data-stu-id="f2cd3-132">Restore packages</span></span>

[!INCLUDE [restore-dotnet-cli](includes/restore-dotnet-cli.md)]
