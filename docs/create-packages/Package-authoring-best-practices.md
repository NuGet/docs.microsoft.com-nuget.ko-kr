---
title: 패키지 제작 모범 사례
description: 높은 품질의 NuGet 패키지를 생성하기 위한 모범 사례 일반 가이드입니다.
author: chgill-MSFT
ms.author: chgill
ms.date: 09/17/2020
ms.topic: conceptual
ms.openlocfilehash: ec1532900bed7d13ea2400afe9f855105a5c2fde
ms.sourcegitcommit: adb261dd4b2a8cd75447f7b5ea6a9e5a1a54d61d
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/16/2021
ms.locfileid: "122209893"
---
# <a name="package-authoring-best-practices"></a>패키지 제작 모범 사례

이 지침은 NuGet 패키지 작성자가 높은 품질의 패키지를 만들고 게시할 수 있도록 간단한 참조 정보를 제공하기 위한 참고 자료입니다. 주로 메타데이터 및 압축과 같은 패키지 관련 모범 사례를 중점적으로 다룹니다. 고품질 라이브러리 빌드에 대한 보다 심층적인 제안 사항은 .NET [오픈 소스 라이브러리 지침](/dotnet/standard/library-guidance/)을 참조하세요.

## <a name="types-of-recommendations"></a>권장 사항 유형

각 문서에서는 **수행**, **고려**, **회피** 및 **금지** 의 네 가지 권장 사항 유형을 제공합니다. 각 권장 사항 유형은 수행해야 하는 필요성의 정도를 나타냅니다.

**수행** 권장 사항은 거의 항상 따라야 합니다. 예:

✔️ 패키지의 목적을 담은 간단한 설명을 포함합니다(수행).

**고려** 권장 사항은 일반적으로 따라야 하지만 규칙에 따른 정당한 예외의 경우가 있습니다.

✔️ NuGet의 접두사 예약 [조건](../nuget-org/id-prefix-reservation.md)을 충족하는 접두사를 가진 NuGet 패키지 이름을 선택합니다.

**회피** 권장 사항은 일반적으로 좋지는 않지만 규칙을 깨는 것이 적합한 경우를 언급합니다.

❌ 정확한 버전을 요구하는 NuGet 패키지 참조는 사용하지 않습니다.

마지막으로, **금지** 는 수행하지 않아야 하는 항목을 나타냅니다.

❌ `LicenseUrl` 메타데이터 속성은 사용하지 마세요(금지).

## <a name="create-a-nuget-package"></a>NuGet 패키지 만들기

