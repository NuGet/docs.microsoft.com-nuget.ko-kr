---
title: NuGet CLI setapikey 명령
description: nuget.exe setapikey 명령에 대 한 참조
author: JonDouglas
ms.author: jodou
ms.date: 01/18/2018
ms.topic: reference
ms.openlocfilehash: 3e0c2f84e336e0a642b1b5e815e74a1fb0878467
ms.sourcegitcommit: ee6c3f203648a5561c809db54ebeb1d0f0598b68
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 01/26/2021
ms.locfileid: "98780019"
---
# <a name="setapikey-command-nuget-cli"></a><span data-ttu-id="e6042-103">setapikey 명령 (NuGet CLI)</span><span class="sxs-lookup"><span data-stu-id="e6042-103">setapikey command (NuGet CLI)</span></span>

<span data-ttu-id="e6042-104">**적용 대상:** 패키지 사용, &bullet; **지원 되는 버전 게시:** 모두</span><span class="sxs-lookup"><span data-stu-id="e6042-104">**Applies to:** package consumption, publishing &bullet; **Supported versions:** all</span></span>

<span data-ttu-id="e6042-105">지정 된 서버 URL에 대 한 API 키를에 저장 하 여 `NuGet.Config` 후속 명령에 대해 입력이 필요 하지 않도록 합니다.</span><span class="sxs-lookup"><span data-stu-id="e6042-105">Saves an API key for a given server URL into `NuGet.Config` so that it doesn't need to be entered for subsequent commands.</span></span>

## <a name="usage"></a><span data-ttu-id="e6042-106">사용량</span><span class="sxs-lookup"><span data-stu-id="e6042-106">Usage</span></span>

```cli
nuget setapikey <key> -Source <url> [options]
```

<span data-ttu-id="e6042-107">여기서는 `<source>` 서버를 식별 하 고 `<key>` 는 저장할 키입니다.</span><span class="sxs-lookup"><span data-stu-id="e6042-107">where `<source>` identifies the server and `<key>` is the key to save.</span></span> <span data-ttu-id="e6042-108">`<source>`을 생략 하면 nuget.org이 가정 됩니다.</span><span class="sxs-lookup"><span data-stu-id="e6042-108">If `<source>` is omitted, nuget.org is assumed.</span></span> 

> [!NOTE]
> <span data-ttu-id="e6042-109">API 키는 프라이빗 피드 인증에 사용되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="e6042-109">API key is not used for authenticating with the private feed.</span></span> <span data-ttu-id="e6042-110">소스 인증에 사용할 자격 증명을 관리하려면 [`nuget sources` 명령](../cli-reference/cli-ref-sources.md)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="e6042-110">Refer to [`nuget sources` command](../cli-reference/cli-ref-sources.md) to manage credentials for authenticating with the source.</span></span>
> <span data-ttu-id="e6042-111">API 키는 개별 NuGet 서버에서 가져올 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="e6042-111">API keys can be obtained from the individual NuGet servers.</span></span> <span data-ttu-id="e6042-112">Nuget.org에 대 한 APIKeys를 만들고 관리 하려면- [api 키](../../nuget-org/scoped-api-keys.md#acquire-an-api-key) 를 참조 하세요.</span><span class="sxs-lookup"><span data-stu-id="e6042-112">To create and manage APIKeys for nuget.org refer to [acquire-an-api-key](../../nuget-org/scoped-api-keys.md#acquire-an-api-key)</span></span>

## <a name="options"></a><span data-ttu-id="e6042-113">옵션</span><span class="sxs-lookup"><span data-stu-id="e6042-113">Options</span></span>

- **`-ConfigFile`**

  <span data-ttu-id="e6042-114">적용할 NuGet 구성 파일입니다.</span><span class="sxs-lookup"><span data-stu-id="e6042-114">The NuGet configuration file to apply.</span></span> <span data-ttu-id="e6042-115">지정 하지 않으면 `%AppData%\NuGet\NuGet.Config` (Windows) 또는 `~/.nuget/NuGet/NuGet.Config` 또는 `~/.config/NuGet/NuGet.Config` (Mac/Linux)가 사용 됩니다.</span><span class="sxs-lookup"><span data-stu-id="e6042-115">If not specified, `%AppData%\NuGet\NuGet.Config` (Windows), or `~/.nuget/NuGet/NuGet.Config` or `~/.config/NuGet/NuGet.Config` (Mac/Linux) is used.</span></span>

- **`-ForceEnglishOutput`**

  <span data-ttu-id="e6042-116">*(3.5 +)* 고정 된 영어 기반 문화권을 사용 하 여 nuget.exe을 강제로 실행 합니다.</span><span class="sxs-lookup"><span data-stu-id="e6042-116">*(3.5+)* Forces nuget.exe to run using an invariant, English-based culture.</span></span>

- **`-?|-help`**

  <span data-ttu-id="e6042-117">명령에 대 한 도움말 정보를 표시 합니다.</span><span class="sxs-lookup"><span data-stu-id="e6042-117">Displays help information for the command.</span></span>

- **`-NonInteractive`**

  <span data-ttu-id="e6042-118">사용자 입력 또는 확인에 대 한 프롬프트를 표시 하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="e6042-118">Suppresses prompts for user input or confirmations.</span></span>

- **`-src|-Source`**

  <span data-ttu-id="e6042-119">API 키가 유효한 서버 URL입니다.</span><span class="sxs-lookup"><span data-stu-id="e6042-119">Server URL where the API key is valid.</span></span>

- **`-Verbosity [normal|quiet|detailed]`**

  <span data-ttu-id="e6042-120">출력에 표시 되는 세부 정보의 양을 지정 합니다. `normal` (기본값), `quiet` 또는 `detailed` 입니다.</span><span class="sxs-lookup"><span data-stu-id="e6042-120">Specifies the amount of detail displayed in the output: `normal` (the default), `quiet`, or `detailed`.</span></span>

<span data-ttu-id="e6042-121">[환경 변수](cli-ref-environment-variables.md) 참조</span><span class="sxs-lookup"><span data-stu-id="e6042-121">Also see [Environment variables](cli-ref-environment-variables.md)</span></span>

## <a name="examples"></a><span data-ttu-id="e6042-122">예</span><span class="sxs-lookup"><span data-stu-id="e6042-122">Examples</span></span>

```cli
nuget setapikey 4003d786-cc37-4004-bfdf-c4f3e8ef9b3a

nuget setapikey 4003d786-cc37-4004-bfdf-c4f3e8ef9b3a -source https://example.com/nugetfeed
```
