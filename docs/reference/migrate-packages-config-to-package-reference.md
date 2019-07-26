---
title: PackageReference 형식으로 마이그레이션
description: NuGet 4.0 + 및 VS2017 및 .NET Core 2.0에서 지원 되는 것 처럼 패키지에서 PackageReference 관리 형식으로 프로젝트를 마이그레이션하는 방법에 대 한 세부 정보
author: karann-msft
ms.author: karann
ms.date: 05/24/2019
ms.topic: conceptual
ms.openlocfilehash: d1c32f4a926f1f688db3ea6a9ca2eed1a21b2dec
ms.sourcegitcommit: f9e39ff9ca19ba4a26e52b8a5e01e18eb0de5387
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/24/2019
ms.locfileid: "68433287"
---
# <a name="migrate-from-packagesconfig-to-packagereference"></a>PackageReference에서로 마이그레이션

Visual Studio 2017 버전 15.7 이상에서는 프로젝트를 PackageReference [관리 형식](./packages-config.md) 에서 [](../consume-packages/Package-References-in-Project-Files.md) 형식으로 마이그레이션하는 것을 지원 합니다.

## <a name="benefits-of-using-packagereference"></a>PackageReference 사용의 이점

* **모든 프로젝트 종속성을 한 곳에서 관리**합니다. 프로젝트 간 참조 및 어셈블리 참조와 마찬가지로, NuGet 패키지 참조 ( `PackageReference` 노드 사용)는 별도의 패키지나 .config 파일을 사용 하는 대신 프로젝트 파일 내에서 직접 관리 됩니다.
* **최상위 종속성의 정리 된 보기**: PackageReference와 달리,는 프로젝트에 직접 설치한 NuGet 패키지만 나열 합니다. 따라서 NuGet 패키지 관리자 UI 및 프로젝트 파일은 하위 수준 종속성으로 복잡 하지 않습니다.
* **성능 향상**: PackageReference를 사용 하는 경우 패키지는 솔루션 내의 `packages` 폴더 대신 [전역 패키지 및 캐시 폴더를 관리](../consume-packages/managing-the-global-packages-and-cache-folders.md) 하는 방법에 설명 된 대로 *전역* 패키지 폴더에 유지 관리 됩니다. 결과적으로 PackageReference는 더 빠르게 수행 되 고 디스크 공간을 더 적게 소비 합니다.
* **종속성 및 콘텐츠 흐름을 세밀 하 게 제어**: MSBuild의 기존 기능을 사용 하면 [조건부로 NuGet 패키지를 참조](../consume-packages/Package-References-in-Project-Files.md#adding-a-packagereference-condition) 하 고 대상 프레임 워크, 구성, 플랫폼 또는 기타 피벗 당 패키지 참조를 선택할 수 있습니다.
* **PackageReference가 활성 개발 중입니다**. [GitHub의 PackageReference 문제를](https://aka.ms/nuget-pr-improvements)참조 하세요. 패키지 .config는 더 이상 활성 개발에 더 이상 적용 되지 않습니다.

### <a name="limitations"></a>제한 사항

* NuGet PackageReference은 Visual Studio 2015 이전 버전에서 사용할 수 없습니다. 마이그레이션된 프로젝트는 Visual Studio 2017 이상 에서만 열 수 있습니다.
* 현재 C++ 및 ASP.NET 프로젝트에는 마이그레이션이 제공되지 않습니다.
* 일부 패키지는 PackageReference와 완전히 호환 되지 않을 수 있습니다. 자세한 내용은 [패키지 호환성 문제](#package-compatibility-issues)를 참조 하세요.

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
> 마이그레이션을 시작 하기 전에 Visual Studio는 필요한 경우 [패키지를 롤백할](#how-to-roll-back-to-packagesconfig) 수 있도록 프로젝트의 백업을 만듭니다.

1. 을 사용 하 여 `packages.config`프로젝트가 포함 된 솔루션을 엽니다.

1. **솔루션 탐색기**에서 **참조** `packages.config` 노드 또는 파일을 마우스 오른쪽 단추로 클릭 하 고 **패키지를 PackageReference로 마이그레이션 ...을**선택 합니다.

1. Migrator는 프로젝트의 NuGet 패키지 참조를 분석 하 고이를 **최상위 종속성** (직접 설치한 NuGet 패키지) 및 **전이적 종속성** (로 설치 된 패키지)으로 분류 하려고 시도 합니다. 최상위 패키지의 종속성).

   > [!Note]
   > PackageReference은 전이적 패키지 복원을 지원 하 고 종속성을 동적으로 확인 합니다. 즉, 전이적 종속성을 명시적으로 설치할 필요가 없습니다.

1. 필드 패키지에 대해 **최상위 수준** 옵션을 선택 하 여 전이적 종속성으로 분류 된 NuGet 패키지를 최상위 종속성으로 처리 하도록 선택할 수 있습니다. 이 옵션은 전이적으로 이동 하지 않는 자산 ( `build` `contentFiles`, `buildCrossTargeting`, 또는 `analyzers` 폴더의 자산) 및 개발 종속성 (`developmentDependency = "true"`)으로 표시 된 자산을 포함 하는 패키지에 대해 자동으로 설정 됩니다.

1. [패키지 호환성 문제](#package-compatibility-issues)를 검토 합니다.

1. **확인** 을 선택 하 여 마이그레이션을 시작 합니다.

1. 마이그레이션이 끝나면 Visual Studio는 백업 경로, 설치 된 패키지 목록 (최상위 종속성), 전이적 종속성으로 참조 되는 패키지 목록, 시작 부분에서 확인 된 호환성 문제 목록 등의 보고서를 제공 합니다. 마이그레이션이나. 보고서는 백업 폴더에 저장 됩니다.

1. 솔루션이 빌드되고 실행 되는지 확인 합니다. 문제가 발생 하는 경우 [GitHub에서 문제를 해결](https://github.com/NuGet/Home/issues/)하세요.

## <a name="how-to-roll-back-to-packagesconfig"></a>패키지 .config로 롤백하는 방법

1. 마이그레이션된 프로젝트를 닫습니다.

1. 프로젝트 파일과 `packages.config` 백업 (일반적으로 `<solution_root>\MigrationBackup\<unique_guid>\<project_name>\`)에서 프로젝트 폴더로 복사 합니다. Obj 폴더가 프로젝트 루트 디렉터리에 있으면 삭제 합니다.

1. 프로젝트를 엽니다.

1. **도구 > NuGet 패키지 관리자 > 패키지 관리자 콘솔** 메뉴 명령을 사용 하 여 패키지 관리자 콘솔을 엽니다.

1. 콘솔에서 다음 명령을 실행 합니다.

   ```ps
   update-package -reinstall
   ```

## <a name="create-a-package-after-migration"></a>마이그레이션 후 패키지 만들기

마이그레이션이 완료 되 면 [nuget.](https://www.nuget.org/packages/nuget.build.tasks.pack) t:pack nuget 패키지에 대 한 참조를 추가 하는 것이 좋으며, 그런 다음 [msbuild](../reference/msbuild-targets.md#pack-target) 를 사용 하 여 패키지를 만듭니다. 대신를 사용 하는 일부 시나리오 `dotnet.exe pack` 에서는 사용 하지 않는 것이 좋습니다. `msbuild -t:pack`

## <a name="package-compatibility-issues"></a>패키지 호환성 문제

PackageReference에서 지원 되 던 일부 측면은 지원 되지 않습니다. Migrator는 이러한 문제를 분석 하 고 검색 합니다. 다음 문제 중 하나 이상이 있는 모든 패키지는 마이그레이션 후 예상 대로 작동 하지 않을 수 있습니다.

### <a name="installps1-scripts-are-ignored-when-the-package-is-installed-after-the-migration"></a>마이그레이션 후 패키지가 설치 되 면 "install. ps1" 스크립트가 무시 됩니다.

| | |
| --- | --- |
| **설명** | PackageReference를 사용 하면 패키지를 설치 하거나 제거 하는 동안. p s 1을 설치 하 고 ps1 PowerShell 스크립트를 실행 하지 않습니다. |
| **잠재적 영향** | 이러한 스크립트를 사용 하 여 대상 프로젝트의 일부 동작을 구성 하는 패키지가 예상 대로 작동 하지 않을 수 있습니다. |

### <a name="content-assets-are-not-available-when-the-package-is-installed-after-the-migration"></a>마이그레이션 후 패키지가 설치 되 면 "콘텐츠" 자산을 사용할 수 없습니다.

| | |
| --- | --- |
| **설명** | 패키지의 `content` 폴더에 있는 자산은 PackageReference에서 지원 되지 않으며 무시 됩니다. PackageReference은에 대 `contentFiles` 한 지원을 추가 하 여 더 나은 전이적 지원 및 공유 콘텐츠를 제공 합니다.  |
| **잠재적 영향** | 의 `content` 자산은 프로젝트에 복사 되지 않고 해당 자산의 존재에 따라 달라 지는 프로젝트 코드에는 리팩터링이 필요 합니다.  |

### <a name="xdt-transforms-are-not-applied-when-the-package-is-installed-after-the-upgrade"></a>업그레이드 후 패키지가 설치 되 면 XDT 변환이 적용 되지 않습니다.

| | |
| --- | --- |
| **설명** | XDT 변환은 PackageReference에서 지원 되지 않으며 패키지 `.xdt` 를 설치 하거나 제거 하는 경우 파일은 무시 됩니다.   |
| **잠재적 영향** | XDT 변환은 프로젝트 XML 파일 (가장 일반적으로 `web.config.install.xdt` `web.config.uninstall.xdt`)에는 적용 되지 않습니다. 즉, 패키지를 설치` web.config` 하거나 제거할 때 프로젝트의 파일이 업데이트 되지 않습니다. |

### <a name="assemblies-in-the-lib-root-are-ignored-when-the-package-is-installed-after-the-migration"></a>마이그레이션 후 패키지가 설치 될 때 lib 루트의 어셈블리는 무시 됩니다.

| | |
| --- | --- |
| **설명** | PackageReference를 사용 하는 경우 대상 프레임 워크 `lib` 특정 하위 폴더가 없는 폴더의 루트에 있는 어셈블리는 무시 됩니다. NuGet은 프로젝트의 대상 프레임 워크에 해당 하는 TFM (대상 프레임 워크 모니커)와 일치 하는 하위 폴더를 찾아 프로젝트에 일치 하는 어셈블리를 설치 합니다. |
| **잠재적 영향** | 프로젝트의 대상 프레임 워크에 해당 하는 TFM (대상 프레임 워크 모니커)와 일치 하는 하위 폴더가 없는 패키지는 마이그레이션 중에 전환 또는 설치 실패 후 예상 대로 작동 하지 않을 수 있습니다. |

## <a name="found-an-issue-report-it"></a>문제가 발견 되었나요? 보고 합니다.

마이그레이션 환경에 문제가 발생 하는 경우 [NuGet GitHub 리포지토리에서 문제](https://github.com/NuGet/Home/issues/)를 해결 하세요.
