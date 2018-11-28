---
title: NuGet 교차 플랫폼 인증 플러그 인
description: NuGet은 NuGet.exe "," dotnet.exe "," msbuild.exe "및" Visual Studio에 대 한 인증 플러그 인 플랫폼 간
author: nkolev92
ms.author: nikolev
ms.date: 07/01/2018
ms.topic: conceptual
ms.openlocfilehash: b76fab1028ec9a4172d2390083fbf9adb4290a6c
ms.sourcegitcommit: 0c5a49ec6e0254a4e7a9d8bca7daeefb853c433a
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 11/28/2018
ms.locfileid: "52453509"
---
# <a name="nuget-cross-platform-authentication-plugin"></a><span data-ttu-id="8bb7c-103">NuGet 교차 플랫폼 인증 플러그 인</span><span class="sxs-lookup"><span data-stu-id="8bb7c-103">NuGet cross platform authentication plugin</span></span>

<span data-ttu-id="8bb7c-104">4.8 이상, 클라이언트 (NuGet.exe를 Visual Studio, dotnet.exe 및 MSBuild.exe) 기반으로 구축 하는 인증 플러그 인을 사용할 수 있습니다 하는 모든 NuGet 버전에는 [플러그 인 플랫폼 간 NuGet](NuGet-Cross-Platform-Plugins.md) 모델입니다.</span><span class="sxs-lookup"><span data-stu-id="8bb7c-104">In version 4.8+, all NuGet clients (NuGet.exe, Visual Studio, dotnet.exe and MSBuild.exe) can use an authentication plugin built on top of the [NuGet cross platform plugins](NuGet-Cross-Platform-Plugins.md) model.</span></span>

## <a name="authentication-in-dotnetexe"></a><span data-ttu-id="8bb7c-105">Dotnet.exe에 인증</span><span class="sxs-lookup"><span data-stu-id="8bb7c-105">Authentication in dotnet.exe</span></span>

