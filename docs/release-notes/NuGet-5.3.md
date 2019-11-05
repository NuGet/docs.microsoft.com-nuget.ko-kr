---
title: NuGet 5.3 릴리스 정보
description: 새 기능, 버그 수정 및 Ecrs를 비롯 한 NuGet 5.3에 대 한 릴리스 정보입니다.
author: karann-msft
ms.author: karann
ms.date: 09/06/2019
ms.topic: conceptual
ms.openlocfilehash: e77219d355f73f3bf01f68283ffb2759813af563
ms.sourcegitcommit: 39f2ae79fbbc308e06acf67ee8e24cfcdb2c831b
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 11/05/2019
ms.locfileid: "73611321"
---
# <a name="nuget-53-release-notes"></a>NuGet 5.3 릴리스 정보

NuGet 배포 차량:

| NuGet 버전 | Visual Studio 버전에서 사용 가능| .NET SDK에서 사용 가능|
|:---|:---|:---|
| [**5.3.0**](https://nuget.org/downloads) | [Visual Studio 2019 버전 16.3](https://visualstudio.microsoft.com/downloads/) | [3.0.100](https://dotnet.microsoft.com/download/dotnet-core/3.0)<sup>1</sup> |
| [**5.3.1**](https://nuget.org/downloads) | [Visual Studio 2019 버전 16.3.6](https://visualstudio.microsoft.com/downloads/) | [이후 버전: 3.0.101](https://dotnet.microsoft.com/download/dotnet-core/3.0) |

<sup>1</sup> .NET Core 워크 로드와 함께 Visual Studio 2019와 함께 설치 됨

## <a name="summary-whats-new-in-53"></a>요약: 5.3의 새로운 기능

* 패키지 아이콘은 외부 URL이 필요 하지 않고 [패키지에 포함 될 수 있습니다](../reference/msbuild-targets.md#packing-an-icon-image-file). - [#352](https://github.com/NuGet/Home/issues/352)

* 패키지에 대 한 SHA 추적 및 적용을 통한 보안 향상- [#7281](https://github.com/NuGet/Home/issues/7281)

* 사용 되지 않는/레거시 NuGet 패키지의 사용 중단을 사용 하도록 설정 [#2867](https://github.com/NuGet/Home/issues/2867) | [블로그 게시물](https://devblogs.microsoft.com/nuget/deprecating-packages-on-nuget-org/) | [문서](https://docs.microsoft.com/nuget/nuget-org/deprecate-packages)

### <a name="issues-fixed-in-this-release"></a>이번 릴리스에서 수정된 문제

**버그**

* 3\.0.100-preview9 SDK로 생성 된 NuGet 패키지는 2.2 SDK 사용자가 사용할 수 없습니다. 표준 시간대에 따라 [#8603](https://github.com/NuGet/Home/issues/8603)

* "경로에 문자가 있습니다." 오류가 발생 하면 `nuget restore` [#8168](https://github.com/NuGet/Home/issues/8168) 에서 "경로에 잘못 된 문자가 있습니다.

* VS: 어셈블리는 부분적으로 ngen 되지 않고 완전히 ngen 됩니다 [#8513](https://github.com/NuGet/Home/issues/8513)

* 메모리 사용 줄이기 (이벤트 구독 취소)- [#8471](https://github.com/NuGet/Home/issues/8471)

* "Error_UnableToFindProjectInfo" 메시지가 문법적으로 올바르지 않습니다.- [#8441](https://github.com/NuGet/Home/issues/8441)

* NU1403 개선-모든 패키지의 유효성을 검사 하 고 예상/실제 sha 값을 포함 합니다.- [#8424](https://github.com/NuGet/Home/issues/8424)

* `NuGetPackageManager.PreviewUpdatePackagesAsync` - 의 여러 열거형 [#8401](https://github.com/NuGet/Home/issues/8401)

* PluginProcess에서 "공용-> 내부" 변경 내용 되돌리기- [#8390](https://github.com/NuGet/Home/issues/8390)

* IVsPackageSourceProvider. GetSources (...)에 잘못 된 예외 동작이 있습니다.- [#8383](https://github.com/NuGet/Home/issues/8383)

* PluginManager 생성자를 다시 공용으로 설정- [#8379](https://github.com/NuGet/Home/issues/8379)

* PM UI의 새로 고침 빈도를 추적 하는 메트릭- [#8369](https://github.com/NuGet/Home/issues/8369)

* 패키지 관리자 UI를 통해 설치할 때 UI 새로 고침 수 줄이기- [#8358](https://github.com/NuGet/Home/issues/8358)

* 원격 분석: datetime 값은 문화권별 형식을 사용 합니다. [#8351](https://github.com/NuGet/Home/issues/8351)

* 패키지 관리자 UI의 찾아보기 탭에서 UI 새로 고침 축소 #6570- [#8339](https://github.com/NuGet/Home/issues/8339)

* [테스트 실패] "구성 파일을 구문 분석할 수 없습니다." 메시지가 표시 되 면 두 번 [#8320](https://github.com/NuGet/Home/issues/8320)

* 고객 수정 (패키지에 필요한 nuspec 파일이 누락 됨)을 설명 하는 좋은 doc 페이지로 NU5037 오류 발생- [#8291](https://github.com/NuGet/Home/issues/8291)

* 프로젝트의 RuntimeIdentifier가 변경 되 면 잠금 모드 복원이 실패 [#8260](https://github.com/NuGet/Home/issues/8260)

* VS 지연- [#8156](https://github.com/NuGet/Home/issues/8156) 에서 설정을 읽습니다.

* `Nuget sources add`의 회귀로 인해 "': ' 문자, 16 진수 값 0x3A를 이름" 오류- [#7948](https://github.com/NuGet/Home/issues/7948) 에 포함할 수 없습니다.

* NuGet 플러그 인 자격 증명 공급자-프로세스 창을 숨깁니다.- [#7511](https://github.com/NuGet/Home/issues/7511)

* PackagePathResolver 적용은 절대 경로- [#7349](https://github.com/NuGet/Home/issues/7349)

* 패키지 관리자 UI의 설치 및 업데이트 탭에서 UI 새로 고침 축소- [#6570](https://github.com/NuGet/Home/issues/6570)

**DCR:**

* NetStandard 2.1에 매핑되도록 Xamarin 프레임 워크 업데이트- [#8368](https://github.com/NuGet/Home/issues/8368)

* 설치/업데이트- [#8324](https://github.com/NuGet/Home/issues/8324) 에 대 한 패키지 관리자 "미리 보기 창"의 콘텐츠 복사 사용

* Proj 파일에서 복원 사용- [#8212](https://github.com/NuGet/Home/issues/8212)

* `NUGET_NETFX_PLUGIN_PATHS` 및 `NUGET_NETCORE_PLUGIN_PATHS`를 도입 하 여 같은 시간에 두 구성을 모두 지원 [#8151](https://github.com/NuGet/Home/issues/8151)

* 버전 특성을 통해 PackageDownload에 여러 버전 사용- [#8074](https://github.com/NuGet/Home/issues/8074)

* Nuget.exe 디렉터리 및-PackageDirectory 옵션을 nuget.exe pack에 추가- [#7163](https://github.com/NuGet/Home/issues/7163)

**[이 릴리스에서 해결 된 모든 문제 목록-5.3](https://github.com/nuget/home/issues?q=is%3Aissue+is%3Aclosed+milestone%3A%225.3")**

## <a name="summary-whats-new-in-531"></a>요약: 5.3.1의 새로운 기능

* 플러그 인: 작업이 취소 되었습니다. 취소가 플러그 인 인스턴스화에 영향을 줌- [#8648](https://github.com/NuGet/Home/issues/8648)

* 자격 증명 공급자를 사용 하는 경우 복원 작업을 한 프로세스에서 두 번 안전 하 게 실행할 수 없습니다.- [#8688](https://github.com/NuGet/Home/issues/8688)
