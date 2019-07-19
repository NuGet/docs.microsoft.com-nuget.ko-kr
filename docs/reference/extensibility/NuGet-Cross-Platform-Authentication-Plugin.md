---
title: NuGet 플랫폼 간 인증 플러그 인
description: Nuget .exe, dotnet, msbuild.exe 및 Visual Studio 용 NuGet 크로스 플랫폼 인증 플러그 인
author: nkolev92
ms.author: nikolev
ms.date: 07/01/2018
ms.topic: conceptual
ms.openlocfilehash: a716737343ea826d28da6de46c32ca73aef590bd
ms.sourcegitcommit: efc18d484fdf0c7a8979b564dcb191c030601bb4
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/18/2019
ms.locfileid: "68317273"
---
# <a name="nuget-cross-platform-authentication-plugin"></a><span data-ttu-id="dd1ca-103">NuGet 플랫폼 간 인증 플러그 인</span><span class="sxs-lookup"><span data-stu-id="dd1ca-103">NuGet cross platform authentication plugin</span></span>

<span data-ttu-id="dd1ca-104">버전 4.8 +에서 모든 NuGet 클라이언트 (Nuget.exe, Visual Studio, dotnet 및 Msbuild.exe)는 [nuget 플랫폼 간 플러그 인](NuGet-Cross-Platform-Plugins.md) 모델을 기반으로 구축 된 인증 플러그 인을 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="dd1ca-104">In version 4.8+, all NuGet clients (NuGet.exe, Visual Studio, dotnet.exe and MSBuild.exe) can use an authentication plugin built on top of the [NuGet cross platform plugins](NuGet-Cross-Platform-Plugins.md) model.</span></span>

## <a name="authentication-in-dotnetexe"></a><span data-ttu-id="dd1ca-105">Dotnet의 인증</span><span class="sxs-lookup"><span data-stu-id="dd1ca-105">Authentication in dotnet.exe</span></span>

<span data-ttu-id="dd1ca-106">Visual Studio 및 Nuget.exe는 기본적으로 대화형입니다.</span><span class="sxs-lookup"><span data-stu-id="dd1ca-106">Visual Studio and NuGet.exe are by default interactive.</span></span> <span data-ttu-id="dd1ca-107">Nuget.exe에는 [비 대화형](../nuget-exe-CLI-Reference.md)으로 만드는 스위치가 포함 되어 있습니다.</span><span class="sxs-lookup"><span data-stu-id="dd1ca-107">NuGet.exe contains a switch to make it [non interactive](../nuget-exe-CLI-Reference.md).</span></span>
<span data-ttu-id="dd1ca-108">또한 Nuget.exe 및 Visual Studio 플러그 인에서 사용자에 게 입력 하 라는 메시지를 표시 합니다.</span><span class="sxs-lookup"><span data-stu-id="dd1ca-108">Additionally the NuGet.exe and Visual Studio plugins prompt the user for input.</span></span>
<span data-ttu-id="dd1ca-109">Dotnet에서 프롬프트가 표시 되지 않으며 기본값은 비 대화형입니다.</span><span class="sxs-lookup"><span data-stu-id="dd1ca-109">In dotnet.exe there is no prompting and the default is non interactive.</span></span>

<span data-ttu-id="dd1ca-110">Dotnet의 인증 메커니즘은 장치 흐름입니다.</span><span class="sxs-lookup"><span data-stu-id="dd1ca-110">The authentication mechanism in dotnet.exe is device flow.</span></span> <span data-ttu-id="dd1ca-111">복원 또는 패키지 추가 작업이 대화형으로 실행 되는 경우 사용자에 대 한 작업 블록과 지침이 명령줄에서 제공 됩니다.</span><span class="sxs-lookup"><span data-stu-id="dd1ca-111">When the restore or add package operation is run interactively, the operation blocks and instructions to the user how to complete the authentications will be provided on the command line.</span></span>
<span data-ttu-id="dd1ca-112">사용자가 인증을 완료 하면 작업이 계속 됩니다.</span><span class="sxs-lookup"><span data-stu-id="dd1ca-112">When the user completes the authentication the operation will continue.</span></span>

