---
title: 새 기호 패키지 형식 '.snupkg'를 사용하여 NuGet 기호 패키지를 게시하는 방법 | Microsoft Docs
author:
- cristinamanu
- kraigb
ms.author:
- cristinamanu
- kraigb
manager: skofman
ms.date: 10/30/2018
ms.topic: reference
ms.prod: nuget
ms.technology: ''
description: NuGet 기호 패키지(snupkg)를 만드는 방법.
keywords: NuGet 기호 패키지, NuGet 패키지 디버깅, NuGet 디버깅 지원, 패키지 기호, 기호 패키지 규칙
ms.reviewer:
- anangaur
- karann
ms.openlocfilehash: 1fbb243a7b3518307a393b5f371feae1edb7623a
ms.sourcegitcommit: 5c5f0f0e1f79098e27d9566dd98371f6ee16f8b5
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 12/20/2018
ms.locfileid: "53645661"
---
# <a name="creating-symbol-packages-snupkg"></a><span data-ttu-id="e2e19-104">기호 패키지(.snupkg) 만들기</span><span class="sxs-lookup"><span data-stu-id="e2e19-104">Creating symbol packages (.snupkg)</span></span>

## <a name="prerequisites"></a><span data-ttu-id="e2e19-105">전제 조건</span><span class="sxs-lookup"><span data-stu-id="e2e19-105">Prerequisites</span></span>

