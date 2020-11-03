---
title: NuGet CLI verify 명령
description: nuget.exe verify 명령에 대 한 참조
author: dtivel
ms.author: dtivel
ms.date: 03/06/2018
ms.topic: reference
ms.reviewer: rmpablos
ms.openlocfilehash: 7ce08f11195437e94bfe69883ff525e9ad3a73f0
ms.sourcegitcommit: b138bc1d49fbf13b63d975c581a53be4283b7ebf
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 11/03/2020
ms.locfileid: "93238142"
---
# <a name="verify-command-nuget-cli"></a>verify 명령 (NuGet CLI)

**적용 대상:** 패키지 사용 &bullet; **지원 버전:** 4.6 이상

패키지를 확인 합니다.

서명 된 패키지의 확인은 Mono에서 아직 지원 되지 않습니다.

## <a name="usage"></a>사용량

```cli
nuget verify <-All|-Signatures> <package(s)> [options]
```

여기서 `<package(s)>` 는 하나 이상의 `.nupkg` 파일입니다.

## <a name="nuget-verify--all"></a>nuget 확인-모두

패키지에 대해 가능한 모든 확인을 수행하도록 지정합니다.

## <a name="nuget-verify--signatures"></a>nuget verify 서명

패키지 서명 확인을 수행 하도록 지정 합니다.

## <a name="options-for-verify--signatures"></a>"서명 확인"에 대 한 옵션

- **`-CertificateFingerprint`**

  서명 된 패키지에 서명 해야 하는 인증서의 SHA-256 인증서 지문을 하나 이상 지정 합니다. 인증서 SHA-256 지문을 인증서의 SHA-256 해시입니다. 여러 입력은 세미콜론으로 구분 해야 합니다.

## <a name="options"></a>옵션

- **`-ConfigFile`**

  적용할 NuGet 구성 파일입니다. 지정 하지 않으면 `%AppData%\NuGet\NuGet.Config` (Windows) 또는 `~/.nuget/NuGet/NuGet.Config` 또는 `~/.config/NuGet/NuGet.Config` (Mac/Linux)가 사용 됩니다.

- **`-ForceEnglishOutput`**

  고정 된 영어 기반 문화권을 사용 하 여 nuget.exe을 강제로 실행 합니다.

- **`-?|-help`**

  명령에 대 한 도움말 정보를 표시 합니다.

- **`-NonInteractive`**

  사용자 입력 또는 확인에 대 한 프롬프트를 표시 하지 않습니다.

- **`-Verbosity [normal|quiet|detailed]`**

  출력에 표시 되는 세부 정보의 양을 지정 합니다. `normal` (기본값), `quiet` 또는 `detailed` 입니다.

## <a name="examples"></a>예

```cli
nuget verify -Signatures .\..\MyPackage.nupkg -CertificateFingerprint "CE40881FF5F0AD3E58965DA20A9F571EF1651A56933748E1BF1C99E537C4E039;5F874AAF47BCB268A19357364E7FBB09D6BF9E8A93E1229909AC5CAC865802E2" -Verbosity detailed

nuget verify -Signatures c:\packages\MyPackage.nupkg -CertificateFingerprint CE40881FF5F0AD3E58965DA20A9F571EF1651A56933748E1BF1C99E537C4E039

nuget verify -Signatures MyPackage.nupkg -Verbosity quiet

nuget verify -Signatures .\*.nupkg

nuget verify -All .\*.nupkg

```