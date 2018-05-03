---
title: NuGet 3.4 RC 릴리스 정보
description: NuGet 3.4 RC 알려진된 문제, 버그 수정, 추가 된 기능 및 Dcr를 포함 하 여에 대 한 릴리스 정보입니다.
author: karann-msft
ms.author: karann
manager: unnir
ms.date: 11/11/2016
ms.topic: conceptual
ms.openlocfilehash: e40d685a5256fdfee818f0cc1f1bc352c698f3c2
ms.sourcegitcommit: 3eab9c4dd41ea7ccd2c28bb5ab16f6fbbec13708
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/26/2018
---
# <a name="nuget-34-rc-release-notes"></a>NuGet 3.4 RC 릴리스 정보

[NuGet 3.3 릴리스 정보](../release-notes/nuget-3.3.md) | [NuGet 3.4 릴리스 정보](../release-notes/nuget-3.4.md)

NuGet 3.4 RC Visual Studio 2015 업데이트 2 RC와 함께 2016 년 3 월 3 일에 릴리스된 및 사람들에 몇 가지 개념을 사용 하 여 빌드한 되었습니다.

* 크로스 플랫폼 지원
* 성능 향상
* 보조 UI 개선 사항

다음 기능은이 RC에서 사용할 수 있는 3.4 최종 릴리스에 계획입니다.

## <a name="new-features"></a>새 기능

* NuGet 클라이언트가 gzip 콘텐츠 인코딩 저장소에서 이제 지원
* Xproj 프로젝트에서 패키지의 Pdb에 대 한 지원
* IOS 및 Android 빌드 작업에서 콘텐츠 파일 요소에 대 한 지원
* Netstandard 및 netstandardapp 프레임 워크 모니커에 대 한 지원

## <a name="new-user-interface-features"></a>새로운 사용자 인터페이스 기능

* 설치 됨, 업데이트 및 통합 탭에 특히 중요 한 성능 향상
* 설치 및 업데이트 탭 이제 사전순으로 정렬 됩니다.
* 검색을 새로 고칠 수 있도록 새로 고침 단추를 추가 합니다.

## <a name="updates-and-improvements"></a>업데이트 및 향상 기능

* 패키지에서 참조 `project.json` 부동 있는 버전 모든 빌드에 대해 업데이트 되지 것입니다. 대신, 복원, 정리, 다시 작성 또는 수정 해야 하는 경우에 업데이트 됩니다 `project.json`합니다.
* nuget.org 리포지토리 소스는 NuGet 구성 UI를 사용 하는 경우 프로젝트 구성에 더 이상 강제 됩니다.
* NuGet에 더 이상 공유 프로젝트의 패키지를 복원 하거나 잠금 파일을 씁니다.
* 네트워크 오류를 개선 했습니다 하 고 연결할 수 없거나 대 한 느린 응답 서버에 대 한 처리를 다시 시도 하십시오.
* Visual Studio 패키지 관리자 UI에서 키보드 및 마우스 동작 개선 되었습니다.
* 이제 최신 지원 `project.json` DNX의 스키마입니다.

## <a name="known-issues"></a>알려진 문제

찾을 수 있는 GitHub 문제 목록에서 문제 추적 계속 합니다. [http://github.com/nuget/home/issues](http://github.com/nuget/home/issues)