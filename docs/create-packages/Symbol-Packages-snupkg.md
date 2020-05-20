---
title: 새 기호 패키지 형식 '.snupkg'를 사용하여 NuGet 기호 패키지를 게시하는 방법 | Microsoft Docs
author: cristinamanu
ms.author: cristinamanu
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
ms.openlocfilehash: c42032f1869f4be0af44ffa8fbd5ad522f73c459
ms.sourcegitcommit: 2b50c450cca521681a384aa466ab666679a40213
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/07/2020
ms.locfileid: "80380420"
---
# <a name="creating-symbol-packages-snupkg"></a><span data-ttu-id="32513-104">기호 패키지(.snupkg) 만들기</span><span class="sxs-lookup"><span data-stu-id="32513-104">Creating symbol packages (.snupkg)</span></span>

<span data-ttu-id="32513-105">디버깅 환경이 제대로 작동하려면 컴파일된 코드와 소스 코드 간의 연결, 지역 변수 이름, 스택 추적 등의 중요한 정보를 제공하는 디버그 기호가 있어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="32513-105">A good debugging experience relies on the presence of debug symbols as they provide critical information like the association between the compiled and the source code, names of local variables, stack traces, and more.</span></span> <span data-ttu-id="32513-106">기호 패키지(.snupkg)를 사용하여 이러한 기호를 배포하고 NuGet 패키지의 디버깅 환경을 개선할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="32513-106">You can use symbol packages (.snupkg) to distribute these symbols and improve the debugging experience of your NuGet packages.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="32513-107">사전 요구 사항</span><span class="sxs-lookup"><span data-stu-id="32513-107">Prerequisites</span></span>

