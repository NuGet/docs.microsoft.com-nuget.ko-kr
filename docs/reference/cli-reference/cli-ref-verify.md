---
title: NuGet CLI verify 명령
description: Nuget.exe verify 명령에 대 한 참조입니다.
author: dtivel
ms.author: dtivel
ms.date: 03/06/2018
ms.topic: reference
ms.reviewer: rmpablos
ms.openlocfilehash: 9510f7323fe0cb860e0dbde51c1eda761846ee27
ms.sourcegitcommit: efc18d484fdf0c7a8979b564dcb191c030601bb4
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/18/2019
ms.locfileid: "68327500"
---
# <a name="verify-command-nuget-cli"></a>verify 명령(NuGet CLI)

**적용 대상:** 패키지 &bullet; 사용 **지원 버전:** 4.6 이상

패키지를 확인 합니다.

서명 된 패키지의 확인은 .NET Core, Mono 또는 비 Windows 플랫폼에서 아직 지원 되지 않습니다.

## <a name="usage"></a>사용

```cli
nuget verify <-All|-Signatures> <package(s)> [options]
```

여기서 `<package(s)>` 는 하나 `.nupkg` 이상의 파일입니다.

## <a name="nuget-verify--all"></a>nuget 확인-모두

패키지에 대해 가능한 모든 확인을 수행 하도록 지정 합니다.

## <a name="nuget-verify--signatures"></a>nuget verify 서명

패키지 서명 확인을 수행 하도록 지정 합니다.

## <a name="options-for-verify--signatures"></a>"서명 확인"에 대 한 옵션

| 옵션 | Description |
| --- | --- |
| CertificateFingerprint | 서명 된 패키지에 서명 해야 하는 인증서의 SHA-256 인증서 지문을 하나 이상 지정 합니다. 인증서 SHA-256 지문을 인증서의 SHA-256 해시입니다. 여러 입력은 세미콜론으로 구분 해야 합니다. |

## <a name="options"></a>변수

| 옵션 | 설명 |
| --- | --- |
| ConfigFile | 적용할 NuGet 설정 파일입니다. 지정하지 않으면 기본적으로 Windows에서는 `%AppData%\NuGet\NuGet.Config`, Mac이나 Linux에서는 `~/.nuget/NuGet/NuGet.Config`가 사용됩니다.|
| ForceEnglishOutput | 고정 영어 기반 문화권을 사용 하 여 nuget.exe를 실행 합니다. |
| Help | 명령어에 대한 도움말을 표시합니다. |
| Verbosity | 출력에 표시되는 세부정보의 양을 지정합니다: *정상적인*, *조용한*, *자세한*합니다. |

## <a name="examples"></a>예

```cli
nuget verify -Signatures .\..\MyPackage.nupkg -CertificateFingerprint "CE40881FF5F0AD3E58965DA20A9F571EF1651A56933748E1BF1C99E537C4E039;5F874AAF47BCB268A19357364E7FBB09D6BF9E8A93E1229909AC5CAC865802E2" -Verbosity detailed

nuget verify -Signatures c:\packages\MyPackage.nupkg -CertificateFingerprint CE40881FF5F0AD3E58965DA20A9F571EF1651A56933748E1BF1C99E537C4E039

nuget verify -Signatures MyPackage.nupkg -Verbosity quiet

nuget verify -Signatures .\*.nupkg

nuget verify -All .\*.nupkg

```