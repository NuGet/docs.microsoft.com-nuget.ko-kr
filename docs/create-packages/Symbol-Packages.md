---
title: NuGet 기호 패키지를 만드는 방법
description: 기호를 포함하는 NuGet 패키지를 만들어서 Visual Studio에서 다른 NuGet 패키지의 디버깅을 지원하는 방법입니다.
author: karann-msft
ms.author: karann
ms.date: 09/12/2017
ms.topic: conceptual
ms.reviewer: anangaur
ms.openlocfilehash: ad1cf08437b4802d981f8c1a96ab9dc75425a2f0
ms.sourcegitcommit: 1d1406764c6af5fb7801d462e0c4afc9092fa569
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 09/04/2018
ms.locfileid: "43550617"
---
# <a name="creating-symbol-packages"></a><span data-ttu-id="84766-103">기호 패키지 만들기</span><span class="sxs-lookup"><span data-stu-id="84766-103">Creating symbol packages</span></span>

<span data-ttu-id="84766-104">NuGet에서는 nuget.org 또는 기타 소스에 대한 패키지를 빌드하는 것 외에도 연관된 기호 패키지를 만들고 SymbolSource 리포지토리에 게시하도록 지원합니다.</span><span class="sxs-lookup"><span data-stu-id="84766-104">In addition to building packages for nuget.org or other sources, NuGet also supports creating associated symbol packages and publishing them to the SymbolSource repository.</span></span>

<span data-ttu-id="84766-105">패키지 소비자는 Visual Studio에서 해당 기호 원본에 `https://nuget.smbsrc.net`을 추가할 수 있습니다. 그러면 Visual Studio 디버거에서 코드 패키지를 한 단계씩 실행할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="84766-105">Package consumers can then add `https://nuget.smbsrc.net` to their symbol sources in Visual Studio, which allows stepping into package code in the Visual Studio debugger.</span></span> <span data-ttu-id="84766-106">해당 프로세스에 대한 자세한 내용은 [Visual Studio 디버거에서 기호 파일(.pdb) 및 원본 파일 지정](/visualstudio/debugger/specify-symbol-dot-pdb-and-source-files-in-the-visual-studio-debugger)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="84766-106">See [Specify symbol (.pdb) and source files in the Visual Studio debugger](/visualstudio/debugger/specify-symbol-dot-pdb-and-source-files-in-the-visual-studio-debugger) for details on that process.</span></span>

## <a name="creating-a-symbol-package"></a><span data-ttu-id="84766-107">기호 패키지 만들기</span><span class="sxs-lookup"><span data-stu-id="84766-107">Creating a symbol package</span></span>

<span data-ttu-id="84766-108">기호 패키지를 만들려면 다음과 같은 규칙을 따릅니다.</span><span class="sxs-lookup"><span data-stu-id="84766-108">To create a symbol package, follow these conventions:</span></span>

- <span data-ttu-id="84766-109">기본 패키지(코드 포함)의 이름을 `{identifier}.nupkg`로 지정하고 `.pdb` 파일을 제외한 모든 파일을 포함합니다.</span><span class="sxs-lookup"><span data-stu-id="84766-109">Name the primary package (with your code) `{identifier}.nupkg` and include all your files except `.pdb` files.</span></span>
- <span data-ttu-id="84766-110">기호 패키지 이름을 `{identifier}.symbols.nupkg`로 지정하고 어셈블리 DLL, `.pdb` 파일, XMLDOC 파일, 원본 파일을 포함합니다(다음 섹션 참조).</span><span class="sxs-lookup"><span data-stu-id="84766-110">Name the symbol package `{identifier}.symbols.nupkg` and include your assembly DLL, `.pdb` files, XMLDOC files, source files (see the sections that follow).</span></span>

<span data-ttu-id="84766-111">`-Symbols` 옵션을 사용하여 `.nuspec` 파일 또는 프로젝트 파일에서 두 패키지를 만들 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="84766-111">You can create both packages with the `-Symbols` option, either from a `.nuspec` file or a project file:</span></span>

```cli
nuget pack MyPackage.nuspec -Symbols

nuget pack MyProject.csproj -Symbols
```

<span data-ttu-id="84766-112">`pack`에는 Mac OS X에서 Mono 4.4.2가 필요하며, Linux 시스템에서는 작동하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="84766-112">Note that `pack` requires Mono 4.4.2 on Mac OS X and does not work on Linux systems.</span></span> <span data-ttu-id="84766-113">또한 Mac에서는 `.nuspec` 파일의 Windows 경로 이름을 Unix 스타일 경로로 변환해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="84766-113">On a Mac, you must also convert Windows pathnames in the `.nuspec` file to Unix-style paths.</span></span>

