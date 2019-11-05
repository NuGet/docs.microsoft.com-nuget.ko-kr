---
title: NuGet CLI 신뢰-서명자 명령
description: Nuget.exe trusted-서명자 명령에 대 한 참조
author: patbel
ms.author: patbel
ms.date: 11/12/2018
ms.topic: reference
ms.reviewer: rmpablos
ms.openlocfilehash: 94c4c6524c1870898893b80be914477af5a14e8b
ms.sourcegitcommit: 39f2ae79fbbc308e06acf67ee8e24cfcdb2c831b
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 11/05/2019
ms.locfileid: "73610343"
---
# <a name="trusted-signers-command-nuget-cli"></a>trusted-서명자 명령 (NuGet CLI)

**적용 대상:** 패키지 사용 &bullet; **지원 되는 버전:** 4.9.1 +

NuGet 구성에 대해 신뢰할 수 있는 서명자를 가져오거나 설정 합니다. 추가 사용에 대해서는 [일반적인 NuGet 구성](../../consume-packages/configuring-nuget-behavior.md)을 참조 하세요. Nuget 스키마의 모양에 대 한 자세한 내용은 [nuget 구성 파일 참조](../nuget-config-file.md)를 참조 하세요.

## <a name="usage"></a>사용 현황

```cli
nuget trusted-signers <list|add|remove|sync> [options]
```

`list|add|remove|sync` 지정 하지 않으면 기본적으로 명령이 `list`됩니다.

## <a name="nuget-trusted-signers-list"></a>nuget 신뢰할 수 있는 서명자 목록

구성의 모든 신뢰할 수 있는 서명자를 나열 합니다. 이 옵션에는 각 서명자가 있는 모든 인증서 (지문 및 지문 알고리즘 포함)가 포함 됩니다. 인증서에 이전 `[U]`있는 경우 인증서 항목 `allowUntrustedRoot` `true`으로 설정 되어 있음을 의미 합니다.

다음은이 명령의 출력 예제입니다.

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

## <a name="nuget-trusted-signers-add-options"></a>nuget 신뢰할 수 있는 서명자 add [options]

지정 된 이름의 신뢰할 수 있는 서명자를 구성에 추가 합니다. 이 옵션은 신뢰할 수 있는 작성자 또는 리포지토리를 추가 하는 다른 제스처를 포함 합니다.

## <a name="options-for-add-based-on-a-package"></a>패키지 기반 추가 옵션

```cli
nuget trusted-signers add <package(s)> -Name <name> [options]
```

여기서 `<package(s)>`은 하나 이상의 `.nupkg` 파일입니다.

| 옵션 | 설명 |
| --- | --- |
| 만든 이 | 패키지의 작성자 서명을 신뢰할 수 있도록 지정 합니다. |
| 리포지토리 | 패키지의 저장소 서명 또는 연대 서명을 신뢰할 수 있도록 지정 합니다. |
| Allowunroot | 신뢰할 수 있는 서명자에 대 한 인증서를 신뢰할 수 없는 루트에 연결할 수 있는지 여부를 지정 합니다. |
| Owners | 리포지토리의 신뢰를 추가로 제한 하는 신뢰할 수 있는 소유자의 세미콜론으로 구분 된 목록입니다. `-Repository` 옵션을 사용 하는 경우에만 유효 합니다. |

동시에 `-Author`와 `-Repository`를 모두 제공 하는 것은 지원 되지 않습니다.

## <a name="options-for-add-based-on-a-service-index"></a>서비스 인덱스를 기반으로 하는 추가 옵션

```cli
nuget trusted-signers add -Name <name> [options]
```

_참고_:이 옵션은 신뢰할 수 있는 리포지토리만 추가 합니다. 

| 옵션 | 설명 |
| --- | --- |
| ServiceIndex | 신뢰할 리포지토리의 V3 서비스 인덱스를 지정 합니다. 이 리포지토리는 리포지토리 서명 리소스를 지원 해야 합니다. 제공 되지 않은 경우이 명령은 동일한 `-Name`의 패키지 소스를 검색 하 여 해당 위치에서 서비스 인덱스를 가져옵니다. |
| Allowunroot | 신뢰할 수 있는 서명자에 대 한 인증서를 신뢰할 수 없는 루트에 연결할 수 있는지 여부를 지정 합니다. |
| Owners | 리포지토리의 신뢰를 추가로 제한 하는 신뢰할 수 있는 소유자의 세미콜론으로 구분 된 목록입니다. |

## <a name="options-for-add-based-on-the-certificate-information"></a>인증서 정보에 따라 추가 옵션

```cli
nuget trusted-signers add -Name <name> [options]
```

_참고_: 지정 된 이름의 신뢰할 수 있는 서명자가 이미 있는 경우 해당 서명자에 게 인증서 항목이 추가 됩니다. 그렇지 않으면 지정 된 인증서 정보에서 인증서 항목을 사용 하 여 신뢰할 수 있는 작성자가 만들어집니다.

| 옵션 | 설명 |
| --- | --- |
| CertificateFingerprint | 서명 된 패키지에 서명 해야 하는 인증서의 인증서 지문을 지정 합니다. 인증서 지문을 인증서의 해시입니다. 이 해시를 계산 하는 데 사용 되는 해시 알고리즘은 `FingerprintAlgorithm` 옵션에서 지정 해야 합니다. |
| FingerprintAlgorithm | 인증서 지문을 계산 하는 데 사용 되는 해시 알고리즘을 지정 합니다. 기본값은 `SHA256`입니다. 지원 되는 값은 `SHA256`, `SHA384` 및 `SHA512` |
| Allowunroot | 신뢰할 수 있는 서명자에 대 한 인증서를 신뢰할 수 없는 루트에 연결할 수 있는지 여부를 지정 합니다. |

## <a name="nuget-trusted-signers-remove--name-name"></a>nuget 신뢰할 수 있는 서명자 제거 이름 \<이름\>

지정 된 이름과 일치 하는 모든 신뢰할 수 있는 서명자를 제거 합니다.

## <a name="nuget-trusted-signers-sync--name-name"></a>nuget 신뢰할 수 있는-서명자 동기화-이름 \<이름\>

현재 신뢰할 수 있는 리포지토리에서 사용 되는 인증서의 최신 목록을 요청 하 여 신뢰할 수 있는 서명자의 기존 인증서 목록을 업데이트 합니다.

_참고_:이 제스처는 현재 인증서 목록을 삭제 하 고 리포지토리의 최신 목록으로 바꿉니다.

## <a name="options"></a>옵션

| 옵션 | 설명 |
| --- | --- |
| Read-configfile | 적용할 NuGet 구성 파일입니다. 지정 하지 않으면 `%AppData%\NuGet\NuGet.Config` (Windows) 또는 `~/.nuget/NuGet/NuGet.Config` (Mac/Linux)가 사용 됩니다.|
| ForceEnglishOutput | 고정 영어 기반 문화권을 사용 하 여 nuget.exe를 실행 합니다. |
| 도움말 | 명령에 대 한 도움말 정보를 표시 합니다. |
| 자세한 정도 | 출력에 표시 되는 세부 정보의 양을 지정 합니다. *보통*, *자동*, *자세히*입니다. |

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
