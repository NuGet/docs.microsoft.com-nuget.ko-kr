---
title: NuGet 3.2 RC 릴리스 정보
description: 알려진 문제, 버그 수정, 추가 된 기능 및 Ecrs를 포함 하는 NuGet 3.2 RC에 대 한 릴리스 정보입니다.
author: JonDouglas
ms.author: jodou
ms.date: 11/11/2016
ms.topic: conceptual
ms.openlocfilehash: 8132affb8273604ae79d4e1f85e6072d8eaf5ad6
ms.sourcegitcommit: ee6c3f203648a5561c809db54ebeb1d0f0598b68
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 01/26/2021
ms.locfileid: "98780297"
---
# <a name="nuget-32-rc-release-notes"></a>NuGet 3.2 RC 릴리스 정보

[NuGet 3.1.1 릴리스 정보](../release-notes/nuget-3.1.1.md)  |  [NuGet 3.2 릴리스 정보](../release-notes/nuget-3.2.md)

NuGet 3.2 릴리스 후보는 3.1.1 릴리스에 대 한 개선 사항 및 수정 사항 모음으로 2015 년 9 월 2 일에 출시 되었습니다.  또한 이러한 릴리스는 먼저 새 dist.nuget.org 리포지토리에 게시 되는 첫 번째 릴리스입니다.

## <a name="new-features"></a>새로운 기능

