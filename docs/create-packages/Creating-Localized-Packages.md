---
title: 지역화된 NuGet 패키지를 만드는 방법
description: 단일 패키지에서 모든 어셈블리를 포함하거나 별도 어셈블리를 게시하여 지역화된 NuGet 패키지를 만드는 두 가지 방법에 대한 자세한 내용입니다.
author: karann-msft
ms.author: karann
ms.date: 01/18/2018
ms.topic: conceptual
ms.openlocfilehash: dbc3781bd17f815c6b32fc70b275469337148f41
ms.sourcegitcommit: 7441f12f06ca380feb87c6192ec69f6108f43ee3
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/15/2019
ms.locfileid: "69488830"
---
# <a name="creating-localized-nuget-packages"></a>지역화된 NuGet 패키지 만들기

두 가지 방법으로 라이브러리의 지역화된 버전을 만들 수 있습니다.

1. 단일 패키지에 모든 지역화된 리소스 어셈블리를 포함합니다.
1. 엄격한 규칙 집합에 따라 별도의 지역화된 위성 패키지를 만듭니다.

두 방법에는 다음 섹션에서 설명된 장점과 단점이 있습니다.

## <a name="localized-resource-assemblies-in-a-single-package"></a>단일 패키지의 모든 지역화된 리소스 어셈블리

단일 패키지에서 지역화된 리소스 어셈블리를 포함하는 작업은 일반적으로 가장 단순한 방법입니다. 이렇게 하려면 패키지 기본값 이외의 지원되는 언어에서 `lib` 내에 폴더를 만듭니다(en-us로 간주). 이러한 폴더에 리소스 어셈블리와 지역화된 IntelliSense XML 파일을 배치할 수 있습니다.

예를 들어 다음 폴더 구조는 독일어(de), 이탈리아어(it), 일본어(ja), 러시아어(ru), 중국어(간체)(zh-Hans) 및 중국어(번체)(zh-Hant)를 지원합니다.

    lib
    └───net40
        │   Contoso.Utilities.dll
        │   Contoso.Utilities.xml
        │
        ├───de
        │       Contoso.Utilities.resources.dll
        │       Contoso.Utilities.xml
        │
        ├───it
        │       Contoso.Utilities.resources.dll
        │       Contoso.Utilities.xml
        │
        ├───ja
        │       Contoso.Utilities.resources.dll
        │       Contoso.Utilities.xml
        │
        ├───ru
        │       Contoso.Utilities.resources.dll
        │       Contoso.Utilities.xml
        │
        ├───zh-Hans
        │       Contoso.Utilities.resources.dll
        │       Contoso.Utilities.xml
        │
        └───zh-Hant
                Contoso.Utilities.resources.dll
                Contoso.Utilities.xml

언어가 모두 `net40` 대상 프레임워크 폴더 아래에 나열됩니다. 사용자가 [여러 프레임워크를 지원하는](../create-packages/supporting-multiple-target-frameworks.md) 경우 `lib` 아래에 각 변형에 대한 폴더가 있습니다.

이러한 폴더가 준비되면 `.nuspec`에 있는 모든 파일을 참조합니다.

```xml
<?xml version="1.0"?>
<package>
    <metadata>...
    </metadata>
    <files>
    <file src="lib\**" target="lib" />
    </files>
</package>
```

