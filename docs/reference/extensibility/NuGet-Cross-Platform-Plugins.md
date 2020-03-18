---
title: NuGet 플랫폼 간 플러그 인
description: NuGet .exe, dotnet, msbuild.exe 및 Visual Studio 용 NuGet 플랫폼 간 플러그 인
author: nkolev92
ms.author: nikolev
ms.date: 07/01/2018
ms.topic: conceptual
ms.openlocfilehash: 00410214500c7f5256be243dd6fca0907ba9b0c4
ms.sourcegitcommit: ddb52131e84dd54db199ce8331f6da18aa3feea1
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 03/16/2020
ms.locfileid: "79428386"
---
# <a name="nuget-cross-platform-plugins"></a><span data-ttu-id="0dab9-103">NuGet 플랫폼 간 플러그 인</span><span class="sxs-lookup"><span data-stu-id="0dab9-103">NuGet cross platform plugins</span></span>

<span data-ttu-id="0dab9-104">NuGet 4.8 + 플랫폼 간 플러그 인에 대 한 지원이 추가 되었습니다.</span><span class="sxs-lookup"><span data-stu-id="0dab9-104">In NuGet 4.8+ support for cross platform plugins has been added.</span></span>
<span data-ttu-id="0dab9-105">이러한 작업은 엄격한 작업 규칙 집합을 준수 해야 하는 새로운 플러그 인 확장성 모델을 빌드하여에서 수행 되었습니다.</span><span class="sxs-lookup"><span data-stu-id="0dab9-105">This was achieved with by building a new plugin extensibility model, that has to conform to a strict set of rules of operation.</span></span>
<span data-ttu-id="0dab9-106">플러그 인은 자체 포함 된 실행 파일 (.NET Core 환경의 runnables) 이며, NuGet 클라이언트는 별도의 프로세스에서 시작 됩니다.</span><span class="sxs-lookup"><span data-stu-id="0dab9-106">The plugins are self-contained executables (runnables in the .NET Core world), that the NuGet Clients launch in a separate process.</span></span>
<span data-ttu-id="0dab9-107">이는 한 번 쓰기 이며 모든 플러그 인을 실행 합니다.</span><span class="sxs-lookup"><span data-stu-id="0dab9-107">This is a true write once, run everywhere plugin.</span></span> <span data-ttu-id="0dab9-108">모든 NuGet 클라이언트 도구에서 작동 합니다.</span><span class="sxs-lookup"><span data-stu-id="0dab9-108">It will work with all NuGet client tools.</span></span>
<span data-ttu-id="0dab9-109">플러그 인은 .NET Framework (Nuget.exe, Msbuild.exe 및 Visual Studio) 또는 .NET Core (dotnet) 중 하나일 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="0dab9-109">The plugins can be either .NET Framework (NuGet.exe, MSBuild.exe and Visual Studio), or .NET Core (dotnet.exe).</span></span>
<span data-ttu-id="0dab9-110">NuGet 클라이언트와 플러그 인 간에 버전이 지정 된 통신 프로토콜이 정의 되어 있습니다.</span><span class="sxs-lookup"><span data-stu-id="0dab9-110">A versioned communication protocol between the NuGet Client and the plugin is defined.</span></span> <span data-ttu-id="0dab9-111">시작 핸드셰이크 중에 2 개 프로세스가 프로토콜 버전을 협상 합니다.</span><span class="sxs-lookup"><span data-stu-id="0dab9-111">During the startup handshake, the 2 processes negotiate the protocol version.</span></span>

<span data-ttu-id="0dab9-112">모든 NuGet 클라이언트 도구 시나리오를 처리 하기 위해 .NET Framework와 .NET Core 플러그 인이 모두 필요 합니다.</span><span class="sxs-lookup"><span data-stu-id="0dab9-112">In order to cover all NuGet client tools scenarios, one would need both a .NET Framework and a .NET Core plugin.</span></span>
<span data-ttu-id="0dab9-113">아래에서는 플러그 인의 클라이언트/프레임 워크 조합을 설명 합니다.</span><span class="sxs-lookup"><span data-stu-id="0dab9-113">The below describes the client/framework combinations of the plugins.</span></span>

| <span data-ttu-id="0dab9-114">클라이언트 도구</span><span class="sxs-lookup"><span data-stu-id="0dab9-114">Client tool</span></span>  | <span data-ttu-id="0dab9-115">프레임워크</span><span class="sxs-lookup"><span data-stu-id="0dab9-115">Framework</span></span> |
| ------------ | --------- |
| <span data-ttu-id="0dab9-116">Visual Studio</span><span class="sxs-lookup"><span data-stu-id="0dab9-116">Visual Studio</span></span> | <span data-ttu-id="0dab9-117">.NET Framework</span><span class="sxs-lookup"><span data-stu-id="0dab9-117">.NET Framework</span></span> |
| <span data-ttu-id="0dab9-118">dotnet.exe</span><span class="sxs-lookup"><span data-stu-id="0dab9-118">dotnet.exe</span></span> | <span data-ttu-id="0dab9-119">.NET Core</span><span class="sxs-lookup"><span data-stu-id="0dab9-119">.NET Core</span></span> |
| <span data-ttu-id="0dab9-120">Nuget.exe</span><span class="sxs-lookup"><span data-stu-id="0dab9-120">NuGet.exe</span></span> | <span data-ttu-id="0dab9-121">.NET Framework</span><span class="sxs-lookup"><span data-stu-id="0dab9-121">.NET Framework</span></span> |
| <span data-ttu-id="0dab9-122">Msbuild.exe</span><span class="sxs-lookup"><span data-stu-id="0dab9-122">MSBuild.exe</span></span> | <span data-ttu-id="0dab9-123">.NET Framework</span><span class="sxs-lookup"><span data-stu-id="0dab9-123">.NET Framework</span></span> |
| <span data-ttu-id="0dab9-124">Mono의 Nuget.exe</span><span class="sxs-lookup"><span data-stu-id="0dab9-124">NuGet.exe on Mono</span></span> | <span data-ttu-id="0dab9-125">.NET Framework</span><span class="sxs-lookup"><span data-stu-id="0dab9-125">.NET Framework</span></span> |

## <a name="how-does-it-work"></a><span data-ttu-id="0dab9-126">작동 방식</span><span class="sxs-lookup"><span data-stu-id="0dab9-126">How does it work</span></span>

<span data-ttu-id="0dab9-127">개략적인 워크플로는 다음과 같이 설명할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="0dab9-127">The high level workflow can be described as follows:</span></span>

1. <span data-ttu-id="0dab9-128">NuGet은 사용 가능한 플러그 인을 검색 합니다.</span><span class="sxs-lookup"><span data-stu-id="0dab9-128">NuGet discovers available plugins.</span></span>
1. <span data-ttu-id="0dab9-129">해당 하는 경우 NuGet은 우선 순위에 따라 플러그 인을 반복 하 여 하나씩 시작 합니다.</span><span class="sxs-lookup"><span data-stu-id="0dab9-129">When applicable, NuGet will iterate over the plugins in priority order and starts them one by one.</span></span>
1. <span data-ttu-id="0dab9-130">NuGet은 요청을 서비스 하는 데 사용할 수 있는 첫 번째 플러그 인을 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="0dab9-130">NuGet will use the first plugin that can service the request.</span></span>
1. <span data-ttu-id="0dab9-131">더 이상 필요 하지 않으면 플러그 인이 종료 됩니다.</span><span class="sxs-lookup"><span data-stu-id="0dab9-131">The plugins will be shut down when they are no longer needed.</span></span>

