---
title: "NuGet CLI 명령 원본 | Microsoft Docs"
author: kraigb
ms.author: kraigb
manager: ghogen
ms.date: 01/18/2018
ms.topic: reference
ms.prod: nuget
ms.technology: 
description: "nuget.exe에 대 한 참조의 소스가 명령"
keywords: "nuget 원본 참조, 명령 원본"
ms.reviewer:
- karann-msft
- unniravindranathan
ms.openlocfilehash: 1e8204f5e1bf712f65d8efb14ca2a4bd802e3f90
ms.sourcegitcommit: 7969f6cd94eccfee5b62031bb404422139ccc383
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 02/20/2018
---
# <a name="sources-command-nuget-cli"></a><span data-ttu-id="ab66c-104">소스 명령은 NuGet CLI)</span><span class="sxs-lookup"><span data-stu-id="ab66c-104">sources command (NuGet CLI)</span></span>

<span data-ttu-id="ab66c-105">**적용 대상:** 패키지 소비, 게시 &bullet; **지원 되는 버전:** 모든</span><span class="sxs-lookup"><span data-stu-id="ab66c-105">**Applies to:** package consumption, publishing &bullet; **Supported versions:** all</span></span>

<span data-ttu-id="ab66c-106">사용자 범위 구성 파일 또는 지정된 된 구성 파일에 있는 원본 목록을 관리 합니다.</span><span class="sxs-lookup"><span data-stu-id="ab66c-106">Manages the list of sources located in the user scope configuration file or a specified configuration file.</span></span> <span data-ttu-id="ab66c-107">사용자 범위 구성 파일은 `%APPDATA%\NuGet\NuGet.Config` 및 Windows에서 `~/.nuget/NuGet.Config` Mac/linux에서.</span><span class="sxs-lookup"><span data-stu-id="ab66c-107">The user scope configuration file is located at `%APPDATA%\NuGet\NuGet.Config` in Windows and at `~/.nuget/NuGet.Config` in Mac/Linux.</span></span>


<span data-ttu-id="ab66c-108">nuget.org에 대한 원본 URL은 `https://api.nuget.org/v3/index.json`입니다.</span><span class="sxs-lookup"><span data-stu-id="ab66c-108">Note that the source URL for nuget.org is `https://api.nuget.org/v3/index.json`.</span></span>

## <a name="usage"></a><span data-ttu-id="ab66c-109">사용법</span><span class="sxs-lookup"><span data-stu-id="ab66c-109">Usage</span></span>

```cli
nuget sources <operation> -Name <name> -Source <source>
```

<span data-ttu-id="ab66c-110">여기서 `<operation>` 중 하나입니다 *목록, 추가, 제거, 설정, 해제* 또는 *업데이트*, `<name>` 에 원본의 이름 및 `<source>` 원본의 URL입니다.</span><span class="sxs-lookup"><span data-stu-id="ab66c-110">where `<operation>` is one of *List, Add, Remove, Enable, Disable,* or *Update*, `<name>` is the name of the source, and `<source>` is the source's URL.</span></span>

## <a name="options"></a><span data-ttu-id="ab66c-111">옵션</span><span class="sxs-lookup"><span data-stu-id="ab66c-111">Options</span></span>

