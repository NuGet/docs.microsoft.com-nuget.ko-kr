---
title: "3.5 RC 릴리스 정보 | Microsoft Docs"
author: karann-msft
ms.author: karann-msft
manager: ghogen
ms.date: 11/11/2016
ms.topic: article
ms.prod: nuget
ms.technology: 
ms.assetid: 75a9b496-5762-48b6-922f-fdddf1369c45
description: "NuGet 3.5 RC 알려진된 문제, 버그 수정, 추가 된 기능 및 Dcr를 포함 하 여에 대 한 릴리스 정보입니다."
keywords: "NuGet 3.5 RC 릴리스 정보, 버그 수정, 알려진 문제, 추가 기능을 Dcr"
ms.reviewer:
- karann-msft
- unniravindranathan
ms.openlocfilehash: 09d566de6f53bc0f0ddd8049143dc647f3075671
ms.sourcegitcommit: d0ba99bfe019b779b75731bafdca8a37e35ef0d9
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 12/14/2017
---
#<a name="35-rc-release-notes"></a>3.5 RC 릴리스 정보

[NuGet 3.5 Beta2 릴리스 정보](../release-notes/nuget-3.5-Beta2.md) | [NuGet 3.5-RTM 릴리스 정보](../release-notes/nuget-3.5-RTM.md)