## <a name="general-plugin-requirements"></a><span data-ttu-id="0dab9-132">일반 플러그 인 요구 사항</span><span class="sxs-lookup"><span data-stu-id="0dab9-132">General plugin requirements</span></span>

<span data-ttu-id="0dab9-133">현재 프로토콜 버전은 *2.0.0*입니다.</span><span class="sxs-lookup"><span data-stu-id="0dab9-133">The current protocol version is *2.0.0*.</span></span>
<span data-ttu-id="0dab9-134">이 버전에서 요구 사항은 다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="0dab9-134">Under this version, the requirements are as follows:</span></span>

- <span data-ttu-id="0dab9-135">Windows 및 Mono에서 실행 되는 신뢰할 수 있는 올바른 Authenticode 서명 어셈블리가 있어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="0dab9-135">Have a valid, trusted Authenticode signature assemblies that will run on Windows and Mono.</span></span> <span data-ttu-id="0dab9-136">Linux 및 Mac에서 아직 어셈블리를 실행 하기 위한 특별 한 신뢰 요구 사항은 없습니다.</span><span class="sxs-lookup"><span data-stu-id="0dab9-136">There is no special trust requirement for assemblies run on Linux and Mac yet.</span></span> [<span data-ttu-id="0dab9-137">관련 문제</span><span class="sxs-lookup"><span data-stu-id="0dab9-137">Relevant issue</span></span>](https://github.com/NuGet/Home/issues/6702)
- <span data-ttu-id="0dab9-138">NuGet 클라이언트 도구의 현재 보안 컨텍스트에서 상태 비저장 시작을 지원 합니다.</span><span class="sxs-lookup"><span data-stu-id="0dab9-138">Support stateless launching under the current security context of NuGet client tools.</span></span> <span data-ttu-id="0dab9-139">예를 들어 NuGet 클라이언트 도구는 나중에 설명 하는 플러그 인 프로토콜 외부에서 권한 상승이 나 추가 초기화를 수행 하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="0dab9-139">For example, NuGet client tools will not perform elevation or additional initialization outside of the plugin protocol described later.</span></span>
- <span data-ttu-id="0dab9-140">명시적으로 지정 되지 않은 경우 비 대화형 이어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="0dab9-140">Be non interactive, unless explicitly specified.</span></span>
- <span data-ttu-id="0dab9-141">협상 된 플러그 인 프로토콜 버전을 준수 합니다.</span><span class="sxs-lookup"><span data-stu-id="0dab9-141">Adhere to the negotiated plugin protocol version.</span></span>
- <span data-ttu-id="0dab9-142">적절 한 기간 내에 모든 요청에 응답 합니다.</span><span class="sxs-lookup"><span data-stu-id="0dab9-142">Respond to all requests within a reasonable time period.</span></span>
- <span data-ttu-id="0dab9-143">진행 중인 작업에 대 한 취소 요청을 적용 합니다.</span><span class="sxs-lookup"><span data-stu-id="0dab9-143">Honor cancellation requests for any in-progress operation.</span></span>

<span data-ttu-id="0dab9-144">기술 사양은 다음 사양에 자세히 설명 되어 있습니다.</span><span class="sxs-lookup"><span data-stu-id="0dab9-144">The technical specification is described in more detail in the following specs:</span></span>

- [<span data-ttu-id="0dab9-145">NuGet 패키지 다운로드 플러그 인</span><span class="sxs-lookup"><span data-stu-id="0dab9-145">NuGet Package Download Plugin</span></span>](https://github.com/NuGet/Home/wiki/NuGet-Package-Download-Plugin)
- [<span data-ttu-id="0dab9-146">NuGet 교차 cross-plat 인증 플러그 인</span><span class="sxs-lookup"><span data-stu-id="0dab9-146">NuGet cross plat authentication plugin</span></span>](https://github.com/NuGet/Home/wiki/NuGet-cross-plat-authentication-plugin)

## <a name="client---plugin-interaction"></a><span data-ttu-id="0dab9-147">클라이언트-플러그 인 상호 작용</span><span class="sxs-lookup"><span data-stu-id="0dab9-147">Client - Plugin interaction</span></span>

<span data-ttu-id="0dab9-148">NuGet 클라이언트 도구 및 플러그 인은 표준 스트림 (stdin, stdout, stderr)을 통해 JSON과 통신 합니다.</span><span class="sxs-lookup"><span data-stu-id="0dab9-148">NuGet client tools and the plugins communicate with JSON over standard streams (stdin, stdout, stderr).</span></span> <span data-ttu-id="0dab9-149">모든 데이터는 u t f-8로 인코딩해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="0dab9-149">All data must be UTF-8 encoded.</span></span>
<span data-ttu-id="0dab9-150">플러그 인은 "-Plugin" 인수를 사용 하 여 시작 됩니다.</span><span class="sxs-lookup"><span data-stu-id="0dab9-150">The plugins are launched with the argument "-Plugin".</span></span> <span data-ttu-id="0dab9-151">사용자가이 인수 없이 플러그 인 실행 파일을 직접 시작 하는 경우 플러그 인은 프로토콜 핸드셰이크를 기다리는 대신 정보 메시지를 제공할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="0dab9-151">In case a user directly launches a plugin executable without this argument, the plugin can give an informative message instead of waiting for a protocol handshake.</span></span>
<span data-ttu-id="0dab9-152">프로토콜 핸드셰이크 시간 제한은 5 초입니다.</span><span class="sxs-lookup"><span data-stu-id="0dab9-152">The protocol handshake timeout is 5 seconds.</span></span> <span data-ttu-id="0dab9-153">플러그 인은 최대한 크기 만큼의 설치를 완료 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="0dab9-153">The plugin should complete the setup in as short of an amount as possible.</span></span>
<span data-ttu-id="0dab9-154">NuGet 클라이언트 도구는 NuGet 소스에 대 한 서비스 인덱스를 전달 하 여 플러그 인의 지원 되는 작업을 쿼리 합니다.</span><span class="sxs-lookup"><span data-stu-id="0dab9-154">NuGet client tools will query a plugin’s supported operations by passing in the service index for a NuGet source.</span></span> <span data-ttu-id="0dab9-155">플러그 인은 서비스 인덱스를 사용 하 여 지원 되는 서비스 유형이 있는지 확인할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="0dab9-155">A plugin may use the service index to check for the presence of supported service types.</span></span>

<span data-ttu-id="0dab9-156">NuGet 클라이언트 도구와 플러그 인 간의 통신은 양방향입니다.</span><span class="sxs-lookup"><span data-stu-id="0dab9-156">The communication between the NuGet client tools and the plugin is bidirectional.</span></span> <span data-ttu-id="0dab9-157">각 요청에는 시간 제한이 5 초입니다.</span><span class="sxs-lookup"><span data-stu-id="0dab9-157">Each request has a timeout of 5 seconds.</span></span> <span data-ttu-id="0dab9-158">작업이 더 오래 걸릴 것으로 예상 되는 경우 요청이 시간 초과 되지 않도록 각 프로세스에서 진행률 메시지를 전송 해야 합니다. 1 분 동안 활동이 없으면 플러그 인은 유휴 상태로 간주 되어 종료 됩니다.</span><span class="sxs-lookup"><span data-stu-id="0dab9-158">If operations are supposed to take longer the respective process should send out a progress message to prevent the request from timing out. After 1 minute of inactivity a plugin is considered idle and is shut down.</span></span>

## <a name="plugin-installation-and-discovery"></a><span data-ttu-id="0dab9-159">플러그 인 설치 및 검색</span><span class="sxs-lookup"><span data-stu-id="0dab9-159">Plugin installation and discovery</span></span>

<span data-ttu-id="0dab9-160">플러그 인은 규칙 기반 디렉터리 구조를 통해 검색 됩니다.</span><span class="sxs-lookup"><span data-stu-id="0dab9-160">The plugins will be discovered via a convention based directory structure.</span></span>
<span data-ttu-id="0dab9-161">CI/CD 시나리오와 고급 사용자는 환경 변수를 사용 하 여 동작을 재정의할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="0dab9-161">CI/CD scenarios and power users can use environment variables to override the behavior.</span></span> <span data-ttu-id="0dab9-162">환경 변수를 사용 하는 경우 절대 경로만 허용 됩니다.</span><span class="sxs-lookup"><span data-stu-id="0dab9-162">When using environment variables, only absolute paths are allowed.</span></span> <span data-ttu-id="0dab9-163">`NUGET_NETFX_PLUGIN_PATHS` 및 `NUGET_NETCORE_PLUGIN_PATHS`는 5.3 이상 버전의 NuGet 도구 이상 에서만 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="0dab9-163">Note that `NUGET_NETFX_PLUGIN_PATHS` and `NUGET_NETCORE_PLUGIN_PATHS` are only available with 5.3+ version of the NuGet tooling and later.</span></span>

- <span data-ttu-id="0dab9-164">`NUGET_NETFX_PLUGIN_PATHS`-.NET Framework 기반 도구 (Nuget.exe/Msbuild.exe/Visual Studio)에서 사용할 플러그 인을 정의 합니다.</span><span class="sxs-lookup"><span data-stu-id="0dab9-164">`NUGET_NETFX_PLUGIN_PATHS` - defines the plugins that will be used by the .NET Framework based tooling (NuGet.exe/MSBuild.exe/Visual Studio).</span></span> <span data-ttu-id="0dab9-165">`NUGET_PLUGIN_PATHS`보다 우선적으로 적용 됩니다.</span><span class="sxs-lookup"><span data-stu-id="0dab9-165">Takes precedence over `NUGET_PLUGIN_PATHS`.</span></span> <span data-ttu-id="0dab9-166">(NuGet 버전 5.3 이상)</span><span class="sxs-lookup"><span data-stu-id="0dab9-166">(NuGet version 5.3+ only)</span></span>
- <span data-ttu-id="0dab9-167">`NUGET_NETCORE_PLUGIN_PATHS`-.NET Core 기반 도구 (dotnet)에서 사용할 플러그 인을 정의 합니다.</span><span class="sxs-lookup"><span data-stu-id="0dab9-167">`NUGET_NETCORE_PLUGIN_PATHS` - defines the plugins that will be used by the .NET Core based tooling (dotnet.exe).</span></span> <span data-ttu-id="0dab9-168">`NUGET_PLUGIN_PATHS`보다 우선적으로 적용 됩니다.</span><span class="sxs-lookup"><span data-stu-id="0dab9-168">Takes precedence over `NUGET_PLUGIN_PATHS`.</span></span> <span data-ttu-id="0dab9-169">(NuGet 버전 5.3 이상)</span><span class="sxs-lookup"><span data-stu-id="0dab9-169">(NuGet version 5.3+ only)</span></span>
- <span data-ttu-id="0dab9-170">`NUGET_PLUGIN_PATHS`-해당 NuGet 프로세스에 사용할 플러그 인을 정의 합니다. 우선 순위는 유지 됩니다.</span><span class="sxs-lookup"><span data-stu-id="0dab9-170">`NUGET_PLUGIN_PATHS` - defines the plugins that will be used for that NuGet process, priority preserved.</span></span> <span data-ttu-id="0dab9-171">이 환경 변수가 설정 되 면 규칙 기반 검색을 재정의 합니다.</span><span class="sxs-lookup"><span data-stu-id="0dab9-171">If this environment variable is set, it overrides the convention based discovery.</span></span> <span data-ttu-id="0dab9-172">프레임 워크 관련 변수 중 하나가 지정 된 경우 무시 됩니다.</span><span class="sxs-lookup"><span data-stu-id="0dab9-172">Ignored if either of the framework specific variables is specified.</span></span>
-  <span data-ttu-id="0dab9-173">`%UserProfile%/.nuget/plugins`의 NuGet 홈 위치인 사용자 위치입니다.</span><span class="sxs-lookup"><span data-stu-id="0dab9-173">User-location, the NuGet Home location in `%UserProfile%/.nuget/plugins`.</span></span> <span data-ttu-id="0dab9-174">이 위치를 재정의할 수 없습니다.</span><span class="sxs-lookup"><span data-stu-id="0dab9-174">This location cannot be overriden.</span></span> <span data-ttu-id="0dab9-175">.NET Core 및 .NET Framework 플러그 인에는 다른 루트 디렉터리가 사용 됩니다.</span><span class="sxs-lookup"><span data-stu-id="0dab9-175">A different root directory will be used for .NET Core and .NET Framework plugins.</span></span>

| <span data-ttu-id="0dab9-176">프레임워크</span><span class="sxs-lookup"><span data-stu-id="0dab9-176">Framework</span></span> | <span data-ttu-id="0dab9-177">루트 검색 위치</span><span class="sxs-lookup"><span data-stu-id="0dab9-177">Root discovery location</span></span>  |
| ------- | ------------------------ |
| <span data-ttu-id="0dab9-178">.NET Core</span><span class="sxs-lookup"><span data-stu-id="0dab9-178">.NET Core</span></span> |  `%UserProfile%/.nuget/plugins/netcore` |
| <span data-ttu-id="0dab9-179">.NET Framework</span><span class="sxs-lookup"><span data-stu-id="0dab9-179">.NET Framework</span></span> | `%UserProfile%/.nuget/plugins/netfx` |

<span data-ttu-id="0dab9-180">각 플러그 인은 해당 폴더에 설치 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="0dab9-180">Each plugin should be installed in its own folder.</span></span>
<span data-ttu-id="0dab9-181">플러그 인 진입점은 설치 된 폴더의 이름이 고, .NET Core의 경우 .dll 확장명, .NET Framework의 경우 .exe 확장명입니다.</span><span class="sxs-lookup"><span data-stu-id="0dab9-181">The plugin entry point will be the name of the installed folder, with the .dll extensions for .NET Core, and .exe extension for .NET Framework.</span></span>

```
.nuget
    plugins
        netfx
            myPlugin
                myPlugin.exe
                nuget.protocol.dll
                ...
        netcore
            myPlugin
                myPlugin.dll
                nuget.protocol.dll
                ...
```

> [!Note]
> <span data-ttu-id="0dab9-182">현재 플러그 인을 설치할 수 있는 사용자 스토리가 없습니다.</span><span class="sxs-lookup"><span data-stu-id="0dab9-182">There is currently no user story for the installation of the plugins.</span></span> <span data-ttu-id="0dab9-183">필수 파일을 미리 정해진 위치로 이동 하는 것 만큼 간단 합니다.</span><span class="sxs-lookup"><span data-stu-id="0dab9-183">It's as simple as moving the required files into the predetermined location.</span></span>

## <a name="supported-operations"></a><span data-ttu-id="0dab9-184">지원되는 작업</span><span class="sxs-lookup"><span data-stu-id="0dab9-184">Supported operations</span></span>

<span data-ttu-id="0dab9-185">새 플러그 인 프로토콜에서 두 가지 작업이 지원 됩니다.</span><span class="sxs-lookup"><span data-stu-id="0dab9-185">Two operations are supported under the new plugin protocol.</span></span>

| <span data-ttu-id="0dab9-186">작업 이름</span><span class="sxs-lookup"><span data-stu-id="0dab9-186">Operation name</span></span> | <span data-ttu-id="0dab9-187">최소 프로토콜 버전</span><span class="sxs-lookup"><span data-stu-id="0dab9-187">Minimum protocol version</span></span> | <span data-ttu-id="0dab9-188">최소 NuGet 클라이언트 버전</span><span class="sxs-lookup"><span data-stu-id="0dab9-188">Minimum NuGet client version</span></span> |
| -------------- | ----------------------- | --------------------- |
| <span data-ttu-id="0dab9-189">패키지 다운로드</span><span class="sxs-lookup"><span data-stu-id="0dab9-189">Download Package</span></span> | <span data-ttu-id="0dab9-190">1.0.0</span><span class="sxs-lookup"><span data-stu-id="0dab9-190">1.0.0</span></span> | <span data-ttu-id="0dab9-191">4.3.0</span><span class="sxs-lookup"><span data-stu-id="0dab9-191">4.3.0</span></span> |
| [<span data-ttu-id="0dab9-192">인증</span><span class="sxs-lookup"><span data-stu-id="0dab9-192">Authentication</span></span>](NuGet-Cross-Platform-Authentication-Plugin.md) | <span data-ttu-id="0dab9-193">2.0.0</span><span class="sxs-lookup"><span data-stu-id="0dab9-193">2.0.0</span></span> | <span data-ttu-id="0dab9-194">4.8.0</span><span class="sxs-lookup"><span data-stu-id="0dab9-194">4.8.0</span></span> |

## <a name="running-plugins-under-the-correct-runtime"></a><span data-ttu-id="0dab9-195">올바른 런타임에 플러그 인 실행</span><span class="sxs-lookup"><span data-stu-id="0dab9-195">Running plugins under the correct runtime</span></span>

<span data-ttu-id="0dab9-196">Dotnet의 NuGet 시나리오에서 플러그 인은 dotnet의 특정 런타임 아래에서 실행할 수 있어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="0dab9-196">For the NuGet in dotnet.exe scenarios, plugins need to be able to execute under that specific runtime of the dotnet.exe.</span></span>
<span data-ttu-id="0dab9-197">호환 되는 dotnet/plugin 조합이 사용 되는지 확인 하기 위해 플러그 인 공급자와 소비자에 게 있습니다.</span><span class="sxs-lookup"><span data-stu-id="0dab9-197">It's on the plugin provider and the consumer to make sure a compatible dotnet.exe/plugin combination is used.</span></span>
<span data-ttu-id="0dab9-198">예를 들어 사용자 위치 플러그 인에서 잠재적 문제가 발생할 수 있습니다. 예를 들어, 2.0 런타임의 dotnet은 2.1 런타임에 대해 작성 된 플러그 인을 사용 하려고 합니다.</span><span class="sxs-lookup"><span data-stu-id="0dab9-198">A potential issue could arise with the user-location plugins when for example, a dotnet.exe under the 2.0 runtime tries to use a plugin written for the 2.1 runtime.</span></span>

## <a name="capabilities-caching"></a><span data-ttu-id="0dab9-199">기능 캐싱</span><span class="sxs-lookup"><span data-stu-id="0dab9-199">Capabilities caching</span></span>

<span data-ttu-id="0dab9-200">플러그 인의 보안 확인 및 인스턴스화는 비용이 많이 듭니다.</span><span class="sxs-lookup"><span data-stu-id="0dab9-200">The security verification and instantiation of the plugins is costly.</span></span> <span data-ttu-id="0dab9-201">다운로드 작업은 인증 작업 보다 더 자주 수행 되지만 평균 NuGet 사용자에 게는 인증 플러그 인만 있을 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="0dab9-201">The download operation happens way more frequently than the authentication operation, however the average NuGet user is only likely to have an authentication plugin.</span></span>
<span data-ttu-id="0dab9-202">환경을 개선 하기 위해 NuGet은 지정 된 요청에 대 한 작업 클레임을 캐시 합니다.</span><span class="sxs-lookup"><span data-stu-id="0dab9-202">To improve the experience, NuGet will cache the operation claims for the given request.</span></span> <span data-ttu-id="0dab9-203">이 캐시는 플러그 인 키가 플러그 인 경로 이며이 기능 캐시의 만료는 30 일입니다.</span><span class="sxs-lookup"><span data-stu-id="0dab9-203">This cache is per plugin with the plugin key being the plugin path, and the expiration for this capabilities cache is 30 days.</span></span> 

<span data-ttu-id="0dab9-204">캐시는 `%LocalAppData%/NuGet/plugins-cache`에 있으며 `NUGET_PLUGINS_CACHE_PATH`환경 변수를 사용 하 여 재정의 됩니다.</span><span class="sxs-lookup"><span data-stu-id="0dab9-204">The cache is located in `%LocalAppData%/NuGet/plugins-cache` and be overriden with the environment variable `NUGET_PLUGINS_CACHE_PATH`.</span></span> <span data-ttu-id="0dab9-205">이 [캐시](../../consume-packages/managing-the-global-packages-and-cache-folders.md)를 지우려면 `plugins-cache` 옵션을 사용 하 여 지역 명령을 실행할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="0dab9-205">To clear this [cache](../../consume-packages/managing-the-global-packages-and-cache-folders.md), one can run the locals command with the `plugins-cache` option.</span></span>
<span data-ttu-id="0dab9-206">이제 `all` 지역 옵션이 플러그 인 캐시도 삭제 됩니다.</span><span class="sxs-lookup"><span data-stu-id="0dab9-206">The `all` locals option will now also delete the plugins cache.</span></span> 

## <a name="protocol-messages-index"></a><span data-ttu-id="0dab9-207">프로토콜 메시지 인덱스</span><span class="sxs-lookup"><span data-stu-id="0dab9-207">Protocol messages index</span></span>

<span data-ttu-id="0dab9-208">프로토콜 버전 *1.0.0* 메시지:</span><span class="sxs-lookup"><span data-stu-id="0dab9-208">Protocol Version *1.0.0* messages:</span></span>

1.  <span data-ttu-id="0dab9-209">닫습니다</span><span class="sxs-lookup"><span data-stu-id="0dab9-209">Close</span></span>
    * <span data-ttu-id="0dab9-210">요청 방향: NuGet-> 플러그 인</span><span class="sxs-lookup"><span data-stu-id="0dab9-210">Request direction:  NuGet -> plugin</span></span>
    * <span data-ttu-id="0dab9-211">요청에 페이로드가 포함 되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="0dab9-211">The request will contain no payload</span></span>
    * <span data-ttu-id="0dab9-212">응답이 필요 하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="0dab9-212">No response is expected.</span></span>  <span data-ttu-id="0dab9-213">적절 한 응답은 플러그 인 프로세스를 즉시 종료 하는 것입니다.</span><span class="sxs-lookup"><span data-stu-id="0dab9-213">The proper response is for the plugin process to promptly exit.</span></span>

2.  <span data-ttu-id="0dab9-214">패키지의 파일 복사</span><span class="sxs-lookup"><span data-stu-id="0dab9-214">Copy files in package</span></span>
    * <span data-ttu-id="0dab9-215">요청 방향: NuGet-> 플러그 인</span><span class="sxs-lookup"><span data-stu-id="0dab9-215">Request direction:  NuGet -> plugin</span></span>
    * <span data-ttu-id="0dab9-216">요청은 다음을 포함 합니다.</span><span class="sxs-lookup"><span data-stu-id="0dab9-216">The request will contain:</span></span>
        * <span data-ttu-id="0dab9-217">패키지 ID 및 버전</span><span class="sxs-lookup"><span data-stu-id="0dab9-217">the package ID and version</span></span>
        * <span data-ttu-id="0dab9-218">패키지 원본 리포지토리 위치</span><span class="sxs-lookup"><span data-stu-id="0dab9-218">the package source repository location</span></span>
        * <span data-ttu-id="0dab9-219">대상 디렉터리 경로</span><span class="sxs-lookup"><span data-stu-id="0dab9-219">destination directory path</span></span>
        * <span data-ttu-id="0dab9-220">대상 디렉터리 경로에 복사할 패키지의 파일에 대 한 열거 가능</span><span class="sxs-lookup"><span data-stu-id="0dab9-220">an enumerable of files in the package to be copied to the destination directory path</span></span>
    * <span data-ttu-id="0dab9-221">응답에는 다음이 포함 됩니다.</span><span class="sxs-lookup"><span data-stu-id="0dab9-221">A response will contain:</span></span>
        * <span data-ttu-id="0dab9-222">작업의 결과를 나타내는 응답 코드입니다.</span><span class="sxs-lookup"><span data-stu-id="0dab9-222">a response code indicating the outcome of the operation</span></span>
        * <span data-ttu-id="0dab9-223">작업에 성공한 경우 대상 디렉터리에 복사 된 파일의 전체 경로를 열거 한 것입니다.</span><span class="sxs-lookup"><span data-stu-id="0dab9-223">an enumerable of full paths for copied files in the destination directory if the operation was successful</span></span>

3.  <span data-ttu-id="0dab9-224">패키지 파일 복사 (. nupkg)</span><span class="sxs-lookup"><span data-stu-id="0dab9-224">Copy package file (.nupkg)</span></span>
    * <span data-ttu-id="0dab9-225">요청 방향: NuGet-> 플러그 인</span><span class="sxs-lookup"><span data-stu-id="0dab9-225">Request direction:  NuGet -> plugin</span></span>
    * <span data-ttu-id="0dab9-226">요청은 다음을 포함 합니다.</span><span class="sxs-lookup"><span data-stu-id="0dab9-226">The request will contain:</span></span>
        * <span data-ttu-id="0dab9-227">패키지 ID 및 버전</span><span class="sxs-lookup"><span data-stu-id="0dab9-227">the package ID and version</span></span>
        * <span data-ttu-id="0dab9-228">패키지 원본 리포지토리 위치</span><span class="sxs-lookup"><span data-stu-id="0dab9-228">the package source repository location</span></span>
        * <span data-ttu-id="0dab9-229">대상 파일 경로</span><span class="sxs-lookup"><span data-stu-id="0dab9-229">the destination file path</span></span>
    * <span data-ttu-id="0dab9-230">응답에는 다음이 포함 됩니다.</span><span class="sxs-lookup"><span data-stu-id="0dab9-230">A response will contain:</span></span>
        * <span data-ttu-id="0dab9-231">작업의 결과를 나타내는 응답 코드입니다.</span><span class="sxs-lookup"><span data-stu-id="0dab9-231">a response code indicating the outcome of the operation</span></span>

4.  <span data-ttu-id="0dab9-232">자격 증명 가져오기</span><span class="sxs-lookup"><span data-stu-id="0dab9-232">Get credentials</span></span>
    * <span data-ttu-id="0dab9-233">요청 방향: 플러그 인-> NuGet</span><span class="sxs-lookup"><span data-stu-id="0dab9-233">Request direction:  plugin -> NuGet</span></span>
    * <span data-ttu-id="0dab9-234">요청은 다음을 포함 합니다.</span><span class="sxs-lookup"><span data-stu-id="0dab9-234">The request will contain:</span></span>
        * <span data-ttu-id="0dab9-235">패키지 원본 리포지토리 위치</span><span class="sxs-lookup"><span data-stu-id="0dab9-235">the package source repository location</span></span>
        * <span data-ttu-id="0dab9-236">현재 자격 증명을 사용 하 여 패키지 원본 리포지토리에서 가져온 HTTP 상태 코드</span><span class="sxs-lookup"><span data-stu-id="0dab9-236">the HTTP status code obtained from the package source repository using current credentials</span></span>
    * <span data-ttu-id="0dab9-237">응답에는 다음이 포함 됩니다.</span><span class="sxs-lookup"><span data-stu-id="0dab9-237">A response will contain:</span></span>
        * <span data-ttu-id="0dab9-238">작업의 결과를 나타내는 응답 코드입니다.</span><span class="sxs-lookup"><span data-stu-id="0dab9-238">a response code indicating the outcome of the operation</span></span>
        * <span data-ttu-id="0dab9-239">사용자 이름 (사용 가능한 경우)</span><span class="sxs-lookup"><span data-stu-id="0dab9-239">a username, if available</span></span>
        * <span data-ttu-id="0dab9-240">암호 (사용 가능한 경우)</span><span class="sxs-lookup"><span data-stu-id="0dab9-240">a password, if available</span></span>

5.  <span data-ttu-id="0dab9-241">패키지에서 파일 가져오기</span><span class="sxs-lookup"><span data-stu-id="0dab9-241">Get files in package</span></span>
    * <span data-ttu-id="0dab9-242">요청 방향: NuGet-> 플러그 인</span><span class="sxs-lookup"><span data-stu-id="0dab9-242">Request direction:  NuGet -> plugin</span></span>
    * <span data-ttu-id="0dab9-243">요청은 다음을 포함 합니다.</span><span class="sxs-lookup"><span data-stu-id="0dab9-243">The request will contain:</span></span>
        * <span data-ttu-id="0dab9-244">패키지 ID 및 버전</span><span class="sxs-lookup"><span data-stu-id="0dab9-244">the package ID and version</span></span>
        * <span data-ttu-id="0dab9-245">패키지 원본 리포지토리 위치</span><span class="sxs-lookup"><span data-stu-id="0dab9-245">the package source repository location</span></span>
    * <span data-ttu-id="0dab9-246">응답에는 다음이 포함 됩니다.</span><span class="sxs-lookup"><span data-stu-id="0dab9-246">A response will contain:</span></span>
        * <span data-ttu-id="0dab9-247">작업의 결과를 나타내는 응답 코드입니다.</span><span class="sxs-lookup"><span data-stu-id="0dab9-247">a response code indicating the outcome of the operation</span></span>
        * <span data-ttu-id="0dab9-248">작업이 성공한 경우 패키지에서 파일 경로의 열거 가능</span><span class="sxs-lookup"><span data-stu-id="0dab9-248">an enumerable of file paths in the package if the operation was successful</span></span>

6.  <span data-ttu-id="0dab9-249">작업 클레임 가져오기</span><span class="sxs-lookup"><span data-stu-id="0dab9-249">Get operation claims</span></span> 
    * <span data-ttu-id="0dab9-250">요청 방향: NuGet-> 플러그 인</span><span class="sxs-lookup"><span data-stu-id="0dab9-250">Request direction:  NuGet -> plugin</span></span>
    * <span data-ttu-id="0dab9-251">요청은 다음을 포함 합니다.</span><span class="sxs-lookup"><span data-stu-id="0dab9-251">The request will contain:</span></span>
        * <span data-ttu-id="0dab9-252">패키지 원본에 대 한 서비스 인덱스인 json</span><span class="sxs-lookup"><span data-stu-id="0dab9-252">the service index.json for a package source</span></span>
        * <span data-ttu-id="0dab9-253">패키지 원본 리포지토리 위치</span><span class="sxs-lookup"><span data-stu-id="0dab9-253">the package source repository location</span></span>
    * <span data-ttu-id="0dab9-254">응답에는 다음이 포함 됩니다.</span><span class="sxs-lookup"><span data-stu-id="0dab9-254">A response will contain:</span></span>
        * <span data-ttu-id="0dab9-255">작업의 결과를 나타내는 응답 코드입니다.</span><span class="sxs-lookup"><span data-stu-id="0dab9-255">a response code indicating the outcome of the operation</span></span>
        * <span data-ttu-id="0dab9-256">작업이 성공한 경우 지원 되는 작업 (예: 패키지 다운로드)의 열거 가능입니다.</span><span class="sxs-lookup"><span data-stu-id="0dab9-256">an enumerable of supported operations (e.g.:  package download) if the operation was successful.</span></span>  <span data-ttu-id="0dab9-257">플러그 인에서 패키지 원본을 지원 하지 않는 경우 플러그 인은 지원 되는 빈 작업 집합을 반환 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="0dab9-257">If a plugin does not support the package source, the plugin must return an empty set of supported operations.</span></span>

> [!Note]
> <span data-ttu-id="0dab9-258">이 메시지는 버전 *2.0.0*에서 업데이트 되었습니다.</span><span class="sxs-lookup"><span data-stu-id="0dab9-258">This message has been updated in version *2.0.0*.</span></span> <span data-ttu-id="0dab9-259">클라이언트에서 이전 버전과의 호환성을 유지 합니다.</span><span class="sxs-lookup"><span data-stu-id="0dab9-259">It is on the client to preserve backward compatibility.</span></span>

7.  <span data-ttu-id="0dab9-260">패키지 해시 가져오기</span><span class="sxs-lookup"><span data-stu-id="0dab9-260">Get package hash</span></span>
    * <span data-ttu-id="0dab9-261">요청 방향: NuGet-> 플러그 인</span><span class="sxs-lookup"><span data-stu-id="0dab9-261">Request direction:  NuGet -> plugin</span></span>
    * <span data-ttu-id="0dab9-262">요청은 다음을 포함 합니다.</span><span class="sxs-lookup"><span data-stu-id="0dab9-262">The request will contain:</span></span>
        * <span data-ttu-id="0dab9-263">패키지 ID 및 버전</span><span class="sxs-lookup"><span data-stu-id="0dab9-263">the package ID and version</span></span>
        * <span data-ttu-id="0dab9-264">패키지 원본 리포지토리 위치</span><span class="sxs-lookup"><span data-stu-id="0dab9-264">the package source repository location</span></span>
        * <span data-ttu-id="0dab9-265">해시 알고리즘</span><span class="sxs-lookup"><span data-stu-id="0dab9-265">the hash algorithm</span></span>
    * <span data-ttu-id="0dab9-266">응답에는 다음이 포함 됩니다.</span><span class="sxs-lookup"><span data-stu-id="0dab9-266">A response will contain:</span></span>
        * <span data-ttu-id="0dab9-267">작업의 결과를 나타내는 응답 코드입니다.</span><span class="sxs-lookup"><span data-stu-id="0dab9-267">a response code indicating the outcome of the operation</span></span>
        * <span data-ttu-id="0dab9-268">작업이 성공한 경우 요청 된 해시 알고리즘을 사용 하는 패키지 파일 해시</span><span class="sxs-lookup"><span data-stu-id="0dab9-268">a package file hash using the requested hash algorithm if the operation was successful</span></span>

8.  <span data-ttu-id="0dab9-269">패키지 버전 가져오기</span><span class="sxs-lookup"><span data-stu-id="0dab9-269">Get package versions</span></span>
    * <span data-ttu-id="0dab9-270">요청 방향: NuGet-> 플러그 인</span><span class="sxs-lookup"><span data-stu-id="0dab9-270">Request direction:  NuGet -> plugin</span></span>
    * <span data-ttu-id="0dab9-271">요청은 다음을 포함 합니다.</span><span class="sxs-lookup"><span data-stu-id="0dab9-271">The request will contain:</span></span>
        * <span data-ttu-id="0dab9-272">패키지 ID</span><span class="sxs-lookup"><span data-stu-id="0dab9-272">the package ID</span></span>
        * <span data-ttu-id="0dab9-273">패키지 원본 리포지토리 위치</span><span class="sxs-lookup"><span data-stu-id="0dab9-273">the package source repository location</span></span>
    * <span data-ttu-id="0dab9-274">응답에는 다음이 포함 됩니다.</span><span class="sxs-lookup"><span data-stu-id="0dab9-274">A response will contain:</span></span>
        * <span data-ttu-id="0dab9-275">작업의 결과를 나타내는 응답 코드입니다.</span><span class="sxs-lookup"><span data-stu-id="0dab9-275">a response code indicating the outcome of the operation</span></span>
        * <span data-ttu-id="0dab9-276">작업이 성공한 경우 패키지 버전의 열거 가능</span><span class="sxs-lookup"><span data-stu-id="0dab9-276">an enumerable of package versions if the operation was successful</span></span>

9.  <span data-ttu-id="0dab9-277">서비스 인덱스 가져오기</span><span class="sxs-lookup"><span data-stu-id="0dab9-277">Get service index</span></span>
    * <span data-ttu-id="0dab9-278">요청 방향: 플러그 인-> NuGet</span><span class="sxs-lookup"><span data-stu-id="0dab9-278">Request direction:  plugin -> NuGet</span></span>
    * <span data-ttu-id="0dab9-279">요청은 다음을 포함 합니다.</span><span class="sxs-lookup"><span data-stu-id="0dab9-279">The request will contain:</span></span>
        * <span data-ttu-id="0dab9-280">패키지 원본 리포지토리 위치</span><span class="sxs-lookup"><span data-stu-id="0dab9-280">the package source repository location</span></span>
    * <span data-ttu-id="0dab9-281">응답에는 다음이 포함 됩니다.</span><span class="sxs-lookup"><span data-stu-id="0dab9-281">A response will contain:</span></span>
        * <span data-ttu-id="0dab9-282">작업의 결과를 나타내는 응답 코드입니다.</span><span class="sxs-lookup"><span data-stu-id="0dab9-282">a response code indicating the outcome of the operation</span></span>
        * <span data-ttu-id="0dab9-283">작업이 성공한 경우의 서비스 인덱스</span><span class="sxs-lookup"><span data-stu-id="0dab9-283">the service index if the operation was successful</span></span>

10.  <span data-ttu-id="0dab9-284">핸드셰이크</span><span class="sxs-lookup"><span data-stu-id="0dab9-284">Handshake</span></span>
     * <span data-ttu-id="0dab9-285">요청 방향: NuGet <-> 플러그 인</span><span class="sxs-lookup"><span data-stu-id="0dab9-285">Request direction:  NuGet <-> plugin</span></span>
     * <span data-ttu-id="0dab9-286">요청은 다음을 포함 합니다.</span><span class="sxs-lookup"><span data-stu-id="0dab9-286">The request will contain:</span></span>
         * <span data-ttu-id="0dab9-287">현재 플러그 인 프로토콜 버전</span><span class="sxs-lookup"><span data-stu-id="0dab9-287">the current plugin protocol version</span></span>
         * <span data-ttu-id="0dab9-288">지원 되는 최소 플러그 인 프로토콜 버전</span><span class="sxs-lookup"><span data-stu-id="0dab9-288">the minimum supported plugin protocol version</span></span>
     * <span data-ttu-id="0dab9-289">응답에는 다음이 포함 됩니다.</span><span class="sxs-lookup"><span data-stu-id="0dab9-289">A response will contain:</span></span>
         * <span data-ttu-id="0dab9-290">작업의 결과를 나타내는 응답 코드입니다.</span><span class="sxs-lookup"><span data-stu-id="0dab9-290">a response code indicating the outcome of the operation</span></span>
         * <span data-ttu-id="0dab9-291">작업에 성공한 경우 협상 된 프로토콜 버전입니다.</span><span class="sxs-lookup"><span data-stu-id="0dab9-291">the negotiated protocol version if the operation was successful.</span></span>  <span data-ttu-id="0dab9-292">오류가 발생 하면 플러그 인이 종료 됩니다.</span><span class="sxs-lookup"><span data-stu-id="0dab9-292">A failure will result in termination of the plugin.</span></span>

11.  <span data-ttu-id="0dab9-293">초기화</span><span class="sxs-lookup"><span data-stu-id="0dab9-293">Initialize</span></span>
     * <span data-ttu-id="0dab9-294">요청 방향: NuGet-> 플러그 인</span><span class="sxs-lookup"><span data-stu-id="0dab9-294">Request direction:  NuGet -> plugin</span></span>
     * <span data-ttu-id="0dab9-295">요청은 다음을 포함 합니다.</span><span class="sxs-lookup"><span data-stu-id="0dab9-295">The request will contain:</span></span>
         * <span data-ttu-id="0dab9-296">NuGet 클라이언트 도구 버전</span><span class="sxs-lookup"><span data-stu-id="0dab9-296">the NuGet client tool version</span></span>
         * <span data-ttu-id="0dab9-297">NuGet 클라이언트 도구 유효 언어입니다.</span><span class="sxs-lookup"><span data-stu-id="0dab9-297">the NuGet client tool effective language.</span></span>  <span data-ttu-id="0dab9-298">ForceEnglishOutput 설정을 사용 하는 경우이 설정을 고려 합니다.</span><span class="sxs-lookup"><span data-stu-id="0dab9-298">This takes into consideration the ForceEnglishOutput setting, if used.</span></span>
         * <span data-ttu-id="0dab9-299">프로토콜 기본값을 대체 하는 기본 요청 시간 제한입니다.</span><span class="sxs-lookup"><span data-stu-id="0dab9-299">the default request timeout, which supersedes the protocol default.</span></span>
     * <span data-ttu-id="0dab9-300">응답에는 다음이 포함 됩니다.</span><span class="sxs-lookup"><span data-stu-id="0dab9-300">A response will contain:</span></span>
         * <span data-ttu-id="0dab9-301">작업의 결과를 나타내는 응답 코드입니다.</span><span class="sxs-lookup"><span data-stu-id="0dab9-301">a response code indicating the outcome of the operation.</span></span>  <span data-ttu-id="0dab9-302">오류가 발생 하면 플러그 인이 종료 됩니다.</span><span class="sxs-lookup"><span data-stu-id="0dab9-302">A failure will result in termination of the plugin.</span></span>

12.  <span data-ttu-id="0dab9-303">로그</span><span class="sxs-lookup"><span data-stu-id="0dab9-303">Log</span></span>
     * <span data-ttu-id="0dab9-304">요청 방향: 플러그 인-> NuGet</span><span class="sxs-lookup"><span data-stu-id="0dab9-304">Request direction:  plugin -> NuGet</span></span>
     * <span data-ttu-id="0dab9-305">요청은 다음을 포함 합니다.</span><span class="sxs-lookup"><span data-stu-id="0dab9-305">The request will contain:</span></span>
         * <span data-ttu-id="0dab9-306">요청에 대 한 로그 수준입니다.</span><span class="sxs-lookup"><span data-stu-id="0dab9-306">the log level for the request</span></span>
         * <span data-ttu-id="0dab9-307">로깅할 메시지</span><span class="sxs-lookup"><span data-stu-id="0dab9-307">a message to log</span></span>
     * <span data-ttu-id="0dab9-308">응답에는 다음이 포함 됩니다.</span><span class="sxs-lookup"><span data-stu-id="0dab9-308">A response will contain:</span></span>
         * <span data-ttu-id="0dab9-309">작업의 결과를 나타내는 응답 코드입니다.</span><span class="sxs-lookup"><span data-stu-id="0dab9-309">a response code indicating the outcome of the operation.</span></span>

13.  <span data-ttu-id="0dab9-310">NuGet 프로세스 종료 모니터링</span><span class="sxs-lookup"><span data-stu-id="0dab9-310">Monitor NuGet process exit</span></span>
     * <span data-ttu-id="0dab9-311">요청 방향: NuGet-> 플러그 인</span><span class="sxs-lookup"><span data-stu-id="0dab9-311">Request direction:  NuGet -> plugin</span></span>
     * <span data-ttu-id="0dab9-312">요청은 다음을 포함 합니다.</span><span class="sxs-lookup"><span data-stu-id="0dab9-312">The request will contain:</span></span>
         * <span data-ttu-id="0dab9-313">NuGet 프로세스 ID</span><span class="sxs-lookup"><span data-stu-id="0dab9-313">the NuGet process ID</span></span>
     * <span data-ttu-id="0dab9-314">응답에는 다음이 포함 됩니다.</span><span class="sxs-lookup"><span data-stu-id="0dab9-314">A response will contain:</span></span>
         * <span data-ttu-id="0dab9-315">작업의 결과를 나타내는 응답 코드입니다.</span><span class="sxs-lookup"><span data-stu-id="0dab9-315">a response code indicating the outcome of the operation.</span></span>

14.  <span data-ttu-id="0dab9-316">패키지 프리페치</span><span class="sxs-lookup"><span data-stu-id="0dab9-316">Prefetch package</span></span>
     * <span data-ttu-id="0dab9-317">요청 방향: NuGet-> 플러그 인</span><span class="sxs-lookup"><span data-stu-id="0dab9-317">Request direction:  NuGet -> plugin</span></span>
     * <span data-ttu-id="0dab9-318">요청은 다음을 포함 합니다.</span><span class="sxs-lookup"><span data-stu-id="0dab9-318">The request will contain:</span></span>
         * <span data-ttu-id="0dab9-319">패키지 ID 및 버전</span><span class="sxs-lookup"><span data-stu-id="0dab9-319">the package ID and version</span></span>
         * <span data-ttu-id="0dab9-320">패키지 원본 리포지토리 위치</span><span class="sxs-lookup"><span data-stu-id="0dab9-320">the package source repository location</span></span>
     * <span data-ttu-id="0dab9-321">응답에는 다음이 포함 됩니다.</span><span class="sxs-lookup"><span data-stu-id="0dab9-321">A response will contain:</span></span>
         * <span data-ttu-id="0dab9-322">작업의 결과를 나타내는 응답 코드입니다.</span><span class="sxs-lookup"><span data-stu-id="0dab9-322">a response code indicating the outcome of the operation</span></span>

15.  <span data-ttu-id="0dab9-323">자격 증명 설정</span><span class="sxs-lookup"><span data-stu-id="0dab9-323">Set credentials</span></span>
     * <span data-ttu-id="0dab9-324">요청 방향: NuGet-> 플러그 인</span><span class="sxs-lookup"><span data-stu-id="0dab9-324">Request direction:  NuGet -> plugin</span></span>
     * <span data-ttu-id="0dab9-325">요청은 다음을 포함 합니다.</span><span class="sxs-lookup"><span data-stu-id="0dab9-325">The request will contain:</span></span>
         * <span data-ttu-id="0dab9-326">패키지 원본 리포지토리 위치</span><span class="sxs-lookup"><span data-stu-id="0dab9-326">the package source repository location</span></span>
         * <span data-ttu-id="0dab9-327">마지막으로 알려진 패키지 원본 사용자 이름 (사용 가능한 경우)</span><span class="sxs-lookup"><span data-stu-id="0dab9-327">the last known package source username, if available</span></span>
         * <span data-ttu-id="0dab9-328">마지막으로 알려진 패키지 원본 암호 (사용 가능한 경우)</span><span class="sxs-lookup"><span data-stu-id="0dab9-328">the last known package source password, if available</span></span>
         * <span data-ttu-id="0dab9-329">마지막으로 알려진 프록시 사용자 이름 (사용 가능한 경우)</span><span class="sxs-lookup"><span data-stu-id="0dab9-329">the last known proxy username, if available</span></span>
         * <span data-ttu-id="0dab9-330">마지막으로 알려진 프록시 암호 (사용 가능한 경우)</span><span class="sxs-lookup"><span data-stu-id="0dab9-330">the last known proxy password, if available</span></span>
     * <span data-ttu-id="0dab9-331">응답에는 다음이 포함 됩니다.</span><span class="sxs-lookup"><span data-stu-id="0dab9-331">A response will contain:</span></span>
         * <span data-ttu-id="0dab9-332">작업의 결과를 나타내는 응답 코드입니다.</span><span class="sxs-lookup"><span data-stu-id="0dab9-332">a response code indicating the outcome of the operation</span></span>

16.  <span data-ttu-id="0dab9-333">로그 수준 설정</span><span class="sxs-lookup"><span data-stu-id="0dab9-333">Set log level</span></span>
     * <span data-ttu-id="0dab9-334">요청 방향: NuGet-> 플러그 인</span><span class="sxs-lookup"><span data-stu-id="0dab9-334">Request direction:  NuGet -> plugin</span></span>
     * <span data-ttu-id="0dab9-335">요청은 다음을 포함 합니다.</span><span class="sxs-lookup"><span data-stu-id="0dab9-335">The request will contain:</span></span>
         * <span data-ttu-id="0dab9-336">기본 로그 수준</span><span class="sxs-lookup"><span data-stu-id="0dab9-336">the default log level</span></span>
     * <span data-ttu-id="0dab9-337">응답에는 다음이 포함 됩니다.</span><span class="sxs-lookup"><span data-stu-id="0dab9-337">A response will contain:</span></span>
         * <span data-ttu-id="0dab9-338">작업의 결과를 나타내는 응답 코드입니다.</span><span class="sxs-lookup"><span data-stu-id="0dab9-338">a response code indicating the outcome of the operation</span></span>

<span data-ttu-id="0dab9-339">프로토콜 버전 *2.0.0* 메시지</span><span class="sxs-lookup"><span data-stu-id="0dab9-339">Protocol Version *2.0.0* messages</span></span>

17. <span data-ttu-id="0dab9-340">작업 클레임 가져오기</span><span class="sxs-lookup"><span data-stu-id="0dab9-340">Get Operation Claims</span></span>

* <span data-ttu-id="0dab9-341">요청 방향: NuGet-> 플러그 인</span><span class="sxs-lookup"><span data-stu-id="0dab9-341">Request direction:  NuGet -> plugin</span></span>
    * <span data-ttu-id="0dab9-342">요청은 다음을 포함 합니다.</span><span class="sxs-lookup"><span data-stu-id="0dab9-342">The request will contain:</span></span>
        * <span data-ttu-id="0dab9-343">패키지 원본에 대 한 서비스 인덱스인 json</span><span class="sxs-lookup"><span data-stu-id="0dab9-343">the service index.json for a package source</span></span>
        * <span data-ttu-id="0dab9-344">패키지 원본 리포지토리 위치</span><span class="sxs-lookup"><span data-stu-id="0dab9-344">the package source repository location</span></span>
    * <span data-ttu-id="0dab9-345">응답에는 다음이 포함 됩니다.</span><span class="sxs-lookup"><span data-stu-id="0dab9-345">A response will contain:</span></span>
        * <span data-ttu-id="0dab9-346">작업의 결과를 나타내는 응답 코드입니다.</span><span class="sxs-lookup"><span data-stu-id="0dab9-346">a response code indicating the outcome of the operation</span></span>
        * <span data-ttu-id="0dab9-347">작업이 성공 하는 경우 지원 되는 작업의 열거 가능입니다.</span><span class="sxs-lookup"><span data-stu-id="0dab9-347">an enumerable of supported operations if the operation was successful.</span></span>  <span data-ttu-id="0dab9-348">플러그 인에서 패키지 원본을 지원 하지 않는 경우 플러그 인은 지원 되는 빈 작업 집합을 반환 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="0dab9-348">If a plugin does not support the package source, the plugin must return an empty set of supported operations.</span></span>

    <span data-ttu-id="0dab9-349">서비스 인덱스와 패키지 원본이 null 이면 플러그 인이 인증을 사용 하 여 대답할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="0dab9-349">If the service index and package source are null, then the plugin can answer with authentication.</span></span>

18. <span data-ttu-id="0dab9-350">인증 자격 증명 가져오기</span><span class="sxs-lookup"><span data-stu-id="0dab9-350">Get Authentication Credentials</span></span>

* <span data-ttu-id="0dab9-351">요청 방향: NuGet-> 플러그 인</span><span class="sxs-lookup"><span data-stu-id="0dab9-351">Request direction: NuGet -> plugin</span></span>
* <span data-ttu-id="0dab9-352">요청은 다음을 포함 합니다.</span><span class="sxs-lookup"><span data-stu-id="0dab9-352">The request will contain:</span></span>
    * <span data-ttu-id="0dab9-353">Uri</span><span class="sxs-lookup"><span data-stu-id="0dab9-353">Uri</span></span>
    * <span data-ttu-id="0dab9-354">IsRetry</span><span class="sxs-lookup"><span data-stu-id="0dab9-354">isRetry</span></span>
    * <span data-ttu-id="0dab9-355">NonInteractive</span><span class="sxs-lookup"><span data-stu-id="0dab9-355">NonInteractive</span></span>
    * <span data-ttu-id="0dab9-356">CanShowDialog</span><span class="sxs-lookup"><span data-stu-id="0dab9-356">CanShowDialog</span></span>
* <span data-ttu-id="0dab9-357">응답에는 다음이 포함 됩니다.</span><span class="sxs-lookup"><span data-stu-id="0dab9-357">A response will contain</span></span>
    * <span data-ttu-id="0dab9-358">사용자 이름</span><span class="sxs-lookup"><span data-stu-id="0dab9-358">Username</span></span>
    * <span data-ttu-id="0dab9-359">암호</span><span class="sxs-lookup"><span data-stu-id="0dab9-359">Password</span></span>
    * <span data-ttu-id="0dab9-360">메시지</span><span class="sxs-lookup"><span data-stu-id="0dab9-360">Message</span></span>
    * <span data-ttu-id="0dab9-361">인증 유형 목록</span><span class="sxs-lookup"><span data-stu-id="0dab9-361">List of Auth Types</span></span>
    * <span data-ttu-id="0dab9-362">MessageResponseCode</span><span class="sxs-lookup"><span data-stu-id="0dab9-362">MessageResponseCode</span></span>
