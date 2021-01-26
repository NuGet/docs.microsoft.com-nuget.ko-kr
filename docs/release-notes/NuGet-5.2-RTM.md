---
title: NuGet 5.2 RTM 릴리스 정보
description: 새 기능, 버그 수정 및 Ecrs를 비롯 한 NuGet 5.2에 대 한 릴리스 정보입니다.
author: JonDouglas
ms.author: jodou
ms.date: 07/23/2019
ms.topic: conceptual
ms.openlocfilehash: 25fa1d09046a583fb987b9f3dd51a0099f4331a7
ms.sourcegitcommit: ee6c3f203648a5561c809db54ebeb1d0f0598b68
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 01/26/2021
ms.locfileid: "98776207"
---
# <a name="nuget-52-release-notes"></a>NuGet 5.2 릴리스 정보

NuGet 배포 차량:

| NuGet 버전 | Visual Studio 버전에서 사용 가능| .NET SDK에서 사용 가능|
|:---|:---|:---|
| [**5.2.0**](https://nuget.org/downloads) | [Visual Studio 2019 버전 16.2](https://visualstudio.microsoft.com/downloads/) | [2.1.80 x](https://dotnet.microsoft.com/download/dotnet-core/2.1)<sup>1</sup>, [2.2.40 x](https://dotnet.microsoft.com/download/dotnet-core/2.2)<sup>2</sup> |

<sup>1</sup> .NET Core 워크 로드와 함께 Visual Studio 2019와 함께 설치 됨 

<sup>2</sup> .NET Core 워크 로드와 함께 Visual Studio 2019을 사용 하 여 선택적으로 설치할 수 있습니다.

## <a name="summary-whats-new-in-52"></a>요약: 5.2의 새로운 기능

* Linux & Mac의 경로 문제로 인 한 NuGet 작업 실패를 야기 하는 중요 한 버그를 수정 했습니다 [#7341](https://github.com/NuGet/Home/issues/7341)

* Visual Studio의 NuGet 패키지 관리자 UI를 사용 하 여 패키지를 검색할 때 UI 응답성이 향상 되었습니다. 특히 속도가 느려지는 경우에는 특히 그렇습니다 [#8039](https://github.com/NuGet/Home/issues/8039)

* 잠금 파일 ([#8187](https://github.com/NuGet/Home/issues/8187),[#8160](https://github.com/NuGet/Home/issues/8160),[#8114](https://github.com/NuGet/Home/issues/8114),[#7840](https://github.com/NuGet/Home/issues/7840)) 및 인증 플러그 인 ([#8300](https://github.com/NuGet/Home/issues/8300),[#8271](https://github.com/NuGet/Home/issues/8271),[#8269](https://github.com/NuGet/Home/issues/8269),[#8210](https://github.com/NuGet/Home/issues/8210),[#8198](https://github.com/NuGet/Home/issues/8198),[#7845](https://github.com/NuGet/Home/issues/7845))의 다양 한 안정성 수정

### <a name="issues-fixed-in-this-release"></a>이번 릴리스에서 수정된 문제

**버그**

* 성능: 패키지 관리자 콘솔: UI 지연 업데이트 "기본 프로젝트" combobox 선택 값- [#8235](https://github.com/NuGet/Home/issues/8235)

* Perf: PM UI의 성능 향상- [#8039](https://github.com/NuGet/Home/issues/8039)

* Perf: PMC에서 기본 프로젝트를 읽을 때 UI 지연이 발생 [#6824](https://github.com/NuGet/Home/issues/6824)

* Perf: [vsfeedback] 로컬 패키지 원본에 대 한 NuGet 업데이트 탭이 동결 됨- [#6470](https://github.com/NuGet/Home/issues/6470)

* 플러그 인: NuGet이 시작 되지 않거나 조기에 종료 되 면 NuGet에서 전체 핸드셰이크 시간 제한을 대기 합니다. [#8300](https://github.com/NuGet/Home/issues/8300)

* 플러그 인: 플러그 인 시작 오류 진단 가능 개선- [#8271](https://github.com/NuGet/Home/issues/8271)

* 플러그 인: 기본 제공 플러그인의 nuget.exe 검색에 문제가 있습니다.- [#8269](https://github.com/NuGet/Home/issues/8269)

* 플러그 인: 캐시 파일을 읽을 수 없습니다. [#8210](https://github.com/NuGet/Home/issues/8210)

* 플러그 인: "작업이 취소 되었습니다." 복원 중 인증 플러그 인 오류- [#8198](https://github.com/NuGet/Home/issues/8198)

* Linux 플랫폼에서 일시적으로 검색 가능 하지 않은 플러그 인 캐시- [#7845](https://github.com/NuGet/Home/issues/7845)

* LockFile: ATF를 사용 하는 경우 잘못 된 대상 프레임 워크 같음 [#8187](https://github.com/NuGet/Home/issues/8187) 검사로 인해 false NU1004

* LockFile: 잠금 파일이 비어 있거나 형식이 잘못 된 경우 '--잠금 모드 ' 복원 플래그가 적용 되지 않습니다. [#8160](https://github.com/NuGet/Home/issues/8160)

* LockFile: 패키지 잠금 파일- [#8114](https://github.com/NuGet/Home/issues/8114) 에서 사용자 지정 어셈블리 이름을 사용 하는 프로젝트를 소문자로 표시 하지 않습니다.

* LockFile: 잠금 파일에서 프로젝트 참조를 소문자로 설정- [#7840](https://github.com/NuGet/Home/issues/7840)

* 복원: 변조 된 서명 된 패키지를 설치 하면 여러 번의 실패 한 설치 시도가 발생 합니다 (반복 된 출력 포함). [#8175](https://github.com/NuGet/Home/issues/8175)

* VS: 솔루션 사용자 옵션은 NuGet 업데이트 후 deserialize 되지 않습니다.- [#8166](https://github.com/NuGet/Home/issues/8166)

* dotnet-list-단위 테스트 프로젝트의 패키지에서 오류를 반환 [#8154](https://github.com/NuGet/Home/issues/8154)

* VS 설치 관리자에 대 한 NuGet 패키지 그룹 만들기-일부 VSIX 설정 문제 해결- [#8033](https://github.com/NuGet/Home/issues/8033)

* GeneratePackageOnBuild는 NoBuild를 설정 하면 안 됩니다. - [#7801](https://github.com/NuGet/Home/issues/7801)

* 새 옵션인 "-기호 Packageformat snupkg"는 nuspec 파일에 명시적 어셈블리 참조 [#7638](https://github.com/NuGet/Home/issues/7638) 요소가 포함 된 경우 오류를 생성 합니다.

* Nuget.exe (498, 5): 오류: ' [#7341](https://github.com/NuGet/Home/issues/7341) /tmp/NuGetScratch ' 경로의 일부를 찾을 수 없습니다.

**DCR:**

* PackageDownload가 지원 됨을 나타내는 msbuild 속성을 추가 [#8106](https://github.com/NuGet/Home/issues/8106)

* FrameworkReference FrameworkReference를 통해 종속성 흐름을 표시 하지 않습니다. PrivateAssets- [#7988](https://github.com/NuGet/Home/issues/7988)

* 패키지 외부에서 runtime.js제공 하는 메커니즘- [#7351](https://github.com/NuGet/Home/issues/7351)

**[이 릴리스에서 해결 된 모든 문제 목록-5.2 RTM](https://github.com/nuget/home/issues?q=is%3Aissue+is%3Aclosed+milestone%3A%225.2")**


