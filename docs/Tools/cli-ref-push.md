---
title: "NuGet CLI 푸시 명령을 | Microsoft Docs"
author: kraigb
ms.author: kraigb
manager: ghogen
ms.date: 01/18/2018
ms.topic: reference
ms.prod: nuget
ms.technology: 
description: "Nuget.exe 푸시 명령에 대 한 참조"
keywords: "nuget 푸시 참조, 푸시 명령"
ms.reviewer:
- karann-msft
- unniravindranathan
ms.openlocfilehash: df8ef42f650a20b92a281fff3e597ac8d484544e
ms.sourcegitcommit: b0af28d1c809c7e951b0817d306643fcc162a030
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 02/14/2018
---
# <a name="push-command-nuget-cli"></a><span data-ttu-id="dfa6e-104">푸시 명령 (NuGet CLI)</span><span class="sxs-lookup"><span data-stu-id="dfa6e-104">push command (NuGet CLI)</span></span>

<span data-ttu-id="dfa6e-105">**적용 대상:** 게시 패키지 &bullet; **지원 되는 버전:** 모든; 4.1.0+ nuget.org에 필요한</span><span class="sxs-lookup"><span data-stu-id="dfa6e-105">**Applies to:** package publishing &bullet; **Supported versions:** all; 4.1.0+ required for nuget.org</span></span>

