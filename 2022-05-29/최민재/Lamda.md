## 람다에 대해서 🧐
람다는 코딩을 조금을 해보아도 쉽게 접할 수 있습니다. 
그러면 대부분의 글은 전부 람다를 아래와 같이 설명합니다.
> **람다는 익명 함수(anonymous function)이다.**

이 말은 이름이 없는 함수라는 뜻입니다.
수학적으로 접근하여 한번 위의 말을 이해해 봅시다.

> $f(x) = x \times 2$

위의 함수를 한번 정리해 볼겠습니다.
일단 $x$값을 받아서 그 값에 2를 곱해주는 역할을 합니다.
그리고 **이름은 f가 되었죠!**

그런데 뭐 솔직히
$g(x), k(x)$
뭐 이름이어도 딱히 상관은 없습니다.
그 말은 **현재 함수의 이름이 딱히 중요하지 않다는 것이죠!**

그렇다면 **'이름이 없이 함수를 어떻게 표현할 것인가?'**
그런 의문이 듭니다.
그에 대한 답은 정말 간단합니다.

> $\lambda x.x \times 2$


뭐 간단하게 해석하자면
> $\lambda x$ -> $x$를 받아
$x \times 2$ 를 하는 함수

위와 같이 정말 정말 정말 간단하게 람다 대수에 대해서 한번 살펴보았습니다.
따라서 람다는 수학에서 사용하는 함수를 더욱 단순화하여 표현하는 것이라고 할 수 있습니다.

### 익명함수 🥸
익명함수의 특징에 대해서 알아봅시다.
**익명함수는 말 그대로 이름이 없는 함수라는 뜻입니다.**

그리고 이런 익명함수는 **일급 객체(First Class Object)** 라는 특징을 가지고 있죠!

**일급 객체란?**
일급 객체를 인터넷에 검색하면 다를 아래의 말을 합니다.
> 아래의 3개의 조건이 충족된다면 일급객체라고 볼 수 있습니다.
**1. 변수에 할당 할 수 있어야 합니다.
2. 객체의 인자로 넘길 수 있어야 합니다.
3. 객체의 리턴값으로 리턴 할 수 있어야 합니다.**


람다 함수는 이런 특징을 가진 다는 것인데
아래의 코드 부분에서 살펴봅시다.

## 람다 사용하기 with Java ☕️
이제 람다를 한번 사용해 보겠습니다.
저는 자바와 코틀린을 열심히 공부하기 때문에 Java를 사용해 정리해 보겠습니다.

JDK1.8부터 람다식(lambda expression)이 등장하였습니다.
**덕분에 자바는 객체지향언어이면서 함수형 언어가 되었죠!**

그러면 이제 람다식을 작성하는 방법을 알아보겠습니다.

원래 함수를 작성할 때는?
```java
반환타입 메서드이름(매개변수) {
	~~~
}
```

이렇게 작성합니다.

하지만 람다식을 쓴다면** 반환타입과 메서드이름을 적어주지 않아도 됩니다!**
```java
(매개변수) -> {
	~~~
}
```
이제 예시를 하나 보자면
```java
int add(int a, int b) {
	return a + b;
}

(int a, int b) -> a + b
```
위와 같이 식이 하나만 있다면 괄호를 생략해도 됩니다.
괄호가 생략되었다면 문장의 끝에 ';'을 붙이면 안되니 주의해야 합니다!

다른 예시를 봅시다!
```java
(num) -> num * num	// 매개변수 타입 생략
num -> num * num	// 괄호() 생략
(int num) -> { return num * num; }	// 괄호() 생략 불가능

() -> System.out.println("Hello")	// 매개변수가 없는 경우
() -> { System.out.println("Hello"); }
```
람다식에 **선언된 매개변수의 타입은 추론 가능한 경우 생략**할 수 있습니다.
람다식에 반환타입이 없는데 그 이유도 마찬가지로 항상 추론이 가능하기 때문입니다.

그리고 **매개변수가 하나만 있을 경우 괄호()를 생략**할 수 있습니다.
하지만 매개변수의 타입이 명시되어 있을 경우 괄호()를 생략할 수 없습니다.

**매개변수가 없는 경우 빈 괄호()로 적어주시면 됩니다.**

## 함수형 인터페이스 🔥
함수형 인터페이스란 **추상 메서드 단 하나만 있는 인터페이스입니다.**
Java8 부터는 인터페이스 내에 Default 메서드 혹은 Static 메서드는 여러개 포함해도 상관이 없습니다.
간단히 말하자면 추상 메서드 단 하나만 있으면 됩니다!

그리고 `@FunctionalInterface`를 사용하는데 
이 어노테이션이 붙은 인터페이스가 함수형 인터페이스 조건에 맞는지 검사해줍니다.
사실 `@FunctionalInterface` 없어도 오류는 나지 않지만 유지보수를 생각하면 붙이는 것이 맞습니다.
```java
@FunctionalInterface
public interface Functional {
    // 추상 메서드
    int add(int a, int b);
    
    static void print() {
        System.out.println("print");
    }
    
    default void minus() {
        System.out.println("-");
    }
}
```
> 추상 메서드 하나만 있으면 함수형 인터페이스가 성립됩니다.
그리고 static 메서드와 default 메서드는 있어도 상관이 없습니다.

그렇다면 이 인터페이스를 사용해보죠!
```java
public static void main(String[] args) {
    Functional test = new Functional() {
        @Override
        public int add(int a, int b) {
            return a + b;
        }
    };
    test.add(3, 2);
}
```

