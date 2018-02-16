---
title: "알려진 NuGet 문제 | Microsoft Docs"
author: karann-msft
ms.author: karann-msft
manager: ghogen
ms.date: 11/11/2016
ms.topic: article
ms.prod: nuget
ms.technology: 
description: "인증, 패키지 설치 및 도구를 포함하여 알려진 NuGet 관련 문제입니다."
keywords: "알려진 NuGet 문제, NuGet 문제"
ms.reviewer:
- karann-msft
- unniravindranathan
ms.openlocfilehash: 2b9190c058215d9e63894de45c0c55c8ddae0e0f
ms.sourcegitcommit: b0af28d1c809c7e951b0817d306643fcc162a030
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 02/14/2018
---
# <a name="known-issues-with-nuget"></a><span data-ttu-id="ca02a-104">알려진 NuGet 문제</span><span class="sxs-lookup"><span data-stu-id="ca02a-104">Known Issues with NuGet</span></span>

<span data-ttu-id="ca02a-105">반복적으로 보고되어 가장 일반적으로 알려진 NuGet 관련 문제입니다.</span><span class="sxs-lookup"><span data-stu-id="ca02a-105">These are the most common known issues with NuGet that are repeatedly reported.</span></span> <span data-ttu-id="ca02a-106">NuGet을 설치하거나 패키지를 관리하는 데 문제가 있는 경우 이러한 알려진 문제와 해결 방법을 살펴보세요.</span><span class="sxs-lookup"><span data-stu-id="ca02a-106">If you are having trouble installing NuGet or managing packages, please take a look through these known issues and their resolutions.</span></span>

> [!Note]
> <span data-ttu-id="ca02a-107">NuGet 4.0부터 알려진 문제는 각 릴리스 정보의 일부가 됩니다.</span><span class="sxs-lookup"><span data-stu-id="ca02a-107">Starting with NuGet 4.0, known issues are a part of the respective release notes.</span></span>

## <a name="authentication-issues-with-nuget-feeds-in-vsts-with-nugetexe-v343"></a><span data-ttu-id="ca02a-108">VSTS에서 nuget.exe v3.4.3을 통한 NuGet 피드 인증 문제</span><span class="sxs-lookup"><span data-stu-id="ca02a-108">Authentication issues with NuGet feeds in VSTS with nuget.exe v3.4.3</span></span>

<span data-ttu-id="ca02a-109">**문제:**</span><span class="sxs-lookup"><span data-stu-id="ca02a-109">**Problem:**</span></span>

<span data-ttu-id="ca02a-110">다음 명령을 사용하여 자격 증명을 저장하면 개인 액세스 토큰을 이중으로 암호화합니다.</span><span class="sxs-lookup"><span data-stu-id="ca02a-110">When we use the following command to store the credentials, we end up double encrypting the Personal Access Token.</span></span>

<span data-ttu-id="ca02a-111">$PAT = "개인 액세스 토큰" $Feed = "URL" .\nuget.exe sources add -Name Test -Source $Feed -UserName $UserName -Password $PAT</span><span class="sxs-lookup"><span data-stu-id="ca02a-111">$PAT = "Your personal access token" $Feed = "Your url" .\nuget.exe sources add -Name Test -Source $Feed -UserName $UserName -Password $PAT</span></span>

<span data-ttu-id="ca02a-112">**해결 방법:**</span><span class="sxs-lookup"><span data-stu-id="ca02a-112">**Workaround:**</span></span>

<span data-ttu-id="ca02a-113">[-StorePasswordInClearText](../tools/cli-ref-sources.md) 옵션을 사용하여 암호를 일반 텍스트로 저장합니다.</span><span class="sxs-lookup"><span data-stu-id="ca02a-113">Store passwords in clear text using the [-StorePasswordInClearText](../tools/cli-ref-sources.md) option.</span></span>

## <a name="error-installing-packages-with-nuget-34-341"></a><span data-ttu-id="ca02a-114">NuGet 3.4, 3.4.1 패키지 설치 오류</span><span class="sxs-lookup"><span data-stu-id="ca02a-114">Error installing packages with NuGet 3.4, 3.4.1</span></span>

<span data-ttu-id="ca02a-115">**문제:**</span><span class="sxs-lookup"><span data-stu-id="ca02a-115">**Problem:**</span></span>

<span data-ttu-id="ca02a-116">NuGet 3.4 및 3.4.1에서 NuGet 추가 기능을 사용하면 사용 가능한 원본이 보고되지 않으며 구성 창에서 새 원본을 추가할 수 없습니다.</span><span class="sxs-lookup"><span data-stu-id="ca02a-116">In NuGet 3.4 and 3.4.1, when using the NuGet add-in, no sources are reported as available and you are unable to add new sources in the configuration window.</span></span> <span data-ttu-id="ca02a-117">결과는 아래 이미지와 비슷합니다.</span><span class="sxs-lookup"><span data-stu-id="ca02a-117">The result is similar to the image below:</span></span>

![원본이 없는 NuGet config 파일](./media/knownIssue-34-NoSources.PNG)

