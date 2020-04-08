---
title: NuGet에 대한 project.json 파일 참조
description: 일부 프로젝트 형식에서 project.json은 프로젝트에 사용된 NuGet 패키지 목록을 유지 관리합니다.
author: karann-msft
ms.author: karann
ms.date: 07/27/2017
ms.topic: reference
ms.openlocfilehash: 5ecbcd4855de8ea7b6301a5e307779216baf96fc
ms.sourcegitcommit: 2b50c450cca521681a384aa466ab666679a40213
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/07/2020
ms.locfileid: "69488291"
---
# <a name="projectjson-reference"></a>project.json 참조

*NuGet 3.x 이상*

`project.json` 파일은 패키지 관리 형식이라고 하는 프로젝트에 사용되는 패키지의 목록을 유지 관리합니다. `packages.config`를 대체하여 NuGet 4.0 이상이 포함된 [PackageReference](../consume-packages/package-references-in-project-files.md)로 대체합니다.

[`project.lock.json`](#projectlockjson) 파일(아래 설명 참조)도 `project.json`을 사용하는 프로젝트에서 사용됩니다.

`project.json`에는 다음과 같은 기본 구조가 있습니다. 여기에는 네 개의 최상위 개체 각각에 임의 개수의 자식 개체가 있을 수 있습니다.

```json
{
    "dependencies": {
        "PackageID" : "{version_constraint}"
    },
    "frameworks" : {
        "TxM" : {}
    },
    "runtimes" : {
        "RID": {}
    },
    "supports" : {
        "CompatibilityProfile" : {}
    }
}
```

## <a name="dependencies"></a>종속성

프로젝트의 NuGet 패키지 종속성은 다음과 같은 형식으로 나열됩니다.

```json
"PackageID" : "version_constraint"
```

다음은 그 예입니다.

```json
"dependencies": {
    "Microsoft.NETCore": "5.0.0",
    "System.Runtime.Serialization.Primitives": "4.0.10"
}
```

`dependencies` 섹션은 NuGet 패키지 관리자 대화 상자에서 패키지 종속성을 프로젝트에 추가하는 부분입니다.

패키지 ID는 nuget.org의 패키지 ID에 해당하며, `Install-Package Microsoft.NETCore` 패키지 관리자 콘솔에서 사용된 ID와 동일합니다.

패키지를 복원할 때 `"5.0.0"`의 버전 제약 조건은 `>= 5.0.0`을 의미합니다. 즉 서버에서 5.0.0이 아닌 5.0.1을 사용할 수 있는 경우 NuGet에서 5.0.1을 설치하고 업그레이드에 대해 경고합니다. 그렇지 않은 경우 NuGet은 제약 조건과 일치하는 서버에서 가능한 가장 낮은 버전을 선택합니다.

확인 규칙에 대한 자세한 내용은 [종속성 확인](../concepts/dependency-resolution.md)을 참조하세요.

### <a name="managing-dependency-assets"></a>종속성 자산 관리

최상위 프로젝트로 이동하는 종속성의 자산은 종속성 참조의 `include` 및 `exclude` 속성에 쉼표로 구분된 태그의 집합을 지정하여 제어됩니다. 이러한 태그는 아래 표에 나와 있습니다.

| include/exclude 태그 | 영향을 받는 대상 폴더 |
| --- | --- |
| contentFiles | 콘텐츠  |
| 런타임 | Runtime, Resources 및 FrameworkAssemblies  |
| compile | lib |
| build | build(MSBuild props 및 targets) |
| native | native |
| none | 영향을 받는 폴더 없음 |
| all | 모든 폴더 |

`exclude`로 지정된 태그는 `include`로 지정된 태그보다 우선 순위가 높습니다. 예를 들어 `include="runtime, compile" exclude="compile"`은 `include="runtime"`과 같습니다.

예를 들어 종속성의 `build` 및 `native` 폴더를 포함하려면 다음을 사용합니다.

```json
{
  "dependencies": {
    "packageA": {
      "version": "1.0.0",
      "include": "build, native"
    }
  }
}
```

종속성의 `content` 및 `build` 폴더를 제외하려면 다음을 사용합니다.

```json
{
  "dependencies": {
    "packageA": {
      "version": "1.0.0",
      "exclude": "contentFiles, build"
    }
  }
}
```

## <a name="frameworks"></a>프레임워크

`net45`, `netcoreapp`, `netstandard`와 같이 프로젝트가 실행되는 프레임워크가 나열됩니다.

```json
"frameworks": {
    "netcore50": {}
    }
 ```

`frameworks` 섹션에는 하나의 항목만 허용됩니다. (여러 대상을 허용하는 사용되지 않는 DNX 도구 체인으로 빌드된 ASP.NET 프로젝트에 대한 `project.json` 파일은 예외입니다.)

## <a name="runtimes"></a>runtimes

`win10-arm`, `win8-x64`, `win8-x86`과 같이 앱이 실행되는 운영 체제 및 아키텍처가 나열됩니다.

```json
"runtimes": {
    "win10-arm": { },
    "win10-arm-aot": { },
    "win10-x86": { },
    "win10-x86-aot": { },
    "win10-x64": { },
    "win10-x64-aot": { }
}
```

모든 런타임에서 실행할 수 있는 PCL이 포함된 패키지는 런타임을 지정할 필요가 없습니다. 또한 모든 종속성을 충족해야 합니다. 그렇지 않으면 런타임을 지정해야 합니다.


## <a name="supports"></a>지원

패키지 종속성에 대한 검사 집합을 정의합니다. 실행될 PCL 또는 앱의 위치를 정의할 수 있습니다. 코드가 다른 곳에서 실행될 수 있으므로 이 정의는 제한적이지 않습니다. 그러나 이러한 검사를 지정하면 NuGet은 나열된 TxM에서 모든 종속성이 충족되는지 확인합니다. 이 값의 예는 `net46.app`, `uwp.10.0.app` 등입니다.

이 섹션은 [이식 가능한 클래스 라이브러리] 대상 대화 상자에서 항목을 선택할 때 자동으로 채워져야 합니다.

```json
"supports": {
    "net46.app": {},
    "uwp.10.0.app": {}
}
```

## <a name="imports"></a>가져오기

imports는 `dotnet` TxM을 사용하는 패키지가 dotnet TxM을 선언하지 않은 패키지와 작동할 수 있도록 설계되었습니다. 프로젝트에서 `dotnet` TxM을 사용하는 경우 `dotnet`이 아닌 플랫폼이 `project.json`과 호환될 수 있도록 `dotnet`에 다음을 추가하지 않는 한 종속된 모든 패키지에도 `dotnet` TxM이 있어야 합니다.

```json
"frameworks": {
    "dotnet": { "imports" : "portable-net45+win81" }
}
```

`dotnet` TxM을 사용하는 경우 PCL 프로젝트 시스템에서 지원되는 대상을 기반으로 하는 적절한 `imports` 문을 추가합니다.

## <a name="differences-from-portable-apps-and-web-projects"></a>이식 가능한 앱 및 웹 프로젝트의 차이점

NuGet에서 사용하는 `project.json` 파일은 ASP.NET Core 프로젝트에 있는 하위 집합입니다. ASP.NET Core `project.json`은 프로젝트 메타데이터, 컴파일 정보 및 종속성에 사용됩니다. 다른 프로젝트 시스템에서 이 세 가지 항목을 사용하면 별도의 파일로 분할되고 `project.json`에는 정보가 거의 포함되지 않습니다. 주목할 만한 차이점은 다음과 같습니다.

- `frameworks` 섹션에는 하나의 프레임워크만 있을 수 있습니다.

- 파일에는 DNX `project.json` 파일에서 나타나는 종속성, 컴파일 옵션 등이 포함될 수 없습니다. 단일 프레임워크만 있을 수 있으므로 프레임워크 특정 종속성을 입력하는 것은 적합하지 않습니다.

- 컴파일은 MSBuild에서 처리하므로 컴파일 옵션, 선행 프로세서 정의 등은 모두 `project.json`이 아니라 MSBuild 프로젝트 파일의 일부입니다.

NuGet 3 이상에서는 Visual Studio의 패키지 관리자 UI에서 내용을 조작하므로 개발자는 `project.json`을 수동으로 편집할 필요가 없습니다. 즉 파일을 확실히 편집할 수 있지만, 패키지 복원을 시작하거나 다른 방식으로 복원을 호출하려면 프로젝트를 빌드해야 합니다. [패키지 복원](../consume-packages/package-restore.md)을 참조하세요.


## <a name="projectlockjson"></a>project.lock.json

`project.lock.json` 파일은 `project.json`을 사용하는 프로젝트에서 NuGet 패키지를 복원하는 과정에서 생성됩니다. NuGet에서 패키지의 그래프를 진행하면서 생성되는 모든 정보의 스냅샷을 저장하며, 프로젝트에 속한 모든 패키지의 버전, 내용 및 종속성이 포함됩니다. 빌드 시스템은 이 기능을 사용하여 프로젝트 자체의 로컬 패키지 폴더를 따르는 대신 프로젝트를 빌드할 때 관련된 전역 위치에서 패키지를 선택합니다. 이렇게 하면 별도의 많은 `project.lock.json` 파일 대신 `.nuspec`만 읽어야 하므로 빌드 성능이 더 빠릅니다.

`project.lock.json`은 패키지 복원 시 자동으로 생성되므로 `.gitignore` 및 `.tfignore`파일에 추가하여 원본 제어에서 생략할 수 있습니다([패키지 및 원본 제어](../consume-packages/packages-and-source-control.md) 참조). 그러나 원본 제어에 포함하는 경우 시간이 지남에 따라 확인된 종속성의 변경 내용이 변경 기록에 표시됩니다.
