---
title: "NuGet 복원 오류 및 경고 참조 | Microsoft Docs"
author: kraigb
ms.author: kraigb
manager: ghogen
ms.date: 12/13/2017
ms.topic: reference
ms.prod: nuget
ms.technology: 
ms.assetid: b76b8a00-7155-4163-b533-894086d2ef78
description: "경고 및 패키지를 복원 하는 동안 NuGet에서 발급 한 오류에 대 한 완전 한 지침"
keywords: "NuGet 오류, 경고 NuGet 진단"
ms.reviewer:
- anangaur
- karann-msft
- unniravindranathan
ms.openlocfilehash: 29eb72cbb6c095cd3aeb524fd8b28416ec5dc798
ms.sourcegitcommit: 6ccb963e065680ab2e7df1d8dd5492897fd56b04
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 01/23/2018
---
# <a name="errors-and-warnings"></a>오류 및 경고

오류 및 경고가이 항목에 설명 된 대로 번호가 매겨집니다 4.3.0 NuGet 및 관련 된 문제를 해결할 수 있도록 자세한 정보를 제공 합니다. 

오류 및 여기에 나열 된 경고에만 사용할 수 있는 [PackageReference 기반](../Consume-Packages/Package-References-in-Project-Files.md) 프로젝트와 NuGet 4.3.0입니다. 또한 NuGet를 경고를 표시 하거나 오류를 상승을 MSBuild 속성을 준수 합니다. 자세한 내용은 참조 [하는 방법: 컴파일러 경고 표시 안 함](/visualstudio/ide/how-to-suppress-compiler-warnings) Visual Studio 설명서에 있습니다.

**오류**

