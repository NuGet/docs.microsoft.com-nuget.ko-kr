---
title: NuGet 패키지 유형 선택
description: 패키지 유형을 설명하여 패키지의 용도를 나타냅니다.
author: karann-msft
ms.author: karann
ms.date: 07/09/2019
ms.topic: conceptual
ms.openlocfilehash: 8a3ba6af19125b75af17cab8c093e89485e20324
ms.sourcegitcommit: 0dea3b153ef823230a9d5f38351b7cef057cb299
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/12/2019
ms.locfileid: "67843495"
---
# <a name="set-a-nuget-package-type"></a><span data-ttu-id="af1d8-103">NuGet 패키지 유형 선택</span><span class="sxs-lookup"><span data-stu-id="af1d8-103">Set a NuGet package type</span></span>

<span data-ttu-id="af1d8-104">NuGet 3.5 이상을 사용하면 의도한 용도를 나타내기 위해 패키지를 특정 *패키지 유형*으로 표시할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="af1d8-104">With NuGet 3.5+, packages can be marked with a specific *package type* to indicate its intended use.</span></span> <span data-ttu-id="af1d8-105">이전 버전의 NuGet으로 만든 모든 패키지를 포함하여 유형으로 표시되지 않은 패키지의 기본값은 `Dependency` 유형입니다.</span><span class="sxs-lookup"><span data-stu-id="af1d8-105">Packages not marked with a type, including all packages created with earlier versions of NuGet, default to the `Dependency` type.</span></span>

- <span data-ttu-id="af1d8-106">`Dependency` 유형 패키지는 라이브러리 또는 애플리케이션에 빌드 시간 자산 또는 런타임 자산을 추가하며, 모든 프로젝트 형식에 설치할 수 있습니다(호환된다고 가정할 경우).</span><span class="sxs-lookup"><span data-stu-id="af1d8-106">`Dependency` type packages add build- or run-time assets to libraries and applications, and can be installed in any project type (assuming they are compatible).</span></span>

- <span data-ttu-id="af1d8-107">`DotnetCliTool` 유형 패키지는 [dotnet CLI](/dotnet/articles/core/tools/index)의 확장이며, 명령줄에서 호출됩니다.</span><span class="sxs-lookup"><span data-stu-id="af1d8-107">`DotnetCliTool` type packages are extensions to the [dotnet CLI](/dotnet/articles/core/tools/index) and are invoked from the command line.</span></span> <span data-ttu-id="af1d8-108">이러한 패키지는 .NET Core 프로젝트에만 설치할 수 있으며 복원 작업에는 영향을 주지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="af1d8-108">Such packages can be installed only in .NET Core projects and have no effect on restore operations.</span></span> <span data-ttu-id="af1d8-109">이러한 프로젝트별 확장에 대한 자세한 내용은 [.NET Core 확장성](/dotnet/articles/core/tools/extensibility#per-project-based-extensibility) 설명서를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="af1d8-109">More details about these per-project extensions are available in the  [.NET Core extensibility](/dotnet/articles/core/tools/extensibility#per-project-based-extensibility) documentation.</span></span>

- <span data-ttu-id="af1d8-110">사용자 지정 유형 패키지는 패키지 ID와 동일한 형식 규칙을 준수하는 임의 형식의 식별자를 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="af1d8-110">Custom type packages use an arbitrary type identifier that conforms to the same format rules as package IDs.</span></span> <span data-ttu-id="af1d8-111">그러나 `Dependency` 및 `DotnetCliTool` 이외의 유형은 Visual Studio의 NuGet 패키지 관리자에서 인식되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="af1d8-111">Any type other than `Dependency` and `DotnetCliTool`, however, are not recognized by the NuGet Package Manager in Visual Studio.</span></span>

<span data-ttu-id="af1d8-112">패키지 형식은 `.nuspec` 파일에 설정됩니다.</span><span class="sxs-lookup"><span data-stu-id="af1d8-112">Package types are set in the `.nuspec` file.</span></span> <span data-ttu-id="af1d8-113">이전 버전과의 호환성에서 `Dependency` 유형을 명시적으로 *설정하지 않고*, 유형을 지정하지 않은 경우 이 유형을 가정하여 NuGet을 대신 사용하는 것이 가장 좋습니다.</span><span class="sxs-lookup"><span data-stu-id="af1d8-113">It's best for backwards compatibility to *not* explicitly set the `Dependency` type and to instead rely on NuGet assuming this type when no type is specified.</span></span>

- <span data-ttu-id="af1d8-114">`.nuspec`: `<metadata>` 요소 아래의 `packageTypes\packageType` 노드 내에서 패키지 유형을 나타냅니다.</span><span class="sxs-lookup"><span data-stu-id="af1d8-114">`.nuspec`: Indicate the package type within a `packageTypes\packageType` node under the `<metadata>` element:</span></span>

    ```xml
    <?xml version="1.0" encoding="utf-8"?>
    <package xmlns="http://schemas.microsoft.com/packaging/2012/06/nuspec.xsd">
        <metadata>
        <!-- ... -->
        <packageTypes>
            <packageType name="DotnetCliTool" />
        </packageTypes>
        </metadata>
    </package>
    ```
