# 8장 인터페이스 344-385p

## 1. 인터페이스의 역할

![인터페이스의 역할](https://postfiles.pstatic.net/MjAyMTEwMzFfMTg4/MDAxNjM1NjM5NTI2NDYw.eWuIl0Lvvk4gfRhbqTuNve21L704Ysi4vWdWbmudV0Yg.8aAoi-RfRwUX--4iqZdD4AQex09guwaQC7dSmrX33DUg.JPEG.chex417/%EC%9D%B8%ED%84%B0%ED%8E%98%EC%9D%B4%EC%8A%A4%EC%9D%98%EC%97%AD%ED%95%A0.jpg?type=w773)

- 자바에서 **인터페이스**는 **객체의 사용 방법을 정의**한 타입이다.

- 개발 코드는 객체의 내부 구조를 알 필요가 없고 인터페이스의 메소드만 알고 있으면 된다.

- 인터페이스를 사용하는 이유? 개발 코드를 수정하지 않고 사용하는 객체를 변경할 수 있도록 하기 위해서이다.

---

## 2. 인터페이스의 선언

- 인터페이스는 "~.java"형태의 소스 파일로 작성되고 컴파일러(javac.exe)를 통해 "~.class" 형태로 컴파일되기 때문에 물리적 형태는 클래스와 동일하다.

- `interface` 키워드를 사용한다.

        [ public ] interface 인터페이스명 {...}

- 인터페이스는 `상수`와 `메소드`만을 구성 멤버로 가진다.

- 인터페이스는 객체로 생성할 수 없기 때문에 \*_생성자를 가질 수 없다_.\*

- 자바7 이전까지는 인터페이스의 메소드는 `추상 메소드`로만 선언이 가능했지만, 자바8부터는 `디폴트 메소드`와 `정적 메소드`도 선언이 가능하다.

```
interface 인터페이스명 {
    //상수
    타입 상수명 = 값;

    //추상 메소드
    타입 메소드명(매개변수, ...);

    //디폴트 메소드
    default 타입 메소드명(매개변수, ...){...}

    //정적 메소드
    static 타입 메소드명(매개변수) {...}
}
```

```
public interface RemoteControl {
    //상수 필드 선언
    public int MAX_VOLUME = 10;
    public int MIN_VOLUME = 0;

    //추상 메소드 -> 메소드 선언부만 작성
    public void turnOn();
    public void turnOff();
    public void setVolume(int volume);

    //디폴트 메소드 -> 실행 내용까지 작성
    default void setMute(boolean mute){
        if(mute){
            System.out.println("무음 처리합니다.");
        }else{
            System.out.println("무음 해제합니다.");
        }
    }

    //정적 메소드
    static void changeBattery(){
        System.out.println("건전지를 교환합니다.");
    }
}
```

### 2.1. 상수 필드(Constatnt Field)

- 인터페이스는 객체 사용 설명서이므로 런타임 시 데이터를 저장할 수 있는 필드를 선언할 수 없지만 상수 필드는 선언이 가능하다.
- 상수는 인터페이스에 고정된 값으로 런타임 시에 데이터를 바꿀 수 없다.
- 상수를 선언할 때에는 반드시 초기값을 대입해야 한다.

```
public interface RemoteControl {
    //상수 필드 선언
    public int MAX_VOLUME = 10;
    public int MIN_VOLUME = 0;
}
```

### 2.2. 추상 메소드(Abstract Method)

- 추상메소드는 객체가 가지고 있는 메소드를 설명한 것
- 어떤 매개값이 필요하고, 리턴 타입이 무엇인지만 알려준다.
- 실제 실행부는 객체(구현 객체)가 가지고 있다.

![추상메소드 선언](https://postfiles.pstatic.net/MjAyMTEwMzFfMjE2/MDAxNjM1NjQwNDQ5MjIz.0oVY4IBknu-cgAoUIf5JZFrEtr6vxBQ2cuejc5ii46Mg.0D_SqOiPBqZZgaAlBwZ2vQA-g06jYAQKOJEm05hjuE0g.JPEG.chex417/%EC%B6%94%EC%83%81%EB%A9%94%EC%86%8C%EB%93%9C_%EC%84%A0%EC%96%B8.jpg?type=w773)

- 인터페이스에 선언된 `추상 메소드`는 모두 `public abstract`의 특성을 갖기 때문에 `public abstract`를 생략하더라도 자동적으로 컴파일 과정에서 붙게 된다.

### 2.3. 디폴트 메소드(Default Method)

- 디폴트 메소드는 인터페이스에 선언되지만 사실은 객체(구현 객체)가 가지고 있는 인스턴스 메소드라고 생각해야 한다.
- 자바8에서 디폴트 메소드를 허용한 이유는 기존 인터페이스를 확장해서 새로운 기능을 추가하기 위해서이다.
- `디폴트 메소드`는 `public`특성을 갖기 때문에 `public`을 생략하더라도 자동적으로 컴파일 과정에서 붙게 된다.

-        [public] defalut 리턴타입 메소드명(매개변수, ...) {...}

### 2.4. 정적 메소드(Static Method)

- 정적 메소드도 역시 자바8부터 작성할 수 있는데, 디폴트 메소드와는 달리
- 정적 메소드는 **객체가 없어도** 인터페이스 만으로 호출이 가능하다.
- `public` 특성을 갖기 때문에 `public`을 생략하더라도 자동적으로 컴파일 과정에서 붙게 된다.
-       [public] static 리턴타입 메소드명(매개변수, ...) {...}

---

## 3. 인터페이스 구현

![인터페이스 구현](https://postfiles.pstatic.net/MjAyMTEwMzFfMjIw/MDAxNjM1NjQxMDY5NjE1.p6Dj4hbhxur5MSNB5Zt4MfsFrGcaGOFRDQWC5QMpPqwg.oF4WBJkmRpevTh7VzHzG4p1fFprtQZ7HNC9li65bVccg.JPEG.chex417/%EC%9D%B8%ED%84%B0%ED%8E%98%EC%9D%B4%EC%8A%A4_%EA%B5%AC%ED%98%84.jpg?type=w773)

- 개발 코드가 인터페이스 메소드를 호출하면 인터페이스는 객체의 메소드를 호출한다.
- 객체는 인터페이스에서 정의된 **추상 메소드와 동일한** 메소드 이름, 매개 타입, 리턴 타입을 가진 실체 메소드를 가지고 있어야 한다.
- 이러한 객체를 `구현(implement) 객체`라고 하고,
- 구현 객체를 생성하는 클래스를 `구현 클래스`라고 한다.

### 3.1. 구현 클래스

    구현 클래스는 보통의 클래스와 동일한데, 인터페이스 타입으로 사용할 수 있음을 알려주기 위해 클래스 선언부에 implements 키워드를 추가하고 인터페이스 명을 명시해야 한다.

    public class 구현 클래스명 implements 인터페이스명 {
        //인터페이스에 선언된 추상 메소드의 실체 메소드 선언
    }

```
public class Television implements RemoteControl{ //구현 클래스
    //필드
    private int volume;

    //turnOn() 추상 메소드의 실체 메소드
    public void turnOn(){
        System.out.println("TV를 켭니다.");
    }

    //turnOff() 추상 메소드의 실체 메소드
    public void turnOff(){
        System.out.println("TV를 끕니다.");
    }

    //setVolume() 추상 메소드의 실체 메소드 -> 인터페이스 상수를 이용해서 volume 필드의 값을 제한함
    public void setVolume(int volume){
        if(volume>RemoteControl.MAX_VOLUME){
            this.volume = RemoteControl.MAX_VOLUME;
        }else if(volume<RemoteControl.MAX_VOLUME){
            this.volume = RemoteControl.MAX_VOLUME;
        }else{
            this.volume = volume;
        }

        System.out.println("현재 TV 볼륨: "+this.volume);
    }
}
```

- `Television클래스`는 `RemoteControl 인터페이스`로 사용이 가능하다.
- `RemoteControl`에는 3개의 추상 메소드가 있기 때문에 `Television`은 이 추상 메소드들에 대한 **실체 메소드**를 가지고 있어야 한다.
- 구현 클래스에서 실체 메소드를 작성할 때 주의할 점은 인터페이스의 모든 메소드들은 기본적으로 `public` 접근 제한을 갖기 때문에 `public`보다 더 낮은 접근 제한으로 작성할 수 없다. `public`을 생략하면 `Cannot reduce the visibility of the inherited method`라는 컴파일 에러가 뜬다.

```
public abstract class Television implements RemoteControl{
    public void turnOn() {...}
    public void turnOff() {...}
    //setVolume()의 실체 메소드가 없다.(일부만 구현)
}
```

- 만약 인터페이스에 선언된 추상 메소드에 대응하는 실체 메소드를 구현 클래스가 작성하지 않으면 구현 클래스는 자동적으로 `추상 클래스`가 된다. 그렇기 때문에 클래스 선언부에 `abstract` 키워드를 추가해야 한다.

### 3.2. 인터페이스 사용 맛보기

- Television 객체를 생성하고 Television 변수에 대입한다고 인터페이스를 사용하는 것이 아니다.

```
Television tv = new Television(); //(X)
```

- 인터페이스로 구현 객체를 사용하려면 인터페이스 변수를 선언하고 구현 객체를 대입해야 한다.
- 인터페이스 변수는 **참조 타입**이기 때문에 구현 객체가 대입될 경우 구현 객체의 **번지**를 저장한다.

```
인터페이스 변수;
변수 = 구현객체
or
인터페이스 변수 = 구현객체;
```

```
public class RemoteControlExample {
    public static void main(String[] args){
        RemoteControl rc = null; //인터페이스 변수rc 선언(참조타입)
        rc = new Television(); // 인터페이스 변수에 구현 객체 대입(구현 객체의 번지를 저장)
        rc.turnOn();
        rc.setMute(true);
        rc.turnOff();

        //인터페이스의 정적메소드는 인터페이스로 바로 호출이 가능하다.
        RemoteControl.changeBattery();
    }
}
```

### 3.3. 익명 구현 객체

    구현 클래스를 만들어 사용하는 것이 일반적이고, 클래스를 재사용할 수 있기 때문에 편리하지만,
    일회성의 구현 객체를 만들기 위해 소스 파일을 만들고 클래스를 선언하는 것은 비효율적이다.
    자바는 소스 파일을 만들지 않고도 구현 객체를 만들 수 있는 방법을 제공하는데, 그것이 익명 구현 객체이다.

    UI프로그래밍에서 이벤트를 처리하기 우히ㅐ, 그리고 임시 작업 스레드를 만들기 위해 익명 구현 객체를 많이 활용한다.

```
인터페이스 변수 = new 인터페이스(){
    //인터페이스에 선언된 추상 메소드의 실체 메소드 선언
};
```

- 인터페이스(){}는 인터페이스를 구현해서 {}과 같이 클래스를 선언하라는 뜻
- new 연산자는 이렇게 선언된 클래스를 객체로 생성한다.
- {}에는 인터페이스에 선언된 모든 추상 메소드의 실체 메소드를 작성해야 한다. 그렇지 않으면 컴파일 에러가 발생한다.
- 추가적으로 필드와 메소드를 선언할 수 있지만, 익명 객체 안에서만 사용할 수 있고 인터페이스 변수로 접근할 수 없다.

```
public class RemoteControlExample {
    public static void main(String[] args){
        RemoteControl rc = new RemoteControl() { //익명 구현 객체
            public void turnOn(){/*실행문*/}
            public void turnOff(){/*실행문*/}
            public void setVolume(int volume){/*실행문*/}
        };
    }
}
```

---

## 4. 다중 인터페이스 구현 클래스

> 인터페이스A와 B가 객체의 메소드를 호출할 수 있으려면 객체는 이 두 인터페이스를 **모두** 구현해야 한다.

![다중 인터페이스 구현 클래스](https://postfiles.pstatic.net/MjAyMTEwMzFfMTI3/MDAxNjM1NjQyNjgzMDE2.tv-jg9EwjVuc6fX4EeMQeuMKPZAwEDh85j47D6yG5Qgg.fiQZg-4CDamtMEQOtMUsdzBWopFSSdxTyQTbyDTu0eEg.JPEG.chex417/%EB%8B%A4%EC%A4%91%EC%9D%B8%ED%84%B0%ED%8E%98%EC%9D%B4%EC%8A%A4_%EA%B5%AC%ED%98%84_%ED%81%B4%EB%9E%98%EC%8A%A4.jpg?type=w773)

```
public class 구현 클래스명 implements 인터페이스A, 인터페이스B{
    //인터페이스 A에 선언된 추상 메소드의 실체 메소드 선언
    //인터페이스 B에 선언된 추상 메소드의 실체 메소드 선언
}
```

    <주의>
    - 다중 인터페이스를 구현할 경우, 구현 클래스는 모든 인터페이스의 추상 메소드에 대해 실체 메소드를 작성해야한다.
    - 만약 하나라도 없으면 추상 클래스로 선언해야 한다.

```
public class SmartTelevision implements  RemoteControl, Searchable{ //다중인터페이스 구현 클래스

    private int volume;
    public void turnOn(){//RemoteControl의 추상메소드에 대한 실체 메소드
        System.out.println("TV를 켭니다.");
    }
    public void turnOff(){//RemoteControl의 추상메소드에 대한 실체 메소드
        System.out.println("TV를 끕니다.");
    }
    public void setVolume(int volume){//RemoteControl의 추상메소드에 대한 실체 메소드
        if(volume>RemoteControl.MAX_VOLUME){
            this.volume = RemoteControl.MAX_VOLUME;
        }else if(volume<RemoteControl.MAX_VOLUME){
            this.volume = RemoteControl.MAX_VOLUME;
        }else{
            this.volume = volume;
        }
        System.out.println("현재 TV 볼륨: "+this.volume);
    }

    public void search(String url){ //Searchable인터페이스의 추상메소드에 대한 실체 메소드
        System.out.println(url+"을 검색합니다.");
    }
}
```

---

## 5. 인터페이스 사용

> 인터페이스로 구현 객체를 사용하려면 `인터페이스 변수`를 선언하고 `구현 객체`를 대입해야 한다.

![인터페이스의 사용](https://postfiles.pstatic.net/MjAyMTEwMzFfMjI3/MDAxNjM1NjQzNTQ4ODI3.ZmKFf0OGjTW6E6TJ9q17rDLyUJxZILlKYsRxmsegiH0g.09ivMDeI33qoEv7iPqNeXgftwX_A_4i6nouvVaO2TLUg.JPEG.chex417/%EC%9D%B8%ED%84%B0%ED%8E%98%EC%9D%B4%EC%8A%A4%EC%9D%98_%EC%82%AC%EC%9A%A9.jpg?type=w773)

- 인터페이스는 `클래스의 필드`/`생성자의 매개변수`/`메소드의 매개변수`/`생성자의 로컬 변수`/`메소드의 로컬변수`로 선언될 수 있다.

### 5.1. 추상 메소드 사용

```
RemoteControl rc = new Televsion(); //인터페이스 변수rc에 Televsion(구현 객체) 대입
rc.turnOn(); //인터페이스의 turnOn()호출 -> Television의 turnOn() 실행
rc. turnOff(); //인터페이스의 turnOff()호출 -> Television의 turnOff() 실행
```

### 5.2. 디폴트 메소드 사용

- 디폴트 메소드는 인터페이스에 선언되지만 인터페이스에서 바로 사용할 수 없다.

        RemoteControl.setMute(true); (X)

- 디폴트 메소드는 추상 메소드가 아닌 **인스턴스 메소드**이므로 **구현 객체**가 있어야 사용할 수 있다.

        RemoteControl rc = new Television();
        rc.setMute(true);

- 디폴트 메소드는 인터페이스의 모든 구현 객체가 가지고 있는 기본 메소드라고 생각하면 된다. (**오버라이딩 가능**)

### 5.3. 정적 메소드 사용

> 인터페이스의 정적메소드는 인터페이스로 바로 호출이 가능하다.

```
public class RemoteControlExample{
    public static void main(String[] args){
        RemoteControl.changeBattery(); //인터페이스로 정적메소드 호출
    }
}
```

---

## 6. 타입 변환과 다형성

> 요즘은 상속보다는 인터페이스를 통해서 다형성을 구현하는 경우가 더 많다.

> 프로그램 소스 코드는 변함이 없는데, 구현 객체를 교체함으로써 프로그램의 실행 결과가 다양해진다. 이것이 **인터페이스의 다형성**이다.

- `상속`은 **같은 종류**의 하위 클래스를 만드는 기술
- `인터페이스`는 **사용 방법**이 동일한 클래스를 만드는 기술

![인터페이스의 다형성](https://postfiles.pstatic.net/MjAyMTEwMzFfNzUg/MDAxNjM1NjQ0NTIxNDY3.2uaoHkgMTfXVnDVUDZ9ro_3o54KJP4kOaE1ieX8OgeEg.cAd9o6RT_dfeXxtBWTJwsWJ0Mg9PTSybgNeBlR4-F9Ug.JPEG.chex417/%EC%9D%B8%ED%84%B0%ED%8E%98%EC%9D%B4%EC%8A%A4%EC%9D%98_%EB%8B%A4%ED%98%95%EC%84%B1.jpg?type=w773)

- 전체 프로그램을 테스트해보니 `A클래스`에 문제가 있어 `B클래스`로 바꾸기로 했다.
- A, B클래스를 설계할 때 **_메소드 선언부를 완전히 동일하게_** 설계하면 메소드 호출 방법이 동일하므로 **_메소드 호출 코드는 수정할 필요 없이_** 객체 생성 부분만 A클래스에서 B클래스로 바꾸기만 하면 된다.
- 문제는 A, B 클래스를 설계할 때 메소드 선언부를 완전히 동일하게 설계할 수 있느냐인데 이 문제를 해결하려면 **_인터페이스를 작성하고 A, B클래스를 구현 클래스로 작성하면 된다!_**

### 6.1. 자동 타입 변환(Promotion)

    구현 객체가 인터페이스 타입으로 변환되는 것은 **자동 타입 변환**에 해당한다. 자동 타입 변환은 프로그램 실행 도중에 자동적으로 타입 변환이 일어나는 것을 말한다.

```
인터페이스 변수 = 구현객체;
```

- 인터페이스 구현 클래스를 상속해서 자식 클래스로 만들었다면 자식 객체 역시 인터페이스 타입으로 자동 타입 변환 시킬 수 있다.

### 6.2. 필드의 다형성

    <상속>
    타이어(클래스타입) - 한국타이어, 금호타이어(자식객체)

    <인터페이스>
    타이어(인터페이스) - 한국타이어, 금호타이어(구현클래스)

- 한국 타이어와 금호 타이어는 공통적으로 타이어 인터페이스를 구현했기 때문에 모두 타이어 인터페이스에 있는 메소드를 가지고 있다.
- 따라서 인터페이스로 동일하게 사용할 수 있는 교체 가능한 객체에 해당한다.

```
public interface Tire { //필드의 다형성을 이해해보자
    public void roll(); //roll()메소드 호출 방법 설명
}
```

```
public class HankookTire implements Tire{//구현 클래스
    @Override
    public void roll(){//Tire 인터페이스 구현
        System.out.println("한국 타이어가 굴러갑니다.");
    }
}
```

```
public class KumhoTire implements Tire{//구현 클래스
    @Override
    public void roll(){ //Tire 인터페이스 구현
        System.out.println("금호 타이어가 굴러갑니다.");
    }
}
```

```
public class Car {//필드 다형성
    //인터페이스 타입 필드 선언과 초기 구현 객체 대입
    Tire frontLeftTire = new HankookTire();
    Tire frontRightTire = new HankookTire();
    Tire backLeftTire = new HankookTire();
    Tire backRightTire = new HankookTire();

    void run(){//인터페이스에서 설명된 roll()메소드 호출
        frontLeftTire.roll();
        frontRightTire.roll();
        backLeftTire.roll();
        backRightTire.roll();
    }
}
```

```
public class CarExample {//필드 다형성 테스트
    public static void main(String[] args){
        Car myCar = new Car();

        myCar.run();

        myCar.frontLeftTire = new KumhoTire();
        myCar.frontRightTire = new KumhoTire();

        myCar.run();
    }
}
```

### 6.4. 매개변수의 다형성

> 인터페이스 타입으로 매개 변수를 선언하면 메소드 호출 시 매개값으로 여러 가지 종류의 구현 객체를 줄 수 있기 때문에 메소드 실행 결과가 다양하게 나온다.(**매개변수의 다형성**)

![매개변수의 다형성](https://postfiles.pstatic.net/MjAyMTEwMzFfMTcy/MDAxNjM1NjQ0OTQxNDAx.fCFDeTcCw4GegbJZc6wT_8AfjD8Gnee9Z7w2IIUVAiMg.eheFyQLFsDObXlOkq3SNWLcW-OOO-n6TnMVTomDmTTEg.JPEG.chex417/%EB%A7%A4%EA%B0%9C%EB%B3%80%EC%88%98%EC%9D%98_%EB%8B%A4%ED%98%95%EC%84%B1.jpg?type=w773)

### 6.5. 강제 타입 변환(Casting)

- 구현 객체가 인터페이스 타입으로 자동변환하면, **인터페이스에 선언된 메소드만 사용 가능**하다는 제약 사항이 따른다.
- 구현 클래스에 선언된 필드와 메소드를 사용해야 할 경우 강제 타입 변환을 해서 다시 구현 클래스로 변환한 다음, 구현 클래스의 필드와 메소드를 사용할 수 있다.

![강제타입변환](https://postfiles.pstatic.net/MjAyMTEwMzFfMjU0/MDAxNjM1NjQ1ODY4NDk2.FM8-SU-976zrPFhDf3OwNQDh8d8nenKlaLSCkRvXWhkg.yUsYC2u55bJMK8BCvelqVXTw77Xn-HFMCWnH4hGvdNsg.JPEG.chex417/%EA%B0%95%EC%A0%9C%ED%83%80%EC%9E%85%EB%B3%80%ED%99%98.jpg?type=w773)

```
    public class Driver{
        public void drive(Vehicle vehicle){//매개변수에 Bus객체 or Taxi객체
            if(vehicle instanceof Bus){//vehicle 매개변수가 참조하는 객체가 Bus인지 조사
                Bus bus = (Bus) vehicle; //Bus 객체일 경우 안전하게 강제타입 변환시킴
                bus.checkFare(); //Bus타입으로 강제 타입 변환을 하는 이유
                //Vehicle인터페이스에는 checkFare()메소드가 없음
            }
            vehicle.run();
        }
    }
```

- 강제 타입 변환은 `구현 객체`가 `인터페이스 타입`으로 변환되어 있는 상태에서 가능하다.
- 그러나 어떤 구현 객체가 변환되어 있는지 알 수 없는 상태에서 무작정 변환을 할 경우 `ClassCastException`이 발생할 수도 있다.
- 강제 타입 변환 전에 `instanceof` 연산자로 변환 가능한지 검사하는 것이 좋다.

---

## 7. 인터페이스 상속

> 인터페이스도 다른 인터페이스를 **상속**할 수 잇다.

- 인터페이스는 클래스와 달리 **다중 상속**을 허용한다.

        public interface 하위인터페이스 extends 상위인터페이스1, 상위인터페이스2 {...}

- 하위 인터페이스를 **구현하는 클래스**는 하위 인터페이스의 메소드뿐만 아니라 상위 인터페이스의 **모든 추상 메소드에 대한 실체 메소드를 가지고 있어야 한다.**
- 그렇기 때문에 구현 클래스로부터 객체를 생성하고 나서 다음과 같이 하위 및 상위 인터페이스 타입으로 변환이 가능하다.

```
하위인터페이스 변수 = new 구현클래스(...);
상위인터페이스1 변수 = new 구현클래스(...);
상위인터페이스2 변수 = new 구현클래스(...);
```

![인터페이스 상속](https://postfiles.pstatic.net/MjAyMTEwMzFfNDUg/MDAxNjM1NjQ2NTk3OTA3.OCVYvXktxmRUJIps_D3iTmg3P49UPnpj--s5AYY1kC0g.m43eNkEGX7K5h8LngfCrN_ZtN0_WZfhoB6XoRfNCNnQg.JPEG.chex417/%EC%9D%B8%ED%84%B0%ED%8E%98%EC%9D%B4%EC%8A%A4_%EC%83%81%EC%86%8D.jpg?type=w773)

- 하위 인터페이스로 타입 변환되면 상하위 인터페이스에 선언된 모든 메소드를 사용할 수 있으나
- 상위 인터페이스로 타입 변환되면 상위 인터페이스에 선언된 메소드만 사용 가능하다.

```
public class Example {//호출 가능 메소드
    public static void main(String[] args){
        //ImplementationC는 하뤼 인터페이스를 구현하는 클래스
        ImplementationC imp1 = new ImplementationC();

        InterfaceA ia = imp1; //인터페이스A로 타입변환
        ia.methodA(); //InterfaceA 변수는 methodA()만 호출 가능
        System.out.println();

        InterfaceB ib = imp1; //인터페이스B로 타입변환
        ib.methodB(); //InterfaceB 변수는 methodB()만 호출 가능
        System.out.println();

        InterfaceC ic = imp1; //인터페이스C로 타입변환
        ic.methodA();
        ic.methodB();
        ic.methodC(); //InterfaceC 변수는 methodA(), methodB(), methodC() 모두 호출 가능
        System.out.println();
    }
}
```

## 8. 디폴트 메소드와 인터페이스 확장

- 디폴트 메소드는 `인터페이스`에 선언되나 `인스턴스 메소드`이기 때문에 `구현 객체`가 있어야 사용할 수 있다.

### 8.1. 디폴트 메소드의 필요성

> 인터페이스에서 디폴트 메소드를 허용한 이유는 기존 인터페이스를 확장해서 새로운 기능을 추가하기 위함이다.

![디폴트메소드의 필요성](https://postfiles.pstatic.net/MjAyMTEwMzFfMTcw/MDAxNjM1NjQ3MTQ2MjA2.0caz3PRHMtQLr-7kan8lurSwmCnXCYObvQONA88X8ckg.rzuZvs4DiimeFWufTqjo0hhbU-ekqe_73Yh6M_4GqtQg.JPEG.chex417/%EB%94%94%ED%8F%B4%ED%8A%B8_%EB%A9%94%EC%86%8C%EB%93%9C%EC%9D%98_%ED%95%84%EC%9A%94%EC%84%B1.jpg?type=w773)

- 기존 `인터페이스`의 이름과 `추상 메소드`의 변경 없이
- `디폴트 메소드`만 추가하면 `이전에 개발한 구현 클래스`를 그대로 사용할 수 있으면서
- `새롭게 개발하는 클래스`는 `디폴트 메소드`를 활용할 수 있다.

- `MyInterface`에 기능 추가를 위해 `추상메소드`를 선언하면 `MyClassA`에는 추가된 `추상메소드`에 대한 `실체메소드`가 없기 때문에 `MyClassA`에서 문제가 발생하므로 MyInterface에 `추상메소드` 대신 `디폴트메소드`를 선언한다.

### 8.2. 디폴트 메소드가 있는 인터페이스의 상속

- 부모 인터페이스에 디폴트 메소드가 정의되어 있을 경우, 자식인터페이스에서 디폴트 메소드를 활용하는 방법은 세 가지가 있다.
  - 디폴트 메소드를 단순히 상속만 받는다.
  - 디폴트 메소드를 재정의(Override)해서 실행 내용을 변경한다.
  - 디폴트 메소드를 추상 메소드로 재선언한다.

```
public interface ParentInterface {//부모인터페이스
    public void method1(); //추상메소드
    public default void method2(){/*실행문*/} //디폴트 메소드
}
```

```
public interface ChildInterface1 extends ParentInterface{//자식 인터페이스1
    public void method3(); //단순히 상속만 받음
}
```

```
public interface ChildInterface2 extends ParentInterface{//자식인터페이스2
    @Override
    public default void method2() {/*실행문*/} //디폴트 메소드 재정의
    public void method3();
}
```

```
public interface ChildInterface3 extends ParentInterface{//자식인터페이스3
    @Override
    public default void method2(); //추상 메소드로 재선언
    public void method3();
}
```

---
