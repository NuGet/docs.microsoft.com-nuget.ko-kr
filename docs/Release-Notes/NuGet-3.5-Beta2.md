---
title: "3.5 베타 2 릴리스 정보 | Microsoft Docs"
author: karann-msft
ms.author: karann-msft
manager: ghogen
ms.date: 11/11/2016
ms.topic: article
ms.prod: nuget
ms.technology: 
description: "알려진된 문제, 버그 수정, 추가 된 기능 및 Dcr를 포함 하 여 NuGet 3.5 베타 2에 대 한 릴리스 정보입니다."
keywords: "NuGet 3.5 베타 2, 릴리스 정보 버그 수정, 알려진 문제, 추가 기능을 Dcr"
ms.reviewer:
- karann-msft
- unniravindranathan
ms.openlocfilehash: 4073b669c19f9e96ebd35ba269919b5f42313e7c
ms.sourcegitcommit: 4651b16a3a08f6711669fc4577f5d63b600f8f58
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 02/02/2018
---
# <a name="nuget-35-beta2-release-notes"></a>NuGet 3.5 베타 2 릴리스 정보

[NuGet 3.5 베타 릴리스 정보](../release-notes/nuget-3.5-Beta.md) | [NuGet 3.5 RC 릴리스 정보](../release-notes/nuget-3.5-RC.md)

2016 년 6 월 27 일에 Visual Studio 2013 및 nuget.exe 릴리스 되었습니다 NuGet 3.5 베타 2 RTM

