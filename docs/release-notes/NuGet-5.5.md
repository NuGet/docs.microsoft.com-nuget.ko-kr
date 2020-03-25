---
title: NuGet 5.5 릴리스 정보
description: 새 기능, 버그 수정 및 Ecrs를 비롯 한 NuGet 5.5에 대 한 릴리스 정보입니다.
author: karann-msft
ms.author: karann
ms.date: 03/19/2020
ms.topic: conceptual
ms.openlocfilehash: 0e8ab66c937058e84420bc3e3a5031cbc133aad7
ms.sourcegitcommit: 1a63a84da2719c8141823ac89a20bf507fd22b00
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 03/24/2020
ms.locfileid: "80148284"
---
# <a name="nuget-55-release-notes"></a>NuGet 5.5 릴리스 정보

NuGet 배포 차량:

| NuGet 버전 | Visual Studio 버전에서 사용 가능| .NET SDK에서 사용 가능|
|:---|:---|:---|
| [**5.5.0**](https://nuget.org/downloads) | [Visual Studio 2019 버전 16.5](https://visualstudio.microsoft.com/downloads/) | [3.1.200](https://dotnet.microsoft.com/download/dotnet-core/3.1)<sup>1</sup> |

<sup>1</sup> .NET Core 워크 로드와 함께 Visual Studio 2019와 함께 설치 됨

## <a name="summary-whats-new-in-55"></a>요약: 5.5의 새로운 기능

* Visual Studio의 NuGet 패키지 관리자 UI에 대 한 내게 필요한 옵션 및 화면 판독기 환경 개선
    * 화면 판독기 환경에서의 접근성 문제, 누락 된 altText, 설치 된 텍스트 상자에 대 한 액세스 가능한 이름 등,- [#9059](https://github.com/NuGet/Home/issues/9059)
    * 패키지 목록에서 화면 판독기 환경의 접근성 문제- [#9077](https://github.com/NuGet/Home/issues/9077)
    * "찾아보기", "설치", "업데이트" 탭과 관련 된 화면 판독기 환경에서 접근성 문제가 있습니다 [#9078](https://github.com/NuGet/Home/issues/9078)
    * 내레이터는 "Blank", "No Dependencies", "," MIT "링크 레이블을 발표 하지 않습니다 [#9157](https://github.com/NuGet/Home/issues/9157)

* 로컬 피드에 호스트 되는 패키지에 대 한 Visual Studio 패키지 관리자 UI의 자동 포함 아이콘에 대 한 지원- [#8189](https://github.com/NuGet/Home/issues/8189)

* MSBuild 정적 Graph Api- [8791](https://github.com/NuGet/Home/issues/8791) 를 호출 하 여 계산 속도를 향상 시키는 `RestoreUseStaticGraphEvaluation`를 사용 하는 op 복원 성능이 크게 향상 됨

* 플랫폼 간 인증 플러그인을 사용 하 여 dotnet 안정성 향상
    * TaskCanceledException를 사용 하 여 dotnet restore 실패- [#7842](https://github.com/NuGet/Home/issues/7842)
    * 플러그 인: "작업이 취소 되었습니다."-이로 인해 ADO 인증에 문제가 있습니다. - [#8528](https://github.com/NuGet/Home/issues/8528)

* `dotnet nuget <add|remove|update|disable|enable|list> source` 명령 추가- [#4126](https://github.com/NuGet/Home/issues/4126)

* Dotnet nuget 푸시 [#8778](https://github.com/NuGet/Home/issues/8778) 를 사용 하는 `--skip-duplicate`에 대 한 지원을

* Msbuild/restore를 사용 하 `packages.config` 지원- [#8506](https://github.com/NuGet/Home/issues/8506)

### <a name="issues-fixed-in-this-release"></a>이번 릴리스에서 수정된 문제

**버그**

* V3 Api를 사용 하 여 자체 업데이트 프로그램 재작업- [#4197](https://github.com/NuGet/Home/issues/4197)

* 패키지 종속성 버전이 ' * '로 설정 된 경우 패키지 종속성 버전이 잘못 되었습니다.- [#6697](https://github.com/NuGet/Home/issues/6697)

* ErrorUnsafePackageEntry 오류 메시지가 문제의 원인을 가리키지 않습니다.- [#7505](https://github.com/NuGet/Home/issues/7505)

* 잠금 파일은 "*" 시나리오에서 적용 되지 않습니다.- [#8073](https://github.com/NuGet/Home/issues/8073)

* PackageReference에서 *를 사용 하는 경우 Nuget.exe는 최신 버전의 패키지로 확인 되지 않습니다 (MSBuild/Dotnet/VS restore do).- [#8432](https://github.com/NuGet/Home/issues/8432)

* 다중 대상 WPF 프로젝트를 사용 하는 dotnet list 패키지- [#8463](https://github.com/NuGet/Home/issues/8463)

* ConcurrencyUtilities 개선 (CPU 사용량 감소)- [#8653](https://github.com/NuGet/Home/issues/8653)

* 언로드된 프로젝트 시나리오에 대 한 DG 사양은 미리 보기 복원으로 작성할 수 없습니다.- [#8793](https://github.com/NuGet/Home/issues/8793)

* Visual Studio NuGet 패키지 (RestoreManagerPackage)는 솔루션 빌드 이벤트에서 자동으로 로드 해야 합니다. [#8796](https://github.com/NuGet/Home/issues/8796)

* .Vssettings init의 교착 상태- [#8842](https://github.com/NuGet/Home/issues/8842)

* VisualStudio 도구 상자는 프로젝트가 솔루션 폴더에 배치 되는 경우 NuGet 패키지에서 채워지지 않습니다.- [#8868](https://github.com/NuGet/Home/issues/8868)

* VS: 솔루션 복원 영구적으로 경합 조건으로 인해 실패 함- [#8881](https://github.com/NuGet/Home/issues/8881)

* "로드 중 ..."이 설치 된 탭에서 " <term>. "업데이트 탭- [#8890](https://github.com/NuGet/Home/issues/8890)

* 캐시 만료 후 VS PM UI에 포함 된 아이콘 누락- [#9069](https://github.com/NuGet/Home/issues/9069)

* FireAndForget PM UI 시작- [#9112](https://github.com/NuGet/Home/issues/9112)

* 복원: IncludeExcludeFiles. Equals (...) 구현이 잘못 되었습니다. [#9167](https://github.com/NuGet/Home/issues/9167)

* 복원: PackageSpec ()는 동일 하지 않은 클론을 만듭니다. [#9211](https://github.com/NuGet/Home/issues/9211)

* "빌드가 오류로 인해 완료 되는 경우 항상 오류 목록 표시"를 선택 하지 않은 경우에도 표시 되는 오류 목록 [#8190](https://github.com/NuGet/Home/issues/8190)

* 정적 그래프 복원은 빈 솔루션 경로를 전달 하면 안 됩니다.- [#9061](https://github.com/NuGet/Home/issues/9061)

* 복원: 각 프로젝트에 대 한 클로저 계산 됨- [#9042](https://github.com/NuGet/Home/issues/9042)

* Restore: DependencyGraphSpec (...)에는 JObject- [#9040](https://github.com/NuGet/Home/issues/9040) 필요 하지 않습니다.

* 복원: LOH (large object heap)에 생성 되는 긴 문자열 [#9031](https://github.com/NuGet/Home/issues/9031)

* MSBuild SDK 확인자- [8848](https://github.com/NuGet/Home/issues/8848) 로 인해 최신 mono의 사용자 지정 nuget.exe가 중단 될 수 있습니다.

* dgspec이 "다른 프로세스에서 사용 되었습니다."- [8692](https://github.com/NuGet/Home/issues/8692) 인 경우 복원이 실패 합니다.

**Dcr**

* _GetRestoreProjectStyle의 논리는 작업에 있어야 합니다. [#8804](https://github.com/NuGet/Home/issues/8804)

* 설치 됨 탭에서 기본적으로 사용 중단 정보를 추가 [#8541](https://github.com/NuGet/Home/issues/8541)

**[이 릴리스에서 해결 된 모든 문제 목록-5.5](https://app.zenhub.com/workspaces/nuget-client-team-55aec9a240305cf007585881/reports/release?release=5e0e5fbd021f7aa0ec95db18)**
