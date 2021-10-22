# 7장 클래스 288-337p

## 1. 상속의 개념

- 부모 클래스의 멤버를 자식 클래스에게 물려주는 것

- 상속은 이미 잘 개발된 클래스를 재사용해서 새로운 클래스를 만들기 때문에 **코드의 중복을 줄여준다.**

- 상속은 부모 클래스의 수정으로 모든 자식 클래스들의 수정 효과를 가져오기 때문에 **유지보수 시간을 최소화**시켜준다.

- 부모 클래스에서 **private** 접근 제한을 갖는 필드와 메소드는 상속 대상에서 **제외**된다.

- 부모 클래스와 자식 클래스가 **다른 패키지**에 존재한다면 **default** 접근 제한을 갖는 필드와 메소드도 상속 대상에서 제외된다.

---

## 2. 클래스 상속

- 자바는 **다중상속**을 허용하지 **않는다.**

```
public class CellPhone {
    //필드
    String model;
    String color;

    //생성자

    //메소드
    void powerOn() { System.out.println("전원을 켭니다."); }
    void powerOff() { System.out.println("전원을 끕니다."); }
    void bell() { System.out.println("벨이 울립니다."); }
    void sendVoice(String message) { System.out.println("본인: "+message); }
    void receiveVoice(String message) { System.out.println("상대방: "+message); }
    void hangUp() { System.out.println("전화를 끊습니다."); }
}
```

```
public class DmbCellPhone  extends CellPhone{ //자식 클래스
    //필드
    int channel;

    //생성자
    DmbCellPhone(String model, String color, int channel){
        //CellPhone으로부터 상속받은 필드
        this.model = model;
        this.color = color;

        this.channel = channel;
    }

    //메소드
    void turnOnDmb(){
        System.out.println("채널 "+channel+"번 DMB 방송 수신을 시작합니다.");
    }

    void changeChannelDmb(int channel){
        this.channel = channel;
        System.out.println("채널 "+channel+"번으로 바꿉니다.");
    }

    void turnOffDmb(){
        System.out.println("DMB 방송 수신을 멈춥니다.");
    }
}

```

```
public class DmbCellPhoneExample { //자식클래스 사용
    public static void main(String[] agrs){
        //DmbCellPhone 객체 생성
        DmbCellPhone dmbCellPhone = new DmbCellPhone("자바폰", "화이트", 10);

        //CellPhone으로부터 상속받은 필드
        System.out.println("모델: "+dmbCellPhone.model);
        System.out.println("색상: "+dmbCellPhone.color);

        //DmbCellPhone의 필드
        System.out.println("채널: "+dmbCellPhone.channel);

        //CellPhone으로부터 상속받은 메소드 호출
        dmbCellPhone.powerOn();
        dmbCellPhone.bell();
        dmbCellPhone.sendVoice("여보세요 나야");
        dmbCellPhone.receiveVoice("안녕하세요! 저는 홍길동인데요");
        dmbCellPhone.sendVoice("아~ 예 반갑습니다.");
        dmbCellPhone.hangUp();

        //DmbCellPhone의 메소드 호출
        dmbCellPhone.turnOnDmb();
        dmbCellPhone.changeChannelDmb(12);
        dmbCellPhone.turnOffDmb();
    }
}
```

---

## 3. 부모 생성자 호출

- 자식 객체를 생성하면, **부모 객체가 먼저** 생성되고 자식 객체가 그 다음에 생성된다.

```
 DmbCellPhone dmbCellPhone = new DmbCellPhone();
```

