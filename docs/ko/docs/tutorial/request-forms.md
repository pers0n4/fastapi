# 폼 데이터

JSON 형식의 데이터 대신 폼 필드를 받아야 하는 경우 `Form`을 사용할 수 있습니다.

!!! info "정보"
    폼을 사용하기 위해 먼저 <a href="https://andrew-d.github.io/python-multipart/" class="external-link" target="_blank">`python-multipart`</a>를 설치해야 합니다.

    예시: `pip install python-multipart`.

## `Form` 임포트

`fastapi`에서 `Form`을 임포트합니다:

```Python hl_lines="1"
{!../../../docs_src/request_forms/tutorial001.py!}
```

## `Form` 매개변수 정의

`Body` 또는 `Query`과 같은 방식으로 폼의 매개변수를 생성합니다:

```Python hl_lines="7"
{!../../../docs_src/request_forms/tutorial001.py!}
```

예를 들어 OAuth2 명세에서 사용되는 방식 중 하나인 "password flow"에서는 `username`과 `password`를 JSON이 아닌 폼 필드로 전송해야 합니다.

<abbr title="specification">명세</abbr>에서는 정확히 `username`과 `password`로 명명된 필드들을 JSON이 아닌 폼 필드로 전송하기를 요구합니다.

`Form`을 사용해 `Body` (및 `Query`, `Path`, `Cookie`)와 동일한 메타데이터 및 유효성 검사를 선언할 수 있습니다.

!!! info "정보"
    `Form`은 `Body`를 직접 상속하고 있는 클래스입니다.

!!! tip "팁"
    폼 본문으로 선언하려는 매개변수가 쿼리 매개변수 또는 본문(JSON) 매개변수로 해석되는 것을 방지하기 위해 명시적으로 `Form`을 사용해야 합니다.

## "폼 필드"란

HTML의 폼 (`<form></form>`)을 통해 서버로 데이터를 전송하는 방식은 일반적으로 JSON과는 다른 "특별한" 인코딩을 사용합니다.

**FastAPI**는 JSON 대신 올바른 위치에서 데이터를 읽을 수 있도록 합니다.

!!! note "기술적 세부사항"
    폼으로부터 전달된 데이터는 일반적으로 "미디어 유형" `application/x-www-form-urlencoded`으로 인코딩 됩니다.

    하지만 폼에 파일이 포함된 경우, `multipart/form-data`로 인코딩됩니다. 파일을 제어하는 방법은 다음 장에서 소개합니다.

    인코딩과 폼 필드에 대해 더 알고싶다면, <a href="https://developer.mozilla.org/en-US/docs/Web/HTTP/Methods/POST" class="external-link" target="_blank"><code>POST</code>에 관한 <abbr title="Mozilla Developer Network">MDN</abbr> 웹 문서</a>를 확인하시기 바랍니다.

!!! warning "주의"
    다수의 `Form` 매개변수를 한 *경로 작동*에 선언할 수 있지만, 요청의 본문이 `application/json`가 아닌 `application/x-www-form-urlencoded`로 인코딩 되므로 JSON으로 받아야 하는 `Body` 필드는 함께 선언할 수는 없습니다.

    이는 **FastAPI**의 한계가 아니라, HTTP 프로토콜의 일부입니다.

## 요약

폼 데이터의 입력 매개변수를 선언하기 위해 `Form`을 사용할 수 있습니다.
