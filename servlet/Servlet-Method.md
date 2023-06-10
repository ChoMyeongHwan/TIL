# Servlet Method
## 사용자 데이터 전송 방식
- get 방식
    * URL 창에 "?" 뒤에 데이터를 입력하는 방법(=쿼리스트링)으로 전송
    * 전송 데이터가 여러 개이면 &로 묶어서 보냄
    * 데이터 검색에 주로 사용, 데이터 크기 한계가 있고 보안에 취약함

* post 방식
    * HTTP header의 내용으로 데이터를 전송
    * 전송 데이터 크기 제한이 없고, header에 포함해 전송하므로 보안이 우수함

## 데이터 전송 방식에 따른 Servlet Method
1. doGet()
    * 클라이언트에서 get으로 데이터 전송을 하면 호출되는 메소드
2. doPost()
    * 클라이언트에서 post로 데이터 전송을 하면 호출되는 메소드
- 이때, 반드시 **ServletException 처리를 해야 함**

## Servlet 매개변수 객체
- `HttpServletRequest` (interface)
    * HTTP Servlet을 위한 요청 정보를 제공하는 객체
    * Method
        |method명|내용|
        |---|---|
        |getParameter(String)|client가 전송한 값의 명칭이 매개변수와 같은 값 가져옴|
        |getParameterNames()|client가 전송한 값의 명칭 가져옴|
        |getParameterValues(String)|client가 전송한 값이 여러 개이면 배열로 가져옴|
        |getParameterMap()|client가 전송한 값 전체를 Map방식으로 가져옴|
        |setAttribute(String, object)|request 객체로 전달할 값을 String 이름-Object 값으로 설정|
        |getAttribute(String)|매개변수와 동일한 객체 속성 값 가져옴|
        |removeAttribute(String)|request객체에 저장된 매개변수와 동일한 속성 값 삭제|
        |setCharacterEncoding(String)|전송 받은 request객체 값들의 CharaterSet 설정|
        |getRequestDispatcher(String)|컨테이너 내에서 request, response객체를 전송하여 처리한 컴포넌트(jsp파일 등)를 가져옴 (forward() method와 같이 사용)|

- `HttpServletResponse` (interface)
    * 요청에 대한 처리 결과를 작성하기 위해 사용하는 객체
    * Method
        |method명|내용|
        |---|---|
        |setContentType(String)|응답으로 작성하는 페이지의 MIME type을 설정|
        |setCharacterEncoding(String)|응답하는 데이터의 CharacterSet을 지정|
        |getWriter()|페이지에 문자 전송을 위한 Stream을 가져옴|
        |getOutputStream()|페이지에 byte단위의 전송을 위한 Stream을 가져옴|
        |sendRedirect(String)|client가 매개변수의 페이지를 다시 서버에 요청함|

## sendRedirect & encodeRedirectURL
>- client 브라우저에게 “(매개변수로 등록한) 페이지를 재요청하라”고 응답. (301/302 코드)
>- encodeRedirectURL은 매개변수(URL)에 Session ID 정보를 추가하여 재요청 처리
>- client가 별도로 다른 페이지 요청을 하지 않아도 url주소(페이지)가 변경됨
>- 브라우저가 알아서 서버에 해당 페이지를 요청하며, 쿼리스트링으로 별도의 데이터를 전송하지 않으면 요청 데이터가 없다.

## RequestDispatcher() ~ forward()
>- 컨테이너 내에서 처음 요청 받은 페이지가 요청 데이터 (HttpServletRequest, HttpServletResponse)를 다른 페이지에 전송하여 처리를 요청하고, 자신이 처리한 것처럼 응답한다.
>- url주소(페이지)가 변경되지 않음.

## 객체별 공유 데이터 설정
- 공유 데이터는 Map 형식으로 저장됨
- ServletContext, ServletRequest, HttpSession 객체에서 사용하는 method

    |method|내용|
    |---|---|
    |setAttribute(String,Object)|공유 데이터 저장|
    |getAttribute(String)|공유 데이터 가져옴|
    |getAttributeName()|공유 데이터 전체의 명칭 가져옴|
    |removeAttribute(String)|공유 데이터 자체를 삭제|