이 방법을 사용하는 하나의 예제 패키지는 [Microsoft.Data.OData 5.4.0](http://nuget.org/packages/Microsoft.Data.OData/5.4.0)입니다.

### <a name="advantages-and-disadvantages-localized-resource-assemblies"></a>장점 및 단점(지역화된 리소스 어셈블리)

단일 패키지에서 모든 언어를 번들하면 몇 가지 단점이 있습니다.

1. **공유 메타데이터**: NuGet 패키지에 단일 `.nuspec` 파일만 포함할 수 있기 때문에 단일 언어의 메타데이터만 제공할 수 있습니다. 즉, NuGet에서는 지역화된 메타데이터를 지원하지 않습니다.
1. **패키지 크기**: 지원하는 언어 수에 따라 라이브러리는 상당히 커질 수 있습니다. 그러면 패키지를 설치하고 복원하는 작업이 느려집니다.
1. **동시 릴리스**: 지역화된 파일을 단일 패키지로 번들하려면 각 지역화를 개별적으로 릴리스하는 대신 해당 패키지에 있는 모든 자산을 동시에 릴리스해야 합니다. 또한 하나의 지역화에 대한 업데이트에는 새 버전의 전체 패키지가 필요합니다.

그러나 몇 가지 이점도 있습니다.

1. **단순성**: 패키지의 소비자가 각 언어를 별도로 설치하는 것이 아니라 단일 설치에서 지원되는 모든 언어를 가져옵니다. 단일 패키지를 nuget.org에서 쉽게 찾을 수 있습니다.
1. **결합 버전**: 모든 리소스 어셈블리가 기본 어셈블리와 동일한 패키지에 있기 때문에 모두 동일한 버전 번호를 공유하며, 잘못 분리될 위험성이 없습니다.

## <a name="localized-satellite-packages"></a>지역화된 위성 패키지

.NET Framework에서 위성 어셈블리를 지원하는 방법과 마찬가지로 이 메서드는 지역화된 리소스 및 IntelliSense XML 파일을 위성 패키지로 구분합니다.

이렇게 하려면 기본 패키지는 `{identifier}.{version}.nupkg` 명명 규칙을 사용하고 기본 언어(예: en-US)에 대한 어셈블리를 포함합니다. 예를 들어 `ContosoUtilities.1.0.0.nupkg`에는 다음과 같은 구조가 포함됩니다.

    lib
    └───net40
            ContosoUtilities.dll
            ContosoUtilities.xml

그런 다음 위성 어셈블리는 `{identifier}.{language}.{version}.nupkg` 명명 규칙(예: `ContosoUtilities.de.1.0.0.nupkg`)을 사용합니다. 식별자는 기본 패키지의 식별자와 정확하게 일치**해야** 합니다.

이것이 별도 패키지이기 때문에 지역화된 메타데이터가 포함된 고유의 `.nuspec` 파일이 있습니다. `.nuspec`의 언어는 파일 이름에서 사용되는 언어와 일치**해야** 합니다.

또한 위성 어셈블리는 [] 버전 표기법을 사용하여 정확한 버전의 기본 패키지를 종속성으로 선언**해야** 합니다([패키지 버전 관리](../concepts/package-versioning.md) 참조). 예를 들어 `ContosoUtilities.de.1.0.0.nupkg`는 `ContosoUtilities.1.0.0.nupkg`에서 `[1.0.0]` 표기법을 사용하여 종속성을 선언해야 합니다. 물론 위성 패키지에는 기본 패키지와 다른 버전 번호가 있습니다.

그런 다음 위성 패키지의 구조에는 패키지 파일 이름에서 `{language}`와 일치하는 하위 폴더에 있는 리소스 어셈블리 및 XML IntelliSense 파일이 포함되어야 합니다.

    lib
    └───net40
        └───de
                ContosoUtilities.resources.dll
                ContosoUtilities.xml

**참고**: `ja-JP`와 같은 특정 하위 문화권이 필요하지 않으면 항상 `ja`와 같은 개략적인 언어 식별자를 사용합니다.

위성 어셈블리에서 NuGet은 파일 이름에서 `{language}`와 일치하는 해당 폴더에 있는 해당 파일**만**을 인식합니다. 다른 특성은 모두 무시됩니다.

이러한 규칙을 모두 충족할 경우 NuGet은 패키지를 위성 패키지로 인식하고, 원래 번들되었던 것처럼 기본 패키지의 `lib` 폴더에 지역화된 파일을 설치합니다. 위성 패키지를 제거하면 동일한 폴더에서 해당 파일이 제거됩니다.

지원되는 각 언어에 대해 같은 방법으로 추가 위성 어셈블리를 만듭니다. 예를 들어 ASP.NET MVC 패키지 집합을 검사합니다.

- [Microsoft.AspNet.Mvc](http://nuget.org/packages/Microsoft.AspNet.Mvc)(영어 기본)
- [Microsoft.AspNet.Mvc.de](http://nuget.org/packages/Microsoft.AspNet.Mvc.de)(독일어)
- [Microsoft.AspNet.Mvc.ja](http://nuget.org/packages/Microsoft.AspNet.Mvc.ja)(일본어)
- [Microsoft.AspNet.Mvc.zh-Hans](http://nuget.org/packages/Microsoft.AspNet.Mvc.zh-Hans)(중국어(간체))
- [Microsoft.AspNet.Mvc.zh-Hant](http://nuget.org/packages/Microsoft.AspNet.Mvc.zh-Hant)(중국어(번체))

### <a name="summary-of-required-conventions"></a>필수 규칙 요약

- 기본 패키지 이름을 `{identifier}.{version}.nupkg`로 지정해야 합니다.
- 위성 패키지 이름을 `{identifier}.{language}.{version}.nupkg`로 지정해야 합니다.
- 위성 패키지의 `.nuspec`는 파일 이름에 맞는 해당 언어를 지정해야 합니다.
- 위성 패키지는 해당 `.nuspec` 파일에서 [] 표기법을 사용하여 정확한 버전의 기본 패키지에서 종속성을 선언해야 합니다. 범위는 지원되지 않습니다.
- 위성 패키지는 파일 이름에서 `{language}`와 정확히 일치하는 `lib\[{framework}\]{language}` 폴더에 파일을 배치해야 합니다.

### <a name="advantages-and-disadvantages-satellite-packages"></a>장점 및 단점(위성 패키지)

위성 패키지를 사용하면 몇 가지 이점이 있습니다.

1. **패키지 크기**: 기본 패키지의 전체 공간을 최소화하며 소비자는 사용할 언어의 비용만을 지불합니다.
1. **별도 메타데이터**: 각 위성 패키지에는 고유의 `.nuspec` 파일이 있으므로 고유의 지역화된 메타데이터도 있습니다. 따라서 일부 소비자는 지역화된 단어를 포함한 nuget.org를 검색하여 패키지를 보다 쉽게 찾을 수 있습니다.
1. **릴리스 분리**: 위성 어셈블리는 한 번이 아니라 시간이 지남에 따라 릴리스될 수 있으며 이를 통해 지역화 작업을 확장할 수 있습니다.

그러나 위성 패키지에는 각자 단점이 있습니다.

1. **잡동사니**: 단일 패키지 대신 nuget.org에서 복잡한 검색 결과 및 Visual Studio 프로젝트에서 긴 참조 목록을 초래할 수 있는 많은 패키지가 있습니다.
1. **엄격한 규칙** 위성 패키지가 규칙을 정확하게 따르지 않으면 적합한 지역화된 버전을 선택할 수 없습니다.
1. **버전 관리**: 각 위성 패키지에는 기본 패키지에 대한 정확한 버전 종속성이 있어야 합니다. 즉, 기본 패키지를 업데이트하면 리소스가 변경되지 않은 경우에도 모든 위성 패키지를 업데이트해야 합니다.