## <a name="symbol-package-structure"></a><span data-ttu-id="84766-114">기호 패키지 구조</span><span class="sxs-lookup"><span data-stu-id="84766-114">Symbol package structure</span></span>

<span data-ttu-id="84766-115">기호 패키지는 라이브러리 패키지가 수행하는 것과 동일한 방식으로 여러 대상 프레임워크를 대상으로 지정할 수 있으므로 `lib` 폴더의 구조는 DLL과 함께 `.pdb` 파일을 비롯한 기본 패키지와 정확히 동일해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="84766-115">A symbol package can target multiple target frameworks in the same way that a library package does, so the structure of the `lib` folder should be exactly the same as the primary package, only including `.pdb` files alongside the DLL.</span></span>

<span data-ttu-id="84766-116">예를 들어, .NET 4.0 및 Silverlight 4를 대상으로 하는 기호 패키지의 레이아웃은 다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="84766-116">For example, a symbol package that targets .NET 4.0 and Silverlight 4 would have this layout:</span></span>

    \lib
        \net40
            \MyAssembly.dll
            \MyAssembly.pdb
        \sl40
            \MyAssembly.dll
            \MyAssembly.pdb

<span data-ttu-id="84766-117">그런 다음 소스 파일은 `src`라는 별도 특수 폴더에 저장됩니다. 이 항목은 소스 리포지토리의 상대 구조에 따라야 합니다.</span><span class="sxs-lookup"><span data-stu-id="84766-117">Source files are then placed in a separate special folder named `src`, which must follow the relative structure of your source repository.</span></span> <span data-ttu-id="84766-118">PDB에는 일치하는 DLL을 컴파일하는 데 사용되는 소스 파일에 대한 절대 경로가 포함되기 때문이며, 게시 프로세스 중에 찾을 수 있어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="84766-118">This is because PDBs contain absolute paths to source files used to compile the matching DLL, and they need to be found during the publishing process.</span></span> <span data-ttu-id="84766-119">기본 경로(공통 경로 접두사)가 제거될 수 있습니다. 예를 들어 이러한 파일에서 빌드된 라이브러리를 고려하세요.</span><span class="sxs-lookup"><span data-stu-id="84766-119">A base path (common path prefix) can be stripped out. For example, consider a library built from these files:</span></span>

    C:\Projects
        \MyProject
            \Common
                \MyClass.cs
            \Full
                \Properties
                    \AssemblyInfo.cs
                \MyAssembly.csproj (producing \lib\net40\MyAssembly.dll)
            \Silverlight
                \Properties
                    \AssemblyInfo.cs
                \MySilverlightExtensions.cs
                \MyAssembly.csproj (producing \lib\sl4\MyAssembly.dll)

<span data-ttu-id="84766-120">`lib` 폴더와 별개로 기호 패키지에 이 레이아웃이 포함되어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="84766-120">Apart from the `lib` folder, a symbol package would need to contain this layout:</span></span>

    \src
        \Common
            \MyClass.cs
        \Full
            \Properties
                \AssemblyInfo.cs
        \Silverlight
            \Properties
                \AssemblyInfo.cs
            \MySilverlightExtensions.cs

## <a name="referring-to-files-in-the-nuspec"></a><span data-ttu-id="84766-121">nuspec에서 파일 참조</span><span class="sxs-lookup"><span data-stu-id="84766-121">Referring to files in the nuspec</span></span>

<span data-ttu-id="84766-122">이전 섹션에 설명된 대로 폴더 구조에서 규칙에 의해 또는 매니페스트의 `files` 섹션에서 해당 내용을 지정하여 기호 패키지를 빌드할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="84766-122">A symbol package can be built by conventions, from a folder structure as described in the previous section, or by specifying its contents in the `files` section of the manifest.</span></span> <span data-ttu-id="84766-123">예를 들어 이전 섹션에 표시된 패키지를 빌드하려면 `.nuspec` 파일에서 다음을 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="84766-123">For example, to build the package shown in the previous section, use the following in the `.nuspec` file:</span></span>

```xml
<files>
    <file src="Full\bin\Debug\*.dll" target="lib\net40" />
    <file src="Full\bin\Debug\*.pdb" target="lib\net40" />
    <file src="Silverlight\bin\Debug\*.dll" target="lib\sl40" />
    <file src="Silverlight\bin\Debug\*.pdb" target="lib\sl40" />
    <file src="**\*.cs" target="src" />
</files>
```

