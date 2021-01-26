---
title: NuGet CLI 소스 명령
description: nuget.exe sources 명령에 대 한 참조
author: JonDouglas
ms.author: jodou
ms.date: 01/18/2018
ms.topic: reference
ms.openlocfilehash: 0e9cbdd089c5c0f66d25e7588ece504feae63f2f
ms.sourcegitcommit: ee6c3f203648a5561c809db54ebeb1d0f0598b68
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 01/26/2021
ms.locfileid: "98780011"
---
# <a name="sources-command-nuget-cli"></a><span data-ttu-id="e6bfe-103">sources 명령 (NuGet CLI)</span><span class="sxs-lookup"><span data-stu-id="e6bfe-103">sources command (NuGet CLI)</span></span>

<span data-ttu-id="e6bfe-104">**적용 대상:** 패키지 사용, &bullet; **지원 되는 버전 게시:** 모두</span><span class="sxs-lookup"><span data-stu-id="e6bfe-104">**Applies to:** package consumption, publishing &bullet; **Supported versions:** all</span></span>

<span data-ttu-id="e6bfe-105">사용자 범위 구성 파일 또는 지정 된 구성 파일에 있는 원본 목록을 관리 합니다.</span><span class="sxs-lookup"><span data-stu-id="e6bfe-105">Manages the list of sources located in the user scope configuration file or a specified configuration file.</span></span> <span data-ttu-id="e6bfe-106">사용자 범위 구성 파일은 `%appdata%\NuGet\NuGet.Config` (Windows) 및 `~/.nuget/NuGet/NuGet.Config` (Mac/Linux)에 있습니다.</span><span class="sxs-lookup"><span data-stu-id="e6bfe-106">The user scope configuration file is located at `%appdata%\NuGet\NuGet.Config` (Windows) and `~/.nuget/NuGet/NuGet.Config` (Mac/Linux).</span></span>

<span data-ttu-id="e6bfe-107">nuget.org에 대한 원본 URL은 `https://api.nuget.org/v3/index.json`입니다.</span><span class="sxs-lookup"><span data-stu-id="e6bfe-107">Note that the source URL for nuget.org is `https://api.nuget.org/v3/index.json`.</span></span>

## <a name="usage"></a><span data-ttu-id="e6bfe-108">사용량</span><span class="sxs-lookup"><span data-stu-id="e6bfe-108">Usage</span></span>

```cli
nuget sources <operation> -Name <name> -Source <source>
```

<span data-ttu-id="e6bfe-109">여기서 `<operation>` 는 *목록, 추가, 제거, 사용, 사용 안 함* 또는 *업데이트*, `<name>` 는 원본의 이름, `<source>` 는 소스의 URL입니다.</span><span class="sxs-lookup"><span data-stu-id="e6bfe-109">where `<operation>` is one of *List, Add, Remove, Enable, Disable,* or *Update*, `<name>` is the name of the source, and `<source>` is the source's URL.</span></span> <span data-ttu-id="e6bfe-110">한 번에 하나의 원본 에서만 작업할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="e6bfe-110">You can operate on only one source at a time.</span></span>

## <a name="options"></a><span data-ttu-id="e6bfe-111">옵션</span><span class="sxs-lookup"><span data-stu-id="e6bfe-111">Options</span></span>

- **`-ConfigFile`**

  <span data-ttu-id="e6bfe-112">적용할 NuGet 구성 파일입니다.</span><span class="sxs-lookup"><span data-stu-id="e6bfe-112">The NuGet configuration file to apply.</span></span> <span data-ttu-id="e6bfe-113">지정 하지 않으면 `%AppData%\NuGet\NuGet.Config` (Windows) 또는 `~/.nuget/NuGet/NuGet.Config` 또는 `~/.config/NuGet/NuGet.Config` (Mac/Linux)가 사용 됩니다.</span><span class="sxs-lookup"><span data-stu-id="e6bfe-113">If not specified, `%AppData%\NuGet\NuGet.Config` (Windows), or `~/.nuget/NuGet/NuGet.Config` or `~/.config/NuGet/NuGet.Config` (Mac/Linux) is used.</span></span>

- **`-ForceEnglishOutput`**

  <span data-ttu-id="e6bfe-114">*(3.5 +)* 고정 된 영어 기반 문화권을 사용 하 여 nuget.exe을 강제로 실행 합니다.</span><span class="sxs-lookup"><span data-stu-id="e6bfe-114">*(3.5+)* Forces nuget.exe to run using an invariant, English-based culture.</span></span>

- **`-Format`**

  <span data-ttu-id="e6bfe-115">작업에 적용 `list` 되며 `Detailed` (기본값) 또는 일 수 있습니다 `Short` .</span><span class="sxs-lookup"><span data-stu-id="e6bfe-115">Applies to the `list` action and can be `Detailed` (the default) or `Short`.</span></span>

