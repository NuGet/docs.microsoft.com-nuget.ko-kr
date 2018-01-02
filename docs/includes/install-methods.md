세 가지 방법으로 패키지를 설치할 수 있습니다.

| 메서드 | 설명 | 참조 |
| --- | --- | --- |
| nuget.exe CLI: `nuget install <package_name>` | \<package_name\>으로 식별되는 패키지를 다운로드하고 현재 디렉터리의 폴더에 해당 내용을 확장합니다. 패키지를 지정하지 않는 경우 프로젝트의 `packages.config` 파일에 나열된 모든 패키지를 설치합니다. 프로젝트 파일이 변경되지 않습니다. 종속성도 다운로드되고 확장됩니다. | [CLI 참조](../tools/nuget-exe-CLI-Reference.md) |
| 패키지 관리자 콘솔(Visual Studio): `Install-Package <package_name>` | 현재 프로젝트에 패키지를 다운로드하고 설치한 다음, 프로젝트 파일을 업데이트하여 패키지를 종속성으로 나열합니다. | [패키지 관리자 콘솔 가이드](../tools/Package-Manager-Console.md) |
| 패키지 관리자 UI(Visual Studio) | 패키지를 찾고, 선택하고, 프로젝트에 설치할 수 있는 UI를 제공합니다. 프로젝트 파일을 업데이트하여 패키지를 종속성으로 나열합니다. | [패키지 관리자 UI 참조](../tools/Package-Manager-UI.md) |