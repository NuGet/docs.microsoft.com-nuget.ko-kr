---
title: "NuGet project.json 보관 콘텐츠 | Microsoft Docs"
author: kraigb
ms.author: kraigb
manager: ghogen
ms.date: 01/17/2018
ms.topic: article
ms.prod: nuget
ms.technology: 
description: "project.json 콘텐츠의 기타 비트는 NuGet 설명서의 다른 영역에서 제거됩니다."
keywords: "NuGet project.json 파일"
ms.reviewer:
- karann-msft
- unniravindranathan
ms.openlocfilehash: 42a40c6c637839c13effc9e476ac5702a92cfd2a
ms.sourcegitcommit: 4651b16a3a08f6711669fc4577f5d63b600f8f58
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 02/01/2018
---
# <a name="projectjson-archive"></a>project.json 보관 파일

`project.json` 참조 형식은 NuGet 3.x와 함께 도입되었으며 특정 프로젝트 유형에 사용됩니다. 이 참조 형식은 종속성이 프로젝트 파일에 직접 나열되는 PackageReference 형식이 도입되면서 더 이상 사용되지 않습니다.

다음 항목도 참조하세요.

- [project.json 스키마](project-json.md)
- [project.json이 패키지 작성자에 미치는 영향](project-json-impact.md)
- [project.json 및 UWP](project-json-and-uwp.md)

## <a name="projectjson-reference-format"></a>project.json 참조 형식

*원래 [패키지 복원](../what-is-nuget.md)에 포함됩니다.*

참조 형식 목록에서:

- [`project.json`](project-json.md): *(사용되지 않음)* 연결된 `project.lock.json` 파일의 전체 패키지 그래프와 함께 프로젝트의 종속성 목록을 유지 관리하는 JSON 파일입니다. 이 형식 대신 PackageReference가 사용됩니다.

## <a name="nuget-restore-on-mono"></a>Mono에서 nuget 복원

*원래 [NuGet 클라이언트 도구 설치](../install-nuget-client-tools.md)에 포함됩니다.*

`project.json`에서 작동합니다.

## <a name="constraining-package-versions-with-restore"></a>복원을 사용하여 패키지 버전 제한