3.5 릴리스는 NuGet 클라이언트의 품질 및 성능 향상에 데 사용 됩니다. 또한에서는 제공 된 몇 가지 기능에 대 한 지원 같은 [대체 폴더](https://github.com/NuGet/Home/issues/2899), [PackageType](https://github.com/NuGet/Home/issues/2476) 지원 `.nuspec` 등입니다.

[문제 목록](https://github.com/NuGet/Home/issues?q=is%3Aissue+is%3Aclosed+milestone%3A%223.5 RC")

## <a name="bug-fixes"></a>버그 수정

* 패키지의 설치/복원 실패 "패키지에 여러 개 포함 된 `.nuspec` 파일입니다." - [#3231](https://github.com/NuGet/Home/issues/3231)

* nuget 팩 강제적으로 추가 `.tt` 어떠한-콘텐츠 폴더에 파일 압축 [#3203](https://github.com/NuGet/Home/issues/3203)

* nuget 팩 csproj (으로 `project.json`) packOptions 및 소유자-JSON 파일에 없는 경우 충돌 [#3180](https://github.com/NuGet/Home/issues/3180)

* 에 대 한 nuget 팩 `project.json` 요약, 작성자, 등-소유자와 같은 packOptions 태그를 무시 [#3161](https://github.com/NuGet/Home/issues/3161)

* 출력에서 종속성을 무시 하는 nuget 팩 `.nuspec` 에 대 한 `project.json`  -  [#3145](https://github.com/NuGet/Home/issues/3145)

* 프로젝트 손상된 상태로-남게 되므로 롤백으로 여러 패키지를 업데이트할 [#3139](https://github.com/NuGet/Home/issues/3139)

* Netstandard 프로젝트-에 대 한 콘텐츠 파일에서 추가 되지 않습니다 [#3118](https://github.com/NuGet/Home/issues/3118)

* .NET을 대상으로 하는 라이브러리 패키지할 수 없습니다. 표준 올바르게- [#3108](https://github.com/NuGet/Home/issues/3108)

* 파일-새 프로젝트 > v s 2015 및 Dev15-클래스 라이브러리 (이식 가능) 프로젝트 실패-> [#3094](https://github.com/NuGet/Home/issues/3094)

* NuGet 오류-1.0.0-*-올바른 버전 문자열이 아닙니다. [#3070](https://github.com/NuGet/Home/issues/3070)

* Find-package 실패를 표시 하지만 Install-package works- [#3068](https://github.com/NuGet/Home/issues/3068)

* 오류 때 dev15-에 "Install-package jquery.validation" [#3061](https://github.com/NuGet/Home/issues/3061)

* 설치 된 VS 2015 업데이트 3 버전 3.5.0 오류가 발생 합니다. NuGet을 사용 하는 VS에서 [#3053](https://github.com/NuGet/Home/issues/3053)

* 패키지 관리자 UI: 패키지를 업데이트 한 후 새 버전을 표시 하지 않는- [#3041](https://github.com/NuGet/Home/issues/3041)

* Delete 명령줄에-ApiKey 읽기/에서 전송 되지 않습니다 3.5.0-beta- [#3037](https://github.com/NuGet/Home/issues/3037)

* 잘못 된 문자열: 안정판 패키지에는 시험판 종속성 없어야 합니다. - [#3030](https://github.com/NuGet/Home/issues/3030)

* (Net46 및 windows 10) PCL 프로젝트 get NullRef 예외를 만듭니다. - [#3014](https://github.com/NuGet/Home/issues/3014)

* 더 높은 버전 allowedversions가 제약 조건-에 의해 제한 되는 경우 Nuget 업데이트 알림 메시지를 제공 해야 [#3013](https://github.com/NuGet/Home/issues/3013)

* 자격 증명 플러그 인) 종료 되었습니다 (오류-1 /-여러 소스가 포함 된 자격 증명 공급자를 사용 하는 경우 패키지 오류 다운로드 [#2885](https://github.com/NuGet/Home/issues/2885)

* nuget 패키지 종속성 누락 Newtonsoft.Json-팩 [#2876](https://github.com/NuGet/Home/issues/2876)

* Linux/MacOS + 모노-에서 ExecuteSynchronizedCore의 버그 [#2860](https://github.com/NuGet/Home/issues/2860)

* VS repositoryPath의 환경 변수를 지원 하지 않습니다 (nuget.exe은)- [#2763](https://github.com/NuGet/Home/issues/2763)

* 내게 필요한 옵션 문제-수정 [#2745](https://github.com/NuGet/Home/issues/2745)

* 하이픈으로 연결 된 프로필을 통해 휴대용 프레임 워크는 거부 됩니다. - [#2734](https://github.com/NuGet/Home/issues/2734)

* NuGet 패키지 관리자를 수행 하는 세부 정보에 적용 되지 않는 패키지에 해당 옵션 목록 지우기 `project.json`  -  [#2665](https://github.com/NuGet/Home/issues/2665)

* NuGet 3.3.0 업데이트와 함께 실패 '... 추가 제약 조건에 정의 된 packages.config이이 작업을 방지 합니다.' - [#1816](https://github.com/NuGet/Home/issues/1816)

* 잘못 된 메시지-throw 존재 하지 않는 로컬 원본의 패키지 설치 [#1674](https://github.com/NuGet/Home/issues/1674)

* "사용 가능한 업그레이드" 필터 표시-버전 제약 조건을 위반 하는 업그레이드 [#1094](https://github.com/NuGet/Home/issues/1094)

## <a name="performance-improvements"></a>성능 향상

* 성능: ContentModel 대상 프레임 워크 구문 분석-개선 [#3162](https://github.com/NuGet/Home/issues/3162)

* 성능: 읽기를 방지 하 `runtime.json` Rid를 갖지 않는 복원에 대 한 파일 [#3150](https://github.com/NuGet/Home/issues/3150)합니다. CI 컴퓨터에서 과도 한 3 초를 15 초 감소 ASP.NET 웹 응용 프로그램 샘플의 복원 합니다.

* 성능: 패키지 관리자 콘솔 init.ps1 로드 시간 [#2956](https://github.com/NuGet/Home/issues/2956)합니다. 132s 단위: 10 일부 경우에는 PackageManagerConsole 데 시간이 향상 되었습니다.

* NuGet 업데이트-에서 ReSharper 성능 문제를 해결 [#3044](https://github.com/NuGet/Home/issues/3044): 예제 프로젝트에서 패키지를 설치 하는 데 걸리는 시간에서에서 감소 140s 68s 합니다.

## <a name="dcrs"></a>Dcr

* 사용자는 업그레이드/설치 기반 dotnet tfm PCL 발생할 수 문제-알 수 있도록 필요한 NuGet [#3138](https://github.com/NuGet/Home/issues/3138)

* 잘못 된 설치/업그레이드 tfm w / 프로젝트에 대 한 경고 "dotnet"-= [#3137](https://github.com/NuGet/Home/issues/3137)

* Netcoreapp11 및 netstandard17 지원-추가 [#2998](https://github.com/NuGet/Home/issues/2998)

* NuGet 경고 헤더 내용을 nuget.exe-에 콘솔에 인쇄 [#2934](https://github.com/NuGet/Home/issues/2934)

* 에 대 한 활용 AssemblyMetadata 특성 `.nuspec` 토큰 바꾸기를- [#2851](https://github.com/NuGet/Home/issues/2851)

* 잠금 파일이-에서 잠긴된 속성을 제거 [#2379](https://github.com/NuGet/Home/issues/2379)

* 기호 패키지도 설치에 사용할 수 없습니다 또는 # 2807를 업데이트 합니다.

## <a name="features"></a>기능

* -대체 패키지 폴더에 대 한 지원 [#2899](https://github.com/NuGet/Home/issues/2899)

* 디자인 및 구현-도구 패키지를 지원 하기 위해 패키지 형식의 개념 [#2476](https://github.com/NuGet/Home/issues/2476)

* 경로 전역 패키지 폴더를 가져와야 하는 API [#2403](https://github.com/NuGet/Home/issues/2403)

* 기본 패키지 업데이트 지원- [#1291](https://github.com/NuGet/Home/issues/1291)
