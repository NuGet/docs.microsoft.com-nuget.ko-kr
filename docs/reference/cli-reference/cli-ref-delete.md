---
title: NuGet CLI delete 명령
description: nuget.exe delete 명령에 대 한 참조
author: karann-msft
ms.author: karann
ms.date: 01/18/2018
ms.topic: reference
ms.openlocfilehash: bec1a778d4986a4cb7ee87e1ef8a98550c96ed57
ms.sourcegitcommit: cbc87fe51330cdd3eacaad3e8656eb4258882fc7
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/19/2020
ms.locfileid: "88622865"
---
# <a name="delete-command-nuget-cli"></a><span data-ttu-id="dc830-103">delete 명령 (NuGet CLI)</span><span class="sxs-lookup"><span data-stu-id="dc830-103">delete command (NuGet CLI)</span></span>

<span data-ttu-id="dc830-104">**적용 대상:** 패키지 게시 &bullet; **지원 버전:** 모두</span><span class="sxs-lookup"><span data-stu-id="dc830-104">**Applies to:** package publishing &bullet; **Supported versions:** all</span></span>

<span data-ttu-id="dc830-105">패키지 원본에서 패키지를 삭제 하거나 목록에서 제거 합니다.</span><span class="sxs-lookup"><span data-stu-id="dc830-105">Deletes or unlists a package from a package source.</span></span> <span data-ttu-id="dc830-106">Nuget.org의 경우 delete 명령은 [패키지를 나열](../../nuget-org/policies/deleting-packages.md)하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="dc830-106">For nuget.org, the delete command [unlists the package](../../nuget-org/policies/deleting-packages.md).</span></span>

## <a name="usage"></a><span data-ttu-id="dc830-107">사용량</span><span class="sxs-lookup"><span data-stu-id="dc830-107">Usage</span></span>

```cli
nuget delete <packageID> <packageVersion> [options]
```

<span data-ttu-id="dc830-108">여기서 `<packageID>` 및 `<packageVersion>` 은 삭제할 정확한 패키지를 식별 합니다.</span><span class="sxs-lookup"><span data-stu-id="dc830-108">where `<packageID>` and `<packageVersion>` identify the exact package to delete or unlist.</span></span> <span data-ttu-id="dc830-109">정확한 동작은 원본에 따라 달라 집니다.</span><span class="sxs-lookup"><span data-stu-id="dc830-109">The exact behavior depends on the source.</span></span> <span data-ttu-id="dc830-110">예를 들어 로컬 폴더의 경우 패키지는 삭제 됩니다. nuget.org의 경우 패키지가 나열 되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="dc830-110">For local folders, for instance, the package is deleted; for nuget.org the package is unlisted.</span></span>

## <a name="options"></a><span data-ttu-id="dc830-111">옵션</span><span class="sxs-lookup"><span data-stu-id="dc830-111">Options</span></span>

- **`-ApiKey`**

  <span data-ttu-id="dc830-112">대상 리포지토리의 API 키입니다.</span><span class="sxs-lookup"><span data-stu-id="dc830-112">The API key for the target repository.</span></span> <span data-ttu-id="dc830-113">존재 하지 않는 경우 구성 파일에 지정 된 항목을 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="dc830-113">If not present, the one specified in the config file is used.</span></span>

- **`-ConfigFile`**

  <span data-ttu-id="dc830-114">적용할 NuGet 구성 파일입니다.</span><span class="sxs-lookup"><span data-stu-id="dc830-114">The NuGet configuration file to apply.</span></span> <span data-ttu-id="dc830-115">지정 하지 않으면 `%AppData%\NuGet\NuGet.Config` (Windows) 또는 `~/.nuget/NuGet/NuGet.Config` 또는 `~/.config/NuGet/NuGet.Config` (Mac/Linux)가 사용 됩니다.</span><span class="sxs-lookup"><span data-stu-id="dc830-115">If not specified, `%AppData%\NuGet\NuGet.Config` (Windows), or `~/.nuget/NuGet/NuGet.Config` or `~/.config/NuGet/NuGet.Config` (Mac/Linux) is used.</span></span>

- **`-ForceEnglishOutput`**

  <span data-ttu-id="dc830-116">*(3.5 +)* 고정 된 영어 기반 문화권을 사용 하 여 nuget.exe을 강제로 실행 합니다.</span><span class="sxs-lookup"><span data-stu-id="dc830-116">*(3.5+)* Forces nuget.exe to run using an invariant, English-based culture.</span></span>

- **`-?|-help`**

  <span data-ttu-id="dc830-117">명령에 대 한 도움말 정보를 표시 합니다.</span><span class="sxs-lookup"><span data-stu-id="dc830-117">Displays help information for the command.</span></span>

- **`-NonInteractive`**

  <span data-ttu-id="dc830-118">사용자 입력 또는 확인에 대 한 프롬프트를 표시 하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="dc830-118">Suppresses prompts for user input or confirmations.</span></span>

 - **`-np|-NoPrompt`**

   <span data-ttu-id="dc830-119">삭제할 때 메시지를 표시 하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="dc830-119">Do not prompt when deleting.</span></span>

 - <span data-ttu-id="dc830-120">**`-NoServiceEndpoint`** "Api/v2/패키지"를 원본 URL에 추가 하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="dc830-120">**`-NoServiceEndpoint`** Does not append "api/v2/packages" to the source URL.</span></span>

- **`-src|-Source`**

  <span data-ttu-id="dc830-121">서버 URL을 지정합니다.</span><span class="sxs-lookup"><span data-stu-id="dc830-121">Specifies the server URL.</span></span> <span data-ttu-id="dc830-122">Nuget.org의 URL은 `https://api.nuget.org/v3/index.json` 입니다.</span><span class="sxs-lookup"><span data-stu-id="dc830-122">The URL for nuget.org is `https://api.nuget.org/v3/index.json`.</span></span> <span data-ttu-id="dc830-123">개인 피드의 경우 호스트 이름 (예: *% hostname%/api/v3*)을 대체 합니다.</span><span class="sxs-lookup"><span data-stu-id="dc830-123">For private feeds, substitute the host name, for example, *%hostname%/api/v3*.</span></span>

- **`-Verbosity [normal|quiet|detailed]`**

  <span data-ttu-id="dc830-124">출력에 표시 되는 세부 정보의 양을 지정 합니다. `normal` (기본값), `quiet` 또는 `detailed` 입니다.</span><span class="sxs-lookup"><span data-stu-id="dc830-124">Specifies the amount of detail displayed in the output: `normal` (the default), `quiet`, or `detailed`.</span></span>

<span data-ttu-id="dc830-125">[환경 변수](cli-ref-environment-variables.md) 참조</span><span class="sxs-lookup"><span data-stu-id="dc830-125">Also see [Environment variables](cli-ref-environment-variables.md)</span></span>

## <a name="examples"></a><span data-ttu-id="dc830-126">예</span><span class="sxs-lookup"><span data-stu-id="dc830-126">Examples</span></span>

```cli
nuget delete MyPackage 1.0

nuget delete MyPackage 1.0 -Source http://package.contoso.com/source -apikey A1B2C3
```