<span data-ttu-id="dd1ca-113">작업을 대화형으로 만들려면 한 번 통과 `--interactive`해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="dd1ca-113">To make the operation interactive, one should pass `--interactive`.</span></span>
<span data-ttu-id="dd1ca-114">현재 명시적 `dotnet restore` 및 `dotnet add package` 명령만 대화형 스위치를 지원 합니다.</span><span class="sxs-lookup"><span data-stu-id="dd1ca-114">Currently only the explicit `dotnet restore` and `dotnet add package` commands support an interactive switch.</span></span>
<span data-ttu-id="dd1ca-115">`dotnet build` 및`dotnet publish`에는 대화형 스위치가 없습니다.</span><span class="sxs-lookup"><span data-stu-id="dd1ca-115">There is no interactive switch on `dotnet build` and `dotnet publish`.</span></span>

## <a name="authentication-in-msbuild"></a><span data-ttu-id="dd1ca-116">MSBuild의 인증</span><span class="sxs-lookup"><span data-stu-id="dd1ca-116">Authentication in MSBuild</span></span>

<span data-ttu-id="dd1ca-117">Sc.exe와 마찬가지로 Msbuild.exe는 기본적으로 비 대화형입니다. Msbuild.exe 인증 메커니즘은 장치 흐름입니다.</span><span class="sxs-lookup"><span data-stu-id="dd1ca-117">Similar to dotnet.exe, MSBuild.exe is by default non interactive the MSBuild.exe authentication mechanism is device flow.</span></span>
<span data-ttu-id="dd1ca-118">복원을 일시 중지 하 고 인증을 대기 하려면를 사용 하 여 `msbuild -t:restore -p:NuGetInteractive="true"`restore를 호출 합니다.</span><span class="sxs-lookup"><span data-stu-id="dd1ca-118">To allow the restore to pause and wait for authentication, call restore with `msbuild -t:restore -p:NuGetInteractive="true"`.</span></span>

## <a name="creating-a-cross-platform-authentication-plugin"></a><span data-ttu-id="dd1ca-119">플랫폼 간 인증 플러그 인 만들기</span><span class="sxs-lookup"><span data-stu-id="dd1ca-119">Creating a cross platform authentication plugin</span></span>

