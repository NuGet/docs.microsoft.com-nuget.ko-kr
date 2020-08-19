---
title: NuGet CLI push 명령
description: nuget.exe push 명령에 대 한 참조
author: karann-msft
ms.author: karann
ms.date: 01/18/2018
ms.topic: reference
ms.openlocfilehash: d53a2e7f41219e68e59b195d1d5a9d1f62ad7c63
ms.sourcegitcommit: cbc87fe51330cdd3eacaad3e8656eb4258882fc7
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/19/2020
ms.locfileid: "88622848"
---
# <a name="push-command-nuget-cli"></a><span data-ttu-id="776d4-103">push 명령 (NuGet CLI)</span><span class="sxs-lookup"><span data-stu-id="776d4-103">push command (NuGet CLI)</span></span>

<span data-ttu-id="776d4-104">**적용 대상:** 패키지 게시 &bullet; **지원 버전:** 모두, 4.1.0 + nuget.org에 필요 합니다.</span><span class="sxs-lookup"><span data-stu-id="776d4-104">**Applies to:** package publishing &bullet; **Supported versions:** all; 4.1.0+ required for nuget.org</span></span>

> [!Important]
> <span data-ttu-id="776d4-105">Nuget.org에 패키지를 푸시 하려면 필요한 [nuget 프로토콜](../../api/nuget-protocols.md)을 구현 하는 nuget.exe v 4.1.0 +를 사용 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="776d4-105">To push packages to nuget.org you must use nuget.exe v4.1.0+, which implements the required [NuGet protocols](../../api/nuget-protocols.md).</span></span>

<span data-ttu-id="776d4-106">패키지 소스에 패키지를 푸시하고 게시 합니다.</span><span class="sxs-lookup"><span data-stu-id="776d4-106">Pushes a package to a package source and publishes it.</span></span>

<span data-ttu-id="776d4-107">NuGet의 기본 구성은 `%AppData%\NuGet\NuGet.Config` (Windows) 또는 `~/.nuget/NuGet/NuGet.Config` (Mac/Linux)를 로드 한 다음 `Nuget.Config` `.nuget\Nuget.Config` 드라이브의 루트에서 시작 하 여 현재 디렉터리에서 끝나는 또는 파일을 로드 하 여 가져옵니다 ( [일반적인 NuGet 구성](../../consume-packages/configuring-nuget-behavior.md)참조).</span><span class="sxs-lookup"><span data-stu-id="776d4-107">NuGet's default configuration is obtained by loading `%AppData%\NuGet\NuGet.Config` (Windows) or `~/.nuget/NuGet/NuGet.Config` (Mac/Linux), then loading any `Nuget.Config` or `.nuget\Nuget.Config` files starting from root of drive and ending in current directory (see [Common NuGet configurations](../../consume-packages/configuring-nuget-behavior.md))</span></span>

## <a name="usage"></a><span data-ttu-id="776d4-108">사용량</span><span class="sxs-lookup"><span data-stu-id="776d4-108">Usage</span></span>

```cli
nuget push <packagePath> [options]
```

<span data-ttu-id="776d4-109">여기서는 `<packagePath>` 서버에 푸시할 패키지를 식별 합니다.</span><span class="sxs-lookup"><span data-stu-id="776d4-109">where `<packagePath>` identifies the package to push to the server.</span></span>

## <a name="options"></a><span data-ttu-id="776d4-110">옵션</span><span class="sxs-lookup"><span data-stu-id="776d4-110">Options</span></span>

- **`-ApiKey`**

  <span data-ttu-id="776d4-111">대상 리포지토리의 API 키입니다.</span><span class="sxs-lookup"><span data-stu-id="776d4-111">The API key for the target repository.</span></span> <span data-ttu-id="776d4-112">존재 하지 않는 경우 구성 파일에 지정 된 항목을 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="776d4-112">If not present,  the one specified in the config file is used.</span></span>

- **`-ConfigFile`**

  <span data-ttu-id="776d4-113">적용할 NuGet 구성 파일입니다.</span><span class="sxs-lookup"><span data-stu-id="776d4-113">The NuGet configuration file to apply.</span></span> <span data-ttu-id="776d4-114">지정 하지 않으면 `%AppData%\NuGet\NuGet.Config` (Windows) 또는 `~/.nuget/NuGet/NuGet.Config` 또는 `~/.config/NuGet/NuGet.Config` (Mac/Linux)가 사용 됩니다.</span><span class="sxs-lookup"><span data-stu-id="776d4-114">If not specified, `%AppData%\NuGet\NuGet.Config` (Windows), or `~/.nuget/NuGet/NuGet.Config` or `~/.config/NuGet/NuGet.Config` (Mac/Linux) is used.</span></span>

- **`-DisableBuffering`**

  <span data-ttu-id="776d4-115">메모리 사용을 줄이기 위해 HTTP (s) 서버로 푸시할 때 버퍼링을 사용 하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="776d4-115">Disables buffering when pushing to an HTTP(s) server to decrease memory usages.</span></span> <span data-ttu-id="776d4-116">주의:이 옵션을 사용 하는 경우 Windows 통합 인증이 작동 하지 않을 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="776d4-116">Caution: when this option is used, integrated Windows authentication might not work.</span></span>

