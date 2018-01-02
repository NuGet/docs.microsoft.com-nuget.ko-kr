---
title: "NuGet 패키지 복원 | Microsoft Docs"
author: kraigb
ms.author: kraigb
manager: ghogen
ms.date: 10/24/2017
ms.topic: article
ms.prod: nuget
ms.technology: 
ms.assetid: a7bf21da-86ae-4c2d-8750-04ff53f41967
description: "복원을 사용하지 않도록 설정하고 버전을 제한하는 방법을 포함하여 NuGet에서 프로젝트가 종속된 패키지를 복원하는 방법을 설명합니다."
keywords: "NuGet 패키지 복원, NuGet 패키지 설치, 패키지 설치, 패키지 복원, 종속성 버전, 자동 복원 사용 해제, 패키지 버전 제한"
ms.reviewer:
- karann-msft
- unniravindranathan
ms.openlocfilehash: c2567f45b6bb36cdd94c4ce6f1418cb1c7ceac5e
ms.sourcegitcommit: d0ba99bfe019b779b75731bafdca8a37e35ef0d9
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 12/14/2017
---
# <a name="package-restore"></a>패키지 복원

더 깨끗한 개발 환경을 촉진하고 리포지토리 크기를 줄이기 위해 NuGet **패키지 복원**은 프로젝트가 빌드되기 전에 참조된 모든 패키지를 설치합니다. 널리 사용되는 이 기능은 패키지를 원본 제어에 저장하지 않고도 프로젝트에서 모든 종속성을 사용할 수 있게 합니다(패키지 이진 파일을 제외하도록 리포지토리를 구성하는 방법은 [패키지 및 원본 제어](../consume-packages/packages-and-source-control.md) 참조).

