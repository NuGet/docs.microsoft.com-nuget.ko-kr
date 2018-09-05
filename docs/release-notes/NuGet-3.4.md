---
title: NuGet 3.4 릴리스 정보
description: 알려진된 문제, 버그 수정, 추가 된 기능 및 Dcr 포함 하는 NuGet 3.4에 대 한 릴리스 정보입니다.
author: karann-msft
ms.author: karann
ms.date: 11/11/2016
ms.topic: conceptual
ms.openlocfilehash: 77c0117fc40031a327e8dcb0aac5cd4045239e97
ms.sourcegitcommit: 1d1406764c6af5fb7801d462e0c4afc9092fa569
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 09/04/2018
ms.locfileid: "43551193"
---
# <a name="nuget-34-release-notes"></a>NuGet 3.4 릴리스 정보

[NuGet 3.4 RC 릴리스 정보](../release-notes/nuget-3.4-RC.md) | [3.4.1 NuGet 릴리스 정보](../release-notes/nuget-3.4.1.md)

NuGet 3.4 Visual Studio 2015 업데이트 2 및 Visual Studio 15 Preview 릴리스의 일부로 2016 년 3 월 30 일에 릴리스 되었으며 머리에 몇 가지 개념을 사용 하 여 빌드된:

* 플랫폼 간 지원
* 성능 향상
* 보조 UI 개선 사항

다음과 같은 기능 RC의 이전에 추가한 및 업데이트 되었거나 3.4 릴리스에 대 한 완료 되었습니다.

## <a name="new-features"></a>새 기능

* NuGet 클라이언트는 이제 gzip 콘텐츠 인코딩 리포지토리에서 지원
* Xproj 프로젝트에서 패키지의 Pdb에 대 한 지원
* ContentFiles 요소에서 작업을 iOS 및 Android 빌드에 대 한 지원
* Netstandard 및 netstandardapp 프레임 워크 모니커 지원

## <a name="new-user-interface-features"></a>새로운 사용자 인터페이스 기능

* 설치 됨, 업데이트 및 통합 탭에서 특히 중요 한 성능 향상
* 집계 ' 모든 패키지 소스 ' 소스를 사용 하 여 적절 한 검색 결과 병합 수
* 설치 하 고 이제 업데이트 탭은 사전순으로 정렬
* 검색을 새로 고칠 수 있도록 새로 고침 단추를 추가 합니다.
* 버전 목록 맨 위에 있는 최신 빌드 옵션

## <a name="updates-and-improvements"></a>업데이트 및 향상 된 기능

* 참조 된 패키지 `project.json` 부동 있는 버전 모든 빌드에 대해 업데이트 되지 것입니다. 대신, 복원, 정리, 다시 작성 하거나 수정 해야 하는 경우에 업데이트 됩니다 `project.json`합니다.
* nuget.org 리포지토리 소스는 NuGet 구성 UI를 사용 하는 경우 프로젝트 구성에 더 이상 강제 됩니다.
* NuGet에 더 이상 공유 프로젝트에서 패키지를 복원 하거나 잠금 파일을 씁니다.
* 향상 되었습니다. 네트워크 오류가 발생 하 고 연결할 수 없거나 응답 속도가 느린 서버에 대 한 처리를 다시 시도 하세요.
* Visual Studio 패키지 관리자 UI에서 키보드 및 마우스 동작 개선 되었습니다.
* 이제 최신 지원 `project.json` 스키마 DNX에서.

## <a name="breaking-changes"></a>주요 변경 사항

* 패키지 버전 번호 형식으로 이제 정규화할지 *주요*. *사소한*. *패치*-*시험판* 각 주 버전, 부 및 패치 정수로 처리 되 고 모든 선행 0을 삭제 합니다.  시험판 정보를 문자열로 처리 됩니다 하 고 내용이 적용 됩니다. 이러한 번호는 NuGet 클라이언트 및 nuget.org 서비스에서 제공 하는 검색에서 쿼리에 사용 됩니다.  자세한 내용은 아래에서 NuGet 문서에서 찾을 수 있습니다 [시험판 버전](../create-packages/prerelease-packages.md)합니다.

## <a name="known-issues"></a>알려진 문제

* **문제:** Windows 10 v1511 사용자 문제나도 Visual Studio 충돌 Visual Studio에서 Powershell 사용 하 여 다음 시나리오에서 발생할 수 있습니다.
    * 설치 / install.ps1 있는 패키지를 제거 / uninstall.ps1 스크립트
    * (예: EntityFramework) init.ps1 스크립트를 포함 하는 프로젝트를 로드 합니다.
    * 웹 콘텐츠 게시

* **해결 방법:** Windows 10 설치에 최신 패치 적용, 특별히 (KB 3124263) 2016 년 1 월 또는 이후 업데이트가 있는지 확인 합니다.  자세한 내용은 [GitHub 문제 #1638](http://github.com/nuget/home/issues/1638)

* **문제:** NuGet v2 프로토콜 리디렉션이 끊어집니다.
대체 호스트에 요청을 리디렉션하는 사용자 지정 NuGet 리포지토리에서 리디렉션 요청을 인식하지 못합니다.
* **해결 방법:** 이 문제를 해결 하려면 리디렉션된 서버 위치를 가리키도록 설정에서 패키지 리포지토리 URI를 구성 합니다.
자세한 내용은 [GitHub 끌어오기 요청 #387](https://github.com/NuGet/NuGet.Client/pull/387)합니다.

찾을 수 있는 GitHub 문제 목록에서 문제를 추적 하려면 계속 합니다. [http://github.com/nuget/home/issues](http://github.com/nuget/home/issues)