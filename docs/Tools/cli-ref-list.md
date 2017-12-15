---
title: "NuGet CLI 목록 표시 명령 | Microsoft Docs"
author: kraigb
ms.author: kraigb
manager: ghogen
ms.date: 10/24/2017
ms.topic: reference
ms.prod: nuget
ms.technology: 
ms.assetid: 728c8452-0457-4bb8-bfdc-de77fe1570bd
description: "Nuget.exe 목록 명령에 대 한 참조"
keywords: "nuget 목록 참조 패키지 목록 표시 명령"
ms.reviewer:
- karann-msft
- unniravindranathan
ms.openlocfilehash: 62a7077e7adac1e4d8cf305fd6e66a6ce5ebfb76
ms.sourcegitcommit: d0ba99bfe019b779b75731bafdca8a37e35ef0d9
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 12/14/2017
---
# <a name="list-command-nuget-cli"></a>목록 표시 명령 (NuGet CLI)

**적용 대상:** 패키지 소비, 게시 &bullet; **지원 되는 버전:** 모든

지정된 된 원본에서 패키지의 목록이 표시 됩니다. 모든 소스에서 글로벌 구성 파일에 정의 된 원본이 지정 된 경우 `%AppData%\NuGet\NuGet.Config`, 사용 됩니다. 경우 `NuGet.Config` 다음 원본이 없습니다 지정 `list` 기본 피드 (nuget.org)를 사용 하 여 합니다.

## <a name="usage"></a>용도

```
nuget list [search terms] [options]
```

여기서 선택적 검색 단어에 표시 된 목록을 필터링 합니다. 검색어는 패키지, 태그 및 패키지 설명의 이름에 적용 됩니다.

## <a name="options"></a>옵션
| 옵션 | 설명 |
| --- | --- |
| AllVersions | 패키지의 모든 버전을 나열 합니다. 기본적으로는 최신 패키지 버전에만 표시 됩니다. |
| ConfigFile | *(2.5 +)*  NuGet 구성 파일을 적용 합니다. 지정 하지 않으면 *%AppData%\NuGet\NuGet.Config* 사용 됩니다. |
| ForceEnglishOutput | *(3.5 +)*  고정, 영어 기반 문화권을 사용 하 여 실행할 nuget.exe를 강제로 수행 합니다. |
| 도움말 | 도움말의 명령에 대 한 정보를 표시 합니다. |
| IncludeDelisted | *(3.2 +)*  목록에 없는 패키지를 표시 합니다. |
| 비 대화형 | 사용자 입력 또는 확인에 대 한 프롬프트를 표시 하지 않습니다. |
| 시험판 | 목록에 시험판 패키지를 포함합니다. |
| 소스 | 검색할 패키지 소스 목록을 지정 합니다. |
| 자세한 정도 | 출력에 표시 되는 세부 정보 수준을 지정: *일반*, *quiet*, *세부 (2.5 이상)*합니다. |

또한 참조 [환경 변수](cli-ref-environment-variables.md)

## <a name="examples"></a>예제

```
nuget list

nuget list -Verbosity detailed -AllVersions
```
