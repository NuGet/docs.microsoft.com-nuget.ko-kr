---
ms.openlocfilehash: 9764479d88cc8d87a9f455e64bd46ae8de15055d
ms.sourcegitcommit: e763d9549cee3b6254ec2d6382baccb44433d42c
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/09/2019
ms.locfileid: "68860598"
---
<span data-ttu-id="9eea5-101">프로젝트 파일에 나열된 패키지를 복원하는 [dotnet restore](/dotnet/core/tools/dotnet-restore?tabs=netcore2x) 명령을 사용합니다([PackageReference](../../consume-packages/package-references-in-project-files.md) 참조).</span><span class="sxs-lookup"><span data-stu-id="9eea5-101">Use the [dotnet restore](/dotnet/core/tools/dotnet-restore?tabs=netcore2x) command, which restores packages listed in the project file (see [PackageReference](../../consume-packages/package-references-in-project-files.md)).</span></span> <span data-ttu-id="9eea5-102">.NET Core 2.0 이상에서는 `dotnet build` 및 `dotnet run`을 통해 복원이 자동으로 수행됩니다.</span><span class="sxs-lookup"><span data-stu-id="9eea5-102">With .NET Core 2.0 and later, restore is done automatically with `dotnet build` and `dotnet run`.</span></span> <span data-ttu-id="9eea5-103">NuGet 4.0부터 `nuget restore`와 같은 코드가 실행됩니다.</span><span class="sxs-lookup"><span data-stu-id="9eea5-103">As of NuGet 4.0, this runs the same code as `nuget restore`.</span></span>

<span data-ttu-id="9eea5-104">다른 `dotnet` CLI 명령을 사용할 때처럼 명령줄을 열고 프로젝트 파일이 포함된 디렉터리로 전환합니다.</span><span class="sxs-lookup"><span data-stu-id="9eea5-104">As with the other `dotnet` CLI commands, first open a command line and switch to the directory that contains your project file.</span></span>

<span data-ttu-id="9eea5-105">`dotnet restore`를 사용하여 패키지를 복원하려면 다음을 수행합니다.</span><span class="sxs-lookup"><span data-stu-id="9eea5-105">To restore a package using `dotnet restore`:</span></span>

```cli
dotnet restore 
```