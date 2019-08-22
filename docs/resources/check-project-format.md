---
title: 프로젝트 형식 식별
description: 프로젝트 형식을 식별하는 방법을 설명합니다.
author: mikejo5000
ms.author: mikejo
ms.date: 07/09/2019
ms.topic: conceptual
ms.openlocfilehash: b151547e40e567b38acc2b0b9ee84c50d85000c9
ms.sourcegitcommit: 7441f12f06ca380feb87c6192ec69f6108f43ee3
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/15/2019
ms.locfileid: "69488489"
---
# <a name="identify-the-project-format"></a>프로젝트 형식 식별

NuGet은 모든 .NET 프로젝트에서 작동합니다. 그러나 프로젝트 형식(SDK 스타일 또는 비 SDK 스타일)은 NuGet 패키지를 소비 및 만드는 데 사용해야 하는 일부 도구 및 메서드를 결정합니다. Sdk 스타일 프로젝트는 [SDK 특성](/dotnet/core/tools/csproj#additions)을 사용합니다. NuGet 패키지를 소비 및 만드는 데 사용하는 메서드 및 도구는 프로젝트 형식에 따라 달라지므로 프로젝트 형식을 식별하는 것이 중요합니다. 비 SDK 스타일 프로젝트의 경우에는 이러한 메서드 및 도구가 프로젝트를 `PackageReference` 형식으로 마이그레이션했는지 여부에 따라서도 달라집니다.

프로젝트가 SDK 스타일인지 여부는 프로젝트를 만드는 데 사용되는 메서드에 따라 달라집니다. 다음 표에서는 Visual Studio 2017 이상 버전을 사용하여 프로젝트를 만들 때 프로젝트의 기본 프로젝트 형식 및 관련 CLI 도구를 보여 줍니다.

| 프로젝트&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; | 기본 프로젝트 형식 | CLI 도구&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; | 참고 사항 |
|:------------- |:-------------|:-----|:-----|
| .NET Standard | SDK 스타일 | [dotnet CLI](../install-nuget-client-tools.md#dotnetexe-cli) | Visual Studio 2017 이전 버전으로 만든 프로젝트는 SDK 스타일이 아닙니다. `nuget.exe` CLI를 사용합니다. |
| .NET Core | SDK 스타일 | [dotnet CLI](../install-nuget-client-tools.md#dotnetexe-cli) | Visual Studio 2017 이전 버전으로 만든 프로젝트는 SDK 스타일이 아닙니다. `nuget.exe` CLI를 사용합니다. |
| .NET Framework | 비 SDK 스타일 | [nuget.exe CLI](../install-nuget-client-tools.md#nugetexe-cli) | 다른 메서드를 사용하여 만든 .NET Framework 프로젝트는 SDK 스타일 프로젝트일 수 있습니다. 이러한 경우 [dotnet CLI](../install-nuget-client-tools.md#dotnetexe-cli)를 대신 사용합니다. |
| [마이그레이션된](../consume-packages/migrate-packages-config-to-package-reference.md) .NET 프로젝트 | 비 SDK 스타일| 패키지를 만들려면 [msbuild -t:pack](../consume-packages/migrate-packages-config-to-package-reference.md#create-a-package-after-migration)을 사용하여 패키지를 만듭니다. | 패키지를 만들려면 `msbuild -t:pack`이 권장됩니다. 그렇지 않은 경우 [dotnet CLI](../install-nuget-client-tools.md#dotnetexe-cli)를 사용합니다. 마이그레이션된 프로젝트는 SDK 스타일 프로젝트가 아닙니다. |

## <a name="check-the-project-format"></a>프로젝트 형식 확인

프로젝트가 SDK 스타일 형식인지 확실하지 않은 경우 프로젝트 파일의 `<Project>` 요소에서 SDK 특성을 찾습니다(C#의 경우 *.csproj 파일). 이 특성이 있으면 프로젝트가 SDK 스타일 프로젝트입니다.

```xml
<Project Sdk="Microsoft.NET.Sdk">

  <PropertyGroup>
    <TargetFramework>netstandard2.0</TargetFramework>
    <Authors>authorname</Authors>
    <PackageId>mypackageid</PackageId>
    <Company>mycompanyname</Company>
  </PropertyGroup>

</Project>
```

## <a name="check-the-project-format-in-visual-studio"></a>Visual Studio에서 프로젝트 형식 확인

Visual Studio에서 작업하는 경우 다음 방법 중 하나를 사용하여 프로젝트 형식을 빠르게 확인할 수 있습니다.

- 솔루션 탐색기에서 프로젝트를 마우스 오른쪽 단추로 클릭하고 **myprojectname.csproj 편집**을 선택합니다.

   이 옵션은 SDK 스타일 특성을 사용하는 프로젝트의 경우 Visual Studio 2017부터만 사용할 수 있습니다. 그렇지 않으면 다른 메서드를 사용합니다.

   ![프로젝트 파일 편집](media/edit-project-file.png)

   Sdk 스타일 프로젝트는 프로젝트 파일에 [SDK 특성](/dotnet/core/tools/csproj#additions)을 표시합니다.
   
- **프로젝트** 메뉴에서 **프로젝트 언로드**를 선택하거나 프로젝트를 마우스 오른쪽 단추로 클릭하고 **프로젝트 언로드**를 선택합니다.

   이 프로젝트의 경우 프로젝트 파일에 SDK 특성이 포함되지 않습니다. SDK 스타일 프로젝트가 아닙니다.

   ![프로젝트 언로드](media/unload-project.png)

   그런 다음, 언로드된 프로젝트를 마우스 오른쪽 단추로 클릭하고 **myprojectname.csproj 편집**을 선택합니다.

## <a name="see-also"></a>참고 항목

- [dotnet CLI를 사용하여 .NET Standard 패키지 만들기](../quickstart/create-and-publish-a-package-using-the-dotnet-cli.md)
- [Visual Studio를 사용하여 .NET Standard 패키지 만들기](../quickstart/create-and-publish-a-package-using-visual-studio.md)
- [.NET Framework 패키지 만들기 및 게시(Visual Studio)](../quickstart/create-and-publish-a-package-using-visual-studio-net-framework.md)
- [MSBuild 대상으로서의 NuGet pack 및 restore](../reference/msbuild-targets.md)
