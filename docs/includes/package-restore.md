- **패키지 관리자 UI**(Visual Studio): 솔루션 탐색기에서 솔루션을 마우스 오른쪽 단추로 클릭하고 **NuGet 패키지 복원**을 선택합니다. 하나 이상의 개별 패키지가 경우 여전히 올바르게 설치되지 않은 경우(즉, 솔루션 탐색기에 오류 아이콘이 표시됨) 패키지 관리자 UI를 사용하여 영향을 받는 패키지를 제거하고 다시 설치합니다. [패키지 다시 설치 및 업데이트](../Consume-Packages/Reinstalling-and-Updating-Packages.md)를 참조하세요.

- **명령줄**: [NuGet 복원](../tools/cli-ref-restore.md) 명령을 사용합니다. 프로젝트 폴더에서 `nuget restore`를 실행하기만 하면 프로젝트의 종속성을 복원하려고 시도합니다.
