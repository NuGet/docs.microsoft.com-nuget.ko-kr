---
title: NuGet 패키지 종속성 확인
description: NuGet 패키지의 종속성을 확인하여 NuGet 2.x 및 NuGet 3.x 이상에 모두 설치하는 프로세스를 자세히 설명합니다.
author: karann-msft
ms.author: karann
ms.date: 08/14/2017
ms.topic: conceptual
ms.openlocfilehash: cdbe13df04bb27091b684a4ae27b0e751da1098f
ms.sourcegitcommit: 1d1406764c6af5fb7801d462e0c4afc9092fa569
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 09/04/2018
ms.locfileid: "43549036"
---
# <a name="how-nuget-resolves-package-dependencies"></a>NuGet에서 패키지 종속성을 확인하는 방법

[restore](../consume-packages/package-restore.md) 프로세스의 일부로 설치하는 것을 포함하여 패키지를 설치하거나 다시 설치할 때마다 NuGet은 첫 번째 패키지가 종속된 모든 추가 패키지도 설치합니다.

그런 다음 이러한 직접적인 종속성에도 자체의 종속성이 있을 수 있으며, 이에 따라 임의의 수준까지 계속 종속될 수 있습니다. 이렇게 하면 패키지 간의 관계가 모든 수준임을 설명하는 *종속성 그래프*를 생성합니다.

여러 패키지의 종속성이 같은 경우 동일한 패키지 ID가 그래프에 여러 번 표시될 수 있으며, 잠재적으로 서로 다른 버전 제약 조건이 있을 수 있습니다. 그러나 프로젝트에서 특정 패키지의 한 버전만 사용할 수 있으므로 NuGet은 사용할 버전을 선택해야 합니다. 정확한 프로세스는 사용되는 패키지 관리 형식에 따라 다릅니다.

## <a name="dependency-resolution-with-packagereference"></a>PackageReference를 사용하여 종속성 확인

PackageReference 형식을 사용하여 패키지를 프로젝트에 설치하는 경우 NuGet은 적절한 파일에서 단순 패키지 그래프에 대한 참조를 추가하고 충돌을 미리 해결합니다. 이 프로세스는 *전이적 복원*이라고 합니다. 패키지를 다시 설치하거나 복원하면 그래프에 나열된 패키지가 다운로드되어 더 빠르고 예측 가능한 빌드가 수행됩니다. 또한 2.8.\*와 같은 와일드카드(유동) 버전을 활용하여 클라이언트 컴퓨터 및 빌드 서버에서 비용이 많이 들고 오류가 발생하기 쉬운 `nuget update` 호출을 방지할 수 있습니다.

NuGet 복원 프로세스가 빌드하기 전에 실행되면, 먼저 메모리에서 종속성을 확인한 다음, PackageReference를 사용하여 결과 그래프를 프로젝트의 `obj` 폴더에서 `project.assets.json`이라는 파일에 씁니다. 그러면 MSBuild에서 이 파일을 읽고 잠재적인 참조를 찾을 수 있는 폴더의 집합으로 해당 파일을 변환한 다음 메모리의 프로젝트 트리에 추가합니다.

잠금 파일은 임시적이며 원본 제어에 추가하면 안됩니다. `.gitignore`과 `.tfignore` 모두에서 기본적으로 나열됩니다. [패키지 및 원본 제어](packages-and-source-control.md)를 참조하세요.

### <a name="dependency-resolution-rules"></a>종속성 확인 규칙

전이적 복원은 종속성을 확인하는 네 가지 주요 규칙, 즉 적용 가능한 가장 낮은 버전, 유동적인 버전, 가장 가까운 성공 및 사촌 종속성을 적용합니다.

<a name="lowest-applicable-version"></a>

#### <a name="lowest-applicable-version"></a>적용 가능한 가장 낮은 버전

