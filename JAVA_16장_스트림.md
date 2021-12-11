# 16장 스트림 782-833p

## 1. 스트림 소개

- 스트림은 컬렉션(배열포함)의 저장 요소를 하나씩 참조해서 람다식(JAVA8부터 사용가능)으로 처리할 수 있도록 해주는 **내부 반복자**이다.
  ```
  List<String> list = Arrays.asList("홍길동", "신용권", "김자바");
  Stream<String> stream = list.stream(); //컬렉션의 stream()메소드로 스트림 객체 얻음
  stream.forEach( name -> System.out.println(name) ); //컬렉션의 요소를 하나씩 콘솔에 출력
  ```

---

## 2. 스트림 특징

### 2.1. 람다식으로 요소처리 코드를 제공한다.

```
스트림이 제공하는 대부분의 요소 처리 메소드는 매개값으로 람다식 또는 메소드 참조를 대입할 수 있다.

예시) forEach메소드의 매개값으로 람다식을 주었다.

 Stream<Student> stream = list.stream();//스트림 얻기
 //List컬렉션에서 Student를 가져와 람다식의 매개값으로 제공
 forEach( s -> {
   String name = s.getname();
   int score = s.getScore();
   System.out.println(name + "-" + score);
 });
```

### 2.2. 내부 반복자를 사용하므로 병렬처리가 쉽다.

