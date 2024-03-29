## JWT (JSON Web Token)

### 1. JWT란?
- JWT (JSON Web Token)은 선택적 서명 및 선택적 암호화를 사용하여 데이터를 안전하게 만들기 위한 인터넷 표준임 
- 이를 통해 서버는 클레임(claim) 정보를 포함한 토큰을 생성하고 이를 클라이언트에 제공할 수 있음
- 클라이언트는 이 토큰을 사용하여 클레임에 대한 증명을 할 수 있음
- JWT는 주로 웹 애플리케이션에서 사용자 인증 및 권한 부여에 활용됨

### 2. JWT의 구조

JWT는 세 부분으로 구성됨

- **Header(헤더)**: 토큰의 서명 알고리즘과 유형을 정의함 (예: `"alg": "HS256", "typ": "JWT"`와 같이 정의)

- **Payload(페이로드)**: 클레임(claim) 정보를 포함함. `"sub"`(subject), `"iss"`(issuer), `"exp"`(expiration time) 등이 일반적으로 포함됨

- **Signature(서명)**: 토큰의 무결성을 검증하기 위한 서명. 서버는 이 서명을 확인하여 토큰의 유효성을 검사함

### 3. JWT의 사용 예시

JWT는 주로 웹 애플리케이션에서 사용자 인증 및 권한 부여에 사용된다. 사용자가 로그인하면 서버에서 JWT를 생성하고 클라이언트에 반환한다. 클라이언트는 이 JWT를 요청에 포함하여 서버에 인증을 요청하고 권한을 부여받는다.

### 4. JWT의 이점

- 간단하고 가벼움: JSON 형식을 사용하므로 다루기 쉬움
- 자체 포함: 서명을 통해 토큰의 무결성을 검증하므로 추가 데이터베이스 조회 없이도 검증 가능함
- 보안: 서명을 통해 토큰의 무결성을 검증하므로 안전하게 사용 가능함

### 5. JWT 구현체

JWT는 다양한 언어와 프레임워크에서 구현되어 있으며, 각 언어 및 프레임워크에 맞는 라이브러리를 사용하여 JWT를 생성하고 검증할 수 있다.

### 6. 보안 취약성

JWT의 적절한 구현이 중요하며, 알고리즘 선택과 키 크기, 취약성 등을 고려해야 한다. 취약성을 해결하기 위해 일부 주의가 필요하며, 서명 알고리즘 및 키 관리를 신중하게 다루어야 한다.