적용 가능한 가장 낮은 버전 규칙은 패키지의 종속성으로 정의된 대로 가장 낮은 버전의 패키지를 복원합니다. [유동적인 버전](#floating-versions)으로 선언되지 않은 경우 응용 프로그램 또는 클래스 라이브러리에 대한 종속성에도 적용됩니다.

예를 들어 다음 그림에서 1.0-beta는 1.0보다 낮은 것으로 간주되므로 NuGet은 1.0 버전을 선택합니다.

![적용 가능한 가장 낮은 버전 선택](media/projectJson-dependency-1.png)

다음 그림에서 2.1 버전은 피드에서 사용할 수 없지만 버전 제약 조건이 2.1 이상이므로 이 경우 NuGet에서 찾을 수 있는 버전 중 다음으로 가장 낮은 버전인 2.2를 선택합니다.

![피드에서 사용 가능한 버전 중 다음으로 가장 낮은 버전 선택](media/projectJson-dependency-2.png)

응용 프로그램이 피드에서 사용할 수 없는 정확한 버전 번호(예: 1.2)를 지정하면, 패키지를 설치하거나 복원할 때 오류로 인해 NuGet이 실패합니다.

![정확한 패키지 버전을 사용할 수 없는 경우 NuGet에서 오류 생성](media/projectJson-dependency-3.png)

<a name="floating-versions"></a>

#### <a name="floating-wildcard-versions"></a>유동적인(와일드카드) 버전

유동 또는 와일드카드 종속성 버전은 \* 와일드카드로 지정됩니다(예: 6.0.\*). 이 버전 사양에는 "최신 6.0.x 버전 사용"이 나와 있습니다. 4.\*는 "최신 4.x 버전 사용"을 의미합니다. 와일드카드를 사용하면 소비 응용 프로그램(또는 패키지)을 변경하지 않고도 종속성 패키지가 계속 진화할 수 있습니다.

와일드카드를 사용하면 NuGet에서 버전 패턴과 일치하는 패키지의 가장 높은 버전을 확인합니다. 예를 들어 6.0.\*는 6.0으로 시작하는 패키지의 버전 중 가장 높은 버전을 가져옵니다.

![유동적인 6.0.* 버전 요구 시 6.0.1 버전 선택](media/projectJson-dependency-4.png)

> [!Note]
> 와일드카드 및 시험판 버전의 동작에 대한 자세한 내용은 [패키지 버전 관리](../reference/package-versioning.md#version-ranges-and-wildcards)를 참조하세요.


<a name="nearest-wins"></a>

#### <a name="nearest-wins"></a>가장 가까운 성공

응용 프로그램에 대한 패키지 그래프에 동일한 패키지의 다른 버전이 포함된 경우 NuGet은 그래프에서 응용 프로그램과 가장 가까운 패키지를 선택하고 다른 모든 패키지는 무시합니다. 이 동작을 통해 응용 프로그램에서 종속성 그래프의 특정 패키지 버전을 재정의할 수 있습니다.

아래 예에서 응용 프로그램은 버전 제약 조건이 2.0 이상인 B 패키지에 직접 종속됩니다. 또한 이 응용 프로그램은 B 패키지에 종속된 A 패키지에도 종속되지만 1.0 이상인 제약 조건을 갖습니다. B 패키지 2.0에 대한 종속성이 그래프의 응용 프로그램에 더 가깝기 때문에 해당 버전이 사용됩니다.

![가장 가까운 성공 규칙을 사용하는 응용 프로그램](media/projectJson-dependency-5.png)

>[!Warning]
> 가장 가까운 성공 규칙으로 인해 패키지 버전의 다운그레이드가 발생할 수 있으므로 그래프에서 다른 종속성이 손상될 수 있습니다. 따라서 이 규칙은 사용자에게 경고하는 경고와 함께 적용됩니다.

또한 지정된 종속성이 무시되면 NuGet에서 그래프의 해당 분기에 있는 나머지 모든 종속성도 무시하기 때문에 이 규칙에서 큰 종속성 그래프(예: BCL 패키지의 경우)를 사용하여 효율성을 높입니다. 예를 들어 아래 다이어그램에서 C 패키지 2.0이 사용되었기 때문에 NuGet은 이전 버전의 C 패키지를 참조하는 그래프의 모든 분기를 무시합니다.

![NuGet이 그래프에서 패키지를 무시하는 경우 무시되는 전체 분기](media/projectJson-dependency-6.png)

<a name="cousin-dependencies"></a>

#### <a name="cousin-dependencies"></a>사촌 종속성

응용 프로그램이 그래프의 동일한 거리에서 서로 다른 패키지 버전을 참조하는 경우 NuGet은 모든 버전 요구 사항(예: [적용 가능한 가장 낮은 버전](#lowest-applicable-version) 및 [유동적인 버전](#floating-versions) 규칙)을 충족하는 가장 낮은 버전을 사용합니다. 예를 들어 아래 이미지에서 B 패키지의 2.0 버전은 1.0 이상의 다른 제약 조건을 충족하므로 사용됩니다.

![모든 제약 조건을 충족하는 하위 버전을 사용하여 사촌 종속성 확인](media/projectJson-dependency-7.png)

모든 버전 요구 사항을 충족할 수 없는 경우도 있습니다. 아래와 같이 A 패키지에는 정확히 B 패키지 1.0이 필요하고 C 패키지에는 B 패키지 2.0 이상이 필요한 경우, NuGet에서 종속성을 확인할 수 없으며 오류가 발생합니다.

![정확한 버전 요구 사항으로 인해 확인할 수 없는 종속성](media/projectJson-dependency-8.png)

이러한 상황에서는 [가장 가까운 성공](#nearest-wins) 규칙이 적용되도록 최상위 소비자(응용 프로그램 또는 패키지)가 B 패키지에 자체의 직접적인 종속성을 추가해야 합니다.

## <a name="dependency-resolution-with-packagesconfig"></a>packages.config를 사용하여 종속성 확인

`packages.config`를 사용하면 프로젝트의 종속성이 단순 목록으로 `packages.config`에 기록됩니다. 이러한 패키지의 모든 종속성도 동일한 목록에 기록됩니다. 패키지가 설치되면 NuGet에서 `.csproj` 파일, `app.config`, `web.config` 및 기타 개별 파일을 수정할 수도 있습니다.

`packages.config`를 사용하면 NuGet은 각각의 개별 패키지를 설치하는 동안 종속성 충돌을 해결하려고 합니다. 즉 A 패키지가 설치되고 B 패키지에 종속되어 있고 B 패키지가 이미 다른 패키지의 종속성으로 `packages.config`에 나열되어 있는 경우, NuGet은 요청된 B 패키지의 버전을 비교하고 모든 버전 제약 조건을 충족하는 버전을 찾으려고 합니다. 특히 NuGet은 종속성을 충족하는 더 낮은 *major.minor* 버전을 선택합니다.

기본적으로 NuGet 2.8은 가장 낮은 패치 버전을 찾습니다([NuGet 2.8 릴리스 정보](../release-notes/nuget-2.8.md#patch-resolution-for-dependencies) 참조). `Nuget.Config`의 `DependencyVersion` 특성 및 명령줄의 `-DependencyVersion` 스위치를 통해 이 설정을 제어할 수 있습니다.  

더 큰 종속성 그래프의 경우 종속성을 확인하기 위한 `packages.config` 프로세스가 복잡해집니다. 새 패키지를 설치할 때마다 그래프 전체를 통과해야 하며 버전 충돌이 발생할 가능성이 높습니다. 충돌이 발생하면 특히 프로젝트 파일 자체를 잠재적으로 수정하여 설치가 중지되고 프로젝트가 확정되지 않은 상태로 유지됩니다. 다른 패키지 관리 형식을 사용하는 경우에는 문제가 되지 않습니다.

## <a name="managing-dependency-assets"></a>종속성 자산 관리

PackageReference 형식을 사용하는 경우 종속성에서 최상위 프로젝트로 이동하는 자산을 제어할 수 있습니다. 자세한 내용은 [PackageReference](package-references-in-project-files.md#controlling-dependency-assets)를 참조하세요.

또한 최상위 프로젝트 자체가 패키지인 경우 `.nuspec` 파일에 나열된 종속성이 있는 `include` 및 `exclude` 특성을 사용하여 이 흐름을 제어할 수도 있습니다. [.nuspec 참조 - 종속성](../reference/nuspec.md#dependencies)을 참조하세요.

## <a name="excluding-references"></a>참조 제외

프로젝트에서 동일한 이름의 어셈블리를 두 번 이상 참조하여 디자인 타임 및 빌드 시간 오류를 생성할 수 있는 시나리오가 있습니다. `C.dll`의 사용자 지정 버전을 포함하고 `C.dll`도 포함된 C 패키지를 참조하는 프로젝트를 생각해 보세요. 동시에 이 프로젝트는 C 패키지와 `C.dll`에도 종속된 B 패키지에 종속됩니다. 결과적으로 NuGet은 사용할 `C.dll`을 결정할 수 없지만 B 패키지도 이에 종속되기 때문에 C 패키지에 대한 프로젝트의 종속성을 제거할 수 없습니다.

이 문제를 해결하려면, 원하는 `C.dll`을 직접 참조하거나 올바른 패키지를 참조하는 다른 패키지를 사용한 다음, 해당 자산을 모두 제외하는 C 패키지에 대한 종속성을 추가해야 합니다. 이렇게 하려면 사용 중인 패키지 관리 형식에 따라 다음과 같이 수행합니다.

- [PackageReference](../consume-packages/package-references-in-project-files.md): 종속성에 `Exclude="All"`을 추가합니다.

    ```xml
    <PackageReference Include="PackageC" Version="1.0.0" Exclude="All" />
    ```

- `packages.config`: 원하는 `C.dll` 버전만 참조하도록 `.csproj` 파일에서 PackageC에 대한 참조를 제거합니다.
    
## <a name="dependency-updates-during-package-install"></a>패키지 설치 중 종속성 업데이트 

종속성 버전이 이미 충족된 경우 다른 패키지를 설치하는 동안 종속성이 업데이트되지 않습니다. 예를 들어 B 패키지에 종속된 A 패키지를 고려하고 버전 번호를 1.0으로 지정합니다. 소스 리포지토리에는 B 패키지의 버전 1.0, 1.1 및 1.2가 포함되어 있습니다. B 버전 1.0이 이미 포함된 프로젝트에 A가 설치된 경우 B 1.0은 버전 제약 조건을 충족하므로 계속 사용됩니다. 그러나 A 패키지에서 1.1 버전 이상의 B를 요청하면 B 1.2가 설치됩니다. 

## <a name="resolving-incompatible-package-errors"></a>호환되지 않는 패키지 오류 해결

패키지 복원 작업 중에 "하나 이상의 패키지가 호환되지 않습니다..." 또는 패키지가 프로젝트의 대상 프레임워크와 "호환되지 않습니다."라는 오류가 표시될 수 있습니다.

프로젝트에서 참조하는 하나 이상의 패키지에서 프로젝트의 대상 프레임워크를 지원하지 않는다고 나타내는 경우에 이 오류가 발생합니다. 즉 패키지에는 프로젝트와 호환되는 대상 프레임워크에 대한 `lib` 폴더에 적합한 DLL이 포함되지 않습니다. (목록은 [대상 프레임워크](../reference/target-frameworks.md)를 참조하세요.) 

예를 들어 프로젝트에서 `netstandard1.6`을 대상으로 하고 `lib\net20` 및 `\lib\net45` 폴더에만 DLL이 포함되는 패키지를 설치하려고 하면 패키지 및 해당 종속 항목에 대해 다음과 같은 메시지가 표시됩니다.

```output
Restoring packages for myproject.csproj...
Package ContosoUtilities 2.1.2.3 is not compatible with netstandard1.6 (.NETStandard,Version=v1.6). Package ContosoUtilities 2.1.2.3 supports:
  - net20 (.NETFramework,Version=v2.0)
  - net45 (.NETFramework,Version=v4.5)
Package ContosoCore 0.86.0 is not compatible with netstandard1.6 (.NETStandard,Version=v1.6). Package ContosoCore 0.86.0 supports:
  - 11 (11,Version=v0.0)
  - net20 (.NETFramework,Version=v2.0)
  - sl3 (Silverlight,Version=v3.0)
  - sl4 (Silverlight,Version=v4.0)
One or more packages are incompatible with .NETStandard,Version=v1.6.
Package restore failed. Rolling back package changes for 'MyProject'.
```

비호환성을 해결하려면 다음 중 하나를 수행합니다.

- 프로젝트의 대상을 사용할 패키지에서 지원하는 프레임워크로 변경합니다.
- 패키지 작성자에게 문의하고 선택한 프레임워크에 대한 지원을 추가합니다. [nuget.org](https://www.nuget.org/)의 각 패키지 목록 페이지에는 이 목적을 위한 **연락처 소유자** 링크가 있습니다.

