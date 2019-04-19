---
title: NuGet 4.6 RTM 릴리스 정보
description: NuGet 4.6.0에 대한 릴리스 정보(알려진 문제, 버그 수정, 추가된 기능 및 DCR 포함)
author: anangaur
ms.author: anangaur
ms.date: 3/7/2018
ms.topic: conceptual
ms.openlocfilehash: eacd29d4c9340a0f015fcdf6c5b9dd41bf781419
ms.sourcegitcommit: 74bf831e013470da8b0c1f43193df10bfb1f4fe6
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 03/26/2019
ms.locfileid: "58432558"
---
# <a name="nuget-46-release-notes"></a>NuGet 4.6 릴리스 정보

[Visual Studio 2017 15.6 RTW](https://www.visualstudio.com/news/releasenotes/vs2017-relnotes)는 [NuGet 4.6.0](https://dist.nuget.org/win-x86-commandline/v4.6.0/nuget.exe)과 함께 제공됩니다.

## <a name="summary-whats-new-in-460"></a>요약: 4.6.0의 새로운 기능

* [패키지 서명](../create-packages/sign-a-package.md)에 대한 지원을 추가했습니다.
* Visual Studio 2017 및 nuget.exe는 이제 [서명된 패키지](../reference/signed-packages-reference.md)의 패키지 설치, 복원 전에 패키지 무결성을 확인합니다.
* 연속 복원의 성능을 개선했습니다.

## <a name="summary-whats-new-in-463"></a>요약: 4.6.3의 새로운 기능

* 보안 수정: ~/.nuget 내에서 만든 파일에 대한 사용 권한이 열려 있습니다. [#7673](https://github.com/NuGet/Home/issues/7673) [CVE-2019-0757](https://portal.msrc.microsoft.com/en-us/security-guidance/advisory/CVE-2019-0757)

## <a name="summary-whats-new-in-464"></a>요약: 4.6.4의 새로운 기능

* 보안 수정: NUPKG 내부에 있는 파일에는 NUPKG 디렉터리 위의 상대 경로가 포함될 수 있습니다. [#7906](https://github.com/NuGet/Home/issues/7906)

## <a name="known-issues"></a>알려진 문제

### <a name="issues-with-net-standard-20-with-net-framework--nuget"></a>.NET Framework 및 NuGet이 포함된 .NET Standard 2.0 관련 문제 

.NET Standard 및 해당 도구는 .NET Framework 4.6.1을 대상으로 하는 프로젝트에서 .NET Standard 2.0 또는 이전 버전을 대상으로 하는 NuGet 패키지 및 프로젝트를 사용할 수 있도록 설계되었습니다. [이 문서](https://github.com/dotnet/standard/issues/481)에서는 해당 시나리오와 관련된 문제, 문제를 해결하기 위한 계획 및 현재의 도구 상태로 배포할 수 있는 해결 방법을 요약하고 있습니다.

## <a name="top-issues-fixed-in-this-release"></a>이번 릴리스에서 해결된 주요 문제

**성능 개선**

* 변경 내용이 없는 경우 자산 파일을 기록하지 않음 - [#6491](https://github.com/NuGet/Home/issues/6491)
* 자식 프로젝트의 TFM이 부모 프로젝트와 일치하지 않는 경우 복원 시 추가 MSBuild 평가가 수행됨 - [#6311](https://github.com/NuGet/Home/issues/6311)
* 종속성 그래프 사양 생성을 최적화하여 NoOp 복원 성능 개선 - [#6252](https://github.com/NuGet/Home/issues/6252)

**버그**

* 로컬 폴더로 푸시하면 nupkg가 잠김 - [#6325](https://github.com/NuGet/Home/issues/6325)
* NuGet 플러그인 구현: 여러 문제 - [#6149](https://github.com/NuGet/Home/issues/6149)
* UIHang - VSSolutionManager에서 MEF 초기화의 쿼리 서비스 호출 제거 - [#6110](https://github.com/NuGet/Home/issues/6110)
* 취소된 패키지 다운로드 작업의 오류 보고 예외 - [#6096](https://github.com/NuGet/Home/issues/6096)
* NuGet.exe가 어셈블리 이름의 '+'를 '%2B'로 바꿈 - [#5956](https://github.com/NuGet/Home/issues/5956)
* Fn+F1을 눌러도 PM UI 및 콘솔의 올바른 도움말 페이지로 이동되지 않음 - [#5912](https://github.com/NuGet/Home/issues/5912)
* VS NuGet가 특정 상황에서 프로젝트 파일에 절대 경로를 기록함 - [#5888](https://github.com/NuGet/Home/issues/5888)
* 4.3 재발 해결 - 콘텐츠 파일에서 자리 표시자 $product$ 및 $AssemblyGuid$가 변환을 통해 대체되지 않음 - [#5880](https://github.com/NuGet/Home/issues/5880)
* 여러 소스를 사용하는 dotnet restore가 충돌함 - [#5817](https://github.com/NuGet/Home/issues/5817)
* 팩이 프로젝트 버전을 다시 계산해야 git 버전 관리가 가능함 - [#4790](https://github.com/NuGet/Home/issues/4790)
* 호환되지 않는 패키지를 설치할 때 이해하기 어려운 오류 개선 - [#4555](https://github.com/NuGet/Home/issues/4555)
* TemplateWizard에서 패키지를 PackageReference로 설치하는 옵션이 필요함 - [#4549](https://github.com/NuGet/Home/issues/4549)
* 개발자 명령 프롬프트 외부에서 MSBuild.exe를 실행할 때 패키지에서 제공한 props 파일이 무시됨 - [#4530](https://github.com/NuGet/Home/issues/4530)
* 프로젝트에 적용할 수 없는 .NET Standard 라이브러리를 참조할 때 나쁨 오류 메시지 해결 - [#4423](https://github.com/NuGet/Home/issues/4423)
* 약간의 지침이 포함된 이식 가능한 프로필을 대상으로 하는 패키지의 경우 dotnet add package가 실패함 - [#4349](https://github.com/NuGet/Home/issues/4349)
* dotnet pack - ProjectReference에 버전 접미사가 없음 - [#4337](https://github.com/NuGet/Home/issues/4337)
* .NET Core 템플릿 관련 빌드 오류 및 VS 충돌 - [#3973](https://github.com/NuGet/Home/issues/3973)
* 소스 https:*의 서비스 인덱스를 로드할 수 없음 - [#3681](https://github.com/NuGet/Home/issues/3681)
* nuget.exe 목록 -allversion이 작동하지 않음 - [#3441](https://github.com/NuGet/Home/issues/3441)
* 잘못된 종속성 해결 오류 메시지 - [#2984](https://github.com/NuGet/Home/issues/2984)
* nuget.exe restore가 .msbuildproj에 대한 .props 및 .targets 파일을 생성하지 않음(v3.3.0-3.4.4 업그레이드에서 재발) - [#2921](https://github.com/NuGet/Home/issues/2921)
* XAML 파일을 연 상태에서 NuGet 패키지를 업데이트할 때 UI 지연 - [#2878](https://github.com/NuGet/Home/issues/2878)
* 경로에 잘못된 문자가 있을 경우 IIS의 WebSite 프로젝트가 실패함 - [#2798](https://github.com/NuGet/Home/issues/2798)
* CentOS에서 Nuget add가 중지됨 - [#2708](https://github.com/NuGet/Home/issues/2708)
* json.net의 경우 packagesavemode -nupkg를 사용한 복원이 실패함 - [#2706](https://github.com/NuGet/Home/issues/2706)
* 복원 명령의 vs 출력 창에서 패키지 관리자 필터를 사용할 수 없음 - [#2704](https://github.com/NuGet/Home/issues/2704)

[이번 릴리스에서 수정된 모든 문제 목록](https://github.com/NuGet/Home/issues?q=is%3Aissue+is%3Aclosed+milestone%3A%224.6")
