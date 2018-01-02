### <a name="priority-ordering"></a><span data-ttu-id="ad3b4-101">우선 순위 순서</span><span class="sxs-lookup"><span data-stu-id="ad3b4-101">Priority ordering</span></span>

<span data-ttu-id="ad3b4-102">기본적으로 처리 순서와 반대인 설정이 적용되는 "우선 순위 순서"에 대해 이해할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="ad3b4-102">It can also help to think about the "priority order" in which settings are applied, which is essentially the reverse of the processing order.</span></span> <span data-ttu-id="ad3b4-103">예를 들어 프로젝트가 `c:\A\B\C`에 있는 경우 NuGet에서는 다음과 같은 우선 순위 순서로 설정을 적용합니다. 즉, 순서가 높은 설정이 먼저입니다.</span><span class="sxs-lookup"><span data-stu-id="ad3b4-103">For example, if a project is located in `c:\A\B\C`, then NuGet applies settings in the following priority order, meaning settings found higher up in the order win:</span></span>

    (For solution-level packages only in NuGet 2.x; ignored in NuGet 3.x)
    c:\A\B\C\.nuget\NuGet.Config

    (For all version of NuGet)
    c:\A\B\C\NuGet.Config
    c:\A\B\NuGet.Config
    c:\A\NuGet.Config
    c:\NuGet.Config

    configFile, if specified

    (Ignored in NuGet 3.4 and later if -configFile is used)
    %AppData%\NuGet\NuGet.Config

    (NuGet 2.6 to 3.5)
    %ProgramData%\NuGet\Config\{IDE}\{Version}\{SKU}\NuGet.Config
    %ProgramData%\NuGet\Config\{IDE}\{Version}\NuGet.Config
    %ProgramData%\NuGet\Config\{IDE}\NuGet.Config
    %ProgramData%\NuGet\Config\NuGet.Config

    (NuGet 4.0+)
    %ProgramFiles(x86)%\NuGet\Config\{IDE}\{Version}\{SKU}\NuGet.Config
    %ProgramFiles(x86)%\NuGet\Config\{IDE}\{Version}\NuGet.Config
    %ProgramFiles(x86)%\NuGet\Config\{IDE}\NuGet.Config
    %ProgramFiles(x86)%\NuGet\Config\NuGet.Config