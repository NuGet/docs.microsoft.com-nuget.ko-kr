---
title: 설치된 패키지 문제 해결
description: 개별 패키지에 사용된 패키지 원본을 찾는 방법
author: JonDouglas
ms.author: jodou
ms.date: 03/26/2021
ms.topic: conceptual
ms.openlocfilehash: 22fb51ebb996c66e10b860f0158676fd2d9da295
ms.sourcegitcommit: c8bf16420f235fc3e42c08cd0d56359e91d490e5
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/14/2021
ms.locfileid: "107387534"
---
# <a name="troubleshooting-installed-packages"></a>설치된 패키지 문제 해결

어떤 원본으로부터 특정 패키지가 설치되었는지 확인하려는 경우가 있습니다. 다음은 이를 확인할 수 있는 몇 가지 방법입니다.

> [!Note]
> 일부 패키지 원본은 업스트림 소스라는 개념을 지원합니다. [Azure Artifacts 업스트림 소스](/azure/devops/artifacts/concepts/upstream-sources)를 예로 들 수 있습니다. NuGet 클라이언트는 패키지를 업스트림 소스에서 가져왔는지 여부를 알지 못합니다. 따라서 패키지 원본 로깅 시 업스트림 소스가 아닌 구성된 원본이 나열됩니다.

## <a name="nupkgmetadata-file-in-global-packages-folder"></a>전역 패키지 폴더의 `.nupkg.metadata` 파일

패키지가 *global-packages* 폴더에 추출되면 `.nupkg.metadata` 파일이 기록됩니다. NuGet 5.9.0 이상 버전부터 NuGet은 패키지 원본을 추가합니다. NuGet 버전을 Visual Studio 또는 .NET SDK 버전에 매핑하려면 아래를 참조하세요. 예를 들면 다음과 같습니다.

```json
{
  "version": 2,
  "contentHash": "bw3R9q8cVNhWXNpnvWb0OGP4HadS4zvClq+T1zf7AF+tLY1haZ2AvbHidQekf4PDv1T40c6brZeT/V0IBq7cEQ==",
  "source": "https://api.nuget.org/v3/index.json"
}
```

> [!Note]
> *global-packages* 폴더에 NuGet 5.9.0이 포함된 최신 버전의 도구로 업그레이드하기 전 추출한 패키지가 있는 경우, `.nupkg.metadata` 파일의 버전은 1이며 패키지 원본을 포함하지 않습니다. [*global-packages* 폴더를 지워](../consume-packages/managing-the-global-packages-and-cache-folders.md#clearing-local-folders) 모든 패키지에 패키지 원본이 포함되도록 할 수 있습니다.

> [!Tip]
> NuGet은 *global-packages* 폴더에만 `.nupkg.metadata` 파일을 씁니다. `packages.config`를 사용하는 프로젝트는 `.nupkg.metadata` 파일을 만들지 않는 솔루션 패키지 폴더를 사용합니다.

## <a name="installed-package-log-message"></a>설치된 패키지 로그 메시지

NuGet 5.9.0 이상 버전부터 NuGet은 패키지가 설치되었음을 알리는 복원 메시지에서 패키지 원본을 출력합니다. 예를 들면 다음과 같습니다.

```text
Installed Moq 4.16.1 from https://api.nuget.org/v3/index.json with content hash bw3R9q8cVNhWXNpnvWb0OGP4HadS4zvClq+T1zf7AF+tLY1haZ2AvbHidQekf4PDv1T40c6brZeT/V0IBq7cEQ==.
```

> [!Tip]
> 이 메시지는 일반/알림 세부 정보 표시에 출력됩니다. Visual Studio 및 `dotnet` CLI는 기본적으로 최소한의 세부 정보를 표시하므로 이 메시지는 기본적으로 표시되지 않습니다. `msbuild` 및 `nuget` CLI 도구는 기본적으로 일반적인 세부 정보를 표시하므로 이 메시지는 기본적으로 표시됩니다.

## <a name="http-log-message"></a>HTTP 로그 메시지

*global-packages* 폴더, 대체 폴더 또는 로컬 파일 원본 중 하나에서 로컬로 패키지를 사용할 수 없는 경우, NuGet은 HTTP를 통해 구성된 모든 패키지 원본에서 패키지를 다운로드합니다. HTTP 요청 및 응답은 일반적인 세부 정보 표시 수준으로 로그되며 패키지 버전당 하나의 요청 및 응답만 표시됩니다. 예를 들면 다음과 같습니다.

```text
info :   GET https://api.nuget.org/v3-flatcontainer/moq/index.json
info :   OK https://api.nuget.org/v3-flatcontainer/moq/index.json 56ms
info :   GET https://api.nuget.org/v3-flatcontainer/moq/4.16.1/moq.4.16.1.nupkg
info :   OK https://api.nuget.org/v3-flatcontainer/moq/4.16.1/moq.4.16.1.nupkg 3ms
```

최근에 파일을 다운로드한 경우 NuGet의 *http-cache* 에서 검색할 수 있습니다.

```text
CACHE https://api.nuget.org/v3-flatcontainer/moq/index.json
CACHE https://api.nuget.org/v3-flatcontainer/moq/4.16.1/moq.4.16.1.nupkg
```

URL 형식은 다양한 NuGet HTTP 서버 구현과 형식이 NuGet V2 또는 V3 HTTP 프로토콜을 구현하는지 여부에 따라 다를 수 있습니다.

`nuget.config`에 여러 HTTP 소스가 정의되어 있는 경우, 각 패키지의 `index.json` 파일에 대한 여러 요청이 각 원본에 대해 하나씩 표시됩니다. 그러나 패키지의 각 버전에 대한 `nupkg` 다운로드는 하나만 표시됩니다.

## <a name="package-signature-log-message"></a>패키지 서명 로그 메시지

다운로드되는 패키지가 서명된 경우, NuGet은 서명의 유효성을 검사하고 다음 메시지를 자세한 세부 정보 수준으로 표시합니다.

```text
PackageSignatureVerificationLog: PackageIdentity: Moq.4.16.1 Source: https://api.nuget.org/v3/index.json PackageSignatureValidity: True
```

이 메시지는 패키지가 HTTP 패키지 원본에서 다운로드되었는지 또는 로컬 패키지 원본에서 복사되었는지를 보고합니다. 패키지를 *global-packages* 폴더 또는 대체 폴더에서 이미 사용할 수 있는 경우 해당 메시지는 출력되지 않습니다.

> [!Important]
> [VeriSign CA의 신뢰 제거](https://github.com/dotnet/announcements/issues/180)로 인해 NuGet은 특정 버전의 NuGet 및 .NET SDK에서 특정 플랫폼에 대한 서명된 패키지 확인을 사용하지 않도록 설정했습니다. 따라서 복원을 실행하는 플랫폼 및 사용 중인 .NET 또는 NuGet 버전에 따라 동일한 패키지에 `PackageSignatureVerificationLog` 로그가 있거나 해당 로그가 누락될 수 있습니다.

## <a name="nuget-version-map"></a>NuGet 버전 맵

다음 버전의 NuGet에는 패키지 원본 로깅과 관련된 중요한 변경 사항이 있습니다.

|NuGet 버전|Visual Studio 버전|.NET SDK 버전|
|---|---|---|
|NuGet 5.9.0|Visual Studio 2019 16.9.0|.NET 5 SDK 5.0.200|
