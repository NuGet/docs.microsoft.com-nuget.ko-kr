---
title: NuGet CLI 명령을 확인 | Microsoft Docs
author: dtivel
ms.author: dtivel
manager: doronm
ms.date: 03/06/2018
ms.topic: reference
ms.prod: nuget
ms.technology: ''
description: nuget.exe에 대 한 참조 확인 명령
keywords: nuget 참조를 확인, 확인 명령
ms.reviewer:
- karann
- rmpablos
ms.workload:
- dotnet
- aspnet
ms.openlocfilehash: 4423e491e0ab5dc1e13982440db42bc9b0e85c38
ms.sourcegitcommit: beb229893559824e8abd6ab16707fd5fe1c6ac26
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 03/28/2018
---
# <a name="verify-command-nuget-cli"></a>명령 (NuGet CLI)를 확인 합니다.

**적용 대상:** 소비 패키지 &bullet; **지원 되는 버전:** 4.6 이상

패키지를 확인합니다.

## <a name="usage"></a>사용법

```cli
nuget verify <package(s)> [options]
```

여기서 `<package(s)>` 는 하나 이상의 `.nupkg` 파일입니다.

## <a name="options"></a>옵션

| 옵션 | 설명 |
| --- | --- |
| 모두 | 패키지에서 확인 가능한 모든 작업을 수행 해야 함을 지정 합니다. |
| CertificateFingerprint | 로 서명 된 패키지를 서명 해야 하는 인증서 (s)의 하나 이상의 sha-256 인증서 지문을 지정 합니다. S h A-256 인증서 지문에는 인증서의 s h A-256 해시입니다. 여러 입력을 세미콜론으로 구분 된 있어야 합니다. |
| ConfigFile | 적용할 NuGet 구성 파일입니다. 지정 하지 않으면 `%AppData%\NuGet\NuGet.Config` (Windows) 또는 `~/.nuget/NuGet/NuGet.Config` (Mac/Linux)가 사용 됩니다.|
| ForceEnglishOutput | Nuget.exe 고정, 영어 기반 문화권을 사용 하 여 실행을 강제로 수행 합니다. |
| 도움말 | 도움말의 명령에 대 한 정보를 표시 합니다. |
| NonInteractive | 사용자 입력 또는 확인에 대 한 프롬프트를 표시 하지 않습니다. |
| 서명 | 패키지 서명 확인을 수행 해야 함을 지정 합니다. |
| 자세한 정도 | 출력에 표시 되는 세부 정보 수준을 지정: *일반*, *quiet*, *자세한*합니다. |

## <a name="examples"></a>예제

```cli
nuget verify -Signatures .\..\MyPackage.nupkg -CertificateFingerprint "CE40881FF5F0AD3E58965DA20A9F571EF1651A56933748E1BF1C99E537C4E039;5F874AAF47BCB268A19357364E7FBB09D6BF9E8A93E1229909AC5CAC865802E2" -Verbosity detailed

nuget verify -Signatures c:\packages\MyPackage.nupkg -CertificateFingerprint CE40881FF5F0AD3E58965DA20A9F571EF1651A56933748E1BF1C99E537C4E039

nuget verify -Signatures MyPackage.nupkg -Verbosity quiet

nuget verify -Signatures .\*.nupkg
```