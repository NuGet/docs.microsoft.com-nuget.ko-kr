---
title: NuGet 5.7 릴리스 정보
description: 새 기능, 버그 수정 및 Ecrs를 비롯 한 NuGet 5.7에 대 한 릴리스 정보입니다.
author: chgill-msft
ms.author: chgill
ms.date: 8/14/2020
ms.topic: conceptual
ms.openlocfilehash: 6c821091983ab0b5d59b759e1ee9930cf449fd9d
ms.sourcegitcommit: 6cda91f135e58cf57a2471b0c7c4a2f748f40024
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 09/02/2020
ms.locfileid: "89364155"
---
# <a name="nuget-57-release-notes"></a>NuGet 5.7 릴리스 정보

NuGet 배포 차량:

| NuGet 버전 | Visual Studio 버전에서 사용 가능 | .NET SDK에서 사용 가능 |
|:---|:---|:---|
| [**5.7.0 이상이 필요**](https://nuget.org/downloads) | [Visual Studio 2019 버전 16.7](https://visualstudio.microsoft.com/downloads/) | [3.1.401](https://dotnet.microsoft.com/download/dotnet-core/3.1)<sup>1</sup> |

<sup>1</sup> .net Core 워크 로드와 함께 Visual Studio 2019와 함께 설치 됨

## <a name="summary-whats-new-in-57"></a>요약: 5.7의 새로운 기능

### <a name="features-added-in-this-release"></a>이 릴리스에 추가 된 기능

* NuGet 패키지 참조에 대 한 extern 별칭 지원이 추가 됨- [#4989](https://github.com/NuGet/Home/issues/4989)

* 데이터 원본을 공유 하 고 resfreshing를 줄이는 것을 허용 하 여 설치 된 탭과 업데이트 탭 간의 전환을 더 빠르게 수행 했습니다. [#8294](https://github.com/NuGet/Home/issues/8294)

* MSBuild 정적 그래프 api (dotnet.exe [#9644](https://github.com/NuGet/Home/issues/9644) )를 호출 하 여 신속한 복원 속도 평가

* PackageReference 프로젝트에 대 한 Visual Studio 부분 복원 추가 (op + +)- [#9513](https://github.com/NuGet/Home/issues/9513)

* Visual Studio 패키지 관리자 UI는 HTTP 요청당 요청 된 수를 초과 하 여 반환 되는 오동작 패키지 원본을 검색할 때 자주 중단 됩니다. - [#8478](https://github.com/NuGet/Home/issues/8478)

* VS 복원에서 비 SDK 스타일 프로젝트에 대 한 PackageVersion 정보 통합이 추가 됨- [#9236](https://github.com/NuGet/Home/issues/9236)

* nuget.exe 업데이트에 대 한 지원이 추가 되었습니다 `-self -Source` https://feed  -  [#1783](https://github.com/NuGet/Home/issues/1783)

* %APPDATA%\NuGet 디렉터리- [#9394](https://github.com/NuGet/Home/issues/9394) 에 여러 구성 파일에 대 한 지원이 추가 되었습니다.

* DeterministicSourcePaths는 이제 NuGet 원본 패키지를 계정으로 사용 합니다. [#9431](https://github.com/NuGet/Home/issues/9431)

* INuGetProjectService를 추가 했습니다. GetInstalledPackagesAsync 확장성 API- [#9702](https://github.com/NuGet/Home/issues/9702)

* 솔루션/프로젝트를 요구 하지 않고 대체 폴더를 열거 하는 interop API를 추가 [#9395](https://github.com/NuGet/Home/issues/9395)

* `latest`#8808에 대 한 옵션이 추가 됨 `-MSBuildVersion`  -  [#8808](https://github.com/NuGet/Home/issues/8808)

### <a name="issues-fixed-in-this-release"></a>이번 릴리스에서 수정된 문제

**미**

* Dotnet CLI 복원에서 자격 증명 플러그 인을 시작 하는 경우 `DOTNET_HOST_PATH`  환경 변수가 정의 되어 있지 않으면 시스템 경로에서 DOTNET cli를 시도 합니다. - [#7438](https://github.com/NuGet/Home/issues/7438)

* nuget.exe spec은 #8696 대신 저작권 YYYY의 하드 코드 된 텍스트를 사용 하 여 저작권 태그를 생성 합니다. `$copyright$`  -  [#8696](https://github.com/NuGet/Home/issues/8696)

* 어셈블리 이름이 변경 된 경우에는 assemblyinfo 특성을 무시 하는 .csproj의 pack에서 ' 작성자 필요 ' 예외가 throw 됩니다.- [#4234](https://github.com/NuGet/Home/issues/4234) NuGet.exe

* HttpRequestMessage는 [#8661](https://github.com/NuGet/Home/issues/8661) SocketHttpHandler에서 지원 되지 않는 여러 번 다시 사용 됩니다.

* 5.6.0 preview 3 이상 인덱싱에서 다른 공개 키 토큰을 사용 합니다. [#9481](https://github.com/NuGet/Home/issues/9481)

* NuGet 패키지를 만드는 동안 TreatWarningsAsErrors 준수- [#7404](https://github.com/NuGet/Home/issues/7404)

* [CPVM] 여러 p2p 프로젝트에 대 한 의사 패키지 다운 그레이드- [#9549](https://github.com/NuGet/Home/issues/9549)

* "찾아보기" 탭은 검색 상자를 사용 하 여 왼쪽에 정렬 되지 않습니다. [#9559](https://github.com/NuGet/Home/issues/9559)

* 설치 된 버전은 여러 버전이 설치 된 하나의 패키지 id에 대 한 솔루션 수준 PM UI의 포함 된 아이콘과 일치 하지 않습니다 [#9321](https://github.com/NuGet/Home/issues/9321)

* 누수: PartCreationPolicy (CreationPolicy) SolutionRestoreManager. RestoreOperationLogger- [#9595](https://github.com/NuGet/Home/issues/9595)

* Op 복원에서 자산 파일을 읽지 않습니다.- [#9693](https://github.com/NuGet/Home/issues/9693)

* NuGet. 프로토콜은 검색에서 버전의 다운로드 횟수를 가져오는 기능을 지원 하지 않습니다 [#9086](https://github.com/NuGet/Home/issues/9086)

* JObject [#9719](https://github.com/NuGet/Home/issues/9719) 종속성을 줄여 PackageMetadataResourceV3의 메모리 성능을 향상 시킵니다.

**변경 요청 디자인:**

* `<owners>`중복 된 경우 요소를 표시 하지 않습니다 [#5134](https://github.com/NuGet/Home/issues/5134)

* ETW 이벤트로 Int추적기 기록- [#9593](https://github.com/NuGet/Home/issues/9593)

* CPVM 사용자에 게 기능이 미리 보기 상태 임을 알리기 위해 복원에 정보 메시지를 추가 했습니다 [#9340](https://github.com/NuGet/Home/issues/9340)

* 자산 파일에서 솔루션 탐색기 패키지/프로젝트 전이적 종속성 채우기- [#9580](https://github.com/NuGet/Home/issues/9580)

* 설치 된 패키지 탭에서 패키지 목록의 키를 매길 필요가 없습니다. [#6995](https://github.com/NuGet/Home/issues/6995)

**[이 릴리스에서 해결 된 모든 문제 목록-5.7](https://app.zenhub.com/workspaces/nuget-client-team-55aec9a240305cf007585881/reports/release?release=5ea77f51ab1a972297db2e92)**

### <a name="community-contributions"></a>커뮤니티 기여

이 NuGet 릴리스를 위해 도움을 주는 모든 참가자에 게 감사 합니다.

|대상|Pr|문제|
|----|----|----|
|[campersau](https://github.com/campersau)|[3433](https://github.com/NuGet/NuGet.Client/pull/3433), [3120](https://github.com/NuGet/NuGet.Client/pull/3120)|NuGet. 프로토콜은 검색에서 버전의 다운로드 횟수를 가져오는 기능을 지원 하지 않습니다 [#9086](https://github.com/NuGet/Home/issues/9086) </br>HttpRequestMessage는 [#8661](https://github.com/NuGet/Home/issues/8661) SocketHttpHandler에서 지원 되지 않는 여러 번 다시 사용 됩니다.|
|[Joseph Musser (jnm2)](https://github.com/jnm2)|[3241](https://github.com/NuGet/NuGet.Client/pull/3241)|`<owners>`중복 된 경우 요소를 표시 하지 않습니다 [#5134](https://github.com/NuGet/Home/issues/5134)|
|[Volodymyr Shkolka (블랙 Gad)](https://github.com/BlackGad)|[3273](https://github.com/NuGet/NuGet.Client/pull/3273)|NuGet은 클라이언트 인증서가 필요한 HTTPS 원본에서 복원할 수 없습니다.- [#5773](https://github.com/NuGet/Home/issues/5773)|
|[Marius Unanu (Rezok)](https://github.com/Therzok)|[3357](https://github.com/NuGet/NuGet.Client/pull/3357)|HttpSourceAuthenticationHandler SemaphoreSlim 미래 교정- [#9463](https://github.com/NuGet/Home/issues/9463)|
|[Sunner (SuNNjek)](https://github.com/SuNNjek)|[3088](https://github.com/NuGet/NuGet.Client/pull/3088)|nuget.exe spec은 #8696 대신 저작권 YYYY의 하드 코드 된 텍스트를 사용 하 여 저작권 태그를 생성 합니다. `$copyright$`  -  [#8696](https://github.com/NuGet/Home/issues/8696)|
|[Olivier Spinelli (olivier-spinelli)](https://github.com/olivier-spinelli)|[3335](https://github.com/NuGet/NuGet.Client/pull/3335)|Dotnet CLI 복원에서 자격 증명 플러그 인을 시작 하는 경우 `DOTNET_HOST_PATH`  환경 변수가 정의 되어 있지 않으면 시스템 경로에서 DOTNET cli를 시도 합니다. - [#7438](https://github.com/NuGet/Home/issues/7438)|
|[goyzhang](https://github.com/goyzhang)|[3370](https://github.com/NuGet/NuGet.Client/pull/3370)|`latest`#8808에 대 한 옵션이 추가 됨 `-MSBuildVersion`  -  [#8808](https://github.com/NuGet/Home/issues/8808)|
