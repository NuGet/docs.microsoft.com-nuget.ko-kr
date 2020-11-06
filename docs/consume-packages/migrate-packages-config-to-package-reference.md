---
title: packages.config에서 PackageReference 형식으로 마이그레이션
description: 프로젝트를 packages.config 관리 형식에서 NuGet 4.0 이상, VS2017, .NET Core 2.0이 지원하는 PackageReference 형식으로 마이그레이션하는 방법에 대한 세부 정보
author: karann-msft
ms.author: karann
ms.date: 05/24/2019
ms.topic: conceptual
ms.openlocfilehash: 23bd936707173f49a651a8ba432fa8773fa53881
ms.sourcegitcommit: b138bc1d49fbf13b63d975c581a53be4283b7ebf
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 11/03/2020
ms.locfileid: "93237837"
---
# <a name="migrate-from-packagesconfig-to-packagereference"></a>packages.config를 PackageReference로 마이그레이션

Visual Studio 2017 버전 15.7 이상은 프로젝트를 [packages.config](../reference/packages-config.md) 관리 형식에서 [PackageReference](../consume-packages/Package-References-in-Project-Files.md) 형식으로 마이그레이션하도록 지원합니다.

## <a name="benefits-of-using-packagereference"></a>PackageReference 사용 혜택