[전체 변경 로그](https://github.com/NuGet/NuGet.Client/compare/release-3.5.0-beta...release-3.5.0-beta2)

[문제 목록](https://github.com/Nuget/Home/issues?q=is%3Aissue+milestone%3A%223.5+Beta2%22+is%3Aclosed)

## <a name="bug-fixes"></a>버그 수정

* 업데이트 된 오류 메시지를 인증 된 피드-에 대 한.NET Core에서는 암호 decrpytion에 대 한 지원 부족 [#2942](https://github.com/NuGet/Home/issues/2942)

* 패키지 가져오기 패키지 관리자 콘솔에는.NET Core 프로젝트-열려 있으면 실패 [#2932](https://github.com/NuGet/Home/issues/2932)

* NuGet 푸시 명령에서 403의 잘못 된 처리를 수정 [#2910](https://github.com/NuGet/Home/issues/2910)

* DisableSourceControlIntegration 설정 된 경우 TFS 소스 제어에 바인딩할 솔루션에서 패키지를 제거할 때에 문제 해결-true로 [#2739](https://github.com/NuGet/Home/issues/2739)

* 패키지 업데이트 계정-대상 패키지-상황이 해결 [#2724](https://github.com/NuGet/Home/issues/2724)

* MSBuild의 자세한 정도 수준을 사용 하 여 UI 작업-Nuget 패키지 관리자에 대 한로 거 수준을 설정 [#2705](https://github.com/NuGet/Home/issues/2705)

* NuGet 구성이 수정 프로그램은-VS 2015 VSIX (v3.4.3)-웹 사이트 프로젝트에서 잘못 된 오류 [#2667](https://github.com/NuGet/Home/issues/2667)

* 팩 문제를 해결 `.csproj` 콘텐츠 파일은 포함-때 [#2658](https://github.com/NuGet/Home/issues/2658)

* DefaultPushSource `NuGetDefaults.Config` (`ProgramData\NuGet`) 작동 하지 않는- [#2653](https://github.com/NuGet/Home/issues/2653)

* -값은 패키지 만들기에는 null 일 수 없습니다-Nuget 3.4.3 릴리스에서 문제를 해결 [#2648](https://github.com/NuGet/Home/issues/2648)

* 복원은 Nuget.Config에서 저장 된 자격 증명을 사용 하 여 VSTS 피드에- [#2647](https://github.com/NuGet/Home/issues/2647)

* 성능-버전 비교 코드의 과도 한 할당 수정- [#2632](https://github.com/NuGet/Home/issues/2632)

* Nuget.exe 여러 개 병렬로-같은 패키지를 설치 하려고 할 때 문제를 해결 [#2628](https://github.com/NuGet/Home/issues/2628)

* -다중 프로젝트 작업에 대 한 종속성 정보 캐시-성능 [#2619](https://github.com/NuGet/Home/issues/2619)

* 문제를 해결할 때 소스 목록이 비어 있는-패키지 소스 없습니다 설정에서 추가할 수 [#2617](https://github.com/NuGet/Home/issues/2617)

* 디자인 타임 외관-에 의존 하는 패키지를 설치 하려고 할 때 Misleading 오류를 해결 [#2594](https://github.com/NuGet/Home/issues/2594)

* 첫 번째 소스-시도 PackageManager "All"을 설정 하는 콘솔에서 패키지를 설치 [#2557](https://github.com/NuGet/Home/issues/2557)

* (모노)-나중에 한 번 쓰기를 사용 하 여 파일에 있는 패키지의 문제를 해결 [#2518](https://github.com/NuGet/Home/issues/2518)

* 에 있을 때 오류 찾기 프로젝트 update 명령-예외 표시 [#2418](https://github.com/NuGet/Home/issues/2418)

* 패키지 콘텐츠 인수와 함께 피드 nuget v3.3 +에서 패키지를 설치할 때 제대로 복원 되지-NoCache 패키지에 포함 된 경우 `.nupkg` 파일- [#2354](https://github.com/NuGet/Home/issues/2354)

* 패키지와 문제 해결-1 원본의 패키지 누락 된 경우 (모든 원본의 경우)를 설치 [#2322](https://github.com/NuGet/Home/issues/2322)

* 단일 소스 권한 부여-에 실패 하는 경우 블록 설치 [#2034](https://github.com/NuGet/Home/issues/2034)

* `.nuspec`범위는-IncludeReferencedProjects 버전-를 재정의 해야 하는 버전 [#1983](https://github.com/NuGet/Home/issues/1983)

* NuGet 3.3.0 업데이트와 함께 실패 '... 추가 제약 조건에 정의 된 packages.config이이 작업을 방지 합니다.' - [#1816](https://github.com/NuGet/Home/issues/1816)

* nuget.exe 업데이트 어셈블리의 강력한 이름 및 개인 특성을 삭제합니다. - [#1778](https://github.com/NuGet/Home/issues/1778)

* "DefaultPushSource"-에 대 한 상대 파일 경로 문제 해결 [#1746](https://github.com/NuGet/Home/issues/1746)

* 업데이트 확인자 실패 메시지-개선 [#1373](https://github.com/NuGet/Home/issues/1373)

## <a name="features-and-behavior-changes"></a>기능 및 동작 변경 내용

* nuget.exe 푸시-timeout 매개 변수 작동 하지 않는- [#2785](https://github.com/NuGet/Home/issues/2785)

* nuget.exe 복원을 생성 하지 않는다는 `.props` 및 `.targets` 파일에 대 한 `.nuproj` 프로젝트 (v3.4.3.855 회귀)- [#2711](https://github.com/NuGet/Home/issues/2711)

* 확장성 API 가져오기-프레임 워크를 비교할 필요 [#2633](https://github.com/NuGet/Home/issues/2633)

* 종속성 옵션을 사용 하는 경우 숨기기 `project.json`  -  [#2486](https://github.com/NuGet/Home/issues/2486)

* 인쇄 결과물에 자세한 출력-버전 헤더 nuget.exe [#1887](https://github.com/NuGet/Home/issues/1887)

* NuGet {rid} /runtimes/ /nativeassets/ {txm}에 대 한 지원을 추가 해야 /- [#2782](https://github.com/NuGet/Home/issues/2782)