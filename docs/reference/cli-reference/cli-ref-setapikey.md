---
title: NuGet CLI setapikey 명령
description: Nuget.exe setapikey 명령에 대 한 참조
author: karann-msft
ms.author: karann
ms.date: 01/18/2018
ms.topic: reference
ms.openlocfilehash: e06cfb5b355dfae8104090db7babdecdf9e9fec1
ms.sourcegitcommit: c81561e93a7be467c1983d639158d4e3dc25b93a
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 03/02/2020
ms.locfileid: "78231229"
---
# <a name="setapikey-command-nuget-cli"></a><span data-ttu-id="1215d-103">setapikey 명령 (NuGet CLI)</span><span class="sxs-lookup"><span data-stu-id="1215d-103">setapikey command (NuGet CLI)</span></span>

<span data-ttu-id="1215d-104">**적용 대상:** 패키지 사용, 게시 &bullet; **지원 되는 버전:** 모두</span><span class="sxs-lookup"><span data-stu-id="1215d-104">**Applies to:** package consumption, publishing &bullet; **Supported versions:** all</span></span>

<span data-ttu-id="1215d-105">지정 된 서버 URL에 대 한 API 키를 `NuGet.Config`에 저장 하 여 후속 명령에 대해 입력이 필요 하지 않도록 합니다.</span><span class="sxs-lookup"><span data-stu-id="1215d-105">Saves an API key for a given server URL into `NuGet.Config` so that it doesn't need to be entered for subsequent commands.</span></span>

## <a name="usage"></a><span data-ttu-id="1215d-106">사용</span><span class="sxs-lookup"><span data-stu-id="1215d-106">Usage</span></span>

```cli
nuget setapikey <key> -Source <url> [options]
```

<span data-ttu-id="1215d-107">여기서 `<source>`은 서버를 식별 하 고 `<key>`는 저장할 키입니다.</span><span class="sxs-lookup"><span data-stu-id="1215d-107">where `<source>` identifies the server and `<key>` is the key to save.</span></span> <span data-ttu-id="1215d-108">`<source>` 생략 하면 nuget.org이 가정 됩니다.</span><span class="sxs-lookup"><span data-stu-id="1215d-108">If `<source>` is omitted, nuget.org is assumed.</span></span> 

> [!NOTE]
> <span data-ttu-id="1215d-109">API 키는 개인 피드에 인증 하는 데 사용 되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="1215d-109">API key is not used for authenticating with the private feed.</span></span> <span data-ttu-id="1215d-110">원본으로 인증 하기 위한 자격 증명을 관리 하려면 [`nuget sources` 명령을](../cli-reference/cli-ref-sources.md) 참조 하세요.</span><span class="sxs-lookup"><span data-stu-id="1215d-110">Refer to [`nuget sources` command](../cli-reference/cli-ref-sources.md) to manage credentials for authenticating with the source.</span></span>
> <span data-ttu-id="1215d-111">API 키는 개별 NuGet 서버에서 가져올 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="1215d-111">API keys can be obtained from the individual NuGet servers.</span></span> <span data-ttu-id="1215d-112">Nuget.org에 대 한 APIKeys를 만들고 관리 하려면 [publish-key](../../quickstart/includes/publish-api-key.md) 를 참조 하세요.</span><span class="sxs-lookup"><span data-stu-id="1215d-112">To create and manage APIKeys for nuget.org refer to [publish-api-key](../../quickstart/includes/publish-api-key.md)</span></span>

## <a name="options"></a><span data-ttu-id="1215d-113">옵션</span><span class="sxs-lookup"><span data-stu-id="1215d-113">Options</span></span>

| <span data-ttu-id="1215d-114">옵션</span><span class="sxs-lookup"><span data-stu-id="1215d-114">Option</span></span> | <span data-ttu-id="1215d-115">Description</span><span class="sxs-lookup"><span data-stu-id="1215d-115">Description</span></span> |
| --- | --- |
| <span data-ttu-id="1215d-116">ConfigFile</span><span class="sxs-lookup"><span data-stu-id="1215d-116">ConfigFile</span></span> | <span data-ttu-id="1215d-117">수정할 NuGet 구성 파일입니다.</span><span class="sxs-lookup"><span data-stu-id="1215d-117">The NuGet configuration file to apply.</span></span> <span data-ttu-id="1215d-118">지정 하지 않으면 `%AppData%\NuGet\NuGet.Config` (Windows) 또는 `~/.nuget/NuGet/NuGet.Config` (Mac/Linux)가 사용 됩니다.</span><span class="sxs-lookup"><span data-stu-id="1215d-118">If not specified, `%AppData%\NuGet\NuGet.Config` (Windows) or `~/.nuget/NuGet/NuGet.Config` (Mac/Linux) is used.</span></span>|
| <span data-ttu-id="1215d-119">ForceEnglishOutput</span><span class="sxs-lookup"><span data-stu-id="1215d-119">ForceEnglishOutput</span></span> | <span data-ttu-id="1215d-120">*(3.5 +)* 고정 영어 기반 문화권을 사용 하 여 nuget.exe를 실행 합니다.</span><span class="sxs-lookup"><span data-stu-id="1215d-120">*(3.5+)* Forces nuget.exe to run using an invariant, English-based culture.</span></span> |
| <span data-ttu-id="1215d-121">도움말</span><span class="sxs-lookup"><span data-stu-id="1215d-121">Help</span></span> | <span data-ttu-id="1215d-122">명령어에 대한 도움말을 표시합니다.</span><span class="sxs-lookup"><span data-stu-id="1215d-122">Displays help information for the command.</span></span> |
| <span data-ttu-id="1215d-123">NonInteractive</span><span class="sxs-lookup"><span data-stu-id="1215d-123">NonInteractive</span></span> | <span data-ttu-id="1215d-124">사용자 입력이나 확인에 대한 프롬프트를 표시하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="1215d-124">Suppresses prompts for user input or confirmations.</span></span> |
| <span data-ttu-id="1215d-125">자세한 정도</span><span class="sxs-lookup"><span data-stu-id="1215d-125">Verbosity</span></span> | <span data-ttu-id="1215d-126">출력에 표시 되는 세부 정보의 양을 지정 합니다. *보통*, *자동*, *자세히*입니다.</span><span class="sxs-lookup"><span data-stu-id="1215d-126">Specifies the amount of detail displayed in the output: *normal*, *quiet*, *detailed*.</span></span> |

<span data-ttu-id="1215d-127">[환경 변수](cli-ref-environment-variables.md) 참조</span><span class="sxs-lookup"><span data-stu-id="1215d-127">Also see [Environment variables](cli-ref-environment-variables.md)</span></span>

## <a name="examples"></a><span data-ttu-id="1215d-128">예</span><span class="sxs-lookup"><span data-stu-id="1215d-128">Examples</span></span>

```cli
nuget setapikey 4003d786-cc37-4004-bfdf-c4f3e8ef9b3a

nuget setapikey 4003d786-cc37-4004-bfdf-c4f3e8ef9b3a -source https://example.com/nugetfeed
```
