---
title: NuGet CLI delete 명령
description: Nuget.exe delete 명령에 대 한 참조
author: karann-msft
ms.author: karann
manager: unnir
ms.date: 01/18/2018
ms.topic: reference
ms.openlocfilehash: c0f33dd5475521da47972a6f032ac6ea86d98c83
ms.sourcegitcommit: 2a6d200012cdb4cbf5ab1264f12fecf9ae12d769
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 06/06/2018
ms.locfileid: "34817180"
---
# <a name="delete-command-nuget-cli"></a><span data-ttu-id="13c58-103">delete 명령 (NuGet CLI)</span><span class="sxs-lookup"><span data-stu-id="13c58-103">delete command (NuGet CLI)</span></span>

<span data-ttu-id="13c58-104">**적용 대상:** 게시 패키지 &bullet; **지원 되는 버전:** 모든</span><span class="sxs-lookup"><span data-stu-id="13c58-104">**Applies to:** package publishing &bullet; **Supported versions:** all</span></span>

<span data-ttu-id="13c58-105">삭제 하거나 unlists 패키지 소스에서 패키지 합니다.</span><span class="sxs-lookup"><span data-stu-id="13c58-105">Deletes or unlists a package from a package source.</span></span> <span data-ttu-id="13c58-106">Nuget.org를 delete 명령에 대 한 [패키지 unlists](../policies/deleting-packages.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="13c58-106">For nuget.org, the delete command [unlists the package](../policies/deleting-packages.md).</span></span>

## <a name="usage"></a><span data-ttu-id="13c58-107">사용법</span><span class="sxs-lookup"><span data-stu-id="13c58-107">Usage</span></span>

```cli
nuget delete <packageID> <packageVersion> [options]
```

<span data-ttu-id="13c58-108">여기서 `<packageID>` 및 `<packageVersion>` 정확 하 게 패키지를 삭제 하거나 unlist 식별 합니다.</span><span class="sxs-lookup"><span data-stu-id="13c58-108">where `<packageID>` and `<packageVersion>` identify the exact package to delete or unlist.</span></span> <span data-ttu-id="13c58-109">정확한 동작은 소스에 따라 달라 집니다.</span><span class="sxs-lookup"><span data-stu-id="13c58-109">The exact behavior depends on the source.</span></span> <span data-ttu-id="13c58-110">로컬 폴더에 대 한 예를 들어, 패키지가 삭제 되었습니다. nuget.org에 대 한 패키지는 나열 되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="13c58-110">For local folders, for instance, the package is deleted; for nuget.org the package is unlisted.</span></span>

## <a name="options"></a><span data-ttu-id="13c58-111">옵션</span><span class="sxs-lookup"><span data-stu-id="13c58-111">Options</span></span>

| <span data-ttu-id="13c58-112">옵션</span><span class="sxs-lookup"><span data-stu-id="13c58-112">Option</span></span> | <span data-ttu-id="13c58-113">설명</span><span class="sxs-lookup"><span data-stu-id="13c58-113">Description</span></span> |
| --- | --- |
| <span data-ttu-id="13c58-114">apiKey</span><span class="sxs-lookup"><span data-stu-id="13c58-114">ApiKey</span></span> | <span data-ttu-id="13c58-115">대상 저장소에 대 한 API 키입니다.</span><span class="sxs-lookup"><span data-stu-id="13c58-115">The API key for the target repository.</span></span> <span data-ttu-id="13c58-116">래퍼가 없는 경우 구성 파일에 지정 된 사용 됩니다.</span><span class="sxs-lookup"><span data-stu-id="13c58-116">If not present, the one specified in the config file is used.</span></span> |
| <span data-ttu-id="13c58-117">ConfigFile</span><span class="sxs-lookup"><span data-stu-id="13c58-117">ConfigFile</span></span> | <span data-ttu-id="13c58-118">적용할 NuGet 구성 파일입니다.</span><span class="sxs-lookup"><span data-stu-id="13c58-118">The NuGet configuration file to apply.</span></span> <span data-ttu-id="13c58-119">지정 하지 않으면 `%AppData%\NuGet\NuGet.Config` (Windows) 또는 `~/.nuget/NuGet/NuGet.Config` (Mac/Linux)가 사용 됩니다.</span><span class="sxs-lookup"><span data-stu-id="13c58-119">If not specified, `%AppData%\NuGet\NuGet.Config` (Windows) or `~/.nuget/NuGet/NuGet.Config` (Mac/Linux) is used.</span></span>|
| <span data-ttu-id="13c58-120">ForceEnglishOutput</span><span class="sxs-lookup"><span data-stu-id="13c58-120">ForceEnglishOutput</span></span> | <span data-ttu-id="13c58-121">*(3.5 +)*  고정, 영어 기반 문화권을 사용 하 여 실행할 nuget.exe를 강제로 수행 합니다.</span><span class="sxs-lookup"><span data-stu-id="13c58-121">*(3.5+)* Forces nuget.exe to run using an invariant, English-based culture.</span></span> |
| <span data-ttu-id="13c58-122">도움말</span><span class="sxs-lookup"><span data-stu-id="13c58-122">Help</span></span> | <span data-ttu-id="13c58-123">도움말의 명령에 대 한 정보를 표시 합니다.</span><span class="sxs-lookup"><span data-stu-id="13c58-123">Displays help information for the command.</span></span> |
| <span data-ttu-id="13c58-124">NonInteractive</span><span class="sxs-lookup"><span data-stu-id="13c58-124">NonInteractive</span></span> | <span data-ttu-id="13c58-125">사용자 입력 또는 확인에 대 한 프롬프트를 표시 하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="13c58-125">Suppresses prompts for user input or confirmations.</span></span> |
| <span data-ttu-id="13c58-126">소스</span><span class="sxs-lookup"><span data-stu-id="13c58-126">Source</span></span> | <span data-ttu-id="13c58-127">서버 URL을 지정합니다.</span><span class="sxs-lookup"><span data-stu-id="13c58-127">Specifies the server URL.</span></span> <span data-ttu-id="13c58-128">Nuget.org의 URL은 `https://api.nuget.org/v3/index.json`합니다.</span><span class="sxs-lookup"><span data-stu-id="13c58-128">The URL for nuget.org is `https://api.nuget.org/v3/index.json`.</span></span> <span data-ttu-id="13c58-129">개인 피드 대신 호스트 이름, 예를 들어 *%hostname%/api/v3*합니다.</span><span class="sxs-lookup"><span data-stu-id="13c58-129">For private feeds, substitute the host name, for example, *%hostname%/api/v3*.</span></span> |
| <span data-ttu-id="13c58-130">자세한 정도</span><span class="sxs-lookup"><span data-stu-id="13c58-130">Verbosity</span></span> | <span data-ttu-id="13c58-131">출력에 표시 되는 세부 정보 수준을 지정: *일반*, *quiet*, *자세한*합니다.</span><span class="sxs-lookup"><span data-stu-id="13c58-131">Specifies the amount of detail displayed in the output: *normal*, *quiet*, *detailed*.</span></span> |

<span data-ttu-id="13c58-132">또한 참조 [환경 변수](cli-ref-environment-variables.md)</span><span class="sxs-lookup"><span data-stu-id="13c58-132">Also see [Environment variables](cli-ref-environment-variables.md)</span></span>

## <a name="examples"></a><span data-ttu-id="13c58-133">예제</span><span class="sxs-lookup"><span data-stu-id="13c58-133">Examples</span></span>

```cli
nuget delete MyPackage 1.0

nuget delete MyPackage 1.0 -Source http://package.contoso.com/source -apikey A1B2C3
```