* **모든 프로젝트 종속성을 한 곳에서 관리** : 프로젝트 간 참조나 어셈블리 참조처럼 NuGet 패키지 참조(`PackageReference` 노드 사용)는 별도의 packages.config 파일을 사용하지 않고 프로젝트 파일 내에서 직접 관리됩니다.
* **최상위 종속성의 정리된 보기** : packages.config와 다르게 PackageReference는 프로젝트에 직접 설치한 NuGet 패키지만 나열합니다. 따라서 NuGet 패키지 관리자 UI 및 프로젝트 파일은 하위 수준 종속성으로 인해 복잡하게 보이지 않습니다.
* **향상된 성능** : PackageReference를 사용하는 경우, 패키지는 솔루션 내 `packages` 폴더에서보다는 *전역 패키지* 폴더( [전역 패키지 및 캐시 폴더 관리](../consume-packages/managing-the-global-packages-and-cache-folders.md)에 대해 설명된 대로)에 유지됩니다. 따라서 PackageReference는 처리 속도가 더 빠르고 디스크 공간을 더 적게 사용합니다.
* **종속성 및 콘텐츠 흐름을 세밀하게 제어** : MSBuild의 기존 기능을 사용하면 [조건부로 NuGet 패키지를 참조](../consume-packages/Package-References-in-Project-Files.md#adding-a-packagereference-condition)하고 대상 프레임워크, 구성, 플랫폼 또는 기타 피벗당 패키지 참조를 선택할 수 있습니다.
* **현재 개발 중인 PackageReference** : [GitHub의 PackageReference 문제](https://aka.ms/nuget-pr-improvements)를 참조하세요. packages.config는 더 이상 활발하게 개발하지 않습니다.

### <a name="limitations"></a>제한 사항

* NuGet PackageReference는 Visual Studio 2015 이하에서 사용할 수 없습니다. 마이그레이션된 프로젝트는 Visual Studio 2017 이상에서만 열 수 있습니다.
* 현재 C++ 및 ASP.NET 프로젝트에는 마이그레이션이 제공되지 않습니다.
* 일부 패키지는 PackageReference와 완전히 호환되지 않을 수 있습니다. 자세한 내용은 [패키지 호환성 문제](#package-compatibility-issues)를 참조하세요.

또한 PackageReferences와 packages.config의 작동 방식에는 몇 가지 차이점이 있습니다. 예를 들어 [업그레이드 버전 제한](../consume-packages/reinstalling-and-updating-packages.md#constraining-upgrade-versions)은 PackageReference에서 지원되지 않지만 [부동 버전](../consume-packages/package-references-in-project-files.md#floating-versions) 지원을 추가합니다.

### <a name="known-issues"></a>알려진 문제

1. `Migrate packages.config to PackageReference...` 옵션을 오른쪽 클릭 상황에 맞는 메뉴에서 사용할 수 없습니다. 

#### <a name="issue"></a>문제점 
 
프로젝트를 처음 열면 NuGet 작업이 수행될 때까지 NuGet을 초기화할 수 없습니다. 이로 인해 마이그레이션 옵션이 `packages.config` 또는 `References`의 오른쪽 클릭 상황에 맞는 메뉴에 표시되지 않습니다. 

#### <a name="workaround"></a>해결 방법 

다음 NuGet 작업 중 하나를 수행합니다. 
* 패키지 관리자 UI 열기 - `References`를 마우스 오른쪽 단추로 클릭하고 `Manage NuGet Packages...`를 선택합니다. 
* 패키지 관리자 콘솔 열기 - `Tools > NuGet Package Manager`에서 `Package Manager Console`을 선택합니다. 
* NuGet 복원 실행 - 솔루션 탐색기에서 솔루션 노드를 마우스 오른쪽 단추로 클릭하고 `Restore NuGet Packages`를 선택합니다. 
* NuGet 복원을 트리거하는 프로젝트 빌드 

이제 마이그레이션 옵션이 표시됩니다. 이 옵션은 지원되지 않으며 ASP.NET 및 C++ 프로젝트 형식에 대해 표시되지 않습니다. 

## <a name="migration-steps"></a>마이그레이션 단계

> [!Note]
> 마이그레이션을 시작하기 전에 Microsoft Visual Studio는 필요한 경우 [packages.config로 롤백](#how-to-roll-back-to-packagesconfig)할 수 있도록 프로젝트의 백업을 만듭니다.

1. `packages.config`를 사용하여 프로젝트가 포함된 솔루션을 엽니다.

1. **솔루션 탐색기** 에서 **참조** 노드 또는 `packages.config` 파일을 마우스 오른쪽 단추로 클릭하고 **packages.config에서 PackageReference로 마이그레이션** 을 선택합니다.

1. 마이그레이터는 프로젝트의 NuGet 패키지 참조를 분석하여 **최상위 종속성** (직접 설치한 NuGet 패키지) 및 **전이적 종속성** (최상위 패키지의 종속성으로 설치된 패키지)으로 분류하려고 시도합니다.

   > [!Note]
   > PackageReference는 전이적 패키지 복원을 지원하고 종속성을 동적으로 확인합니다. 즉, 전이적 종속성을 명시적으로 설치할 필요가 없습니다.

1. (선택 사항) 패키지의 **최상위 레벨** 옵션을 선택함으로써 전이적 종속성으로 분류된 NuGet 패키지를 최상위 종속성으로 선택하여 처리할 수 있습니다. 이 옵션은 전이적으로 이동하지 않는 자산(`build`, `buildCrossTargeting`, `contentFiles` 또는 `analyzers` 폴더의 자산) 및 개발 종속성(`developmentDependency = "true"`)으로 표시된 자산을 포함하는 패키지에 대해 자동으로 설정됩니다.

1. 모든 [패키지 호환성 문제](#package-compatibility-issues)를 검토합니다.

1. **확인** 을 선택하여 마이그레이션을 시작합니다.

1. 마이그레이션이 끝나면 Microsoft Visual Studio는 백업 파일 경로, 설치한 패키지 목록(최상위 종속성), 전이적 종속성으로 참조되는 패키지 목록, 마이그레이션 시작 시 식별되는 호환성 문제 목록이 포함된 보고서를 제공합니다. 보고서는 백업 폴더에 저장됩니다.

1. 솔루션이 빌드되고 실행되는지 확인합니다. 문제가 발생하는 경우, [GitHub에 문제를 보고](https://github.com/NuGet/Home/issues/)하세요.

## <a name="how-to-roll-back-to-packagesconfig"></a>packages.config로 롤백하는 방법

1. 마이그레이션된 프로젝트를 닫습니다.

1. 백업한 프로젝트 파일과 `packages.config`(일반적으로 `<solution_root>\MigrationBackup\<unique_guid>\<project_name>\`에 위치)를 프로젝트 폴더에 복사합니다. obj 폴더가 프로젝트 루트 디렉터리에 있으면 삭제합니다.

1. 프로젝트를 엽니다.

1. **도구 > NuGet 패키지 관리자 > 패키지 관리자 콘솔** 메뉴 명령을 사용하여 패키지 관리자 콘솔을 엽니다.

1. 콘솔에서 다음 명령을 실행합니다.

   ```ps
   update-package -reinstall
   ```

## <a name="create-a-package-after-migration"></a>마이그레이션 후 패키지 만들기

마이그레이션이 완료되면 [nuget.build.tasks.pack](https://www.nuget.org/packages/nuget.build.tasks.pack) NuGet 패키지에 대한 참조를 추가한 다음 [msbuild -t:pack](../reference/msbuild-targets.md#pack-target)을 사용하여 패키지를 만드는 것이 좋습니다. 일부 시나리오에서는 `msbuild -t:pack` 대신 `dotnet.exe pack`을 사용할 수 있지만, 이는 권장하지 않습니다.

## <a name="package-compatibility-issues"></a>패키지 호환성 문제

packages.config에서 지원되던 일부 요소가 PackageReference에서는 지원되지 않습니다. 마이그레이터는 이러한 문제를 분석하고 검색합니다. 다음 중 하나 이상의 문제가 있는 패키지는 마이그레이션 후 예상대로 작동하지 않을 수 있습니다.

### <a name="installps1-scripts-are-ignored-when-the-package-is-installed-after-the-migration"></a>패키지가 마이그레이션 후에 설치되면 "install.ps1" 스크립트가 무시됩니다.

| | |
| --- | --- |
| **설명** | PackageReference를 사용하면 패키지를 설치하거나 제거하는 동안 install.ps1 및 uninstall.ps1 PowerShell 스크립트가 실행되지 않습니다. |
| **잠재적 영향** | 대상 프로젝트에서 일부 동작을 구성하기 위해 이러한 스크립트에 의존하는 패키지가 예상대로 작동하지 않을 수 있습니다. |

### <a name="content-assets-are-not-available-when-the-package-is-installed-after-the-migration"></a>패키지가 마이그레이션 후에 설치되면 "콘텐츠" 자산을 사용할 수 없습니다.

| | |
| --- | --- |
| **설명** | 패키지의 `content` 폴더에 있는 자산은 PackageReference를 통해 지원되지 않으며 무시됩니다. PackageReference는 `contentFiles`에 대한 지원을 추가하여 더 나은 전이적 지원 및 공유 콘텐츠를 제공합니다.  |
| **잠재적 영향** | `content`의 자산은 프로젝트에 복사되지 않고, 이러한 자산의 존재에 영향을 받는 프로젝트 코드에는 리팩터링이 필요합니다.  |

### <a name="xdt-transforms-are-not-applied-when-the-package-is-installed-after-the-upgrade"></a>패키지가 업그레이드 후에 설치되면 XDT 변환이 적용되지 않습니다.

| | |
| --- | --- |
| **설명** | PackageReference는 XDT 변환을 지원하지 않으며 패키지를 설치하거나 제거하는 경우 `.xdt` 파일이 무시됩니다.   |
| **잠재적 영향** | XDT 변환은 모든 프로젝트 XML 파일(가장 일반적으로 `web.config.install.xdt` 및 `web.config.uninstall.xdt`)에 적용되지 않습니다. 즉, 패키지를 설치하거나 제거할 때 프로젝트의 ` web.config` 파일이 업데이트되지 않습니다. |

### <a name="assemblies-in-the-lib-root-are-ignored-when-the-package-is-installed-after-the-migration"></a>패키지가 마이그레이션 후에 설치되면 lib 루트의 어셈블리가 무시됩니다.

| | |
| --- | --- |
| **설명** | PackageReference를 사용하면 대상 프레임워크 특정 하위 폴더가 없는 `lib` 폴더의 루트에 있는 어셈블리가 무시됩니다. NuGet은 프로젝트의 대상 프레임워크에 해당하는 TFM(대상 프레임워크 모니커)과 일치하는 하위 폴더를 찾은 다음, 프로젝트에 일치하는 어셈블리를 설치합니다. |
| **잠재적 영향** | 프로젝트의 대상 프레임워크에 해당하는 TFM(대상 프레임워크 모니커)과 일치하는 하위 폴더가 없는 패키지는 전환 후 예상대로 작동하지 않거나 마이그레이션 도중 설치에 실패할 수 있습니다. |

## <a name="found-an-issue-report-it"></a>문제를 발견했나요? 그렇다면 보고해주세요.

마이그레이션 환경에 문제가 발생하는 경우 [NuGet GitHub 리포지토리에 문제를 보고](https://github.com/NuGet/Home/issues/)하세요.
