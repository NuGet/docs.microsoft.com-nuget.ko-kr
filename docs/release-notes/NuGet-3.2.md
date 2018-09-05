---
title: NuGet 3.2 릴리스 정보
description: 알려진된 문제, 버그 수정, 추가 된 기능 및 Dcr 포함 하 여 NuGet 3.2에 대 한 릴리스 정보입니다.
author: karann-msft
ms.author: karann
ms.date: 11/11/2016
ms.topic: conceptual
ms.openlocfilehash: 5bdd2aa5621eead9ce79794052663cc2f8a63d45
ms.sourcegitcommit: 1d1406764c6af5fb7801d462e0c4afc9092fa569
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 09/04/2018
ms.locfileid: "43549524"
---
# <a name="nuget-32-release-notes"></a>NuGet 3.2 릴리스 정보

[NuGet 3.2 RC 릴리스 정보](../release-notes/nuget-3.2-RC.md) | [NuGet 3.2.1 릴리스 정보](../release-notes/nuget-3.2.1.md)

NuGet 3.2 릴리스된 향상 된 기능 및 수정 된 3.1.1 컬렉션으로 2015 년 9 월 16 년 릴리스 되며 둘 다에서 사용할 수 있습니다 [dist.nuget.org](http://dist.nuget.org/index.html) 하며 [Visual Studio 갤러리](https://marketplace.visualstudio.com/items?itemName=NuGetTeam.NuGetPackageManagerforVisualStudio2015)합니다.

## <a name="new-features"></a>새 기능

* 동일한 폴더에 상주 하는 프로젝트 다른 이제 `project.json` 각 프로젝트에 대 한 해당 폴더의 파일입니다.  각 프로젝트에 대 한 이름을 지정 합니다 `project.json` 파일 `{ProjectName}.project.json` NuGet 각 프로젝트에 대 한 해당 구성에 우선 순위를 적절 하 게 제공 됩니다.  Windows 10 도구 v1.1이 설치만 지원 됩니다 [1102](https://github.com/NuGet/Home/issues/1102)
* NuGet 클라이언트에 사용 되는 공유 글로벌 패키지 폴더의 위치를 지정 하는 전역 NUGET_PACKAGES 환경 변수를 지정 하는 지원 `project.json` Windows 10 도구 v1.1 사용 하 여 프로젝트를 관리 합니다.

## <a name="command-line-updates"></a>명령줄 업데이트

NuGet v3 서버를 지 원하는 nuget.exe 클라이언트의 첫 번째 버전 이며 관리 되는 패키지 프로젝트를 복원 하는 `project.json` 파일입니다.

이 릴리스에서 클라이언트와의 상호 작용을 개선 하기 위해 처리 된 인증 된 피드 문제의 수가 있었습니다.

* 설치 / 복원 상호 작용만-인증 된 피드로 초기 요청에 대 한 자격 증명을 제출 [1300](https://github.com/NuGet/Home/issues/1300), [456](https://github.com/NuGet/Home/issues/456)
* Push 명령은 자격 증명 구성-에서 해결 되지 않으면 [1248](https://github.com/NuGet/Home/issues/1248)
* 사용자 에이전트 및 헤더는 이제 통계 추적-위해 NuGet 리포지토리에 제출 [929](https://github.com/NuGet/Home/issues/929)

수많은 개선 사항이 더 잘 원격 NuGet 리포지토리를 사용 하는 동안 네트워크 오류를 처리 하도록 했습니다.

* 향상 된 원격 피드-연결할 수 없는 경우 오류 메시지 [1238](https://github.com/NuGet/Home/issues/1238)
* 제대로 오류 조건 발생-1을 반환 하려면 NuGet 복원 명령을 수정 [1186](https://github.com/NuGet/Home/issues/1186)
* 이제 네트워크 연결을 다시 시도 최대 HTTP 5xx 오류-시 5 회 시도 대 한 모든 200ms [1120](https://github.com/NuGet/Home/issues/1120)
* 개선 된 푸시 명령-중 서버 리디렉션 응답 처리 [1051](https://github.com/NuGet/Home/issues/1051)
* `nuget install -source` URL 또는 리포지토리 이름을 인수로-Nuget.Config는 이제 [1046](https://github.com/NuGet/Home/issues/1046)
* 누락 된 패키지를 복원 하는 동안 저장소에 위치 하지 않은 경고 대신 오류로 보고 이제는 [1038](https://github.com/NuGet/Home/issues/1038)
* Unix/Linux-시나리오용 \r\n multipartwebrequest 처리 수정 [776](https://github.com/NuGet/Home/issues/776)

다양 한 명령 사용 하 여 문제를 수정 사항이 있습니다.

* Push 명령은 GET-패키지 원본에 대해 PUT 하기 전에 더 이상 않습니다 [1237](https://github.com/NuGet/Home/issues/1237)
* 목록 표시 명령에는 더 이상 버전 번호-반복 [1185](https://github.com/NuGet/Home/issues/1185)
* 팩-빌드 인수를 사용 하 여 이제 제대로 지 원하는 C# 6.0- [1107](https://github.com/NuGet/Home/issues/1107)
* F # 프로젝트를 압축 하는 동안 수정 된 문제-Visual Studio 2015를 사용 하 여 빌드한 [1048](https://github.com/NuGet/Home/issues/1048)
* 패키지가 이미 있으면-이제 작동 하지 않습니다 복원 [1040](https://github.com/NuGet/Home/issues/1040)
* 때 향상 된 오류 메시지 `packages.config` 파일의 형식이 잘못 되었습니다- [1034](https://github.com/NuGet/Home/issues/1034)
* 상대 경로-작업-SolutionDirectory 스위치를 사용 하 여 복원 명령을 수정 [992](https://github.com/NuGet/Home/issues/992)
* 솔루션의 전반적인 업데이트-지원 하도록 업데이트 명령을 향상 [924](https://github.com/NuGet/Home/issues/924)

이 릴리스에서 해결 된 문제의 전체 목록을 NuGet GitHub에서 찾을 수 있습니다 [명령줄 마일스 톤](https://github.com/nuget/home/issues?utf8=%E2%9C%93&q=is%3Aissue+milestone%3A3.2.0-commandline+is%3Aclosed+-label%3AClosedAs%3ADuplicate)합니다.

## <a name="visual-studio-extension-updates"></a>Visual Studio 확장 업데이트

### <a name="new-features-in-visual-studio"></a>Visual Studio의 새로운 기능

* 새 상황에 맞는 메뉴 항목을 패키지 솔루션을 작성 하지 않고도 복원할 수 있도록 솔루션 노드에서 솔루션 탐색기에 추가 되었습니다 ([1274](https://github.com/NuGet/Home/issues/1274)).

![새 '패키지를 복원' 상황에 맞는 메뉴 항목](./media/NuGet-3.2/newContextMenu.png)

### <a name="updates-and-fixes-in-visual-studio"></a>업데이트 및 Visual Studio에서 수정

인증 된 피드에 대 한 수정 사항 롤업 했으며도 확장에서 해결 됩니다.  다음 인증 항목이 된 확장에도 해결 됩니다.

* 피드를 올바르게 인증 NuGet v3를 올바르게 처리 하는 이제 대신 인증 된 피드-v2 대로 [1216](https://github.com/NuGet/Home/issues/1216)
* 사용 하 여 프로젝트에 인증 자격 증명에 대 한 수정 된 요청 `project.json` v2 피드-를 사용 하 여 통신 및 [1082](https://github.com/NuGet/Home/issues/1082)

네트워크 연결에는 Visual Studio의 사용자 인터페이스는 영향을 하 고 다음 수정 프로그램을 사용 하 여이 해결 했습니다.

* 패키지 버전의 로컬 캐시의 유지 관리를 향상 [1096](https://github.com/NuGet/Home/issues/1096)
* V2 피드에-로 처리 하려는 시도가 더 이상 피드는 v3에 연결할 때 실패 동작을 변경 [1253](https://github.com/NuGet/Home/issues/1253)
* 여러 패키지 원본을-를 사용 하 여 패키지를 설치 하는 경우 설치 실패를 방지 이제 [1183](https://github.com/NuGet/Home/issues/1183)

빌드 작업을 사용 하 여 상호 작용의 처리를 개선 했습니다.

* 단일 프로젝트 실패-에 대 한 패키지를 복원 하는 경우 프로젝트를 작성 하는 이제 [1169](https://github.com/NuGet/Home/issues/1169)
* 솔루션 다시 빌드-강제로 솔루션의 다른 프로젝트에 종속 되어 있는 프로젝트에 패키지를 설치 [981](https://github.com/NuGet/Home/issues/981)
* 실패 한 패키지를 프로젝트에 제대로 롤백 변경 내용에는 설치를 수정 [1265](https://github.com/NuGet/Home/issues/1265)
* 실수로 제거를 수정 합니다 `developmentDependency` 패키지에 대 한 특성 `packages.config`  -  [1263](https://github.com/NuGet/Home/issues/1263)
* 에 대 한 호출 `install.ps1` 적절 한 이제 `$package.AssemblyReferences` 성공-개체 [1245](https://github.com/NuGet/Home/issues/1245)
* 잘못 된 상태-프로젝트는 UWP 프로젝트에서 패키지 제거 때문에 더 이상 [1128](https://github.com/NuGet/Home/issues/1128)
* 혼합 된 솔루션 `packages.config` 하 고 `project.json` 초를 요구 하지 않고 프로젝트를 올바르게 빌드하 이제 빌드 작업- [1122](https://github.com/NuGet/Home/issues/1122)
* 링크 되는지 아니면 다른 폴더-에 있는 경우 app.config 파일을 제대로 찾을 [1111](https://github.com/NuGet/Home/issues/1111), [894](https://github.com/NuGet/Home/issues/894)
* UWP 프로젝트에서 제외 된 패키지를 설치할 수 [1109](https://github.com/NuGet/Home/issues/1109)
* 솔루션은 저장 된 상태의-패키지 복원을 허용 이제 됩니다 [1081](https://github.com/NuGet/Home/issues/1081)

구성 파일 수정 된 업데이트를 처리 합니다.

* 대상 파일을 제거 하는 더 이상의 후속 빌드에서 패키지에서 제공 되는 `project.json` 관리 되는 프로젝트- [1288](https://github.com/NuGet/Home/issues/1288)
* ASP.NET 5 솔루션 빌드-중 Nuget.Config 파일을 더 이상 수정 [1201](https://github.com/NuGet/Home/issues/1201)
* 패키지 업데이트-중 버전 제약 조건이 더 이상 변경할 수 [1130](https://github.com/NuGet/Home/issues/1130)
* 잠금 파일 이제 잠긴 상태로 유지 하는 동안 빌드- [1127](https://github.com/NuGet/Home/issues/1127)
* 이제 수정 `packages.config` 하지 업데이트-중 다시 작성 및 [585](https://github.com/NuGet/Home/issues/585)

TFS 소스 제어와의 상호 작용 개선 됩니다.

* 더 이상 TFS-바인딩되는 패키지에 대 한 설치 실패 [1164](https://github.com/NuGet/Home/issues/1164), [980](https://github.com/NuGet/Home/issues/980)
* TFS 2013 통합-수 있도록 수정 된 NuGet 사용자 인터페이스 [1071](https://github.com/NuGet/Home/issues/1071)
* 패키지는 패키지 폴더에서 가져와야 제대로 복원에 대 한 참조를 수정 [1004](https://github.com/NuGet/Home/issues/1004)

마지막으로 이러한 항목이 향상 되었습니다.

* 에 대 한 로그 메시지의 자세한 정도 감소 `project.json` 관리 되는 프로젝트- [1163](https://github.com/NuGet/Home/issues/1163)
* 이제 사용자 인터페이스에서 설치 된 버전의 패키지를 제대로 표시 [1061](https://github.com/NuGet/Home/issues/1061)
* 이제 해당 nuspec에 지정 된 종속성 범위를 사용 하 여 패키지 버전이 시험판 버전의 해당 종속성이 안정적인 패키지 버전에 대 한 설치 [1304](https://github.com/NuGet/Home/issues/1304)

전체 목록은 NuGet GitHub에서 Visual Studio 확장을 찾을 수 있습니다에 대 한 해결 된 문제 [3.2 마일스 톤](https://github.com/nuget/home/issues?q=is%3Aissue+is%3Aclosed+-label%3AClosedAs%3ADuplicate+milestone%3A3.2)

## <a name="known-issues"></a>알려진 문제

찾을 수 있는 GitHub 문제 목록에서 문제를 추적 하려면 계속 합니다. [http://github.com/nuget/home/issues](http://github.com/nuget/home/issues)