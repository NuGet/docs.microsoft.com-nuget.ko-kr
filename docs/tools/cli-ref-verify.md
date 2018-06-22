---
title: NuGet CLI 확인 명령
description: nuget.exe에 대 한 참조 확인 명령
author: dtivel
ms.author: dtivel
manager: doronm
ms.date: 03/06/2018
ms.topic: reference
ms.reviewer: rmpablos
ms.openlocfilehash: c80334104f7d8b2ccbf16ea2c11dc37b39408eeb
ms.sourcegitcommit: c8485dc61469511485367d2067b97d6f74b49f6e
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 05/23/2018
ms.locfileid: "34462854"
---
# <a name="verify-command-nuget-cli"></a>verify 명령(NuGet CLI)

**적용 대상:** 소비 패키지 &bullet; **지원 되는 버전:** 4.6 이상

패키지를 확인합니다.

서명 된 패키지 확인 모노, 또는 Windows 이외의 플랫폼에서.NET Core에서는 아직 지원 되지 않습니다.

## <a name="usage"></a>사용법

```cli
nuget verify <-All|-Signatures> <package(s)> [options]
```

여기서 `<package(s)>` 는 하나 이상의 `.nupkg` 파일입니다.

## <a name="nuget-verify--all"></a>nuget 확인-모두

패키지에서 확인 가능한 모든 작업을 수행 해야 함을 지정 합니다.

## <a name="nuget-verify--signatures"></a>nuget 서명 확인

패키지 서명 확인을 수행 해야 함을 지정 합니다.

## <a name="options-for-verify--signatures"></a>"-서명 확인"에 대 한 옵션

| 옵션 | 설명 |
| --- | --- |
| CertificateFingerprint | 로 서명 된 패키지를 서명 해야 하는 인증서 (s)의 하나 이상의 sha-256 인증서 지문을 지정 합니다. S h A-256 인증서 지문에는 인증서의 s h A-256 해시입니다. 여러 입력을 세미콜론으로 구분 된 있어야 합니다. |

## <a name="options"></a>옵션

| 옵션 | 설명 |
| --- | --- |
| ConfigFile | 적용할 NuGet 구성 파일입니다. 지정 하지 않으면 `%AppData%\NuGet\NuGet.Config` (Windows) 또는 `~/.nuget/NuGet/NuGet.Config` (Mac/Linux)가 사용 됩니다.|
| ForceEnglishOutput | Nuget.exe 고정, 영어 기반 문화권을 사용 하 여 실행을 강제로 수행 합니다. |
| 도움말 | 도움말의 명령에 대 한 정보를 표시 합니다. |
| 자세한 정도 | 출력에 표시 되는 세부 정보 수준을 지정: *일반*, *quiet*, *자세한*합니다. |

## <a name="examples"></a>예제

```cli
nuget verify -Signatures .\..\MyPackage.nupkg -CertificateFingerprint "CE40881FF5F0AD3E58965DA20A9F571EF1651A56933748E1BF1C99E537C4E039;5F874AAF47BCB268A19357364E7FBB09D6BF9E8A93E1229909AC5CAC865802E2" -Verbosity detailed

nuget verify -Signatures c:\packages\MyPackage.nupkg -CertificateFingerprint CE40881FF5F0AD3E58965DA20A9F571EF1651A56933748E1BF1C99E537C4E039

nuget verify -Signatures MyPackage.nupkg -Verbosity quiet

nuget verify -Signatures .\*.nupkg

nuget verify -All .\*.nupkg

```