NuGet 패키지를 만드는 최신 권장 방법은 [SDK 스타일 프로젝트](../resources/check-project-format.md)에서 만드는 것입니다. [대상 프레임워크](/dotnet/standard/frameworks) 및 [패키지 메타데이터](#package-metadata)를 비롯한 SDK 스타일 프로젝트 속성은 [프로젝트 파일](/visualstudio/ide/solutions-and-projects-in-visual-studio#project-file)에 정의되어 있습니다.

[Visual Studio](../quickstart/create-and-publish-a-package-using-visual-studio.md?tabs=netcore-cli) 또는 [dotnet CLI](../quickstart/create-and-publish-a-package-using-the-dotnet-cli.md)에서 필수 속성과 압축을 정의하여 SDK 스타일 프로젝트에서 패키지를 만듭니다.

✔️ SDK 스타일 프로젝트를 만들고 Visual Studio 또는 dotnet CLI를 사용하여 패키지를 생성(압축)합니다.

필요한 클라이언트 도구, 프로젝트 파일 예제, 명령 등 패키지 생성에 관련된 보다 자세한 지침은 [dotnet CLI를 사용하여 NuGet 패키지 만들기](./creating-a-package-dotnet-cli.md)를 참조하세요.

대상으로 지정할 .NET Framework를 결정하는 데 도움이 되도록 [플랫폼 간 대상 지정에 대한 최신 지침](/dotnet/standard/library-guidance/cross-platform-targeting)을 참조하세요.

## <a name="package-metadata"></a>패키지 메타데이터

메타데이터는 모든 NuGet 패키지의 기본 구성 요소입니다. 메타데이터의 품질은 패키지의 검색 가능성, 유용성 및 신뢰성에 크게 영향을 줄 수 있습니다.

Visual Studio에서 패키지 메타데이터 지정에 권장되는 방법은 프로젝트 > [프로젝트 이름] 속성 > 패키지로 이동하는 것입니다.

패키지 메타데이터 요소는 [프로젝트 파일에서 직접 지정](./creating-a-package-msbuild.md#set-properties)할 수도 있습니다.

다음은 사용 가능한 패키지 메타데이터 요소를 매핑 및 설명하는 표입니다.

| Visual Studio 속성 이름                       | [프로젝트 파일/MSBuild 속성 이름](/dotnet/core/tools/csproj#packagereleasenotes)                              | [Nuspec 속성 이름](/nuget/reference/nuspec#general-form-and-schema)   | Description                                                                                                           |
|-----------------------------------------------    |-----------------------------------------------------------------------------------------------------------------------------------------  |---------------------------------------------------------------------------------------------------    |-------------------------------------------------------------------------------------------------------------------    |
| [`Package id`](#package-id)                       | [`PackageId`](/nuget/reference/msbuild-targets#pack-target)                                                               | [`id`](/nuget/reference/nuspec#id)                                        | 패키지 이름 또는 ID입니다.                                                                                       |
| [`Package version`](#package-version)             | [`PackageVersion`](/nuget/reference/msbuild-targets#pack-target)                                                      | [`version`](/nuget/reference/nuspec#version)                              | NuGet 패키지 버전입니다.                                                                                                |
| [`Authors`](#authors)                             | [`Authors`](/nuget/reference/msbuild-targets#pack-target)                                                                 | [`authors`](/nuget/reference/nuspec#authors)                              | 쉼표로 구분된 패키지 작성자 목록으로, 주로 개인 또는 조직의 특정 이름을 사용합니다.           |
| [`Description`](#description)                     | [`Description`](/nuget/reference/msbuild-targets#pack-target)                                                         | [`description`](/nuget/reference/nuspec#description)                      | 패키지에 대한 설명입니다.                                                                                         |
| [`Copyright`](#copyright)                         | [`Copyright`](/nuget/reference/msbuild-targets#pack-target)                                                               | [`copyright`](/nuget/reference/nuspec#copyright)                          | 패키지에 대한 저작권 정보입니다.                                                                                    |
| [`Licensing - Expression`](#licensing)            | [`PackageLicenseExpression`](/nuget/reference/msbuild-targets#packing-a-license-expression-or-a-license-file)     | [`license type="expression"`](/nuget/reference/nuspec#license)            | SPDX 라이선스 식입니다.                                                                                           |
| [`Licensing - File`](#licensing)                  | [`PackageLicenseFile`](/nuget/reference/msbuild-targets#packing-a-license-expression-or-a-license-file)           | [`license type="file"`](/nuget/reference/nuspec#license)                  | 사용자 지정 라이선스 파일의 경로입니다.                                                                                        |
| [`Project URL`](#project-url)                     | `PackageProjectUrl`                                                                                                                       | [`projectUrl`](/nuget/reference/nuspec#projecturl)                        | 프로젝트 홈페이지의 URL입니다.                                                                                       |
| [`Icon File`](#icon)                              | [`PackageIcon`](/nuget/reference/msbuild-targets#packing-an-icon-image-file)                                      | [`icon`](/nuget/reference/nuspec#icon)                                    | 패키지 아이콘 이미지 파일의 경로입니다.                                                                                  |
| [`Repository URL`](#repository-type-and-url)      | [`RepositoryUrl`](/nuget/reference/msbuild-targets#pack-target)                                                       | [`repository url`](/nuget/reference/nuspec#repository)                    | 패키지가 빌드된 리포지토리의 URL입니다.                                                               |
| [`Repository type`](#repository-type-and-url)     | [`RespositoryType`](/nuget/reference/msbuild-targets#pack-target)                                                     | [`repository type`](/nuget/reference/nuspec#repository)                   | 리포지토리 URL이 가리키는 리포지토리의 유형입니다(예: "git").                                                    |
| [`Tags`](#tags)                                   | [`PackageTags`](/nuget/reference/msbuild-targets#pack-target)                                                         | [`tags`](/nuget/reference/nuspec#tags)                                    | 패키지를 설명하는 태그 및 키워드의 공백으로 구분된 목록입니다. 태그는 패키지를 검색할 때 사용됩니다.     |
| [`Release notes`](#release-notes)                 | [`PackageReleaseNotes`](/nuget/reference/msbuild-targets#pack-target)                                         | [`releaseNotes`](/nuget/reference/nuspec#releasenotes)                    | 이 패키지 릴리스의 변경 내용에 대한 설명입니다.                                                     |
### <a name="package-id"></a>패키지 ID

완전히 새로운 패키지를 게시하는 경우 다음을 따르세요.

✔️ NuGet.org의 기존 패키지와 명확하게 구분되는 고유한 패키지 ID를 선택합니다.
> NuGet.org에서 ID를 검색하거나 https://www.nuget.org/packages/<package 이름\> 링크가 존재하는지 확인하여 패키지 ID가 고유하고 구분 가능한지 여부를 확인할 수 있습니다.

✔️ NuGet 패키지 이름 선택 시 NuGet의 [접두사 예약 조건](../nuget-org/id-prefix-reservation.md#id-prefix-reservation-criteria)을 충족하는 접두사를 가지도록 하는 것을 고려합니다.
> 패키지에 접두사 ID를 예약하면 다음과 같은 검증 확인 표시를 가질 수 있습니다. ![이미지](media/Verified-check-mark.png)
> 
> 자세한 내용은 [패키지 ID 접두사 예약 문서](../nuget-org/id-prefix-reservation.md)를 확인하세요.

### <a name="package-version"></a>패키지 버전

✔️ NuGet 패키지 버전을 관리하는 데 [SemVer](https://semver.org/)를 사용하는 것을 고려하세요.
> 기본적으로 이는 Major.Minor.Patch[-prerelease] 형식을 사용한다는 의미입니다.

✔️ 안정적이지 않거나 미리 보기인 경우 패키지를 [시험판 패키지](./prerelease-packages.md)로 게시합니다.

고급 지침은 [.NET 라이브러리 버전 관리 가이드](/dotnet/standard/library-guidance/versioning)를 참조하세요.

### <a name="authors"></a>Authors

✔️ 작성자 필드에 개인 또는 조직의 특정 이름을 사용합니다.
> 예를 들어 NuGet.org 사용자 이름이 "jdoe"인 경우 작성자 필드에 "Jane Doe"를 사용하면 소비자가 작성자를 알아보는 데 도움이 될 수 있습니다. 조직의 NuGet.org 사용자 이름이 "ContosoToolkit"인 경우 "Contoso Corporation"을 사용하면 인식하기도 쉽고 소비자의 신뢰도가 높아질 수 있습니다.
### <a name="description"></a>Description

✔️ 패키지에 대한 간단한 설명(최대 4000자)을 포함합니다.
> 패키지 설명은 NuGet 검색에 표시되는 가장 중요한 필드 중 하나이며, 잠재적 소비자가 패키지가 적합한지 여부를 결정할 때 가장 먼저 확인하는 것입니다.

### <a name="copyright"></a>Copyright

✔️ "Copyright (c) <이름/회사\> <year\>" 형식으로 패키지의 저작권을 표시하는 걸 고려하세요.
>저작권 정보는 허가 없이 작업을 복사/복제할 수 없음을 나타냅니다. 패키지에 저작권 표시를 포함하는 건 간단한 작업이며 손해 볼 것이 없습니다.

예: Copyright (c) Contoso 2020

### <a name="licensing"></a>라이선스

✔️ [패키지에 라이선스 식이나 라이선스 파일을 포함](../reference/msbuild-targets.md#packing-a-license-expression-or-a-license-file)합니다.
> [!IMPORTANT]
> 라이선스가 없는 프로젝트는 기본적으로 [배타적 저작권](https://choosealicense.com/no-permission/)을 사용하며, 이는 프로젝트를 사용할 권한을 누구에게도 부여하지 않았다는 것을 의미합니다.

❌ 사용되지 않는 `LicenseUrl` 메타데이터 속성을 사용하지 마세요.
> URL에서 라이선스가 변경되면 이전 패키지 버전에 표시된 라이선스에 변경 내용이 소급 적용되므로 법적 모호성이 발생합니다.

#### <a name="if-your-package-is-open-source"></a>패키지가 [오픈 소스](https://opensource.org/osd)인 경우

✔️ [오픈 소스 라이선스를 선택](https://choosealicense.com/)하여 패키지를 오픈 소스로 만듭니다.
> *"오픈 소스 라이선스는 오픈 소스 정의를 준수하는 라이선스입니다. 간단히 말하자면 소프트웨어를 자유롭게 사용, 수정 및 공유할 수 있도록 합니다."* - Open Source Initiative. 오픈 소스 소프트웨어 및 Open Source Initiative에 대해 자세히 알아보려면 https://opensource.org/ 를 확인하세요.

✔️ [패키지에 라이선스 식을 포함](../reference/msbuild-targets.md#packing-a-license-expression-or-a-license-file)하는 것을 고려합니다.
> 라이선스 식은 가장 명확하게 표시되며 패키지를 사용할 수 있는지 또는 라이선스가 변경되었는지를 소비자에게 더 분명하게 알려줍니다. 
> [!Note]
> NuGet.org는 Open Source Initiative 또는 Free Software Foundation에서 승인한 라이선스에 대한 라이선스 식만 허용합니다.

#### <a name="if-your-package-is-not-open-source"></a>패키지가 오픈 소스가 아닌 경우

✔️ [패키지에 라이선스 파일을 포함](../reference/msbuild-targets.md#packing-a-license-expression-or-a-license-file)합니다.
> 비표준 라이선스를 포함하여 모든 라이선스 파일(.txt 또는 .md)을 패키지에 추가할 수 있습니다. 

### <a name="project-url"></a>프로젝트 URL

✔️ 관련 프로젝트, 리포지토리 또는 회사 웹 사이트로 연결되는 링크를 포함하는 것을 고려합니다.
> 프로젝트 사이트에는 사용자가 패키지에 대해 알아야 하는 모든 정보가 있어야 하며 많은 경우 사용자가 설명서를 찾는 위치이기도 합니다.

### <a name="icon"></a>아이콘

✔️ 패키지를 시각적으로 구분할 수 있도록 [패키지에 아이콘을 포함](../reference/msbuild-targets.md#packing-an-icon-image-file)하는 것을 고려합니다. 이 같은 비교적 사소한 추가를 통해 패키지 인지도를 향상시킬 수 있습니다.
> 아이콘은 개별 패키지에 특정될 수도 있고 브랜드 로고일 수도 있습니다.

✔️ 보기 결과를 최적화하기 위해 128x128이고 투명한 배경을 가진 이미지(PNG)를 사용합니다.
> NuGet은 이미지가 표시되는 클라이언트에 맞게 이미지 크기를 자동으로 조정합니다.

❌사용되지 않는`IconUrl` 메타데이터 속성을 사용하지 마세요.

### <a name="repository-type-and-url"></a>리포지토리 유형 및 URL

✔️ [소스 링크](/dotnet/standard/library-guidance/sourcelink)를 설정하여 NuGet 패키지에 소스 제어 메타데이터를 자동으로 추가하고 라이브러리를 쉽게 디버그할 수 있도록 하는 것을 고려합니다.
> 소스 링크는 `Repository URL` 및 `Repository Type`을 패키지 메타데이터에 자동으로 추가합니다. 또한 패키지 버전과 연결된 특정 커밋을 추가합니다.

### <a name="tags"></a>태그

✔️ 검색 가능성을 향상시키기 위해 패키지와 관련된 주요 용어를 사용해 여러 태그를 포함합니다.
> NuGet.org의 검색 알고리즘은 태그를 고려합니다. 태그는 특히 패키지 ID에는 없지만 관련성 있는 용어에 특히 유용합니다.

예를 들어 콘솔에 문자열을 기록하는 패키지를 게시한 경우 "로깅, 로그, 콘솔, 문자열, 출력"을 포함합니다.

### <a name="release-notes"></a>릴리스 정보

✔️ 업데이트가 있을 때마다 변경 내용에 대해 설명하는 릴리스 정보를 포함하는 것을 고려합니다.
> 릴리스 정보에 요구되는 특정 형식은 없지만 다음을 포함하는 것이 좋습니다.
>
> 1. 주요 변경 내용
> 2. 새로운 기능
> 3. 버그 수정
> 
> 리포지토리에서 릴리스 정보 또는 변경 로그를 이미 추적하는 경우 관련 파일로 연결되는 링크를 포함할 수도 있습니다.

## <a name="related-topics"></a>관련 항목

- [패키지 만들기 및 게시(dotnet CLI)](../quickstart/create-and-publish-a-package-using-the-dotnet-cli.md)
- [패키지 만들기 및 게시(Visual Studio)](../quickstart/create-and-publish-a-package-using-visual-studio.md?tabs=netcore-cli)