<span data-ttu-id="ca02a-119">`%AppData%\NuGet\` 폴더에 있는 `NuGet.Config` 파일이 실수로 비어 있습니다.</span><span class="sxs-lookup"><span data-stu-id="ca02a-119">The `NuGet.Config` file in your `%AppData%\NuGet\` folder has accidentally been emptied.</span></span> <span data-ttu-id="ca02a-120">이 문제를 해결하려면 Visual Studio 2015를 닫고, `%AppData%\NuGet\` 폴더에서 `NuGet.Config` 파일을 삭제한 다음, Visual Studio를 다시 시작합니다.</span><span class="sxs-lookup"><span data-stu-id="ca02a-120">To fix this: Close Visual Studio 2015, delete the `NuGet.Config` file in the `%AppData%\NuGet\` folder and restart Visual Studio.</span></span>  <span data-ttu-id="ca02a-121">새 `NuGet.Config` 파일이 생성되고 계속 진행할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="ca02a-121">A new `NuGet.Config` file will be generated and you are able to proceed.</span></span>

## <a name="error-installing-packages-with-nuget-27"></a><span data-ttu-id="ca02a-122">NuGet 2.7 패키지 설치 오류</span><span class="sxs-lookup"><span data-stu-id="ca02a-122">Error installing packages with NuGet 2.7</span></span>

<span data-ttu-id="ca02a-123">**문제:**</span><span class="sxs-lookup"><span data-stu-id="ca02a-123">**Problem:**</span></span>

<span data-ttu-id="ca02a-124">NuGet 2.7 이상에서 어셈블리 참조가 포함된 패키지를 설치하려고 하면 아래와 같이 **"입력 문자열의 형식이 잘못되었습니다."**라는 오류 메시지가 표시될 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="ca02a-124">In NuGet 2.7 or above, when you attempt to install any package which contains assembly references, you may receive the error message **"Input string was not in a correct format."**, like below:</span></span>

```ps
install-package log4net
    Installing 'log4net 2.0.0'.
    Successfully installed 'log4net 2.0.0'.
    Adding 'log4net 2.0.0' to Tyson.OperatorUpload.
    Install failed. Rolling back...
    install-package : Input string was not in a correct format.
    At line:1 char:1
        install-package log4net
        ~~~~~~~~~~~~~~~~~~~~~~~
        CategoryInfo : NotSpecified: (:) [Install-Package], FormatException
        FullyQualifiedErrorId : NuGetCmdletUnhandledException,NuGet.PowerShell.Commands.InstallPackageCommand
