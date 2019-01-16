---
title: NuGet CLI 신뢰할 수 있는 서명자 명령
description: Nuget.exe 신뢰할 수 있는 서명자 명령에 대 한 참조
author: patbel
ms.author: patbel
ms.date: 11/12/2018
ms.topic: reference
ms.reviewer: rmpablos
ms.openlocfilehash: ee4ffaa7e250cdbf313476fd794a8d87c80b69f9
ms.sourcegitcommit: 6ea2ff8aaf7743a6f7c687c8a9400b7b60f21a52
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 01/16/2019
ms.locfileid: "54324710"
---
# <a name="trusted-signers-command-nuget-cli"></a>신뢰할 수 있는 서명자 명령 (NuGet CLI)

**적용 대상:** 소비 패키지 &bullet; **지원 되는 버전:** 4.9.1+

NuGet 구성에 신뢰할 수 있는 서명자를 가져오거나 설정 합니다. 추가 사용법에 대한 정보는 [NuGet 동작 구성](../consume-packages/configuring-nuget-behavior.md)을 통해 확인할 수 있습니다. Nuget.config 스키마에서 참조 하는 등을 표시 하는 방법에 대 한 내용은 합니다 [NuGet 구성 파일 참조](../reference/nuget-config-file.md)합니다.

## <a name="usage"></a>사용법

```cli
nuget trusted-signers <list|add|remove|sync> [options]
```

없으면 `list|add|remove|sync` 지정 된 경우이 명령은 기본적으로 `list`입니다.

## <a name="nuget-trusted-signers-list"></a>nuget 신뢰할 수 있는 서명자 목록

구성에 대 한 모든 신뢰할 수 있는 서명자를 나열합니다. 이 옵션에는 모든 인증서 포함 됩니다 (지문 및 지문 알고리즘) 각 서명자 수 있습니다. 인증서를 앞에 있으면 `[U]`, 인증서 항목에는 의미 `allowUntrustedRoot` 로 `true`합니다.

다음은이 명령의 예제 출력:

```cli
$ nuget trusted-signers
Registered trusted signers:


 1.   nuget.org [repository]
      Service Index: https://api.nuget.org/v3/index.json
      Certificate fingerprint(s):
        SHA256 - 0E5F38F57DC1BCC806D8494F4F90FBCEDD988B46760709CBEEC6F4219AA6157D

 2.   microsoft [author]
      Certificate fingerprint(s):
        SHA256 - 3F9001EA83C560D712C24CF213C3D312CB3BFF51EE89435D3430BD06B5D0EECE

 3.   myUntrustedAuthorSignature [author]
      Certificate fingerprint(s):
        [U] SHA256 - 518F9CF082C0872025EFB2587B6A6AB198208F63EA58DD54D2B9FF6735CA4434
        
```

## <a name="nuget-trusted-signers-add-options"></a>nuget trusted-signers add [options]

구성에 지정 된 이름의 신뢰할 수 있는 서명자를 추가합니다. 이 옵션은 신뢰할 수 있는 작성자 또는 리포지토리를 추가 하려면 다른 제스처입니다.

## <a name="options-for-add-based-on-a-package"></a>패키지를 기반으로 하는 추가 옵션

```cli
nuget trusted-signers add <package(s)> -Name <name> [options]
```

여기서 `<package(s)>` 는 하나 이상의 `.nupkg` 파일입니다.

| 옵션 | 설명 |
| --- | --- |
| 만든 이 | 패키지의 작성자 서명의 신뢰할 수 있음을 지정 합니다. |
| 리포지토리 | 리포지토리 서명 하거나 연대 서명 된 패키지의을 신뢰할 수 있음을 지정 합니다. |
| AllowUntrustedRoot | 신뢰할 수 있는 서명자 인증서 신뢰할 수 없는 루트에 연결할 수 있어야 하는 경우를 지정 합니다. |
| Owners | 저장소의 신뢰를 더욱 제한 하려면 신뢰할 수 있는 소유자의 세미콜론으로 구분 된 목록입니다. 사용 하는 경우에 유효 합니다 `-Repository` 옵션입니다. |

둘 다 제공할 `-Author` 고 `-Repository` 동시에 지원 되지 않습니다.

## <a name="options-for-add-based-on-a-service-index"></a>서비스 인덱스를 기준으로 하는 추가 옵션

```cli
nuget trusted-signers add -Name <name> [options]
```

