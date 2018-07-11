#### <a name="windows"></a><span data-ttu-id="b95e6-101">Windows</span><span class="sxs-lookup"><span data-stu-id="b95e6-101">Windows</span></span>

1. <span data-ttu-id="b95e6-102">[nuget.org/downloads](https://nuget.org/downloads)를 방문하고 NuGet 3.3 이상을 선택합니다(2.8.6은 Mono와 호환되지 않음).</span><span class="sxs-lookup"><span data-stu-id="b95e6-102">Visit [nuget.org/downloads](https://nuget.org/downloads) and select NuGet 3.3 or higher (2.8.6 is not compatible with Mono).</span></span> <span data-ttu-id="b95e6-103">언제나 최신 버전이 권장되며, 패키지를 nuget.org에 게시하려면 4.1.0 이상이 필요합니다.</span><span class="sxs-lookup"><span data-stu-id="b95e6-103">The latest version is always recommended, and 4.1.0+ is required to publish packages to nuget.org.</span></span>
1. <span data-ttu-id="b95e6-104">각 다운로드는 `nuget.exe` 파일입니다.</span><span class="sxs-lookup"><span data-stu-id="b95e6-104">Each download is the `nuget.exe` file directly.</span></span> <span data-ttu-id="b95e6-105">브라우저의 지침에 따라 선택한 폴더에 파일을 저장합니다.</span><span class="sxs-lookup"><span data-stu-id="b95e6-105">Instruct your browser to save the file to a folder of your choice.</span></span> <span data-ttu-id="b95e6-106">파일은 설치 관리자가 ‘아니며’, 브라우저에서 직접 실행하는 경우 아무것도 표시되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="b95e6-106">The file is *not* an installer; you won't see anything if you run it directly from the browser.</span></span>
1. <span data-ttu-id="b95e6-107">`nuget.exe`를 둔 폴더를 PATH 환경 변수에 추가하여 어디서나 CLI 도구를 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="b95e6-107">Add the folder where you placed `nuget.exe` to your PATH environment variable to use the CLI tool from anywhere.</span></span>

#### <a name="macoslinux"></a><span data-ttu-id="b95e6-108">macOS/Linux</span><span class="sxs-lookup"><span data-stu-id="b95e6-108">macOS/Linux</span></span>

<span data-ttu-id="b95e6-109">OS 배포에 따라 동작이 약간 다를 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="b95e6-109">Behaviors may vary slightly by OS distribution.</span></span>

1. <span data-ttu-id="b95e6-110">[Mono 4.4.2 이상](http://www.mono-project.com/docs/getting-started/install/)을 설치합니다.</span><span class="sxs-lookup"><span data-stu-id="b95e6-110">Install [Mono 4.4.2 or later](http://www.mono-project.com/docs/getting-started/install/).</span></span>

1. <span data-ttu-id="b95e6-111">셸 프롬프트에서 다음 명령을 실행합니다.</span><span class="sxs-lookup"><span data-stu-id="b95e6-111">Execute the following command at a shell prompt:</span></span>

    ```bash
    # Download the latest stable `nuget.exe` to `/usr/local/bin`
    sudo curl -o /usr/local/bin/nuget.exe https://dist.nuget.org/win-x86-commandline/latest/nuget.exe
    ```

1. <span data-ttu-id="b95e6-112">다음 스크립트를 OS에 해당하는 파일에 추가하여 별칭을 만듭니다(일반적으로 `~/.bash_aliases` 또는 `~/.bash_profile`).</span><span class="sxs-lookup"><span data-stu-id="b95e6-112">Create an alias by adding the following script to the appropriate file for your OS (typically `~/.bash_aliases` or `~/.bash_profile`):</span></span>

    ```bash
    # Create as alias for nuget
    alias nuget="mono /usr/local/bin/nuget.exe"
    ```

1. <span data-ttu-id="b95e6-113">셸을 다시 로드합니다.</span><span class="sxs-lookup"><span data-stu-id="b95e6-113">Reload the shell.</span></span>  <span data-ttu-id="b95e6-114">매개 변수 없이 `nuget`을 입력하여 설치를 테스트합니다.</span><span class="sxs-lookup"><span data-stu-id="b95e6-114">Test the installation by entering `nuget` with no parameters.</span></span> <span data-ttu-id="b95e6-115">NuGet CLI 도움말이 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="b95e6-115">NuGet CLI help should display.</span></span>
