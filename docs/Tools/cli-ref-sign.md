---
title: NuGet CLI 기호 명령을 | Microsoft Docs
author: dtivel
ms.author: dtivel
manager: doronm
ms.date: 03/06/2018
ms.topic: reference
ms.prod: nuget
ms.technology: ''
description: Nuget.exe sign 명령에 대 한 참조
keywords: nuget 기호 참조, sign 명령
ms.reviewer:
- karann
- rmpablos
ms.workload:
- dotnet
- aspnet
ms.openlocfilehash: 9c83e5abae0e70cdc62917861c1febfce4f792c7
ms.sourcegitcommit: beb229893559824e8abd6ab16707fd5fe1c6ac26
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 03/28/2018
---
# <a name="sign-command-nuget-cli"></a>sign 명령 (NuGet CLI)

**적용 대상:** 패키지 만들기가 &bullet; **지원 되는 버전:** 4.6 이상

인증서와 함께 첫 번째 인수를 일치 하는 모든 패키지에 서명 합니다. 주체 이름이 나 지문을 제공 하 여 인증서 저장소에 설치 된 인증서 또는 파일에서 인증서와 개인 키를 얻을 수 있습니다.

패키지를 서명 아직 지원 되지 않습니다 모노 또는 Windows 이외의 플랫폼에서 합니다.

## <a name="usage"></a>사용법

```cli
nuget sign <package(s)> [options]
```

여기서 `<package(s)>` 는 하나 이상의 `.nupkg` 파일입니다.

## <a name="options"></a>옵션

| 옵션 | 설명 |
| --- | --- |
| CertificateFingerprint | 인증서에 대 한 로컬 인증서 저장소를 검색 하는 데 사용 되는 인증서의 sha-1 지문을 지정 합니다. |
| CertificatePassword | 필요한 경우 인증서 암호를 지정 합니다. 인증서는 암호로 보호 하는 경우 암호가 제공 됩니다 명령 됩니다 암호를 묻는 메시지를 실행 하지 않는 한-비 대화형 옵션 전달 됩니다. |
| CertificatePath | 패키지에 서명 하는 데 사용할 인증서를 파일 경로 지정 합니다. |
| CertificateStoreLocation | 인증서를 검색할 X.509 인증서 저장소 사용의 이름을 지정 합니다. 기본값은 "CurrentUser", 현재 사용자가 사용 되는 X.509 인증서 저장소입니다. -CertificateSubjectName 또는-CertificateFingerprint 옵션을 통해 인증서를 지정 하는 경우이 옵션을 사용 해야 합니다. |
| CertificateStoreName | X.509 인증서 저장소를 사용 하는 인증서에 대 한 검색의 이름을 지정 합니다. 기본값은 "My", 개인 인증서에 대 한 X.509 인증서 저장소입니다. -CertificateSubjectName 또는-CertificateFingerprint 옵션을 통해 인증서를 지정 하는 경우이 옵션을 사용 해야 합니다. |
| CertificateSubjectName | 인증서에 대 한 로컬 인증서 저장소를 검색 하는 데 사용 되는 인증서의 주체 이름을 지정 합니다.  검색은 다른 주체 값에 관계 없이 해당 문자열을 포함 하는 주체 이름을 가진 모든 인증서를 찾습니다는 제공 된 값을 사용 하 여 대/소문자 구분 문자열 비교 합니다.  인증서 저장소-CertificateStoreName 및-CertificateStoreLocation 옵션에 지정할 수 있습니다. |
| ConfigFile | 적용할 NuGet 구성 파일입니다. 지정 하지 않으면 `%AppData%\NuGet\NuGet.Config` (Windows) 또는 `~/.nuget/NuGet/NuGet.Config` (Mac/Linux)가 사용 됩니다.|
| ForceEnglishOutput | Nuget.exe 고정, 영어 기반 문화권을 사용 하 여 실행을 강제로 수행 합니다. |
| HashAlgorithm | 패키지에 서명 하는 데 사용할 해시 알고리즘입니다. 기본값은 s h a 256입니다. |
| 도움말 | 도움말의 명령에 대 한 정보를 표시 합니다. |
| NonInteractive | 사용자 입력 또는 확인에 대 한 프롬프트를 표시 하지 않습니다. |
| OutputDirectory | 서명된 된 패키지를 저장할 디렉터리를 지정 합니다. 기본적으로 서명된 된 패키지는 원본 패키지를 덮어씁니다. |
| 덮어쓰기 | 현재 서명 덮어써야 하는 경우를 나타내기 위해 스위치입니다. 기본적으로 패키지 서명을 이미 있으면 명령이 실패 합니다. |
| Timestamper | RFC 3161 타임 스탬프 서버 URL입니다. |
| TimestampHashAlgorithm | RFC 3161 타임 스탬프 서버에서 사용할 해시 알고리즘입니다. 기본값은 s h a 256입니다. |
| 자세한 정도 | 출력에 표시 되는 세부 정보 수준을 지정: *일반*, *quiet*, *자세한*합니다. |

## <a name="examples"></a>예제

```cli
nuget sign MyPackage.nupkg -Timestamper http://timestamp.test

nuget sign .\..\MyPackage.nupkg -Timestamper http://timestamp.test -OutputDirectory .\..\Signed
```