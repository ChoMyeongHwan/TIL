# 개요
## Network 통신
- Sever-Client Model
    * Client(서비스 사용자) -> Request(요청)
    * Server(서비스 제공자) -> Response(응답)

- Server의 종류
    |종류|설명|
    |---|---|
    |`Web Server`|웹 브라우저와 HTTP 프로토콜을 사용하여 사용자의 요구에 따른 특정 서비스 제공|
    |Mail Server|인터넷을 통해 사용자 간의 전자 우편을 주고 받는 서비스 제공|
    |FTP Server|서버 내에 파일을 업로드, 다운로드 할 수 있도록 파일 관리 기능 제공|
    |Talnet Server|Terminal, 텍스트로만 이루어진 창에서 특정 명령어를 통해 원격지 서버를 접속 및 관리|
    |Database Server|데이터를 저장하고, 원격지에 접속할 경우 권한에 따라 해당 데이터를 열람, 추가, 수정, 삭제하는 기능 처리|

## Web 통신
- 개별(로컬) 프로그램과 서버 프로그램의 특징
    * 개별 프로그램
        1. 프로그램 업데이트 발생 시 각각 다시 다운로드 해야 함
        2. 각 프로그램에서 생성된 데이터는 개별 저장되어 공유 불가함

    * 서버 프로그램
        1. 프로그램 업데이트 발생 시 서버가 상관하지 않아도 클라이언트가 서버에서 다운받아 업데이트를 개별적으로 진행함
        2. 데이터는 서버에 일괄 저장됨

- Web & WAS
    * 구조 : Web browser ↔ Web(html) ↔ WAS
    * web(html)은 사전에 작성된 화면으로 정적인 페이지를 의미함
    * 서버는 따로 두고 일단 클라이언트 요청에 대해 web에서 응답한 뒤에, 처리할 동적 요청 등 필요에 따라 was에 요청하여 응답함
    * WAS는 Servlet을 보관하다가 서블릿 라이프사이클에 따라 생성, 소멸 등을 주관하는 역할 -> Servlet Container

## CGI & WAS
- CGI(Common Gateway Interface)
    * 웹 서버가 직접적으로 웹 프로그램을 실행하는 방식
    * 동일 프로그램에 대한 요청이 있을 때마다 각각의 프로그램을 실행하여, 요청과 프로그램이 1:1 매칭되어 실행됨

- WAS(Web Application Server)
    * 웹 서버가 웹 애플리케이션 서버에 요청하면, 웹 애플리케이션 서버가 해당 프로그램을 실행하는 방식
    * 동일 프로그램에 대한 여러 요청이 있으면 한 개의 프로그램을 실행하여 다수 요청을 처리(Multi Threading)

- Container(Servlet, JSP)
    * Servlet-Container
        + Servlet의 생명 주기(생성, 초기화, 소멸)를 관리
        + HttpServletRequest, HttpServletResponse 객체를 생성
        + 요청에 따라 멀티스레딩 구성이 가능하며, 전송 방식에 따라 동적으로 페이지 구성하는 작업을 진행
        + 정적 로딩 처리
    * JSP-Container
        + JSP 파일을 java코드로 변경해주고 class파일로 전환하여 메모리 공간에 로드한 뒤 실행 가능하게 만드는 작업(= Servlet화)
        + 처리 결과를 HTML파일로 만들어주는 작업을 진행
        + 동적 로딩 처리

- Web Server & WAS
    |구분|장점|단점|
    |---|---|---|
    |`Web Server`|- 빠른 처리 속도<br> - 쉬운 구현|- 한정적인 서비스<br> - 글의 추가, 수정, 삭제가 어려움|
    |`WAS`|- 서비스의 다양성<br> - 글의 추가, 수정, 삭제가 쉬움|- 느린 처리 속도<br> - 어려운 구현|