```

<span data-ttu-id="ca02a-125">`VSLangProj.dll` COM 구성 요소에 대한 형식 라이브러리가 시스템에서 등록 취소되었기 때문에 이 오류가 발생합니다.</span><span class="sxs-lookup"><span data-stu-id="ca02a-125">This is caused by the type library for the `VSLangProj.dll` COM component being unregistered on your system.</span></span> <span data-ttu-id="ca02a-126">예를 들어 두 버전의 Visual Studio가 나란히 설치되어 있고 이전 버전을 제거하면 이 문제가 발생할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="ca02a-126">This can happen, for example, when you have two versions of Visual Studio installed side-by-side and you then uninstall the older version.</span></span> <span data-ttu-id="ca02a-127">이렇게 하면 위의 COM 라이브러리를 실수로 등록 취소할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="ca02a-127">Doing so may inadvertently unregister the above COM library.</span></span>

<span data-ttu-id="ca02a-128">**해결 방법:**:</span><span class="sxs-lookup"><span data-stu-id="ca02a-128">**Solution:**:</span></span>

<span data-ttu-id="ca02a-129">**관리자 권한 프롬프트에서**에서 다음 명령을 실행하여 `VSLangProj.dll`에 대한 형식 라이브러리를 다시 등록합니다.</span><span class="sxs-lookup"><span data-stu-id="ca02a-129">Run this command from an **elevated prompt** to re-register the type library for `VSLangProj.dll`</span></span>

    regsvr32 "C:\Program Files (x86)\Common Files\microsoft shared\MSEnv\VsLangproj.olb"

<span data-ttu-id="ca02a-130">명령이 실패하면 해당 위치에 파일이 있는지 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="ca02a-130">If the command fails, check to see if the file exists in that location.</span></span>

<span data-ttu-id="ca02a-131">이 오류에 대한 자세한 내용은 이 [작업 항목](https://nuget.codeplex.com/workitem/3609 "작업 항목 3609")를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="ca02a-131">For more information about this error, see this [work item](https://nuget.codeplex.com/workitem/3609 "Work item 3609").</span></span>

## <a name="build-failure-after-package-update-in-vs-2012"></a><span data-ttu-id="ca02a-132">VS 2012에서 패키지를 업데이트한 후에 빌드가 실패합니다.</span><span class="sxs-lookup"><span data-stu-id="ca02a-132">Build failure after package update in VS 2012</span></span>

<span data-ttu-id="ca02a-133">문제: VS 2012 RTM을 사용하고 있습니다.</span><span class="sxs-lookup"><span data-stu-id="ca02a-133">The problem: You are using VS 2012 RTM.</span></span> <span data-ttu-id="ca02a-134">NuGet 패키지를 업데이트할 때 "하나 이상의 패키지를 제거할 수 없습니다."라는 메시지가 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="ca02a-134">When updating NuGet packages, you get this message: "One or more packages could not be completed uninstalled."</span></span> <span data-ttu-id="ca02a-135">그리고 Visual Studio를 다시 시작하라는 메시지가 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="ca02a-135">and you are prompted to restart Visual Studio.</span></span> <span data-ttu-id="ca02a-136">이에 따라 VS를 다시 시작하면 이상한 빌드 오류가 발생합니다.</span><span class="sxs-lookup"><span data-stu-id="ca02a-136">After VS restart, you get weird build errors.</span></span>

<span data-ttu-id="ca02a-137">이는 이전 패키지의 특정 파일이 백그라운드 MSBuild 프로세스에서 잠겨 있기 때문입니다.</span><span class="sxs-lookup"><span data-stu-id="ca02a-137">The cause is that certain files in the old packages are locked by a background MSBuild process.</span></span> <span data-ttu-id="ca02a-138">VS를 다시 시작한 후에도 백그라운드 MSBuild 프로세스에서 이전 패키지의 파일을 계속 사용함으로써 빌드가 실패합니다.</span><span class="sxs-lookup"><span data-stu-id="ca02a-138">Even after VS restart, the background MSBuild process still uses the files in the old packages, causing the build failures.</span></span>

<span data-ttu-id="ca02a-139">이를 수정하려면 VS 2012 업데이트(예: VS 2012 업데이트 2)를 설치합니다.</span><span class="sxs-lookup"><span data-stu-id="ca02a-139">The fix is to install VS 2012 Update, e.g. VS 2012 Update 2.</span></span>

## <a name="upgrading-to-latest-nuget-from-an-older-version-causes-a-signature-verification-error"></a><span data-ttu-id="ca02a-140">이전 버전에서 최신 NuGet으로 업그레이드하면 서명 확인 오류가 발생합니다.</span><span class="sxs-lookup"><span data-stu-id="ca02a-140">Upgrading to latest NuGet from an older version causes a signature verification error</span></span>

<span data-ttu-id="ca02a-141">VS 2010 SP1을 실행하는 경우 설치되어 있는 이전 버전의 NuGet을 업그레이드하려고 할 때 다음과 같은 오류 메시지가 표시될 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="ca02a-141">If you are running VS 2010 SP1, you might run into the following error message when attempting to upgrade NuGet if you have an older version installed.</span></span>

![Visual Studio 확장 설치 관리자](./media/Visual-Studio-Extension-Installer.png)

<span data-ttu-id="ca02a-143">로그를 볼 때 `SignatureMismatchException`에 대한 언급이 표시될 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="ca02a-143">When viewing the logs, you might see a mention of a `SignatureMismatchException`.</span></span>

<span data-ttu-id="ca02a-144">이 문제가 발생하지 않도록 하기 위해 [Visual Studio 2010 SP1 핫픽스](http://bit.ly/vsixcertfix)를 설치할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="ca02a-144">To prevent this from occurring, there is a [Visual Studio 2010 SP1 hotfix](http://bit.ly/vsixcertfix) you can install.</span></span>
<span data-ttu-id="ca02a-145">또는 Visual Studio를 관리자 권한으로 실행하여 NuGet을 제거한 다음 VS 확장 갤러리에서 설치하기만 하면 됩니다.</span><span class="sxs-lookup"><span data-stu-id="ca02a-145">Alternatively, the workaround is to simply uninstall NuGet (while running Visual Studio as Administrator) and then install it from the VS Extension Gallery.</span></span>  <span data-ttu-id="ca02a-146">자세한 내용은 [http://support.microsoft.com/kb/2581019](http://support.microsoft.com/kb/2581019)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="ca02a-146">See [http://support.microsoft.com/kb/2581019](http://support.microsoft.com/kb/2581019) for more information.</span></span>

## <a name="package-manager-console-throws-an-exception-when-the-reflector-visual-studio-add-in-is-also-installed"></a><span data-ttu-id="ca02a-147">리플렉터 Visual Studio 추가 기능이 설치되면 패키지 관리자 콘솔에서 예외가 발생합니다.</span><span class="sxs-lookup"><span data-stu-id="ca02a-147">Package Manager Console throws an exception when the Reflector Visual Studio Add-In is also installed.</span></span>

<span data-ttu-id="ca02a-148">패키지 관리자 콘솔을 실행할 때 리플렉터 VS 추가 기능이 설치되면 다음과 같은 예외 메시지가 표시될 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="ca02a-148">When running the Package Manager console, you may run into the following exception message if you have the Reflector VS Add-in installed.</span></span>

    The following error occurred while loading the extended type data file:
    Microsoft.PowerShell.Core, C:\Windows\SysWOW64\WindowsPowerShell\v1.0\types.ps1xml(2950) :
    Error in type "System.Security.AccessControl.ObjectSecurity":
    Exception: Cannot convert the "Microsoft.PowerShell.Commands.SecurityDescriptorCommandsBase"
    value of type "System.String" to type "System.Type".
    System.Management.Automation.ActionPreferenceStopException:
    Command execution stopped because the preference variable "ErrorActionPreference" or common parameter
    is set to Stop: Unable to find type

<span data-ttu-id="ca02a-149">또는</span><span class="sxs-lookup"><span data-stu-id="ca02a-149">or</span></span>

    System.Management.Automation.CmdletInvocationException: Could not load file or assembly 'Scripts\nuget.psm1' or one of its dependencies. <br />The parameter is incorrect. (Exception from HRESULT: 0x80070057 (E_INVALIDARG)) ---&gt; System.IO.FileLoadException: Could not load file or <br />assembly 'Scripts\nuget.psm1' or one of its dependencies. The parameter is incorrect. (Exception from HRESULT: 0x80070057 (E_INVALIDARG)) <br />---&gt; System.ArgumentException: Illegal characters in path.
       at System.IO.Path.CheckInvalidPathChars(String path)
       at System.IO.Path.Combine(String path1, String path2)
       at Microsoft.VisualStudio.Platform.VsAppDomainManager.<AssemblyPaths>d__1.MoveNext()
       at Microsoft.VisualStudio.Platform.VsAppDomainManager.InnerResolveHandler(String name)
       at Microsoft.VisualStudio.Platform.VsAppDomainManager.ResolveHandler(Object sender, ResolveEventArgs args)
       at System.AppDomain.OnAssemblyResolveEvent(RuntimeAssembly assembly, String assemblyFullName)
       --- End of inner exception stack trace ---
       at Microsoft.PowerShell.Commands.ModuleCmdletBase.LoadBinaryModule(Boolean trySnapInName, String moduleName, String fileName, <br />Assembly assemblyToLoad, String moduleBase, SessionState ss, String prefix, Boolean loadTypes, Boolean loadFormats, Boolean&amp; found)
       at Microsoft.PowerShell.Commands.ModuleCmdletBase.LoadModuleNamedInManifest(String moduleName, String moduleBase, <br />Boolean searchModulePath, <br />String prefix, SessionState ss, Boolean loadTypesFiles, Boolean loadFormatFiles, Boolean&amp; found)
       at Microsoft.PowerShell.Commands.ModuleCmdletBase.LoadModuleManifest(ExternalScriptInfo scriptInfo, ManifestProcessingFlags <br />manifestProcessingFlags, Version version)
       at Microsoft.PowerShell.Commands.ModuleCmdletBase.LoadModule(String fileName, String moduleBase, String prefix, SessionState ss, <br />Boolean&amp; found)
       at Microsoft.PowerShell.Commands.ImportModuleCommand.ProcessRecord()
       at System.Management.Automation.Cmdlet.DoProcessRecord()
       at System.Management.Automation.CommandProcessor.ProcessRecord()
       --- End of inner exception stack trace ---
       at System.Management.Automation.Runspaces.PipelineBase.Invoke(IEnumerable input)
       at System.Management.Automation.Runspaces.Pipeline.Invoke()
       at NuGetConsole.Host.PowerShell.Implementation.PowerShellHost.Invoke(String command, Object input, Boolean outputResults)
       at NuGetConsole.Host.PowerShell.Implementation.PowerShellHostExtensions.ImportModule(PowerShellHost host, String modulePath)
       at NuGetConsole.Host.PowerShell.Implementation.PowerShellHost.LoadStartupScripts()
       at NuGetConsole.Host.PowerShell.Implementation.PowerShellHost.Initialize()
       at NuGetConsole.Implementation.Console.ConsoleDispatcher.Start()
       at NuGetConsole.Implementation.PowerConsoleToolWindow.MoveFocus(FrameworkElement consolePane)

<span data-ttu-id="ca02a-150">문제를 해결하기 위해 추가 기능 작성자에게 연락했습니다.</span><span class="sxs-lookup"><span data-stu-id="ca02a-150">We've contacted the author of the add-in in the hopes of working out a resolution.</span></span>

<p class="info"><span data-ttu-id="ca02a-151">업데이트: 최신 버전인 리플렉터 6.5를 사용하면 더 이상 콘솔에서 이 예외가 발생하지 않음을 확인했습니다.</span><span class="sxs-lookup"><span data-stu-id="ca02a-151">Update: We have verified that the latest version of Reflector, 6.5, no longer causes this exception in the console.</span></span></p>

## <a name="opening-package-manager-console-fails-with-objectsecurity-exception"></a><span data-ttu-id="ca02a-152">ObjectSecurity 예외로 인해 패키지 관리자 콘솔 열기가 실패합니다.</span><span class="sxs-lookup"><span data-stu-id="ca02a-152">Opening Package Manager Console fails with ObjectSecurity exception</span></span>

<span data-ttu-id="ca02a-153">패키지 관리자 콘솔을 열려고 할 때 다음과 같은 오류가 표시될 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="ca02a-153">You might see these errors when trying to open the Package Manager Console:</span></span>

    The following error occurred while loading the extended type data file: Microsoft.PowerShell.Core, C:\Windows\SysWOW64\WindowsPowerShell\v1.0\types.ps1xml(2977) : Error in type "System.Security.AccessControl.ObjectSecurity": Exception: The getter method should be public, non void, static, and have one parameter of type PSObject.
    The following error occurred while loading the extended type data file: Microsoft.PowerShell.Core, C:\Windows\SysWOW64\WindowsPowerShell\v1.0\types.ps1xml(2984) : Error in type "System.Security.AccessControl.ObjectSecurity": Exception: The getter method should be public, non void, static, and have one parameter of type PSObject.
    The following error occurred while loading the extended type data file: Microsoft.PowerShell.Core, C:\Windows\SysWOW64\WindowsPowerShell\v1.0\types.ps1xml(2991) : Error in type "System.Security.AccessControl.ObjectSecurity": Exception: The getter method should be public, non void, static, and have one parameter of type PSObject.
    The following error occurred while loading the extended type data file: Microsoft.PowerShell.Core, C:\Windows\SysWOW64\WindowsPowerShell\v1.0\types.ps1xml(2998) : Error in type "System.Security.AccessControl.ObjectSecurity": Exception: The getter method should be public, non void, static, and have one parameter of type PSObject.
    The following error occurred while loading the extended type data file: Microsoft.PowerShell.Core, C:\Windows\SysWOW64\WindowsPowerShell\v1.0\types.ps1xml(3005) : Error in type "System.Security.AccessControl.ObjectSecurity": Exception: The getter method should be public, non void, static, and have one parameter of type PSObject.
    The term 'Get-ExecutionPolicy' is not recognized as the name of a cmdlet, function, script file, or operable program. Check the spelling of the name, or if a path was included, verify that the path is correct and try again.

<span data-ttu-id="ca02a-154">이 경우 [StackOverflow에서 설명](http://stackoverflow.com/questions/12638289/embedding-powershell-v2-0-in-net-app-on-windows-8-rtm)한 해결 방법에 따라 수정합니다.</span><span class="sxs-lookup"><span data-stu-id="ca02a-154">If so, follow the solution [discussed on StackOverflow](http://stackoverflow.com/questions/12638289/embedding-powershell-v2-0-in-net-app-on-windows-8-rtm) to fix them.</span></span>

## <a name="the-add-package-library-reference-dialog-throws-an-exception-if-the-solution-contains-installshield-limited-edition-project"></a><span data-ttu-id="ca02a-155">솔루션에 InstallShield Limited Edition 프로젝트가 포함된 경우 패키지 라이브러리 참조 추가 대화 상자에서 예외를 throw합니다.</span><span class="sxs-lookup"><span data-stu-id="ca02a-155">The Add Package Library Reference dialog throws an exception if the solution contains InstallShield Limited Edition Project</span></span>

<span data-ttu-id="ca02a-156">솔루션에 하나 이상의 InstallShield Limited Edition 프로젝트가 포함되어 있으면 **패키지 라이브러리 참조 추가** 대화 상자가 열릴 때 예외를 throw한다는 것을 확인했습니다.</span><span class="sxs-lookup"><span data-stu-id="ca02a-156">We have identified that if your solution contains one or more InstallShield Limited Edition project, the **Add Package Library Reference** dialog will throw an exception when opened.</span></span> <span data-ttu-id="ca02a-157">현재 InstallShield 프로젝트를 제거하거나 언로드하는 것을 제외하고는 아직 해결 방법이 없습니다.</span><span class="sxs-lookup"><span data-stu-id="ca02a-157">There is currently no workaround yet except either removing InstallShield projects or unloading them.</span></span>

## <a name="uninstall-button-greyed-out-nuget-requires-admin-privileges-to-installuninstall"></a><span data-ttu-id="ca02a-158">제거 단추가 회색으로 표시되나요?</span><span class="sxs-lookup"><span data-stu-id="ca02a-158">Uninstall Button Greyed out?</span></span> <span data-ttu-id="ca02a-159">NuGet을 설치/제거하려면 관리자 권한이 필요합니다.</span><span class="sxs-lookup"><span data-stu-id="ca02a-159">NuGet Requires Admin Privileges to Install/Uninstall</span></span>

<span data-ttu-id="ca02a-160">Visual Studio 확장 관리자를 통해 NuGet을 제거하려고 하면 [제거] 단추가 비활성화되어 있습니다.</span><span class="sxs-lookup"><span data-stu-id="ca02a-160">If you try to uninstall NuGet via the Visual Studio Extension Manager, you may notice that the Uninstall button is disabled.</span></span> <span data-ttu-id="ca02a-161">NuGet을 설치/제거하려면 관리자 권한이 필요합니다.</span><span class="sxs-lookup"><span data-stu-id="ca02a-161">NuGet requires admin access to install and uninstall.</span></span> <span data-ttu-id="ca02a-162">Visual Studio를 관리자 권한으로 다시 시작하여 확장을 제거합니다.</span><span class="sxs-lookup"><span data-stu-id="ca02a-162">Relaunch Visual Studio as an administrator to uninstall the extension.</span></span> <span data-ttu-id="ca02a-163">관리자 액세스를 통해 NuGet을 사용할 필요가 없습니다.</span><span class="sxs-lookup"><span data-stu-id="ca02a-163">NuGet does not require admin access to use it.</span></span>

## <a name="the-package-manager-console-crashes-when-i-open-it-in-windows-xp-whats-wrong"></a><span data-ttu-id="ca02a-164">Windows XP에서 패키지 관리자 콘솔을 열면 패키지 관리자 콘솔 작동이 중단됩니다.</span><span class="sxs-lookup"><span data-stu-id="ca02a-164">The Package Manager Console crashes when I open it in Windows XP.</span></span> <span data-ttu-id="ca02a-165">무엇이 문제인가요?</span><span class="sxs-lookup"><span data-stu-id="ca02a-165">What's wrong?</span></span>

<span data-ttu-id="ca02a-166">NuGet에는 Powershell 2.0 런타임이 필요합니다.</span><span class="sxs-lookup"><span data-stu-id="ca02a-166">NuGet requires Powershell 2.0 runtime.</span></span> <span data-ttu-id="ca02a-167">Windows XP에는 기본적으로 Powershell 2.0이 없습니다.</span><span class="sxs-lookup"><span data-stu-id="ca02a-167">Windows XP, by default, doesn't have Powershell 2.0.</span></span> <span data-ttu-id="ca02a-168">Powershell 2.0 런타임은 [http://support.microsoft.com/kb/968929](http://support.microsoft.com/kb/968929)에서 다운로드할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="ca02a-168">You can download the Powershell 2.0 runtime from [http://support.microsoft.com/kb/968929](http://support.microsoft.com/kb/968929).</span></span> <span data-ttu-id="ca02a-169">설치한 후에 Visual Studio를 다시 시작하면 패키지 관리자 콘솔을 열 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="ca02a-169">After you install it, restart Visual Studio and you should be able to open Package Manager Console.</span></span>

## <a name="visual-studio-2010-sp1-beta-crashes-on-exit-if-the-package-manager-console-is-open"></a><span data-ttu-id="ca02a-170">패키지 관리자 콘솔이 열려 있으면 종료 시 Visual Studio 2010 SP1 베타가 충돌합니다.</span><span class="sxs-lookup"><span data-stu-id="ca02a-170">Visual Studio 2010 SP1 Beta crashes on exit if the Package Manager Console is open.</span></span>

<span data-ttu-id="ca02a-171">Visual Studio 2010 SP1 베타를 설치한 경우 패키지 관리자 콘솔을 열어 놓은 채 Visual Studio를 닫으면 충돌이 발생할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="ca02a-171">If you have installed Visual Studio 2010 SP1 Beta, you may notice that if you leave the Package Manager Console open and close Visual Studio, it will crash.</span></span> <span data-ttu-id="ca02a-172">이는 알려진 Visual Studio 문제이며 SP1 RTM 릴리스에서 수정될 예정입니다.</span><span class="sxs-lookup"><span data-stu-id="ca02a-172">This is a known issue of Visual Studio and will be fixed in SP1 RTM release.</span></span> <span data-ttu-id="ca02a-173">현재는 이 충돌을 무시하거나 가능한 경우 SP1 베타를 제거합니다.</span><span class="sxs-lookup"><span data-stu-id="ca02a-173">For now, just ignore the crash or uninstall SP1 Beta if you can.</span></span>

## <a name="the-element-metadata--has-invalid-child-element-exception-occurs"></a><span data-ttu-id="ca02a-174">"'metadata' 요소에 잘못된 자식 요소가 있습니다."라는 예외가 발생했습니다.</span><span class="sxs-lookup"><span data-stu-id="ca02a-174">The element 'metadata' ... has invalid child element exception occurs</span></span>

<span data-ttu-id="ca02a-175">NuGet 시험판 버전으로 빌드된 패키지를 설치한 경우 해당 프로젝트를 사용하여 RTM 버전의 NuGet을 실행할 때 "'schemas.microsoft.com/packaging/2010/07/nuspec.xsd' 네임스페이스의 'metadata' 요소에 잘못된 자식 요소가 있습니다."라는 오류 메시지가 발생할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="ca02a-175">If you installed packages built with a pre-release version of NuGet, you might encounter an error message stating "The element 'metadata' in namespace 'schemas.microsoft.com/packaging/2010/07/nuspec.xsd' has invalid child element" when running the RTM version of NuGet with that project.</span></span> <span data-ttu-id="ca02a-176">RTM 버전의 NuGet을 사용하여 각 패키지를 제거한 다음 다시 설치해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="ca02a-176">You need to uninstall and then re-install each package using the RTM version of NuGet.</span></span>

## <a name="attempting-to-install-or-uninstall-results-in-the-error-cannot-create-a-file-when-that-file-already-exists"></a><span data-ttu-id="ca02a-177">설치 또는 제거를 시도하면 “파일이 이미 있는 경우 해당 파일을 만들 수 없습니다.”라는 오류가 발생합니다.</span><span class="sxs-lookup"><span data-stu-id="ca02a-177">Attempting to install or uninstall results in the error "Cannot create a file when that file already exists."</span></span>

<span data-ttu-id="ca02a-178">어떤 이유로 Visual Studio 확장이 VSIX 확장을 제거한 이상한 상태가 될 수 있지만 일부 파일은 남아 있습니다.</span><span class="sxs-lookup"><span data-stu-id="ca02a-178">For some reason, Visual Studio extensions can get in a weird state where you've uninstalled the VSIX extension, but some files were left behind.</span></span> <span data-ttu-id="ca02a-179">이 문제를 해결하려면:</span><span class="sxs-lookup"><span data-stu-id="ca02a-179">To work around this issue:</span></span>

1. <span data-ttu-id="ca02a-180">Visual Studio 끝내기</span><span class="sxs-lookup"><span data-stu-id="ca02a-180">Exit Visual Studio</span></span>
1. <span data-ttu-id="ca02a-181">다음 폴더를 엽니다(컴퓨터의 다른 드라이브에 있을 수 있음).</span><span class="sxs-lookup"><span data-stu-id="ca02a-181">Open the following folder (it might be on a different drive on your machine)</span></span>

    <span data-ttu-id="ca02a-182">C:\Program Files (x86)\Microsoft Visual Studio 10.0\Common7\IDE\Extensions\Microsoft Corporation\NuGet Package Manager\<version>\\</span><span class="sxs-lookup"><span data-stu-id="ca02a-182">C:\Program Files (x86)\Microsoft Visual Studio 10.0\Common7\IDE\Extensions\Microsoft Corporation\NuGet Package Manager\<version>\\</span></span>

1. <span data-ttu-id="ca02a-183">*.deleteme* 확장명이 있는 파일을 모두 삭제합니다.</span><span class="sxs-lookup"><span data-stu-id="ca02a-183">Delete all the files with the *.deleteme* extensions.</span></span>
1. <span data-ttu-id="ca02a-184">Visual Studio를 다시 엽니다.</span><span class="sxs-lookup"><span data-stu-id="ca02a-184">Re-open Visual Studio</span></span>

<span data-ttu-id="ca02a-185">이러한 단계를 수행하면 계속 진행할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="ca02a-185">After following these steps, you should be able to continue.</span></span>

## <a name="in-rare-cases-compiling-with-code-analysis-turned-on-causes-error"></a><span data-ttu-id="ca02a-186">드문 경우이지만 코드 분석을 사용하여 컴파일하면 오류가 발생합니다.</span><span class="sxs-lookup"><span data-stu-id="ca02a-186">In rare cases, compiling with Code Analysis turned on causes error.</span></span>

<span data-ttu-id="ca02a-187">패키지 관리자 콘솔에서 FluentNHibernate를 설치한 다음 "코드 분석"을 설정한 상태에서 프로젝트를 컴파일하면 다음 오류가 발생할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="ca02a-187">You might get the following error if you installs FluentNHibernate with the Package Manager console and then compile your project with "Code Analysis" turned on.</span></span>

    Error 3 CA0058 : The referenced assembly
    'NHibernate, Version=3.0.0.2001, Culture=neutral, PublicKeyToken=aa95f207798dfdb4'
    could not be found. This assembly is required for analysis and was referenced by:
    C:\temp\Scratch\src\MyProject.UnitTests\bin\Debug\MyProject.UnitTests.dll.
    MyProject.UnitTests

<span data-ttu-id="ca02a-188">기본적으로 FluentNHibernate에는 NHibernate 3.0.0.2001이 필요합니다.</span><span class="sxs-lookup"><span data-stu-id="ca02a-188">By default, FluentNHibernate requires NHibernate 3.0.0.2001.</span></span> <span data-ttu-id="ca02a-189">그러나 NuGet은 계획적으로 프로젝트에 NHibernate 3.0.0.4000을 설치하고 적절한 바인딩 리디렉션을 추가하여 작동합니다.</span><span class="sxs-lookup"><span data-stu-id="ca02a-189">However, by design NuGet will install NHibernate 3.0.0.4000 in your project and add the appropriate binding redirects so that it will work.</span></span> <span data-ttu-id="ca02a-190">코드 분석이 설정되지 않으면 프로젝트가 문제 없이 컴파일됩니다.</span><span class="sxs-lookup"><span data-stu-id="ca02a-190">You project will compile just fine if code analysis is not turned on.</span></span> <span data-ttu-id="ca02a-191">컴파일러와 달리, 코드 분석 도구는 3.0.0.2001 대신 3.0.0.4000을 사용하는 바인딩 리디렉션을 제대로 따르지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="ca02a-191">In contrast to the compiler, code analysis tool doesn't properly follow the binding redirects to use 3.0.0.4000 instead of 3.0.0.2001.</span></span> <span data-ttu-id="ca02a-192">NHibernate 3.0.0.2001을 설치하여 이 문제를 해결하거나, 다음을 수행하여 컴파일러와 동일하게 동작하도록 코드 분석 도구에 지시할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="ca02a-192">You can work around the issue by either installing NHibernate 3.0.0.2001 or tell the code analysis tool to behave the same as the compiler by doing the following:</span></span>

1. <span data-ttu-id="ca02a-193">*%PROGRAMFILES%\Microsoft Visual Studio 10.0\Team Tools\Static Analysis Tools\FxCop*으로 이동합니다.</span><span class="sxs-lookup"><span data-stu-id="ca02a-193">Go to *%PROGRAMFILES%\Microsoft Visual Studio 10.0\Team Tools\Static Analysis Tools\FxCop*</span></span>
1. <span data-ttu-id="ca02a-194">FxCopCmd.exe.config를 열고 `AssemblyReferenceResolveMode`를 `StrongName`에서 `StrongNameIgnoringVersion`으로 변경합니다.</span><span class="sxs-lookup"><span data-stu-id="ca02a-194">Open FxCopCmd.exe.config and change `AssemblyReferenceResolveMode` from `StrongName` to `StrongNameIgnoringVersion`.</span></span>
1. <span data-ttu-id="ca02a-195">변경 내용을 저장하고 프로젝트를 다시 빌드합니다.</span><span class="sxs-lookup"><span data-stu-id="ca02a-195">Save the change and rebuild your project.</span></span>

## <a name="write-error-command-doesnt-work-inside-installps1uninstallps1initps1"></a><span data-ttu-id="ca02a-196">쓰기 오류 명령이 install.ps1/uninstall.ps1/init.ps1 내에서 작동하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="ca02a-196">Write-Error command doesn't work inside install.ps1/uninstall.ps1/init.ps1</span></span>

<span data-ttu-id="ca02a-197">이것은 알려진 문제입니다.</span><span class="sxs-lookup"><span data-stu-id="ca02a-197">This is a known issue.</span></span> <span data-ttu-id="ca02a-198">쓰기 오류를 호출하는 대신 throw 호출을 시도합니다.</span><span class="sxs-lookup"><span data-stu-id="ca02a-198">Instead of calling Write-Error, try calling throw.</span></span>

    throw "My error message"

## <a name="installing-nuget-with-restricted-access-on-windows-2003-can-crash-visual-studio"></a><span data-ttu-id="ca02a-199">Windows 2003에서 제한된 액세스 권한으로 NuGet을 설치하면 Visual Studio 작동이 중단될 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="ca02a-199">Installing NuGet with restricted access on Windows 2003 can crash Visual Studio</span></span>

<span data-ttu-id="ca02a-200">Visual Studio 확장 관리자를 사용하고 관리자 권한으로 실행하지 않는 NuGet을 설치하려고 하면, 기본적으로 &#8220;제한된 액세스 권한으로 이 프로그램 실행&#8221 확인란이 선택되어 있는 &#8220;다음 계정으로 실행&#8221 대화 상자가 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="ca02a-200">When attempting to install NuGet using the Visual Studio Extension Manager and not running as an administrator, the &#8220;Run As&#8221; dialog is displayed with the checkbox labeled &#8220;Run this program with restricted access&#8221; checked by default.</span></span>

![제한된 액세스 권한으로 실행 대화 상자](./media/RunAsRestricted.png)

<span data-ttu-id="ca02a-202">선택되어 있는 상태에서 [확인]을 클릭하면 Visual Studio 작동이 중단됩니다.</span><span class="sxs-lookup"><span data-stu-id="ca02a-202">Clicking OK with that checked crashes Visual Studio.</span></span> <span data-ttu-id="ca02a-203">NuGet을 설치하기 전에 해당 옵션을 선택 취소합니다.</span><span class="sxs-lookup"><span data-stu-id="ca02a-203">Make sure to uncheck that option before installing NuGet.</span></span>

## <a name="cannot-uninstall-nuget-for-windows-phone-tools"></a><span data-ttu-id="ca02a-204">Windows Phone 도구에 대한 NuGet을 제거할 수 없습니다.</span><span class="sxs-lookup"><span data-stu-id="ca02a-204">Cannot uninstall NuGet for Windows Phone Tools</span></span>

<span data-ttu-id="ca02a-205">Windows Phone 도구는 Visual Studio 확장 관리자를 지원하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="ca02a-205">Windows Phone Tools does not have support for the Visual Studio Extension Manager.</span></span> <span data-ttu-id="ca02a-206">NuGet을 제거하려면 다음 명령을 실행합니다.</span><span class="sxs-lookup"><span data-stu-id="ca02a-206">In order to uninstall NuGet, run the following command.</span></span>

     vsixinstaller.exe /uninstall:NuPackToolsVsix.Microsoft.67e54e40-0ae3-42c5-a949-fddf5739e7a5

## <a name="changing-the-capitalization-of-nuget-package-ids-breaks-package-restore"></a><span data-ttu-id="ca02a-207">NuGet 패키지 ID의 대/소문자를 변경하면 패키지 복원이 중단됩니다.</span><span class="sxs-lookup"><span data-stu-id="ca02a-207">Changing the capitalization of NuGet package IDs breaks package restore</span></span>

<span data-ttu-id="ca02a-208">[이 GitHub 문제](https://github.com/Particular/NServiceBus/issues/1271#issuecomment-20865932)에서 설명한 대로, NuGet 패키지의 대문자 표시 변경은 NuGet 지원을 통해 수행할 수 있지만, 패키지를 복원하는 동안 로컬 패키지 캐시에서 대/소문자를 다르게 사용한 기존 패키지가 있는 사용자에 대한 복잡성이 발생합니다 .</span><span class="sxs-lookup"><span data-stu-id="ca02a-208">As discussed at length on [this GitHub issue](https://github.com/Particular/NServiceBus/issues/1271#issuecomment-20865932), changing the capitalization of NuGet packages can be done by NuGet support, but causes complications during package restore for users who have existing, differently-cased, packages in their local package cache.</span></span> <span data-ttu-id="ca02a-209">빌드 시간 패키지 복원에 발생할 수 있는 중단에 대해 패키지의 기존 사용자와 통신할 수 있는 경우에만 대/소문자 변경을 요청하는 것이 좋습니다.</span><span class="sxs-lookup"><span data-stu-id="ca02a-209">We recommend only requesting a case change when you have a way to communicate with existing users of your package about the break that may occur to their build-time package restore.</span></span>

## <a name="reporting-issues"></a><span data-ttu-id="ca02a-210">문제 보고</span><span class="sxs-lookup"><span data-stu-id="ca02a-210">Reporting issues</span></span>

<span data-ttu-id="ca02a-211">NuGet 문제를 보고하려면 [https://github.com/nuget/home/issues](https://github.com/nuget/home/issues)를 방문하세요.</span><span class="sxs-lookup"><span data-stu-id="ca02a-211">To report NuGet issues, visit [https://github.com/nuget/home/issues](https://github.com/nuget/home/issues).</span></span>