<span data-ttu-id="8bb7c-106">Visual Studio NuGet.exe와 기본적으로 대화형입니다.</span><span class="sxs-lookup"><span data-stu-id="8bb7c-106">Visual Studio and NuGet.exe are by default interactive.</span></span> <span data-ttu-id="8bb7c-107">NuGet.exe 있도록 스위치를 포함 [비 대화형](../../tools/nuget-exe-CLI-Reference.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="8bb7c-107">NuGet.exe contains a switch to make it [non interactive](../../tools/nuget-exe-CLI-Reference.md).</span></span>
<span data-ttu-id="8bb7c-108">또한 NuGet.exe 및 Visual Studio 플러그 인 묻는 메시지를 입력 합니다.</span><span class="sxs-lookup"><span data-stu-id="8bb7c-108">Additionally the NuGet.exe and Visual Studio plugins prompt the user for input.</span></span>
<span data-ttu-id="8bb7c-109">Dotnet.exe에 메시지가 표시 되지 않습니다 되며 기본값은 비 대화형.</span><span class="sxs-lookup"><span data-stu-id="8bb7c-109">In dotnet.exe there is no prompting and the default is non interactive.</span></span>

<span data-ttu-id="8bb7c-110">Dotnet.exe에 인증 메커니즘은 장치 흐름입니다.</span><span class="sxs-lookup"><span data-stu-id="8bb7c-110">The authentication mechanism in dotnet.exe is device flow.</span></span> <span data-ttu-id="8bb7c-111">때 복원 하거나 패키지 작업을 대화형으로 실행 하 고 작업이 차단 하는 방법에 전체 인증이 제공 됩니다 명령줄에서 사용자에 게 지침을 추가 합니다.</span><span class="sxs-lookup"><span data-stu-id="8bb7c-111">When the restore or add package operation is run interactively, the operation blocks and instructions to the user how to complete the authentications will be provided on the command line.</span></span>
<span data-ttu-id="8bb7c-112">사용자 인증을 완료 하는 경우 작업이 계속 됩니다.</span><span class="sxs-lookup"><span data-stu-id="8bb7c-112">When the user completes the authentication the operation will continue.</span></span>

<span data-ttu-id="8bb7c-113">대화형 작업을 하려면 하나를 전달 해야 `--interactive`합니다.</span><span class="sxs-lookup"><span data-stu-id="8bb7c-113">To make the operation interactive, one should pass `--interactive`.</span></span>
<span data-ttu-id="8bb7c-114">현재는 명시적인 `dotnet restore` 및 `dotnet add package` 명령을 대화형 스위치를 지원 합니다.</span><span class="sxs-lookup"><span data-stu-id="8bb7c-114">Currently only the explicit `dotnet restore` and `dotnet add package` commands support an interactive switch.</span></span>
<span data-ttu-id="8bb7c-115">대화형 스위치가 없을 `dotnet build` 고 `dotnet publish`입니다.</span><span class="sxs-lookup"><span data-stu-id="8bb7c-115">There is no interactive switch on `dotnet build` and `dotnet publish`.</span></span>

## <a name="authentication-in-msbuild"></a><span data-ttu-id="8bb7c-116">MSBuild에서 인증</span><span class="sxs-lookup"><span data-stu-id="8bb7c-116">Authentication in MSBuild</span></span>

<span data-ttu-id="8bb7c-117">MSBuild.exe는 기본적으로 비 대화형 MSBuild.exe 인증 메커니즘은 장치 흐름 dotnet.exe 마찬가지로입니다.</span><span class="sxs-lookup"><span data-stu-id="8bb7c-117">Similar to dotnet.exe, MSBuild.exe is by default non interactive the MSBuild.exe authentication mechanism is device flow.</span></span>
<span data-ttu-id="8bb7c-118">일시 중지 하 고 인증에 대 한 대기에 대 한 복원을 허용 하려면 복원 호출 `msbuild -t:restore -p:NuGetInteractive="true"`합니다.</span><span class="sxs-lookup"><span data-stu-id="8bb7c-118">To allow the restore to pause and wait for authentication, call restore with `msbuild -t:restore -p:NuGetInteractive="true"`.</span></span>

## <a name="creating-a-cross-platform-authentication-plugin"></a><span data-ttu-id="8bb7c-119">플랫폼 간 인증 플러그 인 만들기</span><span class="sxs-lookup"><span data-stu-id="8bb7c-119">Creating a cross platform authentication plugin</span></span>

<span data-ttu-id="8bb7c-120">샘플 구현에서 찾을 수 있습니다 [Microsoft 자격 증명 공급자 플러그 인](https://github.com/Microsoft/artifacts-credprovider)합니다.</span><span class="sxs-lookup"><span data-stu-id="8bb7c-120">A sample implementation can be found in [Microsoft Credential Provider plugin](https://github.com/Microsoft/artifacts-credprovider).</span></span>

<span data-ttu-id="8bb7c-121">것 플러그 인 NuGet 클라이언트 도구에서 제시한 보안 요구 사항을 준수 하는지 매우 중요 합니다.</span><span class="sxs-lookup"><span data-stu-id="8bb7c-121">It's very important that the plugins conforms to the security requirements set forth by the NuGet client tools.</span></span>
<span data-ttu-id="8bb7c-122">인증 하는 플러그 인을 되도록 플러그 인에 대 한 버전이 필요한 최소 *2.0.0*합니다.</span><span class="sxs-lookup"><span data-stu-id="8bb7c-122">The minimum required version for a plugin to be an authentication plugin is *2.0.0*.</span></span>
<span data-ttu-id="8bb7c-123">NuGet 지원 되는 작업이 클레임에 대 한 플러그 인 및 쿼리를 사용 하 여 핸드셰이크를 수행 합니다.</span><span class="sxs-lookup"><span data-stu-id="8bb7c-123">NuGet will perform the handshake with the plugin and query for the supported operation claims.</span></span>
<span data-ttu-id="8bb7c-124">플러그 인 플랫폼 간 NuGet을 참조 하십시오 [메시지 프로토콜](NuGet-Cross-Platform-Plugins.md#protocol-messages-index) 특정 메시지에 대 한 자세한 내용은 합니다.</span><span class="sxs-lookup"><span data-stu-id="8bb7c-124">Please refer to the NuGet cross platform plugin [protocol messages](NuGet-Cross-Platform-Plugins.md#protocol-messages-index) for more details about the specific messages.</span></span>

<span data-ttu-id="8bb7c-125">NuGet 로그 수준을 설정 하 고 해당 하는 경우 플러그 인에 대 한 프록시 정보를 제공 합니다.</span><span class="sxs-lookup"><span data-stu-id="8bb7c-125">NuGet will set the log level and provide proxy information to the plugin when applicable.</span></span>
<span data-ttu-id="8bb7c-126">NuGet에 로깅 콘솔은만 허용 NuGet 플러그 인에는 로그 수준을 설정한 후입니다.</span><span class="sxs-lookup"><span data-stu-id="8bb7c-126">Logging to the NuGet console is only acceptable after NuGet has set the log level to the plugin.</span></span>

- <span data-ttu-id="8bb7c-127">.NET framework 플러그 인 인증 동작</span><span class="sxs-lookup"><span data-stu-id="8bb7c-127">.NET Framework plugin authentication behavior</span></span>

<span data-ttu-id="8bb7c-128">.NET framework에서 플러그 인 대화의 형태로 입력에 대 한 사용자에 게 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="8bb7c-128">In .NET Framework, the plugins are allowed to prompt a user for input, in the form of a dialog.</span></span>

- <span data-ttu-id="8bb7c-129">.NET core 플러그 인 인증 동작</span><span class="sxs-lookup"><span data-stu-id="8bb7c-129">.NET Core plugin authentication behavior</span></span>

<span data-ttu-id="8bb7c-130">.NET Core에서 대화 상자를 표시할 수 없습니다.</span><span class="sxs-lookup"><span data-stu-id="8bb7c-130">In .NET Core, a dialog cannot be shown.</span></span> <span data-ttu-id="8bb7c-131">플러그 인은 장치 흐름 인증을 사용 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="8bb7c-131">The plugins should use device flow to authenticate.</span></span>
<span data-ttu-id="8bb7c-132">플러그 인을 사용자에 게 지침을 사용 하 여 nuget 로그 메시지를 보낼 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="8bb7c-132">The plugin can send log messages to NuGet with instructions to the user.</span></span>
<span data-ttu-id="8bb7c-133">로그 수준을 설정한 후에 플러그 인 로깅을 사용할 수 있는지 참고 합니다.</span><span class="sxs-lookup"><span data-stu-id="8bb7c-133">Note that logging is available after the log level has been set to the plugin.</span></span>
<span data-ttu-id="8bb7c-134">NuGet은 명령줄에서 대화형 입력을 적용 되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="8bb7c-134">NuGet will not take any interactive input from the command line.</span></span>

<span data-ttu-id="8bb7c-135">클라이언트 가져오기 인증 자격 증명을 사용 하 여 플러그 인을 호출할 때 플러그 인 상호 작용 스위치를 준수 하 고 대화 스위치를 준수 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="8bb7c-135">When the client calls the plugin with a Get Authentication Credentials, the plugins need to conform to the interactivity switch and respect the dialog switch.</span></span> 

<span data-ttu-id="8bb7c-136">다음 표에서 모든 조합에 대 한 플러그 인 작동 해야 하는 방법을 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="8bb7c-136">The following table summarizes how the plugin should behave for all combinations.</span></span>

| <span data-ttu-id="8bb7c-137">IsNonInteractive</span><span class="sxs-lookup"><span data-stu-id="8bb7c-137">IsNonInteractive</span></span> | <span data-ttu-id="8bb7c-138">CanShowDialog</span><span class="sxs-lookup"><span data-stu-id="8bb7c-138">CanShowDialog</span></span> | <span data-ttu-id="8bb7c-139">플러그 인 동작</span><span class="sxs-lookup"><span data-stu-id="8bb7c-139">Plugin behavior</span></span> |
| ---------------- | ------------- | --------------- |
| <span data-ttu-id="8bb7c-140">true</span><span class="sxs-lookup"><span data-stu-id="8bb7c-140">true</span></span> | <span data-ttu-id="8bb7c-141">true</span><span class="sxs-lookup"><span data-stu-id="8bb7c-141">true</span></span> | <span data-ttu-id="8bb7c-142">IsNonInteractive 스위치 대화 스위치 보다 우선합니다.</span><span class="sxs-lookup"><span data-stu-id="8bb7c-142">The IsNonInteractive switch takes precedence over the dialog switch.</span></span> <span data-ttu-id="8bb7c-143">대화 상자를 표시 하는 플러그 인 허용 되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="8bb7c-143">The plugin is not allowed to pop a dialog.</span></span> <span data-ttu-id="8bb7c-144">이 조합은.NET Framework 플러그 인에만 유효.</span><span class="sxs-lookup"><span data-stu-id="8bb7c-144">This combination is only valid for .NET Framework plugins</span></span> |
| <span data-ttu-id="8bb7c-145">true</span><span class="sxs-lookup"><span data-stu-id="8bb7c-145">true</span></span> | <span data-ttu-id="8bb7c-146">False</span><span class="sxs-lookup"><span data-stu-id="8bb7c-146">false</span></span> | <span data-ttu-id="8bb7c-147">IsNonInteractive 스위치 대화 스위치 보다 우선합니다.</span><span class="sxs-lookup"><span data-stu-id="8bb7c-147">The IsNonInteractive switch takes precedence over the dialog switch.</span></span> <span data-ttu-id="8bb7c-148">플러그 인을 차단 하도록 허용 되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="8bb7c-148">The plugin is not allowed to block.</span></span> <span data-ttu-id="8bb7c-149">이 조합은.NET 핵심 플러그 인에만 유효.</span><span class="sxs-lookup"><span data-stu-id="8bb7c-149">This combination is only valid for .NET Core plugins</span></span> |
| <span data-ttu-id="8bb7c-150">False</span><span class="sxs-lookup"><span data-stu-id="8bb7c-150">false</span></span> | <span data-ttu-id="8bb7c-151">true</span><span class="sxs-lookup"><span data-stu-id="8bb7c-151">true</span></span> | <span data-ttu-id="8bb7c-152">플러그 인 대화 상자가 표시 됩니다.</span><span class="sxs-lookup"><span data-stu-id="8bb7c-152">The plugin should show a dialog.</span></span> <span data-ttu-id="8bb7c-153">이 조합은.NET Framework 플러그 인에만 유효.</span><span class="sxs-lookup"><span data-stu-id="8bb7c-153">This combination is only valid for .NET Framework plugins</span></span> |
| <span data-ttu-id="8bb7c-154">False</span><span class="sxs-lookup"><span data-stu-id="8bb7c-154">false</span></span> | <span data-ttu-id="8bb7c-155">False</span><span class="sxs-lookup"><span data-stu-id="8bb7c-155">false</span></span> | <span data-ttu-id="8bb7c-156">플러그 인 해야 수는 대화 상자를 표시 합니다.</span><span class="sxs-lookup"><span data-stu-id="8bb7c-156">The plugin should/can not show a dialog.</span></span> <span data-ttu-id="8bb7c-157">플러그 인으로 거를 통해 명령 메시지를 로깅에 의해 인증 장치 흐름을 사용 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="8bb7c-157">The plugin should use device flow to authenticate by logging an instruction message via the logger.</span></span> <span data-ttu-id="8bb7c-158">이 조합은.NET 핵심 플러그 인에만 유효.</span><span class="sxs-lookup"><span data-stu-id="8bb7c-158">This combination is only valid for .NET Core plugins</span></span> |

<span data-ttu-id="8bb7c-159">플러그 인을 작성 하기 전에 다음 사양을 참조 하세요.</span><span class="sxs-lookup"><span data-stu-id="8bb7c-159">Please refer to the following specs before writing a plugin.</span></span>

- [<span data-ttu-id="8bb7c-160">NuGet 패키지 다운로드 플러그 인</span><span class="sxs-lookup"><span data-stu-id="8bb7c-160">NuGet Package Download Plugin</span></span>](https://github.com/NuGet/Home/wiki/NuGet-Package-Download-Plugin)
- [<span data-ttu-id="8bb7c-161">구획 인증 플러그 인 간 NuGet</span><span class="sxs-lookup"><span data-stu-id="8bb7c-161">NuGet cross plat authentication plugin</span></span>](https://github.com/NuGet/Home/wiki/NuGet-cross-plat-authentication-plugin)