<span data-ttu-id="e2e19-106">필수 [NuGet protocols](../api/nuget-protocols.md)를 구현하는 [nuget.exe v4.9.0 이상](https://www.nuget.org/downloads) 또는 [dotnet.exe v2.2.0 이상](https://www.microsoft.com/net/download/dotnet-core/2.2).</span><span class="sxs-lookup"><span data-stu-id="e2e19-106">[nuget.exe v4.9.0 or above](https://www.nuget.org/downloads) or [dotnet.exe v2.2.0 or above](https://www.microsoft.com/net/download/dotnet-core/2.2), which implement the required [NuGet protocols](../api/nuget-protocols.md).</span></span>

## <a name="creating-a-symbol-package"></a><span data-ttu-id="e2e19-107">기호 패키지 만들기</span><span class="sxs-lookup"><span data-stu-id="e2e19-107">Creating a symbol package</span></span>

<span data-ttu-id="e2e19-108">snupkg 기호 패키지는 .nuspec 파일 또는.csproj 파일에서 만들 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="e2e19-108">A snupkg symbol package can be created from a .nuspec file or from a .csproj file.</span></span> <span data-ttu-id="e2e19-109">NuGet.exe 및 dotnet.exe는 둘 다 지원됩니다.</span><span class="sxs-lookup"><span data-stu-id="e2e19-109">NuGet.exe and dotnet.exe are both supported.</span></span> <span data-ttu-id="e2e19-110">nuget.exe pack 명령에서 ```-Symbols -SymbolPackageFormat snupkg``` 옵션을 사용하면 .nupkg 파일에 .snupkg 파일이 추가로 생성됩니다.</span><span class="sxs-lookup"><span data-stu-id="e2e19-110">When the options ```-Symbols -SymbolPackageFormat snupkg``` are used on the nuget.exe pack command a .snupkg file will be created in addition to the .nupkg file.</span></span>

<span data-ttu-id="e2e19-111">.snupkg 파일을 만드는 명령 예제</span><span class="sxs-lookup"><span data-stu-id="e2e19-111">Example commands to create .snupkg files</span></span>
```
dotnet pack MyPackage.csproj --include-symbols -p:SymbolPackageFormat=snupkg

nuget pack MyPackage.nuspec -Symbols -SymbolPackageFormat snupkg

nuget pack MyPackage.csproj -Symbols -SymbolPackageFormat snupkg

msbuild -t:pack MyPackage.csproj -p:IncludeSymbols=true -p:SymbolPackageFormat=snupkg
```

<span data-ttu-id="e2e19-112">`.snupkgs`는 기본적으로 생성되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="e2e19-112">`.snupkgs` are not produced by default.</span></span> <span data-ttu-id="e2e19-113">dotnet.exe의 경우 `-Symbols`와 함께 `SymbolPackageFormat` 속성을 전달하고, dotnet.exe의 경우 `--include-symbols` 또는 msbuild의 경우 `-p:IncludeSymbols`를 전달해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="e2e19-113">You must pass the `SymbolPackageFormat` property along with `-Symbols` in case of nuget.exe, `--include-symbols` in case of dotnet.exe, or `-p:IncludeSymbols` in case of msbuild.</span></span>

<span data-ttu-id="e2e19-114">SymbolPackageFormat 속성은 `symbols.nupkg`(기본값) 또는 `snupkg`의 두 값 중 하나를 가질 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="e2e19-114">SymbolPackageFormat property can have one of the two values: `symbols.nupkg` (the default) or `snupkg`.</span></span> <span data-ttu-id="e2e19-115">SymbolPackageFormat을 지정하지 않으면 기본적으로 `symbols.nupkg`이며 레거시 기호 패키지가 생성됩니다.</span><span class="sxs-lookup"><span data-stu-id="e2e19-115">If the SymbolPackageFormat is not specified, it defaults to `symbols.nupkg` and a legacy symbol package will be created.</span></span>

> [!Note]
> <span data-ttu-id="e2e19-116">레거시 형식 `.symbols.nupkg`는 여전히 호환성 문제에서만 지원됩니다([레거시 기호 패키지](Symbol-Packages.md) 참조).</span><span class="sxs-lookup"><span data-stu-id="e2e19-116">The legacy format `.symbols.nupkg` is still supported but only for compatibility reasons (see [Legacy Symbol Packages](Symbol-Packages.md)).</span></span> <span data-ttu-id="e2e19-117">NuGet.org 기호 서버는 새 기호 패키지 형식(`.snupkg`)만 허용합니다.</span><span class="sxs-lookup"><span data-stu-id="e2e19-117">NuGet.org symbols server only accepts the new symbol package format - `.snupkg`.</span></span>

## <a name="publishing-a-symbol-package"></a><span data-ttu-id="e2e19-118">기호 패키지 게시</span><span class="sxs-lookup"><span data-stu-id="e2e19-118">Publishing a symbol package</span></span>

1. <span data-ttu-id="e2e19-119">편의상 먼저 NuGet과 함께 API 키를 저장합니다([패키지 게시](../create-packages/publish-a-package.md) 참조).</span><span class="sxs-lookup"><span data-stu-id="e2e19-119">For convenience, first save your API key with NuGet (see [publish a package](../create-packages/publish-a-package.md)).</span></span>

    ```cli
    nuget SetApiKey Your-API-Key
    ```

1. <span data-ttu-id="e2e19-120">기본 패키지를 nuget.org에 게시한 후 기호 패키지를 다음과 같이 푸시합니다.</span><span class="sxs-lookup"><span data-stu-id="e2e19-120">After publishing your primary package to nuget.org, push the symbol package as follows.</span></span>

    ```cli
    nuget push MyPackage.snupkg
    ```

1. <span data-ttu-id="e2e19-121">아래 명령을 사용하여 기본 패키지 및 기호 패키지를 동시에 푸시할 수도 있습니다.</span><span class="sxs-lookup"><span data-stu-id="e2e19-121">You can also push both primary and symbol packages at the same time using the below command.</span></span> <span data-ttu-id="e2e19-122">.nupkg 파일 및 .snupkg 파일은 모두 현재 폴더에 있어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="e2e19-122">Both .nupkg and .snupkg files need to be present in the current folder.</span></span>

    ```cli
    nuget push MyPackage.nupkg
    ```

<span data-ttu-id="e2e19-123">NuGet은 두 패키지를 nuget.org에 게시합니다. `MyPackage.nupkg`가 먼저 게시되고 `MyPackage.snupkg`가 그다음으로 게시됩니다.</span><span class="sxs-lookup"><span data-stu-id="e2e19-123">NuGet will publish both packages to nuget.org. `MyPackage.nupkg` will be published first, followed by `MyPackage.snupkg`.</span></span>

## <a name="nugetorg-symbol-server"></a><span data-ttu-id="e2e19-124">NuGet.org 기호 서버</span><span class="sxs-lookup"><span data-stu-id="e2e19-124">NuGet.org symbol server</span></span>

<span data-ttu-id="e2e19-125">NuGet.org는 자체 기호 서버 리포지토리를 지원하며 새 기호 패키지 형식(`.snupkg`)만 허용합니다.</span><span class="sxs-lookup"><span data-stu-id="e2e19-125">NuGet.org supports its own symbols server repository and only accepts the new symbol package format - `.snupkg`.</span></span> <span data-ttu-id="e2e19-126">패키지 소비자는 Visual Studio에서 해당 기호 원본에 `https://symbols.nuget.org/download/symbols`를 추가하여 nuget.org 기호 서버에 게시된 기호를 사용할 수 있습니다. 그러면 Visual Studio 디버거에서 코드 패키지를 단계적으로 실행할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="e2e19-126">Package consumers can use the symbols published to nuget.org symbol server by adding `https://symbols.nuget.org/download/symbols` to their symbol sources in Visual Studio, which allows stepping into package code in the Visual Studio debugger.</span></span> <span data-ttu-id="e2e19-127">해당 프로세스에 대한 자세한 내용은 [Visual Studio 디버거에서 기호 파일(.pdb) 및 원본 파일 지정](https://docs.microsoft.com/en-us/visualstudio/debugger/specify-symbol-dot-pdb-and-source-files-in-the-visual-studio-debugger?view=vs-2017)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="e2e19-127">See [Specify symbol (.pdb) and source files in the Visual Studio debugger](https://docs.microsoft.com/en-us/visualstudio/debugger/specify-symbol-dot-pdb-and-source-files-in-the-visual-studio-debugger?view=vs-2017) for details on that process.</span></span>

### <a name="nugetorg-symbol-package-constraints"></a><span data-ttu-id="e2e19-128">Nuget.org 기호 패키지 제약 조건</span><span class="sxs-lookup"><span data-stu-id="e2e19-128">Nuget.org symbol package constraints</span></span>

<span data-ttu-id="e2e19-129">Nuget.org에서 지원되는 기호 패키지에는 다음과 같은 제약 조건이 있습니다.</span><span class="sxs-lookup"><span data-stu-id="e2e19-129">The symbol packages supported on nuget.org have the following contraints</span></span>

- <span data-ttu-id="e2e19-130">다음 파일 확장명만 기호 패키지에 추가할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="e2e19-130">Only the following file extensions are allowed to be added to a symbol package.</span></span> ```.pdb,.nuspec,.xml,.psmdcp,.rels,.p7s```
- <span data-ttu-id="e2e19-131">관리되는 [이식 가능한 pdbs](https://github.com/dotnet/corefx/blob/master/src/System.Reflection.Metadata/specs/PortablePdb-Metadata.md)만 현재 nuget 기호 서버에서 지원됩니다.</span><span class="sxs-lookup"><span data-stu-id="e2e19-131">Only managed [Portable pdbs](https://github.com/dotnet/corefx/blob/master/src/System.Reflection.Metadata/specs/PortablePdb-Metadata.md) are currently supported on nuget symbol server.</span></span>
- <span data-ttu-id="e2e19-132">pdbs 및 관련 nupkg dlls는 Visual Studio 버전 15.9 이상의 컴파일러로 빌드해야 합니다([pdb crypto 해시](https://github.com/dotnet/roslyn/issues/24429) 참조).</span><span class="sxs-lookup"><span data-stu-id="e2e19-132">The pdbs and associated nupkg dlls need to be built with the compiler in Visual Studio version 15.9 or above (see [pdb crypto hash](https://github.com/dotnet/roslyn/issues/24429))</span></span>

<span data-ttu-id="e2e19-133">다른 파일 형식이 .snupkg에 포함된 경우 nuget.org에 게시되는 기호 패키지가 실패합니다.</span><span class="sxs-lookup"><span data-stu-id="e2e19-133">The symbol package publish on nuget.org will fail if any other file types are included in the .snupkg.</span></span>

### <a name="symbol-package-validation-and-indexing"></a><span data-ttu-id="e2e19-134">기호 패키지 유효성 검사 및 인덱싱</span><span class="sxs-lookup"><span data-stu-id="e2e19-134">Symbol package validation and indexing</span></span>

<span data-ttu-id="e2e19-135">[NuGet.org](https://www.nuget.org/)에 게시된 기호 패키지는 바이러스 검사와 같은 여러 유효성 검사를 거칩니다.</span><span class="sxs-lookup"><span data-stu-id="e2e19-135">Symbol packages published to [NuGet.org](https://www.nuget.org/) undergo several validations, such as virus checks.</span></span>

<span data-ttu-id="e2e19-136">패키지가 모든 유효성 검사를 통과하면 기호가 인덱싱되고 NuGet.org 기호 서버에서 사용할 수 있게 되는 데 시간이 걸릴 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="e2e19-136">When the package has passed all validation checks, it might take a while for the symbols to index and be available for consumption from the NuGet.org symbol servers.</span></span> <span data-ttu-id="e2e19-137">패키지가 유효성 검사에 실패하면 .nupkg의 패키지 세부 정보 페이지가 업데이트되어 관련 오류가 표시되고 이를 알리는 이메일도 받게 됩니다.</span><span class="sxs-lookup"><span data-stu-id="e2e19-137">If the package fails a validation check, the package details page for the .nupkg will update to display the associated error and you will also receive an email notifying you about it.</span></span>

<span data-ttu-id="e2e19-138">패키지 유효성 검사 및 인덱싱은 일반적으로 15분이 걸리지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="e2e19-138">Package validation and indexing usually takes under 15 minutes.</span></span> <span data-ttu-id="e2e19-139">패키지 게시가 예상보다 오래 걸리면 [status.nuget.org](https://status.nuget.org/)를 방문하여 nuget.org에 중단이 발생했는지를 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="e2e19-139">If the package publishing is taking longer than expected, visit [status.nuget.org](https://status.nuget.org/) to check if nuget.org is experiencing any interruptions.</span></span> <span data-ttu-id="e2e19-140">모든 시스템이 모두 제대로 작동하고 패키지가 한 시간 내에 성공적으로 게시되지 않은 경우 nuget.org에 로그인하여 패키지 세부 정보 페이지에서 지원 문의 링크를 사용하여 문의하세요.</span><span class="sxs-lookup"><span data-stu-id="e2e19-140">If all systems are operational and the package hasn't been successfully published within an hour, please login to nuget.org and contact us using the Contact Support link on the package details page.</span></span>

## <a name="symbol-package-structure"></a><span data-ttu-id="e2e19-141">기호 패키지 구조</span><span class="sxs-lookup"><span data-stu-id="e2e19-141">Symbol package structure</span></span>

<span data-ttu-id="e2e19-142">.Nupkg 파일은 현재와 정확히 동일하지만 .snupkg 파일은 다음과 같은 특징이 있습니다.</span><span class="sxs-lookup"><span data-stu-id="e2e19-142">The .nupkg file would be exactly the same as it is today, but the .snupkg file would have the following characteristics:</span></span>

1) <span data-ttu-id="e2e19-143">.snupkg는 해당 .nupkg와 동일한 id 및 버전을 갖습니다.</span><span class="sxs-lookup"><span data-stu-id="e2e19-143">The .snupkg will have the same id and version as the corresponding .nupkg.</span></span>
2) <span data-ttu-id="e2e19-144">.snupkg는 DLL/EXE 대신 해당 PDB가 동일한 폴더 계층 구조에 포함되도록 구분하여 모든 DLL 또는 EXE 파일의 nupkg와 정확히 동일한 폴더 구조를 가집니다.</span><span class="sxs-lookup"><span data-stu-id="e2e19-144">The .snupkg will have the exact folder structure as the nupkg for any DLL or EXE files with the distinction that instead of DLLs/EXEs, their corresponding PDBs will be included in the same folder hierarchy.</span></span> <span data-ttu-id="e2e19-145">PDB 이외의 확장명을 가진 파일 및 폴더는 snupkg에서 제외됩니다.</span><span class="sxs-lookup"><span data-stu-id="e2e19-145">Files and folders with extensions other than PDB will be left out of the snupkg.</span></span>
3) <span data-ttu-id="e2e19-146">.snupkg의 .nuspec 파일도 아래와 같이 새 PackageType을 지정합니다.</span><span class="sxs-lookup"><span data-stu-id="e2e19-146">The .nuspec file in the .snupkg will also specify a new PackageType as below.</span></span> <span data-ttu-id="e2e19-147">하나의 PackageType만 지정해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="e2e19-147">This should the only one PackageType specified.</span></span> 
``` 
<packageTypes>
  <packageType name="SymbolsPackage"/>
</packageTypes>
```
4) <span data-ttu-id="e2e19-148">작성자가 nupkg 및 snupkg를 빌드하는 데 사용자 지정 nuspec을 사용하기로 결정한 경우 snupkg는 2)에 자세히 설명된 것과 동일한 계층 구조와 파일을 가져야 합니다.</span><span class="sxs-lookup"><span data-stu-id="e2e19-148">If an author decides to use a custom nuspec to build their nupkg and snupkg, the snupkg should have the same folder hierarchy and files detailed in 2).</span></span>
5) <span data-ttu-id="e2e19-149">```authors``` 및 ```owners``` 필드는 snupkg의 nuspec에서 제외됩니다.</span><span class="sxs-lookup"><span data-stu-id="e2e19-149">```authors``` and ```owners``` field will be excluded from the snupkg's nuspec.</span></span>

## <a name="see-also"></a><span data-ttu-id="e2e19-150">참고 항목</span><span class="sxs-lookup"><span data-stu-id="e2e19-150">See Also</span></span>

[<span data-ttu-id="e2e19-151">NuGet-Package-Debugging-&-Symbols-Improvements</span><span class="sxs-lookup"><span data-stu-id="e2e19-151">NuGet-Package-Debugging-&-Symbols-Improvements</span></span>](https://github.com/NuGet/Home/wiki/NuGet-Package-Debugging-&-Symbols-Improvements)
