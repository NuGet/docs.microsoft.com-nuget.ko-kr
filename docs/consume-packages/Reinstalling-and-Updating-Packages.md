---
title: NuGet 패키지 다시 설치 및 업데이트
description: Visual Studio에서 손상된 패키지 참조와 같이 패키지를 다시 설치하고 업데이트해야 하는 경우에 대해 자세히 설명합니다.
author: karann-msft
ms.author: karann
ms.date: 12/07/2017
ms.topic: conceptual
ms.openlocfilehash: 32b01e6066cf60f7a0942508e640fdd5658b4444
ms.sourcegitcommit: efc18d484fdf0c7a8979b564dcb191c030601bb4
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/18/2019
ms.locfileid: "68316970"
---
# <a name="how-to-reinstall-and-update-packages"></a>패키지를 다시 설치하고 업데이트하는 방법

아래에서 설명하는 [패키지를 다시 설치하는 경우](#when-to-reinstall-a-package)에는 패키지에 대한 참조가 Visual Studio 프로젝트에서 손상될 수 있는 여러 가지 상황이 있습니다. 이러한 경우 동일한 버전의 패키지를 제거한 다음 다시 설치하면 해당 참조가 작업 순서에 맞게 복원됩니다. 패키지 업데이트는 업데이트된 버전을 설치하는 것이며, 이 경우 패키지를 작업 순서에 맞게 복원하기도 합니다.

패키지 업데이트 및 다시 설치는 다음과 같이 수행됩니다.

| 메서드 | 업데이트 | 다시 설치 |
| --- | --- | --- |
| 패키지 관리자 콘솔([Update-Package 사용](#using-update-package)에서 설명) | `Update-Package` 명령 | `Update-Package -reinstall` 명령 |
| 패키지 관리자 UI | **업데이트** 탭에서 패키지를 하나 이상 선택하고 **업데이트**를 선택합니다. | **설치됨** 탭에서 패키지를 선택하고, 이름을 기록한 다음, **제거**를 선택합니다. **찾아보기** 탭으로 전환하고, 패키지 이름을 검색하여 선택한 다음, **설치**를 선택합니다. |
| nuget.exe CLI | `nuget update` 명령 | 모든 패키지의 경우 패키지 폴더를 삭제한 다음 `nuget install`을 실행합니다. 단일 패키지의 경우 패키지 폴더를 삭제하고 `nuget install <id>`를 사용하여 동일한 패키지를 다시 설치합니다. |

> [!NOTE]
> dotnet CLI의 경우 해당 절차가 필요하지 않습니다. 비슷한 시나리오에서 [dotnet CLI를 사용하여 패키지를 복원](../consume-packages/install-use-packages-dotnet-cli.md#restore-packages)할 수 있습니다.

이 문서의 내용

- [패키지를 다시 설치하는 경우](#when-to-reinstall-a-package)
- [업그레이드 버전 제한](#constraining-upgrade-versions)

## <a name="when-to-reinstall-a-package"></a>패키지를 다시 설치하는 경우

1. **패키지 복원 후 손상된 참조**: 프로젝트를 열고 NuGet 패키지를 복원했지만 손상된 참조가 계속 표시되는 경우 해당 패키지 각각을 다시 설치합니다.
1. **삭제된 파일로 인해 중단된 프로젝트**: NuGet은 패키지에서 추가된 항목을 제거할 수 있도록 하므로 실수로 패키지에서 설치된 내용을 수정하고 프로젝트를 중단할 수 있습니다. 프로젝트를 복원하려면 영향을 받은 패키지를 다시 설치합니다.
1. **패키지 업데이트로 인해 중단된 프로젝트**: 패키지 업데이트로 인해 프로젝트가 중단되는 경우 일반적으로 업데이트된 종속성 패키지로 인해 실패가 발생합니다. 종속성 상태를 복원하려면 특정 패키지를 다시 설치합니다.
1. **프로젝트 대상 변경 또는 업그레이드**: 프로젝트 대상이 변경되거나 프로젝트가 업그레이드된 경우 및 대상 프레임워크의 변경으로 인해 패키지를 다시 설치해야 하는 경우에 유용할 수 있습니다. NuGet에서는 프로젝트 대상을 변경하는 직후 빌드 오류가 표시되며, 뒤이은 빌드 경고에서 패키지를 다시 설치해야 할 수 있음을 알려줍니다. 프로젝트를 업그레이드하는 경우 NuGet은 프로젝트 업그레이드 로그에 오류를 표시합니다.
1. **개발 중에 패키지 다시 설치**: 패키지 작성자는 동작을 테스트하기 위해 개발 중인 패키지와 동일한 버전을 다시 설치해야 하는 경우도 있습니다. `Install-Package` 명령은 강제로 다시 설치하는 옵션을 제공하지 않으므로 `Update-Package -reinstall`을 대신 사용합니다.

## <a name="constraining-upgrade-versions"></a>업그레이드 버전 제한

기본적으로 패키지를 다시 설치하거나 업데이트하는 경우 *항상* 패키지 원본에서 사용 가능한 최신 버전이 설치됩니다.

그러나 `packages.config` 관리 형식을 사용하는 프로젝트에서는 버전 범위를 구체적으로 제한할 수 있습니다. 예를 들어 패키지 API의 주요 변경으로 인해 애플리케이션이 패키지 버전 1.x에서만 작동하고 2.0 이상에서는 작동하지 않는 것으로 알고 있는 경우 업그레이드를 1.x 버전으로 제한하려고 합니다. 이렇게 하면 우발적인 업데이트로 인해 애플리케이션이 중단되는 것을 방지할 수 있습니다.

제한 조건을 설정하려면 텍스트 편집기에서 `packages.config`를 열고, 문제의 종속성을 찾고, 버전 범위가 있는 `allowedVersions` 특성을 추가합니다. 예를 들어 업데이트를 1.x 버전으로 제한하려면 `allowedVersions`를 `[1,2)`로 설정합니다.

```xml
<?xml version="1.0" encoding="utf-8"?>
<packages>
    <package id="ExamplePackage" version="1.1.0" allowedVersions="[1,2)" />

    <!-- ... -->
</packages>
```

모든 경우에 [패키지 버전 관리](../reference/package-versioning.md#version-ranges-and-wildcards)에서 설명한 표기법을 사용하세요.

## <a name="using-update-package"></a>Update-Package 사용

아래에 설명된 [고려 사항](#considerations)에 유념하여 Visual Studio 패키지 관리자 콘솔(**도구** > **NuGet 패키지 관리자** > **패키지 관리자 콘솔**)에서 [Update-Package 명령](../reference/ps-reference/ps-ref-update-package.md)을 통해 모든 패키지를 쉽게 다시 설치할 수 있습니다.

```ps
Update-Package -Id <package_name> –reinstall
```

이 명령을 사용하면 패키지를 제거한 다음 NuGet 갤러리에서 동일한 버전의 동일한 패키지를 찾으려고 하는 것보다 훨씬 쉽습니다. `-Id` 스위치는 선택 사항입니다.

해당되는 경우 `-reinstall`이 없는 동일한 명령으로 패키지를 최신 버전으로 업데이트합니다. 문제의 패키지가 프로젝트에 아직 설치되지 않은 경우 이 명령에서는 오류가 발생합니다. 즉 `Update-Package`에서 패키지를 직접 설치하지 않습니다.

```ps
Update-Package <package_name>
```

기본적으로 `Update-Package`는 솔루션의 모든 패키지에 영향을 줍니다. 작업을 특정 프로젝트로 제한하려면 [솔루션 탐색기]에 표시된 대로 프로젝트 이름을 사용하는 `-ProjectName` 스위치를 사용합니다.

```ps
# Reinstall the package in just MyProject
Update-Package <package_name> -ProjectName MyProject -reinstall
```

프로젝트의 모든 패키지를 *업데이트*(또는 `-reinstall`을 사용하여 다시 설치)하려면 특정 패키지를 지정하지 않은 `-ProjectName`를 사용합니다.

```ps
Update-Package -ProjectName MyProject
```

솔루션의 모든 패키지를 업데이트하려면 다른 인수 또는 스위치 없이 `Update-Package`만 사용합니다. 모든 업데이트를 수행하는 데 상당한 시간이 걸릴 수 있으므로 이 형식은 신중하게 사용해야 합니다.

```ps
# Updates all packages in all projects in the solution
Update-Package 
```

[PackageReference](../Consume-Packages/Package-References-in-Project-Files.md)를 사용하여 프로젝트 또는 솔루션에서 패키지를 업데이트하면 항상 최신 버전의 패키지(시험판 패키지 제외)로 업데이트됩니다. 원하는 경우 [업그레이드 버전 제한](#constraining-upgrade-versions)에서 설명한 대로 `packages.config`를 사용하는 프로젝트에서 업데이트 버전을 제한할 수 있습니다.

명령에 대한 자세한 내용은 [Update-Package](../reference/ps-reference/ps-ref-update-package.md) 참조를 참조하세요.

### <a name="considerations"></a>고려 사항

패키지를 다시 설치할 때 다음과 같은 영향을 받을 수 있습니다.

1. **프로젝트 대상 프레임워크의 대상 변경에 따라 패키지 다시 설치**
    - 간단한 경우에만 `Update-Package –reinstall <package_name>`을 사용하여 패키지를 다시 설치하면 됩니다. 이전 대상 프레임워크에 대해 설치된 패키지가 제거되고, 프로젝트의 현재 대상 프레임워크에 대해 동일한 패키지가 설치됩니다.
    - 경우에 따라 새 대상 프레임워크를 지원하지 않는 패키지가 있을 수 있습니다.
        - 패키지에서 PCL(이식 가능한 클래스 라이브러리)을 지원하고 프로젝트 대상이 해당 패키지에서 더 이상 지원하지 않는 플랫폼의 조합으로 변경된 경우 다시 설치하면 패키지에 대한 참조가 누락됩니다.
        - 이는 직접 사용하는 패키지 또는 종속성으로 설치된 패키지에 대해 발생할 수 있습니다. 해당 종속성이 없는 경우에도 직접 사용하는 패키지에서 새 대상 프레임워크를 지원할 수 있습니다.
        - 애플리케이션을 대상으로 변경한 후 패키지를 다시 설치할 때 빌드 또는 런타임 오류가 발생하는 경우 대상 프레임워크를 되돌리거나 새 대상 프레임워크를 제대로 지원하는 대체 패키지를 검색해야 할 수 있습니다.

1. **프로젝트 대상 변경 또는 프로젝트 업그레이드 후 requireReinstallation 특성이 packages.config에 추가됨**
    - NuGet은 프로젝트 대상을 변경하거나 프로젝트를 업그레이드함으로써 패키지에서 영향을 받았다고 감지하면 `packages.config`의 `requireReinstallation="true"` 특성을 영향을 받은 모든 패키지 참조에 추가합니다. 이로 인해 Visual Studio의 각 후속 빌드에서 다시 설치해야 한다는 것을 기억할 수 있도록 해당 패키지에 대한 빌드 경고를 발생시킵니다.

1. **종속성이 있는 패키지 다시 설치**
    - `Update-Package –reinstall`은 동일한 버전의 원래 패키지를 다시 설치하지만, 특정 버전 제한 조건이 제공되지 않는 한 최신 버전의 종속성을 설치합니다. 이렇게 하면 문제를 해결하는 데 필요한 종속성만 업데이트할 수 있습니다. 그러나 종속성을 이전 버전으로 롤백하는 경우 종속 패키지에 영향을 주지 않고 `Update-Package <dependency_name>`을 사용하여 해당 종속성을 다시 설치할 수 있습니다.
    - `Update-Package –reinstall <packageName> -ignoreDependencies`는 동일한 버전의 원래 패키지를 다시 설치하지만, 종속성은 다시 설치하지 않습니다. 패키지 종속성을 업데이트하면 상태가 손상될 수 있는 경우에 이 명령을 사용합니다.

1. **종속 버전이 포함된 경우 패키지 다시 설치**
    - 위에서 설명한 대로 패키지를 다시 설치해도 설치된 다른 패키지의 버전은 변경되지 않습니다. 따라서 종속성을 다시 설치하면 종속성 패키지가 손상될 수 있습니다.
