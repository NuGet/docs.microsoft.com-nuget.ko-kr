---
title: NuGet 패키지 버전 참조
description: NuGet 패키지가 종속 된 다른 패키지에 대 한 버전 번호 및 범위 지정과 종속성 설치 방법에 대 한 정확한 세부 정보
author: karann-msft
ms.author: karann
ms.date: 03/23/2018
ms.topic: reference
ms.reviewer: anangaur
ms.openlocfilehash: 7c6992d6bf3142eb6aca70f1fa3c46f72efd25a0
ms.sourcegitcommit: fc1b716afda999148eb06d62beedb350643eb346
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/14/2019
ms.locfileid: "69019992"
---
# <a name="package-versioning"></a>패키지 버전 관리

특정 패키지는 항상 패키지 식별자와 정확한 버전 번호를 사용 하는 것으로 간주 됩니다. 예를 들어 nuget.org의 [Entity Framework](https://www.nuget.org/packages/EntityFramework/) 에는 버전 *4.1.10311* 에서 버전 *6.1.3* (안정적인 최신 릴리스) 및 *6.2.0-beta1과 같은 다양 한 시험판 버전까지 사용 가능한 수십 개의 특정 패키지가 있습니다.* .

패키지를 만들 때 선택적 시험판 텍스트 접미사를 사용 하 여 특정 버전 번호를 할당 합니다. 반면 패키지를 사용 하는 경우 정확한 버전 번호 또는 허용 되는 버전 범위를 지정할 수 있습니다.

항목 내용

- 시험판 접미사를 포함 한 [버전 기본 사항](#version-basics) 입니다.
- [버전 범위 및 와일드 카드](#version-ranges-and-wildcards)
- [정규화 된 버전 번호](#normalized-version-numbers)

## <a name="version-basics"></a>버전 기본 사항

특정 버전 번호는 *Major [-Suffix]* 형식으로 되어 있습니다. 여기서 구성 요소의 의미는 다음과 같습니다.

- *주*: 호환성이 손상되는 변경
- *부*: 이전 버전과 호환되는 새로운 기능
- *패치*: 이전 버전과 호환되는 버그 수정에만 해당
- *-접미사* (선택 사항): 하이픈 뒤에 시험판 버전을 나타내는 문자열이 오고 있습니다 ( [의미 체계 버전 관리 또는 SemVer 1.0 규칙](http://semver.org/spec/v1.0.0.html)에 따라).

**예:**

    1.0.1
    6.11.1231
    4.3.1-rc
    2.2.44-beta1

> [!Important]
> nuget.org은 정확한 버전 번호가 없는 패키지 업로드를 거부 합니다. 패키지를 만드는 데 사용 되는 `.nuspec` 또는 프로젝트 파일에 버전을 지정 해야 합니다.

### <a name="pre-release-versions"></a>시험판 버전

기술적으로 말하면 패키지 작성자는 모든 문자열을 접미사로 사용 하 여 시험판 버전을 나타낼 수 있습니다. NuGet은 이러한 버전을 시험판으로 처리 하 고 다른 해석을 수행 하지 않습니다. 즉, NuGet은 관련 된 모든 UI에서 전체 버전 문자열을 표시 하 여 접미사의 의미를 소비자로 해석 합니다.

즉, 패키지 개발자는 일반적으로 인식 되는 명명 규칙을 따릅니다.

- `-alpha`: 일반적으로 진행 중인 작업 및 실험에 사용 되는 알파 릴리스입니다.
- `-beta`: 일반적으로 다음에 계획된 릴리스에 대한 기능 완료인 베타 릴리스이지만 알려진 버그를 포함할 수 있습니다.
- `-rc`: 일반적으로 심각한 버그가 발생하지 않는 한 잠재적으로 최종적(안정적)인 릴리스인 릴리스 후보입니다.

> [!Note]
> NuGet 4.3.0 +는 *1.0.1*에서와 같이 점 표기법이 포함 된 시험판 번호를 지 원하는 [SemVer 2.0.0](http://semver.org/spec/v2.0.0.html)를 지원 합니다. NuGet 4.3.0 이전 버전에서는 점 표기법이 지원되지 않습니다. *1.0.1-build23*와 같은 양식을 사용할 수 있습니다.

패키지 참조를 확인 하는 경우 접미사를 사용 하는 경우에만 다른 패키지 버전을 사용할 수 있습니다. 예를 들어 다음 버전은 표시 된 순서 대로 선택 됩니다.

    1.0.1
    1.0.1-zzz
    1.0.1-rc
    1.0.1-open
    1.0.1-beta
    1.0.1-alpha2
    1.0.1-alpha
    1.0.1-aaa

## <a name="semantic-versioning-200"></a>의미 체계 버전 관리 2.0.0

NuGet 4.3.0 + 및 Visual Studio 2017 버전 15.3 +에서 NuGet은 [의미 체계 버전 관리 2.0.0](http://semver.org/spec/v2.0.0.html)을 지원 합니다.

SemVer v 2.0.0의 특정 의미 체계가 이전 클라이언트에서 지원 되지 않습니다. NuGet은 다음 문 중 하나에 해당 하는 경우 패키지 버전을 SemVer v 2.0.0에 한정 된 것으로 간주 합니다.

- 시험판 레이블은 점으로 구분 됩니다 (예: *1.0.0-alpha. 1).*
- 버전에는 *1.0.0 + githash* 와 같은 빌드 메타 데이터가 있습니다.

Nuget.org의 경우 패키지는 다음 문 중 하나가 true 인 경우 SemVer v 2.0.0 패키지로 정의 됩니다.

- 패키지의 자체 버전은 위에서 정의한 대로 SemVer v 2.0.0 규격 이지만 SemVer v 1.0.0은 호환 되지 않습니다.
- 패키지의 모든 종속성 버전 범위에는 위에서 정의 된 SemVer v 2.0.0 규격 이지만 SemVer v 1.0.0 규격이 아닌 최소 또는 최대 버전이 있습니다. 예를 들면 *[1.0.0-alpha. 1,)* 입니다.

SemVer v 2.0.0 관련 패키지를 nuget.org에 업로드 하는 경우 패키지는 이전 클라이언트에 표시 되지 않으며 다음 NuGet 클라이언트 에서만 사용할 수 있습니다.

- NuGet 4.3.0 +
- Visual Studio 2017 버전 15.3 이상
- [NUGET VSIX v 3.6.0](https://dist.nuget.org/visualstudio-2015-vsix/latest/NuGet.Tools.vsix) 를 사용 하는 Visual Studio 2015
- dotnet
  - dotnetcore (.NET SDK 2.0.0 +)

타사 클라이언트:

- JetBrains Rider
- Paket 버전 5.0 이상

<!-- For compatibility with previous dependency-versions page -->
<a name="version-ranges"></a>

## <a name="version-ranges-and-wildcards"></a>버전 범위 및 와일드 카드

패키지 종속성을 참조할 때 NuGet은 다음과 같이 요약 된 버전 범위를 지정 하기 위한 간격 표기법 사용을 지원 합니다.

| Notation | 적용 된 규칙 | Description |
|----------|--------------|-------------|
| 1.0 | x ≥ 1.0 | 최소 버전 (포함) |
| (1.0,) | x > 1.0 | 최소 버전, 제외 |
| [1.0] | x == 1.0 | 정확한 버전 일치 |
| (,1.0] | x ≤ 1.0 | 최대 버전 (포함) |
| (,1.0) | x < 1.0 | 최대 버전, 제외 |
| [1.0,2.0] | 1.0 ≤ x ≤ 2.0 | 정확한 범위 (포함) |
| (1.0,2.0) | 1.0 < x < 2.0 | 정확한 범위, 제외 |
| [1.0,2.0) | 1.0 ≤ x < 2.0 | 혼합 최소값 및 배타 최대 버전 |
| (1.0)    | 잘못된 | 잘못된 |

PackageReference 형식을 사용 하는 경우 NuGet은 숫자의 주, 부, \*패치 및 시험판 접미사 부분에 와일드 카드 표기법을 사용 하도록 지원 합니다. 와일드 카드는 형식에서 `packages.config` 지원 되지 않습니다.

> [!Note]
> PackageReference의 버전 범위에는 시험판 버전이 포함 되어 있습니다. 기본적으로 부동 버전은 옵트인 (opt in) 하지 않는 한 시험판 버전을 확인 하지 않습니다. 관련 기능 요청의 상태는 [6434 문제](https://github.com/NuGet/Home/issues/6434#issuecomment-358782297)를 참조 하세요.

### <a name="examples"></a>예

프로젝트 파일, `packages.config` 파일 및 `.nuspec` 파일에서 패키지 종속성의 버전 또는 버전 범위를 항상 지정 합니다. 버전 또는 버전 범위를 사용 하지 않으면 NuGet 2.8. x 및 이전 버전은 종속성을 확인할 때 사용 가능한 최신 패키지 버전을 선택 하는 반면, NuGet 3.x 이상에서는 가장 낮은 패키지 버전을 선택 합니다. 버전 또는 버전 범위를 지정 하면 이러한 불확실성이 방지 됩니다.

#### <a name="references-in-project-files-packagereference"></a>프로젝트 파일의 참조 (PackageReference)

```xml
<!-- Accepts any version 6.1 and above. -->
<PackageReference Include="ExamplePackage" Version="6.1" />

<!-- Accepts any 6.x.y version. -->
<PackageReference Include="ExamplePackage" Version="6.*" />
<PackageReference Include="ExamplePackage" Version="[6,7)" />

<!-- Accepts any version above, but not including 4.1.3. Could be
     used to guarantee a dependency with a specific bug fix. -->
<PackageReference Include="ExamplePackage" Version="(4.1.3,)" />

<!-- Accepts any version up below 5.x, which might be used to prevent pulling in a later
     version of a dependency that changed its interface. However, this form is not
     recommended because it can be difficult to determine the lowest version. -->
<PackageReference Include="ExamplePackage" Version="(,5.0)" />

<!-- Accepts any 1.x or 2.x version, but not 0.x or 3.x and higher. -->
<PackageReference Include="ExamplePackage" Version="[1,3)" />

<!-- Accepts 1.3.2 up to 1.4.x, but not 1.5 and higher. -->
<PackageReference Include="ExamplePackage" Version="[1.3.2,1.5)" />
```

**의 `packages.config`참조:**

에서 `packages.config`모든 종속성은 패키지를 복원할 때 사용 `version` 되는 정확한 특성으로 나열 됩니다. `allowedVersions` 특성은 업데이트 작업을 수행 하는 동안에만 패키지를 업데이트할 수 있는 버전을 제한 하는 데 사용 됩니다.

```xml
<!-- Install/restore version 6.1.0, accept any version 6.1.0 and above on update. -->
<package id="ExamplePackage" version="6.1.0" allowedVersions="6.1.0" />

<!-- Install/restore version 6.1.0, and do not change during update. -->
<package id="ExamplePackage" version="6.1.0" allowedVersions="[6.1.0]" />

<!-- Install/restore version 6.1.0, accept any 6.x version during update. -->
<package id="ExamplePackage" version="6.1.0" allowedVersions="[6,7)" />

<!-- Install/restore version 4.1.4, accept any version above, but not including, 4.1.3.
     Could be used to guarantee a dependency with a specific bug fix. -->
<package id="ExamplePackage" version="4.1.4" allowedVersions="(4.1.3,)" />

<!-- Install/restore version 3.1.2, accept any version up below 5.x on update, which might be
     used to prevent pulling in a later version of a dependency that changed its interface.
     However, this form is not recommended because it can be difficult to determine the lowest version. -->
<package id="ExamplePackage" version="3.1.2" allowedVersions="(,5.0)" />

<!-- Install/restore version 1.1.4, accept any 1.x or 2.x version on update, but not
     0.x or 3.x and higher. -->
<package id="ExamplePackage" version="1.1.4" allowedVersions="[1,3)" />

<!-- Install/restore version 1.3.5, accepts 1.3.2 up to 1.4.x on update, but not 1.5 and higher. -->
<package id="ExamplePackage" version="1.3.5" allowedVersions="[1.3.2,1.5)" />
```

**파일의 `.nuspec` 참조**

요소의`<dependency>` 특성은 `version` 종속성에 허용 되는 범위 버전을 설명 합니다.

```xml
<!-- Accepts any version 6.1 and above. -->
<dependency id="ExamplePackage" version="6.1" />

<!-- Accepts any version above, but not including 4.1.3. Could be
     used to guarantee a dependency with a specific bug fix. -->
<dependency id="ExamplePackage" version="(4.1.3,)" />

<!-- Accepts any version up below 5.x, which might be used to prevent pulling in a later
     version of a dependency that changed its interface. However, this form is not
     recommended because it can be difficult to determine the lowest version. -->
<dependency id="ExamplePackage" version="(,5.0)" />

<!-- Accepts any 1.x or 2.x version, but not 0.x or 3.x and higher. -->
<dependency id="ExamplePackage" version="[1,3)" />

<!-- Accepts 1.3.2 up to 1.4.x, but not 1.5 and higher. -->
<dependency id="ExamplePackage" version="[1.3.2,1.5)" />
```

## <a name="normalized-version-numbers"></a>정규화 된 버전 번호

> [!Note]
> 이는 NuGet 3.4 이상에 대 한 주요 변경 내용입니다.

설치, 다시 설치 또는 복원 작업 중에 리포지토리에서 패키지를 가져올 때 NuGet 3.4 +는 버전 번호를 다음과 같이 처리 합니다.

- 버전 번호에서 앞에 오는 0이 제거 됩니다.

        1.00 is treated as 1.0
        1.01.1 is treated as 1.1.1
        1.00.0.1 is treated as 1.0.0.1

- 버전 번호의 네 번째 부분에서 0이 생략 됩니다.

        1.0.0.0 is treated as 1.0.0
        1.0.01.0 is treated as 1.0.1

`pack`및 `restore` 작업은 가능한 경우 버전을 정규화 합니다. 이미 빌드된 패키지의 경우에는이 정규화가 패키지 자체의 버전 번호에 영향을 주지 않습니다. 종속성을 확인할 때 NuGet이 버전과 일치 하는 방식에만 영향을 줍니다.

그러나 NuGet 패키지 리포지토리는 패키지 버전 복제를 방지 하기 위해 NuGet과 동일한 방식으로 이러한 값을 처리 해야 합니다. 따라서 패키지의 버전 *1.0* 을 포함 하는 리포지토리는 버전 *1.0.0* 을 별도의 다른 패키지로 호스트 해서는 안 됩니다.