<span data-ttu-id="32513-108">필수 [NuGet 프로토콜](../api/nuget-protocols.md)을 구현하는 [nuget.exe v4.9.0 이상](https://www.nuget.org/downloads) 또는 [dotnet CLI v2.2.0 이상](https://www.microsoft.com/net/download/dotnet-core/2.2)</span><span class="sxs-lookup"><span data-stu-id="32513-108">[nuget.exe v4.9.0 or above](https://www.nuget.org/downloads) or [dotnet CLI v2.2.0 or above](https://www.microsoft.com/net/download/dotnet-core/2.2), which implement the required [NuGet protocols](../api/nuget-protocols.md).</span></span>

## <a name="creating-a-symbol-package"></a><span data-ttu-id="32513-109">기호 패키지 만들기</span><span class="sxs-lookup"><span data-stu-id="32513-109">Creating a symbol package</span></span>

<span data-ttu-id="32513-110">dotnet CLI 또는 MSBuild를 사용하는 경우 nupkg 파일 외에 .snupkg 파일을 만들도록 `IncludeSymbols` 및 `SymbolPackageFormat` 속성을 설정해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="32513-110">If you're using dotnet CLI or MSBuild, you need to set the `IncludeSymbols` and `SymbolPackageFormat` properties to create a .snupkg file in addition to the .nupkg file.</span></span>

* <span data-ttu-id="32513-111">.csproj 파일에 다음 속성을 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="32513-111">Either add the following properties to your .csproj file:</span></span>

   ```xml
   <PropertyGroup>
      <IncludeSymbols>true</IncludeSymbols>
      <SymbolPackageFormat>snupkg</SymbolPackageFormat>
   </PropertyGroup>
   ```

* <span data-ttu-id="32513-112">또는 명령줄에서 다음 속성을 지정합니다.</span><span class="sxs-lookup"><span data-stu-id="32513-112">Or specify these properties on the command-line:</span></span>

     ```dotnetcli
     dotnet pack MyPackage.csproj -p:IncludeSymbols=true -p:SymbolPackageFormat=snupkg
     ```

  <span data-ttu-id="32513-113">또는</span><span class="sxs-lookup"><span data-stu-id="32513-113">or</span></span>

  ```cli
  msbuild MyPackage.csproj /t:pack /p:IncludeSymbols=true /p:SymbolPackageFormat=snupkg
  ```

<span data-ttu-id="32513-114">NuGet.exe를 사용하는 경우 다음 명령을 사용하여 .nupkg 파일 외에도 .snupkg 파일을 만들 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="32513-114">If you're using NuGet.exe, you can use the following commands to create a .snupkg file in addition to the .nupkg file:</span></span>

```cli
nuget pack MyPackage.nuspec -Symbols -SymbolPackageFormat snupkg

nuget pack MyPackage.csproj -Symbols -SymbolPackageFormat snupkg
```

<span data-ttu-id="32513-115">[`SymbolPackageFormat`](/dotnet/core/tools/csproj#symbolpackageformat) 속성은 `symbols.nupkg`(기본값) 또는 `snupkg`의 두 값 중 하나를 가질 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="32513-115">The [`SymbolPackageFormat`](/dotnet/core/tools/csproj#symbolpackageformat) property can have one of two values: `symbols.nupkg` (the default) or `snupkg`.</span></span> <span data-ttu-id="32513-116">이 속성을 지정하지 않으면 레거시 기호 패키지가 생성됩니다.</span><span class="sxs-lookup"><span data-stu-id="32513-116">If this property is not specified, a legacy symbol package will be created.</span></span>

> [!Note]
> <span data-ttu-id="32513-117">레거시 형식 `.symbols.nupkg`는 여전히 호환성 문제에서만 지원됩니다([레거시 기호 패키지](Symbol-Packages.md) 참조).</span><span class="sxs-lookup"><span data-stu-id="32513-117">The legacy format `.symbols.nupkg` is still supported but only for compatibility reasons (see [Legacy Symbol Packages](Symbol-Packages.md)).</span></span> <span data-ttu-id="32513-118">NuGet.org의 기호 서버는 새 기호 패키지 형식(`.snupkg`)만 허용합니다.</span><span class="sxs-lookup"><span data-stu-id="32513-118">NuGet.org's symbol server only accepts the new symbol package format - `.snupkg`.</span></span>

## <a name="publishing-a-symbol-package"></a><span data-ttu-id="32513-119">기호 패키지 게시</span><span class="sxs-lookup"><span data-stu-id="32513-119">Publishing a symbol package</span></span>

1. <span data-ttu-id="32513-120">편의상 먼저 NuGet과 함께 API 키를 저장합니다([패키지 게시](../nuget-org/publish-a-package.md) 참조).</span><span class="sxs-lookup"><span data-stu-id="32513-120">For convenience, first save your API key with NuGet (see [publish a package](../nuget-org/publish-a-package.md)).</span></span>

    ```cli
    nuget SetApiKey Your-API-Key
    ```

1. <span data-ttu-id="32513-121">기본 패키지를 nuget.org에 게시한 후 기호 패키지를 다음과 같이 푸시합니다.</span><span class="sxs-lookup"><span data-stu-id="32513-121">After publishing your primary package to nuget.org, push the symbol package as follows.</span></span>

    ```cli
    nuget push MyPackage.snupkg
    ```

1. <span data-ttu-id="32513-122">아래 명령을 사용하여 기본 패키지 및 기호 패키지를 동시에 푸시할 수도 있습니다.</span><span class="sxs-lookup"><span data-stu-id="32513-122">You can also push both primary and symbol packages at the same time using the below command.</span></span> <span data-ttu-id="32513-123">.nupkg 파일 및 .snupkg 파일은 모두 현재 폴더에 있어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="32513-123">Both .nupkg and .snupkg files need to be present in the current folder.</span></span>

    ```cli
    nuget push MyPackage.nupkg
    ```

<span data-ttu-id="32513-124">NuGet은 두 패키지를 nuget.org에 게시합니다. `MyPackage.nupkg`가 먼저 게시되고 `MyPackage.snupkg`가 그다음으로 게시됩니다.</span><span class="sxs-lookup"><span data-stu-id="32513-124">NuGet will publish both packages to nuget.org. `MyPackage.nupkg` will be published first, followed by `MyPackage.snupkg`.</span></span>

> [!Note]
> <span data-ttu-id="32513-125">기호 패키지가 게시되지 않은 경우 NuGet.org 소스를 `https://api.nuget.org/v3/index.json`(으)로 구성했는지 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="32513-125">If the symbol package isn't published, check that you've configured the NuGet.org source as `https://api.nuget.org/v3/index.json`.</span></span> <span data-ttu-id="32513-126">기호 패키지 게시는 [NuGet V3 API](../api/overview.md#versioning)에서만 지원됩니다.</span><span class="sxs-lookup"><span data-stu-id="32513-126">Symbol package publishing is only supported by [the NuGet V3 API](../api/overview.md#versioning).</span></span>

## <a name="nugetorg-symbol-server"></a><span data-ttu-id="32513-127">NuGet.org 기호 서버</span><span class="sxs-lookup"><span data-stu-id="32513-127">NuGet.org symbol server</span></span>

<span data-ttu-id="32513-128">NuGet.org는 자체 기호 서버 리포지토리를 지원하며 새 기호 패키지 형식(`.snupkg`)만 허용합니다.</span><span class="sxs-lookup"><span data-stu-id="32513-128">NuGet.org supports its own symbols server repository and only accepts the new symbol package format - `.snupkg`.</span></span> <span data-ttu-id="32513-129">패키지 소비자는 Visual Studio에서 해당 기호 원본에 `https://symbols.nuget.org/download/symbols`를 추가하여 nuget.org 기호 서버에 게시된 기호를 사용할 수 있습니다. 그러면 Visual Studio 디버거에서 코드 패키지를 단계적으로 실행할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="32513-129">Package consumers can use the symbols published to nuget.org symbol server by adding `https://symbols.nuget.org/download/symbols` to their symbol sources in Visual Studio, which allows stepping into package code in the Visual Studio debugger.</span></span> <span data-ttu-id="32513-130">해당 프로세스에 대한 자세한 내용은 [Visual Studio 디버거에서 기호 파일(.pdb) 및 원본 파일 지정](/visualstudio/debugger/specify-symbol-dot-pdb-and-source-files-in-the-visual-studio-debugger)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="32513-130">See [Specify symbol (.pdb) and source files in the Visual Studio debugger](/visualstudio/debugger/specify-symbol-dot-pdb-and-source-files-in-the-visual-studio-debugger) for details on that process.</span></span>

### <a name="nugetorg-symbol-package-constraints"></a><span data-ttu-id="32513-131">NuGet.org 기호 패키지 제약 조건</span><span class="sxs-lookup"><span data-stu-id="32513-131">NuGet.org symbol package constraints</span></span>

<span data-ttu-id="32513-132">NuGet.org에는 기호 패키지에 대한 다음과 같은 제약 조건이 있습니다.</span><span class="sxs-lookup"><span data-stu-id="32513-132">NuGet.org has the following constraints for symbol packages:</span></span>

- <span data-ttu-id="32513-133">기호 패키지에는 `.pdb`, `.nuspec`, `.xml`, `.psmdcp`, `.rels`, `.p7s`와 같은 파일 확장명만 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="32513-133">Only the following file extensions are allowed in symbol packages: `.pdb`, `.nuspec`, `.xml`, `.psmdcp`, `.rels`, `.p7s`</span></span>
- <span data-ttu-id="32513-134">관리형 [이동식 PDB](https://github.com/dotnet/runtime/blob/87572a799bfd37779c079faf28544e3f9a16be58/src/libraries/System.Reflection.Metadata/specs/PortablePdb-Metadata.md)만 NuGet.org의 기호 서버에서 지원됩니다.</span><span class="sxs-lookup"><span data-stu-id="32513-134">Only managed [Portable PDBs](https://github.com/dotnet/runtime/blob/87572a799bfd37779c079faf28544e3f9a16be58/src/libraries/System.Reflection.Metadata/specs/PortablePdb-Metadata.md) are supported on NuGet.org's symbol server.</span></span>
- <span data-ttu-id="32513-135">PDB 및 관련 .nupkg DLL은 Visual Studio 버전 15.9 이상의 컴파일러로 빌드해야 합니다([PDB crypto 해시](https://github.com/dotnet/roslyn/issues/24429) 참조).</span><span class="sxs-lookup"><span data-stu-id="32513-135">The PDBs and their associated .nupkg DLLs need to be built with the compiler in Visual Studio version 15.9 or above (see [PDB crypto hash](https://github.com/dotnet/roslyn/issues/24429))</span></span>

<span data-ttu-id="32513-136">이러한 제약 조건이 충족되지 않으면 NuGet.org에 게시된 기호 패키지가 유효성 검사에 실패합니다.</span><span class="sxs-lookup"><span data-stu-id="32513-136">Symbol packages published to NuGet.org will fail validation if these constraints aren't met.</span></span> 

### <a name="symbol-package-validation-and-indexing"></a><span data-ttu-id="32513-137">기호 패키지 유효성 검사 및 인덱싱</span><span class="sxs-lookup"><span data-stu-id="32513-137">Symbol package validation and indexing</span></span>

<span data-ttu-id="32513-138">[NuGet.org](https://www.nuget.org/)에 게시된 기호 패키지는 맬웨어 검색을 포함한 여러 유효성 검사를 거칩니다.</span><span class="sxs-lookup"><span data-stu-id="32513-138">Symbol packages published to [NuGet.org](https://www.nuget.org/) undergo several validations, including malware scanning.</span></span> <span data-ttu-id="32513-139">패키지가 유효성 검사에 실패하면 패키지 세부 정보 페이지에 오류 메시지가 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="32513-139">If a package fails a validation check, its package details page will display an error message.</span></span> <span data-ttu-id="32513-140">또한 패키지 소유자는 식별된 문제를 해결하는 방법에 대한 지침이 포함된 전자 메일을 받게 됩니다.</span><span class="sxs-lookup"><span data-stu-id="32513-140">In addition, the package's owners will receive an email with instructions on how to fix the identified issues.</span></span>

<span data-ttu-id="32513-141">기호 패키지가 모든 유효성 검사를 통과하면 기호는 NuGet.org의 기호 서버에 의해 인덱싱되어 사용할 수 있게 됩니다.</span><span class="sxs-lookup"><span data-stu-id="32513-141">When the symbol package has passed all validations, the symbols will be indexed by NuGet.org's symbol servers and will be available for consumption.</span></span>

<span data-ttu-id="32513-142">패키지 유효성 검사 및 인덱싱은 일반적으로 15분이 걸리지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="32513-142">Package validation and indexing usually takes under 15 minutes.</span></span> <span data-ttu-id="32513-143">패키지 게시가 예상보다 오래 걸리면 [status.nuget.org](https://status.nuget.org/)를 방문하여 NuGet.org에 중단이 발생했는지를 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="32513-143">If the package publishing takes longer than expected, visit [status.nuget.org](https://status.nuget.org/) to check if NuGet.org is experiencing any interruptions.</span></span> <span data-ttu-id="32513-144">모든 시스템이 모두 제대로 작동하고 패키지가 한 시간 내에 성공적으로 게시되지 않은 경우 nuget.org에 로그인하여 패키지 세부 정보 페이지에서 지원 문의 링크를 사용하여 문의하세요.</span><span class="sxs-lookup"><span data-stu-id="32513-144">If all systems are operational and the package hasn't been successfully published within an hour, please login to nuget.org and contact us using the Contact Support link on the package details page.</span></span>

## <a name="symbol-package-structure"></a><span data-ttu-id="32513-145">기호 패키지 구조</span><span class="sxs-lookup"><span data-stu-id="32513-145">Symbol package structure</span></span>

<span data-ttu-id="32513-146">기호 패키지(. snupkg)의 특징은 다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="32513-146">The symbol package (.snupkg) has the following characteristics:</span></span>

1) <span data-ttu-id="32513-147">.snupkg는 해당 NuGet 패키지(.nupkg)와 동일한 ID 및 버전을 갖습니다.</span><span class="sxs-lookup"><span data-stu-id="32513-147">The .snupkg has the same id and version as its corresponding NuGet package (.nupkg).</span></span>
2) <span data-ttu-id="32513-148">.snupkg는 DLL/EXE 대신 해당 PDB가 동일한 폴더 계층 구조에 포함되도록 구분하여 모든 DLL 또는 EXE 파일의 해당 nupkg와 정확히 동일한 폴더 구조를 가집니다.</span><span class="sxs-lookup"><span data-stu-id="32513-148">The .snupkg has the same folder structure as its corresponding .nupkg for any DLL or EXE files with the distinction that instead of DLLs/EXEs, their corresponding PDBs will be included in the same folder hierarchy.</span></span> <span data-ttu-id="32513-149">PDB 이외의 확장명을 가진 파일 및 폴더는 snupkg에서 제외됩니다.</span><span class="sxs-lookup"><span data-stu-id="32513-149">Files and folders with extensions other than PDB will be left out of the snupkg.</span></span>
3) <span data-ttu-id="32513-150">기호 패키지의 .nuspec 파일은 `SymbolsPackage` 패키지 유형입니다.</span><span class="sxs-lookup"><span data-stu-id="32513-150">The symbol package's .nuspec file has the `SymbolsPackage` package type:</span></span>

   ```xml
   <packageTypes>
      <packageType name="SymbolsPackage"/>
   </packageTypes>
   ```

4) <span data-ttu-id="32513-151">작성자가 nupkg 및 snupkg를 빌드하는 데 사용자 지정 nuspec을 사용하기로 결정한 경우 snupkg는 2)에 자세히 설명된 것과 동일한 계층 구조와 파일을 가져야 합니다.</span><span class="sxs-lookup"><span data-stu-id="32513-151">If an author decides to use a custom nuspec to build their nupkg and snupkg, the snupkg should have the same folder hierarchy and files detailed in 2).</span></span>
5) <span data-ttu-id="32513-152">```authors```, ```owners```, ```requireLicenseAcceptance```, ```license type```, ```licenseUrl``` 및 ```icon``` 필드는 snupkg의 nuspec에서 제외됩니다.</span><span class="sxs-lookup"><span data-stu-id="32513-152">The following fields will be excluded from the snupkg's nuspec: ```authors```, ```owners```, ```requireLicenseAcceptance```, ```license type```, ```licenseUrl```, and  ```icon```.</span></span>
6) <span data-ttu-id="32513-153">```<license>``` 요소를 사용하지 마세요.</span><span class="sxs-lookup"><span data-stu-id="32513-153">Do not use the ```<license>``` element.</span></span> <span data-ttu-id="32513-154">.snupkg에는 해당 .nupkg와 동일한 라이선스가 적용됩니다.</span><span class="sxs-lookup"><span data-stu-id="32513-154">A .snupkg is covered under the same license as the corresponding .nupkg.</span></span>

## <a name="see-also"></a><span data-ttu-id="32513-155">참고 항목</span><span class="sxs-lookup"><span data-stu-id="32513-155">See also</span></span>

<span data-ttu-id="32513-156">소스 링크를 사용하여 .NET 어셈블리의 소스 코드 디버깅을 사용하도록 설정하는 것이 좋습니다.</span><span class="sxs-lookup"><span data-stu-id="32513-156">Consider using Source Link to enable source code debugging of .NET assemblies.</span></span> <span data-ttu-id="32513-157">자세한 내용은 [소스 링크 지침](/dotnet/standard/library-guidance/sourcelink)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="32513-157">For more information, please refer to the [Source Link guidance](/dotnet/standard/library-guidance/sourcelink).</span></span>

<span data-ttu-id="32513-158">기호 패키지에 대한 자세한 내용은 [NuGet 패키지 디버깅 & 기호 향상](https://github.com/NuGet/Home/wiki/NuGet-Package-Debugging-&-Symbols-Improvements) 디자인 사양을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="32513-158">For more information on symbol packages, please refer to the [NuGet Package Debugging & Symbols Improvements](https://github.com/NuGet/Home/wiki/NuGet-Package-Debugging-&-Symbols-Improvements) design spec.</span></span>
