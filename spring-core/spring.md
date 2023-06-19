# 프로젝트 관련 공부
## Lombok
- 자바 클래스에서 반복적으로 작성되는 getter, setter, toString, 생성자 코드 등의 소스들을 어노테이션을 사용하여 생략할 수 있도록 컴파일 시점에 자동으로 생성해주는 라이브러리
- Lombok Annotation 종류
    * @Getter : 해당 멤버 변수에 대한 getter를 생성
    * @Setter : 해당 멤버 변수에 대한 setter를 생성
    * @ToString : 해당 클래스의 toString()을 자동으로 생성
    * @EqualsAndHashCode : 해당 클래스의 equals()와 hashCode()를 자동으로 생성
    * @NoArgsConstructor : 파라미터가 없는 생성자를 생성
    * @AllArgsConstructor : 모든 멤버 변수를 파라미터로 받는 생성자를 생성
    * @RequiredArgsConstructor : final이나 @NonNull인 멤버 변수만 파라미터로 받는 생성자를 생성
    * @Data : @ToString, @EqualsAndHashCode, @Getter, @Setter, @RequiredArgsConstructor을 모두 적용한 것과 동일

## IoC Container
- IoC란 제어의 역전(Inversion of Control), 일반적인 프로그래밍에서 프로그램의 제어 흐름 구조가 뒤바뀌는 것을 의미
- 대표적인 IoC Container -> Spring Framework의 **ApplicationContext**

## Bean
- Spring IoC Container에서 관리되는 객체
    * 스프링은 Bean을 생성하고, 초기화하고, 의존성 주입하고, 제거하는 등의 일을 IoC Container를 통해 자동으로 처리할 수 있음
- BeanFactory -> Spring IoC Container의 가장 기본적인 형태
    * Bean의 생성, 초기화, 연결, 제거 등의 라이프사이클을 관리

## @ComponentScan
- base package로 설정 된 하위 경로에 특정 어노테이션을 가지고 있는 클래스를 bean으로 등록하는 기능
- @Component 어노테이션이 작성 된 클래스를 인식하여 bean으로 등록
    
    |종류|설명|
    |---|---|
    |`@Component`|객체를 나타내는 일반적인 타입으로 bean 태그와 동일한 역할|
    |`@Controller`|프리젠테이션 레이어. 웹 어플리케이션에서 View에서 전달된 웹 요청과 응답을 처리하는 클래스 ex) Controller Class|
    |`@Service`|서비스 레이어, 비즈니스 로직을 가진 클래스 ex) Service Class|
    |`@Repository`|퍼시스턴스(persistence) 레이어, 영속성을 가지는 속성(파일, 데이터베이스)을 가진 클래스 ex) Data Access Object Class|
    |`@Configuration`|빈을 등록하는 설정 클래스|
