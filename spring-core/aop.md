# AOP
## AOP란?
- 관점 지향 프로그래밍(Aspect Oriented Programming)
- 중복되는 공통 코드를 분리하고 코드 실행 전이나 후의 시점에 해당 코드를 삽입함으로써 소스 코드의 중복을 줄이고, 필요할 때마다 가져다 쓸 수 있게 객체화하는 기술
- 핵심 관점과 횡단 관점(Logging, Security, 트랜잭션)으로 분류
- Ioc가 낮은 결합도와 관련된 것이라면 **AOP는 높은 응집도**와 관련됨

## AOP 핵심 용어
|용어|설명|
|---|---|
|`Aspect`|핵심 비즈니스 로직과는 별도로 수행되는 횡단 관심사<br> pointcut + advice = **aspect**|
|`Advice`|Aspect의 기능 자체|
|`Join point`|Advice가 적용될 수 있는 위치|
|`Pointcut`|Join point 중에서 Advice가 적용될 가능성이 있는 부분을 선별한 것|
|`Weaving`|Advice를 핵심 비즈니스 로직에 적용하는 것|

## Advice의 시점
|종류|설명|
|---|---|
|`Before`|대상 메소드가 실행되기 이전에 동작|
|`After-returning`|대상 메소드가 정상적으로 실행된 이후에 동작|
|`After-throwing`|예외가 발생했을 때 동작|
|`After`|대상 메소드가 실행된 이후에 동작(정상, 예외 관계X)|
|`Around`|대상 메소드 실행 전/후에 동작<br> Advice 중 가장 강력한 기능을 제공|

# Spring AOP
## Spring AOP 특징
- **프록시 기반의 AOP 구현체**
    * 대상 객체(Target Object)에 대한 프록시를 만들어 제공함
    * 타겟을 감싸는 프록시는 서버 Runtime 시에 생성됨
- **메서드 조인 포인트만 제공**
    * 핵심기능(대상 객체)의 메소드가 호출되는 Runtime 시점에만 부가기능(Advice)을 적용할 수 있음

## 라이브러리 의존성 추가
- AOP 기능이 동작할 수 있도록 build.gradle 파일에 dependencies 추가
```
dependencies {
    ... 생략
    // https://mvnrepository.com/artifact/org.aspectj/aspectjrt
    implementation 'org.aspectj:aspectjrt:1.9.7'
    // https://mvnrepository.com/artifact/org.aspectj/aspectjweaver
    implementation 'org.aspectj:aspectjweaver:1.9.7'
}
```

## AutoProxy 설정
```java
@Configuration
@EnableAspectJAutoProxy(proxyTargetClass = true)
/* proxyTargetClass=true 설정은 cglib를 이용한 프록시를 생성하는 방식
    Spring 3.2부터 별도 설정없이 사용 가능하지만 설정시 성능 면에서 우수함 */
public class ContextConfiguration {
}
```

## Aspect 생성
```java
@Aspect // ponitcut과 advice를 하나의 클래스 단위로 정의하기 위한 어노테이션
@Component
public class LoggingAspect {}
```

## Pointcut
```java
// Pointcut -> 여러 조인 포인트를 매치하기 위해 지정한 표현식
@Pointcut("execution(* com.ohgiraffers.section01.aop.*Service.*(..))")
public void logPointcut() {}
```
- execution 표현식은 메서드 실행 시점에 일치하는 조인포인트를 정의하는데 사용함
```
// 기본 구성
execution([접근제한자패턴] [리턴타입패턴] [클래스이름패턴] [메서드이름패턴]([파라미터타입패턴]))
```

## Before
```java
@Before("LoggingAspect.logPointcut()")  // 대상 메소드가 실행되기 이전에 동작
public void logBefore(JoinPoint joinPoint) {
    /* 매개변수로 전달한 JoinPoint 객체는 현재 조인 포인트의 메소드명, 인수값 등의 
    자세한 정보를 엑세스 할 수 있음*/ 
    System.out.println("Before joinPoint.getTarget() " + joinPoint.getTarget());
    System.out.println("Before joinPoint.getSignature() " + joinPoint.getSignature());
    if(joinPoint.getArgs().length > 0){
        System.out.println("Before joinPoint.getArgs()[0] " + joinPoint.getArgs()[0]);
    }
}
```

## After
```java
@After("logPointcut()")
/* 포인트컷을 동일한 클래스 내에서 사용하는 것이면 클래스명은 생략 가능
    패키지가 다르면 패키지를 포함한 클래스명을 기술 */
public void logAfter(JoinPoint joinPoint) {
    System.out.println("After joinPoint.getTarget() " + joinPoint.getTarget());
    System.out.println("After joinPoint.getSignature() " + joinPoint.getSignature());
    if(joinPoint.getArgs().length > 0){
        System.out.println("After joinPoint.getArgs()[0] " + joinPoint.getArgs()[0]);
    }
}
```

## AfterReturning
```java
@AfterReturning(pointcut="logPointcut()", returning="result")
/* 1. returning 속성은 리턴값으로 받아올 오브젝트의 매개변수 이름과 동일해야 함 
   2. joinPoint는 반드시 첫 번째 매개변수로 선언해야 함 */
public void logAfterReturning(JoinPoint joinPoint, Object result) {
    System.out.println("After Returning result " + result);
    /* 리턴할 결과값을 변경할 수도 있음 */
    if(result != null && result instanceof Map) {
        ((Map<Long, MemberDTO>) result).put(100L, new MemberDTO(100L, "반환 값 가공"));
    }
}
```

## AfterThrowing
```java
@AfterThrowing(pointcut="logPointcut()", throwing="exception")
/* throwing 속성의 이름과 매개변수의 이름이 동일해야 함 */
public void logAfterThrowing(Throwable exception) {
    System.out.println("After Throwing exception " + exception);
}
```

## Around
```java
@Around("logPointcut()")
public Object logAround(ProceedingJoinPoint joinPoint) throws Throwable {
    /* 매개변수는 ProceedingJoinPoint로 고정
       JoinPoint의 하위 인터페이스로 원본 조인포인트의 진행 시점을 제어할 수 있음 */
    System.out.println("Around Before " + joinPoint.getSignature().getName());
    /* 원본 조인포인트를 실행 */
    Object result = joinPoint.proceed();
    System.out.println("Around After " + joinPoint.getSignature().getName());
    /* 원본 조인포인트를 호출한 쪽 혹은 다른 어드바이스가 다시 실행할 수 있도록 반환 */
    return result;
}
```