_참고_: 이 옵션에서 신뢰할 수 있는 리포지토리를 추가 합니다. 

| 옵션 | 설명 |
| --- | --- |
| ServiceIndex | 신뢰할 수 있는 리포지토리의 V3 서비스 인덱스를 지정 합니다. 이 리포지토리는 리포지토리 서명을 리소스를 지원 해야 합니다. 같은 패키지 원본에 대해 명령이 표시 됩니다 제공 되지 않으면 `-Name` 및 여기에서 서비스 인덱스를 가져옵니다. |
| AllowUntrustedRoot | 신뢰할 수 있는 서명자 인증서 신뢰할 수 없는 루트에 연결할 수 있어야 하는 경우를 지정 합니다. |
| Owners | 저장소의 신뢰를 더욱 제한 하려면 신뢰할 수 있는 소유자의 세미콜론으로 구분 된 목록입니다. |

## <a name="options-for-add-based-on-the-certificate-information"></a>인증서 정보를 기반으로 하는 추가 옵션

```cli
nuget trusted-signers add -Name <name> [options]
```

_참고_: 지정 된 이름의 신뢰할 수 있는 서명자가 이미 있는 경우 인증서 항목은 서명자에 추가 됩니다. 그렇지 않으면 신뢰할 수 있는 작성자 만들어집니다 인증서 항목을 사용 하 여에서 인증서 정보를 제공 합니다.

| 옵션 | 설명 |
| --- | --- |
| CertificateFingerprint | 서명 된 패키지는 인증서의 지문을 사용 하 여 서명 해야 하는 인증서를 지정 합니다. 인증서 지문은 인증서의 해시입니다. 이 해시 해야 계산에 사용 된 해시 알고리즘의 지정 된 `FingerprintAlgorithm` 옵션입니다. |
| FingerprintAlgorithm | 인증서 지문을 계산 하는 데 해시 알고리즘을 지정 합니다. 기본값은 `SHA256`입니다. 값이 지원 됨 `SHA256`, `SHA384` 및 `SHA512` |
| AllowUntrustedRoot | 신뢰할 수 있는 서명자 인증서 신뢰할 수 없는 루트에 연결할 수 있어야 하는 경우를 지정 합니다. |

## <a name="nuget-trusted-signers-remove--name-name"></a>nuget 신뢰할 수 있는 서명자 이름을 제거 <name>

지정 된 이름과 일치 하는 모든 신뢰할 수 있는 서명자를 제거 합니다.

## <a name="nuget-trusted-signers-sync--name-name"></a>nuget trusted-signers sync -Name <name>

최신 목록을 업데이트 하려면 현재 신뢰할 수 있는 저장소에 사용 되는 인증서 요청을 신뢰할 수 있는 서명자의 기존 인증서 목록입니다.

_참고_: 이 제스처는 인증서의 현재 목록을 삭제 하 고 리포지토리에서 최신 목록을 바꿉니다.

## <a name="options"></a>옵션

| 옵션 | 설명 |
| --- | --- |
| ConfigFile | 수정할 NuGet 구성 파일입니다. 지정하지 않으면 기본적으로 Windows에서는 `%AppData%\NuGet\NuGet.Config`, Mac이나 Linux에서는 `~/.nuget/NuGet/NuGet.Config`가 사용됩니다.|
| ForceEnglishOutput | 고정 영어 기반 문화권을 사용 하 여 실행할 nuget.exe를 강제로 수행 합니다. |
| 도움말 | 명령어에 대한 도움말을 표시합니다. |
| 자세한 정도 | 출력에 표시되는 세부정보의 양을 지정합니다: *정상적인*, *조용한*, *자세한*합니다. |

## <a name="examples"></a>예제

```cli
nuget trusted-signers list

nuget trusted-signers Add -Name existingSource

nuget trusted-signers Add -Name trustedRepo -ServiceIndex https://trustedRepo.test/v3ServiceIndex

nuget trusted-signers Add -Name author1 -CertificateFingerprint CE40881FF5F0AD3E58965DA20A9F571EF1651A56933748E1BF1C99E537C4E039 -FingerprintAlgorithm SHA256

nuget trusted-signers Add -Repository .\..\MyRepositorySignedPackage.nupkg -Name TrustedRepo

nuget-trusted-signers Remove -Name TrustedRepo

nuget-trusted-signers Sync -Name TrustedRepo
```