| <span data-ttu-id="ab66c-112">옵션</span><span class="sxs-lookup"><span data-stu-id="ab66c-112">Option</span></span> | <span data-ttu-id="ab66c-113">설명</span><span class="sxs-lookup"><span data-stu-id="ab66c-113">Description</span></span> |
| --- | --- |
| <span data-ttu-id="ab66c-114">ConfigFile</span><span class="sxs-lookup"><span data-stu-id="ab66c-114">ConfigFile</span></span> | <span data-ttu-id="ab66c-115">적용할 NuGet 구성 파일입니다.</span><span class="sxs-lookup"><span data-stu-id="ab66c-115">The NuGet configuration file to apply.</span></span> <span data-ttu-id="ab66c-116">지정 하지 않으면 *%AppData%\NuGet\NuGet.Config* 사용 됩니다.</span><span class="sxs-lookup"><span data-stu-id="ab66c-116">If not specified, *%AppData%\NuGet\NuGet.Config* is used.</span></span> |
| <span data-ttu-id="ab66c-117">ForceEnglishOutput</span><span class="sxs-lookup"><span data-stu-id="ab66c-117">ForceEnglishOutput</span></span> | <span data-ttu-id="ab66c-118">*(3.5 +)*  고정, 영어 기반 문화권을 사용 하 여 실행할 nuget.exe를 강제로 수행 합니다.</span><span class="sxs-lookup"><span data-stu-id="ab66c-118">*(3.5+)* Forces nuget.exe to run using an invariant, English-based culture.</span></span> |
| <span data-ttu-id="ab66c-119">형식</span><span class="sxs-lookup"><span data-stu-id="ab66c-119">Format</span></span> | <span data-ttu-id="ab66c-120">에 적용 됩니다는 `list` 작업 수 및 `Detailed` (기본값) 또는 `Short`합니다.</span><span class="sxs-lookup"><span data-stu-id="ab66c-120">Applies to the `list` action and can be `Detailed` (the default) or `Short`.</span></span> |
| <span data-ttu-id="ab66c-121">도움말</span><span class="sxs-lookup"><span data-stu-id="ab66c-121">Help</span></span> | <span data-ttu-id="ab66c-122">도움말의 명령에 대 한 정보를 표시 합니다.</span><span class="sxs-lookup"><span data-stu-id="ab66c-122">Displays help information for the command.</span></span> |
| <span data-ttu-id="ab66c-123">NonInteractive</span><span class="sxs-lookup"><span data-stu-id="ab66c-123">NonInteractive</span></span> | <span data-ttu-id="ab66c-124">사용자 입력 또는 확인에 대 한 프롬프트를 표시 하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="ab66c-124">Suppresses prompts for user input or confirmations.</span></span> |
| <span data-ttu-id="ab66c-125">암호</span><span class="sxs-lookup"><span data-stu-id="ab66c-125">Password</span></span> | <span data-ttu-id="ab66c-126">소스에 인증 하기 위해 암호를 지정 합니다.</span><span class="sxs-lookup"><span data-stu-id="ab66c-126">Specifies the password for authenticating with the source.</span></span> |
| <span data-ttu-id="ab66c-127">StorePasswordInClearText</span><span class="sxs-lookup"><span data-stu-id="ab66c-127">StorePasswordInClearText</span></span> | <span data-ttu-id="ab66c-128">암호화 된 형식에 저장할 경우의 기본 동작 대신 암호화 되지 않은 텍스트에서 암호를 저장 하려면 나타냅니다.</span><span class="sxs-lookup"><span data-stu-id="ab66c-128">Indicates to store the password in unencrypted text instead of the default behavior of storing an encrypted form.</span></span> |
| <span data-ttu-id="ab66c-129">UserName</span><span class="sxs-lookup"><span data-stu-id="ab66c-129">UserName</span></span> | <span data-ttu-id="ab66c-130">소스를 사용 하 여 인증에 대 한 사용자 이름을 지정 합니다.</span><span class="sxs-lookup"><span data-stu-id="ab66c-130">Specifies the user name for authenticating with the source.</span></span> |
| <span data-ttu-id="ab66c-131">자세한 정도</span><span class="sxs-lookup"><span data-stu-id="ab66c-131">Verbosity</span></span> | <span data-ttu-id="ab66c-132">출력에 표시 되는 세부 정보 수준을 지정: *일반*, *quiet*, *자세한*합니다.</span><span class="sxs-lookup"><span data-stu-id="ab66c-132">Specifies the amount of detail displayed in the output: *normal*, *quiet*, *detailed*.</span></span> |

> [!Note]
> <span data-ttu-id="ab66c-133">nuget.exe 패키지 원본에 액세스 하는 데 사용 나중에 동일한 사용자 컨텍스트에서 소스 암호를 추가 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="ab66c-133">Make sure to add the sources' password under the same user context as the nuget.exe is later used to access the package source.</span></span> <span data-ttu-id="ab66c-134">암호 구성 파일에 암호화 된 저장 되 고 암호화 된 대로 동일한 사용자 컨텍스트에서 해독할만 있습니다.</span><span class="sxs-lookup"><span data-stu-id="ab66c-134">The password will be stored encrypted in the config file and can only be decrypted in the same user context as it was encrypted.</span></span> <span data-ttu-id="ab66c-135">예를 사용 하면 빌드 서버 빌드 서버 작업이 실행 될 Windows 사용자가 암호를 암호화 해야 하는 NuGet 패키지를 복원 하려면.</span><span class="sxs-lookup"><span data-stu-id="ab66c-135">So for example when you use a build server to restore NuGet packages the password must be encrypted with the same Windows user under which  the build server task will run.</span></span>

<span data-ttu-id="ab66c-136">또한 참조 [환경 변수](cli-ref-environment-variables.md)</span><span class="sxs-lookup"><span data-stu-id="ab66c-136">Also see [Environment variables](cli-ref-environment-variables.md)</span></span>

## <a name="examples"></a><span data-ttu-id="ab66c-137">예제</span><span class="sxs-lookup"><span data-stu-id="ab66c-137">Examples</span></span>

```cli
nuget sources Add -Name "MyServer" -Source \\myserver\packages

nuget sources Disable -Name "MyServer"

nuget source Enable -Source "nuget.org"

nuget sources add -name foo.bar -source C:\NuGet\local -username foo -password bar -StorePasswordInClearText -configfile %AppData%\NuGet\my.config
```
