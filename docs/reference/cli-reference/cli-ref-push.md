---
title: NuGet CLI push 명령
description: Nuget.exe push 명령에 대 한 참조
author: karann-msft
ms.author: karann
ms.date: 01/18/2018
ms.topic: reference
ms.openlocfilehash: 40b2b2970934bae82c46cbe69156948e90746f97
ms.sourcegitcommit: efc18d484fdf0c7a8979b564dcb191c030601bb4
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/18/2019
ms.locfileid: "68327630"
---
# <a name="push-command-nuget-cli"></a><span data-ttu-id="8f854-103">push 명령 (NuGet CLI)</span><span class="sxs-lookup"><span data-stu-id="8f854-103">push command (NuGet CLI)</span></span>

<span data-ttu-id="8f854-104">**적용 대상:** 패키지 게시 &bullet; **지원 버전:** 모두, 4.1.0 + nuget.org에 필요 합니다.</span><span class="sxs-lookup"><span data-stu-id="8f854-104">**Applies to:** package publishing &bullet; **Supported versions:** all; 4.1.0+ required for nuget.org</span></span>

> [!Important]
> <span data-ttu-id="8f854-105">Nuget.org에 패키지를 푸시 하려면 필요한 [nuget 프로토콜](../../api/nuget-protocols.md)을 구현 하는 nuget.exe v 4.1.0 +를 사용 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="8f854-105">To push packages to nuget.org you must use nuget.exe v4.1.0+, which implements the required [NuGet protocols](../../api/nuget-protocols.md).</span></span>

<span data-ttu-id="8f854-106">패키지 소스에 패키지를 푸시하고 게시 합니다.</span><span class="sxs-lookup"><span data-stu-id="8f854-106">Pushes a package to a package source and publishes it.</span></span>

<span data-ttu-id="8f854-107">NuGet의 기본 구성은 (Windows) 또는 `%AppData%\NuGet\NuGet.Config` `~/.nuget/NuGet/NuGet.Config` (Mac/Linux `Nuget.Config` )를 로드 한 다음 드라이브의 루트에서 시작 `.nuget\Nuget.Config` 하 여 현재 디렉터리에서 끝나는 또는 파일을 로드 하 여 가져옵니다 ( [일반적인 NuGet 참조). 구성](../../consume-packages/configuring-nuget-behavior.md))</span><span class="sxs-lookup"><span data-stu-id="8f854-107">NuGet's default configuration is obtained by loading `%AppData%\NuGet\NuGet.Config` (Windows) or `~/.nuget/NuGet/NuGet.Config` (Mac/Linux), then loading any `Nuget.Config` or `.nuget\Nuget.Config` files starting from root of drive and ending in current directory (see [Common NuGet configurations](../../consume-packages/configuring-nuget-behavior.md))</span></span>

## <a name="usage"></a><span data-ttu-id="8f854-108">사용법</span><span class="sxs-lookup"><span data-stu-id="8f854-108">Usage</span></span>

```cli
nuget push <packagePath> [options]
```

<span data-ttu-id="8f854-109">여기서 `<packagePath>` 는 서버에 푸시할 패키지를 식별 합니다.</span><span class="sxs-lookup"><span data-stu-id="8f854-109">where `<packagePath>` identifies the package to push to the server.</span></span>

## <a name="options"></a><span data-ttu-id="8f854-110">변수</span><span class="sxs-lookup"><span data-stu-id="8f854-110">Options</span></span>

