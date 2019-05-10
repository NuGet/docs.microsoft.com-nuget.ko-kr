---
title: NuGet CLI 푸시 명령
description: Nuget.exe push 명령은 대 한 참조
author: karann-msft
ms.author: karann
ms.date: 01/18/2018
ms.topic: reference
ms.openlocfilehash: 4a9460944e2c232e2a72195434a491d26eee3559
ms.sourcegitcommit: 3fc93f7a64be040699fe12125977dd25a7948470
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/29/2019
ms.locfileid: "64877953"
---
# <a name="push-command-nuget-cli"></a><span data-ttu-id="2781e-103">push 명령은 (NuGet CLI)</span><span class="sxs-lookup"><span data-stu-id="2781e-103">push command (NuGet CLI)</span></span>

<span data-ttu-id="2781e-104">**적용 대상:** 게시 패키지 &bullet; **지원 되는 버전:** 모든; nuget.org에 필요한 4.1.0 이상</span><span class="sxs-lookup"><span data-stu-id="2781e-104">**Applies to:** package publishing &bullet; **Supported versions:** all; 4.1.0+ required for nuget.org</span></span>

> [!Important]
> <span data-ttu-id="2781e-105">Nuget.org에 패키지를 푸시 하려면 사용 해야 nuget.exe v4.1.0 이상, 필수 구현한 [NuGet 프로토콜](../api/nuget-protocols.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="2781e-105">To push packages to nuget.org you must use nuget.exe v4.1.0+, which implements the required [NuGet protocols](../api/nuget-protocols.md).</span></span>

<span data-ttu-id="2781e-106">패키지 원본에 패키지를 푸시하고 게시 합니다.</span><span class="sxs-lookup"><span data-stu-id="2781e-106">Pushes a package to a package source and publishes it.</span></span>

<span data-ttu-id="2781e-107">NuGet의 기본 구성을 로드 하 여 가져올 `%AppData%\NuGet\NuGet.Config` (Windows) 또는 `~/.nuget/NuGet/NuGet.Config` (Mac/Linux), 모든 로드 한 다음 `Nuget.Config` 하거나 `.nuget\Nuget.Config` 드라이브의 루트에서 시작 하 고 현재 디렉터리에서 끝나는 파일 (참조 [구성 NuGet 동작](../consume-packages/configuring-nuget-behavior.md))</span><span class="sxs-lookup"><span data-stu-id="2781e-107">NuGet's default configuration is obtained by loading `%AppData%\NuGet\NuGet.Config` (Windows) or `~/.nuget/NuGet/NuGet.Config` (Mac/Linux), then loading any `Nuget.Config` or `.nuget\Nuget.Config` files starting from root of drive and ending in current directory (see [Configuring NuGet Behavior](../consume-packages/configuring-nuget-behavior.md))</span></span>

## <a name="usage"></a><span data-ttu-id="2781e-108">사용법</span><span class="sxs-lookup"><span data-stu-id="2781e-108">Usage</span></span>

```cli
nuget push <packagePath> [options]
```

<span data-ttu-id="2781e-109">여기서 `<packagePath>` 서버로 푸시 하려면 패키지를 식별 합니다.</span><span class="sxs-lookup"><span data-stu-id="2781e-109">where `<packagePath>` identifies the package to push to the server.</span></span>

## <a name="options"></a><span data-ttu-id="2781e-110">옵션</span><span class="sxs-lookup"><span data-stu-id="2781e-110">Options</span></span>

| <span data-ttu-id="2781e-111">옵션</span><span class="sxs-lookup"><span data-stu-id="2781e-111">Option</span></span> | <span data-ttu-id="2781e-112">설명</span><span class="sxs-lookup"><span data-stu-id="2781e-112">Description</span></span> |
| --- | --- |
| <span data-ttu-id="2781e-113">ApiKey</span><span class="sxs-lookup"><span data-stu-id="2781e-113">ApiKey</span></span> | <span data-ttu-id="2781e-114">대상 리포지토리에 대한 API 키입니다.</span><span class="sxs-lookup"><span data-stu-id="2781e-114">The API key for the target repository.</span></span> <span data-ttu-id="2781e-115">없는 경우 구성 파일에 지정 된 사용 됩니다.</span><span class="sxs-lookup"><span data-stu-id="2781e-115">If not present,  the one specified in the config file is used.</span></span> |
| <span data-ttu-id="2781e-116">ConfigFile</span><span class="sxs-lookup"><span data-stu-id="2781e-116">ConfigFile</span></span> | <span data-ttu-id="2781e-117">적용할 NuGet 설정 파일입니다.</span><span class="sxs-lookup"><span data-stu-id="2781e-117">The NuGet configuration file to apply.</span></span> <span data-ttu-id="2781e-118">지정하지 않으면 기본적으로 Windows에서는 `%AppData%\NuGet\NuGet.Config`, Mac이나 Linux에서는 `~/.nuget/NuGet/NuGet.Config`가 사용됩니다.</span><span class="sxs-lookup"><span data-stu-id="2781e-118">If not specified, `%AppData%\NuGet\NuGet.Config` (Windows) or `~/.nuget/NuGet/NuGet.Config` (Mac/Linux) is used.</span></span>|
| <span data-ttu-id="2781e-119">DisableBuffering</span><span class="sxs-lookup"><span data-stu-id="2781e-119">DisableBuffering</span></span> | <span data-ttu-id="2781e-120">메모리 사용량을 줄이려면 http (s) 서버로 푸시할 때 버퍼링 하는 사용 하지 않도록 설정 합니다.</span><span class="sxs-lookup"><span data-stu-id="2781e-120">Disables buffering when pushing to an HTTP(s) server to decrease memory usages.</span></span> <span data-ttu-id="2781e-121">주의:이 옵션을 사용 하는 통합된 Windows 인증 작동 하지 않을 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="2781e-121">Caution: when this option is used, integrated Windows authentication might not work.</span></span> |
| <span data-ttu-id="2781e-122">ForceEnglishOutput</span><span class="sxs-lookup"><span data-stu-id="2781e-122">ForceEnglishOutput</span></span> | <span data-ttu-id="2781e-123">*(3.5 이상)*  현재 언어 설정을 무시하고 영어를 기반으로 nuget.exe를 강제로 실행합니다.</span><span class="sxs-lookup"><span data-stu-id="2781e-123">*(3.5+)* Forces nuget.exe to run using an invariant, English-based culture.</span></span> |
| <span data-ttu-id="2781e-124">Help</span><span class="sxs-lookup"><span data-stu-id="2781e-124">Help</span></span> | <span data-ttu-id="2781e-125">명령어에 대한 도움말을 표시합니다.</span><span class="sxs-lookup"><span data-stu-id="2781e-125">Displays help information for the command.</span></span> |
| <span data-ttu-id="2781e-126">NonInteractive</span><span class="sxs-lookup"><span data-stu-id="2781e-126">NonInteractive</span></span> | <span data-ttu-id="2781e-127">사용자 입력이나 확인에 대한 프롬프트를 표시하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="2781e-127">Suppresses prompts for user input or confirmations.</span></span> |
| <span data-ttu-id="2781e-128">NoSymbols</span><span class="sxs-lookup"><span data-stu-id="2781e-128">NoSymbols</span></span> | <span data-ttu-id="2781e-129">*(3.5 이상)*  기호 패키지가 있으면 해당 푸시되 지 않습니다 기호 서버에 있습니다.</span><span class="sxs-lookup"><span data-stu-id="2781e-129">*(3.5+)* If a symbols package exists, it will not be pushed to a symbol server.</span></span> |
| <span data-ttu-id="2781e-130">Source</span><span class="sxs-lookup"><span data-stu-id="2781e-130">Source</span></span> | <span data-ttu-id="2781e-131">서버 URL을 지정합니다.</span><span class="sxs-lookup"><span data-stu-id="2781e-131">Specifies the server URL.</span></span> <span data-ttu-id="2781e-132">NuGet은 UNC 또는 로컬 폴더 소스를 식별 하 고 간단히 HTTP를 사용 하 여 푸시하는 대신에 있는 파일을 복사 합니다.</span><span class="sxs-lookup"><span data-stu-id="2781e-132">NuGet identifies a UNC or local folder source and simply copies the file there instead of pushing it using HTTP.</span></span>  <span data-ttu-id="2781e-133">또한 NuGet 3.4.2부터이 않는 필수 매개 변수를 `NuGet.Config` 파일 지정을 *DefaultPushSource* 값 (참조 [NuGet 동작 구성](../consume-packages/configuring-nuget-behavior.md)).</span><span class="sxs-lookup"><span data-stu-id="2781e-133">Also, starting with NuGet 3.4.2, this is a mandatory parameter unless the `NuGet.Config` file specifies a *DefaultPushSource* value (see [Configuring NuGet behavior](../consume-packages/configuring-nuget-behavior.md)).</span></span> |
| <span data-ttu-id="2781e-134">SymbolSource</span><span class="sxs-lookup"><span data-stu-id="2781e-134">SymbolSource</span></span> | <span data-ttu-id="2781e-135">*(3.5 이상)*  기호 서버 URL을 지정 합니다. 즉 nuget.org에 푸시할 때 nuget.smbsrc.net는</span><span class="sxs-lookup"><span data-stu-id="2781e-135">*(3.5+)* Specifies the symbol server URL; nuget.smbsrc.net is used when pushing to nuget.org</span></span> |
| <span data-ttu-id="2781e-136">SymbolApiKey</span><span class="sxs-lookup"><span data-stu-id="2781e-136">SymbolApiKey</span></span> | <span data-ttu-id="2781e-137">*(3.5 이상)*  에 지정 된 URL에 대 한 API 키를 지정 `-SymbolSource`합니다.</span><span class="sxs-lookup"><span data-stu-id="2781e-137">*(3.5+)* Specifies the API key for the URL specified in `-SymbolSource`.</span></span> |
| <span data-ttu-id="2781e-138">제한 시간</span><span class="sxs-lookup"><span data-stu-id="2781e-138">Timeout</span></span> | <span data-ttu-id="2781e-139">서버에 푸시하기 위한 초 제한 시간을 지정 합니다.</span><span class="sxs-lookup"><span data-stu-id="2781e-139">Specifies the timeout, in seconds, for pushing to a server.</span></span> <span data-ttu-id="2781e-140">기본값은 300 초 (5 분).</span><span class="sxs-lookup"><span data-stu-id="2781e-140">The default is 300 seconds (5 minutes).</span></span> |
| <span data-ttu-id="2781e-141">Verbosity</span><span class="sxs-lookup"><span data-stu-id="2781e-141">Verbosity</span></span> | <span data-ttu-id="2781e-142">출력에 표시되는 세부정보의 양을 지정합니다: *정상적인*, *조용한*, *자세한*합니다.</span><span class="sxs-lookup"><span data-stu-id="2781e-142">Specifies the amount of detail displayed in the output: *normal*, *quiet*, *detailed*.</span></span> |

<span data-ttu-id="2781e-143">또한 [환경 변수](cli-ref-environment-variables.md)에 대한 정보를 참조할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="2781e-143">Also see [Environment variables](cli-ref-environment-variables.md)</span></span>

## <a name="examples"></a><span data-ttu-id="2781e-144">예제</span><span class="sxs-lookup"><span data-stu-id="2781e-144">Examples</span></span>

```cli
nuget push foo.nupkg

nuget push foo.symbols.nupkg

nuget push foo.nupkg -Timeout 360

nuget push *.nupkg

nuget.exe push -source \\mycompany\repo\ mypackage.1.0.0.nupkg

nuget push foo.nupkg 4003d786-cc37-4004-bfdf-c4f3e8ef9b3a -Source https://api.nuget.org/v3/index.json

nuget push foo.nupkg 4003d786-cc37-4004-bfdf-c4f3e8ef9b3a

nuget push foo.nupkg 4003d786-cc37-4004-bfdf-c4f3e8ef9b3a -src https://customsource/
```
