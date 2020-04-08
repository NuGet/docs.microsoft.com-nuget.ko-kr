---
title: NuGet 패키지 유형 선택
description: 패키지 유형을 설명하여 패키지의 용도를 나타냅니다.
author: karann-msft
ms.author: karann
ms.date: 07/09/2019
ms.topic: conceptual
ms.openlocfilehash: 1d869f616ce0291cf1c0a17b7ff20fc61e6a3bd5
ms.sourcegitcommit: 2b50c450cca521681a384aa466ab666679a40213
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/07/2020
ms.locfileid: "78230826"
---
# <a name="set-a-nuget-package-type"></a>NuGet 패키지 유형 선택

NuGet 3.5 이상을 사용하면 의도한 용도를 나타내기 위해 패키지를 특정 *패키지 유형*으로 표시할 수 있습니다. 이전 버전의 NuGet으로 만든 모든 패키지를 포함하여 유형으로 표시되지 않은 패키지의 기본값은 `Dependency` 유형입니다.

- `Dependency` 유형 패키지는 라이브러리 또는 애플리케이션에 빌드 시간 자산 또는 런타임 자산을 추가하며, 모든 프로젝트 형식에 설치할 수 있습니다(호환된다고 가정할 경우).

- `DotnetTool` 유형 패키지는 [dotnet CLI](/dotnet/articles/core/tools/index)의 확장이며, 명령줄에서 호출됩니다. 이러한 패키지는 .NET Core 프로젝트에만 설치할 수 있으며 복원 작업에는 영향을 주지 않습니다. 이러한 프로젝트별 확장에 대한 자세한 내용은 [.NET Core 확장성](/dotnet/articles/core/tools/extensibility#per-project-based-extensibility) 설명서를 참조하세요.

- `Template` 유형 패키지에서는 앱, 서비스, 도구 또는 클래스 라이브러리와 같은 파일 또는 프로젝트를 만드는 데 사용할 수 있는 [사용자 지정 템플릿](/dotnet/core/tools/custom-templates)을 제공합니다.

- 사용자 지정 유형 패키지는 패키지 ID와 동일한 형식 규칙을 준수하는 임의 형식의 식별자를 사용합니다. 그러나 `Dependency` 및 `DotnetTool` 이외의 유형은 Visual Studio의 NuGet 패키지 관리자에서 인식되지 않습니다.

패키지 형식은 `.nuspec` 파일에 설정됩니다. 이전 버전과의 호환성에서 *유형을 명시적으로*설정하지 않고`Dependency`, 유형을 지정하지 않은 경우 이 유형을 가정하여 NuGet을 대신 사용하는 것이 가장 좋습니다.

- `.nuspec`: `packageTypes\packageType` 요소 아래의 `<metadata>` 노드 내에서 패키지 유형을 나타냅니다.

    ```xml
    <?xml version="1.0" encoding="utf-8"?>
    <package xmlns="http://schemas.microsoft.com/packaging/2010/07/nuspec.xsd">
        <metadata>
        <!-- ... -->
        <packageTypes>
            <packageType name="DotnetTool" />
        </packageTypes>
        </metadata>
    </package>
    ```
