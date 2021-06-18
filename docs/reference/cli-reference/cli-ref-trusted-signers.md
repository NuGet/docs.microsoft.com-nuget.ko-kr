---
title: NuGet CLI trusted-signers 명령
description: nuget.exe trusted-signers 명령에 대한 참조
author: patbel
ms.author: patbel
ms.date: 11/12/2018
ms.topic: reference
ms.reviewer: rmpablos
ms.openlocfilehash: a5f3564af8b96dfa673d2252aea2e77a79c184a4
ms.sourcegitcommit: f3d98c23408a4a1c01ea92fc45493fa7bd97c3ee
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 06/17/2021
ms.locfileid: "112323592"
---
# <a name="trusted-signers-command-nuget-cli"></a>trusted-signers 명령(NuGet CLI)

**적용 대상:** 패키지 사용 &bullet; **지원 버전:** 4.9.1 이상

NuGet 구성에 대한 신뢰할 수 있는 서명자를 가져오거나 설정합니다. 추가 사용법은 [일반적인 NuGet 구성을 참조하세요.](../../consume-packages/configuring-nuget-behavior.md) nuget.config 스키마의 모양에 대한 자세한 내용은 [NuGet 구성 파일 참조](../nuget-config-file.md)를 참조하세요.

## <a name="usage"></a>사용

```cli
nuget trusted-signers <list|add|remove|sync> [options]
```

를 지정하지 않으면 `list|add|remove|sync` 명령의 기본값은 입니다. `list`

## <a name="nuget-trusted-signers-list"></a>nuget trusted-signers list

구성에서 신뢰할 수 있는 모든 서명자를 나열합니다. 이 옵션에는 각 서명자가 가진 모든 인증서(지문 및 지문 알고리즘 포함)가 포함됩니다. 인증서에 이전 가 있는 경우 `[U]` 인증서 항목이 `allowUntrustedRoot` 로 설정되었다는 의미입니다. `true`

다음은 이 명령의 예제 출력입니다.

```cli
$ nuget trusted-signers
Registered trusted signers:


 1.   nuget.org [repository]
      Service Index: https://api.nuget.org/v3/index.json
      Certificate fingerprint(s):
        SHA256 - 0E5F38F57DC1BCC806D8494F4F90FBCEDD988B46760709CBEEC6F4219AA6157D
        SHA256 - 5A2901D6ADA3D18260B9C6DFE2133C95D74B9EEF6AE0E5DC334C8454D1477DF4

 2.   microsoft [author]
      Certificate fingerprint(s):
        SHA256 - 3F9001EA83C560D712C24CF213C3D312CB3BFF51EE89435D3430BD06B5D0EECE
        SHA256 - AA12DA22A49BCE7D5C1AE64CC1F3D892F150DA76140F210ABD2CBFFCA2C18A27

 3.   myUntrustedAuthorSignature [author]
      Certificate fingerprint(s):
        [U] SHA256 - 518F9CF082C0872025EFB2587B6A6AB198208F63EA58DD54D2B9FF6735CA4434
        
```

## <a name="nuget-trusted-signers-add-options"></a>nuget trusted-signers add [options]

지정된 이름의 신뢰할 수 있는 서명자가 구성에 추가됩니다. 이 옵션에는 신뢰할 수 있는 작성자 또는 리포지토리를 추가하는 다른 제스처가 있습니다.

## <a name="options-for-add-based-on-a-package"></a>패키지 기반 추가 옵션

```cli
nuget trusted-signers add <package> -Name <name> [options]
```

여기서 `<package>` 은 하나의 서명된 `.nupkg` 파일입니다.

- **`-Author`**

  서명된 패키지의 작성자 서명을 신뢰해야 임을 지정합니다.

- **`-AllowUntrustedRoot`**

  신뢰할 수 있는 서명자의 인증서를 신뢰할 수 없는 루트에 연결하도록 허용할지 지정합니다.

- **`-Owners`**

  리포지토리의 신뢰를 추가로 제한하기 위해 세미콜론으로 구분된 신뢰할 수 있는 소유자 목록입니다. 옵션을 사용하는 경우에만 `-Repository` 유효합니다.

- **`-Repository`**

  서명된 패키지의 리포지토리 서명 또는 서명이 신뢰되어야 함을 지정합니다.

및 를 동시에 제공하는 `-Author` `-Repository` 것은 지원되지 않습니다.

## <a name="options-for-add-based-on-a-service-index"></a>서비스 인덱스 기반 추가 옵션

