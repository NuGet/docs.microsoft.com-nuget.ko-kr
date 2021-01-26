---
title: 3.5 Beta2 릴리스 정보
description: 알려진 문제, 버그 수정, 추가 된 기능 및 Ecrs를 비롯 한 NuGet 3.5 베타 2에 대 한 릴리스 정보입니다.
author: JonDouglas
ms.author: jodou
ms.date: 11/11/2016
ms.topic: conceptual
ms.openlocfilehash: 2aa92d4ef97acb2b4b70388cd4d580e7094aea45
ms.sourcegitcommit: ee6c3f203648a5561c809db54ebeb1d0f0598b68
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 01/26/2021
ms.locfileid: "98776394"
---
# <a name="nuget-35-beta2-release-notes"></a>NuGet 3.5 Beta2 릴리스 정보

[NuGet 3.5-베타 릴리스 정보](../release-notes/nuget-3.5-Beta.md)  |  [NuGet 3.5-RC 릴리스 정보](../release-notes/nuget-3.5-RC.md)

NuGet 3.5 베타 2 RTM은 Visual Studio 2013 및 nuget.exe에 대해 2016 년 6 월 27 일에 출시 되었습니다.

[전체 변경 로그](https://github.com/NuGet/NuGet.Client/compare/release-3.5.0-beta...release-3.5.0-beta2)

[문제 목록](https://github.com/Nuget/Home/issues?q=is%3Aissue+milestone%3A%223.5+Beta2%22+is%3Aclosed)

## <a name="bug-fixes"></a>버그 픽스

* 인증 된 피드에 대 한 .NET Core의 암호 decrpytion 지원 되지 않는 오류 메시지를 업데이트 했습니다.- [#2942](https://github.com/NuGet/Home/issues/2942)

* .NET Core 프로젝트가 열려 있는 경우 패키지 관리자 콘솔 Get-Package 실패 함- [#2932](https://github.com/NuGet/Home/issues/2932)

* NuGet push 명령 [#2910](https://github.com/NuGet/Home/issues/2910) 에서 잘못 된 처리 403을 수정 합니다.

* DisableSourceControlIntegration가 true로 설정 된 경우 TFS 소스 제어에 바인딩된 솔루션에서 패키지 제거의 문제를 해결 합니다. [#2739](https://github.com/NuGet/Home/issues/2739)

* 대상 패키지가 아닌 패키지를 고려 하도록 패키지 업데이트 수정- [#2724](https://github.com/NuGet/Home/issues/2724)

* MSBuild의 자세한 정도 수준을 사용 하 여 Nuget 패키지 관리자 UI 작업에 대 한로 거 수준을 설정 합니다.- [#2705](https://github.com/NuGet/Home/issues/2705)

* 웹 사이트 프로젝트에서 NuGet 구성 수정이 잘못 되었습니다.-VS 2015 VSIX (v 3.4.3)- [#2667](https://github.com/NuGet/Home/issues/2667)

* `.csproj`콘텐츠 파일이 포함 된 경우의 팩 문제 해결- [#2658](https://github.com/NuGet/Home/issues/2658)

* DefaultPushSource in `NuGetDefaults.Config` ( `ProgramData\NuGet` )이 작동 하지 않음- [#2653](https://github.com/NuGet/Home/issues/2653)

* Nuget 3.4.3의 문제를 수정 합니다.-값은 패키지를 만들 때 null 일 수 없습니다.- [#2648](https://github.com/NuGet/Home/issues/2648)

* 복원 Nuget.Config VSTS 피드에 대 한 저장 된 자격 증명을 사용 합니다.- [#2647](https://github.com/NuGet/Home/issues/2647)

* 성능-버전 comparsion 코드에서 과도 한 할당 수정- [#2632](https://github.com/NuGet/Home/issues/2632)

* 여러 nuget.exe 인스턴스가 동시에 동일한 패키지를 설치 하려고 할 때 문제를 해결 [#2628](https://github.com/NuGet/Home/issues/2628)

* 다중 프로젝트 작업에 대 한 성능 캐시 종속성 정보- [#2619](https://github.com/NuGet/Home/issues/2619)

* 소스 목록이 없습니다 경우 설정에서 패키지 소스를 추가할 수 있는 문제를 해결 [#2617](https://github.com/NuGet/Home/issues/2617)

* 외관- [#2594](https://github.com/NuGet/Home/issues/2594) 에 종속 된 패키지를 설치 하려고 할 때 잘못 된 오류를 수정 합니다.

* PackageManager 콘솔에서 "All"을 설정 하 여 패키지를 설치 하면 첫 번째 소스- [#2557](https://github.com/NuGet/Home/issues/2557) 만 시도 합니다.

* 나중에 쓰기 시간이 포함 된 파일을 포함 하는 패키지 문제 해결 (Mono)- [#2518](https://github.com/NuGet/Home/issues/2518)

* 업데이트 명령에서 프로젝트를 찾는 동안 오류가 발생 하는 경우 예외 표시- [#2418](https://github.com/NuGet/Home/issues/2418)

* 패키지에 파일이 포함 된 경우 NoCache를 사용 하 여 nuget v 3.3 + 피드에서 패키지를 설치 하면 패키지 콘텐츠가 제대로 복원 되지 않습니다. `.nupkg` - [#2354](https://github.com/NuGet/Home/issues/2354)

* 1 원본에서 패키지가 누락 된 경우 패키지 설치 (모든 원본)의 문제 해결- [#2322](https://github.com/NuGet/Home/issues/2322)

* 단일 원본에서 권한 부여에 실패 하는 경우의 설치 차단- [#2034](https://github.com/NuGet/Home/issues/2034)

* `.nuspec`버전 범위는-IncludeReferencedProjects version- [#1983](https://github.com/NuGet/Home/issues/1983) 를 재정의 해야 합니다.

* ' 추가 제약 조건을 사용 하 여 NuGet 3.3.0 업데이트가 실패 합니다. packages.config에 정의 되어 있으므로이 작업을 수행할 수 없습니다. - [#1816](https://github.com/NuGet/Home/issues/1816)

* nuget.exe 업데이트는 어셈블리의 강력한 이름 및 Private 특성을 삭제 합니다. - [#1778](https://github.com/NuGet/Home/issues/1778)

* "DefaultPushSource"의 상대 파일 경로 문제 해결- [#1746](https://github.com/NuGet/Home/issues/1746)

* 업데이트 해결 프로그램 실패 메시지 개선- [#1373](https://github.com/NuGet/Home/issues/1373)

## <a name="features-and-behavior-changes"></a>기능 및 동작 변경 내용

* nuget.exe 푸시 시간 제한 매개 변수가 작동 하지 않습니다.- [#2785](https://github.com/NuGet/Home/issues/2785)

* nuget.exe 복원은 `.props` 프로젝트에 대해 및 파일을 생성 하지 않습니다 `.targets` `.nuproj` (v 3.4.3.855의 회귀). [#2711](https://github.com/NuGet/Home/issues/2711)

* 프레임 워크를 가져오기와 비교 하려면 확장성 API가 필요 [#2633](https://github.com/NuGet/Home/issues/2633)

* #2486 사용 시 종속성 옵션 숨기기 `project.json`  -  [](https://github.com/NuGet/Home/issues/2486)

* 자세한 출력에서 nuget.exe 버전 헤더를 출력 합니다. [#1887](https://github.com/NuGet/Home/issues/1887)

* NuGet은/runtimes/{rid}/nativeassets/{txm}/에 대 한 지원을 추가 해야 합니다. [#2782](https://github.com/NuGet/Home/issues/2782)