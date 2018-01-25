---
title: "NuGet CLI delete 명령을 | Microsoft Docs"
author: kraigb
ms.author: kraigb
manager: ghogen
ms.date: 01/18/2018
ms.topic: reference
ms.prod: nuget
ms.technology: 
description: "Nuget.exe delete 명령에 대 한 참조"
keywords: "nuget 참조를 삭제, 삭제 패키지 명령"
ms.reviewer:
- karann-msft
- unniravindranathan
ms.openlocfilehash: 3890e33ab0fc425e1c2ee39631ade57ea9b92bc9
ms.sourcegitcommit: 262d026beeffd4f3b6fc47d780a2f701451663a8
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 01/25/2018
---
# <a name="delete-command-nuget-cli"></a><span data-ttu-id="8d70b-104">delete 명령 (NuGet CLI)</span><span class="sxs-lookup"><span data-stu-id="8d70b-104">delete command (NuGet CLI)</span></span>

<span data-ttu-id="8d70b-105">**적용 대상:** 게시 패키지 &bullet; **지원 되는 버전:** 모든</span><span class="sxs-lookup"><span data-stu-id="8d70b-105">**Applies to:** package publishing &bullet; **Supported versions:** all</span></span>

<span data-ttu-id="8d70b-106">삭제 하거나 unlists 패키지 소스에서 패키지 합니다.</span><span class="sxs-lookup"><span data-stu-id="8d70b-106">Deletes or unlists a package from a package source.</span></span> <span data-ttu-id="8d70b-107">Nuget.org를 delete 명령에 대 한 [패키지 unlists](../policies/Deleting-Packages.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="8d70b-107">For nuget.org, the delete command [unlists the package](../policies/Deleting-Packages.md).</span></span>

## <a name="usage"></a><span data-ttu-id="8d70b-108">사용법</span><span class="sxs-lookup"><span data-stu-id="8d70b-108">Usage</span></span>

```cli
nuget delete <packageID> <packageVersion> [options]
```

<span data-ttu-id="8d70b-109">여기서 `<packageID>` 및 `<packageVersion>` 정확 하 게 패키지를 삭제 하거나 unlist 식별 합니다.</span><span class="sxs-lookup"><span data-stu-id="8d70b-109">where `<packageID>` and `<packageVersion>` identify the exact package to delete or unlist.</span></span> <span data-ttu-id="8d70b-110">정확한 동작은 소스에 따라 달라 집니다.</span><span class="sxs-lookup"><span data-stu-id="8d70b-110">The exact behavior depends on the source.</span></span> <span data-ttu-id="8d70b-111">로컬 폴더에 대 한 예를 들어, 패키지가 삭제 되었습니다. nuget.org에 대 한 패키지는 나열 되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="8d70b-111">For local folders, for instance, the package is deleted; for nuget.org the package is unlisted.</span></span>

## <a name="options"></a><span data-ttu-id="8d70b-112">옵션</span><span class="sxs-lookup"><span data-stu-id="8d70b-112">Options</span></span>

| <span data-ttu-id="8d70b-113">옵션</span><span class="sxs-lookup"><span data-stu-id="8d70b-113">Option</span></span> | <span data-ttu-id="8d70b-114">설명</span><span class="sxs-lookup"><span data-stu-id="8d70b-114">Description</span></span> |
| --- | --- |
| <span data-ttu-id="8d70b-115">apiKey</span><span class="sxs-lookup"><span data-stu-id="8d70b-115">ApiKey</span></span> | <span data-ttu-id="8d70b-116">대상 저장소에 대 한 API 키입니다.</span><span class="sxs-lookup"><span data-stu-id="8d70b-116">The API key for the target repository.</span></span> <span data-ttu-id="8d70b-117">없음, 1에 지정 된 경우 *%AppData%\NuGet\NuGet.Config* 사용 됩니다.</span><span class="sxs-lookup"><span data-stu-id="8d70b-117">If not present, the one specified in *%AppData%\NuGet\NuGet.Config* is used.</span></span> |
| <span data-ttu-id="8d70b-118">ConfigFile</span><span class="sxs-lookup"><span data-stu-id="8d70b-118">ConfigFile</span></span> | <span data-ttu-id="8d70b-119">적용할 NuGet 구성 파일입니다.</span><span class="sxs-lookup"><span data-stu-id="8d70b-119">The NuGet configuration file to apply.</span></span> <span data-ttu-id="8d70b-120">지정 하지 않으면 *%AppData%\NuGet\NuGet.Config* 사용 됩니다.</span><span class="sxs-lookup"><span data-stu-id="8d70b-120">If not specified, *%AppData%\NuGet\NuGet.Config* is used.</span></span> |
| <span data-ttu-id="8d70b-121">ForceEnglishOutput</span><span class="sxs-lookup"><span data-stu-id="8d70b-121">ForceEnglishOutput</span></span> | <span data-ttu-id="8d70b-122">*(3.5 +)*  고정, 영어 기반 문화권을 사용 하 여 실행할 nuget.exe를 강제로 수행 합니다.</span><span class="sxs-lookup"><span data-stu-id="8d70b-122">*(3.5+)* Forces nuget.exe to run using an invariant, English-based culture.</span></span> |
| <span data-ttu-id="8d70b-123">도움말</span><span class="sxs-lookup"><span data-stu-id="8d70b-123">Help</span></span> | <span data-ttu-id="8d70b-124">도움말의 명령에 대 한 정보를 표시 합니다.</span><span class="sxs-lookup"><span data-stu-id="8d70b-124">Displays help information for the command.</span></span> |
| <span data-ttu-id="8d70b-125">NonInteractive</span><span class="sxs-lookup"><span data-stu-id="8d70b-125">NonInteractive</span></span> | <span data-ttu-id="8d70b-126">사용자 입력 또는 확인에 대 한 프롬프트를 표시 하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="8d70b-126">Suppresses prompts for user input or confirmations.</span></span> |
| <span data-ttu-id="8d70b-127">소스</span><span class="sxs-lookup"><span data-stu-id="8d70b-127">Source</span></span> | <span data-ttu-id="8d70b-128">서버 URL을 지정합니다.</span><span class="sxs-lookup"><span data-stu-id="8d70b-128">Specifies the server URL.</span></span> <span data-ttu-id="8d70b-129">Nuget.org의 URL은 `https://api.nuget.org/v3/index.json`합니다.</span><span class="sxs-lookup"><span data-stu-id="8d70b-129">The URL for nuget.org is `https://api.nuget.org/v3/index.json`.</span></span> <span data-ttu-id="8d70b-130">개인 피드 대신 호스트 이름, 예를 들어 *%hostname%/api/v3*합니다.</span><span class="sxs-lookup"><span data-stu-id="8d70b-130">For private feeds, substitute the host name, for example, *%hostname%/api/v3*.</span></span> |
| <span data-ttu-id="8d70b-131">자세한 정도</span><span class="sxs-lookup"><span data-stu-id="8d70b-131">Verbosity</span></span> | <span data-ttu-id="8d70b-132">출력에 표시 되는 세부 정보 수준을 지정: *일반*, *quiet*, *자세한*합니다.</span><span class="sxs-lookup"><span data-stu-id="8d70b-132">Specifies the amount of detail displayed in the output: *normal*, *quiet*, *detailed*.</span></span> |

<span data-ttu-id="8d70b-133">또한 참조 [환경 변수](cli-ref-environment-variables.md)</span><span class="sxs-lookup"><span data-stu-id="8d70b-133">Also see [Environment variables](cli-ref-environment-variables.md)</span></span>

## <a name="examples"></a><span data-ttu-id="8d70b-134">예제</span><span class="sxs-lookup"><span data-stu-id="8d70b-134">Examples</span></span>

```cli
nuget delete MyPackage 1.0

nuget delete MyPackage 1.0 -Source http://package.contoso.com/source -apikey A1B2C3
```
