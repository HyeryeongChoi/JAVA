# 15장 컬렉션 프레임워크 722-773p

## 1. 컬렉션 프레임워크 소개

- 다수의 객체를 어떻게 효율적으로 검색, 삽입, 삭제할까?

- 가장 간단한 방법은 배열을 이용하는 것 But 배열의 크기는 생성할 때 결정되기 때문에 불특정 다수의 객체를 저장하기에는 문제가 있다.

- 자바는 배열의 이러한 문제점을 해결하고 널리 알려져있는 자료구조를 바탕으로 객체를 효율적으로 사용(검색, 삽입, 삭제)할 수 있도록 `java.util`패키지에 컬렉션과 관련된 `인터페이스`와 `클래스`를 포함시켜 놓았다.

- 이를 총칭해서 **컬렉션 프레임워크**라고 부른다.

- 자바 **컬렉션**은 객체를 수집해서 저장하는 역할을 한다.

- **프레임워크**란 사용 방법을 미리 정해 놓은 라이브러리를 말한다.

---

## 2. 컬렉션 프레임워크 상세

![컬렉션프레임워크](https://postfiles.pstatic.net/MjAyMTExMTRfMjUy/MDAxNjM2ODk2NDI3MzYw.yYAOw94C6j0PYw_ndQefX5vpyx_TyLyH5_IKurnBpiQg.qQJstN2ZyOM0sBTAiysu-e70rX9iqKH5Rjk4XxUuOhsg.JPEG.chex417/%EC%BB%AC%EB%A0%89%EC%85%98_%ED%94%84%EB%A0%88%EC%9E%84%EC%9B%8C%ED%81%AC.jpg?type=w773)

- **주요 인터페이스**: `List`, `Set`, `Map`

- 즉, `HashSet`, `TreeSet`은 `Set`**인터페이스**를 **구현한 클래스**로 `Set`**인터페이스**로 사용 가능한 **컬렉션**이다.

![인터페이스별 사용할 수 있는 컬렉션의 특징](https://postfiles.pstatic.net/MjAyMTExMTRfOTAg/MDAxNjM2ODk2OTc1MjEy.ThWGuDr5h3qwK-jTIxbexnxt7d5REgW4GZCdGtpo7xcg.aUbnbUYikukofKhe8TMTIjjaS85ssEOUIkyM_lReZ-Qg.JPEG.chex417/%EC%9D%B8%ED%84%B0%ED%8E%98%EC%9D%B4%EC%8A%A4%EB%B3%84_%EC%82%AC%EC%9A%A9%ED%95%A0_%EC%88%98_%EC%9E%88%EB%8A%94_%EC%BB%AC%EB%A0%89%EC%85%98%EC%9D%98_%ED%8A%B9%EC%A7%95.jpg?type=w773)

## 3. List 컬렉션

![List컬렉션](https://postfiles.pstatic.net/MjAyMTExMTRfNTMg/MDAxNjM2ODk3MzkzODA0.Zh4haOmxKiq5swXf_8quZ4iHTMUxtAeuRV_ESel1r90g.Q2WIX9W9dTYVHHTp6UPzXPr7k5a5VrlbiC9UvNI6yBsg.JPEG.chex417/List%EC%BB%AC%EB%A0%89%EC%85%98.jpg?type=w773)

- 객체를 일렬로 늘어놓은 구조로 **인덱스**로 관리한다.
- 객체 자체를 저장하는 것이 아니라 **객체의 번지**를 참조한다.
- **중복 저장**이 가능하며 이 경우 **동일한 번지**가 참조된다.
- `null`도 저장 가능하며 이 경우 해당 인덱스는 객체를 참조하지 않는다.

![List인터페이스의 메소드](https://postfiles.pstatic.net/MjAyMTExMTRfMTcx/MDAxNjM2ODk3NDA0MzU5.kr0pcuxJ3cbSFfEk_invi8iW4rTECDpSFj8FKSm1kWcg.8TyQVFN22H_YPUvlKOVtG-k9INKb0HM4h29nPsH9vf8g.JPEG.chex417/List%EC%9D%B8%ED%84%B0%ED%8E%98%EC%9D%B4%EC%8A%A4%EC%9D%98_%EB%A9%94%EC%86%8C%EB%93%9C.jpg?type=w773)

- **List인터페이스**가 **제네릭 타입**이기 때문에 메소드의 매개변수 타입과 리턴 타입에 E라는 타입 파라미터가 있다.(구체적인 타입은 **구현 객체를 생성할 때** 결정된다.)

### 3.1. ArrayList

- `List<E> list = new ArrayList<E>();` -> `ArrayList` 생성
- List인터페이스의 구현 클래스
- **일반 배열과의 차이?**
  - 배열은 생성할 때 크기가 고정되고 사용 중에 크기를 변경할 수 없지만, `ArrayList`는 저장 용량을 초과한 객체들이 들어오면 **자동적으로 저장 용량이 늘어난다.**
  - 기본생성자로 `ArrayList` 객체를 생성하면 내부에 10개의 객체를 저장할 수 있는 초기 용량을 가지게 되나 처음부터 용량을 크게 잡고 싶다면 용량의 크기를 매개값으로 받는 생성자를 이용하면 된다.
    ```
    //String 객체 30개를 저장할 수 있는 용량을 가짐
    List<String> list = new ArrayList<String>(30);
    ```
- **객체 삽입 및 삭제**
  ![4번 인덱스 제거 시](https://postfiles.pstatic.net/MjAyMTExMTRfODYg/MDAxNjM2ODk4NDc0NTA0.Ii7GeHdsy_ZhF416p06URx0ajqTpnu4BFoZeeMRUPN0g.SQYsRyD7zUR7VWmsibyg2cE256ZcafhbmVchQ3DsfHog.JPEG.chex417/ArrayList%EC%82%BD%EC%9E%85%EC%82%AD%EC%A0%9C.jpg?type=w773)
  - `ArrayList`에 객체를 추가하면 인덱스 0부터 차례대로 저장된다.
  - `ArrayList`에 특정 인덱스의 객체를 **삭제**하면 **바로 뒤 인덱스부터 마지막 인덱스까지 모두 앞으로 1씩 당겨진다.**
  - 마찬가지로 특정 인덱스에 객체를 **삽입**하면 **해당 인덱스부터 마지막 인덱스까지 모두 1씩 밀려난다.**
  - 빈번한 객체 삭제와 삽입이 일어나는 곳에서는 `LinkedList`를 사용하는 것이 좋다.
  - 그러나 **인덱스 검색**이나 맨 **마지막**에 객체를 삽입하는 경우에는 `ArrayList`가 더 좋은 성능을 발휘한다.

### 3.2. Vector

- `List<E> list = new Vector<E>();` -> Vector 생성
- `ArrayList`와 동일한 내부 구조를 가지고 있다.
- `ArrayList`와 다른 점?
  ![Vector는 스레드가 안전하다(Thread Safe)](https://postfiles.pstatic.net/MjAyMTExMTRfMTM1/MDAxNjM2ODk5NDE1NDUy.iFL5SBM-Mrjfc678mFbZGdw1vJm8BkpSJUerVu-lds0g.NLflPQUg-pjGr140Ga2xJnJoBfYxP758zin0Km01a-Mg.JPEG.chex417/Vector%EB%8A%94_%EC%8A%A4%EB%A0%88%EB%93%9Csafe.jpg?type=w773)
  - `Vector`는 동기화(synchronized)된 메소드로 구성되어 있기 때문에 멀티스레드가 **동시에** 이 메소드들을 **실행할 수 없고**, 하나의 스레드가 실행을 완료해야만 다른 스레드를 실행할 수 있다.
  - 그래서 멀티스레드 환경에서 안전하게 객체를 삽입, 삭제할 수 있다.
  - 이것을 **스레드가 안전(Thread Safe)하다**라고 말한다.
- `Vector`의 **객체 삽입 및 삭제**: `ArrayList`처럼 인덱스가 당겨지거나 밀려난다.

### 3.3. LinkedList

![LinkedList의 내부구조](https://postfiles.pstatic.net/MjAyMTExMTRfMTE5/MDAxNjM2ODk5NDM4MzE1.8vtWBOPA6sBJ34_rNouLu8V82SF39IOBsoeG-wDd6Q0g._eDrWWPqgDkeYPKGfbZ-IxXmQl0G4pkbmTaJm5pZZ4Mg.JPEG.chex417/LinkedList_%EB%82%B4%EB%B6%80%EA%B5%AC%EC%A1%B0.jpg?type=w773)

- `List<E> list = new LinkedList<E>();` -> `LinkedList`생성
- `List`의 구현 클래스이므로 `ArrayList`와 **사용 방법**은 똑같지만 **내부 구조**는 완전 다르다.
- `ArrayList`는 내부 배열에 객체를 저장해서 인덱스로 관리하지만
- `LinkedList`는 인접 참조를 링크해서 체인처럼 관리한다.(인접한 리스트를 연결)
- **객체의 삽입 및 삭제**
  - 특정 인덱스의 객체를 삽입하거나 삭제하면 **앞뒤 링크만 변경**되고 나머지 링크는 변경되지 않는다.
  - **끝에서부터(순차적으로) 삽입/삭제하는 경우**는 `ArrayList`가 빠르지만
  - **중간에 삽입/삭제하는 경우**는 앞뒤 링크 정보만 변경하면 되는 `LinkedList`가 더 빠르다.
  - `ArrayList`는 뒤쪽 **인덱스들을 모두 1씩 증가 또는 감소시키는 시간이 필요하므로** 처리 속도가 느리다.

---

## 4. Set 컬렉션

![Set 컬렉션](https://postfiles.pstatic.net/MjAyMTExMTVfMjUw/MDAxNjM2OTg0OTYzNDg5.yoXN6Xq3sF1vD8JQSq6b0jSDA7tPyoEHGvqLWywVyPsg.PGeUdaHy_NotGkFi5kSmeoavpS2cFkn-0PALFiMX1SEg.JPEG.chex417/Set%EC%BB%AC%EB%A0%89%EC%85%98.jpg?type=w773)

- `Set컬렉션`은 **저장 순서가 유지되지 않는다.**(저장할 때의 순서 != 찾을 때의 순서)
- 또한 객체를 **중복해서 저장할 수 없다.**(중복 허용X)
- **하나의** `null`만 저장할 수 있다.
- Set컬렉션에는 `HashSet`, `LinkedHashSet`, `TreeSet` 등이 있다.
- **Set인터페이스의 메소드**
  ![Set인터페이스의 메소드들](https://postfiles.pstatic.net/MjAyMTExMTVfMjc2/MDAxNjM2OTg0OTc2NTM0.SFXc8M8sC1enjd8X2ZQPz7O8OgnnQdAzmyn5R54Nomwg.NpaBo7XV71Hq5LX7NV5-vhJ2QFnEo8gzhrX_o1uXt6Ig.JPEG.chex417/Set%EC%9D%B8%ED%84%B0%ED%8E%98%EC%9D%B4%EC%8A%A4%EC%9D%98_%EB%A9%94%EC%86%8C%EB%93%9C.jpg?type=w773)
- Set 컬렉션은 인덱스로 객체를 검색해서 가져오는 메소드가 없다.
- 대신 전체 객체를 대상으로 한번씩 반복해서 가져오는 반복자(**Iterator**)를 제공한다.
- 반복자는 `Interator` 인터페이스를 구현한 객체를 말하는데, `iterator()`메소드를 호출하면 얻을 수 있다.
  ```
  Set<String> set = ...;
  Iterator<String> iterator = set.iterator();
  ```
- **Iterator 인터페이스에 선언된 메소드들**
  ![Iterator 인터페이스에 선언된 메소드들](https://postfiles.pstatic.net/MjAyMTExMTVfMjQx/MDAxNjM2OTg1NDM5MDkx.jl5QwJ4ZWPQB7zRq3DXJ-mkod-J-hhjLjWknZaWXV_sg.6v7lsP4C9_oexnGZBwfMI_3J9nQ8M2SH8Drt8-ce6Lcg.JPEG.chex417/Iterator%EC%9D%B8%ED%84%B0%ED%8E%98%EC%9D%B4%EC%8A%A4%EC%97%90_%EC%84%A0%EC%96%B8%EB%90%9C_%EB%A9%94%EC%86%8C%EB%93%9C%EB%93%A4.jpg?type=w773)

  ```
  //Set 컬렉션에서 String 객체들을 반복해서 하나씩 가져오는 코드
  Set<String> set = ...;
  Iterator<String> iterator = set.iterator();
  while(iterator.hasNext()){
    //String 객체 하나를 가져옴
    String str = iterator.next();
  }
  ```

  ```
  //Iterator를 사용하지 않더라도 향상된 for문을 이용해서 전체 객체를 대상으로 반복가능
  Set<String> set = ...;
  for(String str : set){
      //저장된 객체 수만큼 루핑한다.
  }
  ```

- Set컬렉션에서 `Iterator`의 `next()`메소드로 가져온 객체를 제거하고 싶다면 `remove()`메소드를 호출하면 된다.
- `Iterator`의 메소드이지만, **실제 `Set`컬렉션에서 객체가 제거됨**을 알아야 한다.
  ```
  while(iterator.hasNext()){
      String str = iterator.next();
      if(str.equals("홍길동")){
          iterator.remove();
      }
  }
  ```

### 4.1. HashSet

- `HashSet`은 `Set`인터페이스의 구현 클래스이다.
- `Set<E> set = new HashSet<E>();` -> `HashSet` 생성
- 객체를 순서 없이 저장하고 동일한 객체는 중복 저장하지 않는다.
  - `HashSet`이 판단하는 **동일한 객체**란 꼭 같은 인스턴스를 뜻하지는 않는다.
  - `HashSet`은 객체를 저장하기 전에 먼저 객체의 `hashCode()` 메소드를 호출해서 해시코드를 얻어낸다.
  - 그리고 이미 저장되어 있는 객체들의 해시코드와 비교한다.
  - 만약 동일한 해시코드가 있다면 다시 `equals()`메소드로 두 객체를 비교해서 `true`가 나오면 **동일한 객체로 판단**하고 중복 저장을 하지 않는다.
    ![HashSet이 동일한 객체인지 판단하는 과정(중복저장을 피하기 위함)](https://postfiles.pstatic.net/MjAyMTExMTVfMjYw/MDAxNjM2OTg2MTQ3NDE2.iCcEORybKzsj_Ci2XbWRIIKNafhrmrKmhfIyw5uM19Yg.8XZ5BqK2yAsIS-GuWamerserLwgOB1xl6ClKlvb8O-Yg.JPEG.chex417/HashSet_%EB%8F%99%EC%9D%BC%ED%95%9C_%EA%B0%9D%EC%B2%B4%EC%9D%B8%EC%A7%80_%ED%8C%90%EB%8B%A8%ED%95%98%EB%8A%94_%EA%B3%BC%EC%A0%95.jpg?type=w773)
- **문자열**을 `HashSet`에 저장할 경우, 같은 문자열을 갖는 `String`객체는 동등한 객체로 간주되고 다른 문자열을 갖는 `String`객체는 다른 객체로 간주되는데, 그 이유는 `String` 클래스가 `hashCode()`와 `equals()`메소드를 재정의해서 같은 문자열일 경우 `hashCode()`의 리턴값을 같게, `equals()`의 리턴값은 `true`가 나오도록 했기 때문이다.
- **인스턴스가 달라도 이름과 나이가 동일하다면 동일한 객체로 간주하여 중복 저장되지 않도록 하는 예제코드**

  ```
  public class Member {//hashCode()와 equals()메소드 재정의
    public String name;
    public int age;

    public Member(String name, int age){
        this.name = name;
        this.age = age;
    }

    @Override
    public boolean equals(Object obj){//name과 age값이 같으면 true를 리턴
        if(obj instanceof Member){
            Member member = (Member)obj;
            return member.name.equals(name) && (member.age==age);
        }else{
            return false;
        }
    }

    @Override
    public int hashCode(){//name과 age 값이 같으면 동일한 hashCode가 리턴
        return name.hashCode()+age;
    }
  }
  ```

  ```
  import java.util.HashSet;
  import java.util.Set;

  public class HashSetExample2 {
    public static void main(String[] args) {
        Set<Member> set = new HashSet<Member>();

        //인스턴스는 다르지만 내부 데이터가 동일하므로 객체 1개만 저장
        set.add(new Member("홍길동", 30));
        set.add(new Member("홍길동", 30));

        System.out.println("총 객체수: "+set.size()); //저장된 객체 수 얻기 -> 1개
    }
  }
  ```

## 5. Map 컬렉션

![Map 컬렉션](https://postfiles.pstatic.net/MjAyMTExMTZfMzUg/MDAxNjM3MDcwNTc2MzUw.CL4SID_8Epxfi6CkVm7VX2szGV3ZUz2iMn2ES5rhtXUg.WAM8bBSTPtHHLYiCMz51BG8vDnSqak_3f_FbO3fK7ukg.JPEG.chex417/Map%EC%BB%AC%EB%A0%89%EC%85%98.jpg?type=w773)

- **키(Key)와 값(value)으로 구성된 `Entry`객체를 저장하는 구조**를 가지고 있다.
- 키와 값은 모두 객체이다.
- **키는 중복 저장될 수 없지만** 값은 중복 저장될 수 있다.
- 만약 기존에 저장된 키와 **동일한 키로 값을 저장하면** 기존 값은 없어지고 새로운 값으로 대치된다.
- `Map`컬렉션에는 `HashMap`, `Hashtable`, `LinkedHashMap`, `Properties`, `TreeMap` 등이 있다.

![Map 인터페이스의 메소드](https://postfiles.pstatic.net/MjAyMTExMTZfNTUg/MDAxNjM3MDcwNTkzOTc3.rrixEn5M_n7HwXJPyRet0rKaWEBGDBnNFvoBDVqnBI4g.1NK2TL0y6mm4vdVpYYeCuMkqBK_5Pwzum344U9GRQvgg.JPEG.chex417/Map_%EC%9D%B8%ED%84%B0%ED%8E%98%EC%9D%B4%EC%8A%A4%EC%9D%98_%EB%A9%94%EC%86%8C%EB%93%9C%EB%93%A41.jpg?type=w773)
![Map 인터페이스의 메소드](https://postfiles.pstatic.net/MjAyMTExMTZfMjYg/MDAxNjM3MDcwNTkyODcy.okrcag2FDLHOWrww4vzyjl5x_CAAU_qUY2dI3WJdi9Qg.Jj8fZsWX0fStCqnGvnblKa683F9pQxuaMCxJWZo6L1sg.JPEG.chex417/Map_%EC%9D%B8%ED%84%B0%ED%8E%98%EC%9D%B4%EC%8A%A4%EC%9D%98_%EB%A9%94%EC%86%8C%EB%93%9C%EB%93%A42.jpg?type=w773)

- 키를 알고싶다면 `get()`메소드로 간단하게 객체를 찾아오면 되지만,
- 저장된 전체 객체를 대상으로 하나씩 얻고 싶을 경우에는 두 가지 방법을 사용할 수 있다.
  - `KeySet()`메소드로 모든 키를 `Set`컬렉션으로 얻은 다음 반복자를 통해 키를 하나씩 얻고 `get()`메소드를 통해 값을 얻으면 된다.
  ```
  Map<K, V> map = ~;
  Set<K> KeySet = map.KeySet();
  Iterator<K> keyIterator = keySet.iterator();
  while(keyIterator.hasNext()){
      K key = keyIterator.next();
      V value = mpa.get(key);
  }
  ```
  - `entrySet()`메소드로 모든 `Map.Entry`를 `Set`컬렉션으로 얻은 다음 반복자를 통해 `Map.Entry`를 하나씩 얻고 `getKey()`와 `getValue()`메소드를 이용해 키와 값을 얻으면 된다.
  ```
  Set<Map.Entry<K, V>> entrySet = map.entrySet();
  Iterator<Map.Entry<K, V>> entryIterator = entrySet.iterator();
  while(entryIterator,hasNext()){
      Map.Entry<K, V> entry = entryIterator.next();
      K key = entry.getKey();
      V value = entry.getValue();
  }
  ```

### 5.1. HashMap

- `HashMap`은 `Map`인터페이스를 구현한 대표적인 `Map`컬렉션이다.
- `Map<K, V> map = new HashMap<K, V>();` -> `HashMap` 생성

  ![동일한 객체(=동일한 키)인지 판단하는 과정](<https://postfiles.pstatic.net/MjAyMTExMTdfNiAg/MDAxNjM3MTYwMDI4NTA0.KLIWshe_EItizSeJolQXAw87Cx18qGZ5BNHVHrgzYqcg.xpJ7jSX-IDc2KUNBc4vlFJ2Gx81jRAIbeL6pS99xMgMg.JPEG.chex417/HashMap%EB%8F%99%EC%9D%BC%ED%95%9C_%EA%B0%9D%EC%B2%B4(=%EB%8F%99%EC%9D%BC%ED%95%9C_%ED%82%A4)%EC%9D%B8%EC%A7%80_%ED%8C%90%EB%8B%A8%ED%95%98%EB%8A%94_%EA%B3%BC%EC%A0%95.jpg?type=w773>)

- `HashMap`의 키로 사용할 객체는 `hashCode()`와 `equals()`메소드를 재정의해서 동등 객체가 될 조건을 정해야 한다.
- 동등 객체, 즉 **동일한 키가 될 조건**은 `hashCode()`의 리턴값이 같아야 하고, `equals()`메소드가 `true`를 리턴해야 한다.
- 주로 키 타입은 `String`을 많이 사용하는데, `String`은 문자열이 같을 경우 동등 객체가 될 수 있도록 `hashCode()`와 `equals()`메소드가 **재정의**되어 있다.
- 키와 값의 타입은 기본 타입(`byte`, `short`, `int`, `float`, `double`, `boolean`, `char`)을 사용할 수 없고 `class` 및 `interface` 타입만 가능하다.

- 이름을 키로, 점수를 값으로 저장하는 `HashMap` 사용 방법

  ```
  import java.util.HashMap;
  import java.util.Iterator;
  import java.util.Map;
  import java.util.Set;

  public class HashMapExample1 {
      public static void main(String[] args) {
          //Map 컬렉션 생성
          Map<String, Integer> map = new HashMap<String, Integer>();

          //객체 저장
          map.put("신용권", 85);
          map.put("홍길동", 90);
          map.put("동장군", 80);
          map.put("홍길동", 95); // "홍길동"이라는 키가 같기 때문에 제일 마지막에 저장한 값으로 대치
          System.out.println("총 Entry 수: "+map.size()); //저장된 총 Entry 수 얻기

          //객체 찾기
          System.out.println("\t홍길동: "+map.get("홍길동"));// 이름(키)으로 점수(값)를 검색
          System.out.println();

          //객체를 하나씩 처리
          Set<String> keySet = map.keySet(); //KeySet 얻기
          Iterator<String> keyIterator = keySet.iterator();
          while(keyIterator.hasNext()){
              String key = keyIterator.next();
              Integer value = map.get(key);
              System.out.println("\t"+key+": "+value);
          }
          System.out.println();

          //객체 삭제
          map.remove("홍길동");
          System.out.println("총 Entry 수: "+map.size());

          //객체를 하나씩 처리
          Set<Map.Entry<String,Integer>> entrySet = map.entrySet(); //Map.EntrySet얻기
          Iterator<Map.Entry<String, Integer>> entryIterator = entrySet.iterator();

          while(entryIterator.hasNext()){
              Map.Entry<String, Integer> entry = entryIterator.next();
              String key = entry.getKey();
              Integer value = entry.getValue();
              System.out.println("\t"+key+": "+value);
          }
          System.out.println();

          //객체 전체 삭제
          map.clear();
          System.out.println("총 Entry 수: "+map.size());
      }
  }
  ```

- `Studnet`객체를 키로하고 점수를 저장하는 `HashMap` 사용 방법

  ```
  public class Student {//키로 사용할 객체 - hashCode()와 equals() 재정의
      public int sno;
      public String name;

      public Student(int sno, String name){
          this.sno = sno;
          this.name = name;
      }

      public boolean equals(Object obj){ //학번과 이름이 동일할 경우 true 리턴
          if(obj instanceof Student){
              Student student = (Student) obj;
              return (sno== student.sno) && (name.equals(student.name));
          } else{
              return false;
          }
      }

      public int hashCode(){//학번과 이름이 같다면 동일한 값을 리턴
          return sno + name.hashCode();
      }
  }
  ```

  ```
  import java.util.HashMap;
  import java.util.Map;

  public class HashMapExample2 {//학번과 이름이 동일한 경우 같은 키로 인식
      public static void main(String[] args) {
          Map<Student, Integer> map = new HashMap<Student, Integer>();

          //학번과 이름이 똑같은 Student를 키로 저장
          map.put(new Student(1, "홍길동"), 95);
          map.put(new Student(1, "홍길동"), 95);

          System.out.println("총 Entry 수: "+map.size());
      }
  }
  ```

### 5.2. Hashtable

- `Hashtable`은 `HashMap`과 동일한 내부 구조를 가지고 있다.
- `Hashtable`도 키로 사용할 객체는 `hashCode()`와 `equals()`메소드를 재정의해서 동등 객체가 될 조건을 정해야 한다.
- `HashMap`과의 차이점은 `Hashtable`은 동기화된 메소드로 구성되어 있기 때문에 멀티 스레드가 동시에 이 메소드들을 실행할 수는 없고, 하나의 스레드가 실행을 완료해야만 다른 스레드를 실행할 수 있다.
- 그래서 멀티 스레드 환경에서 안전하게 객체를 추가, 삭제할 수 있다.
- 이것을 **스레드가 안전(thread safe)하다**고 말한다.
- `Map<K, V> map = new Hashtable<K, V>();` ->Hashtable 생성

### 5.3. Properties

- `Properties`는 `Hashtable`의 하위 클래스이기 때문에 `Hashtable`의 모든 특징을 그대로 가지고 있다.
- 차이점은 `Hashtable`은 키와 값을 다양한 타입으로 지정이 가능한데 비해
- **`Properties`는 키와 값을 `String`타입으로 제한**한 컬렉션이다.
- 애플리케이션의 옵션 정보, 데이터베이스 연결 정보, 국제화(다국어) 정보가 저장된 프로퍼티(~.properties)파일을 읽을 때 주로 사용한다.

#### 5.3.1. 프로퍼티 파일

- 프로퍼티 파일은 키와 값이 `=`기호로 연결되어 있는 텍스트 파일로
- `ISO 8859-1`문자셋으로 저장된다.
- 이 문자셋으로 직접 표현할 수 없는 `한글`은 자동으로 `유니코드(Unicode)`로 변환되어 저장된다.
  ```
  contry=대한민국
  language=한글
  ```
  ```
  contry=\uB300\uD55C\uBBFC\uAD6D
  language=\uD55C\uAE00
  ```

#### 5.3.2. 데이터베이스 연결정보가 있는 프로퍼티 파일

- `driver`, `url`, `username`, `password`는 **키**가 되고
- 그 뒤의 문자열은 **값**이 된다.
  ```
  driver=oracle.jdbc.OracleDriver
  url=jdbc:oracle:thin:@localhost:1521:orcl
  username=scott
  password=tiger
  ```

#### 5.3.3. 프로퍼티 파일 사용 방법

- 프로퍼티 파일을 읽기 위해서는 `Properties`객체 생성 후 `load()`메소드를 호출하면 된다.
- `load()`메소드는 프로퍼티 파일로부터 데이터를 읽기 위해 `FileReader`객체를 매개값으로 받는다.

  ```
  Properties properties = new Properties(); //Propertiest 객체 생성
  properties.load(new FileReader("C:/~/database.properties"));
  ```

- 프로퍼티 파일은 일반적으로 클래스 파일(~.class)과 함께 저장된다.
- 클래스 파일 기준으로 상대 경로를 이용해서 프로퍼티 파일의 경로를 얻으려면 `Class`의 `getResource()`메소드를 이용하면 된다.
- `getResource()`는 주어진 파일의 상대 경로를 `URL`객체로 리턴하는데,
- `URL`의 `getPath()`는 파일의 절대 경로를 리턴한다.
- 예) 클래스 파일과 동일한 위치에 있는 "database.properties"파일을 읽고 `Properties`객체를 생성하는 코드
  ```
  String path = 클래스.class.getResource("database.properties").getPath();
  path = URLDecoder.decode(path, "utf-8"); //경로에 한글이 있을 경우 한글을 복원
  Properties properties = new Properties();
  properties.load(new FileReader(path));
  ```
- 만약 다른 패키지에 프로퍼티 파일이 있을 경우에는 경로 구분자로 `/`를 사용한다.
- 예) `A.class`가 `com.mycompany`패키지에 있고 `database.properties`파일이 `com.mycompany.config`패키지에 있을 경우 프로퍼티 파일의 절대 경로 얻는 방법?

  `String path = A.class.getResource("config/database.properties").getPath();`

- `Properties`객체에서 해당 키의 값을 읽으려면 `getProperty()`메소드 사용
- `Properties`도 `Map`컬렉션이므로 `get()`메소드로 값을 얻을 수 있으나 `get()`메소드는 `Object`타입으로 리턴하므로 강제 타입변환해서 `String`을 얻어야 하기 때문에 일반적으로 `getProperty()`메소드를 사용한다.

  `String value = properties.getProperty("key");`

- 예) 프로퍼티 파일로부터 값을 읽어 출력하는 예제

  ```
  import java.io.FileReader;
  import java.io.IOException;
  import java.net.URLDecoder;
  import java.util.Properties;

  public class PropertiesExample {//프로퍼티 파일로부터 읽기
      public static void main(String[] args) throws IOException {
          Properties properties = new Properties();
          String path = PropertiesExample.class.getResource("database.properties").getPath();
          path = URLDecoder.decode(path, "utf-8");
          properties.load(new FileReader(path));

          String driver = properties.getProperty("driver");
          String url = properties.getProperty("url");
          String username = properties.getProperty("username");
          String password = properties.getProperty("password");

          System.out.println("driver: "+ driver);
          System.out.println("url: "+url);
          System.out.println("username: "+username);
          System.out.println("passwordL "+password);
      }
  }

  ```

---

## 6. 검색 기능을 강화시킨 컬렉션

> 컬렉션 프레임워크는 **검색**기능을 강화시킨 `TreeSet`과 `TreeMap`을 제공한다.
> 이 컬렉션들은 **이진트리(binary tree)를** 이용해서 계층적 구조(Tree 구조)를 가지면서 객체를 저장한다.

### 6.1. 이진 트리 구조

- 이진트리는 여러 개의 노드가 트리 형태로 연결된 구조
- [왼쪽 노드 -> 부모 노드 -> 오른쪽 노드] 순으로 값을 읽으면 오름차순 정렬
- [오른쪽 노드 -> 부모 노드 -> 왼쪽 노드] 순으로 값을 읽으면 내림차순 정렬
- 이진트리가 범위 검색을 쉽게 할 수 있는 이유는 **값들이 정렬되어 있어 그룹핑이 쉽기 때문이다.**

### 6.2. TreeSet

![TreeSet내부구조](https://postfiles.pstatic.net/MjAyMTExMjBfMTEz/MDAxNjM3NDE3NjU0ODU2.PFTsNIYGpupYBJmHxki11lodPDGyRUedNt1i65zr2KEg.LHafIGG2PNWo5sJu3F9AFVQbq3E_QBVcq4kGimx932Yg.JPEG.chex417/TreeSet%EB%82%B4%EB%B6%80%EA%B5%AC%EC%A1%B0.jpg?type=w773)

- 이진트리를 기반으로한 `Set`컬렉션
- `TreeSet<E> treeSet = new TreeSet<E>()` -> `TreeSet` 생성
  - `Set` 인터페이스 타입 변수에 대입해도 되지만 `TreeSet`클래스 타입으로 대입한 이유는 객체를 찾거나 범위 검색과 관련된 **메소드를 사용하기 위해서**이다.
- 하나의 노드는 노드값인 `value`와 양 옆 자식 노드를 참조하기 위한 두 개의 변수로 구성된다.
- `TreeSet`에 객체를 저장하면 **자동으로 정렬**된다.
- `TreeSet` 검색 관련 메소드
  - `first()` 제일 낮은 객체를 리턴
  - `last()` 제일 높은 객체를 리턴
  - `lower(E e)` 주어진 객체보다 바로 아래 객체를 리턴
  - `higher(E e)` 주어진 객체보다 바로 위 객체를 리턴
  - `floor(E e)` 주어진 객체와 동등한 객체가 있으면 리턴, 만약 없다면 바로 아래의 객체를 리턴
  - `ceiling(E e)` 주어진 객체와 동등한 객체가 있으면 리턴, 만약 없다면 바로 위의 객체를 리턴
  - `pollFirst()` 제일 낮은 객체를 꺼내오고 컬렉션에서 제거함
  - `pollLast()` 제일 높은 객체를 꺼내오고 컬렉션에서 제거함
- `TreeSet` 정렬 관련 메소드

  - `descendingIterator()` 내림차순으로 정렬된 Iterator를 리턴
  - `descendingSet()` 내림차순으로 정렬된 NavigableSet을 반환
    - 오름차순으로 정렬하고 싶다면 `descendingSet()`메소드를 2번 호출하면 된다.
  - 객체 정렬하기 예제코드

    ```
    import java.util.NavigableSet;
    import java.util.TreeSet;

    public class TreeSetExample2 {// 객체 정렬하기
        public static void main(String[] args) {
            TreeSet<Integer> scores = new TreeSet<Integer>();
            scores.add(new Integer(87));
            scores.add(new Integer(98));
            scores.add(new Integer(75));
            scores.add(new Integer(95));
            scores.add(new Integer(80));

            NavigableSet<Integer> descendingSet = scores.descendingSet();
            for(Integer score:descendingSet){
                System.out.print(score+" "); //내림차순 정렬
            }
            System.out.println();

            NavigableSet<Integer> ascendingSet = descendingSet.descendingSet();

            for(Integer score: ascendingSet) {
                System.out.print(score + " "); //오름차순 정렬
            }
        }
    }
    ```

- `TreeSet` 범위 검색 관련 메소드

  - `headSet(E toElement, boolean inclusive)` 주어진 객체보다 **낮은** 객체들을 NavigableSet으로 리턴, 주어진 객체 포함 여부는 두 번째 매개값에 따라 달라짐
  - `tailSet(E fromElement, boolean inclusive)` 주어진 객체보다 **높은** 객체들을 NavigableSet으로 리턴, 주어진 객체 포함 여부는 두 번째 매개값에 따라 달라짐
  - `subSet(E fromElement, boolean fromInclusive, E toElement, boolean toInclusive)` 시작과 끝으로 주어진 객체 **사이의** 객체들을 NavigableSet으로 리턴, 시작과 끝 객체의 포함 여부는 두 번째, 네 번째 매개값에 따라 달라짐
  - **영어 단어를 정렬하고, 범위 검색해보기 예제코드**

    ```
    import java.util.NavigableSet;
    import java.util.TreeSet;

    public class TreeSetExample3 {
        public static void main(String[] args) {
            TreeSet<String> treeSet = new TreeSet<String>();
            treeSet.add("apple");
            treeSet.add("forever");
            treeSet.add("description");
            treeSet.add("ever");
            treeSet.add("zoo");
            treeSet.add("base");
            treeSet.add("guess");
            treeSet.add("cherry");

            System.out.println("[c~f 사이의 단어 검색]");
            // "c"<=검색 단어<="f"
            NavigableSet<String> rangeSet = treeSet.subSet("c", true, "f", true);
            for(String word: rangeSet){
                System.out.println(word);
            }
        }
    }
    ```

    ```
    [c~f 사이의 단어 검색]
    cherry
    description
    ever
    ```

### 6.3. TreeMap

![TreeMap내부구조](https://postfiles.pstatic.net/MjAyMTExMjBfMTMg/MDAxNjM3NDE4OTg5NzU1.BIGK1Vwnky4aa2M2ezVrXqN7uWMwC2JML8yDFvvic5Yg.I68GZ4JzRj0eoz_Rydx23tcNRckOiwW7f3p5ebTKLosg.JPEG.chex417/TreeMap_%EB%82%B4%EB%B6%80%EA%B5%AC%EC%A1%B0.jpg?type=w773)

- 이진트리를 기반으로 한 `Map`컬렉션
- `TreeMap<K, V> treeMap = new TreeMap<K, V>();` -> TreeMap 생성
  - `Map`인터페이스 타입 변수에 대입해도 되지만 `TreeMap` 클래스 타입으로 대입한 이유는 특정 객체를 찾거나 범위 검색과 관련된 **메소드를 사용하기 위해서**이다.
- `TreeSet`과의 차이점은 키와 값이 저장된 `Map.Entry`를 저장한다는 점이다.
- `TreeMap`에 객체를 저장하면 자동으로 정렬되는데, 부모 키값과 비교해서 키값이 낮은 것은 왼쪽 자식노드에, 키값이 높은 것은 오른쪽 자식 노드에 `Map.Entry`객체를 저장한다.
- `TreeMap` 검색 관련 메소드

  - `firstEntry()` 제일 낮은 Map.Entry를 리턴
  - `lastEntry()` 제일 높은 Map.Entry를 리턴
  - `lowerEntry(K key)` 주어진 키보다 바로 아래 Map.Entry를 리턴
  - `higherEntry(K key)` 주어진 키보다 바로 위 Map.Entry를 리턴
  - `floorEntry(K key)` 주어진 키와 동등한 키가 있으면 해당 Map.Entry를 리턴 없다면 바로 아래의 Map.Entry를 리턴
  - `ceilingEntry(K key)` 주어진 키와 동등한 키가 있으면 해당 Map.Entry를 리턴 없다면 바로 위의 Map.Entry를 리턴
  - `pollFirstEntry()` 제일 낮은 Map.Entry를 꺼내오고 컬렉션에서 제거함
  - `pollLastEntry()` 제일 높은 Map.Entry를 꺼내오고 컬렉션에서 제거함

- `TreeMap` 정렬 관련 메소드
  - `descendingKeySet()` 내림차순으로 정렬된 키의 NavigableSet을 리턴
  - `descendingMap()` 내림차순으로 정렬된 Map.Entry()의 NavigableMap을 리턴
- `TreeMap` 범위 검색 관련 메소드
  - `headMap(K toKey, boolean inclusive)` 주어진 키보다 **낮은** Map.Entry들을 NavigableMap으로 리턴, 주어진 키의 Map.Entry포함 여부는 두 번째 매개값에 따라 달라짐
  - `tailMap(K fromKey, boolean inclusive)` 주어진 키보다 **높은** Map.Entry들을 NavigableMap으로 리턴, 주어진 키의 Map.Entry포함 여부는 두 번째 매개값에 따라 달라짐
  - `subMap(K fromKey, boolean fromInclusive, K toKey, boolean toInclusive)` 시작과 끝으로 주어진 키 사이의 Map.Entry들을 NavigableMap컬렉션으로 반환, 시작과 끝 키의 Map.Entry 포함 여부는 두 번째, 네 번째 매개값에 따라 달라짐

### 6.4. Comparable과 Comparator

#### 6.4.1. Comparable

- `TreeSet`의 객체와 `TreeMap`의 키는 저장과 동시에 자동으로 오름차순 정렬됨
  - 정렬을 위해 `java.lang.Comparable`을 구현한 객체를 요구하는데, `Integer`, `Double`, `String`은 모두 `Comparable`인터페이스를 구현하고있다.
  - 사용자 정의 클래스도 **`Comparable`을 구현한다면** 자동 정렬이 가능하다.
  - `Comparable`에는 `compareTo()`메소드가 정의되어 있기 때문에 사용자 정의 클래스에서는 이 메소드를 오버라이딩하여 다음과 같이 리턴 값을 만들어 내야 한다.
    ```
    리턴타입 int
    메 소 드 compareTo(T o)
    설    명 주어진 객체와 같으면 0을 리턴
            주어진 객체보다 적으면 음수를 리턴
            주어진 객체보다 크면 양수를 리턴
    ```
- **나이를 기준으로 `Person`객체를 오름차순으로 정렬하기 위해 `Comparable`인터페이스를 구현한 예제코드**

  ```
  public class Person implements Comparable<Person>{ //Comparable 구현 클래스
      public String name;
      public int age;

      public Person(String name, int age){
          this.name = name;
          this.age = age;
      }

      @Override
      public int compareTo(Person o){//Comparable인터페이스 메소드 재정의
          if(age<o.age) return -1;
          else if(age == o.age) return 0;
          else return 1;
      }
  }
  ```

  ```
  import java.util.Iterator;
  import java.util.TreeSet;

  public class ComparableExample {
      public static void main(String[] args) {//사용자 정의 객체 나이 순으로 정렬하기
          TreeSet<Person> treeSet = new TreeSet<Person>();

          //저장될 때 나이순으로 정렬됨
          treeSet.add(new Person("홍길동", 45));
          treeSet.add(new Person("김자바", 25));
          treeSet.add(new Person("박지원", 31));

          Iterator<Person> iterator = treeSet.iterator();
          while(iterator.hasNext()){
              Person person = iterator.next();
              System.out.println(person.name+": "+person.age);
          }
      }
  }
  ```

#### 6.4.2. Comparator

- `TreeSet`의 객체와 `TreeMap`의 키가 `Comparable`을 구현하고 있지 않을 경우에는 저장하는 순간 `ClassCastException`이 발생한다.
  - 그렇다면 `Comparable` 비구현 객체를 정렬하는 방법은 없을까?
  - `TreeSet` 또는 `TreeMap` 생성자의 매개값으로 **정렬자(Comparator)**를 제공하면 `Comparable` 비구현 객체도 정렬시킬 수 있다.
    ```
    TreeSet<E> treeSet = new TreeSet<E>( new AscendingComparator() ); //오름차순 정렬자
    TreeMap<K,V> treeMap = new TreeMap<K, V>( new DescendingComparator() ); // 내림차순 정렬자
    ```
- 정렬자는 `Comparator`인터페이스를 구현한 객체를 말한다.
- `Comparator`인터페이스에 정의되어 있는 메소드

  ```
  리턴타입: int
  메 소 드: compare(T o1, T o2)
  설    명: o1과 o2가 동등하다면 0을 리턴
          o1이 o2보다 앞에 오게 하려면 음수를 리턴
          o1이 o2보다 뒤에 오게 하려면 양수를 리턴
  ```

- **가격을 기준으로 `Fruit`객체를 내림차순으로 정렬시키는 정렬자 예제코드**

  ```
  import java.util.Comparator;

  public class DescendingComparator implements Comparator<Fruit> {//Fruit의 내림차순 정렬자
      @Override
      public int compare(Fruit o1, Fruit o2){ //내림차순이니까 반대로
          if(o1.price<o2.price) return 1; // 가격이 적을 경우 뒤에 오게 함
          else if(o1.price == o2.price) return 0;
          else return -1;// 가격이 클 경우 앞에 오게 함
      }
  }
  ```

  ```
  public class Fruit {//Comparable을 구현하지 않은 클래스
    public String name;
    public int price;

    public Fruit(String name, int price){
        this.name = name;
        this.price = price;
    }
  }
  ```

  ```
  import com.sun.source.tree.Tree;

  import java.util.Iterator;
  import java.util.TreeSet;

  public class ComparatorExample {//내림차순 정렬자를 사용하는 TreeSet
      public static void main(String[] args) {
          /*
          TreeSet<Fruit> treeSet = new TreeSet<Fruit>();
          //Fruit이 Comparable을 구현하지 않았기 때문에 예외 발생 -> ClassCastException
          treeSet.add(new Fruit("포도", 3000));
          treeSet.add(new Fruit("수박", 10000));
          treeSet.add(new Fruit("딸기", 6000));
          */

          TreeSet<Fruit> treeSet = new TreeSet<Fruit>(new DescendingComparator()); //내림차순 정렬자 제공
          treeSet.add(new Fruit("포도", 3000)); //저장될 때 가격을 기준으로 내림차순 정렬됨
          treeSet.add(new Fruit("수박", 10000));
          treeSet.add(new Fruit("딸기", 6000));

          Iterator<Fruit> iterator = treeSet.iterator();
          while(iterator.hasNext()){
              Fruit fruit = iterator.next();
              System.out.println(fruit.name+": "+fruit.price);
          }
      }
  }
  ```

---

## 7. LIFO와 FIFO 컬렉션

- 후입선출(LIFO: Last In First Out)자료구조를 제공하는 스택(Stack)클래스
- 선입선출(FIFO: First In First Out)자료구조를 제공하는 큐(Queue)인터페이스

### 7.1. Stack

- `Stack<E> stack = new Stack<E>();` -> `Stack`생성
- 스택을 응용한 대표적인 예? **JVM스택메모리**, 스택 메모리에 저장된 변수는 나중에 저장된 것부터 제거된다.
- `Stack`클래스의 주요 메소드
  - `push(E item)` 주어진 객체를 스택에 넣는다.
  - `peek()` 스택의 맨 위 객체를 가져온다. 객체를 스택에서 제거하지 않는다.
  - `pop()` 스택의 맨 위 객체를 가져온다. 객체를 스택에서 제거한다.

### 7.2. Queue

- 큐를 응용한 대표적인 예? **스레드풀(ExecutorService)의 작업 큐**, 작업 큐는 먼저 들어온 작업부터 처리한다.
- `Queue`인터페이스의 주요 메소드
  - `offer(E e)` 주어진 객체를 넣는다.
  - `peek()` 객체를 하나 가져온다. 객체를 큐에서 제거하지 않는다.
  - `poll()` 객체를 하나 가져온다. 객체를 큐에서 제거한다.
- `Queue`인터페이스를 구현한 대표적인 클래스는 `LinkedList`이다.
  - `LinkedList`는 `List`인터페이스를 구현했기 때문에 `List`컬렉션이기도 하다.
  - `Queue<E> queue = new LinkedList<E>();`

---

## 8. 동기화된 컬렉션

> 컬렉션 프레임워크의 대부분의 클래스들은 싱글 스레드 환경에서 사용할 수 있도록 설계되었으나 싱글 스레드 환경에서 사용하다가 멀티 스레드 환경으로 전달할 필요도 있을 것이다.

- 이런 경우를 대비해 컬렉션 프레임워크는 비동기화된 메소드를 동기화된 메소드로 래핑하는 `Collections`의 `synchronizedXXX()`메소드를 제공한다.
  - `synchronizedList(List<T> list)` List를 동기화된 List로 리턴
  - `synchronizedMap(Map<K, V> m)` Map을 동기화된 Map으로 리턴
  - `synchronizedSet(Set<T> s)` Set을 동기화된 Set으로 리턴

---

## 9. 병렬 처리를 위한 컬렉션

- 동기화된 컬렉션은 멀티 스레드 환경에서 하나의 스레드가 요소를 안전하게 처리하도록 도와주지만, 전체 요소를 빠르게 처리하지는 못한다.
  - 하나의 스레드가 요소를 처리할 때 전체 잠금이 발생하여 다른 스레드는 대기 상태가 되기 때문에 병렬적으로 컬렉션의 요소들을 처리할 수 없다.
- 자바는 멀티 스레드가 컬렉션의 요소를 **병렬적으로** 처리할 수 있도록 특별한 컬렉션을 제공하고 있다. ->**부분(segment) 잠금**을 사용하기 때문에 가능
  - `java.util.concurrent`패키지의 `ConcurrentHashMap`과 `ConcurrentLinkedQueue`이다.
  - `ConcurrentHashMap`은 `Map`의 구현 클래스
  - `ConcurrentLinkedQueue`는 `Queue`의 구현 클래스
- `Map<K, V> map = new ConcurrentHashMap<K,V>();`
- `Queue<E> queue = new ConcurrentLinkedQueue<E>();`
  - `ConcurrentLinkedQueue`는 **락-프리(lock-free)** 알고리즘을 구현한 컬렉션으로 여러 개의 스레드가 동시에 접근할 경우, 잠금을 사용하지 않고도 최소한 하나의 스레드가 안전하게 요소를 저장하거나 얻도록 해준다.
