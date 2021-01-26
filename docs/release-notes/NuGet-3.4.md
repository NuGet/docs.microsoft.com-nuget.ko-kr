---
title: NuGet 3.4 릴리스 정보
description: 알려진 문제, 버그 수정, 추가 된 기능 및 Ecrs를 비롯 한 NuGet 3.4에 대 한 릴리스 정보입니다.
author: JonDouglas
ms.author: jodou
ms.date: 11/11/2016
ms.topic: conceptual
ms.openlocfilehash: 794b25e2d81d7a2c297a185bdb34a7cf68535723
ms.sourcegitcommit: ee6c3f203648a5561c809db54ebeb1d0f0598b68
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 01/26/2021
ms.locfileid: "98776416"
---
# <a name="nuget-34-release-notes"></a>NuGet 3.4 릴리스 정보

[NuGet 3.4-RC 릴리스 정보](../release-notes/nuget-3.4-RC.md)  |  [NuGet 3.4.1 릴리스 정보](../release-notes/nuget-3.4.1.md)

NuGet 3.4는 Visual Studio 2015 업데이트 2 및 Visual Studio 15 Preview 릴리스의 일부로 년 3 월 30 일에 출시 되었으며 2016, 몇 가지 개념를 바뀌어으로 빌드 되었습니다.

* 플랫폼 간 지원
* 성능 향상
* 사소한 UI 개선

다음 기능은 이전에 RC에 추가 되었으며 3.4 릴리스에 대해 업데이트 또는 완료 되었습니다.

## <a name="new-features"></a>새로운 기능

* NuGet 클라이언트는 이제 리포지토리에서 gzip 콘텐츠 인코딩을 지원 합니다.
* Xproj 프로젝트의 패키지에서 Pdb에 대 한 지원
* ContentFiles 요소에서 iOS 및 Android 빌드 작업에 대 한 지원
* Netstandard.library 및 netstandardapp framework 모니커 지원

## <a name="new-user-interface-features"></a>새 사용자 인터페이스 기능

* 설치, 업데이트 및 통합 탭에서 특히 성능이 크게 향상 되었습니다.
* 올바른 검색 결과 병합에서 ' 모든 패키지 원본 ' 원본을 사용할 수 있습니다.
* 설치 됨 및 업데이트 탭은 이제 사전순으로 정렬 됩니다.
* 검색을 새로 고칠 수 있는 새로 고침 단추를 추가 했습니다.
* 버전 목록의 맨 위에 있는 최신 빌드 옵션

## <a name="updates-and-improvements"></a>업데이트 및 개선 사항

* 부동 버전이 있는에서 참조 되는 패키지는 `project.json` 모든 빌드에서 업데이트 되지 않습니다. 대신 복원, 정리, 다시 빌드 또는 수정이 적용 되는 경우에만 업데이트 됩니다 `project.json` .
* NuGet 구성 UI를 사용 하는 경우 nuget.org 리포지토리 원본은 더 이상 프로젝트 구성에 적용 되지 않습니다.
* NuGet은 더 이상 공유 프로젝트의 패키지를 복원 하거나 잠금 파일을 쓰지 않습니다.
* 네트워크 오류를 개선 하 고 연결이 불가능 하거나 응답 하지 않는 서버에 대 한 처리를 다시 시도 했습니다.
* Visual Studio 패키지 관리자 UI에서 키보드 및 마우스 동작이 개선 되었습니다.
* 이제 `project.json` DNX에서 최신 스키마를 지원 합니다.

## <a name="breaking-changes"></a>주요 변경 내용

* 이제 패키지 버전 번호가 *major* 형식으로 정규화 됩니다. *부*. *패치* - *시험판*   주 버전, 부 버전 및 패치 각각은 정수로 처리 되며 앞에 오는 0을 삭제 합니다.  시험판 정보는 문자열로 처리 되며 변경 내용이 적용 되지 않습니다. 이러한 숫자는 NuGet 클라이언트의 쿼리와 nuget.org 서비스에서 제공 하는 검색에 사용 됩니다.  자세한 내용은 [시험판 버전](../create-packages/prerelease-packages.md)의 NuGet 문서에서 찾을 수 있습니다.

## <a name="known-issues"></a>알려진 문제

* **문제:** Windows 10 v1511 사용자는 다음과 같은 시나리오에서 Visual Studio의 Powershell을 통해 문제 또는 Visual Studio 충돌이 발생할 수 있습니다.
    * install.ps1/uninstall.ps1 스크립트를 포함 하는 패키지 설치/제거
    * init.ps1 스크립트가 있는 프로젝트 로드 (예: EntityFramework)
    * 웹 콘텐츠 게시

* **해결 방법:** Windows 10 install에 최신 패치가 적용 되어 있는지 확인 합니다. expecially 1 월 2016 (KB 3124263) 이상 업데이트입니다.  자세한 내용은 [GitHub 문제](http://github.com/nuget/home/issues/1638) 에서 확인할 수 있습니다 #1638

* **문제:** NuGet v2 프로토콜 리디렉션이 끊어집니다.
대체 호스트에 요청을 리디렉션하는 사용자 지정 NuGet 리포지토리에서 리디렉션 요청을 인식하지 못합니다.
* **해결 방법:**  이 문제를 해결 하려면 리디렉션된 서버 위치를 가리키도록 설정에서 패키지 리포지토리 URI를 구성 합니다.
자세한 내용은 [GitHub 끌어오기 요청 #387](https://github.com/NuGet/NuGet.Client/pull/387)을 참조 하세요.

Microsoft는 GitHub 문제 목록에서 다음 위치에 있는 문제를 계속 추적 합니다. [http://github.com/nuget/home/issues](http://github.com/nuget/home/issues)