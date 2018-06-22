---
title: 알려진 문제
description: 인증, 패키지 설치 및 도구를 포함하여 알려진 NuGet 관련 문제입니다.
author: karann-msft
ms.author: karann
manager: unnir
ms.date: 11/11/2016
ms.topic: conceptual
ms.openlocfilehash: 1f170f377a3394694e953a794f2c814388656c21
ms.sourcegitcommit: 3eab9c4dd41ea7ccd2c28bb5ab16f6fbbec13708
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/26/2018
ms.locfileid: "31822021"
---
# <a name="known-issues-with-nuget"></a>알려진 NuGet 문제

반복적으로 보고되어 가장 일반적으로 알려진 NuGet 관련 문제입니다. NuGet을 설치하거나 패키지를 관리하는 데 문제가 있는 경우 이러한 알려진 문제와 해결 방법을 살펴보세요.

> [!Note]
> NuGet 4.0부터 알려진 문제는 각 릴리스 정보의 일부가 됩니다.

## <a name="authentication-issues-with-nuget-feeds-in-vsts-with-nugetexe-v343"></a>VSTS에서 nuget.exe v3.4.3을 통한 NuGet 피드 인증 문제

**문제:**

다음 명령을 사용하여 자격 증명을 저장하면 개인 액세스 토큰을 이중으로 암호화합니다.

$PAT = "개인 액세스 토큰" $Feed = "URL" .\nuget.exe sources add -Name Test -Source $Feed -UserName $UserName -Password $PAT

**해결 방법:**

[-StorePasswordInClearText](../tools/cli-ref-sources.md) 옵션을 사용하여 암호를 일반 텍스트로 저장합니다.

## <a name="error-installing-packages-with-nuget-34-341"></a>NuGet 3.4, 3.4.1 패키지 설치 오류

**문제:**

NuGet 3.4 및 3.4.1에서 NuGet 추가 기능을 사용하면 사용 가능한 원본이 보고되지 않으며 구성 창에서 새 원본을 추가할 수 없습니다. 결과는 아래 이미지와 비슷합니다.

![원본이 없는 NuGet config 파일](./media/knownIssue-34-NoSources.PNG)

