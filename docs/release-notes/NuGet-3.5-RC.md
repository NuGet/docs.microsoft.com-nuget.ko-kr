---
title: 3.5 RC 릴리스 정보
description: NuGet 3.5 RC 알려진된 문제, 버그 수정, 추가 된 기능 및 Dcr 포함에 대 한 릴리스 정보입니다.
author: karann-msft
ms.author: karann
ms.date: 11/11/2016
ms.topic: conceptual
ms.openlocfilehash: 52c443ecd79c9108203f5a3c327078ce9e28b95b
ms.sourcegitcommit: 1d1406764c6af5fb7801d462e0c4afc9092fa569
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 09/04/2018
ms.locfileid: "43548540"
---
# <a name="nuget-35-rc-release-notes"></a>NuGet 3.5 RC 릴리스 정보

[NuGet 3.5 베타 2 릴리스 정보](../release-notes/nuget-3.5-Beta2.md) | [NuGet 3.5-RTM 릴리스 정보](../release-notes/nuget-3.5-RTM.md)

3.5 릴리스는 NuGet 클라이언트의 품질 및 성능을 개선 중점 합니다. 에 대 한 지원과 같은 몇 가지 기능이 함께 있는 뿐만 [대체 (fallback) 폴더](https://github.com/NuGet/Home/issues/2899), [PackageType](https://github.com/NuGet/Home/issues/2476) 지원 `.nuspec` 등입니다.

[문제 목록](https://github.com/NuGet/Home/issues?q=is%3Aissue+is%3Aclosed+milestone%3A%223.5%20RC")

## <a name="bug-fixes"></a>버그 수정

* 패키지의 설치/복원 실패 "패키지에 여러 개 포함 된 `.nuspec` 파일입니다." - [#3231](https://github.com/NuGet/Home/issues/3231)

* nuget pack 강제적으로 추가 됩니다 `.tt` 어떤-콘텐츠 폴더에 파일 [#3203](https://github.com/NuGet/Home/issues/3203)

* nuget 팩 csproj (사용 하 여 `project.json`) packOptions 및 JSON 파일의 소유자 없는 경우 충돌 [#3180](https://github.com/NuGet/Home/issues/3180)

* 에 대 한 nuget 팩 `project.json` 요약, 작성자, 소유자 등-packOptions 태그를 무시 [#3161](https://github.com/NuGet/Home/issues/3161)

* 출력의 종속성을 무시 하는 nuget 팩 `.nuspec` 에 대 한 `project.json`  -  [#3145](https://github.com/NuGet/Home/issues/3145)

* 손상된 된 상태로-프로젝트 유지 rollback을 사용 하 여 여러 패키지를 업데이트 [#3139](https://github.com/NuGet/Home/issues/3139)

* Netstandard 프로젝트-에 대 한 ContentFiles에서 추가 되지 않습니다 [#3118](https://github.com/NuGet/Home/issues/3118)

* .NET을 대상으로 하는 라이브러리를 패키지할 수 없습니다 표준 제대로 [#3108](https://github.com/NuGet/Home/issues/3108)

* 파일-> 새 프로젝트-Dev15 VS2015에서 클래스 라이브러리 (이식 가능) 프로젝트 실패-> [#3094](https://github.com/NuGet/Home/issues/3094)

* nuGet 오류-1.0.0-* 문자열이 아닙니다. 유효한 버전- [#3070](https://github.com/NuGet/Home/issues/3070)

* Find-package 실패를 표시 하지만 Install-package 작동- [#3068](https://github.com/NuGet/Home/issues/3068)

* 오류 때-dev15에서 "Install-package jquery.validation" [#3061](https://github.com/NuGet/Home/issues/3061)

* 설치 된 VS 2015 업데이트 3 버전 3.5.0 오류 발생-NuGet을 사용 하는 VS에서 [#3053](https://github.com/NuGet/Home/issues/3053)

* 패키지 관리자 UI: 패키지를 업데이트 한 후 새 버전이 표시 되지 않습니다- [#3041](https://github.com/NuGet/Home/issues/3041)

* -ApiKey 삭제 명령줄에서 읽기/에서 전송 되지 않습니다 3.5.0-beta- [#3037](https://github.com/NuGet/Home/issues/3037)

* 잘못 된 문자열: 패키지의 안정적인 릴리스 시험판 종속성에 없어야 합니다. - [#3030](https://github.com/NuGet/Home/issues/3030)

* PCL (net46 및 windows 10) 프로젝트 get NullRef 예외를 만드는 중입니다. - [#3014](https://github.com/NuGet/Home/issues/3014)

* 더 높은 버전 allowedVersions 제약 조건으로 제한 되 면 Nuget 업데이트 알림 메시지를 제공 해야 [#3013](https://github.com/NuGet/Home/issues/3013)

* 오류-1 사용 하 여 자격 증명 플러그 인 종료 / 여러 소스를 사용 하 여 자격 증명 공급자를 사용 하는 경우 패키지 다운로드 중 오류 발생 [#2885](https://github.com/NuGet/Home/issues/2885)

* nuget 패키지 종속성 누락 Newtonsoft.Json-팩 [#2876](https://github.com/NuGet/Home/issues/2876)

* Linux/MacOS + Mono-ExecuteSynchronizedCore 버그 [#2860](https://github.com/NuGet/Home/issues/2860)

* VS repositoryPath에서 환경 변수를 지원 하지 않습니다 (nuget.exe 않습니다)- [#2763](https://github.com/NuGet/Home/issues/2763)

* 액세스 가능성 문제를 해결 [#2745](https://github.com/NuGet/Home/issues/2745)

* 하이픈으로 연결 된 프로필을 사용 하 여 이식 가능한 프레임 워크 거부 됩니다. - [#2734](https://github.com/NuGet/Home/issues/2734)

* NuGet 패키지 관리자를 사용 해야 패키지 세부 정보에 적용 되지 않는 옵션 목록 명확히 `project.json`  -  [#2665](https://github.com/NuGet/Home/issues/2665)

* NuGet 3.3.0 업데이트 실패 '...는 추가 제약 조건에 정의 된 packages.config이이 작업을 방지 합니다.' - [#1816](https://github.com/NuGet/Home/issues/1816)

* 잘못 된 메시지-throw 존재 하지 않는 로컬 원본에서 패키지를 설치 [#1674](https://github.com/NuGet/Home/issues/1674)

* "사용 가능한 업그레이드" 필터 버전 제약 조건 위반 하는 업그레이드를 보여 줍니다. [#1094](https://github.com/NuGet/Home/issues/1094)

## <a name="performance-improvements"></a>성능 향상

* 성능: 개선 contentmodel은 대상 프레임 워크를 구문 분석- [#3162](https://github.com/NuGet/Home/issues/3162)

* 성능: 읽기를 방지 `runtime.json` Rid 되지 않은 복원에 대 한 파일 [#3150](https://github.com/NuGet/Home/issues/3150)합니다. CI 컴퓨터에서 ASP.NET 웹 응용 프로그램 3 초를 15 초 바탕으로 감소 하는 샘플을 복원 합니다.

* 성능: 패키지 관리자 콘솔 init.ps1 로드 시간 [#2956](https://github.com/NuGet/Home/issues/2956)합니다. 132s에서 10 사이의 경우도 PackageManagerConsole를 여는 데 시간이 향상 되었습니다.

* NuGet 업데이트-ReSharper 성능 문제 해결 [#3044](https://github.com/NuGet/Home/issues/3044): 샘플 프로젝트에서 패키지를 설치 하는 데 걸린 시간에서에서 감소 140s 68s 합니다.

## <a name="dcrs"></a>DCR

* 사용자를 기반으로 하는 dotnet tfm에서 업그레이드/설치 PCL 문제가 발생할 수 있습니다-알 수 있도록 필요한 NuGet [#3138](https://github.com/NuGet/Home/issues/3138)

* Tfm (포함)는 프로젝트에 대 한 잘못 된 설치/업그레이드 경고 = "dotnet"- [#3137](https://github.com/NuGet/Home/issues/3137)

* Netcoreapp11 및 netstandard17 지원-추가 [#2998](https://github.com/NuGet/Home/issues/2998)

* NuGet 경고 헤더 내용을 nuget.exe-콘솔에 인쇄 [#2934](https://github.com/NuGet/Home/issues/2934)

* AssemblyMetadata 특성 활용 `.nuspec` 대체-토큰 [#2851](https://github.com/NuGet/Home/issues/2851)

* 잠금 파일에서 잠긴된 속성을 제거 [#2379](https://github.com/NuGet/Home/issues/2379)

* 기호 패키지는 이전 설치에서 사용할 수 없습니다 또는 #2807 업데이트

## <a name="features"></a>기능

* -대체 패키지 폴더에 대 한 지원을 [#2899](https://github.com/NuGet/Home/issues/2899)

* 디자인 및 구현-도구 패키지를 지원 하기 위해 패키지 형식의 개념 [#2476](https://github.com/NuGet/Home/issues/2476)

* 전역 패키지 폴더 경로 이동 하려면 API [#2403](https://github.com/NuGet/Home/issues/2403)

* 네이티브 패키지 업데이트 지원- [#1291](https://github.com/NuGet/Home/issues/1291)