| <span data-ttu-id="8f854-111">옵션</span><span class="sxs-lookup"><span data-stu-id="8f854-111">Option</span></span> | <span data-ttu-id="8f854-112">설명</span><span class="sxs-lookup"><span data-stu-id="8f854-112">Description</span></span> |
| --- | --- |
| <span data-ttu-id="8f854-113">ApiKey</span><span class="sxs-lookup"><span data-stu-id="8f854-113">ApiKey</span></span> | <span data-ttu-id="8f854-114">대상 리포지토리에 대한 API 키입니다.</span><span class="sxs-lookup"><span data-stu-id="8f854-114">The API key for the target repository.</span></span> <span data-ttu-id="8f854-115">존재 하지 않는 경우 구성 파일에 지정 된 항목을 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="8f854-115">If not present,  the one specified in the config file is used.</span></span> |
| <span data-ttu-id="8f854-116">ConfigFile</span><span class="sxs-lookup"><span data-stu-id="8f854-116">ConfigFile</span></span> | <span data-ttu-id="8f854-117">적용할 NuGet 설정 파일입니다.</span><span class="sxs-lookup"><span data-stu-id="8f854-117">The NuGet configuration file to apply.</span></span> <span data-ttu-id="8f854-118">지정하지 않으면 기본적으로 Windows에서는 `%AppData%\NuGet\NuGet.Config`, Mac이나 Linux에서는 `~/.nuget/NuGet/NuGet.Config`가 사용됩니다.</span><span class="sxs-lookup"><span data-stu-id="8f854-118">If not specified, `%AppData%\NuGet\NuGet.Config` (Windows) or `~/.nuget/NuGet/NuGet.Config` (Mac/Linux) is used.</span></span>|
| <span data-ttu-id="8f854-119">DisableBuffering</span><span class="sxs-lookup"><span data-stu-id="8f854-119">DisableBuffering</span></span> | <span data-ttu-id="8f854-120">메모리 사용을 줄이기 위해 HTTP (s) 서버로 푸시할 때 버퍼링을 사용 하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="8f854-120">Disables buffering when pushing to an HTTP(s) server to decrease memory usages.</span></span> <span data-ttu-id="8f854-121">주의:이 옵션을 사용 하는 경우 Windows 통합 인증이 작동 하지 않을 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="8f854-121">Caution: when this option is used, integrated Windows authentication might not work.</span></span> |
| <span data-ttu-id="8f854-122">ForceEnglishOutput</span><span class="sxs-lookup"><span data-stu-id="8f854-122">ForceEnglishOutput</span></span> | <span data-ttu-id="8f854-123">*(3.5 이상)*  현재 언어 설정을 무시하고 영어를 기반으로 nuget.exe를 강제로 실행합니다.</span><span class="sxs-lookup"><span data-stu-id="8f854-123">*(3.5+)* Forces nuget.exe to run using an invariant, English-based culture.</span></span> |
| <span data-ttu-id="8f854-124">Help</span><span class="sxs-lookup"><span data-stu-id="8f854-124">Help</span></span> | <span data-ttu-id="8f854-125">명령어에 대한 도움말을 표시합니다.</span><span class="sxs-lookup"><span data-stu-id="8f854-125">Displays help information for the command.</span></span> |
| <span data-ttu-id="8f854-126">NonInteractive</span><span class="sxs-lookup"><span data-stu-id="8f854-126">NonInteractive</span></span> | <span data-ttu-id="8f854-127">사용자 입력이나 확인에 대한 프롬프트를 표시하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="8f854-127">Suppresses prompts for user input or confirmations.</span></span> |
| <span data-ttu-id="8f854-128">NoSymbols</span><span class="sxs-lookup"><span data-stu-id="8f854-128">NoSymbols</span></span> | <span data-ttu-id="8f854-129">*(3.5 +)* 기호 패키지가 있으면 기호 서버에 푸시되 지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="8f854-129">*(3.5+)* If a symbols package exists, it will not be pushed to a symbol server.</span></span> |
| <span data-ttu-id="8f854-130">Source</span><span class="sxs-lookup"><span data-stu-id="8f854-130">Source</span></span> | <span data-ttu-id="8f854-131">서버 URL을 지정합니다.</span><span class="sxs-lookup"><span data-stu-id="8f854-131">Specifies the server URL.</span></span> <span data-ttu-id="8f854-132">NuGet은 UNC 또는 로컬 폴더 원본을 식별 하 고 HTTP를 사용 하 여 파일을 푸시하는 대신 파일을 복사 합니다.</span><span class="sxs-lookup"><span data-stu-id="8f854-132">NuGet identifies a UNC or local folder source and simply copies the file there instead of pushing it using HTTP.</span></span>  <span data-ttu-id="8f854-133">또한 nuget 3.4.2 부터는이 `NuGet.Config` 파일이 *defaultpushsource* 값을 지정 하지 않는 한 필수 매개 변수입니다 ( [NuGet 동작 구성](../../consume-packages/configuring-nuget-behavior.md)참조).</span><span class="sxs-lookup"><span data-stu-id="8f854-133">Also, starting with NuGet 3.4.2, this is a mandatory parameter unless the `NuGet.Config` file specifies a *DefaultPushSource* value (see [Configuring NuGet behavior](../../consume-packages/configuring-nuget-behavior.md)).</span></span> |
| <span data-ttu-id="8f854-134">SkipDuplicate</span><span class="sxs-lookup"><span data-stu-id="8f854-134">SkipDuplicate</span></span> | <span data-ttu-id="8f854-135">*(5.1 이상)* 패키지와 버전이 이미 있는 경우이를 건너뛰고 밀어넣기 (있는 경우)에서 다음 패키지를 계속 합니다.</span><span class="sxs-lookup"><span data-stu-id="8f854-135">*(5.1+)* If a package and version already exists, skip it and continue with the next package in the push, if any.</span></span> |
| <span data-ttu-id="8f854-136">SymbolSource</span><span class="sxs-lookup"><span data-stu-id="8f854-136">SymbolSource</span></span> | <span data-ttu-id="8f854-137">*(3.5 +)* 기호 서버 URL을 지정 합니다. nuget.smbsrc.net는 nuget.org에 푸시할 때 사용 됩니다.</span><span class="sxs-lookup"><span data-stu-id="8f854-137">*(3.5+)* Specifies the symbol server URL; nuget.smbsrc.net is used when pushing to nuget.org</span></span> |
| <span data-ttu-id="8f854-138">SymbolApiKey</span><span class="sxs-lookup"><span data-stu-id="8f854-138">SymbolApiKey</span></span> | <span data-ttu-id="8f854-139">*(3.5 +)* 에 `-SymbolSource`지정 된 URL에 대 한 API 키를 지정 합니다.</span><span class="sxs-lookup"><span data-stu-id="8f854-139">*(3.5+)* Specifies the API key for the URL specified in `-SymbolSource`.</span></span> |
| <span data-ttu-id="8f854-140">제한 시간</span><span class="sxs-lookup"><span data-stu-id="8f854-140">Timeout</span></span> | <span data-ttu-id="8f854-141">서버에 푸시하는 제한 시간 (초)을 지정 합니다.</span><span class="sxs-lookup"><span data-stu-id="8f854-141">Specifies the timeout, in seconds, for pushing to a server.</span></span> <span data-ttu-id="8f854-142">기본값은 300 초 (5 분)입니다.</span><span class="sxs-lookup"><span data-stu-id="8f854-142">The default is 300 seconds (5 minutes).</span></span> |
| <span data-ttu-id="8f854-143">Verbosity</span><span class="sxs-lookup"><span data-stu-id="8f854-143">Verbosity</span></span> | <span data-ttu-id="8f854-144">출력에 표시되는 세부정보의 양을 지정합니다: *정상적인*, *조용한*, *자세한*합니다.</span><span class="sxs-lookup"><span data-stu-id="8f854-144">Specifies the amount of detail displayed in the output: *normal*, *quiet*, *detailed*.</span></span> |

