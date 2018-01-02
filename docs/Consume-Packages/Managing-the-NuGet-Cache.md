---
title: "NuGet에서 패키지 캐싱을 관리하는 방법 | Microsoft Docs"
author: kraigb
ms.author: kraigb
manager: ghogen
ms.date: 7/26/2017
ms.topic: article
ms.prod: nuget
ms.technology: 
ms.assetid: 3932217d-780d-4bd1-ad15-767acd3e8870
description: "컴퓨터에 있는 다른 NuGet 패키지 캐시를 관리하는 방법은 패키지를 설치하거나 복원할 때 사용됩니다."
keywords: "NuGet 패키지 캐시, 패키지 캐싱, NuGet 캐시, 캐시 관리, 로컬 NuGet 캐시, 전역 NuGet 캐시, NuGet 로컬 명령, 캐시 지우기"
ms.reviewer:
- karann-msft
- unniravindranathan
ms.openlocfilehash: 6e76c219ba420eb285af20e67b26dcdceebb6bab
ms.sourcegitcommit: d0ba99bfe019b779b75731bafdca8a37e35ef0d9
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 12/14/2017
---
# <a name="managing-the-nuget-cache"></a><span data-ttu-id="3f285-104">NuGet 캐시 관리</span><span class="sxs-lookup"><span data-stu-id="3f285-104">Managing the NuGet cache</span></span>

<span data-ttu-id="3f285-105">NuGet은 컴퓨터에 이미 있는 패키지를 다운로드하지 않도록 방지하고 오프라인 지원을 제공하는 여러 로컬 캐시를 관리합니다.</span><span class="sxs-lookup"><span data-stu-id="3f285-105">NuGet manages several local caches to avoid downloading packages that are already on the computer, and to provide offline support.</span></span> <span data-ttu-id="3f285-106">NuGet 2.8+은 네트워크 연결 없이 패키지를 설치하거나 다시 설치할 때 캐시를 자동으로 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="3f285-106">NuGet 2.8+ automatically falls back to the cache when installing or reinstalling packages without a network connection.</span></span>

<span data-ttu-id="3f285-107">[로컬 명령](../tools/cli-ref-locals.md)을 사용하여 캐시 위치를 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="3f285-107">Cache locations are available using the [locals command](../tools/cli-ref-locals.md):</span></span>

```
nuget locals all -list
```

<span data-ttu-id="3f285-108">일반적인 출력은 다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="3f285-108">Typical output is as follows:</span></span>

    http-cache: C:\Users\user\AppData\Local\NuGet\v3-cache   #NuGet 3.x+ cache
    packages-cache: C:\Users\user\AppData\Local\NuGet\Cache  #NuGet 2.x cache
    global-packages: C:\Users\user\.nuget\packages\          #Global packages folder
    temp: C:\Users\user\AppData\Local\Temp\NuGetScratch      #Temp folder

<span data-ttu-id="3f285-109">패키지 설치 문제가 발생하는 경우 또는 원격 갤러리의 패키지를 설치하려는 경우 `locals -clear` 옵션을 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="3f285-109">If you encounter package installation problems or otherwise want to ensure that you're installing packages from a remote gallery, use the `locals -clear` option:</span></span>

```
nuget locals http-cache -clear        #Clear the 3.x+ cache
nuget locals packages-cache -clear    #Clear the 2.x cache
nuget locals global-packages -clear   #Clear the global packages folder
nuget locals temp -clear              #Clear the temporary cache
nuget locals all -clear               #Clear all caches
```

<span data-ttu-id="3f285-110">캐시 관리는 현재 Visual Studio 내 또는 패키지 관리자 콘솔을 통해서가 아닌 NuGet 명령줄에서만 지원됩니다.</span><span class="sxs-lookup"><span data-stu-id="3f285-110">Note that managing the cache is presently supported only from the NuGet command line, and not within Visual Studio or through the Package Manager Console.</span></span> <span data-ttu-id="3f285-111">또한 2.x 캐시 관리는 NuGet 3.6 이상에서 지원되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="3f285-111">Also, managing the 2.x cache is not supported in NuGet 3.6 and later.</span></span>

<span data-ttu-id="3f285-112">`nuget locals`를 사용하는 경우 다음과 같은 오류가 발생할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="3f285-112">The following errors can occur when using `nuget locals`:</span></span>

* <span data-ttu-id="3f285-113">**실패한 로컬 리소스 지우기: 하나 이상의 파일을 삭제할 수 없습니다.**</span><span class="sxs-lookup"><span data-stu-id="3f285-113">**Clearing local resources failed: Unable to delete one or more files**</span></span>
* <span data-ttu-id="3f285-114">**디렉터리가 비어 있지 않습니다.**</span><span class="sxs-lookup"><span data-stu-id="3f285-114">**The directory is not empty**</span></span>

<span data-ttu-id="3f285-115">캐시에서 파일을 삭제할 수 있는 권한이 없거나 캐시에서 하나 이상의 파일 다른 프로세스에 의해 사용 중임을 나타냅니다. 해당 파일을 제거하기 전에 닫아야 합니다.</span><span class="sxs-lookup"><span data-stu-id="3f285-115">These indicate that you either do not have permission to delete files in the cache, or that one or more files in the cache are in use by another process, which must be closed before the those files can be removed.</span></span>