이렇게 객체를 생성하며 함수를 구현하죠!
그런데 람다식
```java
(int a, int b) -> a + b
```
와 메서드 선언부가 일치합니다.
아래와 같이 대체할 수 있죠!
```java
Functional test = (a, b) -> a + b;	// 타입은 추론 가능하니 생략
test.add(3, 5);
```
이렇게 대체가 가능한 이유는
> **`Functional`의 add()와 람다식의 매개변수의 타입과 개수 그리고 반환값이 일치하기 때문입니다!**

그래서 정리하자면
람다식을 다루기 위한 인터페이스를 '함수형 인터페이스(functional interface)'라고 부르기로 했습니다.

잠깐 예시로
안드로이드에서 클릭 이벤트를 감지하는 onClickListener를 봅시다.
```java
tvDate.setOnClickListener(new View.OnClickListener() {
    @Override
    public void onClick(View view) {
        Log.d("ClickEvent", "onClick: click");
    }
});
```

TextView를 클릭했을때 로그를 찍어주는 코드입니다!
`View`의 `OnClickListener`를 `new`를 통해서 생성합니다.
그러면 `OnClickListener` 안의 `onClick` 함수를 구현하죠.
실제로 `View` 안을 보면 ![](https://velog.velcdn.com/images/snack655/post/001806d0-1fb0-4e93-b787-dc95b442566f/image.png)

이렇게 추상 메서드를 하나 가진 함수형 인터페이스가 있습니다.

그렇다면 이제 람다를 사용하여 조금 더 가볍게 나타내보죠.
```java
tvDate.setOnClickListener(view ->
        Log.d("ClickEvent", "onClick: click")
);
```
정말 간편하고 보기 좋습니다!

그렇다면 아래와 같이 사용해도 괜찮을 것입니다.
```java
@FunctionalInterface
public interface Adder {
    void add(int a, int b);
}
````

함수형 인터페이스 `Adder`가 있습니다.
```java
void calc(Adder adder) {
    adder.add(3, 4);
}
```
그리고 매개변수의 타입이 함수형 인터페이스인 함수가 있죠.
이 함수는 `Adder`에 정의한 함수를 사용합니다.

그러면 이 함수는 이렇게 사용 가능합니다.
```java
Adder adder = (a, b) -> a + b;
calc(adder);
```
혹은 바로 **람다식을 매개변수로 지정하는 것도 가능**합니다!
```java
calc(
	(a, b) ->  a + b
);
```
이렇게 람다식을 잘 활용하면 코드를 훨씬 더 간결하게 짤 수 있습니다.


## 메서드 참조 👊
지금까지 정리한 람다가 정말 간단했는데 
더욱 간결하게 표현할 수 있는 방법이 있습니다.

> **람다식이 하나의 메서드만 호출**하는 경우
**'메서드 참조(method reference)'**라는 방법으로
람다식을 더욱 간결하게 표현할 수 있습니다.

그리고 '참조'라는 말의 의미로 알 수 있듯이
이미 존재하는 이름을 가진 메서드를 람다로써 사용할 수 있도록 참조하는 역할입니다.

위의 그 코드를 예를 들자면
```java
Adder adder = (a, b) -> Integer.sum(a, b)
```
위의 예제는 두 개의 값을 받아서 값을 합하는 연산을 수행하는
`Integer` 클래스의 클래스 메서드인 `sum()` 메서드를 호출하는 람다 표현식입니다.

위의 식에서는 간단히 두 개의 값을 받아서 `sum()`에 넘겨주는 역할만 하니
간단하게 메서드 참조를 사용하여 표현할 수 있습니다.
```java
Adder adder = Integer::sum;	 // 메서드 참조
```
일단 괄호()는 쓰지 않습니다.
이렇게 생략이 많이 되었는데 컴파일러는 어떻게 타입을 알 수 있을까요?
**바로 sum() 메서드의 선언부를 통해서 알 수 있다.**

> **이렇게 불필요한 매개변수를 제거하고 `::` 기호를 사용하여 표현할 수 있다.**

메서드 참조에는 2가지가 있습니다.
> 클래스::메소드	// 정적(static) 메소드 참조
참조변수::메소드	// 인스턴스 메소드 참조

위에서 `클래스::메소드`를 알아보았으니
이제 `참조변수::메서드`를 알아봅시다!
```java
class Calculator {
    public int add(int a, int b) {
        return a + b;
    }
}
```
위의 코드에서 보이듯이 `add()` 메서드가 들어있는 클래스가 있습니다.
```java
Adder adder = calculator::add;
System.out.println(adder.add(1, 2));

Adder adder2 = (a, b) -> calculator.add(a, b);
System.out.println(adder2.add(3, 4));
```

> **위와 같이 특정 인스턴스의 메서드를 참조할 때에도
참조 변수의 이름을 통해 메서드 참조를 사용할 수 있습니다.**

### 생성자 참조 🤕
메서드 참조 방식으로 생성자도 참조할 수 있습니다.

예제를 간단하게 하나 봅시다.
```java
class NameTag {
    String name;

    public NameTag(String name) {
        this.name = name;
    }
}
```
`NameTag` 클래스는 생성자를 가지고 있습니다.
```java
Function<String, NameTag> f1 = (String name) -> new NameTag(name);
NameTag nameTag1 = f1.apply("myName");
System.out.println(nameTag1.name);
```
단순히 람다식 형태로 생성자를 호출했습니다.
그렇다면 메서드 참조 방식으로 나타내어 보겠습니다.
```java
Function<String, NameTag> f2 = NameTag::new;
NameTag nameTag2 = f2.apply("yourName");
System.out.println(nameTag2.name);
```
**위와 같이 `NameTag::new`로 간단하게 나타낼 수 있습니다!**
하지만 생성자가 없다면 오류가 발생합니다.
