---
title: Package.config에서 PackageReference 형식으로 마이그레이션
description: NuGet 4.0 이상 및 VS2017 및.NET Core 2.0에서 지 원하는 대로 PackageReference를 package.config 관리 형식에서 프로젝트를 마이그레이션하는 방법에 대 한 세부 정보
author: karann-msft
ms.author: karann
manager: unnir
ms.date: 03/27/2018
ms.topic: conceptual
ms.openlocfilehash: e0a4363a2807874ec8e2693c5b1c1a0eb2e8af0e
ms.sourcegitcommit: 2a6d200012cdb4cbf5ab1264f12fecf9ae12d769
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 06/06/2018
ms.locfileid: "34818788"
---
# <a name="migrate-from-packagesconfig-to-packagereference"></a>Packages.config에서 PackageReference로 마이그레이션

Visual Studio 2017 버전 15.7 미리 보기 3 및 이상에서는에서 프로젝트를 마이그레이션하는 [packages.config](./packages-config.md) 관리 형식에는 [PackageReference](../consume-packages/Package-References-in-Project-Files.md) 형식입니다.

## <a name="benefits-of-using-packagereference"></a>PackageReference 사용의 이점

* **한 곳에서 모든 프로젝트 종속성을 관리**: 프로젝트 간 참조 및 어셈블리 참조와 마찬가지로 NuGet 패키지에서 참조 (사용 하는 `PackageReference` 노드) 프로젝트 파일 내에서 직접 관리 되는 별도 사용 하 여 보다는 packages.config 파일입니다.
* **깔끔하게 보기의 최상위 종속성**: PackageReference 달리 packages.config을 직접 프로젝트에 설치 된 NuGet 패키지만 나열 합니다. 결과적으로, 하위 종속성이 NuGet 패키지 관리자 UI 및 프로젝트 파일 복잡 되지 않습니다.
* **성능 향상**: PackageReference를 사용 하 여 패키지에서 유지 되므로 *전역 패키지* 폴더 (에 설명 된 대로 [전역 패키지 및 캐시 폴더 관리](../consume-packages/managing-the-global-packages-and-cache-folders.md) 대신는 `packages` 솔루션 내에서 폴더입니다. 결과적으로, PackageReference는 더 빠르게 수행 하 고 더 적은 디스크 공간만 사용 합니다.
* **콘텐츠 흐름 및 종속성에 대 한 제어를 미세**: MSBuild의 기존 기능을 사용 하면를 [NuGet 패키지를 참조 하는 조건에 따라](../consume-packages/Package-References-in-Project-Files.md#adding-a-packagereference-condition) 대상 프레임 워크 당 패키지 참조를 선택 하 고 구성, 플랫폼 또는 다른 피벗 합니다.
* **현재 개발 중 PackageReference**: 참조 [PackageReference GitHub에 대 한 문제](https://aka.ms/nuget-pr-improvements)합니다. packages.config를 더 이상 현재 개발에 포함.

### <a name="limitations"></a>제한 사항

* Visual Studio 2015에서 사용할 수 있는 및 이전 NuGet PackageReference 하지 않습니다. Visual Studio 2017 에서만에서 마이그레이션된 프로젝트를 열 수 있습니다.
* 마이그레이션에 c + + 및 ASP.NET 프로젝트에 대 한 현재 사용할 수 없는 경우
* 일부 패키지는 PackageReference 완벽 하 게 호환 일 수 없습니다. 자세한 내용은 참조 [패키지 호환성 문제](#package-compatibility-issues)합니다.

### <a name="known-issues"></a>알려진 문제

1. `Migrate packages.config to PackageReference...` 옵션을 오른쪽 클릭 상황에 맞는 메뉴에서 사용할 수 없습니다. 

#### <a name="issue"></a>문제 
 
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
> Visual Studio 수 있도록 프로젝트의 백업을 만듭니다 마이그레이션을 시작 하기 전에 [롤백 packages.config](#how-to-roll-back-to-packagesconfig) 필요한 경우.

1. 사용 하 여 프로젝트를 포함 하는 솔루션을 열고 `packages.config`합니다.

1. **솔루션 탐색기**를 마우스 오른쪽 단추로 클릭는 **참조** 노드 또는 `packages.config` 파일을 선택 **packages.config PackageReference로 마이그레이션 중...** .

1. migrator 프로젝트의 NuGet 패키지 참조를 분석 하 고 분류로을 **최상위 종속성** (NuGet 패키지를 해당 설치 디렉터리) 및 **전이 종속성**(최상위 패키지의 종속성으로 설치 된 패키지).

   > [!Note]
   > PackageReference 전이적 패키지 복원이 지원 하 고 종속성을 동적으로 확인 하 여 전이 종속성 필요를 설치 하지 않도록 명시적으로 의미 합니다.

1. (선택 사항) 선택 하 여 최상위 종속성으로 전이적 종속성으로 분류 하는 NuGet 패키지를 처리 하도록 선택할 수 있습니다는 **최상위** 패키지에 대 한 옵션입니다. 이 옵션은 전이적으로 전달 하지 않는 자산을 포함 하는 패키지에 대 한 자동으로 설정 됩니다 (에 `build`, `buildCrossTargeting`, `contentFiles`, 또는 `analyzers` 폴더) 및 개발 종속성으로 표시 된 것 (`developmentDependency = "true"`).

1. 모든 검토 [패키지 호환성 문제](#package-compatibility-issues)합니다.

1. 선택 **확인** 마이그레이션을 시작 하려면.

1. 백업, 설치 된 패키지 (최상위 종속성) 목록, 전이적 종속성으로 참조 패키지 목록 및 시작 될 때 식별 하는 호환성 문제 목록은에 Visual Studio 제공 경로 사용 하 여 보고서 마이그레이션 후에 마이그레이션입니다. 보고서는 백업 폴더에 저장 됩니다.

1. 솔루션 빌드 및 실행 되는지 확인 합니다. 문제가 발생 하는 경우 [GitHub에서 문제를 제출](https://github.com/NuGet/Home/issues/)합니다.

## <a name="how-to-roll-back-to-packagesconfig"></a>Packages.config를 롤백해야 하는 방법

1. 마이그레이션된 프로젝트를 닫습니다.

1. 프로젝트 파일을 복사 하 고 `packages.config` 백업에서 (일반적으로 `<solution_root>\MigrationBackup\<unique_guid>\<project_name>\`) 프로젝트 폴더에 있습니다. 프로젝트 루트 디렉터리에 있는 경우 obj 폴더를 삭제 합니다.

1. 프로젝트를 엽니다.

1. 사용 하 여 패키지 관리자 콘솔을 열고는 **도구 > NuGet 패키지 관리자 > 패키지 관리자 콘솔** 메뉴 명령입니다.

1. 콘솔에서 다음 명령을 실행 합니다.

   ```ps
   update-package -reinstall
   ```

## <a name="package-compatibility-issues"></a>패키지 호환성 문제

Packages.config에서 지원 되 던 일부 측면 PackageReference에서 지원 되지 않습니다. migrator를 분석 하 고 이러한 문제를 검색 합니다. 다음 문제 중 하나 이상을 포함 하는 모든 패키지 마이그레이션 후 예상 대로 동작 하지 않을 수 있습니다.

### <a name="installps1-scripts-are-ignored-when-the-package-is-installed-after-the-migration"></a>마이그레이션 후 패키지를 설치할 때 "install.ps1" 스크립트가 무시 됩니다.

| | |
| --- | --- |
| **설명** | PackageReference와 install.ps1 / uninstall.ps1 PowerShell 스크립트는 설치 하거나 패키지를 제거 하는 동안 실행 되지 않습니다. |
| **잠재적인 영향** | 대상 프로젝트에 몇 가지 동작을 구성 하는 이러한 스크립트에 종속 된 패키지 예상 대로 작동 하지 않을 수 있습니다. |

### <a name="content-assets-are-not-available-when-the-package-is-installed-after-the-migration"></a>마이그레이션 후 패키지를 설치할 때 "콘텐츠" 자산 사용할 수 없는

| | |
| --- | --- |
| **설명** | 패키지의 자산 `content` 폴더 PackageReference와 지원 되지 않으며 무시 됩니다. 에 대 한 지원을 추가 하는 PackageReference `contentFiles` 더 잘 전이적 지원 및 공유 콘텐츠입니다.  |
| **잠재적인 영향** | 자산에 `content` 복사 되지 않습니다 프로젝트와 프로젝트에 이러한 자산의 존재 여부에 종속 된 코드가 리팩터링 필요 합니다.  |

### <a name="xdt-transforms-are-not-applied-when-the-package-is-installed-after-the-upgrade"></a>업그레이드 후 패키지를 설치 하는 경우 XDT 변환은 적용 되지 않습니다.

| | |
| --- | --- |
| **설명** | PackageReference XDT 변환은 지원 되지 않습니다 및 `.xdt` 설치 하거나 패키지를 제거 하는 경우 파일은 무시 됩니다.   |
| **잠재적인 영향** | XDT 변환에 적용 되지 않은 모든 프로젝트 XML 파일을 사용 하 여 가장 일반적으로 `web.config.install.xdt` 및 `web.config.uninstall.xdt`, 즉, 프로젝트의` web.config` 패키지 설치 하거나 제거 하는 경우 파일이 업데이트 되지 않습니다. |

### <a name="assemblies-in-the-lib-root-are-ignored-when-the-package-is-installed-after-the-migration"></a>Lib 루트의 어셈블리는 마이그레이션 후 패키지를 설치할 때 무시 됩니다.

| | |
| --- | --- |
| **설명** | 루트에 있는 어셈블리와 PackageReference, `lib` 대상 프레임 워크 특정 하위 폴더 제외 하 고 폴더는 무시 됩니다. NuGet에 해당 하는 프로젝트의 대상 프레임 워크 대상 프레임 워크 모니커 (TFM)와 일치 하는 하위 폴더를 찾아 프로젝트에는 일치 하는 어셈블리를 설치 합니다. |
| **잠재적인 영향** | 패키지에 해당 하는 프로젝트의 대상 프레임 워크 대상 프레임 워크 모니커 (TFM)와 일치 하는 하위 폴더를 갖지 않는 전환 된 후 예상 대로 작동 없거나 마이그레이션하는 동안 설치 실패 |

## <a name="found-an-issue-report-it"></a>문제를 찾을 수 있습니까? 이 보고!

마이그레이션 experience와 함께 문제가 발생 실행 하는 경우 다음 문의 [NuGet GitHub 리포지토리에서 문제를 제출](https://github.com/NuGet/Home/issues/)합니다.
