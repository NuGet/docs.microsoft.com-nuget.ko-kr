---
title: 플러그 인 플랫폼 간 NuGet
description: NuGet은 NuGet.exe "," dotnet.exe "," msbuild.exe "및" Visual Studio에 대 한 플러그 인 플랫폼 간
author: nkolev92
ms.author: nikolev
manager: rrelyea
ms.date: 07/01/2018
ms.topic: conceptual
ms.openlocfilehash: cf2c4fb484703b034a8569d053f2417fe58e41ff
ms.sourcegitcommit: 8d5121af528e68789485405e24e2100fda2868d6
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/23/2018
ms.locfileid: "42794175"
---
# <a name="nuget-cross-platform-plugins"></a><span data-ttu-id="6fe52-103">플러그 인 플랫폼 간 NuGet</span><span class="sxs-lookup"><span data-stu-id="6fe52-103">NuGet cross platform plugins</span></span>

<span data-ttu-id="6fe52-104">NuGet 4.8 이상에서 크로스 플랫폼 플러그 인에 대 한 지원이 추가 되었습니다.</span><span class="sxs-lookup"><span data-stu-id="6fe52-104">In NuGet 4.8+ support for cross platform plugins has been added.</span></span>
<span data-ttu-id="6fe52-105">이 작업이 엄격한 규칙 작업의 집합을 준수 하는 새 플러그 인 확장성 모델을 작성 하 여 사용 하 여 수행 되었습니다.</span><span class="sxs-lookup"><span data-stu-id="6fe52-105">This was achieved with by building a new plugin extensibility model, that has to conform to a strict set of rules of operation.</span></span>
<span data-ttu-id="6fe52-106">플러그 인은 NuGet 클라이언트는 별도의 프로세스로 시작 하는 자체 포함 된 실행 파일 (.NET Core 환경에서 runnables).</span><span class="sxs-lookup"><span data-stu-id="6fe52-106">The plugins are self-contained executables (runnables in the .NET Core world), that the NuGet Clients launch in a separate process.</span></span>
<span data-ttu-id="6fe52-107">이것이 true 쓰기를 한 번 실행 everywhere 플러그 인입니다.</span><span class="sxs-lookup"><span data-stu-id="6fe52-107">This is a true write once, run everywhere plugin.</span></span> <span data-ttu-id="6fe52-108">모든 NuGet 클라이언트 도구를 사용 하 여 작동 합니다.</span><span class="sxs-lookup"><span data-stu-id="6fe52-108">It will work with all NuGet client tools.</span></span>
<span data-ttu-id="6fe52-109">플러그 인 (NuGet.exe, MSBuild.exe 및 Visual Studio)에서.NET Framework 또는.NET Core (dotnet.exe) 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="6fe52-109">The plugins can be either .NET Framework (NuGet.exe, MSBuild.exe and Visual Studio), or .NET Core (dotnet.exe).</span></span>
<span data-ttu-id="6fe52-110">NuGet 클라이언트와 플러그 인 버전 통신 프로토콜 정의 됩니다.</span><span class="sxs-lookup"><span data-stu-id="6fe52-110">A versioned communication protocol between the NuGet Client and the plugin is defined.</span></span> <span data-ttu-id="6fe52-111">시작 핸드셰이크 중 2 프로세스 프로토콜 버전을 협상합니다.</span><span class="sxs-lookup"><span data-stu-id="6fe52-111">During the startup handshake, the 2 processes negotiate the protocol version.</span></span>

<span data-ttu-id="6fe52-112">모든 NuGet 클라이언트 도구 시나리오를 처리 하기 위해.NET Framework 및.NET Core 플러그 인을 하나이 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="6fe52-112">In order to cover all NuGet client tools scenarios, one would need both a .NET Framework and a .NET Core plugin.</span></span>
<span data-ttu-id="6fe52-113">클라이언트/프레임 워크에 대 한 조합을 플러그 인에 설명 합니다.</span><span class="sxs-lookup"><span data-stu-id="6fe52-113">The below describes the client/framework combinations of the plugins.</span></span>

| <span data-ttu-id="6fe52-114">클라이언트 도구</span><span class="sxs-lookup"><span data-stu-id="6fe52-114">Client tool</span></span>  | <span data-ttu-id="6fe52-115">프레임워크</span><span class="sxs-lookup"><span data-stu-id="6fe52-115">Framework</span></span> |
| ------------ | --------- |
| <span data-ttu-id="6fe52-116">Visual Studio</span><span class="sxs-lookup"><span data-stu-id="6fe52-116">Visual Studio</span></span> | <span data-ttu-id="6fe52-117">.NET Framework</span><span class="sxs-lookup"><span data-stu-id="6fe52-117">.NET Framework</span></span> |
| <span data-ttu-id="6fe52-118">dotnet.exe</span><span class="sxs-lookup"><span data-stu-id="6fe52-118">dotnet.exe</span></span> | <span data-ttu-id="6fe52-119">.NET Core</span><span class="sxs-lookup"><span data-stu-id="6fe52-119">.NET Core</span></span> |
| <span data-ttu-id="6fe52-120">NuGet.exe</span><span class="sxs-lookup"><span data-stu-id="6fe52-120">NuGet.exe</span></span> | <span data-ttu-id="6fe52-121">.NET Framework</span><span class="sxs-lookup"><span data-stu-id="6fe52-121">.NET Framework</span></span> |
| <span data-ttu-id="6fe52-122">MSBuild.exe</span><span class="sxs-lookup"><span data-stu-id="6fe52-122">MSBuild.exe</span></span> | <span data-ttu-id="6fe52-123">.NET Framework</span><span class="sxs-lookup"><span data-stu-id="6fe52-123">.NET Framework</span></span> |
| <span data-ttu-id="6fe52-124">Mono에서 NuGet.exe</span><span class="sxs-lookup"><span data-stu-id="6fe52-124">NuGet.exe on Mono</span></span> | <span data-ttu-id="6fe52-125">.NET Framework</span><span class="sxs-lookup"><span data-stu-id="6fe52-125">.NET Framework</span></span> |

## <a name="how-does-it-work"></a><span data-ttu-id="6fe52-126">어떻게 작동 하나요</span><span class="sxs-lookup"><span data-stu-id="6fe52-126">How does it work</span></span>

<span data-ttu-id="6fe52-127">높은 수준의 워크플로 다음과 같이 설명할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="6fe52-127">The high level workflow can be described as follows:</span></span>

1. <span data-ttu-id="6fe52-128">NuGet은 사용 가능한 플러그 인을 검색합니다.</span><span class="sxs-lookup"><span data-stu-id="6fe52-128">NuGet discovers available plugins.</span></span>
1. <span data-ttu-id="6fe52-129">해당 하는 경우 NuGet 하나씩 시작 및 우선 순위 순서 대로 플러그 인 반복 됩니다.</span><span class="sxs-lookup"><span data-stu-id="6fe52-129">When applicable, NuGet will iterate over the plugins in priority order and starts them one by one.</span></span>
1. <span data-ttu-id="6fe52-130">NuGet은 요청을 처리할 수 있는 첫 번째 플러그 인을 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="6fe52-130">NuGet will use the first plugin that can service the request.</span></span>
1. <span data-ttu-id="6fe52-131">플러그 인 종료 됩니다. 더 이상 필요 없는 경우.</span><span class="sxs-lookup"><span data-stu-id="6fe52-131">The plugins will be shut down when they are no longer needed.</span></span>

