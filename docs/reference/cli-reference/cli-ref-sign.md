---
title: NuGet CLI sign 명령
description: Nuget.exe sign 명령에 대 한 참조
author: dtivel
ms.author: dtivel
ms.date: 03/06/2018
ms.topic: reference
ms.reviewer: rmpablos
ms.openlocfilehash: 746f7a421bd855b77716388b4af2fecbd5cf5a68
ms.sourcegitcommit: 96aab8a1ad35eca0c029679d0158d9cc93d66009
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 01/06/2020
ms.locfileid: "75676408"
---
# <a name="sign-command-nuget-cli"></a>sign 명령(NuGet CLI)

**적용 대상:** 패키지 만들기 &bullet; **지원 되는 버전:** 4.6 +

인증서를 사용 하 여 첫 번째 인수와 일치 하는 모든 패키지에 서명 합니다. 개인 키가 있는 인증서는 주체 이름 또는 지문을 제공 하 여 인증서 저장소에 설치 된 인증서 또는 파일에서 가져올 수 있습니다.

> [!Note]
> 패키지 서명은 .NET Core, Mono 또는 Windows 이외의 플랫폼에서 아직 지원 되지 않습니다.

## <a name="usage"></a>용도

```cli
nuget sign <package(s)> [options]
```

여기서 `<package(s)>`은 하나 이상의 `.nupkg` 파일입니다.

## <a name="options"></a>Options

| 옵션 | 설명 |
| --- | --- |
| CertificateFingerprint | 인증서에 대 한 로컬 인증서 저장소를 검색 하는 데 사용 되는 인증서의 SHA-1 지문을 지정 합니다. |
| CertificatePassword | 필요한 경우 인증서 암호를 지정 합니다. 인증서가 암호로 보호 되어 있지만 암호를 제공 하지 않는 경우-비 대화형 옵션을 전달 하지 않으면 명령에서 런타임에 암호를 입력 하 라는 메시지가 표시 됩니다. |
| CertificatePath | 패키지에 서명 하는 데 사용할 인증서의 파일 경로를 지정 합니다. |
| CertificateStoreLocation | 인증서를 검색 하는 데 사용 하는 x.509 인증서 저장소의 이름을 지정 합니다. 기본값은 현재 사용자가 사용 하는 x.509 인증서 저장소 인 "CurrentUser"입니다. -CertificateSubjectName 또는-CertificateFingerprint 옵션을 통해 인증서를 지정할 때이 옵션을 사용 해야 합니다. |
| CertificateStoreName | 인증서를 검색 하는 데 사용할 x.509 인증서 저장소의 이름을 지정 합니다. 기본값은 개인 인증서에 대 한 x.509 인증서 저장소 인 "My"입니다. -CertificateSubjectName 또는-CertificateFingerprint 옵션을 통해 인증서를 지정할 때이 옵션을 사용 해야 합니다. |
| CertificateSubjectName | 인증서에 대 한 로컬 인증서 저장소를 검색 하는 데 사용 되는 인증서의 주체 이름을 지정 합니다.  검색은 제공 된 값을 사용 하 여 대/소문자를 구분 하지 않는 문자열 비교로, 다른 주체 값에 관계 없이 해당 문자열을 포함 하는 주체 이름을 가진 모든 인증서를 찾습니다.  인증서 저장소는-CertificateStoreName 및-CertificateStoreLocation 옵션으로 지정할 수 있습니다. |
| ConfigFile | 수정할 NuGet 구성 파일입니다. 지정하지 않으면 기본적으로 Windows에서는 `%AppData%\NuGet\NuGet.Config`, Mac이나 Linux에서는 `~/.nuget/NuGet/NuGet.Config`가 사용됩니다.|
| ForceEnglishOutput | 고정 영어 기반 문화권을 사용 하 여 nuget.exe를 실행 합니다. |
| HashAlgorithm | 패키지에 서명 하는 데 사용할 해시 알고리즘입니다. 기본값은 SHA256입니다. |
| 도움말 | 명령어에 대한 도움말을 표시합니다. |
| NonInteractive | 사용자 입력이나 확인에 대한 프롬프트를 표시하지 않습니다. |
| OutputDirectory | 서명 된 패키지를 저장할 디렉터리를 지정 합니다. 기본적으로 서명 된 패키지가 원래 패키지를 덮어씁니다. |
| 덮어쓰기 | 현재 서명을 덮어쓸지 여부를 나타내는로 전환 합니다. 기본적으로 패키지에 이미 서명이 있으면 명령이 실패 합니다. |
| Timestamper | RFC 3161 타임 스탬프 서버의 URL입니다. |
| TimestampHashAlgorithm | RFC 3161 타임 스탬프 서버에서 사용 되는 해시 알고리즘입니다. 기본값은 SHA256입니다. |
| 자세한 정도 | 출력에 표시 되는 세부 정보의 양을 지정: *정상적인*, *quiet*, *자세한*합니다. |

## <a name="examples"></a>예

```cli
nuget sign MyPackage.nupkg -Timestamper http://timestamp.test

nuget sign .\..\MyPackage.nupkg -Timestamper http://timestamp.test -OutputDirectory .\..\Signed
```