![부모 생성자 호출](https://postfiles.pstatic.net/MjAyMTEwMjJfMjM5/MDAxNjM0OTEzNjYzNDAy.iGEdoKv_E6foBwFbI66lXGC1UmocWADAO334jdVs9wYg.mbJBX86Zdmqp6yoBku285u3VxDAMITYR7dWmq1x7hD8g.JPEG.chex417/%EB%B6%80%EB%AA%A8%EC%83%9D%EC%84%B1%EC%9E%90%ED%98%B8%EC%B6%9C.jpg?type=w773)

- 모든 객체는 클래스의 **생성자**를 호출해야만 생성된다.
- **부모 생성자는 자식 생성자의 맨 첫 줄에서 호출된다.**
- 자식인 DmbCellPhone의 생성자가 명시적으로 선언되지 않았다면 컴파일러는 다음과 같은 **기본 생성자**를 생성해 낸다.

```
public DmbCellPhone(){
    super(); // 부모의 기본 생성자 호출
}
```

- 만약 직접 자식 생성자를 선언하고 명시적으로 부모 생성자를 호출하고 싶다면 다음과 같이 작성하면 된다.

```
자식클래스(매개변수선언, ...){
    super(매개값, ...);
    ...
}
```

- `super(매개값, ...)`가 생략되면 컴파일러에 의해 `super()`가 자동적으로 추가되기 때문에 **부모의 기본 생성자가 존재해야 한다.**
- 부모 클래스에 기본 생성자가 없고 매개 변수가 있는 생성자만 있다면 자식 생성자에서 **반드시 부모 생성자 호출을 위해 `super(매개값, ...)`를 명시적으로 호출해야 한다.**
- `super(매개값, ...)`는 반드시 **자식 생성자 첫 줄에 위치해야 한다.**

---

## 4. 메소드 오버라이딩(재정의)

> **메소드 오버라이딩**은 상속된 메소드의 내용이 자식 클래스에 맞지 않을 경우, 자식 클래스에서 동일한 메소드를 재정의하는 것을 말한다.

![메소드 오버라이딩](https://postfiles.pstatic.net/MjAyMTEwMjJfMjYy/MDAxNjM0OTE0NDY1NzQz.b-4nDQ9PNyccDD10R0eMGY6-H4W0BNfb23RGT0v1OhYg.NGkVyTjvRWbKi9V0IQsl41zvP0uZO7Hg7RSvVeNhvusg.JPEG.chex417/%EB%A9%94%EC%86%8C%EB%93%9C%EC%98%A4%EB%B2%84%EB%9D%BC%EC%9D%B4%EB%94%A9.jpg?type=w773)

    <주의>
    - 부모의 메소드와 동일한 시그니처(리턴타입, 메소드 이름, 매개변수 리스트)를 가져야 한다.
    - 접근제한을 더 강하게 오버라이딩할 수 없다.
    - 새로운 예외(Exception)를 throws할 수 없다.(예외는 10장에서 학습)

- 예를 들어, 부모 메소드가 default 접근 제한을 가지면 재정의되는 자식 메소드는 default 또는 public 접근 제한을 가질 수 있다.

### 4.1. 부모 메소드 호출(super)

- 자식 클래스 내부에서 오버라이딩된 부모 클래스의 메소드를 호출해야 하는 상황이 발생한다면 명시적으로 `super` 키워드를 붙여서 부모 메소드를 호출할 수 있다.

```
public class Airplane {
    public void land(){
        System.out.println("착륙합니다.");
    }

    public void fly(){
        System.out.println("일반비행합니다.");
    }

    public void takeOff(){
        System.out.println("이륙합니다.");
    }
}
```

```
public class SupersonicAirplane extends Airplane{
    public static final int NORMAL = 1;
    public static final int SUPERSONIC = 2;

    public int flyMode = NORMAL;

    @Override
    public void fly(){ //오버라이딩하고 부모 메소드 호출하기 위해선 super 사용해야함
        if(flyMode == SUPERSONIC){
            System.out.println("초음속비행합니다.");
        }else{
            //Airplane 객체의 fly() 메소드 호출
            super.fly();
        }
    }
}
```

```
public class SupersonicAirplaneExample {
    public static void main(String[] args){
        SupersonicAirplane sa = new SupersonicAirplane(); // 자식 객체 생성
        sa.takeOff(); // 부모 메소드
        sa.fly(); // 부모 메소드
        sa.flyMode = SupersonicAirplane.SUPERSONIC;
        sa.fly(); // 오버라이딩된 자식 메소드
        sa.flyMode = SupersonicAirplane.NORMAL;
        sa.fly(); // super 부모 메소드
        sa.land();
    }
}

```

---

## 5. final 클래스와 final 메소드

### 5.1. final 클래스 - 상속할 수 없는 클래스

```
public final class Member {...}
```

### 5.2. final 메소드 - 오버라이딩 할 수 없는 메소드

```
public final void stop(){...}
```

---

## 6. 타입 변환과 다형성

> 다형성이란 '같은 타입이지만 실행 결과가 다양한' 객체를 이용할 수 있는 성질을 말한다.

- 부모 타입에 모든 자식 객체가 대입될 수 있다. (객체의 부품화)

### 6.1. 자동 타입 변환(Promotion)

    자동 타입 변환의 개념은 자식은 부모의 특징과 기능을 상속받기 때문에 부모와 동일하게 취급될 수 있다는 것이다.

- 자식 타입은 부모 타입으로 자동 타입 변환이 가능하다.

```
부모클래스 변수 = 자식클래스타입;
Aniaml animal = new Cat();
또는
Cat cat = new Cat();
Animal animal = cat;
```

![자동 타입 변환](https://postfiles.pstatic.net/MjAyMTEwMjNfNTUg/MDAxNjM0OTE1NDQ2NTc1.yh5oUpRA_07xODFNC5LSbJbYiZlcBaK9TdZatansUXIg.rkAZArjGAw4I1_1WIuEOBDlMqG7lVySp1FM0PrSlnpAg.JPEG.chex417/%EC%9E%90%EB%8F%99%ED%83%80%EC%9E%85%EB%B3%80%ED%99%98.jpg?type=w773)

- `cat`과 `animal` 변수는 타입만 다를 뿐, 동일한 `Cat` 객체를 참조한다.

![타입변환 오버라이딩](https://postfiles.pstatic.net/MjAyMTEwMjNfMjg2/MDAxNjM0OTE1OTMzNDE4.KDJmHObHnMSWA64MDU91-3S5_bN4DfXUSpkzMyQhIRkg.1N_KdkY7yOlKTbDVV0U4JBDlq7puZlQcIesfN8w9tFsg.JPEG.chex417/%ED%83%80%EC%9E%85%EB%B3%80%ED%99%98%EC%98%A4%EB%B2%84%EB%9D%BC%EC%9D%B4%EB%94%A9.jpg?type=w773)

- 부모타입으로 `자동 타입 변환`된 이후에는 **부모 클래스에 선언된 필드와 메소드만 접근이 가능하다.**
- 비록 변수는 자식 객체를 참조하지만 변수로 접근 가능한 멤버는 부모 클래스로만 한정된다.
- 그러나 예외가 있는데, 메소드가 자식클래스에 **오버라이딩**되었다면 자식 클래스의 메소드가 대신 호출 된다.

### 6.2. 상속계층 자동 타입 변환

![상속계층](https://postfiles.pstatic.net/MjAyMTEwMjNfMjMy/MDAxNjM0OTE1NjE0MDY0.J_3H0oPNQxaCRKiURicU9pLyNElXsl9OCndK2E-arxIg.TTAnxo2MZAaNXQJnrHysvQdR66JVfaUukFi6nG08CwIg.JPEG.chex417/%EC%83%81%EC%86%8D%EA%B3%84%EC%B8%B5%EC%83%81%EC%9C%84%ED%83%80%EC%9E%85.jpg?type=w773)

    바로 위의 부모가 아니더라도 상속 계층에서 상위 타입이라면 자동 타입 변환이 일어날 수 있다.

### 6.3. 필드의 다형성

    필드의 타입은 변함이 없지만 실행 도중에 어떤 객체를 필드로 저장하느냐에 따라 실행결과가 달라질 수 있다. 이것이 필드의 다형성이다.

```
class Car{
    //필드
    Tire frontLeftTire = new Tire();
    Tire frontRightTire = new Tire();
    Tire backLeftTire = new Tire();
    Tire backRightTire = new Tire();

    //메소드
    void run(){...}
}
```

```
Car myCar = new Car();
myCar.frontRightTire = new HankookTire();
myCar.backLeftTire = new KumhoTire();
myCar.run();
```

- `Tire`클래스 타입인 `frontRightTire`와 `backLeftTire`는 원래 `Tire`객체가 저장되어야 하지만, `Tire`의 자식 객체(HankookTire, KumhoTire)가 저장되어도 문제가 없다.
- 왜냐하면 자식 타입은 부모 타입으로 `자동 타입 변환`이 되기 때문이다.

### 6.4. 매개변수의 다형성

> 매개변수에 자식 타입 객체를 지정하여 매개변수의 다형성을 구현할 수 있다. 매개값으로 어떤 자식 객체가 제공되느냐에 따라 메소드의 실행 결과는 다양해질 수 있다.(**매개변수의 다형성**)

```
public class Vehicle {//부모클래스 // 매개변수의 다형성
    public void run(){
        System.out.println("차량이 달립니다.");
    }
}
```

```
public class Driver {
    public void drive(Vehicle vehicle){
        vehicle.run();
    }
}
```

```
public class Bus extends Vehicle{//자식클래스 // 매개변수의 다형성
    @Override
    public void run(){ // 메소드 오버라이딩
        System.out.println("버스가 달립니다.");
    }
}
```

```
public class Taxi extends Vehicle{//자식클래스 //매개변수의 다형성
    @Override
    public void run(){ // 메소드 오버라이딩
        System.out.println("택시가 달립니다.");
    }
}
```

```
public class DriverExample {//매개변수의 다형성
    public static void main(String[] args){
        Driver driver = new Driver();

        Bus bus = new Bus();
        Taxi taxi = new Taxi();

        driver.drive(bus); // 자동타입변환: Vehicle vehicle = bus;
        driver.drive(taxi); // 자동타입변환: Vehicle vehicle = taxi;
    }
}

```

- `drive()`메소드는 `Vehicle` 타입을 매개 변수로 선언했지만, `Vehicle`을 상속받는 `Bus`객체가 매개값으로 사용되면 `자동 타입 변환`이 발생한다.

- 즉, 매개변수의 타입이 클래스일 경우, 해당 클래스의 객체뿐만 아니라 자식 객체까지도 매개값으로 사용할 수 있다.

### 6.5. 강제 타입 변환(Casting)

    강제 타입 변환은 부모 타입을 자식 타입으로 변환하는 것을 말한다.

- 모든 부모 타입을 자식 클래스 타입으로 강제 변환할 수 있는 것은 아니다.
- **_자식 타입이 부모 타입으로 자동 변환한 후,_** 다시 자식 타입으로 변환할 때 강제 타입 변환을 사용할 수 있다.

![강제타입변환](https://postfiles.pstatic.net/MjAyMTEwMjNfNDgg/MDAxNjM0OTE3MDk3MjI0.FD6jqzVDW9Pk0-8lnRWNrKOqD9yHqwHl-ykGmkeRn7Ag.qJ5A0Chd5ZfjMhqPgLIw9ERihyUlntOGAW3Z0EvpEaEg.JPEG.chex417/%EA%B0%95%EC%A0%9C%ED%83%80%EC%9E%85%EB%B3%80%ED%99%98.jpg?type=w773)

- 자식 타입이 부모 타입으로 자동 변환하면, 부모 타입에 선언된 필드와 메소드만 사용 가능하다는 제약 사항이 따른다.
- 만약 자식 타입에 선언된 필드와 메소드를 꼭 사용해야 한다면 `강제 타입 변환`을 해서 다시 자식 타입으로 변환한 다음 자식 타입의 필드와 메소드를 사용하면 된다.

- 강제 타입 변환 전에 `instanceof` 연산자로 변환 가능한지 검사하는 것이 좋다.

```
    public static void method1(Parent parent){ //Parent객체, Child객체 둘다 가능
        if(parent instanceof Child){ // Child 객체인지 조사
            Child child = (Child) parent;
            System.out.println("method1 - Child로 변환 성공");
        }else{
            System.out.println("method1 = Child로 변환되지 않음");
        }
    }
```

---

## 7. 추상 클래스

> 클래스들의 공통적인 특성을 추출해서 선언한 클래스를 **추상 클래스**라고 한다.

- 추상클래스(부모)와 실체 클래스(자식)는 **상속**의 관계를 가지고 있다.
- 추상 클래스는 객체를 직접 생성해서 사용할 수 없다.
- 즉 추상클래스는 `new`연산자를 사용해서 인스턴스를 생성하지 못한다.

```
Animal animal = new Animal(); (X)
```

### 7.1. 추상 클래스의 용도

- 실체 클래스들의 공통된 필드와 메소드의 이름을 통일
- 실체 클래스를 작성할 때 시간을 절약(공통적인 부분은 추상 클래스에 선언)

### 7.2. 추상 클래스 선언

```
public abstract class Phone { //추상클래스
    public String owner;

    public Phone(String owner){
        this.owner = owner;
    }

    public void turnOn(){
        System.out.println("폰 전원을 켭니다.");
    }

    public  void turnOff(){
        System.out.println("폰 전원을 끕니다.");
    }
}

```

public class SmartPhone extends Phone{ //실체 클래스
public SmartPhone(String owner){
super(owner);
}

    public void internetSearch(){
        System.out.println("인터넷 검색을 합니다.");
    }

}

```
public class PhoneExample {
    public static void main(String[] args){
        //Phone phone = new Phone();

        SmartPhone smartPhone = new SmartPhone("홍길동");

        smartPhone.turnOn();
        smartPhone.internetSearch();
        smartPhone.turnOff();
    }
}
```

- 추상클래스는 `new`연산자로 직접 생성자를 호출할 수는 없지만 자식 객체가 생성될 때 `super(...)`를 호출해서 추상클래스의 객체(부모)를 생성하므로 **추상 클래스도 생성자가 반드시 있어야 한다.**

### 7.3. 추상 메소드와 오버라이딩

> 추상 메소드는 `추상 클래스`에서만 선언할 수 있는데 메소드의 **선언부**만 있고 실행 내용인 **중괄호{}가 없는** 메소드를 말한다.

- 하위 클래스가 반드시 실행 내용을 채우도록 하고싶다면 해당 메소드를 추상 메소드로 선언하면 된다.
- 자식 클래스는 반드시 **추상 메소드를 오버라이딩 해서** 실행 내용을 작성해야 하는데, 그렇지 않으면 **컴파일 에러**가 발생한다.

```
public abstract class Animal {//추상 클래스
    public String kind;

    public void breathe(){
        System.out.println("숨을 쉽니다.");
    }

    public abstract void sound(); // 추상 메소드 ({}가 없음)
}
```

```
public class Dog extends Animal{//추상클래스 상속
    public Dog(){
        this.kind = "포유류";
    }

    @Override
    public void sound(){ //추상메소드 오버라이딩
        System.out.println("멍멍");
    }
}

```

```
public class Cat extends Animal{//추상클래스 상속
    public Cat(){
        this.kind="포유류";
    }

    @Override
    public void sound(){//추상메소드 오버라이딩
        System.out.println("야옹");
    }
}
```

```
public class AnimalExample {
    public static void main(String[] args) {
        Dog dog = new Dog();
        Cat cat = new Cat();
        dog.sound();
        cat.sound();
        System.out.println("-----");

        //변수의 자동 타입 변환
        Animal animal = null;
        animal = new Dog(); //자동타입변환
        animal.sound(); //오버라이딩된 메소드 호출

        animal = new Cat(); //자동타입변환
        animal.sound();
        System.out.println("-----");

        //매개변수의 다형성 - 부모타입의 매개변수에 자식 객체를 대입
        animalSound(new Dog());
        animalSound(new Cat());

    }

    public static void animalSound(Animal animal){
        animal.sound(); //오버라이딩된 메소드 호출
    }

}

```

---
