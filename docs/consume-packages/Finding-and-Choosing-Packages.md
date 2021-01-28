---
title: NuGet 패키지 찾기 및 선택
description: NuGet 검색 구문에 대한 세부 정보를 포함하여 프로젝트에 가장 적합한 NuGet 패키지를 찾아 선택하는 방법을 간략히 설명합니다.
author: JonDouglas
ms.author: jodou
ms.date: 06/04/2018
ms.topic: conceptual
ms.openlocfilehash: 4ba51028c1a69a3466cec655db19c2c498e29d9b
ms.sourcegitcommit: ee6c3f203648a5561c809db54ebeb1d0f0598b68
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 01/26/2021
ms.locfileid: "98775176"
---
# <a name="finding-and-evaluating-nuget-packages-for-your-project"></a>프로젝트에 대한 NuGet 패키지 찾기 및 평가

모든 .NET 프로젝트를 시작하거나 앱 또는 서비스에 대한 기능적 요구 사항을 확인할 때마다 해당 요구 사항을 충족하는 기존 NuGet 패키지를 사용하여 많은 시간과 노력을 많이 줄일 수 있습니다. 이러한 패키지는 [nuget.org](https://www.nuget.org/packages/)의 공용 컬렉션 또는 조직이나 다른 제3자가 제공한 전용 원본에서 제공할 수 있습니다.

## <a name="finding-packages"></a>패키지 찾기

nuget.org를 방문하거나 Visual Studio에서 패키지 관리자 UI를 열면 관련성을 기준으로 정렬된 패키지 목록이 표시됩니다. 이 목록은 모든 .NET 프로젝트에서 가장 널리 사용되는 패키지를 보여 줍니다. 이 중에는 사용자의 프로젝트에 유용한 패키지가 있을 가능성이 높습니다.

![가장 인기 있는 패키지를 보여 주는 nuget.org/packages의 기본 보기](media/Finding-01-Popularity.png)

nuget.org에서 페이지 오른쪽 위에 있는 **필터** 단추를 확인합니다. 고급 검색 패널을 클릭하면 확장되어 정렬 및 필터링 옵션이 표시됩니다.

![nuget.org의 'json'에 대한 검색 결과](media/Finding-02-SearchResults.png)

**패키지 형식** 필터를 사용하여 특정 형식의 패키지를 표시할 수 있습니다.
- **`All types`** : 이것은 기본적인 동작입니다. 형식에 관계없이 모든 패키지가 표시됩니다.
- **`Dependency`** : 프로젝트에 설치할 수 있는 일반 NuGet 패키지입니다.
- **`.NET tool`** : 콘솔 애플리케이션을 포함하는 NuGet 패키지인 [.NET 도구](/dotnet/core/tools/global-tools)로 필터링합니다.
- **`Template`** : [`dotnet new`](/dotnet/core/tools/dotnet-new) 명령을 사용하여 새 프로젝트를 만드는 데 사용할 수 있는 [.NET 템플릿](/dotnet/core/install/templates)으로 필터링합니다.

**정렬 기준** 옵션을 사용하여 검색 결과를 정렬할 수 있습니다.
- **`Relevance`** : 이것은 기본적인 동작입니다. 내부 채점 알고리즘에 따라 결과를 정렬합니다.
- **`Downloads`** : 전체 다운로드 수를 기준으로 검색 결과를 내림차순으로 정렬합니다.
- **`Recently updated`** : 검색 결과를 최신 버전의 만든 날짜를 기준으로 내림차순으로 정렬합니다.

**옵션** 섹션에서 **`Include prerelease`** 확인란을 찾을 수 있습니다.
확인란을 선택하면 nuget.org는 시험판을 포함한 모든 패키지 버전을 표시합니다. 안정적인 버전만 표시하려면 이 옵션을 선택 취소합니다.

검색 필터를 적용하려면 **`Apply`** 단추를 클릭합니다. **`Reset`** 단추를 클릭하면 언제든지 기본 동작으로 돌아갈 수 있습니다.

[검색 구문](#search-syntax)을 사용하여 태그, 소유자, 패키지 ID를 필터링할 수도 있습니다.

### <a name="does-the-package-support-my-projects-target-framework"></a>패키지에서 내 프로젝트의 대상 프레임워크를 지원합니까?

패키지에서 지원되는 프레임워크에 프로젝트의 대상 프레임워크가 포함되어 있는 경우에만 NuGet에서 해당 패키지를 프로젝트에 설치합니다. 패키지가 호환되지 않으면 NuGet에서 오류가 발생합니다.

일부 패키지는 지원되는 프레임워크를 nuget.org 갤러리에 직접 나열하지만, 이러한 데이터가 필요하지 않으므로 많은 패키지에는 해당 목록이 포함되지 않습니다. 현재 특정 대상 프레임워크를 지원하는 패키지를 nuget.org에서 검색할 수 있는 방법은 없습니다([NuGet 문제 2936](https://github.com/NuGet/NuGetGallery/issues/2936)에서 고려 중인 기능 참조).

다행히도 두 가지 다른 방법을 통해 지원되는 프레임워크를 결정할 수 있습니다.

1. NuGet 패키지 관리자 콘솔에서 [`Install-Package`](../reference/ps-reference/ps-ref-install-package.md) 명령을 사용하여 프로젝트에 패키지를 설치합니다. 패키지가 호환되지 않으면 이 명령은 패키지에서 지원하는 프레임워크를 표시합니다.

1. **정보** 아래의 **수동 다운로드** 링크를 사용하여 nuget.org의 해당 페이지에서 패키지를 다운로드합니다. 확장명을 `.nupkg`에서 `.zip`으로 변경하고 해당 파일을 열어 `lib` 폴더의 내용을 검사합니다. 각 하위 폴더에는 TFM(대상 프레임워크 모니커, [대상 프레임워크](../reference/target-frameworks.md) 참조)으로 명명된 지원되는 각 프레임워크의 하위 폴더가 표시됩니다. `lib`에 하위 폴더가 없고 단일 DLL만 표시되면 프로젝트에 패키지를 설치하여 해당 호환성을 확인해야 합니다.

## <a name="pre-release-packages"></a>시험판 패키지

대부분의 패키지 작성자는 미리 보기 및 베타 릴리스를 제공하여 지속적으로 개선하고 최신 수정 버전에 대한 피드백을 얻고 있습니다.

기본적으로 nuget.org에서는 시험판 패키지를 검색 결과에 표시합니다. 안정적인 릴리스만 검색하려면 페이지 오른쪽 위의 **필터** 단추에서 액세스할 수 있는 고급 검색 패널의 **시험판 포함** 옵션 선택을 취소합니다.

![nuget.org의 시험판 포함 확인란](media/Finding-06-include-prerelease.png)

Visual Studio에서 NuGet 및 dotnet CLI 도구를 사용하는 경우 NuGet은 기본적으로 시험판 버전을 포함하지 않습니다. 이 동작을 변경하려면 다음 단계를 수행합니다.

- **Visual Studio의 패키지 관리자 UI**: **NuGet 패키지 관리** UI에서 **시험판 포함** 확인란을 설정합니다. 이 확인란을 설정 또는 해제하면 패키지 관리자 UI 및 설치할 수 있는 사용 가능한 버전 목록을 새로 고칩니다.

    ![Visual Studio의 시험판 포함 확인란](media/Prerelease_02-CheckPrerelease.png)

- **패키지 관리자 콘솔**: `Find-Package`, `Get-Package`, `Install-Package`, `Sync-Package` 및 `Update-Package` 명령과 함께 `-IncludePrerelease` 스위치를 사용합니다. [PowerShell 참조](../reference/powershell-reference.md)를 참조하세요.

- **nuget.exe CLI**: `install`, `update`, `delete` 및 `mirror` 명령과 함께 `-prerelease` 스위치를 사용합니다. [NuGet CLI 참조](../reference/nuget-exe-cli-reference.md)를 참조하세요.

- **dotnet.exe CLI**: `-v` 인수를 사용하여 정확한 시험판 버전을 지정합니다. [dotnet add package 참조](/dotnet/core/tools/dotnet-add-package)를 참조하세요.

<a name="native-cpp-packages"></a>

### <a name="native-c-packages"></a>네이티브 C++ 패키지

NuGet은 Visual Studio의 C++ 프로젝트에서 사용할 수 있는 네이티브 C++ 패키지 캔을 지원합니다. 이를 통해 프로젝트의 **NuGet 패키지 관리** 상황에 맞는 메뉴 명령을 사용할 수 있고, `native` 대상 프레임워크를 소개하고, MSBuild 통합을 제공합니다.

[nuget.org](https://www.nuget.org/packages)에서 네이티브 패키지를 찾으려면 `tag:native`를 사용하여 검색합니다. 이러한 패키지는 일반적으로 패키지가 프로젝트에 추가될 때 NuGet에서 자동으로 가져오는 `.targets` 및 `.props` 파일을 제공합니다.

## <a name="evaluating-packages"></a>패키지 평가

패키지가 유용한지 평가하는 가장 좋은 방법은 다운로드하여 코드에 사용해 보는 것입니다(그런데, nuget.org의 모든 패키지는 정기적으로 바이러스가 있는지 검사됨). 즉 인기 있는 모든 패키지는 소수의 개발자만 사용하여 시작되었으며, 사용자는 얼리어답터 중 한 명일 수 있습니다!

한편 NuGet 패키지를 사용한다는 것은 패키지에 의존하고 있다는 것을 의미하므로 패키지가 강력하고 신뢰할 수 있는지 확인하려고 합니다. 패키지 설치 및 직접 테스트는 시간이 오래 걸리므로 패키지의 목록 페이지에 있는 정보를 사용하여 패키지의 품질에 대해 많이 알아볼 수도 있습니다.

- **통계 다운로드**: nuget.org의 패키지 페이지에서 **통계** 섹션에는 총 다운로드 수, 최근 버전 다운로드 수 및 일일 평균 다운로드 수가 표시됩니다. 숫자가 클수록 다른 많은 개발자가 패키지에 의존하고 있음을 나타내며, 이는 패키지가 그 자체를 입증했다는 것을 의미합니다.

    ![패키지의 목록 페이지에 대한 다운로드 통계](media/Finding-03-Downloads.png)

- **사용 대상**: 패키지 페이지의 **사용 대상** 섹션에는 이 패키지에 종속된 가장 널리 사용되는 5개 NuGet.org 패키지와 인기 있는 GitHub 리포지토리가 나열됩니다. 이 패키지에 종속된 패키지 및 리포지토리를 이 패키지의 “종속 항목”이라고 합니다. 종속 패키지와 리포지토리는 패키지 작성자가 신뢰하여 종속하도록 선택했으므로 이 패키지에 대한 “인증”으로 간주될 수 있습니다.
  - 종속 패키지는 ‘나열된 안정적인 최신 버전’에서 이 패키지의 ‘모든 버전’에 종속되어야 합니다.  이 정의는 표시된 종속 패키지가 신뢰할 수 있는 패키지 작성자 결정의 최신 리플렉션이며 이 패키지에 종속된다는 것을 확인합니다. 시험판 종속 항목은 아직 전체적인 인증으로 간주되지 않으므로 나열되지 않습니다. 예는 다음 표를 참조하세요.

    | 패키지 A 버전 | 패키지 A는 패키지 B의 종속 항목으로 나열됩니다. |
    |-|-|
    | v1.0.0<br>v1.1.0(안정적인 최신 버전) --> 패키지 B<br>v1.2.0-미리 보기 | TRUE이면, 안정적인 최신 버전이 패키지 B에 종속됩니다. |
    | v1.0.0 --> 패키지 B<br>v1.1.0(안정적인 최신 버전)<br>v1.2.0-미리 보기 | FALSE면, 안정적인 최신 버전이 패키지 B에 종속되지 않습니다. |
    | v1.0.0 --> 패키지 B<br>v1.1.0(안정적인 최신 버전)<br>v1.2.0-미리 보기 --> 패키지 B | FALSE면, 안정적인 최신 버전이 패키지 B에 종속되지 않습니다. |

  - GitHub 리포지토리의 별 수는 일반적으로 해당 리포지토리가 GitHub 사용자에게 얼마나 인기 있는지를 나타냅니다(별 수가 많을수록 일반적으로 더 인기 있음을 의미). GitHub의 별 및 리포지토리 순위 시스템에 대한 자세한 내용은 [GitHub의 시작 페이지](https://help.github.com/en/github/getting-started-with-github/saving-repositories-with-stars#about-stars)를 참조하세요.

    ![사용 대상](media/Used-By-section-Humanizer.png)

    > [!Note]
    > 패키지의 사용 대상 섹션은 사람이 개별 리포지토리를 검토하는 과정 없이 주기적으로 자동으로 생성되며, 패키지에 종속되는 NuGet.org 패키지와 인기 있는 GitHub 리포지토리를 표시하기 위해 정보를 제공하는 목적으로만 제공됩니다.

- **버전 기록**: 패키지 페이지의 **정보** 아래에서 최신 업데이트 날짜를 확인하고 **버전 기록** 을 검사합니다. 잘 유지 관리된 패키지에는 최신 업데이트와 풍부한 버전 기록이 있습니다. 방치한 패키지에는 업데이트가 거의 없으며, 일정 기간 동안 업데이트되지 않은 경우가 많습니다.

    ![패키지 목록 페이지의 버전 기록](media/Finding-04-VersionHistory.png)

- **최근 설치**: 패키지 페이지의 **통계** 아래에서 **전체 통계 보기** 를 선택합니다. 전체 통계 페이지에서는 지난 6주 동안 버전 번호별로 설치된 패키지를 보여줍니다. 일반적으로 다른 개발자가 적극적으로 사용하는 패키지는 그렇지 않은 패키지보다 더 나은 선택입니다.

- **지원**: 패키지 페이지의 **정보** 아래에서 **프로젝트 사이트**(사용 가능한 경우)를 선택하여 만든 이가 제공하는 지원 옵션을 확인합니다. 일반적으로 전용 사이트가 있는 프로젝트가 더 잘 지원됩니다.

- **개발자 기록**: 패키지 페이지의 **소유자** 아래에서 소유자를 선택하여 게시한 다른 패키지를 확인합니다. 여러 패키지가 있는 사람들은 앞으로도 계속 지원할 가능성이 높습니다.

- **오픈 소스 기여**: 많은 패키지가 오픈 소스 리포지토리에서 유지 관리되므로 개발자가 버그 수정 및 기능 향상에 직접 기여할 수 있도록 합니다. 지정된 패키지의 기여 기록은 얼마나 많은 개발자가 적극적으로 참여했는지를 나타내는 좋은 지표이기도 합니다.

- **소유자 인터뷰**: 사용자가 사용할 수 있는 훌륭한 패키지를 만드는 데 새 개발자도 동등하게 헌신할 수 있으며, NuGet 생태계에 새로운 것을 가져올 수 있는 기회를 제공하는 것이 좋습니다. 이를 고려하여, 목록 페이지의 **정보** 아래에 있는 **연락처 소유자** 옵션을 통해 패키지 개발자에게 직접 문의해 보세요. 아마, 이들은 여러분의 요구에 부응하기 위해 여러분과 함께 기꺼이 협력할 것입니다!

- **예약된 패키지 ID 접두사**: 많은 패키지 소유자가 [예약된 패키지 ID 접두사](../nuget-org/id-prefix-reservation.md)에 지원했으며 허가되었습니다. [nuget.org](https://www.nuget.org/) 또는 Visual Studio에서 패키지 ID 옆에 있는 시각적 개체 확인 표시가 나타나면 패키지 소유자가 ID 접두사 예약에 대한 [조건](../nuget-org/id-prefix-reservation.md#id-prefix-reservation-criteria)을 충족한다는 의미입니다. 즉, 패키지 소유자가 자체 및 해당 패키지를 식별하기에 명확합니다.

> [!Note]
> nuget.org의 패키지 목록 페이지에서 **라이선스 정보** 를 선택하면 볼 수 있는 패키지의 사용 조건에 항상 유의해야 합니다. 패키지에서 사용 조건을 지정하지 않은 경우 패키지 페이지의 **연락처 소유자** 링크를 사용하여 패키지 소유자에게 직접 문의해 보세요. Microsoft는 타사 패키지 공급자로부터 사용자에게 지적 재산권을 부여하지 않으며 타사에서 제공한 정보에 대해 책임을 지지 않습니다.

## <a name="license-url-deprecation"></a>라이선스 URL 사용 중단
[licenseUrl](../reference/nuspec.md#licenseurl)에서 [license](../reference/nuspec.md#license)로 전환하면서 일부 NuGet 클라이언트 및 NuGet 피드에 몇몇 경우에 라이선싱 정보를 표시하는 기능이 아직 없을 수 있습니다. 이전 버전과의 호환성을 유지하기 위해 라이선스 URL은 그러한 경우 라이선스 정보를 검색하는 방법을 설명하는 이 문서를 가리킵니다.

이 페이지로 연결되는 패키지에 대한 라이선스 URL을 클릭하면 패키지에 라이선스 파일이 포함됨을 의미하며
* 새 라이선스 정보를 해석하고 클라이언트에 표시하는 방법을 아직 모르는 피드에 연결됩니다. **또는**
* 잠재적으로 피드에서 제공하는 새 라이선스 정보를 읽고 해석하는 방법을 아직 모르는 클라이언트를 사용하고 있습니다. **또는**
* 둘의 조합

다음은 패키지 내의 라이선스 파일에 포함된 정보를 읽는 방법입니다.
1. NuGet 패키지를 다운로드하고 폴더에 콘텐츠의 압축을 풉니다.
1. 해당 폴더의 루트에 있는 `.nuspec` 파일을 엽니다.
1. `<license type="file">license\license.txt</license>`과 같은 태그가 있어야 합니다. 이는 이름이 `license.txt`인 라이선스 파일을 의미하며 해당 폴더의 루트에 있는 `license`라는 폴더 내에 있습니다.
1. `license` 폴더로 이동하여 `license.txt` 파일을 엽니다.

`.nuspec`에 라이선스를 설정하는 것과 동일한 MSBuild의 경우 [라이선스 표현식 또는 라이선스 파일 압축](../reference/msbuild-targets.md#packing-a-license-expression-or-a-license-file)을 확인하세요.

## <a name="search-syntax"></a>검색 구문

NuGet 패키지 검색은 nuget.org, NuGet CLI 및 Visual Studio의 NuGet 패키지 관리자 확장에서 동일하게 작동합니다. 일반적으로 검색은 패키지 설명뿐만 아니라 키워드에도 적용됩니다.

- **필터링**: `<property>:<term>` 구문을 사용하여 특정 속성에 검색어를 적용할 수 있습니다. 여기서 `<property>`(대/소문자 구분 안 함)은 `id`, `packageid`, `version`, `title`, `tags`, `author`, `description`, `summary` 및 `owner`일 수 있습니다. 동시에 여러 속성을 검색할 수 있습니다. `id` 속성에 대한 검색은 부분 문자열 일치이지만, `packageid` 및 `owner`는 대/소문자를 구분하지 않는 정확한 일치를 사용합니다. 예제:

```
PackageId:jquery             # Match the package ID in an exact, case-insensitive manner

owner:microsoft              # Match the owner in an exact, case-insensitive manner

id:NuGet.Core                # Match any part of the ID property
Id:"Nuget.Core"
ID:jQuery
id:jquery id:ui              # Search for multiple terms in the ID
id:jquery tags:validation    # Search multiple properties

invalid:jquery ui            # Unsupported properties are ignored, so this
                             # is the same as searching on ui
```