항목 내용:
- [패키지 복원에 대한 빠른 지침](#quick-guide-to-package-restore)
- [패키지 복원 개요](#package-restore-overview)
- [패키지 복원 사용 설정/해제](#enabling-and-disabling-package-restore)
- [복원을 사용하여 패키지 버전 제한](#constraining-package-versions-with-restore)
- [명령줄 복원](#command-line-restore)(모든 NuGet 버전)
- [Visual Studio에서 자동 복원](#automatic-restore-in-visual-studio)(NuGet 2.7 이상)
- [Visual Studio에서 MSBuild 통합 복원](#msbuild-integrated-restore)(NuGet 2.6 및 이전 버전)
- [Team Foundation 빌드를 사용하여 패키지 복원](#package-restore-with-team-foundation-build)

복원 동작은 버전에 따라 다릅니다. NuGet 버전을 확인하려면 명령줄에서 `nuget.exe`를 실행하여 첫 번째 출력 줄을 살펴보기만 하면 됩니다.

빌드 서버의 패키지 복원에 대한 자세한 내용은 [TFBuild를 사용하여 패키지 복원](../consume-packages/team-foundation-build.md)을 참조하세요.

> [!Note]
> 패키지 복원에 대해 구성된 프로젝트는 Mono의 xbuild에서도 작동합니다.

## <a name="quick-guide-to-package-restore"></a>패키지 복원에 대한 빠른 지침

[!INCLUDE[package-restore](../includes/package-restore.md)]

> [!Note]
> "이 프로젝트는 이 컴퓨터에 없는 NuGet 패키지를 참조합니다." 또는 "하나 이상의 NuGet 패키지를 복원해야 하지만 동의하지 않아 복원할 수 없습니다."라는 오류 메시지가 표시되면 [패키지 복원 사용 설정/해제](#enabling-and-disabling-package-restore)의 지침에 따라 자동 복원을 설정하세요.

## <a name="package-restore-overview"></a>패키지 복원 개요

먼저, 패키지 참조는 프로젝트 형식 및 NuGet 버전에 따라 다음 패키지 관리 형식 중 하나로 유지됩니다. (NuGet 4 및 MSBuild 15.1은 Visual Studio 2017과 함께 설치됩니다.)

| 메서드 | NuGet 버전 | 설명 | 
| --- | --- | --- |
| `packages.config` | 2.x 이상 | 종속성의 완전한 전체 집합을 나열합니다. `packages.config`에 추가된 Packages도 프로젝트 파일에 추가해야 하며, Targets 및 Props도 프로젝트 파일에 추가해야 합니다. 이는 모든 NuGet 버전에 대한 기준 메서드이지만 다른 옵션에 비해 성능이 떨어집니다. [packages.config 스키마](../schema/packages-config.md)를 참조하세요. | 
| `project.json` | 3.x 이상 | UWP 프로젝트에서는 기본적으로 사용되지만, 프로젝트는 `packages.config`에서 변환할 수 있습니다. `project.json`은 최상위 종속성만 나열합니다. References, Targets 및 Props는 빌드하는 동안 프로젝트에 동적으로 추가되며, 이에 따라 `packages.config`에 비해 성능이 향상됩니다. [project.json 스키마](../schema/project-json.md)를 참조하세요.|
| PackageReference | 4.x 이상 | `<PackageReference>` 노드의 프로젝트 파일에 `<Reference>` 및 `<ProjectReference>`와 함께 종속성을 직접 나열합니다. `project.json`과 비슷하게 작동합니다. [프로젝트 파일의 패키지 참조](../Consume-Packages/Package-References-in-Project-Files.md)를 참조하세요. |

다음으로, 다양한 방법으로 참조 목록을 사용하여 복원을 시작합니다.

명령줄 또는 [패키지 관리자 콘솔](../tools/Package-Manager-Console.md)에서 다음 명령을 사용합니다.

| 명령 | 적용 가능한 시나리오 |
| --- | --- | 
| `nuget restore` | 모든 NuGet 버전 및 모든 참조 형식에 적용됩니다. 아래의 [명령줄 복원](#command-line-restore)을 참조하세요. | 
| `dotnet restore` | .NET Core 프로젝트에 대한 `nuget restore`와 동일합니다. [dotnet restore](https://docs.microsoft.com/dotnet/articles/core/tools/dotnet-restore)를 참조하세요. |
| `msbuild /t:restore` | [프로젝트 파일의 패키지 참조](../Consume-Packages/Package-References-in-Project-Files.md)만 있는 Nuget 4.x 이상 및 MSBuild 15.1 이상에 적용됩니다. `nuget restore` 및 `dotnet restore`는 모두 해당 프로젝트에 대해 이 명령을 사용합니다. [MSBuild 대상으로서의 NuGet pack 및 restore - restore 대상](../schema/msbuild-targets.md#restore-target)을 참조하세요.|

Visual Studio 자체에서도 다른 시간에 패키지를 복원합니다.

| 형식 | 복원이 수행되는 시간 |
| --- | --- |
| 템플릿 복원 | 새 프로젝트를 만드는 동안(일부 템플릿이 외부 패키지에 종속되기 때문) |
| 빌드 복원 | 빌드의 첫 번째 단계로 수행 |
| 솔루션 복원 | 사용자가 솔루션을 마우스 오른쪽 단추로 클릭하고 **NuGet 패키지 복원**을 선택할 때 |
| 프로젝트 변경 시 복원 | *(NuGet 4.x만 해당)* .NET Core SDK 기반 프로젝트를 사용할 때(프로젝트 상태를 변경할 때 포함) |

## <a name="enabling-and-disabling-package-restore"></a>패키지 복원 사용 설정/해제

패키지 복원은 주로 Visual Studio에서 **도구 > 옵션 > NuGet 패키지 관리자**를 통해 사용하도록 설정됩니다.

![NuGet 패키지 관리자 옵션을 통한 패키지 복원 동작 제어](media/Restore-01-AutoRestoreOptions.png)

- **NuGet이 누락된 패키지를 다운로드하도록 허용**: `%AppData%\NuGet\NuGet.Config` 파일의 `packageRestore/enabled` 설정을 아래와 같이 변경하여 모든 형태의 패키지 복원을 제어합니다.

    ```xml
    <configuration>
        <packageRestore>
            <!-- The 'enabled' key is True when the "Allow NuGet to download missing packages" checkbox is set.
                 Clearing the box sets this to False, disabling command-line, automatic, and MSBuild-Integrated restore. -->
            <add key="enabled" value="True" />
        </packageRestore>
    </configuration>
    ```
    <br/>
    > [!Note]
    >  Visual Studio를 시작하거나 빌드를 시작하기 전에 **EnableNuGetPackageRestore**이라는 환경 변수를 TRUE 또는 FALSE 값으로 설정하여 `packageRestore/enabled` 설정을 전역으로 재정의할 수 있습니다.
    

- **Visual Studio에서 빌드 시 누락된 패키지를 자동으로 확인**: `%AppData%\NuGet\NuGet.Config` 파일의 `packageRestore/automatic` 설정을 아래와 같이 변경하여 NuGet 2.7 이상에 대한 자동 복원을 제어합니다.
            
    ```xml
    ...
    <configuration>
        <packageRestore>
            <!-- The 'automatic' key is set to True when the "Automatically check for missing packages during
                 build in Visual Studio" checkbox is set. Clearing the box sets this to False and disables
                 automatic restore. -->
            <add key="automatic" value="True" />
        </packageRestore>
    </configuration>
    ```

해당 참조는 [NuGet.Config 파일 - packageRestore 섹션](../Schema/nuget-config-file.md#packagerestore-section)을 참조하세요.

경우에 따라 개발자 또는 회사에서 모든 사용자에 대해 기본적으로 컴퓨터에서 패키지 복원을 사용하거나 사용하지 않도록 설정할 수도 있습니다. 이렇게 하려면 위의 동일한 설정을 `%ProgramData%\NuGet\Config[\{IDE}[\{Version}[\{SKU}]]]`에 있는 전역 NuGet 구성 파일에 추가하면 됩니다. 개별 사용자는 프로젝트 수준에서 필요에 따라 선택적으로 복원을 사용하도록 설정할 수 있습니다. NuGet에서 여러 config 파일의 우선 순위를 정확히 지정하는 방법에 대한 자세한 내용은 [NuGet 동작 구성](../consume-packages/configuring-nuget-behavior.md#how-settings-are-applied)을 참조하세요.

## <a name="constraining-package-versions-with-restore"></a>복원을 사용하여 패키지 버전 제한

어떤 방법으로든 NuGet에서 패키지를 복원하는 경우 `packages.config`, `project.json` 또는 프로젝트 파일에 지정된 제약 조건을 적용합니다.

- `packages.config`: 종속성의 `allowedVersion` 속성에서 버전 범위를 지정합니다. [패키지 다시 설치 및 업데이트](../consume-packages/reinstalling-and-updating-packages.md#constraining-upgrade-versions)를 참조하세요. 예:

    ```xml
    <package id="Newtonsoft.json" version="6.0.4" allowedVersions="[6,7)" />
    ```

- `project.json`: 종속성의 버전 번호를 사용하여 버전 범위를 직접 지정합니다. 예:

    ```json
    "Newtonsoft.json": "[6, 7)"
    ```

- 프로젝트 파일의 패키지 참조: 종속성의 버전 번호를 사용하여 버전 범위를 직접 지정합니다. 예:
 
    ```xml
    <PackageReference Include="Newtonsoft.json" Version="[6, 7)" />  
    ```

모든 경우에 [패키지 버전 관리](../reference/package-versioning.md)에서 설명한 표기법을 사용하세요.

## <a name="command-line-restore"></a>명령줄 복원

NuGet 2.7 이상의 경우 [Restore](../tools/cli-ref-restore.md) 명령을 사용하여 솔루션의 모든 패키지를 복원합니다(`packages.config`, `project.json` 또는 프로젝트 파일의 패키지 참조를 사용하는지 여부에 관계없이). 지정된 프로젝트 폴더(예: `c:\proj\app`)의 경우 아래의 일반적인 변형 각각에서 패키지를 복원합니다.

```
c:\proj\app\> nuget restore
c:\proj\app\> nuget.exe restore app.sln
c:\proj\> nuget restore app
```

또한 NuGet 4.0 이상 및 MSBuild 15.1 이상의 경우 [MSBuild 대상으로서의 NuGet pack 및 restore](../schema/msbuild-targets.md)에서 설명한 대로 `MSBuild /t:restore`를 사용할 수 있습니다.

## <a name="build-time-restore-in-visual-studio"></a>Visual Studio에서 빌드 시간 복원

Visual Studio는 기본적으로 빌드를 시작할 때 누락된 패키지를 자동으로 복원합니다. 이 동작은 **도구 > 옵션 > NuGet 패키지 관리자 > 일반 > Visual Studio에서 빌드 시 누락된 패키지를 자동으로 확인**을 선택 취소하여 변경할 수 있습니다.

사용하도록 설정되는 경우 자동 복원은 다음과 같이 작동합니다.

1. 빌드가 시작되면 Visual Studio에서 패키지를 복원하도록 NuGet에 지시합니다.
1. NuGet은 재귀적으로 솔루션의 모든 `packages.config` 파일을 찾거나, `project.json`를 찾거나, 프로젝트 파일을 찾습니다.
1. 참조 파일에 나열된 각 패키지에 대해 NuGet은 이미 솔루션에 있는지 확인합니다(프로젝트에서 `packages.config`, `project.json` 또는 프로젝트 파일의 패키지 참조를 사용하는지 여부에 따라 `packages` 폴더, `project.lock.json` 또는 `project.assets.json`).
1. 패키지가 없으면 NuGet은 먼저 캐시에서 해당 패키지를 검색하려고 합니다([NuGet 캐시 관리](../consume-packages/managing-the-nuget-cache.md) 참조). 패키지가 캐시에 없으면 NuGet은 **도구 > 옵션 > NuGet 패키지 관리자 > 패키지 원본**에서 나열한 대로 활성화된 원본에서 표시된 순서대로 해당 패키지를 다운로드하려고 합니다. 이 경우 모든 원본을 확인한 후에 NuGet에서 패키지를 찾지 못했음을 나타내며, 목록의 마지막 원본에 대한 실패만 보고합니다. 이러한 오류는 해당 원본에 대한 오류가 개별적으로 표시되지 않았더라도 패키지가 다른 원본에 존재하지 않음을 함축적으로 의미합니다.
1. 다운로드가 성공하면 NuGet에서 패키지를 캐시하고 솔루션(즉 `packages` 폴더, `project.lock.json` 또는 `project.assets.json`)에 설치합니다. 그렇지 않으면 NuGet이 실패하고 빌드도 실패합니다.

이 프로세스에는 패키지 복원을 취소하는 옵션이 있는 진행률 대화 상자가 표시됩니다.

## <a name="package-restore-with-team-foundation-build"></a>Team Foundation 빌드를 사용하여 패키지 복원

패키지 복원은 TFS(Team Foundation Server) 및 Visual Studio Team Services(여기서 다루지 않는 다른 빌드 시스템도 포함)와 마찬가지로 빌드 서버에서 프로젝트를 빌드할 때 주로 사용됩니다.

### <a name="visual-studio-team-services"></a>Visual Studio Team Services

Team Services에서 빌드 정의를 만들 때 빌드 작업 이전에 NuGet 패키지 복원 작업을 정의에 포함하기만 하면 됩니다. 이 작업은 여러 빌드 템플릿에 기본적으로 포함되어 있습니다.

![Visual Studio Team Service 빌드 정의의 NuGet 패키지 복원 작업](media/Restore-02-VSTSBuild.png)

### <a name="team-foundation-server"></a>Team Foundation Server

Team Foundation Server 2013 이상용 팀 빌드 템플릿을 사용하는 경우, TFS 2013 이상에서는 기본적으로 빌드하는 동안 패키지가 자동으로 복원됩니다.

또한 이전 버전의 빌드 템플릿(예: 이전 버전의 TFS에서 마이그레이션한 프로젝트)을 사용하는 경우, 해당 빌드 템플릿을 TFS 2013으로 마이그레이션해야 합니다. 즉 기본적으로 원본 제어(TFVC 또는 Git)에 적합한 템플릿을 사용하여 빌드 템플릿의 사용자 지정 부분을 다시 만드는 것입니다.

이전 버전의 TFS에서는 앞에서 설명한 대로 [명령줄 복원](#command-line-restore)을 호출하는 빌드 단계를 포함하기만 하면 됩니다.

자세한 내용은 [Team Foundation 빌드를 사용하여 패키지 복원 연습](../consume-packages/team-foundation-build.md)을 참조하세요.    