- **`-?|-help`**

  <span data-ttu-id="e6bfe-116">명령에 대 한 도움말 정보를 표시 합니다.</span><span class="sxs-lookup"><span data-stu-id="e6bfe-116">Displays help information for the command.</span></span>

- **`-Name`**

  <span data-ttu-id="e6bfe-117">소스 이름입니다.</span><span class="sxs-lookup"><span data-stu-id="e6bfe-117">Name of the source.</span></span>

- **`-NonInteractive`**

  <span data-ttu-id="e6bfe-118">사용자 입력 또는 확인에 대 한 프롬프트를 표시 하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="e6bfe-118">Suppresses prompts for user input or confirmations.</span></span>

- **`-Password`**

  <span data-ttu-id="e6bfe-119">원본으로 인증 하는 데 사용할 암호를 지정 합니다.</span><span class="sxs-lookup"><span data-stu-id="e6bfe-119">Specifies the password for authenticating with the source.</span></span>

- **`-src|-Source`**

  <span data-ttu-id="e6bfe-120">패키지 원본에 대 한 경로입니다.</span><span class="sxs-lookup"><span data-stu-id="e6bfe-120">Path to the package(s) source.</span></span>

- **`-StorePasswordInClearText`**

  <span data-ttu-id="e6bfe-121">암호화 된 형식을 저장 하는 기본 동작 대신 암호를 암호화 되지 않은 텍스트로 저장 함을 나타냅니다.</span><span class="sxs-lookup"><span data-stu-id="e6bfe-121">Indicates to store the password in unencrypted text instead of the default behavior of storing an encrypted form.</span></span>

- **`-UserName`**

  <span data-ttu-id="e6bfe-122">원본으로 인증 하는 데 사용할 사용자 이름을 지정 합니다.</span><span class="sxs-lookup"><span data-stu-id="e6bfe-122">Specifies the user name for authenticating with the source.</span></span>

- **`-ValidAuthenticationTypes`**

  <span data-ttu-id="e6bfe-123">이 소스에 대한 유효한 인증 형식의 쉼표로 구분된 목록입니다.</span><span class="sxs-lookup"><span data-stu-id="e6bfe-123">Comma-separated list of valid authentication types for this source.</span></span> <span data-ttu-id="e6bfe-124">기본적으로 모든 인증 유형은 유효 합니다.</span><span class="sxs-lookup"><span data-stu-id="e6bfe-124">By default, all authentication types are valid.</span></span> <span data-ttu-id="e6bfe-125">예: `basic,negotiate`.</span><span class="sxs-lookup"><span data-stu-id="e6bfe-125">Example: `basic,negotiate`.</span></span>

- **`-Verbosity [normal|quiet|detailed]`**

  <span data-ttu-id="e6bfe-126">출력에 표시 되는 세부 정보의 양을 지정 합니다. `normal` (기본값), `quiet` 또는 `detailed` 입니다.</span><span class="sxs-lookup"><span data-stu-id="e6bfe-126">Specifies the amount of detail displayed in the output: `normal` (the default), `quiet`, or `detailed`.</span></span>

> [!Note]
> <span data-ttu-id="e6bfe-127">나중에 패키지 원본에 액세스 하는 데 사용 되는 nuget.exe 같은 사용자 컨텍스트에서 원본 암호를 추가 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="e6bfe-127">Make sure to add the sources' password under the same user context as the nuget.exe is later used to access the package source.</span></span> <span data-ttu-id="e6bfe-128">암호는 구성 파일에 암호화 되어 저장 되며 암호화 된 것과 동일한 사용자 컨텍스트에서 암호를 해독할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="e6bfe-128">The password will be stored encrypted in the config file and can only be decrypted in the same user context as it was encrypted.</span></span> <span data-ttu-id="e6bfe-129">예를 들어 빌드 서버를 사용 하 여 NuGet 패키지를 복원 하는 경우 암호는 빌드 서버 태스크가 실행 되는 동일한 Windows 사용자로 암호화 되어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="e6bfe-129">So for example when you use a build server to restore NuGet packages the password must be encrypted with the same Windows user under which  the build server task will run.</span></span>

<span data-ttu-id="e6bfe-130">[환경 변수](cli-ref-environment-variables.md) 참조</span><span class="sxs-lookup"><span data-stu-id="e6bfe-130">Also see [Environment variables](cli-ref-environment-variables.md)</span></span>

## <a name="examples"></a><span data-ttu-id="e6bfe-131">예</span><span class="sxs-lookup"><span data-stu-id="e6bfe-131">Examples</span></span>

```cli
nuget sources Add -Name "MyServer" -Source \\myserver\packages

nuget sources Disable -Name "MyServer"

nuget sources Enable -Name "nuget.org"

nuget sources add -name foo.bar -source C:\NuGet\local -username foo -password bar -StorePasswordInClearText -configfile %AppData%\NuGet\my.config
```
