---
title: "NuGet 3.2 릴리스 정보 | Microsoft Docs"
author: karann-msft
ms.author: karann-msft
manager: ghogen
ms.date: 11/11/2016
ms.topic: article
ms.prod: nuget
ms.technology: 
description: "알려진된 문제, 버그 수정, 추가 된 기능 및 Dcr를 포함 하 여 NuGet 3.2에 대 한 릴리스 정보입니다."
keywords: "NuGet 3.2 릴리스 정보, 버그 수정, 알려진 문제, 추가 기능을 Dcr"
ms.reviewer:
- karann-msft
- unniravindranathan
ms.openlocfilehash: 1728a5c0d83be84686e7ab1394cfc4f8f809987c
ms.sourcegitcommit: 262d026beeffd4f3b6fc47d780a2f701451663a8
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 01/25/2018
---
# <a name="nuget-32-release-notes"></a>NuGet 3.2 릴리스 정보

[NuGet 3.2 RC 릴리스 정보](../release-notes/nuget-3.2-RC.md) | [NuGet 3.2.1 릴리스 정보](../release-notes/nuget-3.2.1.md)

NuGet 3.2 릴리스된 개선 사항 및는 3.1.1에 대 한 수정 된 컬렉션으로 2015 년 9 월 16 일 놓은 둘 다에서 사용할 수 [dist.nuget.org](http://dist.nuget.org/index.html) 및 [Visual Studio 갤러리](https://marketplace.visualstudio.com/items?itemName=NuGetTeam.NuGetPackageManagerforVisualStudio2015)합니다.

## <a name="new-features"></a>새 기능

* 동일한 폴더에 거주 하는 프로젝트를 서로 다른 점이 이제 `project.json` 각 프로젝트에 해당 폴더의 파일입니다.  각 프로젝트에 대 한 이름을 `project.json` 파일 `{ProjectName}.project.json` NuGet 각 프로젝트에 대 한 해당 구성에 우선 순위를 적절 하 게 제공 됩니다.  이 Windows 10 도구 v 1.1이 설치를 지원만 [1102](https://github.com/NuGet/Home/issues/1102)
* NuGet 클라이언트에 사용 되는 공유 전역 패키지 폴더의 위치를 지정 하는 전역 NUGET_PACKAGES 환경 변수를 지정 하는 지원 `project.json` Windows 10 도구 v 1.1 사용 하 여 프로젝트를 관리 합니다.

## <a name="command-line-updates"></a>명령줄 업데이트

이 첫 번째 버전의 NuGet v3 서버를 지 원하는 nuget.exe 클라이언트 및 관리 되는 프로젝트에 대 한 패키지를 복원 하는 `project.json` 파일입니다.

다양 한 클라이언트와 상호 작용을 개선 하기 위해이 릴리스에서 주소가 지정 된 인증 된 피드 문제가 있었습니다.

* 설치 / 복원 상호 작용-인증 된 피드를 초기 요청에 대 한 자격 증명을 제출만 [1300](https://github.com/NuGet/Home/issues/1300), [456](https://github.com/NuGet/Home/issues/456)
* 푸시 명령에서 구성-자격 증명을 해결 되지 않으면 [1248](https://github.com/NuGet/Home/issues/1248)
* 사용자 에이전트 및 헤더 통계 추적-에 도움이 되도록 NuGet 리포지토리에서에 제출 이제 [929](https://github.com/NuGet/Home/issues/929)

원격 NuGet 리포지토리를 사용 하는 동안 네트워크 오류 처리 하기 위해 향상 된 기능이 다양을 내렸습니다.

* -원격 피드에 연결할 수 없는 경우 오류 메시지가 개선 [1238](https://github.com/NuGet/Home/issues/1238)
* 제대로-에 오류 조건이 발생 하는 경우 1을 반환 하려면 NuGet 복원 명령을 수정 [1186](https://github.com/NuGet/Home/issues/1186)
* 이제 네트워크 연결을 다시 시도 최대 HTTP 5xx 오류-시 5 회 시도 대 한 모든 200ms [1120](https://github.com/NuGet/Home/issues/1120)
* 서버 리디렉션 응답을 처리 중 밀어넣기 명령-향상 된 [1051](https://github.com/NuGet/Home/issues/1051)
* `nuget install -source`이제-인수로 Nuget.Config에서 URL 이나 리포지토리 이름을 지원 [1046](https://github.com/NuGet/Home/issues/1046)
* 누락 된 패키지를 복원 하는 동안 저장소에 배치 되지 않은 경고 대신 오류로 보고 이제 [1038](https://github.com/NuGet/Home/issues/1038)
* Unix/Linux 시나리오-\r\n multipartwebrequest 처리 수정 [776](https://github.com/NuGet/Home/issues/776)

다양 한 명령 사용 하 여 문제를 수정 프로그램의 여러 가지:

* Push 명령이 수행 하는 GET-패키지 소스에 대해 PUT 하기 전에 더 이상 [1237](https://github.com/NuGet/Home/issues/1237)
* 버전 번호를 더 이상 반복 하는 목록 표시 명령 [1185](https://github.com/NuGet/Home/issues/1185)
* 팩-빌드 인수와 함께 이제 제대로 지원 C# 6.0- [1107](https://github.com/NuGet/Home/issues/1107)
* F # 프로젝트를 압축할 수정 된 문제는 Visual Studio 2015-를 사용 하 여 빌드한 [1048](https://github.com/NuGet/Home/issues/1048)
* 패키지는 이미 존재-때 지금 아니요 ops 복원 [1040](https://github.com/NuGet/Home/issues/1040)
* 경우 향상 된 오류 메시지를 `packages.config` 파일 형식이 잘못 되었습니다- [1034](https://github.com/NuGet/Home/issues/1034)
* 상대 경로-작업-SolutionDirectory 스위치와 함께 복원 명령을 수정 [992](https://github.com/NuGet/Home/issues/992)
* 솔루션의 전반적인 업데이트-지원 하도록 업데이트 명령을 향상 [924](https://github.com/NuGet/Home/issues/924)

이 릴리스에서 해결 된 문제의 전체 목록은 NuGet GitHub에서 있습니다 [명령줄 마일스 톤](https://github.com/nuget/home/issues?utf8=%E2%9C%93&q=is%3Aissue+milestone%3A3.2.0-commandline+is%3Aclosed+-label%3AClosedAs%3ADuplicate)합니다.

## <a name="visual-studio-extension-updates"></a>Visual Studio 확장명 업데이트

### <a name="new-features-in-visual-studio"></a>Visual Studio의 새로운 기능

* 패키지는 솔루션을 구축 하지 않고도 복원할 수를 허용 하는 솔루션 노드에서 솔루션 탐색기에 새로운 상황에 맞는 메뉴 항목이 추가 되었습니다 ([1274](https://github.com/NuGet/Home/issues/1274)).

![새 '패키지를 복원' 상황에 맞는 메뉴 항목](./media/NuGet-3.2/newContextMenu.png)

### <a name="updates-and-fixes-in-visual-studio"></a>업데이트 및 Visual Studio에서 수정

인증 된 피드에 대 한 수정 사항 롤업 였으며도 확장에서 해결 됩니다.  다음 인증 항목 확장에도 해결 않은:

* 이제 피드를 적절 하 게 인증 NuGet v3를 올바르게 처리 하는 방법 대신 v2 피드-인증 된 것으로 [1216](https://github.com/NuGet/Home/issues/1216)
* 사용 하 여 프로젝트에서 인증 자격 증명에 대 한 수정 된 요청 `project.json` 및 v2 피드-와 통신 [1082](https://github.com/NuGet/Home/issues/1082)

네트워크 연결에 Visual Studio의 사용자 인터페이스에 영향을 받는 하 고 다음 수정 프로그램으로이 주소를 지정 했습니다.

* 패키지 버전-컴퓨터의 로컬 캐시에 유지 관리를 향상 [1096](https://github.com/NuGet/Home/issues/1096)
* 피드를-v2 피드로 처리 하려는 시도가 더 이상 v3에 연결할 때 실패 동작을 변경 [1253](https://github.com/NuGet/Home/issues/1253)
* 여러 패키지 소스가-포함 된 패키지를 설치할 때 설치 오류를 방지 이제 [1183](https://github.com/NuGet/Home/issues/1183)

빌드 작업와의 상호 작용의 처리를 개선 했습니다.

* 단일 프로젝트 실패-에 대 한 패키지를 복원 하는 경우 프로젝트를 작성을 이제 [1169](https://github.com/NuGet/Home/issues/1169)
* 솔루션 다시 빌드-강제로 패키지를 설치 하면 솔루션의 다른 프로젝트에 의존 하는 프로젝트에 [981](https://github.com/NuGet/Home/issues/981)
* 제대로 변경 내용을 롤백하고 프로젝트-실패 한 패키지 설치를 수정 했습니다. [1265](https://github.com/NuGet/Home/issues/1265)
* 실수로 제거 수정 된 `developmentDependency` 특성에서 패키지에 `packages.config`  -  [1263](https://github.com/NuGet/Home/issues/1263)
* 에 대 한 호출이 `install.ps1` 적절 한 생깁니다 `$package.AssemblyReferences` -전달 된 개체가 [1245](https://github.com/NuGet/Home/issues/1245)
* -잘못 된 상태에는 프로젝트를 UWP 프로젝트에서 패키지의 제거 인해 더 이상 [1128](https://github.com/NuGet/Home/issues/1128)
* 혼합 되어 있는 솔루션 `packages.config` 및 `project.json` 프로젝트가 제대로 두 번째 요구 하지 않고 빌드 이제 빌드 작업- [1122](https://github.com/NuGet/Home/issues/1122)
* 링크 되는지 아니면 다른 폴더-에 있는 경우 app.config 파일을 제대로 찾기 [1111](https://github.com/NuGet/Home/issues/1111), [894](https://github.com/NuGet/Home/issues/894)
* UWP 프로젝트에서는 이제-목록에 없는 패키지를 설치할 수 [1109](https://github.com/NuGet/Home/issues/1109)
* 패키지를 복원이 허용 되지-저장 된 상태의 솔루션이 없을 때 [1081](https://github.com/NuGet/Home/issues/1081)

파일 수정 된 구성에 대 한 업데이트를 처리 합니다.

* 이후 빌드 패키지에서 배달 대상 파일을 제거 하는 더 이상는 `project.json` 관리 되는 프로젝트- [1288](https://github.com/NuGet/Home/issues/1288)
* ASP.NET 5 솔루션 빌드-중 Nuget.Config 파일을 더 이상 수정 [1201](https://github.com/NuGet/Home/issues/1201)
* 패키지 업데이트-중 버전 제약 조건을 더 이상 변경할 수 [1130](https://github.com/NuGet/Home/issues/1130)
* 잠금 파일을 계속 잠긴-빌드하는 동안 [1127](https://github.com/NuGet/Home/issues/1127)
* 이제 수정 `packages.config` 하지 업데이트-중 다시 작성해 [585](https://github.com/NuGet/Home/issues/585)

TFS 소스 제어와의 상호 작용에 맞게 개선 됩니다.

* -TFS에 연결 된 패키지에 대 한 설치를 더 이상 실패 [1164](https://github.com/NuGet/Home/issues/1164), [980](https://github.com/NuGet/Home/issues/980)
* TFS 2013 통합-수 있도록 수정 된 NuGet 사용자 인터페이스 [1071](https://github.com/NuGet/Home/issues/1071)
* 패키지를 제대로 패키지 폴더-에서 온 것으로 복원에 대 한 참조를 수정 했습니다. [1004](https://github.com/NuGet/Home/issues/1004)

마지막으로, 우리 향상 되었습니다. 이러한 항목:

* 에 대 한 로그 메시지의 자세한 정도 감소 `project.json` 관리 되는 프로젝트- [1163](https://github.com/NuGet/Home/issues/1163)
* 이제 사용자 인터페이스-에 설치 된 버전의 패키지를 제대로 표시 [1061](https://github.com/NuGet/Home/issues/1061)
* 이제 해당 nuspec에 지정 된 종속성 범위를 사용 하 여 패키지 설치에 대 한 안정적인 패키지 버전-해당 종속성을 시험판 버전을 보유 [1304](https://github.com/NuGet/Home/issues/1304)

Visual Studio extension NuGet GitHub에서 찾을 수 있습니다에 대 한 처리 문제의 전체 목록은 [3.2 마일스 톤](https://github.com/nuget/home/issues?q=is%3Aissue+is%3Aclosed+-label%3AClosedAs%3ADuplicate+milestone%3A3.2)

## <a name="known-issues"></a>알려진 문제

찾을 수 있는 GitHub 문제 목록에서 문제를 추적 하려면 계속 하기: [http://github.com/nuget/home/issues](http://github.com/nuget/home/issues)