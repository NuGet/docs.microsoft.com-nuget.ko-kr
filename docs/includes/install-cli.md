#### <a name="windows"></a>Windows
1. 방문 [nuget.org/downloads](https://nuget.org/downloads) NuGet 3.3 이상 선택 하 고 (2.8.6 모노와 호환 되지 않습니다.). 최신 버전은 항상 좋으며, 4.1.0+ nuget.org를 패키지를 게시 하려면 필요 합니다.
2. 각 다운로드 되는 `nuget.exe` 파일을 직접 합니다. 선택한 폴더에 파일을 저장 하도록 브라우저에 지시 합니다. 파일은 *하지* ; 설치 관리자는 브라우저에서 직접 실행 하는 경우 아무 것도 표시 되지 않습니다.
3. 배치 하는 위치 폴더 추가 `nuget.exe` 어디에서 나 CLI 도구를 사용 하 여 PATH 환경 변수에 합니다.

#### <a name="macoslinux"></a>macOS/Linux
동작 OS 분배 하 여 약간 다를 수 있습니다.

1. 설치 [모노 4.4.2 이상](http://www.mono-project.com/docs/getting-started/install/)합니다.
2. 셸 프롬프트에서 다음 명령을 실행 합니다.
    
    ```bash
    # Download the latest stable `nuget.exe` to `/usr/local/bin`
    sudo curl -o /usr/local/bin/nuget.exe https://dist.nuget.org/win-x86-commandline/latest/nuget.exe
    # Give the file permissions to execute
    sudo chmod 755 /usr/local/bin/nuget.exe
    ```
3. OS에 대 한 적절 한 파일에 다음 스크립트를 추가 하 여 별칭을 만듭니다 (일반적으로 `~/.bash_aliases` 또는 `~/.bash_profile`):
    
    ```bash
    # Create as alias for nuget
    alias nuget="mono /usr/local/bin/nuget.exe"
    ```
4. 셸 다시 로드 합니다.  입력 하 여 설치를 테스트 `nuget` 매개 변수가 없는 합니다. NuGet CLI 도움말 표시 되어야 합니다.