`push` 명령의 오류는 일반적으로 문제를 나타냅니다. 예를 들어 프로젝트에서 버전 번호를 업데이트하는 것을 잊었을 수 있고 이미 존재하는 패키지를 게시하려고 시도할 수 있습니다.

또한 호스트에 이미 존재하는 식별자를 사용하여 패키지를 게시하려고 하면 오류가 표시됩니다. 예를 들어 이름 “AppLogger”가 이미 있습니다. 이러한 경우 `push` 명령은 다음 오류를 제공합니다.

```output
Response status code does not indicate success: 403 (The specified API key is invalid,
has expired, or does not have permission to access the specified package.).
```

방금 만든 유효한 API 키를 사용하는 경우 이 메시지는 오류의 “사용 권한” 부분에서 완전히 지워지지 않은 명명 충돌을 나타냅니다. 패키지 식별자를 변경하고, 프로젝트를 다시 빌드하고, `.nupkg` 파일을 다시 만들고, `push` 명령을 다시 시도합니다.