* 이제 동일한 폴더에 있는 프로젝트 `project.json` 는 각 프로젝트에 따라 해당 폴더에 서로 다른 파일을 포함할 수 있습니다.  각 프로젝트에 대해 파일 이름 `project.json` `{ProjectName}.project.json` 및 NuGet은 적절 하 게 참조 하 고 각 프로젝트에 대해 해당 콘텐츠를 적절 하 게 사용 합니다.  이는 새로운 기능 [1102](https://github.com/NuGet/Home/issues/1102) 를 지원 합니다.
* `NuGet.Config` 이제 globalPackagesFolder을 상대 경로로 지원 합니다.- [1062](https://github.com/NuGet/Home/issues/1062)

## <a name="command-line-updates"></a>명령줄 업데이트

이는 NuGet v3 서버를 지원 하 고 파일로 관리 되는 프로젝트에 대 한 패키지를 복원 하는 nuget.exe 클라이언트의 첫 번째 버전입니다 `project.json` .

#### <a name="there-were-a-number-of-authenticated-feed-issues-that-were-addressed-in-this-release-to-improve-interactions-with-the-client"></a>이 릴리스에서는 클라이언트와의 상호 작용을 개선 하기 위해 해결 된 여러 가지 인증 된 피드 문제가 있었습니다.

* 설치/복원 상호 작용은 인증 된 피드에 대 한 초기 요청에 대 한 자격 증명 ( [1300](https://github.com/NuGet/Home/issues/1300), [456](https://github.com/NuGet/Home/issues/456) )만 제출 합니다.
* 밀어넣기 명령이 구성에서 자격 증명을 확인 하지 않음- [1248](https://github.com/NuGet/Home/issues/1248)
* 이제 사용자 에이전트와 헤더가 통계 추적을 지원 하기 위해 NuGet 리포지토리로 제출 됩니다.- [929](https://github.com/NuGet/Home/issues/929)

#### <a name="we-made-a-number-of-improvements-to-better-handle-network-failures-while-attempting-to-work-with-a-remote-nuget-repository"></a>원격 NuGet 리포지토리를 사용 하 여 작업을 시도 하는 동안 네트워크 오류를 더 효과적으로 처리할 수 있도록 몇 가지 기능이 향상 되었습니다.

* 원격 피드에 연결할 수 없는 경우의 향상 된 오류 메시지- [1238](https://github.com/NuGet/Home/issues/1238)
* 오류 조건이 발생 하는 경우 1을 올바르게 반환 하도록 NuGet 복원 명령을 수정 했습니다.- [1186](https://github.com/NuGet/Home/issues/1186)
* 이제 HTTP 5xx 오류가 발생 한 경우 최대 5 회 시도에 대해 200ms 마다 네트워크 연결을 다시 시도 합니다.- [1120](https://github.com/NuGet/Home/issues/1120)
* 밀어넣기 명령 중 서버 리디렉션 응답의 향상 된 처리- [1051](https://github.com/NuGet/Home/issues/1051)
* `nuget install -source` 에서는 이제 Nuget.Config의 URL 또는 리포지토리 이름을 인수로 지원 합니다.- [1046](https://github.com/NuGet/Home/issues/1046)
* 복원 중 리포지토리에 없는 누락 된 패키지는 이제 경고 [1038](https://github.com/NuGet/Home/issues/1038) 대신 오류로 보고 됩니다.
* Unix/Linux 시나리오에 대 한 \r\n의 multipartwebrequest 처리를 수정 했습니다.- [776](https://github.com/NuGet/Home/issues/776)

#### <a name="there-are-a-number-of-fixes-to-issues-with-various-commands"></a>다양 한 명령에 대 한 여러 가지 해결 방법이 있습니다.

* 푸시 명령은 패키지 소스에 대 한 PUT 이전에 더 이상 GET을 수행 하지 않습니다.- [1237](https://github.com/NuGet/Home/issues/1237)
* 목록 명령이 더 이상 버전 번호를 반복 하지 않음- [1185](https://github.com/NuGet/Home/issues/1185)
* -Build 인수를 사용 하는 Pack은 이제 c # 6.0- [1107](https://github.com/NuGet/Home/issues/1107) 을 올바르게 지원 합니다.
* Visual Studio 2015- [1048](https://github.com/NuGet/Home/issues/1048) 로 빌드된 F # 프로젝트를 압축 하는 데 문제가 해결 되었습니다.
* 패키지가 이미 있는 경우 지금 복원-- [1040](https://github.com/NuGet/Home/issues/1040)
* 파일의 형식이 잘못 된 경우 오류 메시지가 개선 `packages.config` 됨- [1034](https://github.com/NuGet/Home/issues/1034)
* 상대 경로를 사용 하 여 작동 하도록 스위치를 사용 하 여 복원 명령 수정 `-SolutionDirectory` - [992](https://github.com/NuGet/Home/issues/992)
* 솔루션 전체 업데이트를 지원 하도록 업데이트 된 명령 개선- [924](https://github.com/NuGet/Home/issues/924)

이 릴리스에서 해결 된 문제에 대 한 전체 목록은 NuGet GitHub [명령줄 마일스 톤](https://github.com/nuget/home/issues?utf8=%E2%9C%93&q=is%3Aissue+milestone%3A3.2.0-commandline+is%3Aclosed+-label%3AClosedAs%3ADuplicate)에서 찾을 수 있습니다.

## <a name="visual-studio-extension-updates"></a>Visual Studio 확장 업데이트

### <a name="new-features-in-visual-studio"></a>Visual Studio의 새로운 기능

* 솔루션을 빌드하지 않고 패키지를 복원할 수 있는 새로운 상황에 맞는 메뉴 항목이 솔루션 노드의 솔루션 탐색기에 추가 되었습니다 ([1274](https://github.com/NuGet/Home/issues/1274)).

![새 ' 패키지 복원 ' 상황에 맞는 메뉴 항목](./media/NuGet-3.2/newContextMenu.png)

### <a name="updates-and-fixes-in-visual-studio"></a>Visual Studio의 업데이트 및 수정

#### <a name="the-fixes-for-authenticated-feeds-were-rolled-up-and-addressed-in-the-extension-as-well--the-following-authentication-items-were-also-addressed-in-the-extension"></a>인증 된 피드에 대 한 픽스도 확장 및 해결 되었습니다.  다음 인증 항목도 확장에서 처리 됩니다.

* 이제 v2 인증 된 피드- [1216](https://github.com/NuGet/Home/issues/1216) 대신 NuGet v3 인증 된 피드를 올바르게 처리 합니다.
* 를 사용 하 여 프로젝트에서 인증 자격 증명에 대 한 요청을 수정 `project.json` 했으며 v2 피드와 통신- [1082](https://github.com/NuGet/Home/issues/1082)

#### <a name="network-connectivity-had-affected-the-user-interface-in-visual-studio-and-we-addressed-this-with-the-following-fixes"></a>네트워크 연결이 Visual Studio의 사용자 인터페이스에 영향을 준 것 이며,이 문제는 다음 수정 사항으로 해결 되었습니다.

* 패키지 버전의 로컬 캐시 유지 관리 향상- [1096](https://github.com/NuGet/Home/issues/1096)
* V3 피드에 연결 하 여 더 이상 v2 피드로 처리 하려고 시도 하지 않는 경우 실패 동작이 변경 되었습니다.- [1253](https://github.com/NuGet/Home/issues/1253)
* 이제 여러 패키지 소스가 포함 된 패키지를 설치할 때 설치 오류가 방지 됩니다.- [1183](https://github.com/NuGet/Home/issues/1183)

빌드 작업과의 상호 작용에 대 한 처리가 개선 되었습니다.

* 단일 프로젝트에 대 한 패키지를 복원 하지 못하면 이제 프로젝트 빌드를 계속 합니다.- [1169](https://github.com/NuGet/Home/issues/1169)
* 솔루션의 다른 프로젝트에 종속 된 프로젝트에 패키지를 설치 하면 솔루션 다시 빌드를 강제로 적용 합니다.- [981](https://github.com/NuGet/Home/issues/981)
* 프로젝트에 대 한 변경 내용을 제대로 롤백하기 위해 실패 한 패키지 설치 수정- [1265](https://github.com/NuGet/Home/issues/1265)
* `developmentDependency`1263에서 패키지에 대 한 특성의 실수로 제거 `packages.config`  -  [](https://github.com/NuGet/Home/issues/1263) 를 수정 했습니다.
* 이제에 대 한 호출에 `install.ps1` 적절 한 `$package.AssemblyReferences` 개체가 전달 되었습니다.- [1245](https://github.com/NuGet/Home/issues/1245)
* 프로젝트가 잘못 된 상태에 있는 동안 UWP 프로젝트에서 패키지를 제거 하는 것을 더 이상 방지 하지 않음- [1128](https://github.com/NuGet/Home/issues/1128)
* `packages.config` `project.json` 이제 두 번째 빌드 작업 없이도 및 프로젝트를 포함 하는 솔루션이 제대로 빌드됩니다. [1122](https://github.com/NuGet/Home/issues/1122)
* app.config 파일이 연결 되어 있거나 다른 폴더 ( [1111](https://github.com/NuGet/Home/issues/1111), [894](https://github.com/NuGet/Home/issues/894) )에 있는 경우 적절 하 게 찾기
* UWP 프로젝트에서 목록에 없는 패키지를 설치할 수 있음- [1109](https://github.com/NuGet/Home/issues/1109)
* 솔루션이 저장 된 상태가 아닌 동안 패키지 복원이 허용 됨- [1081](https://github.com/NuGet/Home/issues/1081)


구성 파일에 대 한 업데이트 처리가 수정 되었습니다.

* 관리 되는 프로젝트의 후속 빌드에서 패키지에서 배달 된 대상 파일을 더 이상 제거 하지 않음 `project.json` - [1288](https://github.com/NuGet/Home/issues/1288)
* ASP.NET 5 솔루션 빌드 중에 Nuget.Config 파일을 더 이상 수정 하지 않음- [1201](https://github.com/NuGet/Home/issues/1201)
* 패키지 업데이트 중에 허용 되는 버전 제약 조건을 더 이상 변경 하지 않음- [1130](https://github.com/NuGet/Home/issues/1130)
* 잠금 파일은 이제 빌드 중에 잠긴 상태로 유지 됩니다.- [1127](https://github.com/NuGet/Home/issues/1127)
* `packages.config`업데이트 중에 다시 작성 하지 않고 수정 하 고 있습니다.- [585](https://github.com/NuGet/Home/issues/585)


TFS 원본 제어와의 상호 작용이 향상 되었습니다.

* TFS- [1164](https://github.com/NuGet/Home/issues/1164), [980](https://github.com/NuGet/Home/issues/980) 에 바인딩되는 패키지에 대 한 설치에 더 이상 실패 하지 않음
* TFS 2013 통합을 허용 하도록 NuGet 사용자 인터페이스를 수정 했습니다.- [1071](https://github.com/NuGet/Home/issues/1071)
* 패키지 폴더에서 제대로 가져오도록 복원 된 패키지에 대 한 참조가 수정 되었습니다.- [1004](https://github.com/NuGet/Home/issues/1004)

마지막으로 다음 항목도 향상 시켰습니다.

* 관리 되는 프로젝트에 대해 축소 된 로그 메시지의 자세한 정도 `project.json` - [1163](https://github.com/NuGet/Home/issues/1163)
* 이제 사용자 인터페이스에 설치 된 패키지 버전을 올바르게 표시- [1061](https://github.com/NuGet/Home/issues/1061)


Visual Studio 확장에 대해 해결 된 문제의 전체 목록은 NuGet GitHub [3.2 마일스 톤](https://github.com/nuget/home/issues?q=is%3Aissue+is%3Aclosed+-label%3AClosedAs%3ADuplicate+milestone%3A3.2) 에서 찾을 수 있습니다.

## <a name="known-issues"></a>알려진 문제

Microsoft는 GitHub 문제 목록에서 다음 위치에 있는 문제를 계속 추적 합니다. [http://github.com/nuget/home/issues](http://github.com/nuget/home/issues)