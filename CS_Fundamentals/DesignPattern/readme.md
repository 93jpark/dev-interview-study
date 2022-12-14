# Gof 디자인 패턴

개발을 구조적으로 우아하게 설계하고 노력하다 보니 반복되는 패턴들이 발견됐는데 그걸 **디자인 패턴** 이라고 한다.

### 목적

SW 재사용성, 호환성, 유지 보수성을 보장한다.

### 특징

디자인 패턴은 아이디어임. 항상 프로젝트에 적용해야 하는 것은 아니지만 추후 사용시 발생하는 **문제 해결을 예방하기 위해 패턴을 만들어 둔 것.**

### 디자인 패턴 종류

**1. 생성 패턴 (5개) : 객체를 어떻게 생성할 것인가?**

- 싱글톤
- 팩토리 메소드
- 추상 팩토리
- 빌더
- 프로토 타입

> 예) DBConnection을 관리하는 Instance를 하나만 만들 수 있도록 제한하여, 불필요한 연결을 막음.

**2. 구조 패턴 (7개) : 생성된 객체들을 어떻게 조합/합성할 것인가? (객체간의 관계를 조직)**

- 어댑터
- 브릿지
- 컴포짓
- 데코레이터
- 퍼사드
- 플라이웨이트
- 프록시

> 예) 2개의 인터페이스가 서로 호환이 되지 않을 때, 둘을 연결해주기 위해서 새로운 클래스를 만들어서 연결시킬 수 있도록 함.

**3. 행동 패턴 (11개) : 객체들이 어떻게 상호작용/책임을 가져가는가? (객체의 행위를 조직, 관리, 연합)**

- 책임 연쇄
- 커맨드
- 인터프리터
- 이터레이터
- 메멘토
- 옵저버
- 상태
- 전략
- 템플릿 메소드
- 비지터

> 예) 하위 클래스에서 구현해야 하는 함수 및 알고리즘들을 미리 선언하여, 상속시 이를 필수로 구현하도록 함.

---

## 어댑터 패턴

클래스를 바로 사용할 수 없는 경우(다른 곳에서 개발을 하거나, 수정할 수 없을 때) 중간에서 변환 역할을 해주는 클래스가 필요한데 그걸 **어댑터 패턴** 이라고 한다.

### 특징

1. 호환되지 않은 인터페이스를 사용하는 클라이언트 그대로 활용 가능
2. 향후 인터페이스가 바뀌더라도, 변경 내역은 어댑터에 캡슐화 되므로 클라이언트 바뀔 필요없다.

> 아이폰의 이어폰을 비유하면 가장 흔한 이어폰 잭을 아이폰에 사용하려면,
> 잭 자체가 맞지 않는다.
> 따라서 우리는 어댑터를 따로 구매해서 연결해야 이런 이어폰들을 사용할 수 있다

이처럼 **어댑터는 필요로 하는 인터페이스로 바꿔주는 역할을 한다.**

### 클래스가 기존 시스템에 맞지 않는다면?

기존 시스템을 수정할 것이 아니라, 어댑터를 활용해 유연하게 해결한다.

> **오리와 칠면조 인터페이스 생성**
> 만약 오리 객체가 부족해서 칠면조 객체를 대신 사용해야 한다면?
> 두 객체는 인터페이스가 다르므로, 바로 칠면조 객체를 사용하는 것은 불가능하다.
> 따라서 칠면조 어댑터를 생성해서 활용해야 한다.

---

# 생성 패턴

_인스턴스를 만드는 절차_ 를 **추상화**하는 패턴이다. **시스템으로부터** 객체의 생성/합성 방법을 **분리**해내기 위함.

## 싱글턴 패턴

**오직 한 개의 인스턴스**만을 갖도록 하며, 이에 대한 전역적인 접근을 하용한다.

