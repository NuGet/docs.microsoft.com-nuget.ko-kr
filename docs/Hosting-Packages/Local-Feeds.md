---
title: "로컬 NuGet 피드 설정 | Microsoft Docs"
author: kraigb
ms.author: kraigb
manager: ghogen
ms.date: 12/06/2017
ms.topic: article
ms.prod: nuget
ms.technology: 
description: "로컬 네트워크에서 폴더를 사용하여 NuGet 패키지에 로컬 피드를 만드는 방법"
keywords: "NuGet 피드, NuGet 갤러리, 로컬 패키지 피드"
ms.reviewer:
- karann-msft
- unniravindranathan
ms.openlocfilehash: 0b8633db78b19fecddeb057a9f287ef971aef27a
ms.sourcegitcommit: 4651b16a3a08f6711669fc4577f5d63b600f8f58
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 02/02/2018
---
# <a name="local-feeds"></a>로컬 피드

로컬 NuGet 패키지 피드는 패키지를 배치할 로컬 네트워크(또는 사용자 고유의 컴퓨터)의 단순한 계층적 폴더 구조입니다. CLI, 패키지 관리자 UI 및 패키지 관리자 콘솔을 사용하여 다른 모든 NuGet 작업에서 이러한 피드를 패키지 소스로 사용할 수 있습니다.

소스를 사용하려면 [패키지 관리자 UI](../tools/package-manager-ui.md#package-sources) 또는 [`nuget sources`](../tools/cli-ref-sources.md) 명령을 사용하여 원본 목록에 해당 경로 이름(예: `\\myserver\packages`)을 추가합니다.

> [!Note]
> 계층적 폴더 구조는 NuGet 3.3+에서 지원됩니다. 이전 버전의 NuGet은 성능이 계층적 구조보다 훨씬 낮은 패키지를 포함하는 단일 폴더만을 사용합니다.

## <a name="initializing-and-maintaining-hierarchical-folders"></a>계층적 폴더 초기화 및 유지 관리

계층적 버전이 있는 폴더 트리에는 다음과 같은 일반 구조가 있습니다.

    \\myserver\packages
      └─<packageID>
        └─<version>
          ├─<packageID>.<version>.nupkg
          └─<other files>

[`nuget add`](../tools/cli-ref-add.md) 명령을 사용하여 피드에 패키지를 복사할 때 NuGet이 이 구조를 자동으로 만듭니다.

```cli
nuget add new_package.1.0.0.nupkg -source \\myserver\packages
```

`nuget add` 명령은 한 번에 하나의 패키지에서 작동합니다. 그러면 여러 패키지가 포함된 피드를 설정할 때 편리할 수 있습니다.

이러한 경우에 개별적으로 `nuget add`를 실행한 경우와 같이 피드에 폴더의 모든 패키지를 복사하는 [`nuget init`](../tools/cli-ref-init.md) 명령을 사용합니다. 예를 들어 다음 명령은 `c:\packages`의 모든 패키지를 `\\myserver\packages`의 계층적 트리에 복사합니다.

```cli
nuget init c:\packages \\myserver\packages
```

`add` 명령과 마찬가지로 `init`는 각 패키지 식별자에 폴더를 만듭니다. 각각에는 적절한 패키지 내에 버전 번호 폴더가 포함됩니다.
