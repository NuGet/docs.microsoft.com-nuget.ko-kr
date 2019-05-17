---
title: NuGet 패키지의 시험판 버전
description: 시험판 패키지를 빌드하기 위한 지침
author: karann-msft
ms.author: karann
ms.date: 08/14/2017
ms.topic: conceptual
ms.openlocfilehash: 845f0ea84bcb92fedf9e5f4fb2b1deee1462a004
ms.sourcegitcommit: 4ea46498aee386b4f592b5ebba4af7f9092ac607
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 05/14/2019
ms.locfileid: "65610488"
---
# <a name="building-pre-release-packages"></a>시험판 패키지 빌드

새 버전 번호를 포함하는 업데이트된 패키지를 릴리스할 때마다 NuGet은 해당 패키지를 Visual Studio 내의 패키지 관리자 UI에 표시된 "안정적인 최신 릴리스"로 간주합니다.

![안정적인 최신 릴리스를 보여주는 패키지 관리자 UI](media/Prerelease_01-LatestStable.png)

안정적인 릴리스란 프로덕션 환경에서 사용할 수 있을 만큼 안정적인 릴리스입니다. 안정적인 최신 릴리스는 패키지를 업데이트하거나 복원하는 동안 설치됩니다([패키지 다시 설치 및 업데이트](../consume-packages/reinstalling-and-updating-packages.md)에 설명된 대로 제약 조건 적용).

소프트웨어 릴리스 주기를 지원하기 위해 NuGet 1.6 이상을 사용하면 시험판 패키지의 배포에 허용됩니다. 여기서 버전 번호에는 `-alpha`, `-beta` 또는 `-rc`와 같은 유의적 버전 접미사가 포함됩니다. 자세한 내용은 [패키지 버전 관리](../reference/package-versioning.md#pre-release-versions)를 참조하세요.

다음 방법 중 하나를 사용하여 이러한 버전을 지정할 수 있습니다.

- **프로젝트에서 사용 하는 경우 [ `PackageReference` ](../consume-packages/package-references-in-project-files.md)** : 의미 체계 버전 접미사가 포함된 `.csproj` 파일의 [ `PackageVersion` ](/dotnet/core/tools/csproj.md#packageversion) 요소:

    ```xml
    <PropertyGroup>
        <PackageVersion>1.0.1-alpha</PackageVersion>
    </PropertyGroup>
    ```

- **프로젝트에 [ `packages.config` ](../reference/packages-config.md) 파일이 있는 경우**: 의미 체계 버전 접미사가 포함된 [ `.nuspec` ](../reference/nuspec.md) 파일의 [ `version` ](../reference/nuspec.md#version) 요소:

    ```xml
    <version>1.0.1-alpha</version>
    ```

안정적인 버전을 출시할 준비가 되면 접미사를 제거합니다. 그러면 패키지가 시험판 버전보다 우선 적용됩니다. 다시 [패키지 버전 관리](../reference/package-versioning.md#pre-release-versions)를 참조하세요.

## <a name="installing-and-updating-pre-release-packages"></a>시험판 패키지 설치 및 업데이트

기본적으로 NuGet은 패키지에서 작업할 때 시험판 버전을 포함하지 않지만 다음과 같이 이 동작을 변경할 수 있습니다.

- **패키지 관리자 UI(Visual Studio)**: **NuGet 패키지 관리** UI에서 **시험판 포함** 확인란을 선택합니다.

    ![Visual Studio의 시험판 포함 확인란](media/Prerelease_02-CheckPrerelease.png)

    이 확인란을 설정 또는 해제하면 패키지 관리자 UI 및 설치할 수 있는 사용 가능한 버전 목록을 새로 고칩니다.

- **패키지 관리자 콘솔**: `Find-Package`, `Get-Package`, `Install-Package`, `Sync-Package` 및 `Update-Package` 명령과 함께 `-IncludePrerelease` 스위치를 사용합니다. [PowerShell 참조](../tools/powershell-reference.md)를 참조하세요.

- **NuGet CLI**: `install`, `update`, `delete` 및 `mirror` 명령과 함께 `-prerelease` 스위치를 사용합니다. [NuGet CLI 참조](../tools/nuget-exe-cli-reference.md)를 참조하세요.

## <a name="semantic-versioning"></a>유의적 버전

[유의적 버전 또는 SemVer 규칙](http://semver.org/spec/v1.0.0.html)은 버전 번호의 문자열을 활용하여 기본 코드의 의미를 전달하는 방법을 설명합니다.

이 규칙에서 각 버전에는 다음과 같은 의미를 포함한 세 부분인 `Major.Minor.Patch`가 있습니다.

- `Major`: 호환성이 손상되는 변경
- `Minor`: 이전 버전과 호환되는 새로운 기능
- `Patch`: 이전 버전과 호환되는 버그 수정에만 해당

시험판 버전은 패치 번호 뒤에 하이픈과 문자열을 추가하여 표시됩니다. 엄밀히 말하면 하이픈 뒤에 ‘아무 문자열이나’ 사용할 수 있으며 NuGet은 패키지를 시험판으로 처리합니다. 그런 다음 NuGet은 해당 UI에 전체 버전 번호를 표시하여 소비자가 스스로 의미를 해석하도록 합니다.

이 점을 고려하여 일반적으로 다음과 같이 인식된 명명 규칙을 따르는 것이 좋습니다.

- `-alpha`: 일반적으로 개발 중 및 실험에 사용되는 알파 릴리스
- `-beta`: 일반적으로 다음에 계획된 릴리스에 대한 기능 완료인 베타 릴리스이지만 알려진 버그를 포함할 수 있습니다.
- `-rc`: 일반적으로 심각한 버그가 발생하지 않는 한 잠재적으로 최종적(안정적)인 릴리스인 릴리스 후보입니다.

> [!Note]
> NuGet 4.3.0+는 `1.0.1-build.23`과 마찬가지로 점 표기법을 사용하는 시험판 번호를 지원하는 [유의적 버전 v2.0.0](http://semver.org/spec/v2.0.0.html)을 지원합니다. NuGet 4.3.0 이전 버전에서는 점 표기법이 지원되지 않습니다. 이전 버전의 NuGet에서는 `1.0.1-build23` 같은 양식을 사용할 수 있지만 이는 항상 시험판 버전으로 간주됩니다.

그러나 어떤 접미사를 사용하든지 NuGet은 알파벳 역순으로 우선 순위를 적용합니다.

    1.0.1
    1.0.1-zzz
    1.0.1-rc
    1.0.1-open
    1.0.1-beta12
    1.0.1-beta05
    1.0.1-beta
    1.0.1-alpha2
    1.0.1-alpha

표시된 대로 접미사가 없는 버전은 항상 시험판 버전보다 우선합니다. 또한 두 자리 숫자(이상)를 사용할 수 있는 시험판 태그에서 숫자 접미사를 사용하는 경우 앞에 오는 숫자 0(예: beta01 및 beta05)을 사용하여 숫자가 커지는 경우 올바르게 정렬하도록 합니다.