| 그룹화 | 오류 번호 |
| --- | --- |
| [잘못 된 입력된 오류](#invalid-input-errors) | [NU1001](#nu1001), [NU1002](#nu1002), [NU1003](#nu1003) |
| [패키지 및 프로젝트에 대 한 누락 오류](#missing-package-and-project-errors) | [NU1100](#nu1100), [NU1101](#nu1101), [NU1102](#nu1102), [NU1103](#nu1103), [NU1104](#nu1104), [NU1105](#nu1105), [ NU1106](#nu1106), [NU1107](#nu1107) (이전에 NU1607) [NU1108](#nu1108) (이전에 NU1606) |
| [호환성 오류](#compatibility-errors) | [NU1201](#nu1201), [NU1202](#nu1202), [NU1203](#nu1203), [NU1401](#nu1401) |

**경고**

| 그룹화 | 경고 번호 |
| --- | --- |
| [잘못 된 입력된 경고](#invalid-input-warnings) | [NU1501](#nu1501), [NU1502](#nu1502), [NU1503](#nu1503) |
| [예기치 않은 패키지 버전 경고](#unexpected-package-version-warnings) | [NU1601](#nu1601), [NU1602](#nu1602), [NU1603](#nu1603), [NU1604](#nu1604), [NU1605](#nu1605) |
| [해결 프로그램이 충돌 경고](#resolver-conflict-warnings) | [NU1608](#nu1608) |
| [패키지 대체 (fallback) 경고](#package-fallback-warnings) | [NU1701](#nu1701) |
| [피드 경고](#feed-warnings) | [NU1801](#nu1801) |
| [NuGet 내부 오류 및 경고](#nuget-internal-errors-and-warnings) | [NU1000](#nu1000), [NU1500](#nu1500) |

## <a name="invalid-input-errors"></a>잘못 된 입력된 오류

[NU1001](#nu1001) | [NU1002](#nu1002) | [NU1003](#nu1003)

### <a name="nu1001"></a>NU1001

| | |
| --- | --- |
| **문제** | 프로젝트는 하나 이상의 프레임 워크를 포함 하지 않습니다. |
| **일반적인 원인** | 프로젝트에 포함 되어 있지 않습니다는 `TargetFramework` 또는 `TargetFrameworks` 속성입니다. |
| **예제 메시지** | *프로젝트 projA c:\tmp\projA.csproj의 대상 프레임 워크를 지정 하지 않습니다.* |

### <a name="nu1002"></a>NU1002

| | |
| --- | --- |
| **문제** | 일반 키워드와 함께 입력의 조합이 잘못 되었습니다. |
| **일반적인 원인** | 다른 입력을 지 원하는 일반을 결합할 수 있습니다. |
| **예제 메시지** | *'CLEAR' 없습니다 다른 값과 함께에서 사용할 수* |

### <a name="nu1003"></a>NU1003

| | |
| --- | --- |
| **문제** | `PackageTargetFallback`및 `AssetTargetFallback` 자산을 선택 하기 위한 다른 동작을 제공 하 고 함께 사용할 수 없습니다. |
| **일반적인 원인** | 둘 다 `PackageTargetFallback` 및 `AssetTargetFallback` 프로젝트에 존재 합니다. |
| **예제 메시지** | *PackageTargetFallback와 AssetTargetFallback는 함께 사용할 수 없습니다. 프로젝트 환경에서 PackageTargetFallback(deprecated) 참조를 제거 합니다.* |

## <a name="missing-package-and-project-errors"></a>패키지 및 프로젝트에 대 한 누락 오류

[NU1100](#nu1100) | [NU1101](#nu1101) | [NU1102](#nu1102) | [NU1103](#nu1103) | [NU1104](#nu1104) | [NU1105](#nu1105) | [NU1106](#nu1106)

### <a name="nu1100"></a>NU1100

| | |
| --- | --- |
| **문제** | 종속성 그룹 확인할 수 있습니다. 패키지 또는 프로젝트 하지 않은 형식에 대 한 일반적인 문제입니다. |
| **일반적인 원인** | 프로젝트는 존재 하지 않는 항목에 대 한 종속성을 포함 합니다. |
| **예제 메시지** | *Net45에 대 한 System.Missing를 확인할 수 없습니다.* |

### <a name="nu1101"></a>NU1101

| | |
| --- | --- |
| **문제** | 모든 소스에서 패키지를 찾을 수 없습니다. |
| **일반적인 원인** | 올바른 패키지 원본 누락 되었거나 있는 패키지 식별자가 잘못 되었습니다. |
| **예제 메시지** | *System.Missing 패키지를 찾을 수 없습니다. 패키지 원본에이 id를 가진 존재: dotnet 코어, dotnet roslyn, nuget.org* |

### <a name="nu1102"></a>NU1102

| | |
| --- | --- |
| **문제** | 패키지 식별자를 찾았지만 소스 중 하나에서 지정 된 종속성 범위 내에서 버전을 찾을 수 없습니다. |
| **일반적인 원인** | 올바른 패키지 원본 누락 되었거나 종속성 범위가 잘못 되었습니다. 패키지와 사용자가 아니라에서 범위를 지정할 수 있습니다. 사용자는이 패키지는 프로젝트에서 직접 참조 하는 경우 사용 가능한 버전으로 전환 해야 합니다. |
| **예제 메시지** | *버전으로 NuGet.Versioning 패키지를 찾을 수 없습니다. (> = 9.0.1)<br/> -nuget.org에 30 찾을 버전 [버전 가장 가까운: 4.0.0]<br/> -dotnet buildtools에서 찾은 10 버전 [버전 가장 가까운: 4.0.0-rc-2129]<br/> -9 찾을 수 NuGetVolatile에서 버전 [버전 가장 가까운: 3.0.0-beta-00032]<br/> -0 버전 dotnet 코어 있는<br/> -dotnet roslyn에서 0 버전을 찾을 수* |

### <a name="nu1103"></a>NU1103

| | |
| --- | --- |
| **문제** | 종속성 범위에 안정적 버전을 찾지 못했습니다. 시험판 버전을 찾았지만 허용 되지 않습니다. |
| **일반적인 원인** | 프로젝트는 종속성 범위에 대 한 안정적인 버전을 지정 합니다. 사용자는 시험판 버전을 포함 하도록 버전 범위를 변경 해야 합니다. |
| **예제 메시지** | *버전과 NuGet.Versioning 안정적인 패키지를 찾을 수 없습니다. (> = 3.0.0)<br/> -dotnet buildtools에서 찾은 10 버전 [버전 가장 가까운: 4.0.0-rc-2129]<br/> -NuGetVolatile에서 찾을 9 버전 [버전 가장 가까운: 3.0.0-beta-00032] <br/> -0 버전 dotnet 코어 있는<br/> -dotnet roslyn에서 0 버전을 찾을 수* |

### <a name="nu1104"></a>NU1104

| | |
| --- | --- |
| **문제** | ProjectReference 존재 하지 않는 파일을 가리킵니다. |
| **일반적인 원인** | 프로젝트 파일에는 디스크에서 누락 되었거나는 참조가 잘못 되었습니다. |
| **예제 메시지** | *프로젝트 참조 'c:\a.csproj' 존재 하지 않습니다. 프로젝트 참조는 유효 하 고 프로젝트 파일이 있는지 확인 합니다.* |

### <a name="nu1105"></a>NU1105

| | |
| --- | --- |
| **문제** | 프로젝트 파일이 있지만에 제공 된 복원 정보가 없는 합니다. |
| **일반적인 원인** | Visual Studio에서 프로젝트가 로드 되지 않은 것을 의미할 수이 있습니다. 명령줄에서이 파일이 손상 되었거나 imports 대상 프로젝트를 읽을 수는 복원에 필요한 이후에 사용자 지정 포함 되지 않았는지를 의미할 수 있습니다. |
| **예제 메시지** | *'C:\a.csproj'에 대 한 프로젝트 정보를 읽을 수 없습니다. 프로젝트 파일이 올바르지 않거나 누락 된 대상으로 복원 하는 데 필요한 수 있습니다.* |

### <a name="nu1106"></a>NU1106

| | |
| --- | --- |
| **문제** | 종속성 제약 조건을 확인할 수 없습니다. |
| **일반적인 원인** | 패키지 범위를 제한 하는 대신 패키지의 정확한 버전에 대 한 종속성을 포함합니다. |
| **예제 메시지** | *{Id}에 대 한 충돌 하는 요청을 충족할 수 없습니다. {충돌 경로} 프레임 워크: {대상 그래프}* |

<a name="nu1107"></a> 

### <a name="nu1107-previously-nu1607"></a>NU1107 (이전에 NU1607)

| | |
| --- | --- |
| **문제** | 패키지 간에 종속성 제약 조건을 확인할 수 없습니다. |
| **일반적인 원인** | 정확한 버전에 대 한 종속성 제약 조건 사용 하 여 패키지에는 다른 패키지 버전을 필요에 따라 증가를 허용 하지 않습니다. |
| **예제 메시지** | *NuGet.Versioning에 대 한 검색 버전 충돌 합니다. 이 문제를 해결 하려면 프로젝트에서 직접 패키지를 참조 합니다.<br/>  NuGet.Packaging 3.5.0 NuGet.Versioning (3.5.0 =)-><br/> NuGet.Configuration 4.0.0 NuGet.Versioning (4.0.0 =)->* |

<a name="nu1108"></a>

### <a name="nu1108-previously-nu1606"></a>NU1108 (이전에 NU1606)

| | |
| --- | --- |
| **문제** | 순환 종속성이 발견 되었습니다. |
| **일반적인 원인** | 패키지를 제대로 작성 됩니다. |
| **예제 메시지** | *순환 발견: A-B A->* |

## <a name="compatibility-errors"></a>호환성 오류

[NU1201](#nu1201) | [NU1202](#nu1202) | [NU1203](#nu1203) | [NU1401](#nu1401)

### <a name="nu1201"></a>NU1201

| | |
| --- | --- |
| **문제** | 종속성 프로젝트는 현재 프로젝트와 호환 되는 프레임 워크를 포함 하지 않습니다. |
| **일반적인 원인** | 프로젝트의 대상 프레임 워크에는 프로젝트가 보다 더 높은 버전입니다. |
| **예제 메시지** | *프로젝트 서버 netstandard1.3와 호환 되지 않습니다 (합니다. NETStandard, Version = v1.3). 프로젝트 서버 지원:<br/> -netstandard1.6 (합니다. NETStandard, Version = v1.6)<br/> -netcoreapp1.0 (합니다. NETCoreApp, Version = v1.0)* |

### <a name="nu1202"></a>NU1202

| | |
| --- | --- |
| **문제** | 종속성 패키지는 프로젝트와 호환 되는 모든 자산을 포함 하지 않습니다. |
| **일반적인 원인** | 패키지는 프로젝트의 대상 프레임 워크를 지원 하지 않습니다. |
| **예제 메시지** | *패키지 System.ComponentModel.EventBasedAsync 4.0.11 netstandard1.3와 호환 되지 않습니다 (합니다. NETStandard, Version = v1.3). System.ComponentModel.EventBasedAsync 4.0.11 지원 패키지:<br/> -monoandroid10 (MonoAndroid, 버전 = v1.0)<br/> -monotouch10 (MonoTouch, Version = v1.0)<br/> -net45 (합니다. NETFramework, Version = v4.5)<br/> -netcore50 (합니다. NETCore, Version = v5.0)<br/> -netstandard1.0 (합니다. NETStandard, Version = v1.0)<br/> -portable net45 + win8 + w p 8 + wpa81 (합니다. NETPortable, 버전 = v0.0, 프로필 Profile259 =)<br/> -win8 (Windows, Version = v 8.0)<br/> -w p 8 (WindowsPhone, 버전 v 8.0 =)<br/> -wpa81 (이 WindowsPhoneApp, 버전 = v8.1)<br/> -xamarinios10 ( Xamarin.iOS,Version=v1.0)<br/> -xamarinmac20 (Xamarin.Mac,Version=v2.0)<br/> -xamarintvos10 (Xamarin.TVOS,Version=v1.0)<br/> -xamarinwatchos10 (Xamarin.WatchOS,Version=v1.0)*|

### <a name="nu1203"></a>NU1203

| | |
| --- | --- |
| **문제** | 패키지는 프로젝트를 지원 하지 않습니다 `RuntimeIdentifier`합니다. |
| **일반적인 원인** | 패키지는 현재 지원 하지 않는 `RuntimeIdentifier`합니다. 변경 된 `RuntimeIdentifier` 필요한 경우 프로젝트에 사용 되는 값입니다. |
| **예제 메시지** | *System.Example 1.0.0 net461에 a.dll에 대 한 compile-time 참조 어셈블리를 제공 하지만 호환 런타임 어셈블리가 없습니다.* |

### <a name="nu1401"></a>NU1401

| | |
| --- | --- |
| **문제** | 패키지 기능 또는 현재 설치 된 버전의 NuGet에서 지원 되는 프레임 워크에 필요 합니다. |
| **일반적인 원인** | 문제를 해결 하는 NuGet을 업그레이드 합니다. |
| **예제 메시지** | *'NuGet.Versioning' 패키지에는 NuGet 클라이언트 버전 '5.0.0' 필요 이상 하지만 현재 NuGet 버전은 '4.3.0'. NuGet을 업그레이드 하려면 http://docs.nuget.org/consume/installing-nuget으로 이동 하십시오.* |

## <a name="invalid-input-warnings"></a>잘못 된 입력된 경고

[NU1501](#nu1501) | [NU1502](#nu1502) | [NU1503](#nu1503)

### <a name="nu1501"></a>NU1501

| | |
| --- | --- |
| **문제** | 프로젝트 복원 작동 하려고에서 찾을 수 없습니다. |
| **일반적인 원인** | 프로젝트는 없습니다. |
| **예제 메시지** | *'C:\projects\a' 폴더에 복원할 프로젝트가 없습니다.* |

### <a name="nu1502"></a>NU1502

| | |
| --- | --- |
| **문제** | `RuntimeSupports`잘못 된 프로필을 포함합니다. |
| **일반적인 원인** | 지원 프로필에 없습니다. 한 `runtime.json` 현재 종속성 패키지의 파일입니다. |
| **예제 메시지** | *알 수 없는 호환성 프로필이: aaa* |

### <a name="nu1503"></a>NU1503

| | |
| --- | --- |
| **문제** | 종속성 프로젝트에는 NuGet의 복원 대상 가져오기 하지 않습니다. 이 NU1105와 유사 하지만 프로젝트는 생략 여기 모든 복원 실패를 유발 하는 대신 무시 합니다. 복잡 한 솔루션에서 종종 있습니다 다른 형식의 프로젝트 복원을 지원 하지 않을 수 있습니다. |
| **일반적인 원인** | 이 자동으로 복원 가져오기는 공통 props/대상 가져오지 않는 프로젝트에 대해 발생할 수 있습니다. 프로젝트를 복원할 필요가 없는 경우 무시 됩니다. |
| **예제 메시지** | *'C:\a.csproj' 프로젝트에 대 한 복원을 건너뜁니다. 프로젝트 파일이 올바르지 않거나 누락 된 대상으로 복원 하는 데 필요한 수 있습니다.* |

## <a name="unexpected-package-version-warnings"></a>예기치 않은 패키지 버전 경고

[NU1601](#nu1601) | [NU1602](#nu1602) | [NU1603](#nu1603) | [NU1604](#nu1604) | [NU1605](#nu1605)

### <a name="nu1601"></a>NU1601

| | |
| --- | --- |
| **문제** | 지정 된 프로젝트 보다 높은 버전을 직접 프로젝트 종속성 추락 되었습니다. |
| **일반적인 원인** | 다른 종속성 패키지가 더 높은 버전에 필요한 및 패키지 추락. |
| **예제 메시지** | *지정 된 종속성은 NuGet.Versioning (> = 3.5.0) 이었지만 결과적으로 NuGet.Versioning 4.0.0 합니다.* |

### <a name="nu1602"></a>NU1602

| | |
| --- | --- |
| **문제** | 패키지 종속성은 없습니다. 복원 찾을 수 없도록는 *가장 일치 하는*합니다. 각 복원 아래쪽으로 사용할 수 있는 더 낮은 버전을 검색 하려고 이동 수입니다. 즉, 복원 될 때마다 사용자 패키지 폴더에 이미 존재 하는 패키지를 사용 하는 대신 모든 소스를 확인 하려면 온라인 전환 되는 것을 의미 합니다. |
| **일반적인 원인** | 이 일반적으로 오류를 제작 하는 패키지입니다. |
| **예제 메시지** | *NuGet.Packaging 4.0.0 NuGet.Versioning (> 3.5.0) 종속성에 대 한는 경계값을 제공 하지 않습니다. 3.6.0의 일부만 가장 일치 하는 해결 되었습니다.* |

### <a name="nu1603"></a>NU1603

| | |
| --- | --- |
| **문제** | 패키지 종속성 지정 버전을 찾을 수 없습니다. 패키지에 대해 작성 된에서 다른 상위 버전 대신 사용 되었습니다.<br/><br/>즉, 복원이 찾을 수 없습니다는 *가장 일치 하는*합니다. 각 복원 아래쪽으로 사용할 수 있는 더 낮은 버전을 검색 하려고 이동 수입니다. 즉, 복원 될 때마다 사용자 패키지 폴더에 이미 존재 하는 패키지를 사용 하는 대신 모든 소스를 확인 하려면 온라인 전환 되는 것을 의미 합니다. |
| **일반적인 원인** | 패키지 소스에서 예상된 하한값 버전을 포함 하지 않습니다. 예상 패키지 해제 되지 않은 경우 오류를 제작 하는 패키지를 수 있습니다이. |
| **예제 메시지** | NuGet.Packaging 4.0.0 NuGet.Versioning에 따라 달라 집니다 (> = 4.0.0) 4.0.0를 찾을 수 없습니다. 5.0.0의 일부만 가장 일치 하는 해결 되었습니다. |

### <a name="nu1604"></a>NU1604

| | |
| --- | --- |
| **문제** | 프로젝트 종속성 배열은 하 한을 정의 하지 않습니다.<br/><br/>즉, 복원이 찾을 수 없습니다는 *가장 일치 하는*합니다. 각 복원 아래쪽으로 사용할 수 있는 더 낮은 버전을 검색 하려고 이동 수입니다. 즉, 복원 될 때마다 사용자 패키지 폴더에 이미 존재 하는 패키지를 사용 하는 대신 모든 소스를 확인 하려면 온라인 전환 되는 것을 의미 합니다. |
| **일반적인 원인** | 프로젝트의 *PackageReference* *버전* 특성 배열은 하 한을 포함 하도록 업데이트 해야 합니다. |
| **예제 메시지** | *종속성 NuGet.Versioning 프로젝트 (< = 9.0.0) doe는 경계값을 포함 하지 합니다. 일치 복원 결과 보장 하는 종속성의 버전에 배열은 하 한을 포함 합니다.* |

### <a name="nu1605"></a>NU1605

| | |
| --- | --- |
| **문제** | 종속성 패키지에는 궁극적으로 해결 하는 복원 보다 더 높은 버전의 패키지에 버전 제약 조건을 지정 합니다. |
| **일반적인 원인** | 패키지를 확인할 때 가장 가까운 우선 합니다. 그래프에 할수록 패키지 먼 패키지를 무시 있을 수 있습니다. |
| **예제 메시지** | *패키지가 다운 그레이드를 발견 했습니다: 3.5.0 4.0.0에서 NuGet.Versioning 합니다. 다른 버전을 선택 하는 프로젝트에서 직접 패키지를 참조 합니다.<br/>  NuGet.Packaging 3.5.0 NuGet.Versioning 3.5.0-><br/> NuGet.Commands 4.0.0 NuGet.Configuration-> 4.0.0 NuGet.Versioning 4.0.0->* |

## <a name="resolver-conflict-warnings"></a>해결 프로그램이 충돌 경고

### <a name="nu1608"></a>NU1608

| | |
| --- | --- |
| **문제** | 해결 패키지 종속성 제약 조건을 허용 된 것 보다 더 높습니다. 일부 경우에이 의도적인와 경고가 표시 될 수 있습니다. |
| **일반적인 원인** | 프로젝트에서 직접 참조 하는 패키지에는 다른 패키지에서 제약 조건 종속성 보다 우선 합니다.   |
| **예제 메시지** | *외부 종속성 제약 조건에서 검색 된 패키지 버전: x 1.0.0 y (1.0.0 =) 이어야 하는데 버전 2.0.0 y 해결 되었습니다.* |

## <a name="package-fallback-warnings"></a>패키지 대체 (fallback) 경고

### <a name="nu1701"></a>NU1701

| | |
| --- | --- |
| **문제** | *PackageTargetFallback/AssetTargetFallback* 패키지에서 자산을 선택 하는 데 사용 되었습니다. 이 경고를 사용자에 게 알리는 자산 100% 호환 되지 않을 수 있습니다. |
| **일반적인 원인** | 패키지는 프로젝트 프레임 워크를 지원 하지 않습니다. |
| **예제 메시지** | *패키지 'NuGet.Versioning'를 사용 하 여 '노트북 net45 + win8' 대신 프로젝트 대상 프레임 워크 'netstandard1.5' 복원 되었습니다. 이 패키지는 프로젝트와 완전히 호환 하지 못할 수 있습니다.* |

## <a name="feed-warnings"></a>피드 경고

### <a name="nu1801"></a>NU1801

| | |
| --- | --- |
| **문제** | 피드를 읽을 때 오류가 발생 했습니다 때 `IgnoreFailedSources` 설정을 true로 변환 하는 치명적이 지 않은 경고 합니다. 이 모든 메시지를 포함할 수 이며 일반 합니다. |
| **일반적인 원인** | 원본이 올바르지 않습니다. |
| **예제 메시지** | N/A |

## <a name="nuget-internal-errors-and-warnings"></a>NuGet 내부 오류 및 경고

[NU1000](#nu1000) | [NU1500](#nu1500)

### <a name="nu1000"></a>NU1000

| | |
| --- | --- |
| **문제** | NuGet에서 비 특정 내부 오류입니다. |
| **일반적인 원인** | 자세한 내용은 로그를 확인 하십시오 |

### <a name="nu1500"></a>NU1500

| | |
| --- | --- |
| **문제** | NuGet에서 비 특정 내부 경고 합니다. |
| **일반적인 원인** | 자세한 내용은 로그를 확인 하십시오 |