- **`-ForceEnglishOutput`**

  <span data-ttu-id="776d4-117">*(3.5 +)* 고정 된 영어 기반 문화권을 사용 하 여 nuget.exe을 강제로 실행 합니다.</span><span class="sxs-lookup"><span data-stu-id="776d4-117">*(3.5+)* Forces nuget.exe to run using an invariant, English-based culture.</span></span>

- **`-?|-help`**

  <span data-ttu-id="776d4-118">명령에 대 한 도움말 정보를 표시 합니다.</span><span class="sxs-lookup"><span data-stu-id="776d4-118">Displays help information for the command.</span></span>

- **`-NonInteractive`**

  <span data-ttu-id="776d4-119">사용자 입력 또는 확인에 대 한 프롬프트를 표시 하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="776d4-119">Suppresses prompts for user input or confirmations.</span></span>

- **`-NoServiceEndpoint`**

  <span data-ttu-id="776d4-120">`api/v2/packages`원본 URL에를 추가 하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="776d4-120">Does not append `api/v2/packages` to the source URL.</span></span>

- **`-NoSymbols`**

  <span data-ttu-id="776d4-121">*(3.5 +)* 기호 패키지가 있으면 기호 서버에 푸시되 지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="776d4-121">*(3.5+)* If a symbols package exists, it will not be pushed to a symbol server.</span></span>

- **`-src|-Source`**

  <span data-ttu-id="776d4-122">서버 URL을 지정합니다.</span><span class="sxs-lookup"><span data-stu-id="776d4-122">Specifies the server URL.</span></span> <span data-ttu-id="776d4-123">NuGet은 UNC 또는 로컬 폴더 원본을 식별 하 고 HTTP를 사용 하 여 파일을 푸시하는 대신 파일을 복사 합니다.</span><span class="sxs-lookup"><span data-stu-id="776d4-123">NuGet identifies a UNC or local folder source and simply copies the file there instead of pushing it using HTTP.</span></span>  <span data-ttu-id="776d4-124">또한 NuGet 3.4.2 부터는이 `NuGet.Config` 파일이 *Defaultpushsource* 값을 지정 하지 않는 한 필수 매개 변수입니다 ( [NuGet 동작 구성](../../consume-packages/configuring-nuget-behavior.md)참조).</span><span class="sxs-lookup"><span data-stu-id="776d4-124">Also, starting with NuGet 3.4.2, this is a mandatory parameter unless the `NuGet.Config` file specifies a *DefaultPushSource* value (see [Configuring NuGet behavior](../../consume-packages/configuring-nuget-behavior.md)).</span></span>

- **`-SkipDuplicate`**

  <span data-ttu-id="776d4-125">*(5.1 이상)* 패키지와 버전이 이미 있는 경우이를 건너뛰고 밀어넣기 (있는 경우)에서 다음 패키지를 계속 합니다.</span><span class="sxs-lookup"><span data-stu-id="776d4-125">*(5.1+)* If a package and version already exists, skip it and continue with the next package in the push, if any.</span></span>

- **`-SymbolSource`**

  <span data-ttu-id="776d4-126">*(3.5 +)* 기호 서버 URL을 지정 합니다. nuget.smbsrc.net는 nuget.org에 푸시할 때 사용 됩니다.</span><span class="sxs-lookup"><span data-stu-id="776d4-126">*(3.5+)* Specifies the symbol server URL; nuget.smbsrc.net is used when pushing to nuget.org</span></span>

- **`-SymbolApiKey`**

  <span data-ttu-id="776d4-127">*(3.5 +)* 에 지정 된 URL에 대 한 API 키를 지정 합니다 `-SymbolSource` .</span><span class="sxs-lookup"><span data-stu-id="776d4-127">*(3.5+)* Specifies the API key for the URL specified in `-SymbolSource`.</span></span>

- **`-Timeout`**

  <span data-ttu-id="776d4-128">서버에 푸시하는 제한 시간 (초)을 지정 합니다.</span><span class="sxs-lookup"><span data-stu-id="776d4-128">Specifies the timeout, in seconds, for pushing to a server.</span></span> <span data-ttu-id="776d4-129"> 기본값은 300초(5분)입니다.</span><span class="sxs-lookup"><span data-stu-id="776d4-129">The default is 300 seconds (5 minutes).</span></span>

- **`-Verbosity [normal|quiet|detailed]`**

  <span data-ttu-id="776d4-130">출력에 표시 되는 세부 정보의 양을 지정 합니다. `normal` (기본값), `quiet` 또는 `detailed` 입니다.</span><span class="sxs-lookup"><span data-stu-id="776d4-130">Specifies the amount of detail displayed in the output: `normal` (the default), `quiet`, or `detailed`.</span></span>


<span data-ttu-id="776d4-131">[환경 변수](cli-ref-environment-variables.md) 참조</span><span class="sxs-lookup"><span data-stu-id="776d4-131">Also see [Environment variables](cli-ref-environment-variables.md)</span></span>

## <a name="examples"></a><span data-ttu-id="776d4-132">예</span><span class="sxs-lookup"><span data-stu-id="776d4-132">Examples</span></span>

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
