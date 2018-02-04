---
title: "NuGet 3.4.2 릴리스 정보 | Microsoft Docs"
author: karann-msft
ms.author: karann-msft
manager: ghogen
ms.date: 11/11/2016
ms.topic: article
ms.prod: nuget
ms.technology: 
description: "포함 하 여 NuGet 3.4.2에 대 한 릴리스 정보는 문제, 버그 수정, 추가 된 기능 및 Dcr 알려져 있습니다."
keywords: "NuGet 3.4.2 릴리스 정보, 버그 수정, 알려진 문제, 추가 기능을 Dcr"
ms.reviewer:
- karann-msft
- unniravindranathan
ms.openlocfilehash: 892a965e67762af2ae42c2d6ee75d2838104d1c2
ms.sourcegitcommit: 4651b16a3a08f6711669fc4577f5d63b600f8f58
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 02/02/2018
---
# <a name="nuget-342-release-notes"></a>NuGet 3.4.2 릴리스 정보

[NuGet 3.4.1 릴리스 정보](../release-notes/nuget-3.4.1.md) | [NuGet 3.4.3 릴리스 정보](../release-notes/nuget-3.4.3.md)

3.4.2 NuGet 3.4는 및 3.4.1에서 식별 된 몇 가지 문제를 해결 하기 2016 년 4 월 8 일에 릴리스된 해제 합니다.

## <a name="nugetexe-342-rc-is-now-available"></a>nuget.exe 3.4.2 RC 출시 되었습니다.

Nuget.exe 3.4.2의 릴리스 후보를 다운로드할 수 있습니다 [여기](https://dist.nuget.org/index.html)합니다.

## <a name="updates-and-improvements"></a>업데이트 및 향상 기능

* 특정 시나리오에서는 여기서 상세한 종속성 그래프를 사용 하 여 패키지에 대 한 업데이트 시간이 매우 오래 걸린 하 고 Visual Studio 중지 되었습니다. 업데이트의 성능을 크게 개선 했습니다.
* 네트워크 트래픽 없이 nuget 복원 2.5-3 배 Visual Studio 내에서 더 빠른 배입니다.
* 이 변경 외에도 해결 했습니다 문제가 있는 VS UI에 계산 업데이트를 인출 하는 경우에 두 번 네트워크 적중 된 것입니다. 이 부분적으로 3.4/3.4.1 한 경험이 일부 시간 초과 문제 고객에 대 한 책임입니다.
* No_proxy 설정에 대 한 지원 추가

## <a name="fixes"></a>수정 프로그램

* 3.4.1으로 업데이트 한 후 nuget.org 소스 NuGet 설정 또는 구성에서 누락 된 문제를 해결 합니다.
* 3.4.1 FindPackagesById 대/소문자 변경 Artifactory을 중단 문제를 해결 합니다.
* FIPS nuget.exe와 NuGet 복원 오류를 발생 시킨 문제를 수정 했습니다.
* 잘못 된 아이콘 URL로 소스를 검색할 때 충돌을 수정 했습니다.
* 버전 및 ' 모든 소스 '에서 항목을 병합을 문제가 해결된 되었습니다.

## <a name="known-issues-in-342-windows-x86-commandline-rc"></a>알려진 문제 3.4.2에 Windows x86 명령줄 (RC)

이러한 문제는 다음 주 초기 RTM 도달하기 전에 수정 됩니다.

*  솔루션에 대 한 실행 중인 nuget 복원을 솔루션 파일은 프로젝트 파일 보다 더 낮은 폴더 계층 구조에 저장 하는 경우 실패 합니다.
*  Nuget delete 명령을 V2 피드를 사용 하 여 패키지 실행이 실패 합니다. V3 피드를 대신 사용 합니다.


수정 사항 및이 릴리스에서 향상 된 전체 목록은 체크 아웃 문제 목록 [여기](https://github.com/NuGet/Home/issues?utf8=%E2%9C%93&q=is%3Aissue+milestone%3A3.4.2++is%3Aclosed+)합니다.