```cli
nuget trusted-signers add -Name <name> [options]
```

_참고:_ 이 옵션은 신뢰할 수 있는 리포지토리만 추가합니다. 

- **`-AllowUntrustedRoot`**

  신뢰할 수 있는 서명자의 인증서를 신뢰할 수 없는 루트에 연결하도록 허용할지 지정합니다.

- **`-Owners`**

  리포지토리의 신뢰를 추가로 제한하기 위해 세미콜론으로 구분된 신뢰할 수 있는 소유자 목록입니다.

- **`-ServiceIndex`**

  신뢰할 리포지토리의 V3 서비스 인덱스를 지정합니다. 이 리포지토리는 리포지토리 서명 리소스를 지원해야 합니다. 제공되지 않으면 명령은 동일한 패키지 원본을 찾고 `-Name` 해당 위치에서 서비스 인덱스 를 얻습니다.

## <a name="options-for-add-based-on-the-certificate-information"></a>인증서 정보를 기반으로 추가하기 위한 옵션

```cli
nuget trusted-signers add -Name <name> [options]
```

_참고:_ 지정된 이름의 신뢰할 수 있는 서명자가 이미 있는 경우 인증서 항목이 해당 서명자에게 추가됩니다. 그렇지 않으면 지정된 인증서 정보의 인증서 항목을 통해 신뢰할 수 있는 작성자가 만들어집니다.


- **`-AllowUntrustedRoot`**

  신뢰할 수 있는 서명자의 인증서를 신뢰할 수 없는 루트에 연결하도록 허용할지 지정합니다.

- **`-CertificateFingerprint`**

  서명된 패키지에 서명해야 하는 인증서의 인증서 지문을 지정합니다. 인증서 지문은 인증서의 해시입니다. 이 해시를 계산하는 데 사용되는 해시 알고리즘은 옵션에서 지정해야 `FingerprintAlgorithm` 합니다.

- **`-FingerprintAlgorithm`**

  인증서 지문을 계산하는 데 사용되는 해시 알고리즘을 지정합니다. 기본값은 `SHA256`입니다. 지원되는 값은 `SHA256` , `SHA384` 및 `SHA512` 입니다.

## <a name="nuget-trusted-signers-remove--name-name"></a>nuget trusted-signers remove -Name \<name\>

지정된 이름과 일치하는 신뢰할 수 있는 서명자를 제거합니다.

## <a name="nuget-trusted-signers-sync--name-name"></a>nuget trusted-signers sync -Name \<name\>

신뢰할 수 있는 서명자의 기존 인증서 목록을 업데이트하기 위해 현재 신뢰할 수 있는 리포지토리에서 사용되는 최신 인증서 목록을 요청합니다.

_참고:_ 이 제스처는 현재 인증서 목록을 삭제하고 리포지토리의 최신 목록으로 대체합니다.

## <a name="options"></a>옵션

- **`-ConfigFile`**

  적용할 NuGet 구성 파일입니다. 지정하지 않으면 `%AppData%\NuGet\NuGet.Config` (Windows) `~/.nuget/NuGet/NuGet.Config` 또는 `~/.config/NuGet/NuGet.Config` (Mac/Linux)가 사용됩니다.

- **`-ForceEnglishOutput`**

  고정 영어 기반 문화권으로 nuget.exe 강제로 실행합니다.

- **`-?|-help`**

  명령에 대한 도움말 정보를 표시합니다.

- **`-Name`**

  신뢰할 수 있는 서명자의 이름입니다.

- **`-NonInteractive`**

  사용자 입력 또는 확인에 대한 프롬프트를 표시하지 않습니다.

- **`-Verbosity [normal|quiet|detailed]`**

  (기본값), 또는 출력에 표시되는 세부 정보의 양을 `normal` `quiet` `detailed` 지정합니다.


## <a name="examples"></a>예

```cli
nuget trusted-signers list

nuget trusted-signers Add -Name existingSource

nuget trusted-signers Add -Name trustedRepo -ServiceIndex https://trustedRepo.test/v3ServiceIndex

nuget trusted-signers Add -Name author1 -CertificateFingerprint CE40881FF5F0AD3E58965DA20A9F571EF1651A56933748E1BF1C99E537C4E039 -FingerprintAlgorithm SHA256

nuget trusted-signers Add -Repository .\..\MyRepositorySignedPackage.nupkg -Name TrustedRepo

nuget trusted-signers Remove -Name TrustedRepo

nuget trusted-signers Sync -Name TrustedRepo
```
