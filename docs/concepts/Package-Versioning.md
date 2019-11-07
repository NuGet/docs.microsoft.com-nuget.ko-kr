---
title: NuGet 패키지 버전 참조
description: NuGet 패키지가 종속된 다른 패키지의 버전 번호 및 범위 지정과 종속성 설치 방법에 대한 정확한 세부 정보입니다.
author: karann-msft
ms.author: karann
ms.date: 03/23/2018
ms.topic: reference
ms.reviewer: anangaur
ms.openlocfilehash: e0014a812ea591ef40c961e13864652d75ebdf6c
ms.sourcegitcommit: 39f2ae79fbbc308e06acf67ee8e24cfcdb2c831b
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 11/05/2019
ms.locfileid: "73610981"
---
# <a name="package-versioning"></a>패키지 버전 관리

특정 패키지는 항상 패키지 식별자와 정확한 버전 번호를 사용하여 참조됩니다. 예를 들어, nuget.org의 [Entity Framework](https://www.nuget.org/packages/EntityFramework/)에는 버전 *4.1.10311*에서 버전 *6.1.3*(안정적인 최신 릴리스)과 *6.2.0-beta1*과 같은 다양한 시험판 버전에 이르기까지 수십 개의 특정 패키지가 있습니다.

패키지를 만들 때 선택적 시험판 문자 접미사를 사용하여 특정 버전 번호를 할당합니다. 반면, 패키지를 사용할 때는 정확한 버전 번호 또는 허용 가능한 버전 범위를 지정할 수 있습니다.

항목 내용

- 시험판 접미사 등의 [버전 기본 사항](#version-basics)입니다.
- [버전 범위 및 와일드카드](#version-ranges-and-wildcards)
- [정규화된 버전 번호](#normalized-version-numbers)

## <a name="version-basics"></a>버전 기본 사항

특정 버전 번호는 *주.부.패치[-접미사]* 형식으로 되어 있으며, 해당 구성 요소의 의미는 다음과 같습니다.

- *주*: 호환성이 손상되는 변경
- *부*: 이전 버전과 호환되는 새로운 기능
- *패치*: 이전 버전과 호환되는 버그 수정에만 해당
- *-접미사*(선택 사항): 하이픈 다음에는 시험판 버전을 나타내는 문자열([유의적 버전 또는 SemVer 1.0 규칙](https://semver.org/spec/v1.0.0.html)을 따름)이 옵니다.

**예제:**

    1.0.1
    6.11.1231
    4.3.1-rc
    2.2.44-beta1

> [!Important]
> nuget.org는 정확한 버전 번호가 없는 패키지 업로드를 모두 거부합니다. 버전은 패키지를 만드는 데 사용되는 `.nuspec` 또는 프로젝트 파일에 지정해야 합니다.

### <a name="pre-release-versions"></a>시험판 버전

엄밀히 따지면, 패키지 작성자는 어떤 문자열이든 시험판 버전을 나타내는 접미사로 사용할 수 있습니다. 그 이유는 NuGet이 이러한 모든 버전을 시험판으로 처리하며, 달리 해석하지 않기 때문입니다. 즉, NuGet은 어떤 UI가 사용되었는지에 상관없이 전체 버전 문자열을 표시하며, 접미사의 의미는 전적으로 소비자의 해석에 맡깁니다.

그렇긴 하지만 패키지 개발자는 일반적으로 널리 인정된 명명 규칙을 따릅니다.

- `-alpha`: 일반적으로 진행 중인 작업이나 실험에 사용되는 알파 릴리스입니다.
- `-beta`: 일반적으로 다음에 계획된 릴리스에 대한 기능 완료인 베타 릴리스이지만 알려진 버그를 포함할 수 있습니다.
- `-rc`: 일반적으로 심각한 버그가 발생하지 않는 한 잠재적으로 최종적(안정적)인 릴리스인 릴리스 후보입니다.

> [!Note]
> NuGet 4.3.0 이상은 *1.0.1-build.23*에서와 같이 시험판 번호에 점 표기법을 지원하는 [SemVer 2.0.0](https://semver.org/spec/v2.0.0.html)을 지원합니다. NuGet 4.3.0 이전 버전에서는 점 표기법이 지원되지 않습니다. *1.0.1-build23*과 같은 형식을 사용할 수 있습니다.

패키지 참조를 확인할 때 패키지 버전 여러 개가 접미사만 다른 경우 NuGet은 먼저 접미사가 없는 버전을 선택한 다음, 알파벳 역순으로 시험판 버전에 우선 순위를 적용합니다. 예를 들어, 다음 버전은 정확히 표시된 순서대로 선택됩니다.

    1.0.1
    1.0.1-zzz
    1.0.1-rc
    1.0.1-open
    1.0.1-beta
    1.0.1-alpha2
    1.0.1-alpha
    1.0.1-aaa

## <a name="semantic-versioning-200"></a>유의적 버전 2.0.0

NuGet은 NuGet 4.3.0 이상 및 Visual Studio 2017 버전 15.3 이상을 통해 [유의적 버전 2.0.0](https://semver.org/spec/v2.0.0.html)을 지원합니다.

SemVer v2.0.0의 특정 의미 체계는 이전 클라이언트에서 지원되지 않습니다. NuGet은 다음 문 중 하나라도 참인 경우 패키지 버전이 SemVer v2.0.0에 해당한다고 간주합니다.

- 시험판 레이블이 점으로 구분됩니다(예: *1.0.0-alpha.1*).
- 버전에 빌드-메타데이터(예: *1.0.0+githash*)가 있습니다.

nuget.org의 경우 패키지는 다음 문 중 하나가 참인 경우 SemVer v2.0.0 패키지로 정의됩니다.

- 패키지의 자체 버전은 위에서 정의한 대로 SemVer v2.0.0 규격이며, SemVer v1.0.0 규격이 아닙니다.
- 패키지의 모든 종속성 버전 범위에는 최소 또는 최대 버전이 있으며, 이는 위에서 정의한 대로 SemVer v2.0.0 규격이며, SemVer v1.0.0 규격이 아닙니다(예: *[1.0.0-alpha.1, )* ).

SemVer v2.0.0 특정 패키지를 nuget.org에 업로드하는 경우 패키지는 이전 클라이언트에 표시되지 않으며, 다음 NuGet 클라이언트에서만 사용할 수 있습니다.

- NuGet 4.3.0 이상
- Visual Studio 2017 버전 15.3 이상
- [NuGet VSIX v3.6.0](https://dist.nuget.org/visualstudio-2015-vsix/latest/NuGet.Tools.vsix)을 사용하는 Visual Studio 2015
- dotnet
  - dotnetcore.exe(.NET SDK 2.0.0 이상)

타사 클라이언트:

- JetBrains Rider
- Paket 버전 5.0 이상

<!-- For compatibility with previous dependency-versions page -->
<a name="version-ranges"></a>

## <a name="version-ranges-and-wildcards"></a>버전 범위 및 와일드카드

패키지 종속성을 참조할 때 NuGet은 간격 표기법으로 버전 범위를 다음과 같이 요약하여 지정합니다.

| Notation | 적용된 규칙 | 설명 |
|----------|--------------|-------------|
| 1.0 | x ≥ 1.0 | 최소 버전(포함) |
| (1.0,) | x > 1.0 | 최소 버전(제외) |
| [1.0] | x == 1.0 | 정확한 버전 일치 |
| (,1.0] | x ≤ 1.0 | 최대 버전(포함) |
| (,1.0) | x < 1.0 | 최대 버전(제외) |
| [1.0,2.0] | 1.0 ≤ x ≤ 2.0 | 정확한 범위(포함) |
| (1.0,2.0) | 1.0 < x < 2.0 | 정확한 범위(제외) |
| [1.0,2.0) | 1.0 ≤ x < 2.0 | 최소 포함 및 최대 제외 혼합 버전 |
| (1.0)    | 잘못된 | 잘못된 |

PackageReference 형식을 사용하는 경우 NuGet은 숫자의 주, 부, 패치, 시험판 접미사 부분에 와일드카드 표기법(\*)도 사용할 수 있도록 지원합니다. 와일드카드는 `packages.config` 형식으로 지원되지 않습니다.

> [!Note]
> PackageReference의 버전 범위에는 시험판 버전이 포함됩니다. 부동 버전은 옵트인되지 않는 한 의도적으로 시험판 버전을 확인하지 않도록 설계되었습니다. 관련 기능 요청 상태는 [문제 6434](https://github.com/NuGet/Home/issues/6434#issuecomment-358782297)를 참조하세요.

### <a name="examples"></a>예

프로젝트 파일, `packages.config` 파일, `.nuspec` 파일에서 패키지 종속성의 버전 또는 버전 범위를 항상 지정합니다. 버전 또는 버전 범위가 없으면, 종속성을 확인할 때 NuGet 2.8.x 이하는 사용 가능한 최신 패키지 버전을 선택하는 반면, NuGet 3.x 이상은 가장 낮은 패키지 버전을 선택합니다. 버전 또는 버전 범위를 지정하면 이러한 불확실성을 피할 수 있습니다.

#### <a name="references-in-project-files-packagereference"></a>프로젝트 파일의 참조(PackageReference)

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

**`packages.config`에서의 참조:**

`packages.config`에서 모든 종속성은 패키지를 복원할 때 사용되는 정확한 `version` 특성과 함께 나열됩니다. `allowedVersions` 특성은 패키지가 업데이트될 수 있는 버전을 제한하기 위해 업데이트 작업 시에만 사용됩니다.

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

**`.nuspec`파일에서의 참조**

`<dependency>` 요소의 `version` 특성은 종속성에 허용되는 범위 버전을 설명합니다.

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

## <a name="normalized-version-numbers"></a>정규화된 버전 번호

> [!Note]
> 이는 NuGet 3.4 이상에서 호환성이 손상되는 변경입니다.

설치, 다시 설치 또는 복원 작업 시 리포지토리에서 패키지를 가져올 때 NuGet 3.4 이상은 버전 번호를 다음과 같이 처리합니다.

- 버전 번호 앞에 있는 0을 제거합니다.

        1.00 is treated as 1.0
        1.01.1 is treated as 1.1.1
        1.00.0.1 is treated as 1.0.0.1

- 버전 번호의 네 번째 파트에서 0을 생략합니다.

        1.0.0.0 is treated as 1.0.0
        1.0.01.0 is treated as 1.0.1

`pack` 및 `restore` 작업은 가능한 경우 항상 버전을 정규화합니다. 이미 빌드된 패키지의 경우, 이 정규화 작업이 패키지 자체의 버전 번호에 영향을 주지는 않습니다. NuGet이 종속성을 확인할 때 버전과 일치시키는 방식에만 영향을 줍니다.

그러나 패키지 버전 중복을 방지하기 위해서는 NuGet 패키지 리포지토리에서 이러한 값을 NuGet과 동일한 방식으로 처리해야 합니다. 따라서 패키지 버전 *1.0*을 포함하는 리포지토리는 버전 *1.0.0*도 별도의 다른 패키지로 호스트해서는 안 됩니다.