> [!Important]
> <span data-ttu-id="dfa6e-106">Nuget.org를 패키지를 강제를 사용 해야 nuget.exe v4.1.0 +에서 구현 하는 필수는 [NuGet 프로토콜](../api/nuget-protocols.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="dfa6e-106">To push packages to nuget.org you must use nuget.exe v4.1.0+, which implements the required [NuGet protocols](../api/nuget-protocols.md).</span></span>

<span data-ttu-id="dfa6e-107">패키지를 패키지 원본에 푸시합니다를 게시 합니다.</span><span class="sxs-lookup"><span data-stu-id="dfa6e-107">Pushes a package to a package source and publishes it.</span></span>

<span data-ttu-id="dfa6e-108">NuGet의 기본 구성을 로드 하 여 가져온 `%AppData%\NuGet\NuGet.Config`을 로드 한 다음 `Nuget.Config` 또는 `.nuget\Nuget.Config` 드라이브의 루트에서 시작 하 고 현재 디렉터리에서 끝나는 파일 (참조 [NuGet 동작 구성](../consume-packages/configuring-nuget-behavior.md))</span><span class="sxs-lookup"><span data-stu-id="dfa6e-108">NuGet's default configuration is obtained by loading `%AppData%\NuGet\NuGet.Config`, then loading any `Nuget.Config` or `.nuget\Nuget.Config` files starting from root of drive and ending in current directory (see [Configuring NuGet Behavior](../consume-packages/configuring-nuget-behavior.md))</span></span>

## <a name="usage"></a><span data-ttu-id="dfa6e-109">사용법</span><span class="sxs-lookup"><span data-stu-id="dfa6e-109">Usage</span></span>

```cli
nuget push <packagePath> [options]
```

<span data-ttu-id="dfa6e-110">여기서 `<packagePath>` 패키지는 서버에 대 한 푸시를 식별 합니다.</span><span class="sxs-lookup"><span data-stu-id="dfa6e-110">where `<packagePath>` identifies the package to push to the server.</span></span>

## <a name="options"></a><span data-ttu-id="dfa6e-111">옵션</span><span class="sxs-lookup"><span data-stu-id="dfa6e-111">Options</span></span>

| <span data-ttu-id="dfa6e-112">옵션</span><span class="sxs-lookup"><span data-stu-id="dfa6e-112">Option</span></span> | <span data-ttu-id="dfa6e-113">설명</span><span class="sxs-lookup"><span data-stu-id="dfa6e-113">Description</span></span> |
| --- | --- |
| <span data-ttu-id="dfa6e-114">apiKey</span><span class="sxs-lookup"><span data-stu-id="dfa6e-114">ApiKey</span></span> | <span data-ttu-id="dfa6e-115">대상 저장소에 대 한 API 키입니다.</span><span class="sxs-lookup"><span data-stu-id="dfa6e-115">The API key for the target repository.</span></span> <span data-ttu-id="dfa6e-116">없음, 1에 지정 된 경우 *%AppData%\NuGet\NuGet.Config* 사용 됩니다.</span><span class="sxs-lookup"><span data-stu-id="dfa6e-116">If not present,  the one specified in *%AppData%\NuGet\NuGet.Config* is used.</span></span> |
| <span data-ttu-id="dfa6e-117">ConfigFile</span><span class="sxs-lookup"><span data-stu-id="dfa6e-117">ConfigFile</span></span> | <span data-ttu-id="dfa6e-118">적용할 NuGet 구성 파일입니다.</span><span class="sxs-lookup"><span data-stu-id="dfa6e-118">The NuGet configuration file to apply.</span></span> <span data-ttu-id="dfa6e-119">지정 하지 않으면 *%AppData%\NuGet\NuGet.Config* 사용 됩니다.</span><span class="sxs-lookup"><span data-stu-id="dfa6e-119">If not specified, *%AppData%\NuGet\NuGet.Config* is used.</span></span> |
| <span data-ttu-id="dfa6e-120">DisableBuffering</span><span class="sxs-lookup"><span data-stu-id="dfa6e-120">DisableBuffering</span></span> | <span data-ttu-id="dfa6e-121">메모리 사용량을 줄이기 위해 http (s) 서버에 적용할 때 버퍼링 하는 데 사용 하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="dfa6e-121">Disables buffering when pushing to an HTTP(s) server to decrease memory usages.</span></span> <span data-ttu-id="dfa6e-122">주의:이 옵션을 사용 Windows 통합된 인증 작동 하지 않을 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="dfa6e-122">Caution: when this option is used, integrated Windows authentication might not work.</span></span> |
| <span data-ttu-id="dfa6e-123">ForceEnglishOutput</span><span class="sxs-lookup"><span data-stu-id="dfa6e-123">ForceEnglishOutput</span></span> | <span data-ttu-id="dfa6e-124">*(3.5 +)*  고정, 영어 기반 문화권을 사용 하 여 실행할 nuget.exe를 강제로 수행 합니다.</span><span class="sxs-lookup"><span data-stu-id="dfa6e-124">*(3.5+)* Forces nuget.exe to run using an invariant, English-based culture.</span></span> |
| <span data-ttu-id="dfa6e-125">도움말</span><span class="sxs-lookup"><span data-stu-id="dfa6e-125">Help</span></span> | <span data-ttu-id="dfa6e-126">도움말의 명령에 대 한 정보를 표시 합니다.</span><span class="sxs-lookup"><span data-stu-id="dfa6e-126">Displays help information for the command.</span></span> |
| <span data-ttu-id="dfa6e-127">NonInteractive</span><span class="sxs-lookup"><span data-stu-id="dfa6e-127">NonInteractive</span></span> | <span data-ttu-id="dfa6e-128">사용자 입력 또는 확인에 대 한 프롬프트를 표시 하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="dfa6e-128">Suppresses prompts for user input or confirmations.</span></span> |
| <span data-ttu-id="dfa6e-129">NoSymbols</span><span class="sxs-lookup"><span data-stu-id="dfa6e-129">NoSymbols</span></span> | <span data-ttu-id="dfa6e-130">*(3.5 +)*  기호 패키지 있으면 해당 기호 서버에 푸시되 지 것입니다.</span><span class="sxs-lookup"><span data-stu-id="dfa6e-130">*(3.5+)* If a symbols package exists, it will not be pushed to a symbol server.</span></span> |
| <span data-ttu-id="dfa6e-131">소스</span><span class="sxs-lookup"><span data-stu-id="dfa6e-131">Source</span></span> | <span data-ttu-id="dfa6e-132">서버 URL을 지정합니다.</span><span class="sxs-lookup"><span data-stu-id="dfa6e-132">Specifies the server URL.</span></span> <span data-ttu-id="dfa6e-133">NuGet은 UNC 또는 로컬 폴더 소스를 식별 하 고 간단히 HTTP를 사용 하 여 푸시하는 대신 거기 파일을 복사 합니다.</span><span class="sxs-lookup"><span data-stu-id="dfa6e-133">NuGet identifies a UNC or local folder source and simply copies the file there instead of pushing it using HTTP.</span></span>  <span data-ttu-id="dfa6e-134">또한 NuGet 3.4.2 부터는이 표시 되지 않으면 필수 매개 변수는 `NuGet.Config` 파일 지정는 *DefaultPushSource* 값 (참조 [NuGet 구성 동작](../consume-packages/configuring-nuget-behavior.md)).</span><span class="sxs-lookup"><span data-stu-id="dfa6e-134">Also, starting with NuGet 3.4.2, this is a mandatory parameter unless the `NuGet.Config` file specifies a *DefaultPushSource* value (see [Configuring NuGet behavior](../consume-packages/configuring-nuget-behavior.md)).</span></span> |
| <span data-ttu-id="dfa6e-135">SymbolSource</span><span class="sxs-lookup"><span data-stu-id="dfa6e-135">SymbolSource</span></span> | <span data-ttu-id="dfa6e-136">*(3.5 +)*  기호 서버 URL을 지정 합니다. 즉 nuget.smbsrc.net nuget.org를 푸시할 때 사용 됩니다</span><span class="sxs-lookup"><span data-stu-id="dfa6e-136">*(3.5+)* Specifies the symbol server URL; nuget.smbsrc.net is used when pushing to nuget.org</span></span> |
| <span data-ttu-id="dfa6e-137">SymbolApiKey</span><span class="sxs-lookup"><span data-stu-id="dfa6e-137">SymbolApiKey</span></span> | <span data-ttu-id="dfa6e-138">*(3.5 +)*  에 지정 된 URL에 대 한 API 키 지정 `-SymbolSource`합니다.</span><span class="sxs-lookup"><span data-stu-id="dfa6e-138">*(3.5+)* Specifies the API key for the URL specified in `-SymbolSource`.</span></span> |
| <span data-ttu-id="dfa6e-139">시간 제한</span><span class="sxs-lookup"><span data-stu-id="dfa6e-139">Timeout</span></span> | <span data-ttu-id="dfa6e-140">서버에 밀어 넣는 초 제한 시간을 지정 합니다.</span><span class="sxs-lookup"><span data-stu-id="dfa6e-140">Specifies the timeout, in seconds, for pushing to a server.</span></span> <span data-ttu-id="dfa6e-141">기본값은 300 초 (5 분)입니다.</span><span class="sxs-lookup"><span data-stu-id="dfa6e-141">The default is 300 seconds (5 minutes).</span></span> |
| <span data-ttu-id="dfa6e-142">자세한 정도</span><span class="sxs-lookup"><span data-stu-id="dfa6e-142">Verbosity</span></span> | <span data-ttu-id="dfa6e-143">출력에 표시 되는 세부 정보 수준을 지정: *일반*, *quiet*, *자세한*합니다.</span><span class="sxs-lookup"><span data-stu-id="dfa6e-143">Specifies the amount of detail displayed in the output: *normal*, *quiet*, *detailed*.</span></span> |

<span data-ttu-id="dfa6e-144">또한 참조 [환경 변수](cli-ref-environment-variables.md)</span><span class="sxs-lookup"><span data-stu-id="dfa6e-144">Also see [Environment variables](cli-ref-environment-variables.md)</span></span>

## <a name="examples"></a><span data-ttu-id="dfa6e-145">예제</span><span class="sxs-lookup"><span data-stu-id="dfa6e-145">Examples</span></span>

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
