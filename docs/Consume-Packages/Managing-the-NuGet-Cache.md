---
title: NuGet에서 패키지 캐싱을 관리하는 방법 | Microsoft Docs
author: kraigb
ms.author: kraigb
manager: ghogen
ms.date: 7/26/2017
ms.topic: article
ms.prod: nuget
ms.technology: ''
description: 컴퓨터에 있는 다른 NuGet 패키지 캐시를 관리하는 방법은 패키지를 설치하거나 복원할 때 사용됩니다.
keywords: NuGet 패키지 캐시, 패키지 캐싱, NuGet 캐시, 캐시 관리, 로컬 NuGet 캐시, 전역 NuGet 캐시, NuGet 로컬 명령, 캐시 지우기
ms.reviewer:
- karann-msft
- unniravindranathan
ms.openlocfilehash: 09b3560d67ff8a38677dd1e27d85cdf234495aae
ms.sourcegitcommit: 718e6cb88e45fa07c85d653f216bf92eaaf81625
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 03/23/2018
---
# <a name="managing-the-nuget-cache"></a>NuGet 캐시 관리

NuGet은 컴퓨터에 이미 있는 패키지를 다운로드하지 않도록 방지하고 오프라인 지원을 제공하는 여러 로컬 캐시를 관리합니다. NuGet은 네트워크 연결 없이 패키지를 설치하거나 다시 설치할 때 캐시를 자동으로 사용합니다.

[로컬 명령](../tools/cli-ref-locals.md)을 사용하여 캐시 위치를 사용할 수 있습니다.

```cli
nuget locals all -list
```

일반적인 출력은 다음과 같습니다.

```output
http-cache: C:\Users\user\AppData\Local\NuGet\v3-cache   #NuGet 3.x+ cache
packages-cache: C:\Users\user\AppData\Local\NuGet\Cache  #NuGet 2.x cache
global-packages: C:\Users\user\.nuget\packages\          #Global packages folder
temp: C:\Users\user\AppData\Local\Temp\NuGetScratch      #Temp folder
```

패키지 설치 문제가 발생하는 경우 또는 원격 갤러리의 패키지를 설치하려는 경우 `locals -clear` 옵션을 사용합니다.

```cli
nuget locals http-cache -clear        #Clear the 3.x+ cache
nuget locals packages-cache -clear    #Clear the 2.x cache
nuget locals global-packages -clear   #Clear the global packages folder
nuget locals temp -clear              #Clear the temporary cache
nuget locals all -clear               #Clear all caches
```

캐시 관리는 현재 Visual Studio 내 또는 패키지 관리자 콘솔을 통해서가 아닌 NuGet 명령줄에서만 지원됩니다. 또한 2.x 캐시 관리는 NuGet 3.6 이상에서 지원되지 않습니다.

`nuget locals`를 사용하는 경우 다음과 같은 오류가 발생할 수 있습니다.

- **실패한 로컬 리소스 지우기: 하나 이상의 파일을 삭제할 수 없습니다.**
- **디렉터리가 비어 있지 않습니다.**

캐시에서 파일을 삭제할 수 있는 권한이 없거나 캐시에서 하나 이상의 파일이 다른 프로세스에 의해 사용 중임을 나타냅니다. 해당 파일을 제거하기 전에 닫아야 합니다.
