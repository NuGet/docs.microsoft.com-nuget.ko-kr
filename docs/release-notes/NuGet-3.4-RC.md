---
title: NuGet 3.4 RC 릴리스 정보
description: NuGet 3.4 RC 알려진된 문제, 버그 수정, 추가 된 기능 및 Dcr 포함에 대 한 릴리스 정보입니다.
author: karann-msft
ms.author: karann
ms.date: 11/11/2016
ms.topic: conceptual
ms.openlocfilehash: 795bdcfaa2e22447856b60d05807aeb0992cdfa0
ms.sourcegitcommit: 1d1406764c6af5fb7801d462e0c4afc9092fa569
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 09/04/2018
ms.locfileid: "43546756"
---
# <a name="nuget-34-rc-release-notes"></a>NuGet 3.4 RC 릴리스 정보

[NuGet 3.3 릴리스 정보](../release-notes/nuget-3.3.md) | [NuGet 3.4 릴리스 정보](../release-notes/nuget-3.4.md)

NuGet 3.4 RC Visual Studio 2015 업데이트 2 RC와 함께 2016 년 3 월 3 일에 릴리스 되었으며 머리에 몇 가지 개념을 사용 하 여 빌드된:

* 플랫폼 간 지원
* 성능 향상
* 보조 UI 개선 사항

다음 기능은 수 더 3.4 최종 릴리스에 대 한 계획 된이 RC에서 사용할 수 있습니다.

## <a name="new-features"></a>새 기능

* NuGet 클라이언트는 이제 gzip 콘텐츠 인코딩 리포지토리에서 지원
* Xproj 프로젝트에서 패키지의 Pdb에 대 한 지원
* ContentFiles 요소에서 작업을 iOS 및 Android 빌드에 대 한 지원
* Netstandard 및 netstandardapp 프레임 워크 모니커 지원

## <a name="new-user-interface-features"></a>새로운 사용자 인터페이스 기능

* 설치 됨, 업데이트 및 통합 탭에서 특히 중요 한 성능 향상
* 설치 하 고 이제 업데이트 탭은 사전순으로 정렬
* 검색을 새로 고칠 수 있도록 새로 고침 단추를 추가 합니다.

## <a name="updates-and-improvements"></a>업데이트 및 향상 된 기능

* 참조 된 패키지 `project.json` 부동 있는 버전 모든 빌드에 대해 업데이트 되지 것입니다. 대신, 복원, 정리, 다시 작성 하거나 수정 해야 하는 경우에 업데이트 됩니다 `project.json`합니다.
* nuget.org 리포지토리 소스는 NuGet 구성 UI를 사용 하는 경우 프로젝트 구성에 더 이상 강제 됩니다.
* NuGet에 더 이상 공유 프로젝트에서 패키지를 복원 하거나 잠금 파일을 씁니다.
* 향상 되었습니다. 네트워크 오류가 발생 하 고 연결할 수 없거나 응답 속도가 느린 서버에 대 한 처리를 다시 시도 하세요.
* Visual Studio 패키지 관리자 UI에서 키보드 및 마우스 동작 개선 되었습니다.
* 이제 최신 지원 `project.json` 스키마 DNX에서.

## <a name="known-issues"></a>알려진 문제

찾을 수 있는 GitHub 문제 목록에서 문제를 추적 하려면 계속 합니다. [http://github.com/nuget/home/issues](http://github.com/nuget/home/issues)