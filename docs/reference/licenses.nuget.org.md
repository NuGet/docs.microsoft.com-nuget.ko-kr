# <a name="licensesnugetorg"></a>licenses.nuget.org

## <a name="rationale"></a>설명

도입 된 [식 라이선스](nuspec.md#license) 개별 라이선스 식별자, 예외 식별자 또는 라이선스 식에 대 한 참조 텍스트를 제공 하는 신뢰할 수 있는 서비스에 등장 한 후 요구 사항.
이 서비스에 대 한 추가 요구 사항은 이전 버전의 클라이언트에 대 한 이전 버전과 호환성을 제공 하기 안전 하 게 사용할 수 있도록, rot에 대 한 연결에 취약 하지 않은 안정적인 URL 스키마를 가진 하는 것입니다.

Licenses.nuget.org 해당 역할을 수행 합니다. Nuget.org는 라이선스 식을 사용 하 여 해당 라이선스를 지정 하는 패키지에 대 한 라이선스 텍스트 참조를 제공 하는 데 사용 합니다. `nuget pack` 또는 다른 압축 [클라이언트 도구](https://docs.microsoft.com/en-us/nuget/install-nuget-client-tools) 설정 된 [ `licenseUrl` ](nuspec.md#licenseurl) licenses.nuget.org 이전 버전과 호환성을 제공 하기를 지원 하지 않는 이전 버전의 클라이언트를 가리키도록 요소는 `license` 요소입니다.

## <a name="protocol"></a>프로토콜

사용자가 브라우저에서 볼 수 있도록 Licenses.nuget.org 것, 컴퓨터가 읽을 수 있는 응답이 없습니다 제공 됩니다.
HTTPS 프로토콜을 사용 해야 하 고 요청을 특정 방식으로 생성할 수 해야 합니다. 지원 `GET` 요청 합니다.
라이선스 식 또는 라이선스 예외 식별자 아래에 지정 하는 방법에 대 한 입력으로 허용 합니다. 하세요 note, 라이선스 식의 모든 요소는 대 소문자를 구분 하 고 따라서 licenses.nuget.org에 대 한 모든 입력도 대/소문자 구분 합니다.

### <a name="license-expressions"></a>라이선스 식

#### <a name="request"></a>요청

라이선스 식 (식은 단일 라이선스의 경우 간단한 사례 포함) 일 필요가 [URL로 인코딩된](https://tools.ietf.org/html/rfc3986#section-2.1) licenses.nuget.org 요청에 경로로 사용 합니다.

| 라이선스 식 | 사용 하는 URL |
|:---|:---|
MIT                                                | https://licenses.nuget.org/MIT
(MIT)                                              | https://licenses.nuget.org/(MIT)
(LGPL 2.0 전용 FLTK 예외 또는 Apache를 사용 하 여-2.0+) | https://licenses.nuget.org/(LGPL-2.0-only%20WITH%20FLTK-exception%20OR%20Apache-2.0+)

서비스는 라이선스 식별자 및 nuget.org에서 허용 되는 라이선스 예외 식별자만 지원 합니다. 모든 라이선스 식은 지원 되지 않는 라이선스 식별자 또는 라이선스 예외 식별자를 포함 하는 라이선스 식 구문에 맞지 않습니다 또는 잘못 된 간주 됩니다.

#### <a name="response"></a>응답

Licenses.nuget.org는 HTTP 200 상태 코드 및 라이선스 식의 설명이 포함 된 웹 페이지를 사용 하 여 식이 유효한 라이선스가 포함 된 요청에 응답 합니다.
* 라이선스 식을 제공 하는 경우 해당 라이선스 참조 텍스트를 포함 하는 웹 페이지는 반환 하는 단일 라이선스 식별자가 포함
* 제공 된 경우 라이선스 식은 복합 라이선스 식이고, 웹 페이지의 개별 라이선스 또는 라이선스 예외 참조에 대 한 링크를 사용 하 여 라이선스 식을 포함 하는 반환 됩니다.

HTTP 404 응답에 잘못 된 라이선스 식 결과 포함 하는 모든 요청 합니다.

### <a name="license-exceptions"></a>라이선스 예외

#### <a name="request"></a>요청

라이선스 예외 식별자 URL로 인코딩된 및 licenses.nuget.org 요청에 경로 사용 해야 합니다. 단일 라이선스 예외 식별자만 단일 요청에 제공할 수 있습니다. 라이선스 예외 식별자 외에도 추가 문자가 없는 URL의 경로 부분에 있을 수 있습니다.

| 라이선스 예외 식별자 | 사용 하는 URL |
|:---|:---|
FLTK 예외            | https://licenses.nuget.org/FLTK-exception
openvpn-openssl-exception | https://licenses.nuget.org/openvpn-openssl-exception

#### <a name="response"></a>응답

Licenses.nuget.org는 HTTP 200 응답 및 지정 된 라이선스는 예외에 대 한 참조 텍스트를 포함 하는 웹 페이지를 사용 하 여 알려진된 라이선스 예외 식별자를 사용 하 여 요청에 응답 합니다.

지원 되지 않는 라이선스 예외 식별자를 포함 하는 모든 요청에서 HTTP 404 응답을 발생 합니다.