---
title: NuGet CLI 삭제 명령
description: Nuget.exe delete 명령에 대 한 참조
author: karann-msft
ms.author: karann
ms.date: 01/18/2018
ms.topic: reference
ms.openlocfilehash: 11eea6e806d7bfe364587db9c7ef8374da1819f9
ms.sourcegitcommit: 1d1406764c6af5fb7801d462e0c4afc9092fa569
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 09/04/2018
ms.locfileid: "43548512"
---
# <a name="delete-command-nuget-cli"></a><span data-ttu-id="238d0-103">delete 명령 (NuGet CLI)</span><span class="sxs-lookup"><span data-stu-id="238d0-103">delete command (NuGet CLI)</span></span>

<span data-ttu-id="238d0-104">**적용 대상:** 게시 패키지 &bullet; **지원 되는 버전:** 모든</span><span class="sxs-lookup"><span data-stu-id="238d0-104">**Applies to:** package publishing &bullet; **Supported versions:** all</span></span>

<span data-ttu-id="238d0-105">삭제 하거나 패키지 소스에서 패키지 목록에서 제거 합니다.</span><span class="sxs-lookup"><span data-stu-id="238d0-105">Deletes or unlists a package from a package source.</span></span> <span data-ttu-id="238d0-106">Nuget.org를 delete 명령에 대 한 [패키지 목록](../policies/deleting-packages.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="238d0-106">For nuget.org, the delete command [unlists the package](../policies/deleting-packages.md).</span></span>

## <a name="usage"></a><span data-ttu-id="238d0-107">사용법</span><span class="sxs-lookup"><span data-stu-id="238d0-107">Usage</span></span>

```cli
nuget delete <packageID> <packageVersion> [options]
```

<span data-ttu-id="238d0-108">여기서 `<packageID>` 및 `<packageVersion>` 정확한 패키지 나열을 취소 하거나 삭제를 식별 합니다.</span><span class="sxs-lookup"><span data-stu-id="238d0-108">where `<packageID>` and `<packageVersion>` identify the exact package to delete or unlist.</span></span> <span data-ttu-id="238d0-109">정확한 동작은 원본에 따라 달라 집니다.</span><span class="sxs-lookup"><span data-stu-id="238d0-109">The exact behavior depends on the source.</span></span> <span data-ttu-id="238d0-110">로컬 폴더에 대 한 예를 들어 패키지를 삭제 합니다. nuget.org 패키지 나열 하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="238d0-110">For local folders, for instance, the package is deleted; for nuget.org the package is unlisted.</span></span>

## <a name="options"></a><span data-ttu-id="238d0-111">옵션</span><span class="sxs-lookup"><span data-stu-id="238d0-111">Options</span></span>

| <span data-ttu-id="238d0-112">옵션</span><span class="sxs-lookup"><span data-stu-id="238d0-112">Option</span></span> | <span data-ttu-id="238d0-113">설명</span><span class="sxs-lookup"><span data-stu-id="238d0-113">Description</span></span> |
| --- | --- |
| <span data-ttu-id="238d0-114">ApiKey</span><span class="sxs-lookup"><span data-stu-id="238d0-114">ApiKey</span></span> | <span data-ttu-id="238d0-115">대상 리포지토리에 대 한 API 키입니다.</span><span class="sxs-lookup"><span data-stu-id="238d0-115">The API key for the target repository.</span></span> <span data-ttu-id="238d0-116">없는 경우 구성 파일에 지정 된 사용 됩니다.</span><span class="sxs-lookup"><span data-stu-id="238d0-116">If not present, the one specified in the config file is used.</span></span> |
| <span data-ttu-id="238d0-117">ConfigFile</span><span class="sxs-lookup"><span data-stu-id="238d0-117">ConfigFile</span></span> | <span data-ttu-id="238d0-118">NuGet 구성 파일을 적용 합니다.</span><span class="sxs-lookup"><span data-stu-id="238d0-118">The NuGet configuration file to apply.</span></span> <span data-ttu-id="238d0-119">지정 하지 않으면 `%AppData%\NuGet\NuGet.Config` (Windows) 또는 `~/.nuget/NuGet/NuGet.Config` (Mac/Linux)가 사용 됩니다.</span><span class="sxs-lookup"><span data-stu-id="238d0-119">If not specified, `%AppData%\NuGet\NuGet.Config` (Windows) or `~/.nuget/NuGet/NuGet.Config` (Mac/Linux) is used.</span></span>|
| <span data-ttu-id="238d0-120">ForceEnglishOutput</span><span class="sxs-lookup"><span data-stu-id="238d0-120">ForceEnglishOutput</span></span> | <span data-ttu-id="238d0-121">*(3.5 이상)*  고정 영어 기반 문화권을 사용 하 여 실행할 nuget.exe를 강제로 수행 합니다.</span><span class="sxs-lookup"><span data-stu-id="238d0-121">*(3.5+)* Forces nuget.exe to run using an invariant, English-based culture.</span></span> |
| <span data-ttu-id="238d0-122">도움말</span><span class="sxs-lookup"><span data-stu-id="238d0-122">Help</span></span> | <span data-ttu-id="238d0-123">도움말의 명령에 대 한 정보를 표시 합니다.</span><span class="sxs-lookup"><span data-stu-id="238d0-123">Displays help information for the command.</span></span> |
| <span data-ttu-id="238d0-124">NonInteractive</span><span class="sxs-lookup"><span data-stu-id="238d0-124">NonInteractive</span></span> | <span data-ttu-id="238d0-125">사용자 입력 또는 확인에 대 한 프롬프트를 표시 하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="238d0-125">Suppresses prompts for user input or confirmations.</span></span> |
| <span data-ttu-id="238d0-126">소스</span><span class="sxs-lookup"><span data-stu-id="238d0-126">Source</span></span> | <span data-ttu-id="238d0-127">서버 URL을 지정합니다.</span><span class="sxs-lookup"><span data-stu-id="238d0-127">Specifies the server URL.</span></span> <span data-ttu-id="238d0-128">Nuget.org에 대 한 URL은 `https://api.nuget.org/v3/index.json`합니다.</span><span class="sxs-lookup"><span data-stu-id="238d0-128">The URL for nuget.org is `https://api.nuget.org/v3/index.json`.</span></span> <span data-ttu-id="238d0-129">개인 피드를 대체 호스트 이름, 예를 들어 *%hostname%/api/v3*합니다.</span><span class="sxs-lookup"><span data-stu-id="238d0-129">For private feeds, substitute the host name, for example, *%hostname%/api/v3*.</span></span> |
| <span data-ttu-id="238d0-130">자세한 정도</span><span class="sxs-lookup"><span data-stu-id="238d0-130">Verbosity</span></span> | <span data-ttu-id="238d0-131">출력에 표시 되는 세부 정보의 양을 지정: *정상적인*, *quiet*, *자세한*합니다.</span><span class="sxs-lookup"><span data-stu-id="238d0-131">Specifies the amount of detail displayed in the output: *normal*, *quiet*, *detailed*.</span></span> |

<span data-ttu-id="238d0-132">또한 참조 [환경 변수](cli-ref-environment-variables.md)</span><span class="sxs-lookup"><span data-stu-id="238d0-132">Also see [Environment variables](cli-ref-environment-variables.md)</span></span>

## <a name="examples"></a><span data-ttu-id="238d0-133">예제</span><span class="sxs-lookup"><span data-stu-id="238d0-133">Examples</span></span>

```cli
nuget delete MyPackage 1.0

nuget delete MyPackage 1.0 -Source http://package.contoso.com/source -apikey A1B2C3
```