## <a name="publishing-a-symbol-package"></a><span data-ttu-id="84766-124">기호 패키지 게시</span><span class="sxs-lookup"><span data-stu-id="84766-124">Publishing a symbol package</span></span>

> [!Important]
> <span data-ttu-id="84766-125">nuget.org에 패키지를 푸시하려면 [nuget.exe v4.1.0 이상](https://www.nuget.org/downloads)을 사용해야 합니다. 여기서는 필수 [NuGet 프로토콜](../api/nuget-protocols.md)을 구현합니다.</span><span class="sxs-lookup"><span data-stu-id="84766-125">To push packages to nuget.org you must use [nuget.exe v4.1.0 or above](https://www.nuget.org/downloads), which implements the required [NuGet protocols](../api/nuget-protocols.md).</span></span>

1. <span data-ttu-id="84766-126">편의상 먼저 NuGet이 포함된 API 키를 저장합니다([패키지 게시](../create-packages/publish-a-package.md) 참조). 그러면 사용자가 패키지 소유자인지 확인하기 위해 symbolsource.org는 nuget.org를 사용하여 확인하기 때문에 nuget.org 및 symbolsource.org 모두에 적용됩니다.</span><span class="sxs-lookup"><span data-stu-id="84766-126">For convenience, first save your API key with NuGet (see [publish a package](../create-packages/publish-a-package.md), which will apply to both nuget.org and symbolsource.org, because symbolsource.org will check with nuget.org to verify that you are the package owner.</span></span>

    ```cli
    nuget SetApiKey Your-API-Key
    ```

2. <span data-ttu-id="84766-127">nuget.org에 기본 패키지를 게시한 후에 기호 패키지를 다음과 같이 푸시합니다. 그러면 파일 이름의 `.symbols` 때문에 자동으로 symbolsource.org를 대상으로 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="84766-127">After publishing your primary package to nuget.org, push the symbol package as follows, which will automatically use symbolsource.org as the target because of the `.symbols` in the filename:</span></span>

    ```cli
    nuget push MyPackage.symbols.nupkg
    ```

3. <span data-ttu-id="84766-128">다른 기호 리포지토리에 게시하거나 명명 규칙을 따르지 않는 기호 패키지를 푸시하려면 `-Source` 옵션을 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="84766-128">To publish to a different symbol repository, or to push a symbol package that doesn't follow the naming convention, use the `-Source` option:</span></span>

    ```cli
    nuget push MyPackage.symbols.nupkg -source https://nuget.smbsrc.net/
    ```

4. <span data-ttu-id="84766-129">동시에 다음을 사용하여 기본 패키지 및 기호 패키지를 두 리포지토리에 푸시할 수도 있습니다.</span><span class="sxs-lookup"><span data-stu-id="84766-129">You can also push both primary and symbol packages to both repositories at the same time using the following:</span></span>

    ```cli
    nuget push MyPackage.nupkg
    ```

   > [!Note]
   > <span data-ttu-id="84766-130">nuget.exe 4.5.0 이상에서 기호 패키지는 symbolsource.org로 자동으로 푸시되지 않습니다. 다음 단계에 설명된 대로 별도로 기호 패키지를 푸시해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="84766-130">With nuget.exe 4.5.0 or above, the symbols packages are not automatically pushed to symbolsource.org. You would need to push the symbols packages separately as explained in the next step.</span></span>
   
<span data-ttu-id="84766-131">이 경우에 NuGet은 nuget.org에 기본 패키지를 게시한 후에 `MyPackage.symbols.nupkg`가 있으면 해당 항목을 https://nuget.smbsrc.net/ (symbolsource.org의 푸시 URL)에 게시합니다.</span><span class="sxs-lookup"><span data-stu-id="84766-131">In this case, NuGet will publish `MyPackage.symbols.nupkg`, if present, to https://nuget.smbsrc.net/ (the push URL for symbolsource.org), after it publishes the primary package to nuget.org.</span></span>

## <a name="see-also"></a><span data-ttu-id="84766-132">참고 항목</span><span class="sxs-lookup"><span data-stu-id="84766-132">See Also</span></span>

<span data-ttu-id="84766-133">[새 SymbolSource 엔진(symbolsource.org)으로 이동](https://tripleemcoder.com/2015/10/04/moving-to-the-new-symbolsource-engine/)</span><span class="sxs-lookup"><span data-stu-id="84766-133">[Moving to the new SymbolSource engine](https://tripleemcoder.com/2015/10/04/moving-to-the-new-symbolsource-engine/) (symbolsource.org)</span></span>