*원래 [패키지 복원](../consume-packages/package-restore.md#constraining-package-versions-with-restore)에 포함됩니다.*

- `project.json`: 종속성의 버전 번호를 사용하여 버전 범위를 직접 지정합니다. 예:

    ```json
    "Newtonsoft.json": "[6, 7)"
    ```

## <a name="nuget-cli-commands"></a>NuGet CLI 명령

- `nuget install`은 `project.json`에서 작동하지 않습니다.
- `nuget restore`: `project.json`을 사용하는 프로젝트에서 필요한 경우 `project.lock.json` 파일과 `<project>.nuget.props` 파일을 생성합니다. (두 파일 모두 소스 제어에서 생략할 수 있습니다.) `<projectPath>` 인수는 `project.json` 파일을 가리키고 `packages.config` 또는 프로젝트 파일을 가리키는 것과 동일한 동작을 포함할 수 있습니다. 패키지 폴더의 우선 순위에서 `project.json`를 사용하면 `%userprofile%\.nuget\packages`가 먼저 검색됩니다.
- `nuget update`: Mono에서 이 명령은 `project.json`을 사용하는 프로젝트에서 작동하지 않습니다.

## <a name="dependency-resolution-with-packagereference"></a>PackageReference를 사용하여 종속성 확인

*원래 [종속성 확인](../consume-packages/dependency-resolution.md#dependency-resolution-with-packagereference)에 포함됩니다.*

PackageReference의 동작은 `project.json`에도 적용됩니다. NuGet 복원은 종속성 그래프를 `project.json` 옆에 있는 `project.lock.json` 파일에 씁니다.

## <a name="managing-dependency-assets"></a>종속성 자산 관리

*원래 [종속성 확인](../consume-packages/dependency-resolution.md#managing-dependency-assets)에 포함됩니다.*

`project.json` 형식을 사용하는 경우 종속성에서 최상위 프로젝트로 이동하는 자산을 제어할 수 있습니다. 자세한 내용은 [project.json](project-json.md)을 참조하세요.

## <a name="excluding-references"></a>참조 제외

*원래 [종속성 확인](../consume-packages/dependency-resolution.md#excluding-references)에 포함됩니다.*

- `project.json`: PackageC에 대한 종속성에 `"exclude" : "all"`을 추가합니다.

    ```json
    {
        "dependencies": {
            "PackageC": {
            "version": "1.0.0",
            "exclude": "all"
            }
        }
    }
    ```

## <a name="resolving-incompatible-package-errors"></a>호환되지 않는 패키지 오류 해결

*원래 [종속성 확인](../consume-packages/dependency-resolution.md#resolving-incompatible-package-errors)에 포함됩니다.*

추가된 오류 해결 방법:

- **권장하지 않음**: 패키지 작성자와 함께 작업하는 동안의 임시 해결 방법으로, `netcore`, `netstandard` 및 `netcoreapp`을 대상으로 하는 프로젝트에서 다른 프레임워크를 호환되는 항목으로 나타낼 수 있으므로 다른 프레임워크를 대상으로 하는 패키지를 사용할 수 있습니다. [project.json imports](project-json.md#imports) 및 [PackageTargetFallback MSBuild restore 대상](../reference/msbuild-targets.md#packagetargetfallback)을 참조하세요. 이로 인해 예기치 않은 동작이 발생할 수 있으므로 업데이트 시 패키지 작성자와 협력하여 패키지 비호환성 문제를 해결하는 것이 가장 좋습니다.

## <a name="target-frameworks"></a>대상 프레임워크

*원래 [대상 프레임워크](../reference/target-frameworks.md)에 포함됩니다.*

- [project.json](project-json.md): `frameworks` 노드는 프로젝트를 컴파일할 수 있는 프레임워크 버전을 지정합니다.

## <a name="creating-a-package"></a>패키지 만들기

*원래 [패키지 만들기](../create-packages/creating-a-package.md)에 포함됩니다.*

### <a name="setting-a-package-type"></a>패키지 유형 설정

.NET Core 1.x의 경우 DotnetCliTool 패키지가 설치되면 Visual Studio에서는 패키지를 `dependencies` 노드 대신 `project.json` `tools` 노드에 배치합니다.

패키지 형식은 `project.json`에 설정되어 있습니다.

- `project.json`: `packOptions.packageType` 속성 json 내에 패키지 유형을 나타냅니다.

    ```json
    {
        // ...
        "packOptions": {
        "packageType": "DotnetCliTool"
        }
    }
    ```

### <a name="adding-targets-and-props-for-msbuild"></a>MSBuild용 targets 및 props 추가

*원래 [Visual Studio 2015를 통해 .NET Standard NuGet 패키지 만들기](../guides/create-net-standard-packages-vs2015.md)에 포함됩니다.*

`project.json`을 사용하는 경우 대상이 프로젝트에는 추가되지 않지만 `project.lock.json`을 통해 사용될 수 있게 됩니다.

### <a name="package-versioning"></a>패키지 버전 관리

*원래 [패키지 버전 관리](../reference/package-versioning.md)에 포함됩니다.*

`project.json` 형식을 사용하는 경우 NuGet은 숫자의 주, 부, 패치 및 시험판 접미사 부분에 와일드카드 표기법(\*)도 사용하도록 지원합니다.

### <a name="nugetconfig-reference"></a>NuGet.Config 참조

*원래 [NuGet.Config 참조](../reference/nuget-config-file.md)에 포함됩니다.*

`globalPackagesFolder`는 `project.json`에만 적용됩니다.

### <a name="nuspec-file-reference"></a>nuspec 파일 참조

*원래 [nuspec 참조](../reference/nuspec.md)에 포함됩니다.*

`project.json`에서는 `<contentFiles>` 요소가 `<files>` 대신 사용됩니다.

### <a name="package-manager-options-control"></a>패키지 관리자 옵션 제어

*원래 [패키지 관리자 UI 참조](../tools/package-manager-ui.md)에 포함됩니다.*

`project.json` 참조 형식을 사용하는 프로젝트는 **미리 보기 창 표시** 옵션만 표시합니다.

### <a name="visual-studio-templates"></a>Visual Studio 템플릿

*원래 [Visual Studio 템플릿의 NuGet 패키지](../visual-studio-extensibility/visual-studio-templates.md)에 포함됩니다.*

모범 사례: `project.json` 파일을 템플릿에 포함하지 않고, NuGet 패키지를 설치할 때 추가될 참조 또는 내용을 포함하지 않습니다.