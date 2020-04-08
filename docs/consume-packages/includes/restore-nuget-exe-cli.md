---
ms.openlocfilehash: 2fc62e7161a07d739760ed638653fbdec0dfc330
ms.sourcegitcommit: 2b50c450cca521681a384aa466ab666679a40213
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/07/2020
ms.locfileid: "68860568"
---
<span data-ttu-id="a1c41-101">[복원](../../reference/cli-reference/cli-ref-restore.md) 명령을 사용하면 *패키지* 폴더에서 누락된 모든 패키지를 다운로드하고 설치할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="a1c41-101">Use the [restore](../../reference/cli-reference/cli-ref-restore.md) command, which downloads and installs any packages missing from the *packages* folder.</span></span>

<span data-ttu-id="a1c41-102">PackageReference로 마이그레이션된 프로젝트의 경우 대신 [msbuild -t:restore](../package-restore.md#restore-using-msbuild)를 사용하여 패키지를 복원합니다.</span><span class="sxs-lookup"><span data-stu-id="a1c41-102">For projects migrated to PackageReference, use [msbuild -t:restore](../package-restore.md#restore-using-msbuild) to restore packages instead.</span></span>

<span data-ttu-id="a1c41-103">`restore`는 디스크에만 패키지를 추가하지만 프로젝트의 종속성은 변경하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="a1c41-103">`restore` only adds packages to disk but does not change a project's dependencies.</span></span> <span data-ttu-id="a1c41-104">프로젝트 종속성을 복원하려면 `packages.config`를 수정한 다음, `restore` 명령을 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="a1c41-104">To restore project dependencies, modify `packages.config`, then use the `restore` command.</span></span>

<span data-ttu-id="a1c41-105">다른 `nuget.exe` CLI 명령을 사용할 때처럼 명령줄을 열고 프로젝트 파일이 포함된 디렉터리로 전환합니다.</span><span class="sxs-lookup"><span data-stu-id="a1c41-105">As with the other `nuget.exe` CLI commands, first open a command line and switch to the directory that contains your project file.</span></span>

<span data-ttu-id="a1c41-106">`restore`를 사용하여 패키지를 복원하려면 다음을 수행합니다.</span><span class="sxs-lookup"><span data-stu-id="a1c41-106">To restore a package using `restore`:</span></span>

```cli
nuget restore MySolution.sln
```