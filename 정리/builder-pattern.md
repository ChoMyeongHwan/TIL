## Builder Pattern

### 빌더 패턴이란?

- 복잡한 객체의 생성 과정과 표현 방법을 분리하여 다양한 구성의 인스턴스를 만드는 생성 패턴
- 생성자에 들어갈 매개변수를 메서드로 하나하나 받아들이고 마지막에 통합 빌드해서 객체를 생성하는 방식

### 빌더 패턴 탄생 배경

**점층적 생성자 패턴**
- 필수 매개변수와 함께 선택 매개변수를 0개, 1개, 2개 ... 받는 형태로, 우리가 다양한 매개변수를 입력받아 인스턴스를 생성하고 싶을때 사용하던 **생성자를 오버로딩** 하는 방식
- 클래스 인스턴스 필드들이 많으면 많을 수록 생성자에 들어갈 인자의 수가 늘어나 몇번째 인자가 어떤 필드였는지 햇갈릴 경우가 생김
- 생성자로만으로는 필드를 선택적으로 생략할 수 있는 방법이 없음
- 타입이 다양할 수록 생성자 메서드 수가 기하급수적으로 늘어나 가독성이나 유지보수 측면에서 좋지 않음
<br/>

**자바 빈(Java Beans) 패턴**
- 매개변수가 없는 생성자로 객체 생성 후 Setter 메소드를 이용해 클래스 필드의 초깃값을 설정하는 방식
- 점층적 생성자 패턴의 단점을 보완
- 가독성 문제점이 사라지고 선택적인 파라미터에 대해 해당되는 Setter 메서드를 호출함으로써 유연적으로 객체 생성이 가능해짐
- 하지만 객체 생성 시점에 모든 값들을 주입 하지 않아 `일관성(consistency)` 문제와 `불변성(immutable)` 문제가 발생

```
1. 일관성 문제
 - 필수 매개변수란 객체가 초기화될때 반드시 설정되어야 하는 값
 - 일관성이 무너지면 객체가 유효하지 않은 상태
 - 해당 인스턴스를 사용 시 런타임 예외가 발생 할 수 있음

2. 불변성 문제
 - 자바 빈즈 패턴의 Setter 메서드는 객체를 처음 생성할때 필드값을 설정하기 위해 존재하는 메서드
 - 객체 생성 후에도 외부적으로 Setter 메소드를 노출하고 있음
 - 협업 과정에서 언제 어디서 누군가 Setter 메서드를 호출해 함부로 객체를 조작할 수 있음
 - 불변함을 보장할 수 없음
```

**빌더(Builder) 패턴**
- **별도의 Builder 클래스**를 만들어 메소드를 통해 **step-by-step** 으로 값을 입력받은 후에 최종적으로 build() 메소드로 하나의 인스턴스를 생성하여 리턴하는 패턴
- 빌더 클래스의 **메서드를 체이닝(Chaining) 형태로 호출**함으로써 자연스럽게 인스턴스를 구성하고 마지막에 build() 메서드를 통해 최종적으로 객체를 생성
- 일관성 및 불변성 문제 해결을 위해 탄생
```java
public static void main(String[] args) {

    // 생성자 방식
    Hamburger hamburger = new Hamburger(2, 3, 0, 3, 0, 0);

    // 빌더 방식
    Hamburger hamburger = new Hamburger.Builder(10)
        .bun(2)
        .patty(3)
        .lettuce(3)
        .build();
}
```
- 점층적 생성자 패턴과 자바빈즈 패턴 두 가지의 장점만을 채택함

### 빌더 패턴 구조

**빌더 클래스 구현**
```java
class StudentBuilder {
    private int id;
    private String name;
    private String grade;
    private String phoneNumber;

    public StudentBuilder id(int id) { ... }

    public StudentBuilder name(String name) { ... }

    public StudentBuilder grade(String grade) { ... }

    public StudentBuilder phoneNumber(String phoneNumber) { ... }

    public Student build() {
        // Student 생성자 호출
        return new Student(id, name, grade, phoneNumber);
    }
}
```
**빌더 클래스 실행**
```java
public static void main(String[] args) {

    Student student = new StudentBuilder()
                .id(111)
                .name("홍길동")
                .grade("Senior")
                .phoneNumber("010-1234-5678")
                .build();

    System.out.println(student);
}
```
### 빌더 패턴 네이밍 형식
 
 1. **멤버이름()** : 추천되는 형식
 2. set멤버이름() : 일반 Setter 메소드와 헷갈릴 소지가 있음
 3. with멤버이름() : 빌더 지연 생성 방식에서 미리 빌더를 설정할 때 쓰이기도 함

### 빌더 패턴 장단점
 
**장점**
 1. 객체 생성 과정을 일관된 프로세스로 표현
 2. 디폴트 매개변수 생략을 간접적으로 지원
 3. 필수 멤버와 선택적 멤버를 분리 가능
 4. 객체 생성 단계를 지연할 수 있음
 ```java
 // 1. 빌더 클래스 전용 리스트 생성
List<StudentBuilder> builders = new ArrayList<>();

// 2. 객체를 최종 생성 하지말고 초깃값만 세팅한 빌더만 생성
builders.add(
    new StudentBuilder(2016120091)
    .name("홍길동")
);

builders.add(
    new StudentBuilder(2016120092)
    .name("임꺽정")
    .grade("senior")
);

builders.add(
    new StudentBuilder(2016120093)
    .name("박혁거세")
    .grade("sophomore")
    .phoneNumber("010-5555-5555")
);

// 3. 나중에 빌더 리스트를 순회하여 최종 객체 생성을 주도
for(StudentBuilder b : builders) {
    Student student = b.build();
    System.out.println(student);
}
 ```
 5. 초기화 검증을 멤버별로 분리
 6. 멤버에 대한 변경 가능성 최소화를 추구

 > 빌더 패턴은 생성자 없이 어느 객체에 대해 '변경 가능성을 최소화' 를 추구하여 불변성을 갖게 해주게 되는 것
 
**단점**
 1. 코드 복잡성 증가
 2. 생성자 보다는 성능은 떨어짐
 3. 지나친 빌더 남용은 금지 : 클래스의 필드 갯수가 4개보다 적고, 필드의 변경 가능성이 없는 경우라면 생성자나 정적 팩토리 메소드를 이용하는 것이 더 좋을 수 있음

 [[참고] 빌더(Builder) 패턴 - 완벽 마스터하기](https://inpa.tistory.com/entry/GOF-%F0%9F%92%A0-%EB%B9%8C%EB%8D%94Builder-%ED%8C%A8%ED%84%B4-%EB%81%9D%ED%8C%90%EC%99%95-%EC%A0%95%EB%A6%AC)