`%AppData%\NuGet\`(Windows) 또는 `~/.nuget/`(Mac/Linux) 폴더에 있는 `NuGet.Config` 파일이 실수로 비어 있습니다. 이 문제를 해결하려면 Visual Studio(Windows에서 해당하는 경우)를 닫고 `NuGet.Config` 파일을 삭제하고 작업을 다시 시도해 봅니다. NuGet이 새 `NuGet.Config`를 생성한 후에 계속할 수 있습니다.

## <a name="error-installing-packages-with-nuget-27"></a>NuGet 2.7 패키지 설치 오류

**문제:**

NuGet 2.7 이상에서 어셈블리 참조가 포함된 패키지를 설치하려고 하면 아래와 같이 **"입력 문자열의 형식이 잘못되었습니다."** 라는 오류 메시지가 표시될 수 있습니다.

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

`VSLangProj.dll` COM 구성 요소에 대한 형식 라이브러리가 시스템에서 등록 취소되었기 때문에 이 오류가 발생합니다. 예를 들어 두 버전의 Visual Studio가 나란히 설치되어 있고 이전 버전을 제거하면 이 문제가 발생할 수 있습니다. 이렇게 하면 위의 COM 라이브러리를 실수로 등록 취소할 수 있습니다.

**해결 방법:**:

**관리자 권한 프롬프트에서**에서 다음 명령을 실행하여 `VSLangProj.dll`에 대한 형식 라이브러리를 다시 등록합니다.

    regsvr32 "C:\Program Files (x86)\Common Files\microsoft shared\MSEnv\VsLangproj.olb"

명령이 실패하면 해당 위치에 파일이 있는지 확인합니다.

이 오류에 대한 자세한 내용은 이 [작업 항목](https://nuget.codeplex.com/workitem/3609 "작업 항목 3609")를 참조하세요.

## <a name="build-failure-after-package-update-in-vs-2012"></a>VS 2012에서 패키지를 업데이트한 후에 빌드가 실패합니다.

문제: VS 2012 RTM을 사용하고 있습니다. NuGet 패키지를 업데이트할 때 "하나 이상의 패키지를 제거할 수 없습니다."라는 메시지가 표시됩니다. 그리고 Visual Studio를 다시 시작하라는 메시지가 표시됩니다. 이에 따라 VS를 다시 시작하면 이상한 빌드 오류가 발생합니다.

이는 이전 패키지의 특정 파일이 백그라운드 MSBuild 프로세스에서 잠겨 있기 때문입니다. VS를 다시 시작한 후에도 백그라운드 MSBuild 프로세스에서 이전 패키지의 파일을 계속 사용함으로써 빌드가 실패합니다.

이를 수정하려면 VS 2012 업데이트(예: VS 2012 업데이트 2)를 설치합니다.

## <a name="upgrading-to-latest-nuget-from-an-older-version-causes-a-signature-verification-error"></a>이전 버전에서 최신 NuGet으로 업그레이드하면 서명 확인 오류가 발생합니다.

VS 2010 SP1을 실행하는 경우 설치되어 있는 이전 버전의 NuGet을 업그레이드하려고 할 때 다음과 같은 오류 메시지가 표시될 수 있습니다.

![Visual Studio 확장 설치 관리자](./media/Visual-Studio-Extension-Installer.png)

로그를 볼 때 `SignatureMismatchException`에 대한 언급이 표시될 수 있습니다.

이 문제가 발생하지 않도록 하기 위해 [Visual Studio 2010 SP1 핫픽스](http://bit.ly/vsixcertfix)를 설치할 수 있습니다.
또는 Visual Studio를 관리자 권한으로 실행하여 NuGet을 제거한 다음 VS 확장 갤러리에서 설치하기만 하면 됩니다.  자세한 내용은 [http://support.microsoft.com/kb/2581019](http://support.microsoft.com/kb/2581019)를 참조하세요.

## <a name="package-manager-console-throws-an-exception-when-the-reflector-visual-studio-add-in-is-also-installed"></a>리플렉터 Visual Studio 추가 기능이 설치되면 패키지 관리자 콘솔에서 예외가 발생합니다.

패키지 관리자 콘솔을 실행할 때 리플렉터 VS 추가 기능이 설치되면 다음과 같은 예외 메시지가 표시될 수 있습니다.

    The following error occurred while loading the extended type data file:
    Microsoft.PowerShell.Core, C:\Windows\SysWOW64\WindowsPowerShell\v1.0\types.ps1xml(2950) :
    Error in type "System.Security.AccessControl.ObjectSecurity":
    Exception: Cannot convert the "Microsoft.PowerShell.Commands.SecurityDescriptorCommandsBase"
    value of type "System.String" to type "System.Type".
    System.Management.Automation.ActionPreferenceStopException:
    Command execution stopped because the preference variable "ErrorActionPreference" or common parameter
    is set to Stop: Unable to find type

또는

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

문제를 해결하기 위해 추가 기능 작성자에게 연락했습니다.

<p class="info">업데이트: 최신 버전인 리플렉터 6.5를 사용하면 더 이상 콘솔에서 이 예외가 발생하지 않음을 확인했습니다.</p>

## <a name="opening-package-manager-console-fails-with-objectsecurity-exception"></a>ObjectSecurity 예외로 인해 패키지 관리자 콘솔 열기가 실패합니다.

패키지 관리자 콘솔을 열려고 할 때 다음과 같은 오류가 표시될 수 있습니다.

    The following error occurred while loading the extended type data file: Microsoft.PowerShell.Core, C:\Windows\SysWOW64\WindowsPowerShell\v1.0\types.ps1xml(2977) : Error in type "System.Security.AccessControl.ObjectSecurity": Exception: The getter method should be public, non void, static, and have one parameter of type PSObject.
    The following error occurred while loading the extended type data file: Microsoft.PowerShell.Core, C:\Windows\SysWOW64\WindowsPowerShell\v1.0\types.ps1xml(2984) : Error in type "System.Security.AccessControl.ObjectSecurity": Exception: The getter method should be public, non void, static, and have one parameter of type PSObject.
    The following error occurred while loading the extended type data file: Microsoft.PowerShell.Core, C:\Windows\SysWOW64\WindowsPowerShell\v1.0\types.ps1xml(2991) : Error in type "System.Security.AccessControl.ObjectSecurity": Exception: The getter method should be public, non void, static, and have one parameter of type PSObject.
    The following error occurred while loading the extended type data file: Microsoft.PowerShell.Core, C:\Windows\SysWOW64\WindowsPowerShell\v1.0\types.ps1xml(2998) : Error in type "System.Security.AccessControl.ObjectSecurity": Exception: The getter method should be public, non void, static, and have one parameter of type PSObject.
    The following error occurred while loading the extended type data file: Microsoft.PowerShell.Core, C:\Windows\SysWOW64\WindowsPowerShell\v1.0\types.ps1xml(3005) : Error in type "System.Security.AccessControl.ObjectSecurity": Exception: The getter method should be public, non void, static, and have one parameter of type PSObject.
    The term 'Get-ExecutionPolicy' is not recognized as the name of a cmdlet, function, script file, or operable program. Check the spelling of the name, or if a path was included, verify that the path is correct and try again.

이 경우 [StackOverflow에서 설명](http://stackoverflow.com/questions/12638289/embedding-powershell-v2-0-in-net-app-on-windows-8-rtm)한 해결 방법에 따라 수정합니다.

## <a name="the-add-package-library-reference-dialog-throws-an-exception-if-the-solution-contains-installshield-limited-edition-project"></a>솔루션에 InstallShield Limited Edition 프로젝트가 포함된 경우 패키지 라이브러리 참조 추가 대화 상자에서 예외를 throw합니다.

솔루션에 하나 이상의 InstallShield Limited Edition 프로젝트가 포함되어 있으면 **패키지 라이브러리 참조 추가** 대화 상자가 열릴 때 예외를 throw한다는 것을 확인했습니다. 현재 InstallShield 프로젝트를 제거하거나 언로드하는 것을 제외하고는 아직 해결 방법이 없습니다.

## <a name="uninstall-button-greyed-out-nuget-requires-admin-privileges-to-installuninstall"></a>제거 단추가 회색으로 표시되나요? NuGet을 설치/제거하려면 관리자 권한이 필요합니다.

Visual Studio 확장 관리자를 통해 NuGet을 제거하려고 하면 [제거] 단추가 비활성화되어 있습니다. NuGet을 설치/제거하려면 관리자 권한이 필요합니다. Visual Studio를 관리자 권한으로 다시 시작하여 확장을 제거합니다. 관리자 액세스를 통해 NuGet을 사용할 필요가 없습니다.

## <a name="the-package-manager-console-crashes-when-i-open-it-in-windows-xp-whats-wrong"></a>Windows XP에서 패키지 관리자 콘솔을 열면 패키지 관리자 콘솔 작동이 중단됩니다. 무엇이 문제인가요?

NuGet에는 Powershell 2.0 런타임이 필요합니다. Windows XP에는 기본적으로 Powershell 2.0이 없습니다. [http://support.microsoft.com/kb/968929](http://support.microsoft.com/kb/968929)에서 Powershell 2.0 런타임을 다운로드할 수 있습니다. 설치한 후에 Visual Studio를 다시 시작하면 패키지 관리자 콘솔을 열 수 있습니다.

## <a name="visual-studio-2010-sp1-beta-crashes-on-exit-if-the-package-manager-console-is-open"></a>패키지 관리자 콘솔이 열려 있으면 종료 시 Visual Studio 2010 SP1 베타가 충돌합니다.

Visual Studio 2010 SP1 베타를 설치한 경우 패키지 관리자 콘솔을 열어 놓은 채 Visual Studio를 닫으면 충돌이 발생할 수 있습니다. 이는 알려진 Visual Studio 문제이며 SP1 RTM 릴리스에서 수정될 예정입니다. 현재는 이 충돌을 무시하거나 가능한 경우 SP1 베타를 제거합니다.

## <a name="the-element-metadata--has-invalid-child-element-exception-occurs"></a>"'metadata' 요소에 잘못된 자식 요소가 있습니다."라는 예외가 발생했습니다.

NuGet 시험판 버전으로 빌드된 패키지를 설치한 경우 해당 프로젝트를 사용하여 RTM 버전의 NuGet을 실행할 때 "'schemas.microsoft.com/packaging/2010/07/nuspec.xsd' 네임스페이스의 'metadata' 요소에 잘못된 자식 요소가 있습니다."라는 오류 메시지가 발생할 수 있습니다. RTM 버전의 NuGet을 사용하여 각 패키지를 제거한 다음 다시 설치해야 합니다.

## <a name="attempting-to-install-or-uninstall-results-in-the-error-cannot-create-a-file-when-that-file-already-exists"></a>설치 또는 제거를 시도하면 “파일이 이미 있는 경우 해당 파일을 만들 수 없습니다.”라는 오류가 발생합니다.

어떤 이유로 Visual Studio 확장이 VSIX 확장을 제거한 이상한 상태가 될 수 있지만 일부 파일은 남아 있습니다. 이 문제를 해결하려면:

1. Visual Studio 끝내기
1. 다음 폴더를 엽니다(컴퓨터의 다른 드라이브에 있을 수 있음).

    C:\Program Files (x86)\Microsoft Visual Studio 10.0\Common7\IDE\Extensions\Microsoft Corporation\NuGet Package Manager\<version>\

1. *.deleteme* 확장명이 있는 파일을 모두 삭제합니다.
1. Visual Studio를 다시 엽니다.

이러한 단계를 수행하면 계속 진행할 수 있습니다.

## <a name="in-rare-cases-compiling-with-code-analysis-turned-on-causes-error"></a>드문 경우이지만 코드 분석을 사용하여 컴파일하면 오류가 발생합니다.

패키지 관리자 콘솔에서 FluentNHibernate를 설치한 다음 "코드 분석"을 설정한 상태에서 프로젝트를 컴파일하면 다음 오류가 발생할 수 있습니다.

    Error 3 CA0058 : The referenced assembly
    'NHibernate, Version=3.0.0.2001, Culture=neutral, PublicKeyToken=aa95f207798dfdb4'
    could not be found. This assembly is required for analysis and was referenced by:
    C:\temp\Scratch\src\MyProject.UnitTests\bin\Debug\MyProject.UnitTests.dll.
    MyProject.UnitTests

기본적으로 FluentNHibernate에는 NHibernate 3.0.0.2001이 필요합니다. 그러나 NuGet은 계획적으로 프로젝트에 NHibernate 3.0.0.4000을 설치하고 적절한 바인딩 리디렉션을 추가하여 작동합니다. 코드 분석이 설정되지 않으면 프로젝트가 문제 없이 컴파일됩니다. 컴파일러와 달리, 코드 분석 도구는 3.0.0.2001 대신 3.0.0.4000을 사용하는 바인딩 리디렉션을 제대로 따르지 않습니다. NHibernate 3.0.0.2001을 설치하여 이 문제를 해결하거나, 다음을 수행하여 컴파일러와 동일하게 동작하도록 코드 분석 도구에 지시할 수 있습니다.

1. *%PROGRAMFILES%\Microsoft Visual Studio 10.0\Team Tools\Static Analysis Tools\FxCop*으로 이동합니다.
1. FxCopCmd.exe.config를 열고 `AssemblyReferenceResolveMode`를 `StrongName`에서 `StrongNameIgnoringVersion`으로 변경합니다.
1. 변경 내용을 저장하고 프로젝트를 다시 빌드합니다.

## <a name="write-error-command-doesnt-work-inside-installps1uninstallps1initps1"></a>쓰기 오류 명령이 install.ps1/uninstall.ps1/init.ps1 내에서 작동하지 않습니다.

이것은 알려진 문제입니다. 쓰기 오류를 호출하는 대신 throw 호출을 시도합니다.

    throw "My error message"

## <a name="installing-nuget-with-restricted-access-on-windows-2003-can-crash-visual-studio"></a>Windows 2003에서 제한된 액세스 권한으로 NuGet을 설치하면 Visual Studio 작동이 중단될 수 있습니다.

Visual Studio 확장 관리자를 사용하고 관리자 권한으로 실행하지 않는 NuGet을 설치하려고 하면, 기본적으로 &#8220;제한된 액세스 권한으로 이 프로그램 실행&#8221 확인란이 선택되어 있는 &#8220;다음 계정으로 실행&#8221 대화 상자가 표시됩니다.

![제한된 액세스 권한으로 실행 대화 상자](./media/RunAsRestricted.png)

선택되어 있는 상태에서 [확인]을 클릭하면 Visual Studio 작동이 중단됩니다. NuGet을 설치하기 전에 해당 옵션을 선택 취소합니다.

## <a name="cannot-uninstall-nuget-for-windows-phone-tools"></a>Windows Phone 도구에 대한 NuGet을 제거할 수 없습니다.

Windows Phone 도구는 Visual Studio 확장 관리자를 지원하지 않습니다. NuGet을 제거하려면 다음 명령을 실행합니다.

     vsixinstaller.exe /uninstall:NuPackToolsVsix.Microsoft.67e54e40-0ae3-42c5-a949-fddf5739e7a5

## <a name="changing-the-capitalization-of-nuget-package-ids-breaks-package-restore"></a>NuGet 패키지 ID의 대/소문자를 변경하면 패키지 복원이 중단됩니다.

[이 GitHub 문제](https://github.com/Particular/NServiceBus/issues/1271#issuecomment-20865932)에서 설명한 대로, NuGet 패키지의 대문자 표시 변경은 NuGet 지원을 통해 수행할 수 있지만, 패키지를 복원하는 동안 *global-packages* 폴더에서 대/소문자를 다르게 사용한 기존 패키지가 있는 사용자에 대한 복잡성이 발생합니다. 빌드 시간 패키지 복원에 발생할 수 있는 중단에 대해 패키지의 기존 사용자와 통신할 수 있는 경우에만 대/소문자 변경을 요청하는 것이 좋습니다.

## <a name="reporting-issues"></a>문제 보고

NuGet 문제를 보고하려면 [https://github.com/nuget/home/issues](https://github.com/nuget/home/issues)를 방문하세요.
