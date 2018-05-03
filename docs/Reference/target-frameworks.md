---
title: NuGet에 대 한 대상 프레임 워크 참조
description: NuGet 대상 프레임워크 참조는 패키지의 프레임워크 종속 구성 요소를 식별하고 격리합니다.
author: kraigb
ms.author: kraigb
manager: douge
ms.date: 12/11/2017
ms.topic: reference
ms.reviewer: anangaur
ms.openlocfilehash: 6b7ee3f739847777dda638d8fed083c48ed5812e
ms.sourcegitcommit: a6ca160b1e7e5c58b135af4eba0e9463127a59e8
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/28/2018
---
# <a name="target-frameworks"></a>대상 프레임워크

NuGet은 다양한 위치에서 대상 프레임워크 참조를 사용하여 패키지의 프레임워크 종속 구성 요소를 구체적으로 식별하고 격리합니다.

- [.nuspec 매니페스트](../reference/nuspec.md): 패키지는 프로젝트의 대상 프레임워크에 따라 프로젝트에 포함될 고유한 패키지를 나타낼 수 있습니다.
- [.nupkg 폴더 이름](../create-packages/creating-a-package.md#from-a-convention-based-working-directory): 패키지의 `lib` 폴더 내에 있는 폴더는 대상 프레임워크에 따라 이름을 지정할 수 있으며, 각 폴더에는 해당 프레임워크에 적합한 DLL 및 다른 콘텐츠가 포함됩니다.
- [packages.config](../reference/packages-config.md): 종속성의 `targetframework` 특성은 설치할 패키지의 변형을 지정합니다.

> [!Note]
> 아래 표를 계산하는 NuGet 클라이언트 소스 코드는 다음 위치에 있습니다.
> - 지원되는 프레임워크 이름: [FrameworkConstants.cs](https://github.com/NuGet/NuGet.Client/blob/dev/src/NuGet.Core/NuGet.Frameworks/FrameworkConstants.cs)
> - 프레임워크 우선 순위 및 매핑: [DefaultFrameworkMappings.cs](https://github.com/NuGet/NuGet.Client/blob/dev/src/NuGet.Core/NuGet.Frameworks/DefaultFrameworkMappings.cs)

## <a name="supported-frameworks"></a>지원되는 프레임워크

프레임워크는 일반적으로 짧은 대상 프레임워크 모니커 또는 TFM에서 참조됩니다. .NET Standard에서 이 프레임워크는 *TxM*으로 일반화되어 여러 프레임워크에 대한 단일 참조를 허용합니다.

NuGet 클라이언트는 아래 표의 프레임워크를 지원합니다. 대괄호([]) 안에 표시된 항목은 동등한 항목입니다. `dotnet`과 같은 일부 도구는 일부 파일에서 정식 TFM의 변형을 사용할 수 있습니다. 예를 들어 `dotnet pack`은 `.nuspec` 파일에서 `netcoreapp2.0` 대신 `.NETCoreApp2.0`을 사용합니다. 다양한 NuGet 클라이언트 도구에서 이러한 변형을 적절하게 처리하지만, 파일을 직접 편집할 때는 항상 정식 TFM을 사용해야 합니다.

| 이름 | 약어 | TFM/TxM |
| ------------- | ------------ | --------- |
|.NET Framework | net | net11 |
| | | net20 |
| | | net35 |
| | | net40 |
| | | net403 |
| | | net45 |
| | | net451 |
| | | net452 |
| | | net46 |
| | | net461 |
| | | net462 |
|Microsoft Store(Windows 스토어) | netcore | netcore [netcore45] |
| | | netcore45 [win, win8] |
| | | netcore451 [win81] |
| | | netcore50 |
|.NET MicroFramework | netmf | netmf |
|Windows | win | win [win8, netcore45] |
| | | win8 [netcore45, win] |
| | | win81 [netcore451] |
| | | win10(Windows 10 플랫폼에서 지원되지 않음) |
Silverlight | sl | sl4 |
| | | sl5 |
Windows Phone(SL) | wp | wp [wp7] |
| | | wp7 |
| | | wp75 |
| | | wp8 |
| | | wp81 |
Windows Phone(UWP) | | wpa81 |
유니버설 Windows 플랫폼 | uap | uap [uap10.0] |
| | | uap10.0 |
.NET Standard | netstandard | netstandard1.0 |
| | | netstandard1.1 |
| | | netstandard1.2 |
| | | netstandard1.3 |
| | | netstandard1.4 |
| | | netstandard1.5 |
| | | netstandard1.6 |
| | | netstandard2.0 |
.NET Core 앱 | netcoreapp | netcoreapp1.0 |
| | | netcoreapp1.1 |
| | | netcoreapp2.0 |
Tizen | tizen | tizen3 |
| | | tizen4 |

## <a name="deprecated-frameworks"></a>사용되지 않는 프레임워크

다음 프레임워크는 사용되지 않습니다. 이러한 프레임워크를 대상으로 하는 패키지는 지정된 대체 항목으로 마이그레이션되어야 합니다.

| 사용되지 않는 프레임워크 | Replacement
| --- | ---
| aspnet50 | netcoreapp |
| aspnetcore50 |
| dnxcore50 |
| dnx |
| dnx45 |
| dnx451 |
| dnx452 |
| dotnet | netstandard |
| dotnet50 | |
| dotnet51 | |
| dotnet52 | |
| dotnet53 | |
| dotnet54 | |
| dotnet55 | |
| dotnet56 | |
| winrt | win |

## <a name="precedence"></a>우선 순위

많은 프레임워크가 서로 관련되고 호환되지만 반드시 동등한 것은 아닙니다.

| 프레임워크 | 사용 가능 |
| -- | --- |
| uap(유니버설 Windows 플랫폼) | win81 |
| | wpa81 |
| | netcore50 |
| win(Microsoft Store) | winrt |
| | |

## <a name="net-platform-standard"></a>.NET 플랫폼 표준

[.NET 플랫폼 표준](https://github.com/dotnet/corefx/blob/master/Documentation/architecture/net-platform-standard.md)은 이진 호환 가능 프레임워크 간의 참조를 간소화하여 단일 대상 프레임워크가 다른 프레임워크의 조합을 참조할 수 있게 합니다. (배경 지식에 대한 자세한 내용은 [.NET 입문서](/dotnet/articles/standard/index)를 참조하세요.)

[NuGet Get Nearest Framework 도구](https://aka.ms/s2m3th)는 NuGet에서 프로젝트 프레임워크에 따라 패키지에서 사용할 수 있는 많은 프레임워크 자산 중에서 하나의 프레임워크를 선택하는 데 사용하는 것을 시뮬레이션합니다.

모니커의 `dotnet` 계열은 NuGet 3.3 및 이전 버전에서 사용해야 하고, `netstandard` 모니커 구문은 v3.4 이상에서 사용해야 합니다.

## <a name="portable-class-libraries"></a>이식 가능한 클래스 라이브러리

> [!Warning]
> **PCL은 권장되지 않습니다**. PCL이 지원되지만 패키지 작성자는 netstandard를 대신 지원해야 합니다. .NET 플랫폼 표준을 PCLs 발전 하 고 같은 정적 라이브러리에 연결 되지 않은 단일 모니커를 사용 하 여 플랫폼 간에 이식 나타냅니다 *휴대용-a + b + c* 모니커 합니다.

여러 자식 대상 프레임워크를 참조하는 대상 프레임워크를 정의하려면 `portable` 키워드를 사용하여 참조된 프레임워크 목록의 접두사로 지정합니다. 이러한 프레임워크에서 의도하지 않은 부작용이 발생할 수 있으므로 직접 컴파일되지 않은 추가 프레임워크를 인위적으로 포함하지 않습니다.

타사에서 정의한 추가 프레임워크는 이러한 방식으로 액세스할 수 있는 다른 환경과의 호환성을 제공합니다. 또한 관련 프레임워크의 이러한 조합을 `Profile#`으로 참조할 수 있는 약식 프로필 번호가 있지만 폴더 및 `.nuspec`의 가독성을 떨어뜨리기 때문에 이러한 번호를 사용하지 않는 것이 좋습니다.

| Profile# | 프레임워크 | 전체 이름 | .NET Standard |
 --- | --- | --- | ---
 Profile2 | .NETFramework 4.0 | portable-net40+win8+sl4+wp7 |
 | | Windows 8.0 | |
 | | Silverlight 4.0 |
 | | WindowsPhone 7.0|
 Profile3 | .NETFramework 4.0 | portable-net40+sl4
 | | Silverlight 4.0 |
 Profile4 | .NETFramework 4.5 | portable-net45+sl4+win8+wp7
 | | Silverlight 4.0 |
 | | Windows 8.0 |
 | | WindowsPhone 7.0 |
 Profile5 | .NETFramework 4.0 | portable-net40+win8
 | | Windows 8.0 |
 Profile6 | .NETFramework 4.0.3 | portable-net403+win8
 | | Windows 8.0 |
 Profile7 | .NETFramework 4.5 | portable-net45+win8 | netstandard1.1
 | | Windows 8.0 |
 Profile14 | .NETFramework 4.0 | portable-net40+sl5
 | | Silverlight 5.0 |
 Profile18 | .NETFramework 4.0.3 | portable-net403+sl4
 | | Silverlight 4.0 |
 Profile19 | .NETFramework 4.0.3 | portable-net403+sl5
 | | Silverlight 5.0 |
 Profile23 | .NETFramework 4.5 | portable-net45+sl4
 | | Silverlight 4.0 |
 Profile24 | .NETFramework 4.5 | portable-net45+sl5
 | | Silverlight 5.0 |
 Profile31 | Windows 8.1 | portable-win81+wp81 | netstandard1.0
 | | WindowsPhone 8.1(SL) |
 Profile32 | Windows 8.1 | portable-win81+wpa81 | netstandard1.2
 | | WindowsPhone 8.1(UWP) |
 Profile36 | .NETFramework 4.0 | portable-net40+sl4+win8+wp8
 | | Silverlight 4.0 |
 | | Windows 8.0 |
 | | WindowsPhone 8.0(SL) |
 Profile37 | .NETFramework 4.0 | portable-net40+sl5+win8
 | | Silverlight 5.0 |
 | | Windows 8.0 |
 Profile41 | .NETFramework 4.0.3 | portable-net403+sl4+win8
 | | Silverlight 4.0 |
 | | Windows 8.0 |
 Profile42 | .NETFramework 4.0.3 | portable-net403+sl5+win8
 | | Silverlight 5.0 |
 | | Windows 8.0 |
 Profile44 | .NETFramework 4.5.1 | portable-net451+win81 | netstandard1.2
 | | Windows 8.1 |
 Profile46 | .NETFramework 4.5 | portable-net45+sl4+win8
 | | Silverlight 4.0 |
 | | Windows 8.0 |
 Profile47 | .NETFramework 4.5 | portable-net45+sl5+win8
 | | Silverlight 5.0 |
 | | Windows 8.0 |
 Profile49 | .NETFramework 4.5 | portable-net45+wp8 | netstandard1.0
 | | WindowsPhone 8.0(SL) |
 Profile78 | .NETFramework 4.5 | portable-net45+win8+wp8 | netstandard1.0
 | | Windows 8.0 |
 | | WindowsPhone 8.0(SL) |
 Profile84 | WindowsPhone 8.1 | portable-wp81+wpa81 | netstandard1.0
 | | WindowsPhone 8.1(UWP) |
 Profile88 | .NETFramework 4.0 | portable-net40+sl4+win8+wp75
 | | Silverlight 4.0 |
 | | Windows 8.0 |
 | | WindowsPhone 7.5 |
 Profile92 | .NETFramework 4.0 | portable-net40+win8+wpa81
 | | Windows 8.0 |
 | | WindowsPhone 8.1(UWP) |
 Profile95 | .NETFramework 4.0.3 | portable-net403+sl4+win8+wp7
 | | Silverlight 4.0 |
 | | Windows 8.0 |
 | | WindowsPhone 7.0 |
 Profile96 | .NETFramework 4.0.3 | portable-net403+sl4+win8+wp75
 | | Silverlight 4.0 |
 | | Windows 8.0 |
 | | WindowsPhone 7.5 |
 Profile102 | .NETFramework 4.0.3 | portable-net403+win8+wpa81
 | | Windows 8.0 |
 | | WindowsPhone 8.1(UWP) |
 Profile104 | .NETFramework 4.5 | portable-net45+sl4+win8+wp75
 | | Silverlight 4.0 |
 | | Windows 8.0 |
 | | WindowsPhone 7.5 |
 Profile111 | .NETFramework 4.5 | portable-net45+win8+wpa81 | netstandard1.1
 | | Windows 8.0 |
 | | WindowsPhone 8.1(UWP) |
 Profile136 | .NETFramework 4.0 | portable-net40+sl5+win8+wp8
 | | Silverlight 5.0 |
 | | Windows 8.0 |
 | | WindowsPhone 8.0(SL) |
 Profile143 | .NETFramework 4.0.3 | portable-net403+sl4+win8+wp8
 | | Silverlight 4.0 |
 | | Windows 8.0 |
 | | WindowsPhone 8.0(SL) |
 Profile147 | .NETFramework 4.0.3 | portable-net403+sl5+win8+wp8
 | | Silverlight 5.0 |
 | | Windows 8.0 |
 | | WindowsPhone 8.0(SL) |
 Profile151 | NETFramework 4.5.1 | portable-net451+win81+wpa81 | netstandard1.2
 | | Windows 8.1 |
 | | WindowsPhone 8.1(UWP) |
 Profile154 | .NETFramework 4.5 | portable-net45+sl4+win8+wp8
 | | Silverlight 4.0 |
 | | Windows 8.0 |
 | | WindowsPhone 8.0(SL) |
 Profile157 | Windows 8.1 | portable-win81+wp81+wpa81 | netstandard1.0
 | | WindowsPhone 8.1(SL) |
 | | WindowsPhone 8.1(UWP) |
 Profile158 | .NETFramework 4.5 | portable-net45+sl5+win8+wp8
 | | Silverlight 5.0 |
 | | Windows 8.0 |
 | | WindowsPhone 8.0(SL) |
 Profile225 | .NETFramework 4.0 | portable-net40+sl5+win8+wpa81
 | | Silverlight 5.0 |
 | | Windows 8.0 |
 | | WindowsPhone 8.1(UWP) |
 Profile240 | .NETFramework 4.0.3 | portable-net403+sl5+win8+wpa8
 | | Silverlight 5.0 |
 | | Windows 8.0 |
 | | WindowsPhone 8.1(UWP) |
 Profile255 | .NETFramework 4.5 | portable-net45+sl5+win8+wpa81
 | | Silverlight 5.0 |
 | | Windows 8.0 |
 | | WindowsPhone 8.1(UWP) |
 Profile259 | .NETFramework 4.5 | portable-net45+win8+wpa81+wp8 | netstandard1.0
 | | Windows 8.0 |
 | | WindowsPhone 8.1(UWP) |
 | | WindowsPhone 8.0(SL) |
 Profile328 | .NETFramework 4.0 | portable-net40+sl5+win8+wpa81+wp8
 | | Silverlight 5.0 |
 | | Windows 8.0 |
 | | WindowsPhone 8.1(UWP) |
 | | WindowsPhone 8.0(SL) |
 Profile336 | .NETFramework 4.0.3 | portable-net403+sl5+win8+wpa81+wp8
 | | Silverlight 5.0 |
 | | Windows 8.0 |
 | | WindowsPhone 8.1(UWP) |
 | | WindowsPhone 8.0(SL) |
 Profile344 | .NETFramework 4.5 | portable-net45+sl5+win8+wpa81+wp8
 | | Silverlight 5.0 |
 | | Windows 8.0 |
 | | WindowsPhone 8.1(UWP) |
 | | WindowsPhone 8.0(SL) |

또한 Xamarin을 대상으로 하는 NuGet 패키지는 Xamarin에서 정의한 추가 프레임워크를 사용할 수 있습니다. [Xamarin에 대한 NuGet 패키지 만들기](https://developer.xamarin.com/guides/cross-platform/advanced/nuget/)를 참조하세요.

| 이름 | 설명 | .NET Standard |
| --- | --- | ---
| monoandroid | Android OS에 대한 Mono 지원 | netstandard1.4 |
| monotouch | iOS에 대한 Mono 지원 | netstandard1.4 |
| monomac | OSX에 대한 Mono 지원 | netstandard1.4 |
| xamarinios | iOS용 Xamarin에 대한 지원 | netstandard1.4 |
| xamarinmac | Mac용 Xamarin에 대한 지원 | netstandard1.4 |
| xamarinpsthree | Playstation 3에서 Xamarin에 대한 지원 | netstandard1.4 |
| xamarinpsfour | Playstation 4에서 Xamarin에 대한 지원 | netstandard1.4 |
| xamarinpsvita | PS Vita에서 Xamarin에 대한 지원 | netstandard1.4 |
| xamarinwatchos | Watch OS용 Xamarin | netstandard1.4 |
| xamarintvos | TV OS용 Xamarin | netstandard1.4 |
| xamarinxboxthreesixty | XBox 360용 Xamarin | netstandard1.4 |
| xamarinxboxone | XBox One용 Xamarin | netstandard1.4 |

> [!Note]
> Stephen Cleary가 지원되는 PCL을 나열하는 도구를 만들었습니다. 이 도구는 [.NET의 프레임워크 프로필](http://blog.stephencleary.com/2012/05/framework-profiles-in-net.html) 게시물에서 찾을 수 있습니다.
