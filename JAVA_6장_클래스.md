# 6장 클래스 186-276p

## 1. 객체지향 프로그래밍

- 부품 객체를 먼저 만들고 이것들을 하나씩 조립해서 완성된 프로그램을 만드는 기법 **(OOP: Object Oriented Programming)**

- **객체**: 물리적으로 존재하거나(자동차, 책, 사람), 추상적인 것(회사, 날짜) 중에서 자신의 속성과 동작을 가지는 모든 것

### 1.1 객체 간의 관계

![객체 간의 관계](https://postfiles.pstatic.net/MjAyMTA5MjVfMzQg/MDAxNjMyNTY5Mjk2ODc3.pX6tdXYhQhqNjFHrQ2VE4fTAQiGQXlyUk2sfKObnMgIg.4uPIcKeOQYPd5ZqN8njRPeWAgMJcx7AvGDRLOTX-6zsg.JPEG.chex417/%EA%B0%9D%EC%B2%B4%EA%B0%84%EC%9D%98%EA%B4%80%EA%B3%84.jpg?type=w773)

    - 집합관계: 완성품과 부품의 관계
       ex. 자동차 - 엔진, 타이어, 핸들

    - 사용관계: 객체가 다른 객체를 사용하는 관계(객체 간 상호작용)
       ex. 사람 - 자동차, 사람은 자동차를 사용할 때 메소드 호출(달린다, 멈춘다)

    - 상속관계: 종류 객체와 구체적인 사물 객체 관계
       ex. 기계(종류) - 자동차(구체적인 사물)

### 1.2 객체 지향 프로그래밍의 특징

    - 캡슐화(Encapsulation): 객체의 필드, 메소드를 하나로 묶고 실제 구현 내용을 감추는 것 -> 접근제한자를 사용
    - 상속(Inheritance): 상위 객체가 자신의 필드와 메소드를 하위 객체에게 물려주는 것 -> 코드중복과 유지보수 시간을 줄여줌
    - 다형성(Polymorphism): 같은 타입이지만 실행 결과가 다양한 객체를 이용할 수 있는 성질을 말함. 부모 타입에는 모든 자식 객체가 대입될 수 있고, 인터페이스 타입에는 모든 구현 객체가 대입될 수 있다. -> 객체의 부품화
                            ex. 자동차를 설계할 때 타이어 인터페이스 타입을 적용했다면 이 인터페이스를 구현한 실제 타이어들은 어떤 것이든 상관없이 장착(대입) 가능

---

## 2. 객체와 클래스

- **클래스(class)**: 설계도
- **인스턴스(instance)**: 클래스로부터 만들어진 객체
- **객체 생성**: **new**연산자는 **힙** 영역에 객체를 생성시킨 후 객체의 주소를 리턴한다.

```
public class StudentExample {
    public static void main(String[] args){
        Student s1 = new Student(); // 객체 생성 후 객체의 주소를 리턴
        System.out.println("s1 변수가 Student 객체를 참조합니다.");

        Student s2 = new Student();
        System.out.println("s2 변수가 또 다른 Student 객체를 참조합니다.");
    }
}
```

- 클래스의 용도: 라이브러리용, 실행용(main메소드 제공)

---

## 3. 클래스의 구성 멤버

- **필드**: 객체의 데이터가 저장되는 곳
- **생성자**: 객체 생성 시 초기화 역할 담당
- **메소드**: 객체의 동작에 해당하는 실행 블록

### 3.1 필드

    선언 형태는 변수(variable)과 비슷하지만, 필드를 변수라고 부르지 않는다.
    변수는 생성자와 메소드 내에서만 사용되고 생성자와 메소드가 실행 종료되면 자동 소멸된다.
    하지만 **필드**는 생성자와 메소드 전체에서 사용되며 객체가 소멸되지 않는 한 객체와 함께 존재한다.

### 3.2 생성자

- 모든 클래스는 생성자가 반드시 존재하며 하나 이상 가짐

![생성자](https://postfiles.pstatic.net/MjAyMTA5MjVfMjg3/MDAxNjMyNTcxNDgxMDQ2.7ytAFDLCAqR-NYMArxoO4bZhDNJHA5OVkXVPTTyDV0Yg.G78ixdiR449I1JXli6AOqt3lSfDDYFCyxP8sB6_7OMMg.JPEG.chex417/%EC%83%9D%EC%84%B1%EC%9E%90.jpg?type=w773)

- 생성자 선언 생략 시 기본 생성자를 바이트 코드에 자동 추가시킴
- 클래스가 public으로 선언되면 기본 생성자도 public
- 클래스가 public없이 선언되면 기본 생성자도 public이 붙지 않는다.
- 클래스에 명시적으로 선언한 생성자가 1개라도 있으면 컴파일러는 기본 생성자를 추가하지 않는다.
  ```
  Car myCar = new Car("검정, 3000); // 명시적으로 선언한 생성자
  // Car myCar = new Car(); (X) // 기본 생성자 호출 불가
  ```

---

## 4. 생성자 오버로딩(Overloading)

    자바는 다양한 방법으로 객체를 생성하기 위한 생성자 오버로딩을 제공한다.
    생성자오버로딩: 매개 변수를 달리하는 생성자를 여러 개 선언하는 것

![생성자 오버로딩](https://postfiles.pstatic.net/MjAyMTA5MjVfMTkx/MDAxNjMyNTcyMTQ2MDA5.RDnEFC3SlReDXT3WVwdLc3mHtg6d-JAG36-pf9uxzlcg.K2Esl343adL-2khA3N6471quxw9EmDe8CxSP6cSaiYsg.PNG.chex417/%EC%83%9D%EC%84%B1%EC%9E%90%EC%98%A4%EB%B2%84%EB%A1%9C%EB%94%A9.PNG?type=w773)

- 생성자의 오버로딩: 매개변수의 타입, 개수, 순서를 다르게 선언
- 생성자에서 다른 생성자를 호출할 때에는 `this()`코드를 사용한다. -> 중복 코드 방지

```
Car(String model, String color){...}
Car(String color, String model){...} // 오버로딩이 아님
```

- 매개변수 타입, 개수, 그리고 선언된 순서가 같을 경우 변수 이름만 바꾸는 것은 오버로딩이 아니다.

---

## 5. 메소드

### 5.1 매개변수의 수를 모를 경우

```
public class Computer {
    int sum1(int[] values){
        int sum = 0;
        for(int i = 0; i < values.length; i++){
            sum += values[i];
        }
        return sum;
    }

    int sum2(int ... values){ // 자동으로 배열 생성해줌
        int sum = 0;
        for(int i = 0; i < values.length; i++){
            sum += values[i];
        }
        return sum;
    }
}
```

    매개 변수의 수를 모를 경우 매개 변수를 배열 타입으로 선언하거나
    "..."를 사용해서 선언하게 되면 메소드 호출 시 넘겨준 값의 수에 따라 자동으로 배열이 생성되고 매개값으로 사용된다.

```
public class ComputerExample {
    public static void main(String[] args){
        Computer myCom = new Computer();

        int[] values1 = {1, 2, 3};
        int result1 = myCom.sum1(values1);
        System.out.println("result1: "+result1);

        int result2 = myCom.sum2(1, 2, 3);
        System.out.println("result2: "+result2);
    }
}
```

### 5.2 메소드 오버로딩

    메소드 오버로딩의 조건은 매개변수의 타입, 개수, 순서 중 하나가 달라야 한다.

```
    public class Calculator {

        // 정사각형의 넓이
        double areaRectangle(double width){
            return width * width;
        }

        // 직사각형의 넓이
        double areaRectangle(double width, double height){
            return width * height;
        }
    }

```

```
    public class CalculatorExample { // 메소드 오버로딩
        public static void main(String[] args){
            Calculator myCalcu = new Calculator();

            // 정사각형의 넓이 구하기
            double result1 = myCalcu.areaRectangle(10);

            // 직사각형의 넓이 구하기
            double result2 = myCalcu.areaRectangle(10, 20);

            // 결과 출력
            System.out.println("정사각형 넓이 = "+result1);
            System.out.println("직사각형 넓이 = "+result2);

        }
    }
```

- **주의**

  - 매개변수의 타입, 개수, 순서가 같을 경우 변수 이름만 바꾸는 것은 메소드 오버로딩X
  - 리턴 타입만 다르고 매개변수가 동일한 경우도 메소드 오버로딩X
    -> 리턴 타입은 자바 가상머신이 메소드를 선택할 때 아무런 도움을 주지 못하기 때문이다.

---

## 6. 인스턴스 멤버

    인스턴스 멤버란 객체(인스턴스)를 생성한 후 사용할 수 있는 필드와 메소드를 말하는데, 이들을 각각 인스턴스 필드, 인스턴스 메소드라고 부른다.

- 인스턴스 멤버는 객체에 소속된 멤버이기 때문에 객체 없이 사용불가

```
Car myCar = new Car();
myCar.gas = 10;
myCar.setSpeed(60);

Car yourCar = new Car();
yourCar.gas = 20;
yourCar.setSpeed(80);
```

![인스턴스멤버](https://postfiles.pstatic.net/MjAyMTA5MjVfOTgg/MDAxNjMyNTczMzcxMzEz.cGNP7Uf6qNjdycQQb_C1IxNwEHNcUSGWyhXimBGkbVkg.DperFq0ay1eAWFsqFxrsF56_oHlZMQbpFHMXp8nQPNEg.JPEG.chex417/%EC%9D%B8%EC%8A%A4%ED%84%B4%EC%8A%A4%EB%A9%A4%EB%B2%84.jpg?type=w773)

- 위 코드가 실행된 후 메모리 상태
- 인스턴스 필드 gas는 **객체마다** 따로 존재
- 인스턴스 메소드 setSpeed()는 객체마다 존재하지않고 **메소드 영역**에 저장되고 공유된다.

---

## 7. 정적 멤버와 static

- 정적멤버는 클래스에 고정된 멤버로서 **객체를 생성하지 않고** 사용할 수 있는 필드와 메소드를 말한다.

- 객체(인스턴스)에 소속된 멤버가 아니라 클래스에 소속된 멤버이기 때문에 **클래스 멤버**라고도 한다.

![정적멤버선언](https://postfiles.pstatic.net/MjAyMTA5MjVfMTk3/MDAxNjMyNTczNzMwMjE0.xck1QS16RC9DQDYiiERPTAJH3LLM1OEZ9H2wPk5LbWUg.7W2oXKBuueVD6Ng31ueibZetJ0ce_ZcC4EiYLHi4E4Eg.JPEG.chex417/%EC%A0%95%EC%A0%81%EB%A9%A4%EB%B2%84%EC%84%A0%EC%96%B8.jpg?type=w773)

- 정적 필드와 정적 메소드는 클래스에 고정된 멤버이므로 **클래스 로더**가 클래스(바이트 코드)를 로딩해서 **메소드** 메모리 영역에 적재할 때 **클래스 별**로 관리된다.

### 7.1 인스턴스 필드로 선언 vs 정적 필드로 선언

- 인스턴스 필드: 객체마다 갖고 있어야할 데이터
- 정적 필드: 객체마다 갖고 있을 필요성이 없는 공용적인 데이터

  ```
  public class Calculator {
  String color; // 계산기별로 색깔이 다를 수 있음 -> 인스턴스 필드(인스턴스 멤버)
  static double pi = 3.14159; // 계산기에서 사용하는 파이값은 동일 -> 정적 필드(클래스 멤버)
  }
  ```

### 7.2 인스턴스 메소드로 선언 vs 정적 메소드로 선언

- 인스턴스 메소드: 인스턴스 필드를 이용해서 실행해야 한다면
- 정적 메소드: 인스턴스 필드를 이용하지 않는다면

  ```
  public class Calculator {
  String color;                                     // 인스턴스 필드(인스턴스 멤버)
  void setColor(String color){ this.color = color;} // 인스턴스 메소드(인스턴스 멤버)
  static int plus(int x, int y){return x+y;}        // 정적 메소드(클래스 멤버)
  static int minus(int x, int y){return x-y;}       // 정적 메소드(클래스 멤버)
  }
  ```

### 7.3 정적 초기화 블록

    인스턴스 필드는 생성자에서 초기화하지만
    정적 필드는 객체 생성 없이도 사용해야 하므로 생성자에서 초기화 작업을 할 수 없다.

    그렇다면
    정적 필드를 위한 초기화 작업은 어디에서 할까?

    자바는 정적 필드의 복잡한 초기화 작업을 위해서 `정적 블록(static block)`을 제공한다.

- 정적블록은 클래스가 메모리로 로딩될 때 자동적으로 실행된다.

  ```
  public class Television {

    static String company = "Samsung";
    static String model = "LDC";
    static String info;

    static{ // 정적 초기화 블록
        info = company + "-" + model;
    }
  }
  ```

- 주의

        정적메소드와 정적 블록을 선언할 때 주의할 점은 객체가 없어도 실행된다는 특징 때문에,
        이들 내부에 인스턴스 필드나 인스턴스 메소드를 사용할 수 없다.

        정적 메소드와 정적 블록에서 인스턴스 멤버를 사용하고 싶다면
        다음과 같이 객체를 먼저 생성하고 참조변수로 접근해야 한다.

        static void Method1(){ // 정적 메소드
            ClassName obj = new ClassName(); //객체 생성
            obj.field = 10;
            obj.method2(); // 인스턴스 메소드
        }

---

## 8. 싱글톤(Singleton)

> 전체 프로그램에서 **단 하나의 객체만 만들도록 보장**해야 하는 경우가 있다.
> 단 하나만 생성된다고 해서 이 객체를 **싱글톤(Singleton)** 이라고 한다.

- **싱글톤을 만들려면**? 생성자 앞에 `private` 접근 제한자를 붙여 클래스 외부에서 new 연산자로 생성자를 호출할 수 없도록 막아야한다.

```
public class Singleton {
    //정적 필드
    private static Singleton singleton = new Singleton(); //자신의 타입인 정적 필드를 하나 선언하고, 자신의 객체를 생성해 초기화한다.

    //생성자
    private Singleton(){} // 생성자를 호출한 만큼 객체가 생성되므로 외부에서 호출할 수 없도록 생성자 앞에 private를 붙인다.

    //정적 메소드
    static Singleton getInstance(){ // 외부에서 호출할 수 있는 정적 메소드
        return singleton;
    }
}

```

```
public class SingletonExample { // 싱글톤 예제
    public static void main(String[] args){
        /*
        Singleton obj1 = new Singleton(); // 컴파일 에러
        Singleton obj2 = new Singleton(); // 컴파일 에러
        */

        Singleton obj1 = Singleton.getInstance();
        Singleton obj2 = Singleton.getInstance();

        if(obj1 == obj2){
            System.out.println("같은 Singleton 객체입니다.");
        } else{
            System.out.println("다른 Singleton 객체입니다.");
        }
    }
}
```

    getInstance()메소드는 단 하나의 객체만 리턴하기 때문에 obj1과 obj2는 동일한 객체를 참조한다.

---

## 9. final 필드와 상수

## 9.1 final 필드

> **final 필드**는 초기값이 저장되면 이것이 **최종적인 값**이 되어서 프로그램 실행 도중에 수정할 수 없다.

### 9.1.1 final 필드 선언과 초기화

```
    public class Person { // final 필드 선언과 초기화
        final String nation = "Korea";
        final String ssn;
        String name;

        public Person(String ssn, String name){
            this.ssn = ssn;
            this.name = name;
        }
    }
```

- `nation`은 항상 고정된 값을 갖기 때문에 **필드 선언 시** 초기값으로 "Korea"를 줌
- 주민등록번호(`ssn`)는 `Person` 객체가 생성될 때 부여되므로 `Person` 클래스 설계 시 초기값을 미리 줄 수 없음
- 따라서 **생성자** 매개값으로 주민등록번호(`ssn`)를 받아서 초기값으로 지정해줌
- **주의**: 만약 **초기화되지 않은** final 필드를 그대로 남겨두면 컴파일 에러가 발생한다.

## 9.2 상수(static final)

> 원주율 파이나 지구의 무게 및 둘레 등의 불변의 값을 상수라고 하는데 이러한 불변의 값을 저장하는 필드를 자바에서는 **상수(constant)** 라고 한다.

```
static final double PI = 3.14159;
```

- 상수는 `static`이면서 `final`이어야 한다.
- `static final`필드는 객체마다 저장되지 않고 **클래스에만** 포함된다.
- 한 번 초기값이 저장되면 변경할 수 없다.

```
public class Earth { // 상수 선언
    static final double EARTH_RADIUS = 6400;
    static final double EARTH_SURFACE_AREA;

    static{ // 상수는 정적블록에서도 초기화 가능
        EARTH_SURFACE_AREA = 4 * Math.PI * EARTH_RADIUS * EARTH_RADIUS;
    }
}
```

- 복잡한 초기화일 경우 **정적 블록**에서 초기화할 수 있다.

- 상수 이름은 **대문자**로 작성
- 혼합된 이름이라면 언더바(\_)로 연결

```
public class EarthExample {
    public static void main(String[] args){ // 상수 사용
        System.out.println("지구의 반지름: "+Earth.EARTH_RADIUS+" km");
        System.out.println("지구의 표면적: "+Earth.EARTH_SURFACE_AREA+" km^2");
    }
}
```

---

## 10. 패키지

> 프로젝트를 개발하다 보면 수 많은 클래스를 작성해야한다. 자바에서는 클래스를 **체계적으로 관리**하기 위해 **패키지(package)** 를 사용한다.

- 패키지는 클래스를 유일하게 만들어주는 **식별자**역할을 한다.
- 클래스 이름이 동일하더라도 패키지가 다르면 다른 클래스로 인식한다.
- 클래스의 전체 이름은 **"패키지명+클래스명"** 인데 패키지가 상 하위로 구분되어 있다면 도트(.)를 사용한다.

- 보통 회사들 간에 패키지가 서로 중복되지 않도록 회사의 도메인 이름으로 패키지를 만든다.
- 도메인은 등록 기관에서 유일한 이름이 되도록 검증되었기 때문
- 포괄적인 이름이 상위 패키지가 되도록 도메인 이름 **역순**으로 패키지 이름을 지어준다.

```
com.samsung.projectname
com.hyndai.projectname
com.lg.projectname
org.apache.projectname
```

---

## 11. 접근제한자

![접근제한자](https://postfiles.pstatic.net/MjAyMTA5MjZfNzIg/MDAxNjMyNTgyNjI0OTQ4.l7r4HymC4AGXc-EpODCuXeSiTwpbykmPKvt_vt2k4Msg.VSW8ue7djD58hIbiRnNxbQNZkf8foP0srOQ2wBp4xxsg.JPEG.chex417/%EC%A0%91%EA%B7%BC%EC%A0%9C%ED%95%9C%EC%9E%90.jpg?type=w773)

- `public` 외부 클래스가 자유롭게 사용할 수 있도록 공개 멤버를 만듦
- `protected` **같은 패키지** 또는 다른 패키지의 **자식클래스**에서 사용할 수 있는 멤버를 만듦
- `default` **같은 패키지**에 소속된 클래스에서만 사용할 수 있는 멤버를 만듦
- `private` 클래스 내부에서만 사용할 수 있는 멤버를 만듦

```
package com.ch6class.thisisjavastudy;

class A {} // default 접근 제한
```

```
package com.ch6class.thisisjavastudy;

public class B {
    A a; //(o) B 클래스는 A 클래스와 같은 패키지이므로 A 클래스에 접근 가능
}
```

```
package com.ch6class2.thisisjavastudy; // 패키지가 다름

import  com.ch6class.thisisjavastudy.*;

public class C {
    //A a; //(x) C 클래스는 A 클래스와 다른 패키지이므로 A 클래스 접근 불가
    B b; //(o) B 클래스는 접근제한자가 "public"이므로 접근 가능
}
```

### 11.1 생성자의 접근제한

```
ackage com.ch6class.thisisjavastudy;

public class One { // 생성자의 접근제한
    //필드
    One a1 = new One(true);    // (O)
    One a2 = new One(1);       // (O)
    One a3 = new One("문자열"); // (O)

    //생성자
    public One(boolean b){} // public 접근제한
    One(int b){}            // default 접근제한
    private One(String s){} // private 접근제한
}
```

```
package com.ch6class.thisisjavastudy; // One 클래스와 같은 패키지

public class Two {
    //필드
    One a1 = new One(true);   // (O) public 생성자 접근 가능
    One a2 = new One(1);      // (O) default 생성자 접근 가능
    //One a3 = new One("문자열"); // (X) private 생성자 접근 불가(컴파일에러)
```

```
package com.ch6class2.thisisjavastudy; // One 클래스와 다른 패키지

import com.ch6class.thisisjavastudy.One;

public class Three {
    //필드
    One a1 = new One(true);    // (O) -> public 생성자 접근가능
    //One a2 = new One(1);        // (X) -> default 생성자 접근불가(컴파일에러)
    //One a3 = new One("문자열");  // (X) -> private 생성자 접근불가(컴파일에러)
}
```

### 11.2 필드와 메소드의 접근제한

```
package com.ch6class.thisisjavastudy;

public class One {//필드와 메소드의 접근 제한
    //필드
    public int field1;  // public 접근제한
    int field2;         // default 접근제한
    private int field3; // private 접근제한

    //생성자
    public One(){ // 클래스 내부일 경우 접근 제한자의 영향을 받지 않는다.
        field1 = 1;  // (O)
        field2 = 1;  // (O)
        field3 = 1;  // (O)

        method1();   // (O)
        method2();   // (O)
        method3();   // (O)
    }

    //메소드
    public void method1() {}  // public 접근제한
    void method2() {}         // default 접근제한
    private void method3() {} // private 접근제한

}
```

```
package com.ch6class.thisisjavastudy; // One 클래스와 같은 패키지

public class Two { // 필드와 메소드의 접근 제한
    public Two(){
        One a = new One();
        a.field1 = 1;   // (O) -> public 필드 접근 가능
        a.field2 = 1;   // (O) -> default 필드 접근 가능
        //a.field3 = 1; // (X) -> private 필드 접근 불가(컴파일에러)

        a.method1();    // (O) -> public 메소드 접근 가능
        a.method2();    // (O) -> default 메소드 접근 가능
        //a.method3();  // (X) -> private 메소드 접근 불가(컴파일에러)
    }
}
```

```
package com.ch6class2.thisisjavastudy; // One 클래스와 다른 패키지

import com.ch6class.thisisjavastudy.One;

public class Three { // 필드와 메소드의 접근 제한
    public Three(){
        One a = new One();
        a.field1 = 1;   // (O) -> public 필드 접근가능
        //a.field2 = 1; // (X) -> default 필드 접근불가(컴파일에러)
        //a.field3 = 1; // (X) -> private 필드 접근불가(컴파일에러)

        a.method1();   // (O) -> public 메소드 접근가능
        //a.method2(); // (X) -> default 메소드 접근불가(컴파일에러)
        //a.method3(); // (X) -> private 메소드 접근불가(컴파일에러)
    }
}
```

---

## 12. 어노테이션(Annotation)

> **어노테이션**은 메타데이터라고 볼 수 있다. 메타데이터란 애플리케이션이 처리해야 할 데이터가 아니라, 컴파일 과정과 실행 과정에서 **코드를 어떻게 컴파일하고 처리할 것인지 알려주는 정보**이다.

### 12.1 어노테이션의 용도

- 컴파일러에게 코드 문법 에러를 체크하도록 정보 제공
- sw개발 퉁이 빌드나 배치 시 코드를 자동으로 생성할 수 있도록 정보 제공
- 실행 시(런타임 시) 특정 기능을 실행하도록 정보 제공

  ..컴파일러에게 코드 문법 에러를 체크하도록 정보를 제공하는 대표적인 예는 `@Override`어노테이션이다. 메소드가 오버라이드(재정의)된 것임을 컴파일러에게 알려주어 **컴파일러가 오버라이드 검사를 하도록** 해준다. 정확히 오버라이드가 되지 않았다면 컴파일러는 에러를 발생시킨다.

### 12.2 어노테이션 타입 정의와 적용

```
package com.ch6class.thisisjavastudy;

import java.lang.annotation.ElementType;
import java.lang.annotation.Retention;
import java.lang.annotation.RetentionPolicy;
import java.lang.annotation.Target;

// (TYPE/ANNOTIATION_TYPE/FIELD/CONSTRUCTOR/METHOD/LOCAL_VARIABLE/PACKAGE)
@Target({ElementType.METHOD}) // 어노테이션이 적용될 대상 지정, 여기선 메소드에만 적용
@Retention(RetentionPolicy.RUNTIME) // 어노테이션 유지 정책 지정(SOURCE/CLASS/RUNTIME)
public @interface PrintAnnotation { //어노테이션 정의
    String value() default "-";
    int number() default 15; // 어노테이션은 element를 멤버로 가질 수 있다.
}
```

- `@interface`를 사용해서 어노테이션을 정의한다.
- 위 예제에서 `PrintAnnotation`은 `value`엘리먼트와 `number`엘리먼트를 멤버로 가진다.
- `value` 엘리먼트를 가진 어노테이션을 코드에서 적용할 때에는 다음과 같이 **값만** 기술할 수 있다.
  ```
  @AnnotationName("값");
  ```

```
package com.ch6class.thisisjavastudy;

public class Service { // PrintAnnotation을 적용한 Service 클래스

    @PrintAnnotation
    public void method1(){
        System.out.println("실행내용1");
    }

    @PrintAnnotation("*") // value 엘리먼트를 가진 어노테이션을 코드에서 적용할 때에는 값만 기술할 수 있다.
    public void method2(){
        System.out.println("실행내용2");
    }

    @PrintAnnotation(value="#", number=20) // value 엘리먼트와 다른 엘리먼트의 값을 동시에 주고 싶을 때
    public void method3(){
        System.out.println("실행내용3");
    }
}

```

### 12.3 어노테이션 유지 정책

- `@Retention`어노테이션을 사용한다.
- 용도에 따라 `@AnnotationName`을 어느 범위까지 유지할 것인지 지정해야 한다.

- `SOURCE`: 소스상에만 유지
- `CLASS`: 컴파일된 클래스까지 유지
- `RUNTIME`: 런타임 시에도 유지, **리플렉션**을 이용해서 런타임 시에 어노테이션 정보를 얻을 수 있다.

- **리플렉션**: 런타임 시에 클래스의 메타 정보를 얻는 기능, 예를 들어 클래스가 가지고 있는 필드가 무엇인지, 어떤 생성자, 어떤 메소드를 가지고 있는지, 적용된 어노테이션이 무엇인지 알아내는 것이다.

### 12.4 런타임 시 어노테이션 정보 사용하기

> 어노테이션 자체는 아무런 동작을 가지지 않는 단지 표식일 뿐이지만, **리플렉션**을 이용해서 어노테이션의 적용 여부와 엘리먼트 값을 읽고 적절히 처리할 수 있다.

```
package com.ch6class.thisisjavastudy;

import java.lang.reflect.Method; // 런타임 시 메소드에 적용된 어노테이션 정보를 얻기위해 import

public class PrintAnnotationExample {
    public static void main(String[] args){
        //리플렉션이란 런타임 시에 클래스의 메타 정보를 얻는 기능
        //예를 들어 클래스가 가지고 있는 필드, 생성자, 메소드가 무엇인지 또는 적용된 어노테이션이 무엇인지 알아내는 것이 리플렉션

        //Service 클래스에 선언된 메소드 얻기(리플렉션)
        Method[] declareMethods = Service.class.getDeclaredMethods();

        //Method 객체를 하나씩 처리
        for(Method method : declareMethods){
            //PrintAnnotation이 적용되었는지 확인
            if(method.isAnnotationPresent(PrintAnnotation.class)){
                //PrintAnnotation 객체 얻기
                PrintAnnotation printAnnotation = method.getAnnotation(PrintAnnotation.class);

                //메소드 이름 출력
                System.out.println("["+method.getName()+"] ");
                //어노테이션이 멤버로 갖고있는 value 엘리먼트의 값 출력
                for(int i=0; i<printAnnotation.number(); i++){
                    System.out.print(printAnnotation.value());
                }
                System.out.println();


                try{
                    //메소드 호출
                    method.invoke(new Service()); // Service 객체 생성 후 Service 객체의 메소드 호출
                } catch (Exception e){}
                System.out.println();
            }
        }
    }
}
```

> 위 Example 클래스는 **리플렉션**을 이용해서 `Service` 클래스에 적용된 어노테이션 정보를 읽고 엘리먼트 값에 따라 출력할 문자를 콘솔에 출력한 후, 해당 메소드를 호출한다.

```
// 실행 결과

[method1]
---------------
실행내용1

[method2]
***************
실행내용2

[method3]
####################
실행내용3

```
