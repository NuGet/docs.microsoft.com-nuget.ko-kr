---
title: "NuGet CLI 지역 명령을 | Microsoft Docs"
author: kraigb
ms.author: kraigb
manager: ghogen
ms.date: 01/18/2018
ms.topic: reference
ms.prod: nuget
ms.technology: 
description: "Nuget.exe 지역 명령에 대 한 참조"
keywords: "nuget 지역 변수 참조, 지역 명령"
ms.reviewer:
- karann-msft
- unniravindranathan
ms.openlocfilehash: b2f62a9ab5699bfb486eee146ab7046f5240aa50
ms.sourcegitcommit: 4651b16a3a08f6711669fc4577f5d63b600f8f58
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 02/02/2018
---
# <a name="locals-command-nuget-cli"></a>지역 명령 (NuGet CLI)

**적용 대상:** 소비 패키지 &bullet; **지원 되는 버전:** 3.3 +

Http 요청 캐시, 패키지 캐시 및 시스템 수준의 글로벌 패키지 폴더와 같은 로컬 NuGet 리소스를 나열 하거나 선택을 취소 합니다. `locals` 해당 위치의 목록을 표시 하려면 명령을 사용할 수도 있습니다. 자세한 내용은 참조 [NuGet 캐시 관리](../consume-packages/managing-the-nuget-cache.md)합니다.

## <a name="usage"></a>사용법

```cli
nuget locals <cache> [options]
```

여기서 `<cache>` 중 하나인 `all`, `http-cache`, `packages-cache`, `global-packages`, 및 `temp` *(3.4 +)*합니다.

## <a name="options"></a>옵션

| 옵션 | 설명 |
| --- | --- |
| 지우기 | 지정된 된 캐시를 지웁니다. |
| ConfigFile | 적용할 NuGet 구성 파일입니다. 지정 하지 않으면 *%AppData%\NuGet\NuGet.Config* 사용 됩니다. |
| ForceEnglishOutput | *(3.5 +)*  고정, 영어 기반 문화권을 사용 하 여 실행할 nuget.exe를 강제로 수행 합니다. |
| 도움말 | 도움말의 명령에 대 한 정보를 표시 합니다. |
| 목록 | 지정된 된 캐시의 위치 또는 함께 사용할 경우 모든 캐시의 위치 나열 *모든*합니다. |
| NonInteractive | 사용자 입력 또는 확인에 대 한 프롬프트를 표시 하지 않습니다. |
| 자세한 정도 | 출력에 표시 되는 세부 정보 수준을 지정: *일반*, *quiet*, *자세한*합니다. |

또한 참조 [환경 변수](cli-ref-environment-variables.md)

## <a name="examples"></a>예제

```cli
nuget locals all -list
nuget locals http-cache -clear
```
