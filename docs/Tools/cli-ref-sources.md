---
title: "NuGet CLI 명령 원본 | Microsoft Docs"
author: kraigb
ms.author: kraigb
manager: ghogen
ms.date: 10/24/2017
ms.topic: reference
ms.prod: nuget
ms.technology: 
ms.assetid: 997ce736-91ba-4cd2-88c9-b4b168e3130a
description: "nuget.exe에 대 한 참조의 소스가 명령"
keywords: "nuget 원본 참조, 명령 원본"
ms.reviewer:
- karann-msft
- unniravindranathan
ms.openlocfilehash: 2eca8557840c467a60f5f708efe242cd83609164
ms.sourcegitcommit: bdcd2046b1b187d8b59716b9571142c02181c8fb
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 01/10/2018
---
# <a name="sources-command-nuget-cli"></a>소스 명령은 NuGet CLI)

**적용 대상:** 패키지 소비, 게시 &bullet; **지원 되는 버전:** 모든

원본에 있는 목록 관리 `%AppData%\NuGet\NuGet.Config` 또는 지정된 된 구성 파일입니다.

Nuget.org에 대 한 원본 URL은 `https://api.nuget.org/v3/index.json`합니다.

## <a name="usage"></a>사용법

```
nuget sources <operation> -Name <name> -Source <source>
```

여기서 `<operation>` 중 하나입니다 *목록, 추가, 제거, 설정, 해제* 또는 *업데이트*, `<name>` 에 원본의 이름 및 `<source>` 원본의 URL입니다.

## <a name="options"></a>옵션

| 옵션 | 설명 |
| --- | --- |
| ConfigFile | *(2.5 +)*  NuGet 구성 파일을 적용 합니다. 지정 하지 않으면 *%AppData%\NuGet\NuGet.Config* 사용 됩니다. |
| ForceEnglishOutput | *(3.5 +)*  고정, 영어 기반 문화권을 사용 하 여 실행할 nuget.exe를 강제로 수행 합니다. |
| 형식 | 에 적용 됩니다는 `list` 작업 수 및 `Detailed` (기본값) 또는 `Short`합니다. |
| 도움말 | 도움말의 명령에 대 한 정보를 표시 합니다. |
| 비 대화형 | 사용자 입력 또는 확인에 대 한 프롬프트를 표시 하지 않습니다. |
| 암호 | 소스에 인증 하기 위해 암호를 지정 합니다. |
| StorePasswordInClearText | 암호화 된 형식에 저장할 경우의 기본 동작 대신 암호화 되지 않은 텍스트에서 암호를 저장 하려면 나타냅니다. |
| UserName | 소스를 사용 하 여 인증에 대 한 사용자 이름을 지정 합니다. |
| 자세한 정도 | 출력에 표시 되는 세부 정보 수준을 지정: *일반*, *quiet*, *세부 (2.5 이상)*합니다. |

> [!Note]
> nuget.exe 패키지 원본에 액세스 하는 데 사용 나중에 동일한 사용자 컨텍스트에서 소스 암호를 추가 해야 합니다. 암호 구성 파일에 암호화 된 저장 되 고 암호화 된 대로 동일한 사용자 컨텍스트에서 해독할만 있습니다. 예를 사용 하면 빌드 서버 빌드 서버 작업이 실행 될 Windows 사용자가 암호를 암호화 해야 하는 NuGet 패키지를 복원 하려면.

또한 참조 [환경 변수](cli-ref-environment-variables.md)

## <a name="examples"></a>예제

```
nuget sources Add -Name "MyServer" -Source \\myserver\packages

nuget sources Disable -Name "MyServer"

nuget source Enable -Source "nuget.org"

nuget sources add -name foo.bar -source C:\NuGet\local -username foo -password bar -StorePasswordInClearText -configfile %AppData%\NuGet\my.config
```
