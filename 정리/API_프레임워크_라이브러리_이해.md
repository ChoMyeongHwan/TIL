# API, 프레임워크, 라이브러리
**모두 소프트웨어 개발에서 사용되는 용어다.**

## API(Application Programming Interface)
- 두 개 이상의 소프트웨어 컴포넌트 사이에서 상호 작용할 수 있도록 정의된 인터페이스
- 일반적으로 함수, 프로토콜 또는 클래스로 구성됨
- 다른 소프트웨어 개발자들이 이를 사용하여 특정 서비스 또는 기능을 사용할 수 있음

## 라이브러리(Library)
- 단순 활용가능한 도구들의 집합
- 즉, 개발자가 만든 클래스에서 호출하여 사용, 클래스들의 나열로 필요한 클래스를 불러서 사용하는 방식을 취함

## 프레임워크(Framework)
- 프레임워크는 뼈대나 기반구조를 뜻하고, 제어의 역전 개념이 적용된 대표적인 기술
- 소프트웨어에서의 프레임워크는 '소프트웨어의 특정 문제를 해결하기 위해서 상호 협력하는 클래스와 인터페이스의 집합' 이라 할 수 있으며, 완성된 어플리케이션이 아닌 프로그래머가 완성시키는 작업을 해야함
- 일련의 규칙과 구조를 정의하고, 개발자가 애플리케이션을 작성할 때 이러한 규칙과 구조를 따르도록 함
- 객체 지향 개발을 하게 되면서 `통합성`, `일관성`의 부족이 발생되는 문제를 해결할 방법중 하나다.

### 프레임워크의 특징
- 특정 개념들의 추상화를 제공하는 여러 클래스나 컴포넌트로 구성
- 추상적인 개념들이 문제를 해결하기 위해 같이 작업하는 방법을 정의
- 컴포넌트들은 재사용이 가능함
- 높은 수준에서 패턴들을 조작화 할 수 있음

## 프레임워크와 라이브러리의 차이점
**제어 흐름에 대한 주도성이 누구에게/어디에 있는가**<br/>
**Flow(흐름)을/를 누가 쥐고 있느냐?**
```
라이브러리를 사용하는 애플리케이션 코드는 애플리케이션 흐름을 직접 제어합니다.  

단지 동작하는 중에 필요한 기능이 있을 때 능동적으로 라이브러리를 사용할 뿐입니다. 

반면에 프레임워크는 거꾸로 애플리케이션 코드가 프레임워크에 의해 사용되는 것입니다. 

보통 프레임워크 위에 개발한 클래스를 등록해두고, 프레임워크가 흐름을 주도하는 중에 개발자가 만든 애플리케이션 코드를 사용하도록 만드는 방식입니다.

프레임워크에는 분명한 제어의 역전 개념이 적용되어 있어야 합니다.

애플리케이션 코드는 프레임워크가 짜놓은 틀에서 수동적으로 동작해야 합니다.

```

[[참고 1] API-vs-라이브러리-풀리지-않는-미스터리에-관하여](https://velog.io/@bcl0206/API-vs-%EB%9D%BC%EC%9D%B4%EB%B8%8C%EB%9F%AC%EB%A6%AC-%ED%92%80%EB%A6%AC%EC%A7%80-%EC%95%8A%EB%8A%94-%EB%AF%B8%EC%8A%A4%ED%84%B0%EB%A6%AC%EC%97%90-%EA%B4%80%ED%95%98%EC%97%AC/)<br />
[[참고 2] 프레임워크와 라이브러리의 차이점](https://webclub.tistory.com/458)