<span data-ttu-id="dd1ca-120">샘플 구현은 [Microsoft 자격 증명 공급자 플러그 인](https://github.com/Microsoft/artifacts-credprovider)에서 찾을 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="dd1ca-120">A sample implementation can be found in [Microsoft Credential Provider plugin](https://github.com/Microsoft/artifacts-credprovider).</span></span>

<span data-ttu-id="dd1ca-121">플러그 인이 NuGet 클라이언트 도구에 의해 설정 된 보안 요구 사항을 준수 하는 것이 매우 중요 합니다.</span><span class="sxs-lookup"><span data-stu-id="dd1ca-121">It's very important that the plugins conforms to the security requirements set forth by the NuGet client tools.</span></span>
<span data-ttu-id="dd1ca-122">플러그 인에 대 한 플러그 인에 필요한 최소 버전은 *2.0.0*입니다.</span><span class="sxs-lookup"><span data-stu-id="dd1ca-122">The minimum required version for a plugin to be an authentication plugin is *2.0.0*.</span></span>
<span data-ttu-id="dd1ca-123">NuGet은 플러그 인 및 지원 되는 작업 클레임에 대 한 쿼리를 사용 하 여 핸드셰이크를 수행 합니다.</span><span class="sxs-lookup"><span data-stu-id="dd1ca-123">NuGet will perform the handshake with the plugin and query for the supported operation claims.</span></span>
<span data-ttu-id="dd1ca-124">특정 메시지에 대 한 자세한 내용은 NuGet 플랫폼 간 플러그 인 [프로토콜 메시지](NuGet-Cross-Platform-Plugins.md#protocol-messages-index) 를 참조 하세요.</span><span class="sxs-lookup"><span data-stu-id="dd1ca-124">Please refer to the NuGet cross platform plugin [protocol messages](NuGet-Cross-Platform-Plugins.md#protocol-messages-index) for more details about the specific messages.</span></span>

<span data-ttu-id="dd1ca-125">NuGet은 로그 수준을 설정 하 고 해당 하는 경우 플러그 인에 프록시 정보를 제공 합니다.</span><span class="sxs-lookup"><span data-stu-id="dd1ca-125">NuGet will set the log level and provide proxy information to the plugin when applicable.</span></span>
<span data-ttu-id="dd1ca-126">Nuget 콘솔에 로깅은 NuGet에서 로그 수준을 플러그 인으로 설정한 후에만 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="dd1ca-126">Logging to the NuGet console is only acceptable after NuGet has set the log level to the plugin.</span></span>

- <span data-ttu-id="dd1ca-127">.NET Framework 플러그 인 인증 동작</span><span class="sxs-lookup"><span data-stu-id="dd1ca-127">.NET Framework plugin authentication behavior</span></span>

<span data-ttu-id="dd1ca-128">.NET Framework 플러그 인은 대화 상자 형식으로 사용자에 게 입력 하 라는 메시지를 표시할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="dd1ca-128">In .NET Framework, the plugins are allowed to prompt a user for input, in the form of a dialog.</span></span>

- <span data-ttu-id="dd1ca-129">.NET Core 플러그 인 인증 동작</span><span class="sxs-lookup"><span data-stu-id="dd1ca-129">.NET Core plugin authentication behavior</span></span>

<span data-ttu-id="dd1ca-130">.NET Core에서는 대화 상자를 표시할 수 없습니다.</span><span class="sxs-lookup"><span data-stu-id="dd1ca-130">In .NET Core, a dialog cannot be shown.</span></span> <span data-ttu-id="dd1ca-131">플러그 인은 장치 흐름을 사용 하 여 인증 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="dd1ca-131">The plugins should use device flow to authenticate.</span></span>
<span data-ttu-id="dd1ca-132">플러그 인은 사용자에 게 지침을 포함 하 여 NuGet에 로그 메시지를 보낼 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="dd1ca-132">The plugin can send log messages to NuGet with instructions to the user.</span></span>
<span data-ttu-id="dd1ca-133">로그 수준이 플러그 인으로 설정 된 후에는 로깅을 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="dd1ca-133">Note that logging is available after the log level has been set to the plugin.</span></span>
<span data-ttu-id="dd1ca-134">NuGet은 명령줄에서 대화형 입력을 사용 하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="dd1ca-134">NuGet will not take any interactive input from the command line.</span></span>

<span data-ttu-id="dd1ca-135">클라이언트에서 Get Authentication 자격 증명을 사용 하 여 플러그 인을 호출 하는 경우 플러그 인은 대화형 스위치를 준수 하 고 대화 상자 스위치를 준수 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="dd1ca-135">When the client calls the plugin with a Get Authentication Credentials, the plugins need to conform to the interactivity switch and respect the dialog switch.</span></span> 

<span data-ttu-id="dd1ca-136">다음 표에는 플러그 인이 모든 조합에 대해 어떻게 동작 하는지 요약 되어 있습니다.</span><span class="sxs-lookup"><span data-stu-id="dd1ca-136">The following table summarizes how the plugin should behave for all combinations.</span></span>

| <span data-ttu-id="dd1ca-137">IsNonInteractive 대화형</span><span class="sxs-lookup"><span data-stu-id="dd1ca-137">IsNonInteractive</span></span> | <span data-ttu-id="dd1ca-138">CanShowDialog</span><span class="sxs-lookup"><span data-stu-id="dd1ca-138">CanShowDialog</span></span> | <span data-ttu-id="dd1ca-139">플러그 인 동작</span><span class="sxs-lookup"><span data-stu-id="dd1ca-139">Plugin behavior</span></span> |
| ---------------- | ------------- | --------------- |
| <span data-ttu-id="dd1ca-140">true</span><span class="sxs-lookup"><span data-stu-id="dd1ca-140">true</span></span> | <span data-ttu-id="dd1ca-141">true</span><span class="sxs-lookup"><span data-stu-id="dd1ca-141">true</span></span> | <span data-ttu-id="dd1ca-142">IsNonInteractive 대화형 스위치는 대화 상자 스위치 보다 우선적으로 적용 됩니다.</span><span class="sxs-lookup"><span data-stu-id="dd1ca-142">The IsNonInteractive switch takes precedence over the dialog switch.</span></span> <span data-ttu-id="dd1ca-143">플러그 인에서 대화 상자를 표시할 수 없습니다.</span><span class="sxs-lookup"><span data-stu-id="dd1ca-143">The plugin is not allowed to pop a dialog.</span></span> <span data-ttu-id="dd1ca-144">이 조합은 .NET Framework 플러그 인에만 유효 합니다.</span><span class="sxs-lookup"><span data-stu-id="dd1ca-144">This combination is only valid for .NET Framework plugins</span></span> |
| <span data-ttu-id="dd1ca-145">true</span><span class="sxs-lookup"><span data-stu-id="dd1ca-145">true</span></span> | <span data-ttu-id="dd1ca-146">false</span><span class="sxs-lookup"><span data-stu-id="dd1ca-146">false</span></span> | <span data-ttu-id="dd1ca-147">IsNonInteractive 대화형 스위치는 대화 상자 스위치 보다 우선적으로 적용 됩니다.</span><span class="sxs-lookup"><span data-stu-id="dd1ca-147">The IsNonInteractive switch takes precedence over the dialog switch.</span></span> <span data-ttu-id="dd1ca-148">플러그 인을 차단할 수 없습니다.</span><span class="sxs-lookup"><span data-stu-id="dd1ca-148">The plugin is not allowed to block.</span></span> <span data-ttu-id="dd1ca-149">이 조합은 .NET Core 플러그인에만 유효 합니다.</span><span class="sxs-lookup"><span data-stu-id="dd1ca-149">This combination is only valid for .NET Core plugins</span></span> |
| <span data-ttu-id="dd1ca-150">false</span><span class="sxs-lookup"><span data-stu-id="dd1ca-150">false</span></span> | <span data-ttu-id="dd1ca-151">true</span><span class="sxs-lookup"><span data-stu-id="dd1ca-151">true</span></span> | <span data-ttu-id="dd1ca-152">플러그 인은 대화 상자를 표시 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="dd1ca-152">The plugin should show a dialog.</span></span> <span data-ttu-id="dd1ca-153">이 조합은 .NET Framework 플러그 인에만 유효 합니다.</span><span class="sxs-lookup"><span data-stu-id="dd1ca-153">This combination is only valid for .NET Framework plugins</span></span> |
| <span data-ttu-id="dd1ca-154">false</span><span class="sxs-lookup"><span data-stu-id="dd1ca-154">false</span></span> | <span data-ttu-id="dd1ca-155">false</span><span class="sxs-lookup"><span data-stu-id="dd1ca-155">false</span></span> | <span data-ttu-id="dd1ca-156">플러그 인은 대화 상자를 표시할 수 없습니다.</span><span class="sxs-lookup"><span data-stu-id="dd1ca-156">The plugin should/can not show a dialog.</span></span> <span data-ttu-id="dd1ca-157">플러그 인은로 거를 통해 명령 메시지를 기록 하 여 인증 하려면 장치 흐름을 사용 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="dd1ca-157">The plugin should use device flow to authenticate by logging an instruction message via the logger.</span></span> <span data-ttu-id="dd1ca-158">이 조합은 .NET Core 플러그인에만 유효 합니다.</span><span class="sxs-lookup"><span data-stu-id="dd1ca-158">This combination is only valid for .NET Core plugins</span></span> |

<span data-ttu-id="dd1ca-159">플러그 인을 작성 하기 전에 다음 사양을 참조 하십시오.</span><span class="sxs-lookup"><span data-stu-id="dd1ca-159">Please refer to the following specs before writing a plugin.</span></span>

- [<span data-ttu-id="dd1ca-160">NuGet 패키지 다운로드 플러그 인</span><span class="sxs-lookup"><span data-stu-id="dd1ca-160">NuGet Package Download Plugin</span></span>](https://github.com/NuGet/Home/wiki/NuGet-Package-Download-Plugin)
- [<span data-ttu-id="dd1ca-161">NuGet 교차 cross-plat 인증 플러그 인</span><span class="sxs-lookup"><span data-stu-id="dd1ca-161">NuGet cross plat authentication plugin</span></span>](https://github.com/NuGet/Home/wiki/NuGet-cross-plat-authentication-plugin)