## <a name="general-plugin-requirements"></a><span data-ttu-id="6fe52-132">일반 플러그 인 요구 사항</span><span class="sxs-lookup"><span data-stu-id="6fe52-132">General plugin requirements</span></span>

<span data-ttu-id="6fe52-133">현재 프로토콜 버전이 *2.0.0*합니다.</span><span class="sxs-lookup"><span data-stu-id="6fe52-133">The current protocol version is *2.0.0*.</span></span>
<span data-ttu-id="6fe52-134">이 버전에서 요구 사항은 다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="6fe52-134">Under this version, the requirements are as follows:</span></span>

- <span data-ttu-id="6fe52-135">신뢰할 수 있는 유효한 Authenticode 서명을 어셈블리를 Windows 및 Mono에서 실행 되는 경우</span><span class="sxs-lookup"><span data-stu-id="6fe52-135">Have a valid, trusted Authenticode signature assemblies that will run on Windows and Mono.</span></span> <span data-ttu-id="6fe52-136">Linux 및 Mac에서 아직 실행 되는 어셈블리에 대 한 특별 한 신뢰 요건은 없습니다.</span><span class="sxs-lookup"><span data-stu-id="6fe52-136">There is no special trust requirement for assemblies run on Linux and Mac yet.</span></span> [<span data-ttu-id="6fe52-137">관련 문제</span><span class="sxs-lookup"><span data-stu-id="6fe52-137">Relevant issue</span></span>](https://github.com/NuGet/Home/issues/6702)
- <span data-ttu-id="6fe52-138">NuGet 클라이언트 도구의 현재 보안 컨텍스트 내에서 상태 비저장 시작을 지원 합니다.</span><span class="sxs-lookup"><span data-stu-id="6fe52-138">Support stateless launching under the current security context of NuGet client tools.</span></span> <span data-ttu-id="6fe52-139">예를 들어, NuGet 클라이언트 도구는 권한 상승 또는 나중에 설명 된 플러그 인 프로토콜 외부의 추가 초기화 수행 하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="6fe52-139">For example, NuGet client tools will not perform elevation or additional initialization outside of the plugin protocol described later.</span></span>
- <span data-ttu-id="6fe52-140">명시적으로 지정 되지 않은 경우 비 대화형를 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="6fe52-140">Be non interactive, unless explicitly specified.</span></span>
- <span data-ttu-id="6fe52-141">플러그 인 협상 된 프로토콜 버전을 준수 합니다.</span><span class="sxs-lookup"><span data-stu-id="6fe52-141">Adhere to the negotiated plugin protocol version.</span></span>
- <span data-ttu-id="6fe52-142">적절 한 기간 내에서 모든 요청에 응답 합니다.</span><span class="sxs-lookup"><span data-stu-id="6fe52-142">Respond to all requests within a reasonable time period.</span></span>
- <span data-ttu-id="6fe52-143">모든 진행 중인 작업에 대 한 취소 요청을 인식 합니다.</span><span class="sxs-lookup"><span data-stu-id="6fe52-143">Honor cancellation requests for any in-progress operation.</span></span>

<span data-ttu-id="6fe52-144">기술 사양은 다음 사양에 자세히 설명 되어 있습니다.</span><span class="sxs-lookup"><span data-stu-id="6fe52-144">The technical specification is described in more detail in the following specs:</span></span>

- [<span data-ttu-id="6fe52-145">NuGet 패키지 다운로드 플러그 인</span><span class="sxs-lookup"><span data-stu-id="6fe52-145">NuGet Package Download Plugin</span></span>](https://github.com/NuGet/Home/wiki/NuGet-Package-Download-Plugin)
- [<span data-ttu-id="6fe52-146">구획 인증 플러그 인 간 NuGet</span><span class="sxs-lookup"><span data-stu-id="6fe52-146">NuGet cross plat authentication plugin</span></span>](https://github.com/NuGet/Home/wiki/NuGet-cross-plat-authentication-plugin)

## <a name="client---plugin-interaction"></a><span data-ttu-id="6fe52-147">클라이언트-플러그 인 상호 작용</span><span class="sxs-lookup"><span data-stu-id="6fe52-147">Client - Plugin interaction</span></span>

<span data-ttu-id="6fe52-148">NuGet 클라이언트 도구와 플러그 인 표준 스트림 (stdin, stdout, stderr)을 통해 JSON을 사용 하 여 통신합니다.</span><span class="sxs-lookup"><span data-stu-id="6fe52-148">NuGet client tools and the plugins communicate with JSON over standard streams (stdin, stdout, stderr).</span></span> <span data-ttu-id="6fe52-149">모든 데이터는 u t F-8로 인코딩된 이어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="6fe52-149">All data must be UTF-8 encoded.</span></span>
<span data-ttu-id="6fe52-150">플러그 인 인수를 사용 하 여 시작 "-플러그 인"입니다.</span><span class="sxs-lookup"><span data-stu-id="6fe52-150">The plugins are launched with the argument "-Plugin".</span></span> <span data-ttu-id="6fe52-151">사용자 플러그 인이이 인수 없이 실행 파일을 직접 시작 하는 경우 플러그 인 프로토콜 핸드셰이크를 기다리는 대신 정보 메시지를 제공할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="6fe52-151">In case a user directly launches a plugin executable without this argument, the plugin can give an informative message instead of waiting for a protocol handshake.</span></span>
<span data-ttu-id="6fe52-152">프로토콜 핸드셰이크 제한 시간은 5 초입니다.</span><span class="sxs-lookup"><span data-stu-id="6fe52-152">The protocol handshake timeout is 5 seconds.</span></span> <span data-ttu-id="6fe52-153">플러그 인을 최대한 용량 부족으로 설치를 완료 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="6fe52-153">The plugin should complete the setup in as short of an amount as possible.</span></span>
<span data-ttu-id="6fe52-154">NuGet 클라이언트 도구는 NuGet 소스에 대 한 서비스 인덱스를 전달 하 여 플러그 인의 지원 되는 작업을 조회 합니다.</span><span class="sxs-lookup"><span data-stu-id="6fe52-154">NuGet client tools will query a plugin’s supported operations by passing in the service index for a NuGet source.</span></span> <span data-ttu-id="6fe52-155">플러그 인에 지원 되는 서비스 형식의 현재 상태를 확인할 서비스 인덱스를 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="6fe52-155">A plugin may use the service index to check for the presence of supported service types.</span></span>

<span data-ttu-id="6fe52-156">NuGet 클라이언트 도구 및 플러그 인 간의 통신은 양방향입니다.</span><span class="sxs-lookup"><span data-stu-id="6fe52-156">The communication between the NuGet client tools and the plugin is bidirectional.</span></span> <span data-ttu-id="6fe52-157">각 요청에 5 초의 제한 시간입니다.</span><span class="sxs-lookup"><span data-stu-id="6fe52-157">Each request has a timeout of 5 seconds.</span></span> <span data-ttu-id="6fe52-158">작업은 시간이 오래 걸릴 간주 하는 경우 해당 프로세스는 요청 시간 초과 되지 않도록 하려면 진행률 메시지 전송 해야 합니다. 전까지 비활성 시간 1 분 후 플러그 인을 유휴 간주 되 고 종료 됩니다.</span><span class="sxs-lookup"><span data-stu-id="6fe52-158">If operations are supposed to take longer the respective process should send out a progress message to prevent the request from timing out. After 1 minute of inactivity a plugin is considered idle and is shut down.</span></span>

## <a name="plugin-installation-and-discovery"></a><span data-ttu-id="6fe52-159">플러그 인 설치 및 검색</span><span class="sxs-lookup"><span data-stu-id="6fe52-159">Plugin installation and discovery</span></span>

<span data-ttu-id="6fe52-160">플러그 인 기반 규칙 디렉터리 구조를 통해 검색 됩니다.</span><span class="sxs-lookup"><span data-stu-id="6fe52-160">The plugins will be discovered via a convention based directory structure.</span></span>
<span data-ttu-id="6fe52-161">CI/CD 시나리오 및 고급 사용자 동작을 재정의 하는 환경 변수를 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="6fe52-161">CI/CD scenarios and power users can use an environment variable to override the behavior.</span></span>

- <span data-ttu-id="6fe52-162">`NUGET_PLUGIN_PATHS` -해당 NuGet 프로세스를 예약 하는 우선 순위에 사용할 플러그 인을 정의 합니다.</span><span class="sxs-lookup"><span data-stu-id="6fe52-162">`NUGET_PLUGIN_PATHS` - defines the plugins that will be used for that NuGet process, priority reserved.</span></span> <span data-ttu-id="6fe52-163">이 환경 변수를 설정 하는 경우 규칙 기반 검색을 재정의 합니다.</span><span class="sxs-lookup"><span data-stu-id="6fe52-163">If this environment variable is set, it overrides the convention based discovery.</span></span>
-  <span data-ttu-id="6fe52-164">사용자 위치, NuGet 홈 위치 `%UserProfile%/.nuget/plugins`합니다.</span><span class="sxs-lookup"><span data-stu-id="6fe52-164">User-location, the NuGet Home location in `%UserProfile%/.nuget/plugins`.</span></span> <span data-ttu-id="6fe52-165">이 위치는 재정의할 수 없습니다.</span><span class="sxs-lookup"><span data-stu-id="6fe52-165">This location cannot be overriden.</span></span> <span data-ttu-id="6fe52-166">.NET Core와.NET Framework 플러그 인에 대 한 다른 루트 디렉터리가 사용 됩니다.</span><span class="sxs-lookup"><span data-stu-id="6fe52-166">A different root directory will be used for .NET Core and .NET Framework plugins.</span></span>

| <span data-ttu-id="6fe52-167">프레임워크</span><span class="sxs-lookup"><span data-stu-id="6fe52-167">Framework</span></span> | <span data-ttu-id="6fe52-168">루트 검색 위치</span><span class="sxs-lookup"><span data-stu-id="6fe52-168">Root discovery location</span></span>  |
| ------- | ------------------------ |
| <span data-ttu-id="6fe52-169">.NET Core</span><span class="sxs-lookup"><span data-stu-id="6fe52-169">.NET Core</span></span> |  `%UserProfile%/.nuget/plugins/netcore` |
| <span data-ttu-id="6fe52-170">.NET Framework</span><span class="sxs-lookup"><span data-stu-id="6fe52-170">.NET Framework</span></span> | `%UserProfile%/.nuget/plugins/netfx` |

<span data-ttu-id="6fe52-171">각 플러그 인 폴더에 설치 되어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="6fe52-171">Each plugin should be installed in its own folder.</span></span>
<span data-ttu-id="6fe52-172">플러그 인 진입점에는.NET Core 용.dll 확장명 및.NET Framework에 대 한.exe 확장명을 사용 하 여 설치 된 폴더의 이름이 됩니다.</span><span class="sxs-lookup"><span data-stu-id="6fe52-172">The plugin entry point will be the name of the installed folder, with the .dll extensions for .NET Core, and .exe extension for .NET Framework.</span></span>

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
> <span data-ttu-id="6fe52-173">현재 플러그 인 설치에 없는 사용자 스토리가입니다.</span><span class="sxs-lookup"><span data-stu-id="6fe52-173">There is currently no user story for the installation of the plugins.</span></span> <span data-ttu-id="6fe52-174">미리 결정 된 위치에 필요한 파일을 이동 하는 것으로 간단 합니다.</span><span class="sxs-lookup"><span data-stu-id="6fe52-174">It's as simple as moving the required files into the predetermined location.</span></span>

## <a name="supported-operations"></a><span data-ttu-id="6fe52-175">지원 되는 작업</span><span class="sxs-lookup"><span data-stu-id="6fe52-175">Supported operations</span></span>

<span data-ttu-id="6fe52-176">두 작업은 새 플러그 인 프로토콜에서 지원 됩니다.</span><span class="sxs-lookup"><span data-stu-id="6fe52-176">Two operations are supported under the new plugin protocol.</span></span>

| <span data-ttu-id="6fe52-177">작업 이름</span><span class="sxs-lookup"><span data-stu-id="6fe52-177">Operation name</span></span> | <span data-ttu-id="6fe52-178">최소 프로토콜 버전</span><span class="sxs-lookup"><span data-stu-id="6fe52-178">Minimum protocol version</span></span> | <span data-ttu-id="6fe52-179">최소 NuGet 클라이언트 버전</span><span class="sxs-lookup"><span data-stu-id="6fe52-179">Minimum NuGet client version</span></span> |
| -------------- | ----------------------- | --------------------- |
| <span data-ttu-id="6fe52-180">패키지를 다운로드 합니다.</span><span class="sxs-lookup"><span data-stu-id="6fe52-180">Download Package</span></span> | <span data-ttu-id="6fe52-181">1.0.0</span><span class="sxs-lookup"><span data-stu-id="6fe52-181">1.0.0</span></span> | <span data-ttu-id="6fe52-182">4.3.0</span><span class="sxs-lookup"><span data-stu-id="6fe52-182">4.3.0</span></span> |
| [<span data-ttu-id="6fe52-183">인증</span><span class="sxs-lookup"><span data-stu-id="6fe52-183">Authentication</span></span>](NuGet-Cross-Platform-Authentication-Plugin.md) | <span data-ttu-id="6fe52-184">2.0.0</span><span class="sxs-lookup"><span data-stu-id="6fe52-184">2.0.0</span></span> | <span data-ttu-id="6fe52-185">4.8.0</span><span class="sxs-lookup"><span data-stu-id="6fe52-185">4.8.0</span></span> |

## <a name="running-plugins-under-the-correct-runtime"></a><span data-ttu-id="6fe52-186">올바른 런타임에서 플러그 인 실행</span><span class="sxs-lookup"><span data-stu-id="6fe52-186">Running plugins under the correct runtime</span></span>

<span data-ttu-id="6fe52-187">Dotnet.exe 시나리오의 NuGet, 플러그 인을 dotnet.exe의 해당 특정 런타임 실행 하려면 필요 합니다.</span><span class="sxs-lookup"><span data-stu-id="6fe52-187">For the NuGet in dotnet.exe scenarios, plugins need to be able to execute under that specific runtime of the dotnet.exe.</span></span>
<span data-ttu-id="6fe52-188">호환 dotnet.exe/plugin 결합 하 여 사용할 되도록 플러그 인 공급자와 소비자입니다.</span><span class="sxs-lookup"><span data-stu-id="6fe52-188">It's on the plugin provider and the consumer to make sure a compatible dotnet.exe/plugin combination is used.</span></span>
<span data-ttu-id="6fe52-189">예를 들어 하는 경우 사용자 위치 플러그 인을 사용 하 여 잠재적인 문제를 발생할 수 있습니다, 그리고 2.0 런타임에서 dotnet.exe 2.1 런타임용으로 작성 하는 플러그 인을 사용 하려고 합니다.</span><span class="sxs-lookup"><span data-stu-id="6fe52-189">A potential issue could arise with the user-location plugins when for example, a dotnet.exe under the 2.0 runtime tries to use a plugin written for the 2.1 runtime.</span></span>

## <a name="capabilities-caching"></a><span data-ttu-id="6fe52-190">캐싱 기능</span><span class="sxs-lookup"><span data-stu-id="6fe52-190">Capabilities caching</span></span>

<span data-ttu-id="6fe52-191">보안 확인 및 플러그 인의 인스턴스화 비용이 많이 듭니다.</span><span class="sxs-lookup"><span data-stu-id="6fe52-191">The security verification and instantiation of the plugins is costly.</span></span> <span data-ttu-id="6fe52-192">다운로드 작업 평균 NuGet 사용자가 인증 하는 플러그 인을 갖고 있지만 인증 작업을 보다 훨씬 더 자주 발생 합니다.</span><span class="sxs-lookup"><span data-stu-id="6fe52-192">The download operation happens way more frequently than the authentication operation, however the average NuGet user is only likely to have an authentication plugin.</span></span>
<span data-ttu-id="6fe52-193">환경을 개선 하기 위해 NuGet에는 지정된 된 요청에 대 한 작업 클레임을 캐시 합니다.</span><span class="sxs-lookup"><span data-stu-id="6fe52-193">To improve the experience, NuGet will cache the operation claims for the given request.</span></span> <span data-ttu-id="6fe52-194">이 캐시 플러그 인당 플러그 인 경로 플러그 인 키를 사용 하 여 이며이 기능 캐시의 만료 30 일입니다.</span><span class="sxs-lookup"><span data-stu-id="6fe52-194">This cache is per plugin with the plugin key being the plugin path, and the expiration for this capabilities cache is 30 days.</span></span> 

<span data-ttu-id="6fe52-195">캐시에 위치한 `%LocalAppData%/NuGet/plugins-cache` 환경 변수를 사용 하 여 재정의할 수 및 `NUGET_PLUGINS_CACHE_PATH`합니다.</span><span class="sxs-lookup"><span data-stu-id="6fe52-195">The cache is located in `%LocalAppData%/NuGet/plugins-cache` and be overriden with the environment variable `NUGET_PLUGINS_CACHE_PATH`.</span></span> <span data-ttu-id="6fe52-196">이 지우려면 [캐시](../../consume-packages/managing-the-global-packages-and-cache-folders.md), 지역 변수를 실행할 수 있는 명령과 `plugins-cache` 옵션입니다.</span><span class="sxs-lookup"><span data-stu-id="6fe52-196">To clear this [cache](../../consume-packages/managing-the-global-packages-and-cache-folders.md), one can run the locals command with the `plugins-cache` option.</span></span>
<span data-ttu-id="6fe52-197">`all` 이제 지역 옵션 플러그 인 캐시도 삭제 됩니다.</span><span class="sxs-lookup"><span data-stu-id="6fe52-197">The `all` locals option will now also delete the plugins cache.</span></span> 

## <a name="protocol-messages-index"></a><span data-ttu-id="6fe52-198">프로토콜 메시지 인덱스</span><span class="sxs-lookup"><span data-stu-id="6fe52-198">Protocol messages index</span></span>

<span data-ttu-id="6fe52-199">프로토콜 버전 *1.0.0* 메시지:</span><span class="sxs-lookup"><span data-stu-id="6fe52-199">Protocol Version *1.0.0* messages:</span></span>

1.  <span data-ttu-id="6fe52-200">닫기</span><span class="sxs-lookup"><span data-stu-id="6fe52-200">Close</span></span>
    * <span data-ttu-id="6fe52-201">방향 요청: NuGet-플러그 인 ></span><span class="sxs-lookup"><span data-stu-id="6fe52-201">Request direction:  NuGet -> plugin</span></span>
    * <span data-ttu-id="6fe52-202">요청 페이로드 없이 포함 됩니다.</span><span class="sxs-lookup"><span data-stu-id="6fe52-202">The request will contain no payload</span></span>
    * <span data-ttu-id="6fe52-203">응답이 필요 합니다.</span><span class="sxs-lookup"><span data-stu-id="6fe52-203">No response is expected.</span></span>  <span data-ttu-id="6fe52-204">즉시 종료 하는 플러그 인 프로세스에 대 한 적절 한 응답이입니다.</span><span class="sxs-lookup"><span data-stu-id="6fe52-204">The proper response is for the plugin process to promptly exit.</span></span>

2.  <span data-ttu-id="6fe52-205">패키지의 파일 복사</span><span class="sxs-lookup"><span data-stu-id="6fe52-205">Copy files in package</span></span>
    * <span data-ttu-id="6fe52-206">방향 요청: NuGet-플러그 인 ></span><span class="sxs-lookup"><span data-stu-id="6fe52-206">Request direction:  NuGet -> plugin</span></span>
    * <span data-ttu-id="6fe52-207">요청이 포함 됩니다.</span><span class="sxs-lookup"><span data-stu-id="6fe52-207">The request will contain:</span></span>
        * <span data-ttu-id="6fe52-208">패키지 ID 및 버전</span><span class="sxs-lookup"><span data-stu-id="6fe52-208">the package ID and version</span></span>
        * <span data-ttu-id="6fe52-209">패키지 원본 리포지토리 위치</span><span class="sxs-lookup"><span data-stu-id="6fe52-209">the package source repository location</span></span>
        * <span data-ttu-id="6fe52-210">대상 디렉터리 경로</span><span class="sxs-lookup"><span data-stu-id="6fe52-210">destination directory path</span></span>
        * <span data-ttu-id="6fe52-211">대상 디렉터리 경로 복사할 대상 패키지의 파일 열거</span><span class="sxs-lookup"><span data-stu-id="6fe52-211">an enumerable of files in the package to be copied to the destination directory path</span></span>
    * <span data-ttu-id="6fe52-212">응답에 포함 됩니다.</span><span class="sxs-lookup"><span data-stu-id="6fe52-212">A response will contain:</span></span>
        * <span data-ttu-id="6fe52-213">작업의 결과 나타내는 응답 코드</span><span class="sxs-lookup"><span data-stu-id="6fe52-213">a response code indicating the outcome of the operation</span></span>
        * <span data-ttu-id="6fe52-214">열거 가능한 작업에 성공 하는 경우 대상 디렉터리에 복사한 파일의 전체 경로</span><span class="sxs-lookup"><span data-stu-id="6fe52-214">an enumerable of full paths for copied files in the destination directory if the operation was successful</span></span>

3.  <span data-ttu-id="6fe52-215">패키지 파일 (.nupkg)를 복사 합니다.</span><span class="sxs-lookup"><span data-stu-id="6fe52-215">Copy package file (.nupkg)</span></span>
    * <span data-ttu-id="6fe52-216">방향 요청: NuGet-플러그 인 ></span><span class="sxs-lookup"><span data-stu-id="6fe52-216">Request direction:  NuGet -> plugin</span></span>
    * <span data-ttu-id="6fe52-217">요청이 포함 됩니다.</span><span class="sxs-lookup"><span data-stu-id="6fe52-217">The request will contain:</span></span>
        * <span data-ttu-id="6fe52-218">패키지 ID 및 버전</span><span class="sxs-lookup"><span data-stu-id="6fe52-218">the package ID and version</span></span>
        * <span data-ttu-id="6fe52-219">패키지 원본 리포지토리 위치</span><span class="sxs-lookup"><span data-stu-id="6fe52-219">the package source repository location</span></span>
        * <span data-ttu-id="6fe52-220">대상 파일 경로</span><span class="sxs-lookup"><span data-stu-id="6fe52-220">the destination file path</span></span>
    * <span data-ttu-id="6fe52-221">응답에 포함 됩니다.</span><span class="sxs-lookup"><span data-stu-id="6fe52-221">A response will contain:</span></span>
        * <span data-ttu-id="6fe52-222">작업의 결과 나타내는 응답 코드</span><span class="sxs-lookup"><span data-stu-id="6fe52-222">a response code indicating the outcome of the operation</span></span>

4.  <span data-ttu-id="6fe52-223">자격 증명 가져오기</span><span class="sxs-lookup"><span data-stu-id="6fe52-223">Get credentials</span></span>
    * <span data-ttu-id="6fe52-224">방향 요청: 플러그 인에는 NuGet-></span><span class="sxs-lookup"><span data-stu-id="6fe52-224">Request direction:  plugin -> NuGet</span></span>
    * <span data-ttu-id="6fe52-225">요청이 포함 됩니다.</span><span class="sxs-lookup"><span data-stu-id="6fe52-225">The request will contain:</span></span>
        * <span data-ttu-id="6fe52-226">패키지 원본 리포지토리 위치</span><span class="sxs-lookup"><span data-stu-id="6fe52-226">the package source repository location</span></span>
        * <span data-ttu-id="6fe52-227">현재 자격 증명을 사용 하 여 패키지 원본 저장소에서 가져온 HTTP 상태 코드</span><span class="sxs-lookup"><span data-stu-id="6fe52-227">the HTTP status code obtained from the package source repository using current credentials</span></span>
    * <span data-ttu-id="6fe52-228">응답에 포함 됩니다.</span><span class="sxs-lookup"><span data-stu-id="6fe52-228">A response will contain:</span></span>
        * <span data-ttu-id="6fe52-229">작업의 결과 나타내는 응답 코드</span><span class="sxs-lookup"><span data-stu-id="6fe52-229">a response code indicating the outcome of the operation</span></span>
        * <span data-ttu-id="6fe52-230">사용 가능한 경우 사용자 이름</span><span class="sxs-lookup"><span data-stu-id="6fe52-230">a username, if available</span></span>
        * <span data-ttu-id="6fe52-231">암호를 사용할 수 있는 경우</span><span class="sxs-lookup"><span data-stu-id="6fe52-231">a password, if available</span></span>

5.  <span data-ttu-id="6fe52-232">패키지의 파일</span><span class="sxs-lookup"><span data-stu-id="6fe52-232">Get files in package</span></span>
    * <span data-ttu-id="6fe52-233">방향 요청: NuGet-플러그 인 ></span><span class="sxs-lookup"><span data-stu-id="6fe52-233">Request direction:  NuGet -> plugin</span></span>
    * <span data-ttu-id="6fe52-234">요청이 포함 됩니다.</span><span class="sxs-lookup"><span data-stu-id="6fe52-234">The request will contain:</span></span>
        * <span data-ttu-id="6fe52-235">패키지 ID 및 버전</span><span class="sxs-lookup"><span data-stu-id="6fe52-235">the package ID and version</span></span>
        * <span data-ttu-id="6fe52-236">패키지 원본 리포지토리 위치</span><span class="sxs-lookup"><span data-stu-id="6fe52-236">the package source repository location</span></span>
    * <span data-ttu-id="6fe52-237">응답에 포함 됩니다.</span><span class="sxs-lookup"><span data-stu-id="6fe52-237">A response will contain:</span></span>
        * <span data-ttu-id="6fe52-238">작업의 결과 나타내는 응답 코드</span><span class="sxs-lookup"><span data-stu-id="6fe52-238">a response code indicating the outcome of the operation</span></span>
        * <span data-ttu-id="6fe52-239">열거 작업에 성공 하는 경우 패키지의 파일 경로</span><span class="sxs-lookup"><span data-stu-id="6fe52-239">an enumerable of file paths in the package if the operation was successful</span></span>

6.  <span data-ttu-id="6fe52-240">작업 클레임 가져오기</span><span class="sxs-lookup"><span data-stu-id="6fe52-240">Get operation claims</span></span> 
    * <span data-ttu-id="6fe52-241">방향 요청: NuGet-플러그 인 ></span><span class="sxs-lookup"><span data-stu-id="6fe52-241">Request direction:  NuGet -> plugin</span></span>
    * <span data-ttu-id="6fe52-242">요청이 포함 됩니다.</span><span class="sxs-lookup"><span data-stu-id="6fe52-242">The request will contain:</span></span>
        * <span data-ttu-id="6fe52-243">패키지 원본에 대 한 서비스 index.json</span><span class="sxs-lookup"><span data-stu-id="6fe52-243">the service index.json for a package source</span></span>
        * <span data-ttu-id="6fe52-244">패키지 원본 리포지토리 위치</span><span class="sxs-lookup"><span data-stu-id="6fe52-244">the package source repository location</span></span>
    * <span data-ttu-id="6fe52-245">응답에 포함 됩니다.</span><span class="sxs-lookup"><span data-stu-id="6fe52-245">A response will contain:</span></span>
        * <span data-ttu-id="6fe52-246">작업의 결과 나타내는 응답 코드</span><span class="sxs-lookup"><span data-stu-id="6fe52-246">a response code indicating the outcome of the operation</span></span>
        * <span data-ttu-id="6fe52-247">열거 가능한 지원 되는 작업 (예: 패키지 다운로드) 작업에 성공 하는 경우.</span><span class="sxs-lookup"><span data-stu-id="6fe52-247">an enumerable of supported operations (e.g.:  package download) if the operation was successful.</span></span>  <span data-ttu-id="6fe52-248">플러그 인 패키지 소스를 지원 하지 않는 경우 플러그 인에 지원 되는 작업의 빈 집합을 반환 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="6fe52-248">If a plugin does not support the package source, the plugin must return an empty set of supported operations.</span></span>

> [!Note]
> <span data-ttu-id="6fe52-249">이 메시지 버전에서 업데이트 되었습니다 *2.0.0*합니다.</span><span class="sxs-lookup"><span data-stu-id="6fe52-249">This message has been updated in version *2.0.0*.</span></span> <span data-ttu-id="6fe52-250">이전 버전과 호환성을 유지 하기 위해 클라이언트입니다.</span><span class="sxs-lookup"><span data-stu-id="6fe52-250">It is on the client to preserve backward compatibility.</span></span>

7.  <span data-ttu-id="6fe52-251">패키지 해시를 가져오려면</span><span class="sxs-lookup"><span data-stu-id="6fe52-251">Get package hash</span></span>
    * <span data-ttu-id="6fe52-252">방향 요청: NuGet-플러그 인 ></span><span class="sxs-lookup"><span data-stu-id="6fe52-252">Request direction:  NuGet -> plugin</span></span>
    * <span data-ttu-id="6fe52-253">요청이 포함 됩니다.</span><span class="sxs-lookup"><span data-stu-id="6fe52-253">The request will contain:</span></span>
        * <span data-ttu-id="6fe52-254">패키지 ID 및 버전</span><span class="sxs-lookup"><span data-stu-id="6fe52-254">the package ID and version</span></span>
        * <span data-ttu-id="6fe52-255">패키지 원본 리포지토리 위치</span><span class="sxs-lookup"><span data-stu-id="6fe52-255">the package source repository location</span></span>
        * <span data-ttu-id="6fe52-256">해시 알고리즘</span><span class="sxs-lookup"><span data-stu-id="6fe52-256">the hash algorithm</span></span>
    * <span data-ttu-id="6fe52-257">응답에 포함 됩니다.</span><span class="sxs-lookup"><span data-stu-id="6fe52-257">A response will contain:</span></span>
        * <span data-ttu-id="6fe52-258">작업의 결과 나타내는 응답 코드</span><span class="sxs-lookup"><span data-stu-id="6fe52-258">a response code indicating the outcome of the operation</span></span>
        * <span data-ttu-id="6fe52-259">작업에 성공 하는 경우 요청 된 해시 알고리즘을 사용 하 여 패키지 파일 해시</span><span class="sxs-lookup"><span data-stu-id="6fe52-259">a package file hash using the requested hash algorithm if the operation was successful</span></span>

8.  <span data-ttu-id="6fe52-260">패키지 버전 가져오기</span><span class="sxs-lookup"><span data-stu-id="6fe52-260">Get package versions</span></span>
    * <span data-ttu-id="6fe52-261">방향 요청: NuGet-플러그 인 ></span><span class="sxs-lookup"><span data-stu-id="6fe52-261">Request direction:  NuGet -> plugin</span></span>
    * <span data-ttu-id="6fe52-262">요청이 포함 됩니다.</span><span class="sxs-lookup"><span data-stu-id="6fe52-262">The request will contain:</span></span>
        * <span data-ttu-id="6fe52-263">패키지 ID</span><span class="sxs-lookup"><span data-stu-id="6fe52-263">the package ID</span></span>
        * <span data-ttu-id="6fe52-264">패키지 원본 리포지토리 위치</span><span class="sxs-lookup"><span data-stu-id="6fe52-264">the package source repository location</span></span>
    * <span data-ttu-id="6fe52-265">응답에 포함 됩니다.</span><span class="sxs-lookup"><span data-stu-id="6fe52-265">A response will contain:</span></span>
        * <span data-ttu-id="6fe52-266">작업의 결과 나타내는 응답 코드</span><span class="sxs-lookup"><span data-stu-id="6fe52-266">a response code indicating the outcome of the operation</span></span>
        * <span data-ttu-id="6fe52-267">열거 가능한 작업에 성공 하는 경우 패키지 버전</span><span class="sxs-lookup"><span data-stu-id="6fe52-267">an enumerable of package versions if the operation was successful</span></span>

9.  <span data-ttu-id="6fe52-268">서비스 인덱스 가져오기</span><span class="sxs-lookup"><span data-stu-id="6fe52-268">Get service index</span></span>
    * <span data-ttu-id="6fe52-269">방향 요청: 플러그 인에는 NuGet-></span><span class="sxs-lookup"><span data-stu-id="6fe52-269">Request direction:  plugin -> NuGet</span></span>
    * <span data-ttu-id="6fe52-270">요청이 포함 됩니다.</span><span class="sxs-lookup"><span data-stu-id="6fe52-270">The request will contain:</span></span>
        * <span data-ttu-id="6fe52-271">패키지 원본 리포지토리 위치</span><span class="sxs-lookup"><span data-stu-id="6fe52-271">the package source repository location</span></span>
    * <span data-ttu-id="6fe52-272">응답에 포함 됩니다.</span><span class="sxs-lookup"><span data-stu-id="6fe52-272">A response will contain:</span></span>
        * <span data-ttu-id="6fe52-273">작업의 결과 나타내는 응답 코드</span><span class="sxs-lookup"><span data-stu-id="6fe52-273">a response code indicating the outcome of the operation</span></span>
        * <span data-ttu-id="6fe52-274">서비스 인덱스 작업에 성공 하는 경우</span><span class="sxs-lookup"><span data-stu-id="6fe52-274">the service index if the operation was successful</span></span>

10.  <span data-ttu-id="6fe52-275">핸드셰이크</span><span class="sxs-lookup"><span data-stu-id="6fe52-275">Handshake</span></span>
     * <span data-ttu-id="6fe52-276">방향 요청: NuGet <>-플러그 인</span><span class="sxs-lookup"><span data-stu-id="6fe52-276">Request direction:  NuGet <-> plugin</span></span>
     * <span data-ttu-id="6fe52-277">요청이 포함 됩니다.</span><span class="sxs-lookup"><span data-stu-id="6fe52-277">The request will contain:</span></span>
         * <span data-ttu-id="6fe52-278">현재 플러그 인 프로토콜 버전</span><span class="sxs-lookup"><span data-stu-id="6fe52-278">the current plugin protocol version</span></span>
         * <span data-ttu-id="6fe52-279">지원 되는 플러그 인을 최소 프로토콜 버전</span><span class="sxs-lookup"><span data-stu-id="6fe52-279">the minimum supported plugin protocol version</span></span>
     * <span data-ttu-id="6fe52-280">응답에 포함 됩니다.</span><span class="sxs-lookup"><span data-stu-id="6fe52-280">A response will contain:</span></span>
         * <span data-ttu-id="6fe52-281">작업의 결과 나타내는 응답 코드</span><span class="sxs-lookup"><span data-stu-id="6fe52-281">a response code indicating the outcome of the operation</span></span>
         * <span data-ttu-id="6fe52-282">작업에 성공 하는 경우 협상 된 프로토콜 버전입니다.</span><span class="sxs-lookup"><span data-stu-id="6fe52-282">the negotiated protocol version if the operation was successful.</span></span>  <span data-ttu-id="6fe52-283">플러그 인 종료 오류가 발생 합니다.</span><span class="sxs-lookup"><span data-stu-id="6fe52-283">A failure will result in termination of the plugin.</span></span>

11.  <span data-ttu-id="6fe52-284">초기화</span><span class="sxs-lookup"><span data-stu-id="6fe52-284">Initialize</span></span>
     * <span data-ttu-id="6fe52-285">방향 요청: NuGet-플러그 인 ></span><span class="sxs-lookup"><span data-stu-id="6fe52-285">Request direction:  NuGet -> plugin</span></span>
     * <span data-ttu-id="6fe52-286">요청이 포함 됩니다.</span><span class="sxs-lookup"><span data-stu-id="6fe52-286">The request will contain:</span></span>
         * <span data-ttu-id="6fe52-287">NuGet 클라이언트 도구 버전</span><span class="sxs-lookup"><span data-stu-id="6fe52-287">the NuGet client tool version</span></span>
         * <span data-ttu-id="6fe52-288">NuGet 클라이언트 도구 효과적인 언어입니다.</span><span class="sxs-lookup"><span data-stu-id="6fe52-288">the NuGet client tool effective language.</span></span>  <span data-ttu-id="6fe52-289">이 고려 ForceEnglishOutput 설정을 사용 하는 경우.</span><span class="sxs-lookup"><span data-stu-id="6fe52-289">This takes into consideration the ForceEnglishOutput setting, if used.</span></span>
         * <span data-ttu-id="6fe52-290">기본 요청 제한 시간이 프로토콜 기본 대체 합니다.</span><span class="sxs-lookup"><span data-stu-id="6fe52-290">the default request timeout, which supersedes the protocol default.</span></span>
     * <span data-ttu-id="6fe52-291">응답에 포함 됩니다.</span><span class="sxs-lookup"><span data-stu-id="6fe52-291">A response will contain:</span></span>
         * <span data-ttu-id="6fe52-292">작업의 결과 나타내는 응답 코드입니다.</span><span class="sxs-lookup"><span data-stu-id="6fe52-292">a response code indicating the outcome of the operation.</span></span>  <span data-ttu-id="6fe52-293">플러그 인 종료 오류가 발생 합니다.</span><span class="sxs-lookup"><span data-stu-id="6fe52-293">A failure will result in termination of the plugin.</span></span>

12.  <span data-ttu-id="6fe52-294">로그</span><span class="sxs-lookup"><span data-stu-id="6fe52-294">Log</span></span>
     * <span data-ttu-id="6fe52-295">방향 요청: 플러그 인에는 NuGet-></span><span class="sxs-lookup"><span data-stu-id="6fe52-295">Request direction:  plugin -> NuGet</span></span>
     * <span data-ttu-id="6fe52-296">요청이 포함 됩니다.</span><span class="sxs-lookup"><span data-stu-id="6fe52-296">The request will contain:</span></span>
         * <span data-ttu-id="6fe52-297">요청에 대 한 로그 수준</span><span class="sxs-lookup"><span data-stu-id="6fe52-297">the log level for the request</span></span>
         * <span data-ttu-id="6fe52-298">기록할 메시지</span><span class="sxs-lookup"><span data-stu-id="6fe52-298">a message to log</span></span>
     * <span data-ttu-id="6fe52-299">응답에 포함 됩니다.</span><span class="sxs-lookup"><span data-stu-id="6fe52-299">A response will contain:</span></span>
         * <span data-ttu-id="6fe52-300">작업의 결과 나타내는 응답 코드입니다.</span><span class="sxs-lookup"><span data-stu-id="6fe52-300">a response code indicating the outcome of the operation.</span></span>

13.  <span data-ttu-id="6fe52-301">NuGet 프로세스 종료를 모니터링 합니다.</span><span class="sxs-lookup"><span data-stu-id="6fe52-301">Monitor NuGet process exit</span></span>
     * <span data-ttu-id="6fe52-302">방향 요청: NuGet-플러그 인 ></span><span class="sxs-lookup"><span data-stu-id="6fe52-302">Request direction:  NuGet -> plugin</span></span>
     * <span data-ttu-id="6fe52-303">요청이 포함 됩니다.</span><span class="sxs-lookup"><span data-stu-id="6fe52-303">The request will contain:</span></span>
         * <span data-ttu-id="6fe52-304">NuGet 프로세스 ID</span><span class="sxs-lookup"><span data-stu-id="6fe52-304">the NuGet process ID</span></span>
     * <span data-ttu-id="6fe52-305">응답에 포함 됩니다.</span><span class="sxs-lookup"><span data-stu-id="6fe52-305">A response will contain:</span></span>
         * <span data-ttu-id="6fe52-306">작업의 결과 나타내는 응답 코드입니다.</span><span class="sxs-lookup"><span data-stu-id="6fe52-306">a response code indicating the outcome of the operation.</span></span>

14.  <span data-ttu-id="6fe52-307">패키지를 사전 인출</span><span class="sxs-lookup"><span data-stu-id="6fe52-307">Prefetch package</span></span>
     * <span data-ttu-id="6fe52-308">방향 요청: NuGet-플러그 인 ></span><span class="sxs-lookup"><span data-stu-id="6fe52-308">Request direction:  NuGet -> plugin</span></span>
     * <span data-ttu-id="6fe52-309">요청이 포함 됩니다.</span><span class="sxs-lookup"><span data-stu-id="6fe52-309">The request will contain:</span></span>
         * <span data-ttu-id="6fe52-310">패키지 ID 및 버전</span><span class="sxs-lookup"><span data-stu-id="6fe52-310">the package ID and version</span></span>
         * <span data-ttu-id="6fe52-311">패키지 원본 리포지토리 위치</span><span class="sxs-lookup"><span data-stu-id="6fe52-311">the package source repository location</span></span>
     * <span data-ttu-id="6fe52-312">응답에 포함 됩니다.</span><span class="sxs-lookup"><span data-stu-id="6fe52-312">A response will contain:</span></span>
         * <span data-ttu-id="6fe52-313">작업의 결과 나타내는 응답 코드</span><span class="sxs-lookup"><span data-stu-id="6fe52-313">a response code indicating the outcome of the operation</span></span>

15.  <span data-ttu-id="6fe52-314">자격 증명 설정</span><span class="sxs-lookup"><span data-stu-id="6fe52-314">Set credentials</span></span>
     * <span data-ttu-id="6fe52-315">방향 요청: NuGet-플러그 인 ></span><span class="sxs-lookup"><span data-stu-id="6fe52-315">Request direction:  NuGet -> plugin</span></span>
     * <span data-ttu-id="6fe52-316">요청이 포함 됩니다.</span><span class="sxs-lookup"><span data-stu-id="6fe52-316">The request will contain:</span></span>
         * <span data-ttu-id="6fe52-317">패키지 원본 리포지토리 위치</span><span class="sxs-lookup"><span data-stu-id="6fe52-317">the package source repository location</span></span>
         * <span data-ttu-id="6fe52-318">마지막으로 알려진된 패키지 원본 사용자 이름, 사용 가능한 경우</span><span class="sxs-lookup"><span data-stu-id="6fe52-318">the last known package source username, if available</span></span>
         * <span data-ttu-id="6fe52-319">마지막으로 알려진된 패키지 소스 암호를 사용할 수 있는 경우</span><span class="sxs-lookup"><span data-stu-id="6fe52-319">the last known package source password, if available</span></span>
         * <span data-ttu-id="6fe52-320">마지막으로 알려진된 프록시 사용자 이름, 사용 가능한 경우</span><span class="sxs-lookup"><span data-stu-id="6fe52-320">the last known proxy username, if available</span></span>
         * <span data-ttu-id="6fe52-321">마지막으로 알려진된 프록시 암호를 사용할 수 있는 경우</span><span class="sxs-lookup"><span data-stu-id="6fe52-321">the last known proxy password, if available</span></span>
     * <span data-ttu-id="6fe52-322">응답에 포함 됩니다.</span><span class="sxs-lookup"><span data-stu-id="6fe52-322">A response will contain:</span></span>
         * <span data-ttu-id="6fe52-323">작업의 결과 나타내는 응답 코드</span><span class="sxs-lookup"><span data-stu-id="6fe52-323">a response code indicating the outcome of the operation</span></span>

16.  <span data-ttu-id="6fe52-324">로그 수준 설정</span><span class="sxs-lookup"><span data-stu-id="6fe52-324">Set log level</span></span>
     * <span data-ttu-id="6fe52-325">방향 요청: NuGet-플러그 인 ></span><span class="sxs-lookup"><span data-stu-id="6fe52-325">Request direction:  NuGet -> plugin</span></span>
     * <span data-ttu-id="6fe52-326">요청이 포함 됩니다.</span><span class="sxs-lookup"><span data-stu-id="6fe52-326">The request will contain:</span></span>
         * <span data-ttu-id="6fe52-327">기본 로그 수준</span><span class="sxs-lookup"><span data-stu-id="6fe52-327">the default log level</span></span>
     * <span data-ttu-id="6fe52-328">응답에 포함 됩니다.</span><span class="sxs-lookup"><span data-stu-id="6fe52-328">A response will contain:</span></span>
         * <span data-ttu-id="6fe52-329">작업의 결과 나타내는 응답 코드</span><span class="sxs-lookup"><span data-stu-id="6fe52-329">a response code indicating the outcome of the operation</span></span>

<span data-ttu-id="6fe52-330">프로토콜 버전 *2.0.0* 메시지</span><span class="sxs-lookup"><span data-stu-id="6fe52-330">Protocol Version *2.0.0* messages</span></span>

17. <span data-ttu-id="6fe52-331">작업 클레임 가져오기</span><span class="sxs-lookup"><span data-stu-id="6fe52-331">Get Operation Claims</span></span>

* <span data-ttu-id="6fe52-332">방향 요청: NuGet-플러그 인 ></span><span class="sxs-lookup"><span data-stu-id="6fe52-332">Request direction:  NuGet -> plugin</span></span>
    * <span data-ttu-id="6fe52-333">요청이 포함 됩니다.</span><span class="sxs-lookup"><span data-stu-id="6fe52-333">The request will contain:</span></span>
        * <span data-ttu-id="6fe52-334">패키지 원본에 대 한 서비스 index.json</span><span class="sxs-lookup"><span data-stu-id="6fe52-334">the service index.json for a package source</span></span>
        * <span data-ttu-id="6fe52-335">패키지 원본 리포지토리 위치</span><span class="sxs-lookup"><span data-stu-id="6fe52-335">the package source repository location</span></span>
    * <span data-ttu-id="6fe52-336">응답에 포함 됩니다.</span><span class="sxs-lookup"><span data-stu-id="6fe52-336">A response will contain:</span></span>
        * <span data-ttu-id="6fe52-337">작업의 결과 나타내는 응답 코드</span><span class="sxs-lookup"><span data-stu-id="6fe52-337">a response code indicating the outcome of the operation</span></span>
        * <span data-ttu-id="6fe52-338">열거 작업에 성공 하는 경우 지원 되는 작업입니다.</span><span class="sxs-lookup"><span data-stu-id="6fe52-338">an enumerable of supported operations if the operation was successful.</span></span>  <span data-ttu-id="6fe52-339">플러그 인 패키지 소스를 지원 하지 않는 경우 플러그 인에 지원 되는 작업의 빈 집합을 반환 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="6fe52-339">If a plugin does not support the package source, the plugin must return an empty set of supported operations.</span></span>

    <span data-ttu-id="6fe52-340">서비스 인덱스와 패키지 원본 null 인 경우에 인증을 사용 하 여 플러그 인 답변할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="6fe52-340">If the service index and package source are null, then the plugin can answer with authentication.</span></span>

18. <span data-ttu-id="6fe52-341">인증 자격 증명 가져오기</span><span class="sxs-lookup"><span data-stu-id="6fe52-341">Get Authentication Credentials</span></span>

* <span data-ttu-id="6fe52-342">방향 요청: NuGet-플러그 인 ></span><span class="sxs-lookup"><span data-stu-id="6fe52-342">Request direction: NuGet -> plugin</span></span>
* <span data-ttu-id="6fe52-343">요청이 포함 됩니다.</span><span class="sxs-lookup"><span data-stu-id="6fe52-343">The request will contain:</span></span>
    * <span data-ttu-id="6fe52-344">URI</span><span class="sxs-lookup"><span data-stu-id="6fe52-344">Uri</span></span>
    * <span data-ttu-id="6fe52-345">isRetry</span><span class="sxs-lookup"><span data-stu-id="6fe52-345">isRetry</span></span>
    * <span data-ttu-id="6fe52-346">NonInteractive</span><span class="sxs-lookup"><span data-stu-id="6fe52-346">NonInteractive</span></span>
    * <span data-ttu-id="6fe52-347">CanShowDialog</span><span class="sxs-lookup"><span data-stu-id="6fe52-347">CanShowDialog</span></span>
* <span data-ttu-id="6fe52-348">응답에 포함 됩니다.</span><span class="sxs-lookup"><span data-stu-id="6fe52-348">A response will contain</span></span>
    * <span data-ttu-id="6fe52-349">사용자 이름</span><span class="sxs-lookup"><span data-stu-id="6fe52-349">Username</span></span>
    * <span data-ttu-id="6fe52-350">암호</span><span class="sxs-lookup"><span data-stu-id="6fe52-350">Password</span></span>
    * <span data-ttu-id="6fe52-351">메시지</span><span class="sxs-lookup"><span data-stu-id="6fe52-351">Message</span></span>
    * <span data-ttu-id="6fe52-352">인증 유형 목록</span><span class="sxs-lookup"><span data-stu-id="6fe52-352">List of Auth Types</span></span>
    * <span data-ttu-id="6fe52-353">MessageResponseCode</span><span class="sxs-lookup"><span data-stu-id="6fe52-353">MessageResponseCode</span></span>