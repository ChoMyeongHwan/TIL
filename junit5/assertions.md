# Assertions

### JUnit Jupiter는 JUnit4로부터 온 assertion 메소드와 새롭게 자바8 람다 표현식으로 추가된 메소드를 제공함

## 테스트코드 작성 패턴
- given - when - then 패턴
    * given : 테스트 시 필요한 파라미터를 준비
    
    * when : 테스트 할 메소드를 호출
    
    * then : 실행 결과를 검증

- when & then 동시 진행 경우도 있음

## 메소드 종류
- assertEquals(expected, actual) : 실제 값과 기대 값의 일치 여부를 동일성으로 판단
- assertNotEquals(expected, actual) : 불일치 여부를 동일성(같은 주소)으로 판단

- assertNull(actual) : 참조변수가 null값을 가지는지 판단
- assertNotNull(actual) : null값을 가지지 않는지 판단

- assertTrue(actual) : 결과 값이 true인지 판단
- assertFalse(actual) : 결과 값이 false인지 판단

- assertAll(Executable...) : 모든 Assertion이 실행되고 실패가 함께 보고되는 그룹화된 Assertion
```java
@Test
@DisplayName("동시에 여러 가지 값에 대한 검증")
void testAssertAll() {

    //given
    String firstName = "길동";
    String lastName = "홍";

    //when
    Person person = new Person(firstName, lastName);

    //then
    Assertions.assertAll(
        "그룹화된 테스트의 이름(테스트 실패 시 보여짐)",
        () -> Assertions.assertEquals(firstName, person.getFirstName(), () -> "firstName이 잘못됨"),
        () -> Assertions.assertEquals(lastName, person.getLastName(), () -> "lastName이 잘못됨")
    );
}
```

- assertDoesNotThrow(excutable) : 메소드 호출 시 아무런 예외가 발생하지 않는지 확인
- assertThrows(Class, excutable) : 특정한 예외가 발생하는지 확인

- assertLinesMatch(list, list) : 두 개의 문자열 목록이 같은지 확인(문자열만 가능함)