![내부반복자](https://postfiles.pstatic.net/MjAyMTEyMTFfMTU3/MDAxNjM5MjA5OTg0ODEy.4o5eJNiow2FT_grFg6p0_xtAuS2tEtaMS_2bL3tEM7Qg.1ZcWydxEXXufjeRvOYEUUtJjHi17VinRUn1HjNmOFiMg.JPEG.chex417/%EB%82%B4%EB%B6%80%EB%B0%98%EB%B3%B5%EC%9E%90.jpg?type=w773)

- **외부 반복자?** 개발자가 코드로 직접 요소를 반복해서 가져오는 패턴
  ex. `for`문, `while`문
- **내부 반복자?** 컬렉션 내부에서 요소드를 반복시키고, 개발자는 요소당 처리해 할 코드만 제공하는 코드 패턴
- **내부 반복자의 이점?**
  1. 개발자는 **요소처리** 코드에만 집중
  2. 멀티코어 CPU를 최대한 활용하기 위해 요소들을 분배시켜 **병렬작업**을 할 수 있다. (하나씩 처리하는 순차적 외부 반복자보다는 요소를 효율적으로 반복시킬 수 있다.)
- **병렬처리?** 한 가지 작업을 서브 작업으로 나누고, 서브 작업들을 분리된 스레드에서 병렬적으로 처리하는 것

### 2.3. **중간처리**와 **최종처리**를 수행한다.

![중간처리와 최종처리](https://postfiles.pstatic.net/MjAyMTEyMTFfMTU0/MDAxNjM5MjExNTU3MzM4.ZfwY5QlDciA9aj1jCuSu4cde_CMrSagO_IAb8zkslbgg.Uyap_bDj_NfSQbD-7tXfUDXBkrK2zHdbLRDiZ0EHLWIg.JPEG.chex417/%EC%A4%91%EA%B0%84%EC%B2%98%EB%A6%AC_%EC%B5%9C%EC%A2%85%EC%B2%98%EB%A6%AC.jpg?type=w773)

- 중간처리: 매핑, 필터링, 정렬
- 최종처리: 반복, 카운트, 평균, 총합등의 집계처리
- 예시) `List`에 저장되어 있는 `Student` 객체를 중간처리에서 `score`필드값으로 매핑하고, 최종처리에서 `score`의 평균값을 구한다.

```

import java.util.Arrays;
import java.util.List;

public class MapAndReduceExample {//중간처리와 최종처리

  public static void main(String[] args) {
      List<Student> studentList = Arrays.asList(
              new Student("홍길동", 10),
              new Student("신용권", 20),
              new Student("유미선", 30)
      );

      double avg = studentList.stream()
              //중간처리(학생 객체를 점수로 매핑)
              .mapToInt(Student::getScore)
              //최종처리(평균점수)
              .average()
              .getAsDouble();

      System.out.println("평균점수: " + avg);
  }
}

```

---

## 3. 스트림의 종류

- `BaseStream`: 모든 스트림에서 사용할 수 있는 공통 메소드들이 정의되어 있을 뿐 코드에서 직접적으로 사용되지는 않음
- `Stream`: **객체를 요소로** 해서 처리하는 스트림
- `IntStream`, `LongStream`, `DoubleStream`: 각각 기본타입인 `int`, `long`, `double`요소를 처리하는 스트림이다.

`BaseStream`인터페이스를 부모로 해서 자식 인터페이스들이(`Stream`, `IntSream`, `LongStream`, `DobuleStream`) 상속관계를 이룬다.

## 4. 스트림 얻기

### 4.1. 컬렉션으로부터 스트림 얻기

```
List<Student> studentList = Arrays.asList(
  new Student("홍길동", 10),
  new Student("신용권", 5),
  new Student("김자바", 50)
);

Stream<Student> stream = studentList.stream();//List컬렉션에서 스트림 객체 얻기
```

### 4.2. 배열로부터 스트림 얻기

```
String[] strArray = {"홍길동", "신용권", "김자바"};
Stream<String> strStream = Arrays.stream(strarray);
```

### 4.3. 숫자 범위로부터 스트림 얻기

```
IntStream stream = IntStream.rangeClosed(1, 100); //1부터 100까지 순차적으로 제공하는 IntStream 리턴
stream.forEach(a -> sum += a);
System.out.println("총합: "+sum);
```

### 4.4. 파일로부터 스트림 얻기

```
Files의 정적 메소드인 lines()와 BufferedReader의 lines()메소드를 이용하여 문자 파일의 내용을 스트림을 통해 행 단위로 읽고 콘솔에 출력한다.

Path path = Paths.get("~~~/test.txt"); // 파일의 경로 정보를 가지고 있는 Path객체 생성

//Files.lines()메소드 이용
stream = Files.lines(path, Charset.defaultCharset()); //운영체제의 기본 문자셋
stream.forEach(System.out :: println);
System.out.println();

//BufferedReader의 lines() 메소드 이용
File file = path.toFile();
FileReader fileReader = new FileReader(file);
BufferedReader br = new BufferedReader(fileReader);
stream = br.lines();
stream.forEach( System.out :: println );
```

### 4.5. 디렉토리로부터 스트림 얻기

```
Files의 정적 메소드인 list()를 이용해서 디렉토리의 내용(서브 디렉토리 또는 파일목록)을 스트림을 통해 읽고 콘솔에 출력한다.

Stream<Path> stream = Files.list(path);
stream.forEach( p -> System.out.println(p.getFileName()) );

//p는 서브 디렉토리 또는 파일에 해당하는 Path 객체
//p.getFileName()은 서브 디렉토리 이름 또는 파일 이름 리턴
```

---

## 5. 스트림 파이프라인

- **리덕션(Reduction)**: 대량의 데이터를 가공해서 축소하는 것(합계, 평균, 카운트, 최댓값, 최솟값 등)

```
- 컬렉션의 요소를 리덕션의 결과물로 바로 집계할 수 없을 경우에는 필터링, 매핑, 정렬, 그룹핑 등의 중간처리가 필요하다.

- 스트림은 중간처리와 최종처리를 파이프라인으로 해결한다.
```

- **파이프라인**: 여러 개의 스트림이 연결되어 있는 구조

```
- Stream 인터페이스에 있는 필터링, 매핑, 정렬 등의 중간처리 메소드들은 중간처리된 스트림을 리턴한다.
- 이 스트림에서 다시 중간처리 메소드를 호출해서 파이프라인을 형성하게 된다.

- 예) 회원 컬렉션에서 남자만 필터링하는 중간 스트림을 연결하고, 다시 나이로 매핑하는 스트림을 연결한 후, 최종 남자 평균 나이를 집계하면 파이프라인이 형성된다.
   double ageAvg = list.stream() //오리지널 스트림
        .filter(m -> m.getSex()==Member.MaLE) //중간처리 스트림
        .mapToInt(Member :: getAge) //중간처리 스트림
        .average() //최종처리
        .getAsDouble();
```

- **지연(Lazy)**: 최종처리가 시작되기 전까지 _중간 처리는 지연된다._

```
- 최종처리가 시작되면 비로소 컬렉션의 요소가 하나씩 중간 스트림에서 처리되고 최종처리까지 오게 된다.
```

## 6. 중간처리 메소드와 최종처리 메소드

- 리턴타입을 보면 중간처리 메소드인지 최종처리 메소드인지 구분할 수 있다.
  - 중간처리 메소드: 리턴타입이 `스트림`
  - 최종처리 메소드: 리턴타입이 `기본타입`이거나 `OptionalXXX`

### 6.1. 중간처리 메소드

_최종처리 메소드가 시작을 해야만 중간처리 메소드가 작동한다._

#### 6.1.1. 필터링

- `distinct()`: 중복 제거

```
- Stream: Object.equals(Object)가 true이면 동일한 객체로 판단하고 중복 제거
- IntStream, LongStream, DoubleStream: 동일값일 경우 중복 제거
```

- `filter()`: 조건에 맞는 것만 필터링

```
- 매개값으로 주어진 Predicate가 true를 리턴하는 요소만 필터링

  names.stream()
   .filter(n -> n.startsWith("김")) //필터링
   .forEach(n -> System.out.println(n));
```

#### 6.1.2. 매핑

_중간처리 기능으로 스트림의 요소를 다른 요소로 대체하는 작업을 말한다._

- **flatMapXXX()**: 요소를 대체하는 복수 개의 요소들로 구성된 새로운 스트림을 리턴(_복수의 요소로 대체_)

  `B, A -> B2, B1, A2, A1`

- **mapXXX()**: 요소를 대체하는 요소로 구성된 새로운 스트림을 리턴(_하나의 요소로 대체_)

  `B, A -> D, C`

- **asXXXStream()**: XXX요소로 타입변환해서 XXXStream을 생성
- **boxed()**: int, long, double 요소를 Integer, Long, Double 요소로 박싱해서 Stream을 생성

#### 6.1.3. 정렬

- `sorted()`: 객체를 `Comparable`구현 방법에 따라 정렬
- `sorted(Comparator<T>)`: 객체를 주어진 `Comparator`에 따라 정렬

```
객체요소일 경우에는 Comparable을 구현하지 않으면 첫번째 sorted()메소드를 호출했을 때 ClassCastException이 발생하므로 Comparable을 구현한 요소에서만 sorted()메소드를 호출해야 한다.

객체요소가 Comparable을 구현하지 않았거나,
구현했더라도 다른 비교방법으로 정렬하려면 Comparator를 매개값으로 하는 두번째 sorted(Comparator<T>)메소드를 사용


-> Comparator는 함수적 인터페이스이므로 람다식으로 매개값을 작성할 수 있다.
   sorted( (a,b) -> {...} )
   {}안에는 a와 b를 비교해서 a가 작으면 음수, 같으면 0, a가 크면 양수를 리턴하는 코드를 작성하면 된다.
```

#### 6.1.4. 루핑(looping)

_요소 전체를 반복하는 것을 말한다._

- `peek()`: 중간처리 메소드

```
최종처리 메소드가 실행되지 않으면 지연되기 때문에 반드시 최종처리 메소드가 호출되어야 동작한다.

예) 필터링 후 어떤 요소만 남았는지 확인하기 위해 다음과 같이 peek()를 마지막에서 호출할 경우, 스트림은 전혀 동작하지 않는다.
    intStream
      .filter( a-> a%2==0 )
      .peek( a-> System.out.println(a) )

    peek()메소드 호출 후 최종처리 메소드인 sum()을 호출해야만 peek()가 정상적으로 동작한다.
    intStream
      .filter( a-> a%2==0 )
      .peek( a-> System.out.println(a) )
      .sum()
```

- `forEach()`: 최종처리 메소드이기 때문에 파이프라인 마지막에 루핑하면서 요소를 하나씩 처리

```
요소를 소비하는 최종처리 메소드이므로 이후에 sum()과 같은 다른 최종 메소드를 호출하면 안된다.
```

### 6.2. 최종처리 메소드

#### 6.2.1. 매칭

_요소들이 특정 조건에 만족하는지 조사한다._

- `allMatch()`: **모든 요소들이** 매개값으로 주어진 `Predicate`의 조건을 만족하는지 조사
- `anyMatch()`: **최소한 한 개의 요소**가 매개값으로 주어진 `Predicate`의 조건을 만족하는지 조사
- `noneMatch()`: **모든 요소들이** 매개값으로 주어진 `Predicate`의 조건을 만족하는지 **않는지** 조사

#### 6.2.2. 기본 집계

_집계는 대량의 데이터를 가공해서 축소하는 리덕션(Reduction)이라고 볼 수 있다._

- `sum()`
- `count()`
- `averager()`
- `max()`
- `min()`
- `findFirst()`

#### 6.2.3. Optional 클래스

```
- 값을 저장하는 값 기반 클래스
- 집계 값이 존재하지 않을 경우 디폴트 값을 설정할 수 있고,
- 집계 값을 처리하는 Consumer도 등록할 수 있다.
```

- `isPresent()`: 값이 저장되어 있는지 여부
- `orElse(T)`: 값이 저장되어 있지 않을 경우 디폴트 값 지정
- `ifPresent(Consumer)`: 값이 저장되어 있을 경우에만 Consumer에서 처리

#### 6.2.4. 커스텀집계

- `reduce()`: 프로그램화해서 다양한 집계(리덕션) 결과물을 만들 수 있다.

```
<매개변수>
a. XXXBinaryOperator<T>: 집계 처리를 위한 람다식을 대입
  int sum = studentList.stream()
      .map(Student :: getScore)
      .reduce((a, b) -> a+b)
      .get();


b. identity: 스트림에 요소가 없을 경우 리턴될 디폴트 값
  int sum = studentList.stream()
      .map(Student :: getScore)
      .reduce(0, (a, b) -> a+b)


-> 스트림에 요소가 없을 경우
- a.는 NoSuchElementException 발생
- b.는 디폴트 값(identity)인 0을 리턴

-> 스트림에 요소가 있을 경우
- 두 코드 모두 동일한 결과 리턴
```

#### 6.2.5. 수집(collect())

```
- 스트림은 요소들을 필터링 또는 매핑한 후 요소들을 수집하는 최종 메소드인 collect()를 제공한다.
- 이 메소드를 이용하면 필요한 요소만 컬렉션으로 담을 수 있고,
- 요소들을 그룹핑한 후 집계(리덕션)할 수 있다.
```

- **필터링한 요소 수집**

  - Stream의 `collect(Collector<T,A,R> collector)`메소드는 필터링 또는 매핑된 요소들을 새로운 컬렉션에 수집하고 이 컬렉션을 리턴한다.

  ```
  Collector(수집기): 어떤 요소를 어떤 컬렉션에 수집할 것인지 결정
  - T: 요소
  - A: 누적기, 컬렉션에 요소를 수집하는 역할
  - R: 요소가 저장될 컬렉션
  ```

  - `Collector`의 구현 객체는 `Collectors`클래스의 다양한 정적 메소드를 이용해서 얻을 수 있다.

  ```
  Collector<Student, ?, List<Studnet>> collector = Collectors.toList(); // List컬렉션에 요소를 수집시키는 Collector를 얻음

  - A(누적기)가 ?인 이유
    널리알려져 있는 컬렉션 즉 List, Map, Set 같은 경우에는
    Collector내부에서 이들 컬렉션에 저장하는 방법을 이미 알고 있기 때문에 별도의 누적기가 필요없다.
  ```

  - 예제코드

  ```
  1. Stream<Student> totalStream = totalList.stream(); //전체 학생 List에서 Stream을 얻는다.
  2. Stream<Student> maleStream = totalStream.filter( s-> s.getSex()==Student.Sex.MALE); //남학생만 필터링해서 Stream을 얻는다.
  3. Collector<Student, ?, List<Student>> collector = Collectors.toList(); //List에 Studnet를 수집하는 Collector를 얻는다.

  4. List<Student> maleList = maleStream.collect(collector); // Stream에서 collect()메소드로 Student를 수집해서 새로운 List를 얻는다.
  ```

  ```
  위 코드에서 변수를 생략하면 다음과 같이 간단하게 작성할 수 있다.
  List<Studnet> maleList = totalList.stream()
    .filter(s->s.getSex()==Student.Sex.MALE)
    .collect(Collectors.toList());
  ```

- **사용자 정의 컨테이너에 수집하기**

  _List, Set, Map과 같은 컬렉션이 아니라 사용자 정의 컨테이너 객체에 수집하는 것을 말한다._

  ```
  인터페이스  리턴타입                           메소드(매개변수)
    Stream      R        collect(Supplier<R>, BiConsumer<R, ?, super T>, BiConsumer<R,R>)
  ```

  - 매개변수

  ```
  1. Supplier: 요소들이 수집될 컨테이너 객체를 생성하는 역할
   - 순차처리(싱글 스레드) 스트림: 단 한 번 Supplier가 실행
   - 병렬처리(멀티 스레드) 스트림: 스레드별로 Supplier가 실행되어 스레드별로 컨테이너가 생성

  2. XXXConsumer: 컨테이너 객체(R)에 요소(T)를 수집하는 역할
    - 스트림에서 요소를 컨테이너에 누적할 때마다 실행

  3. BiConsumer: 컨테이너 객체(R)를 결합하는 역할
   - 순차처리(싱글 스레드) 스트림: 실행되지 않음
   - 병렬처리(멀티 스레드) 스트림: 스레드별로 생성된 컨테이너를 결합해서 최종 컨테이너를 완성
  ```

  - 리턴타입 R: 요소들이 최종 수집된 컨테이너 객체

  ```
  순차 처리 스트림: 리턴 객체가 첫번째 Supplier가 생성한 객체지만
  병렬 처리 스트림: 리턴 객체는 최종 결합된 컨테이너 객체가 됨
  ```

  - 예제코드

  ```
  1. Stream<Student> totalStream = totalList.stream(); //전체 학생List에서 Stream을 얻음
  2. Stream<Student> maleStream = totalStream.filter(s -> s.getSex() == Student.Sex.MALE); //남학생만 필터링해서 Stream을 얻음


  3. Supplier<MaleStudent> supplier = ()->new MaleStudent(); //MaleStudent를 생성하는 Supplier를 얻음
  4. BiConsumer<MaleStudent, Student> accumulator = (ms, s)->ms.accumulate(s); //MaleStudent와 Student를 매개값으로 받아 MaleStudent의 accumulate()메소드로 Student를 수집하는 BiConsumer를 얻음
  5. BiConsumer<MaleStudent, MaleStudent> combiner = (ms1, ms2)->ms1.combine(ms2); // 2개의 MaleStudent를 매개값으로 받아 combine()메소드로 결합하는 BiConsumer를 얻음


  6. MaleStudent maleStudent = maleStream.collect(supplier, accumulator, combiner); //supplier가 제공하는 MaleStudent에 accumulator가 Student를 수집해서 최종 처리된 MaleStudent를 얻음(싱글 스레드에서는 combiner는 사용되지 않음)
  ```

  ```
  위 코드에서 변수를 생략하면 다음과 같이 간단하게 작성할 수 있다.

  MaleStudent maleStudent = totalList.stream()
     .filter(s->s.getSex()==Student.Sex.MALE)
     .collect(
       () -> new MaleStudent(),
       (r, t) -> r.accumulate(t),
       (r1, r2) -> r1.combine(r2)
     );
  ```

  ```
  람다식을 메소드 참조로 변경하면 다음과 같이 더 간단하게 작성할 수 있다.

  MaleStudent maleStudent = totalList.stream()
     .filter(s->s.getSex() == Student.Sex.MALE)
     .collect(MaleStudent :: new, MaleStudent :: accumulate, MaleStudent :: combine);
  ```

- **요소를 그룹핑해서 수집**

  _`collect()` 메소드는 요소를 수집하는 기능 이외에 컬렉션의 요소들을 그룹핑해서 `Map`객체로 생성하는 기능도 제공한다._

  - `Collectors.groupingBy()`의 리턴 객체를 매개값으로 대입: 스레드에 안전하지 않은 `Map` 객체 생성

  - `Collectors.groupingByConcurrent()`의 리턴 객체를 매개값으로 대입: 스레드에 안전한 `ConcurrentMap` 객체 생성

  ```
  학생들을 거주 도시별로 그룹핑하고,
  같은 그룹에 속하는 학생들의 이름 List를 생성한 후,
  거주 도시를 키로 이름 List를 값으로 갖는 Map을 생성한다.

  Map<Student.City, List<String>> mapByCity = totalList.stream()
     .collect(
       Collectors.groupingBy(
         Student::getCity,
         Collectors.mapping(Student::getName, Collectors.toList())
       )
     ;)
  ```

- **그룹핑 후 매핑 및 집계**
  - `Collectors.groupingBy()`메소드는 그룹핑 후 매핑이나 집계(평균, 카운트, 연결, 최대, 최소, 합계)를 할 수 있도록 두 번째 매개값으로 `Collector`를 가질 수 있다.
  - 위 예제에서 도시(city)로 그룹핑된 학생 객체를 학생 이름(name)으로 매핑하기 위해 `mapping()`메소드로 `Collector`를 얻었다.
  - 예제코드
  ```
  //성별에 따른 평균점수를 저장하는 Map 얻기
  Map<Student.Sex, Double> mapBySex = totalList.sream()
    .collect(
      Collectors.groupingBy(
        Student::getSex,
        Collectors.averagingDouble(Student :: getScore)
      )
    );
  ```