일반적으로 특정 클래스의 **인스턴스가 반드시 하나**여야 하나 여러 곳에서 사용하는 경우 **싱글턴 패턴**을 사용한다. (가장 유명한 생성 패턴)

또한 생성된 인스턴스를 여러 곳에서 **공유**하여 사용해도 무리가 없다면 **메모리 낭비를 방지**하기 위해 **싱글턴 패턴을** 적용하기도 한다.

### 예제

> 카페의 와이파이를 이용하여 네트워크에 연결하는 경우
> 카페에서는 와이파이가 필요한 사용자마다 와이파이를 새로 만들지 않는다.
> 기존에 있던 네트워크를 **공유해서 사용하도록 한다**

이처럼 *싱글턴 패턴*을 사용하면 단 하나의 **인스턴스**(일반적으로 실행 중인 임의의 프로세스, 클래스의 현재 생성된 오브젝트를 가리킴)만 생성된다.

*싱글턴 패턴*을 사용하면 고정된 메모리 영역을 받기 때문에 단 하나의 객체만 생성되어 메모리가 낭비를 방지할 수 있다.

### 문제점

1. **상속**할 수 없다.

- 원하는 대로 생성되는걸 방지하기 위해 생성자를 private으로 선언한다.
  => 객체지향 프로그램의 핵심인 **상속**과 **다형성**을 해치는 개념.

2. 강제로 **전역 상태**

- **공유 목적**으로 생성된 클래스이기에 객체를 요청하는 메소드를 public으로 강제할 수 밖에 없다.
  => 객체지향 프로그램의 또 다른 핵심인 **'정보 은닉'** 을 해친다.

3. **객체가 하나인 것**을 보장할 수 없다.

- 인스턴스는 공유돼서 사용도기 때문에 여러개의 쓰레드가 동시에 접근하여 메소드를 호출 할 수 있다.
  => 문제는 2개 이상의 쓰레드가 동시에 객체 생성을 하게 된다면 2개 이상의 객체가 생성되는것.
  => 즉, 싱글턴 패턴을 적용해씅나, **싱글턴이 아닌 게 되는것이다.**

### 결론

_싱글턴 패턴_ 은 많이 활용되는 패턴이지만, **객체지향 프로그래밍**의 기본 사상들을 많이 침해하기 때문에 굉장히 비판을 많이 받는 디자인 패턴이다.

따라서 사용 시 매우 조심해서 사용해야 하며, 그것이 아니라면 개선된 방식으로 객체의 싱글턴 방식을 구현하여 사용해야 한다.

---

## 프로토타입 패턴

인스턴스들이 서로 다른 상태 값 또는 서로 다른 조합으로 지속적/주기적으로 필요할 때, 나중에 인스턴스 생성을 위해 **복제의** 견본이 되어줄 **원형 인스턴스**를 준비해둔다.

그 후, 새로운 인스턴스 생성 요청이 오거나 필요할 때 미리 만둘어둔 견본을 **복제하여 사용한다.** _(비용이 큰 경우 주로 사용되는 패턴이다.)_

---

## 팩토리 메소드 패턴

객체 생성을 서브 클래스에서 처리하도록 분리하여 캡슐화한 패턴이다. 객체를 생성하기 위해 인터페이스를 정의하지만 어떤 클래스의 인스턴스를 생성할지는 **서브 클래스가 결정**한다.

---

## 추상 팩토리

구체적인 클래스에 의존하지 않고, 인터페이스를 통해 서로 연관/의존하는 객체들의 그룹으로 생성하여 추상적으로 표현한다.
연관된 서브 클래스를 묶어 한 번에 교체하는 것이 가능하다.

---

## 빌더

생성하려는 객체가 매우 복잡할 때 유용하다. 복잡한 객체를 생성하는 방법과 표현하는 방법을 정의하는 클래스를 별도로 분리하여, 서로 다른 표현이라도 이를 생성할 수 있는 동일한 절차를 제공할 수 있다.
