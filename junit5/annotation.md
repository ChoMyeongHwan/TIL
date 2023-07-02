# Annotation
## JUnit5 서브 프로젝트
- JUnit Platform : JVM에서 테스트 프레임워크를 실행하기 위한 테스트 엔진을 제공
- JUnit Jupiter : JUnit5에서 테스트를 작성하고 실행하기 위한 엔진을 제공
- JUnit Vintage : JUnit3, 4를 기반으로 돌아가는 테스트 엔진을 제공(하위 호환용)

## 테스트 클래스
- 적어도 한 개 이상의 @Test 어노테이션이 달린 메소드를 가진 클래스
- abstract이면 안되고, 한 개의 생성자를 가지고 있어야 함
    * 두 개 이상 작성하면 런타임 시 PreconditionViolationException이 발생
    * 아무런 생성자도 작성하지 않으면 기본 생성자는 컴파일러가 자동으로 추가
- @Test 메소드는 단독 실행 가능
- 기본적으로 테스트 이름은 메소드 이름을 따라가지만 @DisplayName에 설정한 이름으로 테스트의 이름을 표기
- 과거에는 공백문자를 언더파로 표기한 한글 메소드 형태로 테스트메소드를 작성하기도 했음
- 클래스 레벨에 @DisplayNameGenerator를 붙이게 되면 언더바를 공백으로 처리하여 테스트 이름을 부여해줌
    * 단, @DisplayName과 중복 작성 시 @DisplayName에 부여한 테스트 이름이 우선권을 가짐
- 각각의 테스트는 실행 순서를 작성 순서로 보장하지 않음

## Lifecycle Annotation
- 모든 테스트 메소드와 라이프사이클 관련 메소드는 abstract이면 안되고, **void** 형으로 작성
- 접근제한자는 사용하지 않아도 되지만(default), private이면 안됨
- 종류
    * @BeforeAll
        + 테스트가 실행되기 전 딱 한 번만 실행됨
    * @BeforeEach
        + 각각의 테스트 메소드가 실행되기 전 실행됨
        + @Test, @RepeatedTest, @ParameterizedTest, @TestFactory가 실행되기 전에 동작
        + 주로 테스트 하기 전에 필요한 목업 데이터를 미리 세팅해 줄 목적으로 사용
    * @AfterEach
        + 각각의 테스트 메소드가 동작한 직후 동작함
        + @Test, @RepeatedTest, @ParameterizedTest, @TestFactory가 실행된 이후 동작
        + 주로 단위 테스트들이 수행된 이후 사용한 자원을 해제할 목적으로 사용
    + @AfterAll
        + 모든 단위 테스트가 완전히 끝난 후 딱 한 번만 실행됨