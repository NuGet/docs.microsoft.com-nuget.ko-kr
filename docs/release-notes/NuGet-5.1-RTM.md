---
ms.openlocfilehash: 48306e77a017c11fa7dc0d695e0177edf4e79d1e
ms.sourcegitcommit: 69b5eb1494a1745a4b1a7f320a91255d5d8356a9
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 05/21/2019
ms.locfileid: "65975837"
---
# <a name="nuget-51-release-notes"></a>NuGet 5.1 릴리스 정보

NuGet 배포 차량:

| NuGet 버전 | Visual Studio 버전에서 사용 가능| .NET SDK에서 사용 가능|
|:---|:---|:---|
| [**5.1.0**](https://nuget.org/downloads) | [Visual Studio 2019 16.1 버전](https://visualstudio.microsoft.com/downloads/) | [2.1.70X](https://dotnet.microsoft.com/download/dotnet-core/2.1)<sup>1</sup>, [2.2.30X](https://dotnet.microsoft.com/download/dotnet-core/2.2)<sup>2</sup> |

<sup>1</sup>.NET Core 워크 로드를 사용 하 여 Visual Studio 2019와 함께 설치 

<sup>2</sup>.NET Core 워크 로드를 사용 하 여 Visual Studio 2019를 사용 하 여 설치를 선택적으로 사용 가능

## <a name="summary-whats-new-in-51"></a>요약: 5.1의 새로운 기능

* CI/CD 워크플로에-를 사용 하 여 더 나은 통합 수 있도록 이미 있는 경우 패키지 푸시를 표시 하지 않으려면 지원 [#1630](https://github.com/NuGet/Home/issues/1630#issuecomment-483461100)

* Visual Studio에는 이제 편리한 링크를 제공 된 패키지를 nuget.org 갤러리 페이지- [#5299](https://github.com/NuGet/Home/issues/5299#issuecomment-494458510)

* 와 같은 새.NET Core 3.0 자산에 대 한 지원 [타기 팅 팩](https://github.com/dotnet/cli/issues/10006) 고 [런타임 팩](https://github.com/dotnet/cli/issues/10007)
  * NuGet pack 및 restore 대상 지정 및 런타임 패키지 참조를 사용 하도록 설정 하려면 FrameworkReferences 지원 [#7342](https://github.com/NuGet/Home/issues/7342)
  * 지원 PackageDownload-를 사용 하 여 패키지 시나리오 "다운로드" [#7339](https://github.com/NuGet/Home/issues/7339)
  * Exlcude 런타임 및 타기 팅 팩이 복원 검색 결과에서 그래프를 사용 하 여 PackageType- [#7337](https://github.com/NuGet/Home/issues/7337)

### <a name="issues-fixed-in-this-release"></a>이번 릴리스에서 수정된 문제

**버그**

* 플러그 인: 플러그 인 만들기 중 예외 정보 손실 [#8057](https://github.com/NuGet/Home/issues/8057)

* 단독 하한값을 사용 하 여 PackageReference 범위 하한값 원본 중 하나에 있는 경우 작동 하지 않습니다. - [#8054](https://github.com/NuGet/Home/issues/8054)

* IsPackableFalseError 메시지 개선 [#8021](https://github.com/NuGet/Home/issues/8021)

* -프로젝트 그래프 변경 될 때 파일 다시 생성 잠금-잠금 파일 [#8019](https://github.com/NuGet/Home/issues/8019)

* ProjectSystem 버그: 자동 시작 하는 Nuget 패키지 제거- [#8017](https://github.com/NuGet/Home/issues/8017)

* FrameworkReference 반환에 대 한 대상을 추가 CollectPackageDownloads 및 CollectPackageReferences-비슷합니다 [#8005](https://github.com/NuGet/Home/issues/8005)

* HTTP 캐시:  RepositoryResources 리소스 버전 관리 방식-캐시 되지 [#7997](https://github.com/NuGet/Home/issues/7997)

* 로깅: 예외 호출 스택 세부 자세한 정도-를 사용 하 여 보고 되지 않습니다 [#7955](https://github.com/NuGet/Home/issues/7955)

* -HTTPS를 사용 하도록 모든 NuGet Docs Url 변경 [#7950](https://github.com/NuGet/Home/issues/7950)

* NU3024 경고 메시지 개선 [#7933](https://github.com/NuGet/Home/issues/7933)

* 잠금 파일 업데이트 되지 않는 경우 제거 하는 packagereference [#7930](https://github.com/NuGet/Home/issues/7930)

* Nuspec-의 licenseurl 및 라이선스 요소의 유효성을 검사 하는 경우 오류 사례 처리 향상 [#7915](https://github.com/NuGet/Home/issues/7915)

* 탭 헤더에 오류가-발생 클릭 "파일 위치 열기" PM UI-마우스 오른쪽 단추로 클릭 [#7913](https://github.com/NuGet/Home/issues/7913)

* 플러그 인:-플러그 인 프로세스를 종료 하는 경우 로그 [#7907](https://github.com/NuGet/Home/issues/7907)

* 플러그 인: 로깅 날짜/시간 값에서 높은 충돌 비율 [#7899](https://github.com/NuGet/Home/issues/7899)

* Manifest.ReadFrom LicenseExpression-를 사용 하 여 모든 nuspec에서 실패 [#7894](https://github.com/NuGet/Home/issues/7894)

* RestoreLockedMode: ProjectReference 사용자 지정 AssemblyName-를 사용 하 여 프로젝트를 참조할 때 예기치 않은 NU1004 [#7889](https://github.com/NuGet/Home/issues/7889)

* 플러그 인 시작 실패-예외가 발생 하는 경우 더 나은 오류 메시지가 [#7857](https://github.com/NuGet/Home/issues/7857)

* 방지 NoOp 복원 작업을 수행 하는 경우 *. obj 디렉터리-dgspec.json 쓰기 [#7854](https://github.com/NuGet/Home/issues/7854)

* GeneratePathProperty 사례 일치 하지 않아서에서 속성을 생성 하는 true 실패 = [#7843](https://github.com/NuGet/Home/issues/7843)

* 설정: 패키지 원본 경로에 잘못 된 문자가-VS와 충돌할 수 있다 [#7820](https://github.com/NuGet/Home/issues/7820)

* 복원-NoOp에 잠금 파일을 생성 하지 않습니다 잠금 파일 삭제 되 면 [#7807](https://github.com/NuGet/Home/issues/7807)

* 라이선스 URL 및 읽기-메타 데이터를 사용 하 여 오류 라이선스 원인 [#7547](https://github.com/NuGet/Home/issues/7547)

* 처리 되지 않은 예외가 V2FeedParser- [#7523](https://github.com/NuGet/Home/issues/7523)

* 잘못 된 인수-에 대 한 종료 코드 0을 반환 하는 nuget.exe [#7178](https://github.com/NuGet/Home/issues/7178)

* 오류 및 경고 문서 서명 관련된 시나리오에 맞게 업데이트 [#6498](https://github.com/NuGet/Home/issues/6498)

* 자산 파일 상대 경로 사용 하 여 이동 프로젝트를 더 쉽게 사용 하도록 설정 해야 [#4582](https://github.com/NuGet/Home/issues/4582)

**DCRs**

* 플러그 인: 진단 로깅을- [#7859](https://github.com/NuGet/Home/issues/7859)

* 확인 Tizen 6 매핑할 NetStandard 2.1- [#7773](https://github.com/NuGet/Home/issues/7773)

**[이 릴리스에 5.1 RTM에서 수정 된 모든 문제 목록](https://github.com/nuget/home/issues?q=is%3Aissue+is%3Aclosed+milestone%3A%225.1")**
