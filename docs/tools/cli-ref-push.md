---
title: NuGet CLI 푸시 명령
description: Nuget.exe push 명령은 대 한 참조
author: karann-msft
ms.author: karann
ms.date: 01/18/2018
ms.topic: reference
ms.openlocfilehash: 125671ca3f695f82bd74f8097e590c3972003e22
ms.sourcegitcommit: 1d1406764c6af5fb7801d462e0c4afc9092fa569
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 09/04/2018
ms.locfileid: "43548345"
---
# <a name="push-command-nuget-cli"></a><span data-ttu-id="82514-103">push 명령은 (NuGet CLI)</span><span class="sxs-lookup"><span data-stu-id="82514-103">push command (NuGet CLI)</span></span>

<span data-ttu-id="82514-104">**적용 대상:** 게시 패키지 &bullet; **지원 되는 버전:** 모든; nuget.org에 필요한 4.1.0 이상</span><span class="sxs-lookup"><span data-stu-id="82514-104">**Applies to:** package publishing &bullet; **Supported versions:** all; 4.1.0+ required for nuget.org</span></span>

> [!Important]
> <span data-ttu-id="82514-105">Nuget.org에 패키지를 푸시 하려면 사용 해야 nuget.exe v4.1.0 이상, 필수 구현한 [NuGet 프로토콜](../api/nuget-protocols.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="82514-105">To push packages to nuget.org you must use nuget.exe v4.1.0+, which implements the required [NuGet protocols](../api/nuget-protocols.md).</span></span>

<span data-ttu-id="82514-106">패키지 원본에 패키지를 푸시하고 게시 합니다.</span><span class="sxs-lookup"><span data-stu-id="82514-106">Pushes a package to a package source and publishes it.</span></span>

<span data-ttu-id="82514-107">NuGet의 기본 구성을 로드 하 여 가져올 `%AppData%\NuGet\NuGet.Config` (Windows) 또는 `~/.nuget/NuGet/NuGet.Config` (Mac/Linux), 모든 로드 한 다음 `Nuget.Config` 하거나 `.nuget\Nuget.Config` 드라이브의 루트에서 시작 하 고 현재 디렉터리에서 끝나는 파일 (참조 [구성 NuGet 동작](../consume-packages/configuring-nuget-behavior.md))</span><span class="sxs-lookup"><span data-stu-id="82514-107">NuGet's default configuration is obtained by loading `%AppData%\NuGet\NuGet.Config` (Windows) or `~/.nuget/NuGet/NuGet.Config` (Mac/Linux), then loading any `Nuget.Config` or `.nuget\Nuget.Config` files starting from root of drive and ending in current directory (see [Configuring NuGet Behavior](../consume-packages/configuring-nuget-behavior.md))</span></span>

## <a name="usage"></a><span data-ttu-id="82514-108">사용법</span><span class="sxs-lookup"><span data-stu-id="82514-108">Usage</span></span>

```cli
nuget push <packagePath> [options]
```

<span data-ttu-id="82514-109">여기서 `<packagePath>` 서버로 푸시 하려면 패키지를 식별 합니다.</span><span class="sxs-lookup"><span data-stu-id="82514-109">where `<packagePath>` identifies the package to push to the server.</span></span>

## <a name="options"></a><span data-ttu-id="82514-110">옵션</span><span class="sxs-lookup"><span data-stu-id="82514-110">Options</span></span>

| <span data-ttu-id="82514-111">옵션</span><span class="sxs-lookup"><span data-stu-id="82514-111">Option</span></span> | <span data-ttu-id="82514-112">설명</span><span class="sxs-lookup"><span data-stu-id="82514-112">Description</span></span> |
| --- | --- |
| <span data-ttu-id="82514-113">ApiKey</span><span class="sxs-lookup"><span data-stu-id="82514-113">ApiKey</span></span> | <span data-ttu-id="82514-114">대상 리포지토리에 대 한 API 키입니다.</span><span class="sxs-lookup"><span data-stu-id="82514-114">The API key for the target repository.</span></span> <span data-ttu-id="82514-115">없는 경우 구성 파일에 지정 된 사용 됩니다.</span><span class="sxs-lookup"><span data-stu-id="82514-115">If not present,  the one specified in the config file is used.</span></span> |
| <span data-ttu-id="82514-116">ConfigFile</span><span class="sxs-lookup"><span data-stu-id="82514-116">ConfigFile</span></span> | <span data-ttu-id="82514-117">NuGet 구성 파일을 적용 합니다.</span><span class="sxs-lookup"><span data-stu-id="82514-117">The NuGet configuration file to apply.</span></span> <span data-ttu-id="82514-118">지정 하지 않으면 `%AppData%\NuGet\NuGet.Config` (Windows) 또는 `~/.nuget/NuGet/NuGet.Config` (Mac/Linux)가 사용 됩니다.</span><span class="sxs-lookup"><span data-stu-id="82514-118">If not specified, `%AppData%\NuGet\NuGet.Config` (Windows) or `~/.nuget/NuGet/NuGet.Config` (Mac/Linux) is used.</span></span>|
| <span data-ttu-id="82514-119">DisableBuffering</span><span class="sxs-lookup"><span data-stu-id="82514-119">DisableBuffering</span></span> | <span data-ttu-id="82514-120">메모리 사용량을 줄이려면 http (s) 서버로 푸시할 때 버퍼링 하는 사용 하지 않도록 설정 합니다.</span><span class="sxs-lookup"><span data-stu-id="82514-120">Disables buffering when pushing to an HTTP(s) server to decrease memory usages.</span></span> <span data-ttu-id="82514-121">주의:이 옵션을 사용 하는 통합된 Windows 인증 작동 하지 않을 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="82514-121">Caution: when this option is used, integrated Windows authentication might not work.</span></span> |
| <span data-ttu-id="82514-122">ForceEnglishOutput</span><span class="sxs-lookup"><span data-stu-id="82514-122">ForceEnglishOutput</span></span> | <span data-ttu-id="82514-123">*(3.5 이상)*  고정 영어 기반 문화권을 사용 하 여 실행할 nuget.exe를 강제로 수행 합니다.</span><span class="sxs-lookup"><span data-stu-id="82514-123">*(3.5+)* Forces nuget.exe to run using an invariant, English-based culture.</span></span> |
| <span data-ttu-id="82514-124">도움말</span><span class="sxs-lookup"><span data-stu-id="82514-124">Help</span></span> | <span data-ttu-id="82514-125">도움말의 명령에 대 한 정보를 표시 합니다.</span><span class="sxs-lookup"><span data-stu-id="82514-125">Displays help information for the command.</span></span> |
| <span data-ttu-id="82514-126">NonInteractive</span><span class="sxs-lookup"><span data-stu-id="82514-126">NonInteractive</span></span> | <span data-ttu-id="82514-127">사용자 입력 또는 확인에 대 한 프롬프트를 표시 하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="82514-127">Suppresses prompts for user input or confirmations.</span></span> |
| <span data-ttu-id="82514-128">NoSymbols</span><span class="sxs-lookup"><span data-stu-id="82514-128">NoSymbols</span></span> | <span data-ttu-id="82514-129">*(3.5 이상)*  기호 패키지가 있으면 해당 푸시되 지 않습니다 기호 서버에 있습니다.</span><span class="sxs-lookup"><span data-stu-id="82514-129">*(3.5+)* If a symbols package exists, it will not be pushed to a symbol server.</span></span> |
| <span data-ttu-id="82514-130">소스</span><span class="sxs-lookup"><span data-stu-id="82514-130">Source</span></span> | <span data-ttu-id="82514-131">서버 URL을 지정합니다.</span><span class="sxs-lookup"><span data-stu-id="82514-131">Specifies the server URL.</span></span> <span data-ttu-id="82514-132">NuGet은 UNC 또는 로컬 폴더 소스를 식별 하 고 간단히 HTTP를 사용 하 여 푸시하는 대신에 있는 파일을 복사 합니다.</span><span class="sxs-lookup"><span data-stu-id="82514-132">NuGet identifies a UNC or local folder source and simply copies the file there instead of pushing it using HTTP.</span></span>  <span data-ttu-id="82514-133">또한 NuGet 3.4.2부터이 않는 필수 매개 변수를 `NuGet.Config` 파일 지정을 *DefaultPushSource* 값 (참조 [NuGet 동작 구성](../consume-packages/configuring-nuget-behavior.md)).</span><span class="sxs-lookup"><span data-stu-id="82514-133">Also, starting with NuGet 3.4.2, this is a mandatory parameter unless the `NuGet.Config` file specifies a *DefaultPushSource* value (see [Configuring NuGet behavior](../consume-packages/configuring-nuget-behavior.md)).</span></span> |
| <span data-ttu-id="82514-134">SymbolSource</span><span class="sxs-lookup"><span data-stu-id="82514-134">SymbolSource</span></span> | <span data-ttu-id="82514-135">*(3.5 이상)*  기호 서버 URL을 지정 합니다. 즉 nuget.org에 푸시할 때 nuget.smbsrc.net는</span><span class="sxs-lookup"><span data-stu-id="82514-135">*(3.5+)* Specifies the symbol server URL; nuget.smbsrc.net is used when pushing to nuget.org</span></span> |
| <span data-ttu-id="82514-136">SymbolApiKey</span><span class="sxs-lookup"><span data-stu-id="82514-136">SymbolApiKey</span></span> | <span data-ttu-id="82514-137">*(3.5 이상)*  에 지정 된 URL에 대 한 API 키를 지정 `-SymbolSource`합니다.</span><span class="sxs-lookup"><span data-stu-id="82514-137">*(3.5+)* Specifies the API key for the URL specified in `-SymbolSource`.</span></span> |
| <span data-ttu-id="82514-138">시간 제한</span><span class="sxs-lookup"><span data-stu-id="82514-138">Timeout</span></span> | <span data-ttu-id="82514-139">서버에 푸시하기 위한 초 제한 시간을 지정 합니다.</span><span class="sxs-lookup"><span data-stu-id="82514-139">Specifies the timeout, in seconds, for pushing to a server.</span></span> <span data-ttu-id="82514-140">기본값은 300 초 (5 분).</span><span class="sxs-lookup"><span data-stu-id="82514-140">The default is 300 seconds (5 minutes).</span></span> |
| <span data-ttu-id="82514-141">자세한 정도</span><span class="sxs-lookup"><span data-stu-id="82514-141">Verbosity</span></span> | <span data-ttu-id="82514-142">출력에 표시 되는 세부 정보의 양을 지정: *정상적인*, *quiet*, *자세한*합니다.</span><span class="sxs-lookup"><span data-stu-id="82514-142">Specifies the amount of detail displayed in the output: *normal*, *quiet*, *detailed*.</span></span> |

<span data-ttu-id="82514-143">또한 참조 [환경 변수](cli-ref-environment-variables.md)</span><span class="sxs-lookup"><span data-stu-id="82514-143">Also see [Environment variables](cli-ref-environment-variables.md)</span></span>

## <a name="examples"></a><span data-ttu-id="82514-144">예제</span><span class="sxs-lookup"><span data-stu-id="82514-144">Examples</span></span>

```cli
nuget push foo.nupkg

nuget push foo.symbols.nupkg

nuget push foo.nupkg -Timeout 360

nuget push *.nupkg

nuget.exe push -source \\mycompany\repo\ mypackage.1.0.0.nupkg

nuget push foo.nupkg 4003d786-cc37-4004-bfdf-c4f3e8ef9b3a -Source https://api.nuget.org/v3/index.json

nuget push foo.nupkg 4003d786-cc37-4004-bfdf-c4f3e8ef9b3a

nuget push foo.nupkg 4003d786-cc37-4004-bfdf-c4f3e8ef9b3a -s https://customsource/
```
