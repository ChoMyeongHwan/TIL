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