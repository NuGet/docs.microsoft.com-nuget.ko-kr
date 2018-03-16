---
title: "NuGet 4.0 RC 릴리스 정보 | Microsoft Docs"
author: anangaur
ms.author: anangaur
manager: unniravindranathan
ms.date: 03/03/2017
ms.topic: article
ms.prod: nuget
ms.technology: 
description: "NuGet 4.0 RTM에 대한 릴리스 정보(알려진 문제, 버그 수정, 추가된 기능 및 DCR 포함)"
keywords: "NuGet 4.0 RTM 릴리스 정보, 버그 수정, 알려진 문제, 추가된 기능, DCR"
ms.reviewer:
- karann-msft
- unniravindranathan
ms.openlocfilehash: d1ab89f0decb64a64d04dc293e5273b577e8398b
ms.sourcegitcommit: 7969f6cd94eccfee5b62031bb404422139ccc383
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 02/20/2018
---
# <a name="nuget-40-rtm-release-notes"></a>NuGet 4.0 RTM 릴리스 정보

[Visual Studio 2017](https://www.visualstudio.com/news/releasenotes/vs2017-relnotes)은 .NET Core에 대한 지원을 추가하고, 많은 품질 수정을 포함하며, 성능을 향상시키는 NuGet 4.0과 함께 제공됩니다. 또한 이 릴리스에는 PackageReference 지원, MSBuild 대상 NuGet 명령, 백그라운드 패키지 복원 등과 같이 향상된 몇 가지 기능도 제공됩니다.

## <a name="known-issues"></a>알려진 문제

### <a name="nuget-restore-may-fail-when-you-have-multiple-projects-referencing-another-project-in-a-solution"></a>솔루션에 다른 프로젝트를 참조하는 프로젝트가 여러 개 있는 경우 NuGet 복원이 실패할 수 있습니다.

#### <a name="issue"></a>문제

대/소문자나 상대 경로가 다른, 동일한 프로젝트에 대한 프로젝트 참조가 솔루션에 있는 경우 NuGet 복원이 작동하지 않을 수 있습니다. [NuGet#4574](https://github.com/NuGet/Home/issues/4574)

#### <a name="workaround"></a>해결 방법

모든 프로젝트 참조에 대해 대/소문자나 상대 경로를 동일하게 수정합니다.

### <a name="while-using-package-manager-console-enter-key-may-not-work"></a>패키지 관리자 콘솔을 사용하는 동안 'Enter' 키가 작동하지 않을 수 있음

#### <a name="issue"></a>문제

경우에 따라 패키지 관리자 콘솔에서 Enter 키가 작동하지 않습니다. 이런 경우 수정 진행 상황을 확인하고 재현 단계에 대해 도움이 되는 추가 정보를 제공하세요. [NuGet#4204](https://github.com/NuGet/Home/issues/4204) [NuGet#4570](https://github.com/NuGet/Home/issues/4570)

#### <a name="workaround"></a>해결 방법

Visual Studio를 다시 시작하고 솔루션을 열기 전에 PMC를 엽니다. 또는 `project.lock.json`을 삭제하고 다시 복원합니다.

### <a name="in-net-core-projects-you-may-end-up-in-infinite-restore-loop-when-you-use-a-package-containing-an-assembly-with-an-invalid-signature"></a>.NET Core 프로젝트에서 잘못된 시그니처와 함께 어셈블리가 포함된 패키지를 사용할 때 무한 복원 루프가 발생할 수 있음

#### <a name="issue"></a>문제

경우에 따라 잘못된 시그니처와 함께 어셈블리가 포함된 패키지를 사용하거나 패키지 버전이 'DateTime' 표시기로 설정되었을 때 패키지 자동 복원이 무한 루프로 실행됩니다. [NuGet#4542](https://github.com/NuGet/Home/issues/4542)

#### <a name="workaround"></a>해결 방법

지금은 해결 방법이 없습니다.

### <a name="you-are-unable-to-view-add-or-update-dotnetclitools-using-nuget-package-manager"></a>NuGet 패키지 관리자를 사용하여 DotNetCLITools를 보거나 추가 또는 업데이트할 수 없음

#### <a name="issue"></a>문제

NuGet 패키지 관리자는 DotNetCLITools 추가/업데이트를 표시하지 않으며 허용하지도 않습니다. [NuGet#4256](https://github.com/NuGet/Home/issues/4256)

#### <a name="workaround"></a>해결 방법

프로젝트 파일에서 DotNetCLIToolReferences를 수동으로 편집해야 합니다.

### <a name="nuget-restore-will-fail-when-you-set-packageid-property-for-projects"></a>프로젝트에 대해 PackageId 속성을 설정하면 NuGet 복원이 실패함

#### <a name="issue"></a>문제

.NET Core 프로젝트의 경우 Visual Studio의 NuGet 복원에 프로젝트의 PackageId 속성이 반영되지 않습니다. [NuGet#4586](https://github.com/NuGet/Home/issues/4586)

#### <a name="workaround"></a>해결 방법

명령줄을 사용하여 복원을 실행합니다.

### <a name="when-your-project-does-not-have-obj-folder-package-restore-may-fail"></a>프로젝트에 'obj' 폴더가 없는 경우 패키지 복원에 실패할 수 있음

#### <a name="issue"></a>문제

'obj' 폴더가 삭제된 경우 Visual Studio에서 PackageReferences를 복원하지 못합니다. [NuGet#4528](https://github.com/NuGet/Home/issues/4528)

#### <a name="workaround"></a>해결 방법

수동으로 'obj' 폴더를 만들면 복원이 작동합니다.

### <a name="manually-updating-packages-using-update-package-in-console-may-fail"></a>콘솔에서 Update-Package를 사용하여 패키지를 수동으로 업데이트하면 실패할 수 있음

#### <a name="issue"></a>문제

방금 변환된 PackageReferences 프로젝트에 대해 한 번만 콘솔에서 Update-Package를 수동으로 사용할 수 있습니다. [NuGet#4431](https://github.com/NuGet/Home/issues/4431)

#### <a name="workaround"></a>해결 방법

지금은 해결 방법이 없습니다.

### <a name="retargeting-target-framework-version-may-lead-to-incomplete-intellisense"></a>대상 프레임워크 버전의 대상을 변경하면 불완전한 IntelliSense가 발생할 수 있음

#### <a name="issue"></a>문제

Visual Studio에서 대상 프레임워크 버전의 대상을 변경하면 불완전한 IntelliSense가 발생할 수 있습니다. 이 문제는 PackageReferences를 패키지 관리자 형식으로 사용하는 경우에 발생합니다. [NuGet#4216](https://github.com/NuGet/Home/issues/4216)

#### <a name="workaround"></a>해결 방법

수동 복원을 수행합니다.

### <a name="msbuild-trestore-fails-when-a-project-targeting-net461-references-another-project-targeting-netstandard"></a>.NET461을 대상으로 하는 프로젝트가 .NETStandard를 대상으로 하는 다른 프로젝트를 참조하는 경우 msbuild /t:restore가 실패함

#### <a name="issue"></a>문제

.NET461을 대상으로 하는 PackageReference 기반 프로젝트가 .NETStandard를 대상으로 하는 다른 PackageReference 기반 프로젝트를 참조하는 경우 msbuild /t:restore가 실패합니다.  [NuGet#4532](https://github.com/NuGet/Home/issues/4532)

#### <a name="workaround"></a>해결 방법

지금은 해결 방법이 없습니다.

## <a name="issues-fixed-in-nuget-40-rtm-timeframe"></a>NuGet 4.0 RTM 기간에서 수정된 문제

[NuGet 4.0 RC 릴리스 정보](../release-notes/nuget-4.0-RC.md) - NuGet 4.0 RC에서 수정된 모든 문제를 나열합니다.

### <a name="features"></a>기능

- NuGet.Core.sln의 문자열을 지역화합니다. - [#2041](https://github.com/NuGet/Home/issues/2041)

- Nuget은 LSL 모드에서 웹 응용 프로그램 프로젝트를 강제로 로드합니다. - [#4258](https://github.com/NuGet/Home/issues/4258)

- UI에서 "SDK가 설치된" 패키지에 대한 버전 변경을 차단하기 위해 AutoReferenced PackageReference를 지원합니다. - [#4044](https://github.com/NuGet/Home/issues/4044)

- 모든 프로젝트 종속성에 대해 PackageSpec.Version을 올바르게 전달합니다(PackageRef). - [#3902](https://github.com/NuGet/Home/issues/3902)

- 명령줄에서 `.csproj`로부터 참조를 제거하는 기능을 지원합니다. - [#4101](https://github.com/NuGet/Home/issues/4101)

- PackageReference 프로젝트(일반 및 xplat) 및 경량 솔루션 로드에 대한 복원을 지원합니다. - [#4003](https://github.com/NuGet/Home/issues/4003)

- 명령줄에서 `.csproj`에 참조를 추가하는 기능을 지원합니다. - [#3751](https://github.com/NuGet/Home/issues/3751)

- `packages.config` 또는 `project.json`의 경량 솔루션 로드에 대한 NuGet 복원을 지원합니다. - [#3711](https://github.com/NuGet/Home/issues/3711)

- nuget에서 생성된 targets 파일에서 contentFiles를 지원합니다. - [#3683](https://github.com/NuGet/Home/issues/3683)

- MSBuild를 사용하여 Mac에서 nuget.exe 유효성 검사에 대한 Mono CI를 설정합니다. - [#3646](https://github.com/NuGet/Home/issues/3646)

- v2 NuGet.Core 종속성에서 NuGet을 이동합니다. - [#3645](https://github.com/NuGet/Home/issues/3645)

### <a name="bugs"></a>버그

- Visual Studio의 NuGet restore에서 프로젝트의 PackageId 속성이 적용되지 않습니다. - [#4586](https://github.com/NuGet/Home/issues/4586)

- vsix 패키지에 패키지를 추가하면 NuGet ProjectSystemCache 오류가 발생합니다. - [#4545](https://github.com/NuGet/Home/issues/4545)

- IncludeSource가 여러 TFM이 있는 프로젝트에서 사용되는 경우 Pack에서 예외를 throw합니다. - [#4536](https://github.com/NuGet/Home/issues/4536)

- 솔루션 전체 패키지 관리에서 업데이트를 사용하면 VS 2017 RC3 작동이 중단됩니다. - [#4474](https://github.com/NuGet/Home/issues/4474)

- 새로 설치된 패키지를 제거할 수 없습니다. - [#4435](https://github.com/NuGet/Home/issues/4435)

- PackageRef로 마이그레이션하면 하이브리드 솔루션에 이상한 복원 동작이 발생합니다. - [#4433](https://github.com/NuGet/Home/issues/4433)

- NuGet 작업(install, update, restore)을 시작한 직후에 빌드하면 VS가 중단될 수 있습니다. - [#4420](https://github.com/NuGet/Home/issues/4420)

- UI 중단 - NuGet.SolutionRestoreManager.RestoreManagerPackage 초기화 시 교착 상태 - [#4371](https://github.com/NuGet/Home/issues/4371)

- 패키지 추가 명령은 요소 대신 버전을 특성으로 추가해야 합니다. - [#4325](https://github.com/NuGet/Home/issues/4325)

- dotnet restore foo.sln - SLN의 구성으로 인해 복원 그래프에서 중복(그러나 구성과 다름) 프로젝트가 발생하면 실패합니다. - [#4316](https://github.com/NuGet/Home/issues/4316)

- 콘텐츠 전용 패키지 - [#3668](https://github.com/NuGet/Home/issues/3668)

- 기본적으로 패키지 형식 선택기 옵션을 선택 취소합니다. - [#4468](https://github.com/NuGet/Home/issues/4468)

- 성능: CreateUAP_CSharp_VS.01.1.Create 프로젝트에서 Duration_TotalElapsedTime을 3,153.570ms(149.1%)만큼 재귀했습니다. 기준 26129.02 - [#4452](https://github.com/NuGet/Home/issues/4452)

- 성능: ManagedLangs_CS_DDRIT.0300.Rebuild 솔루션에서 Duration_TotalElapsedTime을 1.5초만큼 재귀했습니다. 기준 26105 - [#4441](https://github.com/NuGet/Home/issues/4441)

- 다중 TFM 프로젝트에서 지정 유효성 검사가 실패합니다. - [#4419](https://github.com/NuGet/Home/issues/4419)

- 성능: WebForms_DDRIT.1200.Close 솔루션에서 VM_ImagesInMemory_Total_devenv를 3.000개(0.5%)만큼 재귀했습니다. 기준 26123.04 - [#4408](https://github.com/NuGet/Home/issues/4408)

- vsfeedback - netcoreapp1.1을 대상으로 지정하면 경고가 표시됩니다. - [#4397](https://github.com/NuGet/Home/issues/4397)

- 빈 ASP.NET Core 웹 응용 프로그램에 NuGet 패키지를 추가하려고 하면 PathTooLongException이 발생합니다. - [#4391](https://github.com/NuGet/Home/issues/4391)

- Pack이 너무 자주 실행됨 - "Pack" 대상과 관련된 대상 종속성 그래프에 순환 종속성이 있으므로 dotnet pack이 실패합니다. - [#4381](https://github.com/NuGet/Home/issues/4381)

- Pack이 너무 자주 실행됨 - NuGet 패키지 생성에 모든 구성이 포함되지 않습니다. - [#4380](https://github.com/NuGet/Home/issues/4380)

- NullReferenceException - C++ 프로젝트에서 packageref가 포함된 nuget을 추가했습니다. - [#4378](https://github.com/NuGet/Home/issues/4378)

- 내게 필요한 옵션: 내레이터에서 패키지를 설치할 프로젝트를 선택하는 확인란을 설명하지 않습니다. - [#4366](https://github.com/NuGet/Home/issues/4366)

- NuGet VS17에서 VSO/VSTS 피드에 연결하는 데 산발적으로 실패합니다(VS 버그 365798). - [#4365](https://github.com/NuGet/Home/issues/4365)

- PackagePath에서 path를 "contentFiles"로 지정하면 contentFiles가 잘못된 위치로 출력됩니다. - [#4348](https://github.com/NuGet/Home/issues/4348)

- Pack 대상에서 VersionSuffix를 사용하여 PackageVersion 속성을 추가합니다. - [#4324](https://github.com/NuGet/Home/issues/4324)

- dotnet pack에서 패키지 경로 지정이 작동하지 않습니다. - [#4321](https://github.com/NuGet/Home/issues/4321)

- NuGet에서 복원하는 동안 중복 가져오기에 대한 많은 경고를 출력합니다. - [#4304](https://github.com/NuGet/Home/issues/4304)

- "NuGet 패키지 관리자 형식 선택" 대화 상자가 어두운 테마에서 제대로 표시되지 않습니다. - [#4300](https://github.com/NuGet/Home/issues/4300)

- 빌드 복원 시 VS 작동이 중단됩니다. - [#4298](https://github.com/NuGet/Home/issues/4298)

- targetframeworks에 TFM을 추가하고 저장한 다음 빌드하면 Visual Studio 교착 상태가 발생합니다. 시간의 10% - [#4295](https://github.com/NuGet/Home/issues/4295)

- nuget pack에서 프로젝트를 성공적으로 압축했지만 성공 메시지를 출력하지 않습니다. - [#4294](https://github.com/NuGet/Home/issues/4294)

- System.IO.Compression 4.1을 찾을 수 없어 PackTask가 실패합니다. - [#4290](https://github.com/NuGet/Home/issues/4290)

- Pack이 너무 자주 실행됨 - 파일 액세스 충돌로 인해 PackTask가 자주 실패합니다. - [#4289](https://github.com/NuGet/Home/issues/4289)

- NuGet에서 백그라운드 복원 중에 출력 창을 엽니다. - [#4274](https://github.com/NuGet/Home/issues/4274)

- ServiceProvider를 위험한 코딩 패턴으로 제거합니다(중단이 발생할 수 있음). - [#4268](https://github.com/NuGet/Home/issues/4268)

- 성능/UI 중지 - DownloadTimeoutStream 읽기가 향상되었습니다. - [#4266](https://github.com/NuGet/Home/issues/4266)

- nuget restore가 완료되기 전에 프로젝트를 닫으려고 하면 Visual Studio 교착 상태가 발생합니다. - [#4257](https://github.com/NuGet/Home/issues/4257)

- PackTask 및 `.nuspec` 압축 관련 문제 - [#4250](https://github.com/NuGet/Home/issues/4250)

- [vsfeedback] 새 프로젝트에서 NuGet 패키지를 확인할 수 없습니다(Visual Studio를 다시 시작해야 함). - [#4217](https://github.com/NuGet/Home/issues/4217)

- [vsfeedback] 사용 가능한 패키지 버전을 표시하는 "Version" 드롭다운에서 선택한 NuGet 패키지와 동기화 상태를 유지하기가 어렵습니다. - [#4198](https://github.com/NuGet/Home/issues/4198)

- Nuget.Client에서 CPS와 상호 작용하여 교착 상태를 방지하는 경우 CPS JoinableTaskFactory를 사용해야 합니다. - [#4185](https://github.com/NuGet/Home/issues/4185)

- NuGet 3.5.0에서 패키지의 `.targets`를 압축 해제하지 않습니다. - [#4171](https://github.com/NuGet/Home/issues/4171)

- dotnet pack에서 `.csproj`의 제목을 지원하지 않습니다. - [#4150](https://github.com/NuGet/Home/issues/4150)

- VS2017 RC에서 Install-Package가 오류 대화 상자를 표시합니다. - [#4127](https://github.com/NuGet/Home/issues/4127)

- UI에서 지정된 위치의 CPS 업데이트를 가져오지 않으므로 .NET Core 프로젝트에 대한 패키지 업데이트가 작동하지 않는 것으로 나타납니다. - [#4035](https://github.com/NuGet/Home/issues/4035)

- 확인되지 않은 참조 경고가 향상되었습니다. - [#3955](https://github.com/NuGet/Home/issues/3955)

- dotnet pack - ProjectReference에서 버전 정보가 손실됩니다. - [#3953](https://github.com/NuGet/Home/issues/3953)

- UWP 앱 만들기 프로젝트 생성 및 총 경과 시간 재귀 다시 빌드 - [#3873](https://github.com/NuGet/Home/issues/3873)

- 복원 중에 오류가 발생한 후에도 성공적인 복원 메시지가 표시됩니다. - [#3799](https://github.com/NuGet/Home/issues/3799)

- Nuget.CommandLine 3.4.4를 Nuget.org에 다시 게시합니다. - [#2931](https://github.com/NuGet/Home/issues/2931)

- 마이그레이션 시 프로젝트가 `project.json`에서 `.csproj`로 변경되면 복원이 실패합니다. - [#4297](https://github.com/NuGet/Home/issues/4297)

- 새로 만든 xunit 테스트 프로젝트에서 복원이 실패합니다. - [#4296](https://github.com/NuGet/Home/issues/4296)

- Core 프로젝트가 중단되고 열린 상태에서 UI를 잠글 수 있습니다. - [#4269](https://github.com/NuGet/Home/issues/4269)

- 빌드 작업에 대한 대상 파일을 수정합니다. - [#4267](https://github.com/NuGet/Home/issues/4267)

- 참조된 프로젝트를 언로드하는 솔루션을 빌드한 후에 오류 목록에 오류가 있습니다. - [#4208](https://github.com/NuGet/Home/issues/4208)

- MSB4057: "_GenerateRestoreGraphProjectEntry" 대상이 프로젝트에 존재하지 않습니다. - [#4194](https://github.com/NuGet/Home/issues/4194)

- vsfeedback: 모든 프로젝트를 선택하면 솔루션에 대한 NuGet 관리자 UI 작동이 중단됩니다. - [#4191](https://github.com/NuGet/Home/issues/4191)

- 후행 슬래시가 있으면 nuget.exe msbuildpath가 실패합니다. - [#4180](https://github.com/NuGet/Home/issues/4180)

- vsfeedback: nuget restore에서 LinqToTwitter 프로젝트에 대한 여러 프로젝트 참조 경고를 제공합니다 - [#4156](https://github.com/NuGet/Home/issues/4156)

- `.csproj`의 pack에 minClientVersion 특성이 포함되지 않습니다. - [#4135](https://github.com/NuGet/Home/issues/4135)

- NuGet.Build.Tasks.Pack.dll이 VS2017(d15rel 26014.00)에서 지연된 서명으로 제공되었습니다. - [#4122](https://github.com/NuGet/Home/issues/4122)

- VSFeedback: CMake 3.7.1을 사용하여 생성된 VS 2015 프로젝트에 대한 복원이 실패합니다. - [#4114](https://github.com/NuGet/Home/issues/4114)

- VSFeedback: 복원 오류로 인해 빌드에서 제공할 수 있는 완전한 오류 메시지가 손상될 수 있습니다. - [#4113](https://github.com/NuGet/Home/issues/4113)

- [VSFeedback] 웹 사이트 프로젝트에 대한 NuGet 패키지를 복원하는 동안 오류가 발생했습니다. 값은 null일 수 없습니다. - [#4092](https://github.com/NuGet/Home/issues/4092)

- 마이그레이션 중에 NuGet.PackageManagement.VisualStudio.SolutionRestoreWorker에서 "개체 참조 예외"를 throw합니다. - [#4067](https://github.com/NuGet/Home/issues/4067)

- dotnet pack에서 도구를 패키지가 빌드된 버전으로 압축해야 합니다. - [#4063](https://github.com/NuGet/Home/issues/4063)

- 복원하는 데 몇 초가 걸리는 경우 새 백그라운드 복원에서 상태 표시줄에 밀리초를 씁니다. - [#4036](https://github.com/NuGet/Home/issues/4036)

- 오타로 인해 모든 프로젝트 참조를 확인하지 못했습니다. - [#4018](https://github.com/NuGet/Home/issues/4018)

- 패키지 참조 시나리오에서 PCM 워크플로를 사용하도록 설정합니다. - [#4016](https://github.com/NuGet/Home/issues/4016)

- 패키지 관리자 UI에서 설치된 패키지를 찾을 수 없습니다. - [#4015](https://github.com/NuGet/Home/issues/4015)

- PackagePath가 비어 있으면 dotnet pack이 실패합니다. - [#3993](https://github.com/NuGet/Home/issues/3993)

- 다중 사용자 시나리오에서 복원 작업이 실패합니다. - [#3897](https://github.com/NuGet/Home/issues/3897)

- NuGet Pack 작업을 사용하여 압축할 때 콘텐츠 형식을 변경할 수 없습니다. - [#3895](https://github.com/NuGet/Home/issues/3895)

- MsBuild /t:pack에 대한 ContentFiles 기본 복사가 올바르지 않습니다. - [#3894](https://github.com/NuGet/Home/issues/3894)

- 설치 패키지 복원에서 패키지 복원 메시지가 두 번 기록됩니다. - [#3785](https://github.com/NuGet/Home/issues/3785)

- Guardrails 제거 - "runtimes" 섹션의 복원은 현재 프로젝트에만 적용해야 합니다. - [#3768](https://github.com/NuGet/Home/issues/3768)

- Pack 작업에서 'content/' 및 'contentFiles/' 모두에 콘텐츠 파일을 넣습니다. - [#3718](https://github.com/NuGet/Home/issues/3718)

- dotnet pack3에서 별도의 태그 분할을 수행합니다. - [#3701](https://github.com/NuGet/Home/issues/3701)

- dotnet pack: 패키지 참조가 포함된 프로젝트를 압축하면 중복적인 가져오기 경고가 발생합니다. - [#3665](https://github.com/NuGet/Home/issues/3665)

- VS에서 복원 로깅이 항상 표시되지 않습니다. - [#3633](https://github.com/NuGet/Home/issues/3633)

- nuget locals help 텍스트에서 여전히 패키지 캐시를 언급했습니다. - [#3592](https://github.com/NuGet/Home/issues/3592)

- Restore3에서 PackageReferences를 TargetFrameworks와 결합합니다. - [#3504](https://github.com/NuGet/Home/issues/3504)

- Nuget이 VS "15" Preview 4 dev 명령 프롬프트에서 MSBuild의 예기치 않은 버전을 선택합니다. - [#3408](https://github.com/NuGet/Home/issues/3408)

- 실패한 복원에서 targets/props 파일을 작성합니다. - [#3399](https://github.com/NuGet/Home/issues/3399)

- VS 15 명령 프롬프트에서 실행할 때 NuGet에서 복원하는 동안 MSBuild와 동일한 compat shim을 따르지 않습니다. - [#3387](https://github.com/NuGet/Home/issues/3387)

- VS15에 대해 PackFromProjectWithDevelopmentDependencySet을 사용하도록 다시 설정합니다. - [#3272](https://github.com/NuGet/Home/issues/3272)

- NuGet과 관련된 Blend 문제 - [#4043](https://github.com/NuGet/Home/issues/4043)

- 4.0.0.2067을 CLI 및 SDK 리포지토리에 통합하여 RC2와 함께 제공합니다. - [#4029](https://github.com/NuGet/Home/issues/4029)

- 새 Core 콘솔 앱 만들기, 솔루션 닫기, 솔루션 열기 및 솔루션 닫기를 수행하면 VS가 중단됩니다. - [#4008](https://github.com/NuGet/Home/issues/4008)

- d15prerel.25916.01에 대한 프로젝트 열기가 중단됩니다. - [#3982](https://github.com/NuGet/Home/issues/3982)

- dotnet/nuget.exe locals doc/help 메시지를 수정합니다. - [#3919](https://github.com/NuGet/Home/issues/3919)

- 후행 또는 선행 공백 문제에 대한 PackTask를 검사합니다. - [#3906](https://github.com/NuGet/Home/issues/3906)

- dotnet pack은 bin이 아닌 obj에서 압축합니다. - [#3880](https://github.com/NuGet/Home/issues/3880)

- dotnet pack에서 항상 ProjectReference 버전을 1.0.0으로 설정하는 것으로 보입니다. - [#3874](https://github.com/NuGet/Home/issues/3874)

- 프로젝트 참조 및 <TargetFramework>로 인해 dotnet pack이 실패합니다. - [#3865](https://github.com/NuGet/Home/issues/3865)

- ProjectSystemCache.TryGetProjectNameByShortName에서 LockRecursionException을 throw합니다. - [#3861](https://github.com/NuGet/Home/issues/3861)

- MSBuild 속성에서 공백을 제거해야 합니다. - [#3819](https://github.com/NuGet/Home/issues/3819)

- 프로젝트 로드 시 발생한 두 프로젝트 이벤트를 통합합니다. - [#3759](https://github.com/NuGet/Home/issues/3759)

- `project.assets.json` 파일의 P2P 라이브러리에 잘못된 버전이 있습니다. - [#3748](https://github.com/NuGet/Home/issues/3748)

- 응답하지 않는 피드 및 사용할 수 없는 패키지로 인해 복원 작동이 중단됩니다. - [#3672](https://github.com/NuGet/Home/issues/3672)

- 대량의 MSBuild 오류 출력에서 nuget.exe가 중단될 수 있습니다. - [#3572](https://github.com/NuGet/Home/issues/3572)

- Blend에 대한 빌드 시 복원(Restore-on-build)이 처음에는 실패하고 두 번째에 성공합니다(VS 시나리오가 수정됨). - [#2121](https://github.com/NuGet/Home/issues/2121)

### <a name="dcrs"></a>DCR

- vsix를 v2 vsix에서 v3 vsix로 마이그레이션합니다. - [#4196](https://github.com/NuGet/Home/issues/4196)

- MSBuild에서 잠금 파일의 경로를 가져오는 메커니즘이 NuGet에 있어야 합니다. - [#3351](https://github.com/NuGet/Home/issues/3351)

- TFM 호환성 검사 및 자산 파일에 빌드 자산을 추가합니다. - [#3296](https://github.com/NuGet/Home/issues/3296)

- Pack 대상에 새 ProjectCapability "Pack"을 정의하여 패키지 관련 기능을 사용하도록 설정합니다. - [#4146](https://github.com/NuGet/Home/issues/4146)

- "GeneratePackageOnBuild" MSBuild 속성에 따른 빌드 후 대상으로 Pack을 실행합니다. - [#4145](https://github.com/NuGet/Home/issues/4145)

- RestoreProjectStyle NuGet 속성을 사용하여 특정 NuGet 프로젝트를 만듭니다. - [#4134](https://github.com/NuGet/Home/issues/4134)

- 전이적 프로젝트 참조 변경에 맞게 복원을 조정합니다. - [#4076](https://github.com/NuGet/Home/issues/4076)

- 비UWP 프로젝트의 대상 파일에 NuGet 속성을 추가합니다. - [#4030](https://github.com/NuGet/Home/issues/4030)

- UWP TargetPlatformVersion 지원 - [#3923](https://github.com/NuGet/Home/issues/3923)

- NuGet 프로젝트 시스템에 프로젝트 참조 메타데이터를 전달합니다. - [#3922](https://github.com/NuGet/Home/issues/3922)

- 패키징 모드에 대한 UI를 추가해야 합니다. - [#3921](https://github.com/NuGet/Home/issues/3921)

- 레거시 `.csproj`에는 proj/targets에 설정된 NugetTargetMoniker 및 RuntimeIdentifiers가 있어야 합니다. - [#3854](https://github.com/NuGet/Home/issues/3854)

- 설치 패키지가 자동 복원과 겹칠 수 있습니다. - [#3836](https://github.com/NuGet/Home/issues/3836)

- VSPackage가 로드되지 않은 경우 QueryStatus 상황에 맞는 메뉴가 발생하지 않습니다. - [#3835](https://github.com/NuGet/Home/issues/3835)

- 솔루션 복원 및 빌드 복원 대화 상자가 계속 표시됩니다. - [#3789](https://github.com/NuGet/Home/issues/3789)

- NuGet.Clients 솔루션 빌드에서 VSSDK 버전을 격리합니다. - [#3890](https://github.com/NuGet/Home/issues/3890)

## <a name="links-to-github-issues-fixed-in-rtm"></a>RTM에서 수정된 GitHub 문제에 대한 링크
[문제 목록 1](https://github.com/NuGet/Home/issues?q=is%3Aissue+is%3Aclosed+milestone%3A%224.0 RTM")  
[문제 목록 2](https://github.com/NuGet/Home/issues?q=is%3Aissue+is%3Aclosed+milestone%3A%224.0 RC4")  
[문제 목록 3](https://github.com/NuGet/Home/issues?q=is%3Aissue+is%3Aclosed+milestone%3A%224.0 RC3")  
[문제 목록 4](https://github.com/NuGet/Home/issues?q=is%3Aissue+is%3Aclosed+milestone%3A%224.0 RC2")  
[문제 목록 5](https://github.com/NuGet/Home/issues?q=is%3Aissue+is%3Aclosed+milestone%3A%224.0 RC")
