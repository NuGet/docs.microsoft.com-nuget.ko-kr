---
title: 3.5 베타 2 릴리스 정보
description: NuGet 3.5 베타 2의 알려진된 문제, 버그 수정, 추가 된 기능 및 Dcr 포함에 대 한 릴리스 정보입니다.
author: karann-msft
ms.author: karann
ms.date: 11/11/2016
ms.topic: conceptual
ms.openlocfilehash: 4b47939e2fafc11823c41a849b3c58bbf0800ada
ms.sourcegitcommit: 1d1406764c6af5fb7801d462e0c4afc9092fa569
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 09/04/2018
ms.locfileid: "43551993"
---
# <a name="nuget-35-beta2-release-notes"></a>NuGet 3.5 베타 2 릴리스 정보

[NuGet 3.5 베타 릴리스 정보](../release-notes/nuget-3.5-Beta.md) | [NuGet 3.5 RC 릴리스 정보](../release-notes/nuget-3.5-RC.md)

Visual Studio 2013 및 nuget.exe에 대 한 2016 년 6 월 27 일 출시 된 NuGet 3.5 베타 2 RTM

[전체 변경 로그](https://github.com/NuGet/NuGet.Client/compare/release-3.5.0-beta...release-3.5.0-beta2)

[문제 목록](https://github.com/Nuget/Home/issues?q=is%3Aissue+milestone%3A%223.5+Beta2%22+is%3Aclosed)

## <a name="bug-fixes"></a>버그 수정

* 업데이트 된 오류 메시지를.NET Core에서 인증 된 피드-에 대 한 암호 decrpytion에 대 한 지원 부족 [#2942](https://github.com/NuGet/Home/issues/2942)

* 패키지 가져오기 패키지 관리자 콘솔에는.NET Core 프로젝트-열려 있으면 실패 [#2932](https://github.com/NuGet/Home/issues/2932)

* NuGet push 명령은 403의 잘못 된 처리 수정 [#2910](https://github.com/NuGet/Home/issues/2910)

* TFS 소스 제어에 바인딩된 disableSourceControlIntegration 설정 된 경우 솔루션의 패키지를 제거 하는 문제 해결로- [#2739](https://github.com/NuGet/Home/issues/2739)

* 계정 목표가 아닌 패키지로-되려면 패키지 업데이트 수정 [#2724](https://github.com/NuGet/Home/issues/2724)

* MSBuild의 자세한 정도 수준을 사용 하 여 UI 작업-Nuget 패키지 관리자에 대 한로 거 수준 설정 [#2705](https://github.com/NuGet/Home/issues/2705)

* 수정 NuGet 구성은-VS 2015 VSIX (v3.4.3)-웹 사이트 프로젝트에서 잘못 된 오류 [#2667](https://github.com/NuGet/Home/issues/2667)

* 팩 문제 해결 `.csproj` 콘텐츠 파일이 포함 인 경우 [#2658](https://github.com/NuGet/Home/issues/2658)

* 에 DefaultPushSource `NuGetDefaults.Config` (`ProgramData\NuGet`) 작동 하지 않음- [#2653](https://github.com/NuGet/Home/issues/2653)

* -값 패키지 생성 시 null 일 수 없습니다-Nuget 3.4.3 릴리스에서 문제를 해결 [#2648](https://github.com/NuGet/Home/issues/2648)

* 복원은 Nuget.Config에서 저장 된 자격 증명을 사용 하 여 VSTS 피드의- [#2647](https://github.com/NuGet/Home/issues/2647)

* 성능-버전 비교 코드에서 과도 하 게 할당 수정- [#2632](https://github.com/NuGet/Home/issues/2632)

* Nuget.exe의 여러 인스턴스를 병렬로-같은 패키지를 설치 하려고 할 때 문제를 해결 [#2628](https://github.com/NuGet/Home/issues/2628)

* 성능-다중 프로젝트 작업에 대 한 캐시 종속성 정보- [#2619](https://github.com/NuGet/Home/issues/2619)

* 문제를 해결할 때 원본 목록이 비어 있는-설정에서 패키지 원본은 추가할 경우 [#2617](https://github.com/NuGet/Home/issues/2617)

* 디자인 타임 외관-종속 된 패키지를 설치 하려고 할 때 Misleading 오류를 해결 [#2594](https://github.com/NuGet/Home/issues/2594)

* 첫 번째 소스만-시도 PackageManager "All"을 설정 하는 콘솔에서 패키지를 설치 [#2557](https://github.com/NuGet/Home/issues/2557)

* (Mono)-나중에 한 번 쓰기를 사용 하 여 파일에 있는 패키지를 사용 하 여 문제를 해결 [#2518](https://github.com/NuGet/Home/issues/2518)

* 오류 찾기 프로젝트에에서 있으면 업데이트 명령-예외 표시 [#2418](https://github.com/NuGet/Home/issues/2418)

* 인수를 사용 하 여 피드 nuget v3.3 이상에서 패키지를 설치 하는 경우 패키지 콘텐츠가 제대로 복원 되지 않습니다-패키지에 포함 된 경우 NoCache `.nupkg` 파일- [#2354](https://github.com/NuGet/Home/issues/2354)

* 패키지에서 1 소스-누락 된 경우 패키지 관련 문제 수정 (모든 원본)를 설치 [#2322](https://github.com/NuGet/Home/issues/2322)

* 단일 소스 권한-확인에 실패할 경우 요소를 설치 [#2034](https://github.com/NuGet/Home/issues/2034)

* `.nuspec` 범위는-IncludeReferencedProjects 버전을 재정의 해야 하는 버전 [#1983](https://github.com/NuGet/Home/issues/1983)

* NuGet 3.3.0 업데이트 실패 '...는 추가 제약 조건에 정의 된 packages.config이이 작업을 방지 합니다.' - [#1816](https://github.com/NuGet/Home/issues/1816)

* nuget.exe 업데이트 어셈블리 강력한 이름 및 개인 특성을 삭제합니다. - [#1778](https://github.com/NuGet/Home/issues/1778)

* "DefaultPushSource"-에 대 한 상대 파일 경로 사용 하 여 문제를 해결 [#1746](https://github.com/NuGet/Home/issues/1746)

* 오류 메시지를 해결 하는 업데이트-개선 [#1373](https://github.com/NuGet/Home/issues/1373)

## <a name="features-and-behavior-changes"></a>기능 및 동작 변경 내용

* nuget.exe push-시간 제한 매개 변수 작동 하지 않음- [#2785](https://github.com/NuGet/Home/issues/2785)

* nuget.exe restore 나오지 `.props` 하 고 `.targets` 파일에 대 한 `.nuproj` 프로젝트 (v3.4.3.855에서 재발)- [#2711](https://github.com/NuGet/Home/issues/2711)

* 확장성 API 가져오기-프레임 워크를 비교할 필요 [#2633](https://github.com/NuGet/Home/issues/2633)

* 사용 하는 경우 종속성 옵션 숨기기 `project.json`  -  [#2486](https://github.com/NuGet/Home/issues/2486)

* Nuget.exe 자세한 출력-버전 헤더 출력 [#1887](https://github.com/NuGet/Home/issues/1887)

* NuGet {rid} /runtimes/ /nativeassets/ {txm}에 대 한 지원을 추가 해야- [#2782](https://github.com/NuGet/Home/issues/2782)