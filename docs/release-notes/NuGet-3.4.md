---
title: NuGet 3.4 릴리스 정보
description: 알려진된 문제, 버그 수정, 추가 된 기능 및 Dcr를 포함 하 여 NuGet 3.4에 대 한 릴리스 정보입니다.
author: karann-msft
ms.author: karann
manager: unnir
ms.date: 11/11/2016
ms.topic: conceptual
ms.openlocfilehash: 3f2a945b628022bdcc6e69a7a4b1be6c53b65626
ms.sourcegitcommit: 3eab9c4dd41ea7ccd2c28bb5ab16f6fbbec13708
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/26/2018
ms.locfileid: "31820474"
---
# <a name="nuget-34-release-notes"></a>NuGet 3.4 릴리스 정보

[NuGet 3.4 RC 릴리스 정보](../release-notes/nuget-3.4-RC.md) | [NuGet 3.4.1 릴리스 정보](../release-notes/nuget-3.4.1.md)

NuGet 3.4 2016 년 3 월 30 일의 Visual Studio 2015 업데이트 2 및 Visual Studio 15 Preview 릴리스 일환으로 릴리스 되었습니다 및 사람들에 몇 가지 개념을 사용 하 여 빌드한 되었습니다.

* 크로스 플랫폼 지원
* 성능 향상
* 보조 UI 개선 사항

다음과 같은 기능 RC에서 이전에 추가 된 및 업데이트 되었거나 3.4 릴리스에 대 한 완료 되었습니다.

## <a name="new-features"></a>새 기능

* NuGet 클라이언트가 gzip 콘텐츠 인코딩 저장소에서 이제 지원
* Xproj 프로젝트에서 패키지의 Pdb에 대 한 지원
* IOS 및 Android 빌드 작업에서 콘텐츠 파일 요소에 대 한 지원
* Netstandard 및 netstandardapp 프레임 워크 모니커에 대 한 지원

## <a name="new-user-interface-features"></a>새로운 사용자 인터페이스 기능

* 설치 됨, 업데이트 및 통합 탭에 특히 중요 한 성능 향상
* 집계 ' 모든 패키지 소스 ' 소스를 적절 한 검색 결과 병합을 사용할 수
* 설치 및 업데이트 탭 이제 사전순으로 정렬 됩니다.
* 검색을 새로 고칠 수 있도록 새로 고침 단추를 추가 합니다.
* 버전 목록 맨 위에 있는 최신 빌드 옵션

## <a name="updates-and-improvements"></a>업데이트 및 향상 기능

* 패키지에서 참조 `project.json` 부동 있는 버전 모든 빌드에 대해 업데이트 되지 것입니다. 대신, 복원, 정리, 다시 작성 또는 수정 해야 하는 경우에 업데이트 됩니다 `project.json`합니다.
* nuget.org 리포지토리 소스는 NuGet 구성 UI를 사용 하는 경우 프로젝트 구성에 더 이상 강제 됩니다.
* NuGet에 더 이상 공유 프로젝트의 패키지를 복원 하거나 잠금 파일을 씁니다.
* 네트워크 오류를 개선 했습니다 하 고 연결할 수 없거나 대 한 느린 응답 서버에 대 한 처리를 다시 시도 하십시오.
* Visual Studio 패키지 관리자 UI에서 키보드 및 마우스 동작 개선 되었습니다.
* 이제 최신 지원 `project.json` DNX의 스키마입니다.

## <a name="breaking-changes"></a>주요 변경 사항

* 패키지 버전 번호 형식으로 정규화 된 이제은 *주요*. *사소한*. *패치*-*시험판* 패치 및 사소한, 각각의 주 버전, 정수로 처리 되 고 모든 앞에 오는 0을 삭제 합니다.  시험판 정보를 문자열로 취급 되며 및에 적용 된 변경 내용이 없습니다. 이러한 번호는 NuGet 클라이언트 및 nuget.org 서비스에서 제공 된 검색에 쿼리에서 사용 됩니다.  자세한 내용은 아래에서 NuGet 문서에서 확인할 수 있습니다 [시험판 버전](../create-packages/prerelease-packages.md)합니다.

## <a name="known-issues"></a>알려진 문제

* **문제:** 문제 또는 심지어는 Visual Studio 충돌 Visual Studio에서 Powershell과 함께 다음과 같은 시나리오에서 Windows 10 v1511 사용자가 발생할 수 있습니다.
    * Install.ps1 있는 패키지를 제거 / 설치 / uninstall.ps1 스크립트
    * Init.ps1 스크립트가 (예: EntityFramework) 프로젝트를 로드 합니다.
    * 웹 콘텐츠 게시

* **해결 방법:** 귀하의 Windows 10 설치에 적용 된 최신 패치, expecially 2016 년 1 월 (KB 3124263) 또는 이후 업데이트가 있는지 확인 합니다.  자세한 내용은에서 사용할 수 있는 [GitHub 문제 #1638](http://github.com/nuget/home/issues/1638)

* **문제:** NuGet v2 프로토콜 리디렉션이 끊어집니다.
대체 호스트에 요청을 리디렉션하는 사용자 지정 NuGet 리포지토리에서 리디렉션 요청을 인식하지 못합니다.
* **해결 방법:** 이 문제를 해결 하려면 리디렉션된 서버 위치를 가리키도록 설정에서 패키지 리포지토리 URI를 구성 합니다.
자세한 내용은 참조 [GitHub 끌어오기 요청 #387](https://github.com/NuGet/NuGet.Client/pull/387)합니다.

찾을 수 있는 GitHub 문제 목록에서 문제 추적 계속 합니다. [http://github.com/nuget/home/issues](http://github.com/nuget/home/issues)