<span data-ttu-id="8f854-145">또한 [환경 변수](cli-ref-environment-variables.md)에 대한 정보를 참조할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="8f854-145">Also see [Environment variables](cli-ref-environment-variables.md)</span></span>

## <a name="examples"></a><span data-ttu-id="8f854-146">예제</span><span class="sxs-lookup"><span data-stu-id="8f854-146">Examples</span></span>

```cli
nuget push foo.nupkg

nuget push foo.symbols.nupkg

nuget push foo.nupkg -Timeout 360

nuget push *.nupkg

nuget.exe push -source \\mycompany\repo\ mypackage.1.0.0.nupkg

nuget push foo.nupkg 4003d786-cc37-4004-bfdf-c4f3e8ef9b3a -Source https://api.nuget.org/v3/index.json

nuget push foo.nupkg 4003d786-cc37-4004-bfdf-c4f3e8ef9b3a

nuget push foo.nupkg 4003d786-cc37-4004-bfdf-c4f3e8ef9b3a -src https://customsource/

:: In the example below -SkipDuplicate will skip pushing the package if package "Foo" version "5.0.2" already exists on NuGet.org
nuget push Foo.5.0.2.nupkg 4003d786-cc37-4004-bfdf-c4f3e8ef9b3a -src https://api.nuget.org/v3/index.json -SkipDuplicate
```
