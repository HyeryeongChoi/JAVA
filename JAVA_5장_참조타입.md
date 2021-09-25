# 5장 참조타입 138-180p

## 1. 데이터 타입 분류

![데이터타입](https://postfiles.pstatic.net/MjAyMTA5MTFfMTM0/MDAxNjMxMjkxMTI2Nzk4.SkHGvdXZ9WCRtfWTBIeDIdareVHLZYKolz9362IXnL4g.SO9bdGtGIDgEmMzdgFPZP-XEXW6tvS9u8pAMnMH0wIYg.JPEG.chex417/%EB%8D%B0%EC%9D%B4%ED%84%B0%ED%83%80%EC%9E%85.jpg?type=w773)

- 기본타입이란? 정수, 실수, 문자, 논리 리터럴을 저장하는 타입
- 참조타입이란? 객체의 주소를 참조하는 타입(배열, 열거, 클래스, 인터페이스 타입을 말함)

![참조변수](https://postfiles.pstatic.net/MjAyMTA5MTFfMjc2/MDAxNjMxMjkxNDIwNjM5.7-zHRwMaPJtXVynlttZoEWEU84RwZ4NnU-jGpsxa9CEg.5VnczYF9guSSbqY4VKXN4f66Q8oTsKQtaBGxc70Fzesg.JPEG.chex417/%EC%B0%B8%EC%A1%B0%EB%B3%80%EC%88%98.jpg?type=w773)

---

## 2. 메모리 사용 영역

- 프로그램을 실행하면 JVM(자바 가상 머신)을 구동하게 되는데, JVM은 OS로부터 할당받은 세개의 메모리 영역(Runtime Data Area)을 사용한다.

![메모리 사용 영역](https://postfiles.pstatic.net/MjAyMTA5MTFfMTQ0/MDAxNjMxMjkxODU2NTkx.t9fSVKXp9pcIROJywEtP2FtF59GxJnoMesvs5xeQNC4g.KVP3qParFmMRGP--FEzCBChZbxcSlTUlN84gPXI0ZwYg.JPEG.chex417/%EB%A9%94%EB%AA%A8%EB%A6%AC%EC%82%AC%EC%9A%A9%EC%98%81%EC%97%AD.jpg?type=w773)

### 2.1 메소드 영역

    - 생성 시점: JVM을 시작할 때

    - 저장 되는 것: 로딩된 클래스(~.class) 바이트 코드 내용을 분석 후 저장(런타임 상수풀, 필드, 메소드, 메소드 코드, 생성자 코드)

    - 공유 범위: 모든 스레드

### 2.2 힙 영역

    - 생성 시점: JVM을 시작할 때

    - 저장 되는 것: 객체, 배열

    - 사용하지 않는 객체는 쓰레기 수집기(Garbage Collector)가 자동으로 제거

### 2.3 JVM 스택 영역

    - 생성 시점: 스레드가 시작될 때 할당

    - 각 스레드마다 하나씩 존재

    - 메소드를 호출할 때 마다 Frame을 스택에 추가(push)

    - 메소드를 종료하면 Frame을 제거(pop)

    - Frame 안에 변수들이 생성된다.

    - 변수는 선언된 블록 안에서만 스택에 존재하고 블록을 벗어나면 스택에서 제거된다.

![스택영역과 힙영역](https://postfiles.pstatic.net/MjAyMTA5MTFfMTcg/MDAxNjMxMjkyNzgyOTE4.kx2e84MsG2BJbKc9xc34BaYt1fAXNjRR9eUgEteA9wcg.lyLGd0yaDsRsqCzmWH5d6Q5PPPfOETztypnXdD6CZBcg.JPEG.chex417/%EC%8A%A4%ED%83%9D%ED%9E%99%EC%98%81%EC%97%AD.jpg?type=w773)

- 배열변수인 scores는 스택 영역에 생성
- 실제 10, 20, 30을 갖는 배열은 힙 영역에 생성
- 배열변수 scores에는 배열의 주소값이 저장

---

## 3. 참조 변수의 ==, != 연산

![예시](https://postfiles.pstatic.net/MjAyMTA5MTFfNTcg/MDAxNjMxMjkzMDI2ODE4.5HL-w8FJeO8oZuI7--hXQbEgw_zLv41dr3CjOtW-1UQg.JZpr_KdAIFN-GAEOCr6P-CPeWRCZaFmdKu_yMX-zLsUg.JPEG.chex417/%EC%B0%B8%EC%A1%B0%EB%B3%80%EC%88%98%EC%9D%98%EC%97%B0%EC%82%B0.jpg?type=w773)

- 기본타입변수의 경우: 변수의 값이 같은지 다른지
- **참조타입변수**의 경우: 동일한 객체를 참조하는지 다른 객체를 참조하는지
  - 동일한 주소값을 가짐 == 동일한 객체를 참조함

---

## 4. null과 NullPointerException

- 참조 타입 변수는 NULL 값을 가질 수 있다.(힙영역의 객체를 참조하지 않는 다는 뜻)
- **NullPointerException**? null값을 가지고 있는 참조 타입 변수를 사용했을 경우 발생한다.

---

## 5. String 타입

- 사실 문자열을 String 변수에 저장한다는 말은 틀린 표현이다.
- 문자열이 직접 변수에 저장되는 것이 아니라, **문자열은 String 객체로 생성되고 변수는 String 객체를 참조한다.**

  ![예제](https://postfiles.pstatic.net/MjAyMTA5MTFfMjQy/MDAxNjMxMjkzNzkyMDQ1.D3mNEWo-pN1YuZEjIusT4fciXyhyKgLicosAN_D4K20g.xeXbGbBhsRFXCZPk_4ovxt3CuPJJIj7JyisemAZGUWsg.JPEG.chex417/String_%ED%83%80%EC%9E%85.jpg?type=w773)

  - name 변수와 hobby 변수는 스택영역에 생성
  - 문자열 리터럴인 "신용권"과 "자바"는 힙 영역에 String 객체로 생성
  - name 변수와 hobby 변수에는 String 객체의 주소값이 저장

- 자바는 문자열 리터럴이 동일하다면 String 객체를 공유한다.
  ![예시](https://postfiles.pstatic.net/MjAyMTA5MTFfOCAg/MDAxNjMxMjk0MDg1NjUx.uo3NbSyB0w6DgE_yLHbAo8JbXpvXZ2mQJN5HWDGhwM4g.VG5ewPN53V-uMETYmLwhWFzAY_qGIR-ucEqsqmDbzq8g.JPEG.chex417/String%EA%B0%9D%EC%B2%B4%EA%B3%B5%EC%9C%A0.jpg?type=w773) - name1과 name2 변수가 동일한 문자열 리터럴인 "신용권"을 참조할 경우 동일한 String 객체를 참조하게 된다.

- 일반적으로 변수에 문자열을 저장할 경우에는 위와 같이 문자열 리터럴을 사용하지만, **new 연산자**를 사용해서 String 객체를 생성할 수 있다.
  ![new연산자로 String 객체 생성](https://postfiles.pstatic.net/MjAyMTA5MTFfMTEg/MDAxNjMxMjk0NDUyNDcz.pbnEOFJXBbYCfBe5WoMSKEYPhlN-o0LHRw4-2OCWTaIg.pkGcHMmY2X5y5CBDwzAEgmpCnwE1ma8V2rxZDE4aRHQg.JPEG.chex417/new%EC%97%B0%EC%82%B0%EC%9E%90.jpg?type=w773)

- **문자열 리터럴**로 생성하느냐 VS **new 연산자**로 생성하느냐에 따라 비교 연산자의 결과가 달라질 수 있다.

  ```
  String name1 = "강동원";
  String name1 = "강동원";
  String name3 = new String("강동원");

  name1 == name2 // true
  name1 == name3 // false

  boolean result = name1.equals(name3); // true
  ```

  동일한 String 객체이건 다른 String 객체이건 상관없이 **문자열만을** 비교할 대에는 String 객체의 **equals()** 메소드를 사용해야 한다.

---

## 6. 배열 타입

- 각 데이터에 인덱스(index)를 부여해 놓은 자료구조
- 배열도 객체이므로 힙 영역에 생성된다.
- 배열 변수는 참조 변수에 속하며 힙 영역의 배열 객체를 참조한다.
- 주의: **배열 변수를 이미 선언한 후에** 다른 실행문에서 중괄호를 사용한 배열 생성은 허용되지 않는다.
- 배열 변수를 미리 선언한 후, 값 목록들이 나중에 결정되는 상황이라면 다음과 같이 **new 연산자**를 사용해서 값 목록을 저장해주면 된다.

  ```
  Stirng[] names = null;
  names = new String[] {"강아지", "고양이", "다람쥐"};
  ```

  메소드의 매개값이 배열일 경우에도 마찬가지이다.

  매개 변수로 int[] 배열이 **선언된** add()메소드가 있을 경우,
  배열을 생성함과 동시에 add() 메소드의 매개값으로 사용하고자 할 때는 반드시 **new연산자**를 사용해야 한다.

  ```
  int add(int[] scores){ ... }

  int result add( {95, 85, 90} ); // 컴파일 에러
  int result add( new int[] {95, 85, 90} );
  ```

- 데이터 타입별 **배열의 초기값**
  ![배열의 초기값](https://postfiles.pstatic.net/MjAyMTA5MTFfMjIy/MDAxNjMxMjk1ODgyNTQy.8oODkLqFMHRMyVm-b_O4R3-7Dj-lDX2WvWSfeZEjdLsg.MN2BcSDtjOUMyBQ_cC0vSgyiMb0dBkHTX5ImBL8HrTog.JPEG.chex417/%EB%B0%B0%EC%97%B4%EC%9D%98_%EC%B4%88%EA%B8%B0%EA%B0%92.jpg?type=w773)

- **다차원 배열**

  - 자바는 일차원 배열이 서로 연결된 구조로 다차원 배열을 구현하기 때문에 수학 행렬 구조가 아닌 **계단식 구조**를 가진다.
    ![다차원배열](https://postfiles.pstatic.net/MjAyMTA5MTFfMTE2/MDAxNjMxMjk2MTQyMzI4.JrylcxOj3aPhD3E-s3yfnD4hCdSWYDe6b238cU3Q2_8g.06KgquPoSIdP7XNQ1MvKHa4b2b8FJEjbIcFOHRg8I7Qg.JPEG.chex417/%EB%8B%A4%EC%B0%A8%EC%9B%90%EB%B0%B0%EC%97%B4.jpg?type=w773)
    scores는 길이 2인 배열A를 참조한다.

    배열A의 scores[0]은 다시 길이2인 배열B를 참조한다.

    배열A의 scores[1]은 다시 길이3인 배열C를 참조한다.

    scores[0]과 scores[1]은 모두 **배열을 참조하는 변수** 역할을 한다.

- **객체를 참조하는 배열**

  기본 타입(int, char, long 등) 배열은 각 항목에 직접 값을 갖고 있지만, **참조 타입(클래스, 인터페이스) 배열**은 각 항목에 **객체의 주소**를 갖고 있다.

  ```
  String[] strArr = new String[3];
  StrArr[0] = "Java";
  strArr[1] = "C++";
  strArr[2] = "C#";
  ```

  String은 클래스 타입으로 String[] 배열은 각 항목에 문자열이 아니라 **String 객체의 주소**를 가진다.

- **배열 복사**

  ```
  String[] oldStrArr = {"java", "array", "copy"};
  Stirng[] newStrArr = new String[5];

  System.arraycopy( oldStrArr, 0, newStrArr, 0, oldStrArr.length ); // 원본배열, 복사할 시작 인덱스, 새 배열, 붙여넣을 시작 인덱스, 복사할 개수
  ```

  ![얕은복사](https://postfiles.pstatic.net/MjAyMTA5MTFfMjMz/MDAxNjMxMjk2OTYyNjMx.H9KJx4m2f4Ivt2g2QUMZ72ZRqYHAnSa2S2tfWPfjeaIg.DQ8WK52nRMoclhveUotdyNh-oTyxItIpKn7LByoV2zwg.JPEG.chex417/%EC%96%95%EC%9D%80%EB%B3%B5%EC%82%AC.jpg?type=w773)
  객체를 참조하는 배열인 경우, 배열 복사가 되면 복사되는 것이 객체의 주소이므로 새 배열의 항목은 이전 배열의 항목이 참조하는 객체와 동일하다.
  이것을 `얕은 복사(shallow copy)`라고 한다.

  반대로 `깊은 복사(deep copy)`는 참조하는 객체도 별도로 생성하는 것을 말한다.

- **향상된 for문**

  ```
  int scores[] = {95, 71, 84, 93, 87};
  int sum = 0;
  for (int score : scores){
      sum = sum + score;
  }
  System.out.println("총합 = " + sum);
  ```

  for문이 처음 실행될 때

  ① 배열(scores)에서 가져올 첫 번째 값이 존재하는지 봄

  ② 가져올 값이 존재하면 해당 값을 score변수에 저장

  ③ 실행문을 실행

  socres 배열에서 가져올 다음 항목이 없으면 for문이 종료된다.
  따라서 for문의 반복 횟수는 배열의 항목 수가 된다.

---

## 7. 열거 타입

- **열거 타입**이란 한정된 값만을 갖는 데이터 타입
- ex. 요일(월~일) 또는 계절(봄, 여름, 가을, 겨울) 등에 대한 데이터
- 열거 타입은 몇 개의 **열거 상수**(enumeration constant) 중에서 하나의 상수를 저장하는 데이터 타입

- 선언하기: 열거 타입의 이름을 정하고 그 이름으로 소스파일(.java)을 생성해야 한다.
  ![열거타입](https://postfiles.pstatic.net/MjAyMTA5MTFfNjcg/MDAxNjMxMjk3NjgzNTkw.VXBruPj-doW9e1JJ1fHbFuvJMvSkdpeSdT9UopwJVZgg.cfQJRNAIkzC1h0JtNGTez0K37rnb76LpNHsbwaXbs54g.JPEG.chex417/%EC%97%B4%EA%B1%B0%ED%83%80%EC%9E%85.jpg?type=w773)

  - 열거 타입 이름은 단어 첫 문자는 대문자, 나머지는 소문자
  - MemberGrade.java 또는 ProductKind.java
  - 열거 상수는 모두 대문자
  - 열거 상수가 여러 단어일 경우 사이를 밑줄(\_)로 연결
  - 예를 들어, LOGIN_SUCCESS 또는 LOGIN_FAILED

  ```
  Week today = Week.SUNDAY; // today열거변수에 열거상수인 SUNDAY를 저장
  Week birthday = null; // 열거타입도 참조타입이므로 null값 가능
  ```

  ![열거상수](https://postfiles.pstatic.net/MjAyMTA5MTFfMTg2/MDAxNjMxMjk4NDIwNzM5.jimijlvqYqC4Xza6du5_nJgSCPpHsmfFxjO0TMPJrwIg.6eEdcnGpqjBge330sGL4gSkXSwRoUwd9r8k_PaqgGA0g.JPEG.chex417/%EC%97%B4%EA%B1%B0%EC%83%81%EC%88%98.jpg?type=w773)

  - 열거 타입 Week의 경우 MONDAY부터 SUNDAY까지의 열거 상수는 총 7개의 Week 객체로 생성된다.
  - `메소드 영역`에 생성된 열거 상수가 해당 week 객체를 각각 참조하게 된다.

- 예제로 이해하기

```
Week today = Week.SUNDAY;

today == Week.SUNDAY // true
```

![예제](https://postfiles.pstatic.net/MjAyMTA5MTFfMjY1/MDAxNjMxMjk4NjU0MjY3.y9bQXAC-xd1uXYUKyIeXyzc2Ym0Fq-HI02TsGSlCDWwg.ZNMHkysVUJFU7FeEyEMXb3oj9wkkTxjuD1ID3r0L1Bog.JPEG.chex417/%EC%97%B4%EA%B1%B0.jpg?type=w773)

    - 열거타입 변수 today는 스택 영역에 생성
    - today에 저장되는 값은 Week.SUNDAY 열거 상수가 참조하는 객체의 주소
    - 즉, 열거상수 Week.SUNDAY와 today 변수는 서로 같은 Week객체를 참조하게 된다.

- **열거 객체의 메소드**

  - 열거 객체는 열거 상수의 문자열을 내부 데이터로 가짐
    ![열거객체의 메소드](https://postfiles.pstatic.net/MjAyMTA5MTFfMjU3/MDAxNjMxMjk5MDc4OTYw.ZKYI98k-R7W4BWjVt7NxKU--cDu6-nz4V9Fu9l-TYacg.cjN09TlHiteE82ZGfBFfgD5ujTVXLU533TJtKiLElhYg.JPEG.chex417/%EC%97%B4%EA%B1%B0%EA%B0%9D%EC%B2%B4%EC%9D%98_%EB%A9%94%EC%86%8C%EB%93%9C.jpg?type=w773)

    ```
    Week today = Week.SUNDAY;
    String name = today.neme(); // SUNDAY
    int ordinal = today.ordinal(); // 6

    Week day1 = Week.MONDAY;
    Week day2 = Week.WEDNESDAY;
    int result1 = day1.compareTo(day2); // -2 (day2기준)
    int result2 = day2.compareTo(day1); //  2 (day1기준)

    Week weekDay = Week.valueOf("SATURDAY"); // weekDay변수는 Week.SATUREDAY 열거 객체를 참조하게 된다.

    Week[] days = Week.values(); // 모든 열거 객체들을 배열로 만들어 리턴한다.
    for(Week day : days){
        System.out.println(day); // MONDAY ~ SUNDAY
    }
    ```
