#### <a name="windows"></a><span data-ttu-id="8f5ac-101">Windows</span><span class="sxs-lookup"><span data-stu-id="8f5ac-101">Windows</span></span>
1. <span data-ttu-id="8f5ac-102">방문 [nuget.org/downloads](https://nuget.org/downloads) NuGet 3.3 이상 선택 하 고 (2.8.6 모노와 호환 되지 않습니다.).</span><span class="sxs-lookup"><span data-stu-id="8f5ac-102">Visit [nuget.org/downloads](https://nuget.org/downloads) and select NuGet 3.3 or higher (2.8.6 is not compatible with Mono).</span></span> <span data-ttu-id="8f5ac-103">최신 버전은 항상 좋으며, 4.1.0+ nuget.org를 패키지를 게시 하려면 필요 합니다.</span><span class="sxs-lookup"><span data-stu-id="8f5ac-103">The latest version is always recommended, and 4.1.0+ is required to publish packages to nuget.org.</span></span>
2. <span data-ttu-id="8f5ac-104">각 다운로드 되는 `nuget.exe` 파일을 직접 합니다.</span><span class="sxs-lookup"><span data-stu-id="8f5ac-104">Each download is the `nuget.exe` file directly.</span></span> <span data-ttu-id="8f5ac-105">선택한 폴더에 파일을 저장 하도록 브라우저에 지시 합니다.</span><span class="sxs-lookup"><span data-stu-id="8f5ac-105">Instruct your browser to save the file to a folder of your choice.</span></span> <span data-ttu-id="8f5ac-106">파일은 *하지* ; 설치 관리자는 브라우저에서 직접 실행 하는 경우 아무 것도 표시 되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="8f5ac-106">The file is *not* an installer; you won't see anything if you run it directly from the browser.</span></span>
3. <span data-ttu-id="8f5ac-107">배치 하는 위치 폴더 추가 `nuget.exe` 어디에서 나 CLI 도구를 사용 하 여 PATH 환경 변수에 합니다.</span><span class="sxs-lookup"><span data-stu-id="8f5ac-107">Add the folder where you placed `nuget.exe` to your PATH environment variable to use the CLI tool from anywhere.</span></span>

#### <a name="macoslinux"></a><span data-ttu-id="8f5ac-108">macOS/Linux</span><span class="sxs-lookup"><span data-stu-id="8f5ac-108">macOS/Linux</span></span>
<span data-ttu-id="8f5ac-109">동작 OS 분배 하 여 약간 다를 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="8f5ac-109">Behaviors may vary slightly by OS distribution.</span></span>

1. <span data-ttu-id="8f5ac-110">설치 [모노 4.4.2 이상](http://www.mono-project.com/docs/getting-started/install/)합니다.</span><span class="sxs-lookup"><span data-stu-id="8f5ac-110">Install [Mono 4.4.2 or later](http://www.mono-project.com/docs/getting-started/install/).</span></span>
2. <span data-ttu-id="8f5ac-111">셸 프롬프트에서 다음 명령을 실행 합니다.</span><span class="sxs-lookup"><span data-stu-id="8f5ac-111">Execute the following commands at a shell prompt:</span></span>
    
    ```bash
    # Download the latest stable `nuget.exe` to `/usr/local/bin`
    sudo curl -o /usr/local/bin/nuget.exe https://dist.nuget.org/win-x86-commandline/latest/nuget.exe
    # Give the file permissions to execute
    sudo chmod 755 /usr/local/bin/nuget.exe
    ```
3. <span data-ttu-id="8f5ac-112">OS에 대 한 적절 한 파일에 다음 스크립트를 추가 하 여 별칭을 만듭니다 (일반적으로 `~/.bash_aliases` 또는 `~/.bash_profile`):</span><span class="sxs-lookup"><span data-stu-id="8f5ac-112">Create an alias by adding the following script to the appropriate file for your OS (typically `~/.bash_aliases` or `~/.bash_profile`):</span></span>
    
    ```bash
    # Create as alias for nuget
    alias nuget="mono /usr/local/bin/nuget.exe"
    ```
4. <span data-ttu-id="8f5ac-113">셸 다시 로드 합니다.</span><span class="sxs-lookup"><span data-stu-id="8f5ac-113">Reload the shell.</span></span>  <span data-ttu-id="8f5ac-114">입력 하 여 설치를 테스트 `nuget` 매개 변수가 없는 합니다.</span><span class="sxs-lookup"><span data-stu-id="8f5ac-114">Test the installation by entering `nuget` with no parameters.</span></span> <span data-ttu-id="8f5ac-115">NuGet CLI 도움말 표시 되어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="8f5ac-115">NuGet CLI help should display.</span></span>