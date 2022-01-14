# 13장 654-671p

## 1. 왜 제네릭을 사용해야 하는가?

- **제네릭**은 클래스, 인터페이스 그리고 메소드를 정의할 때 타입(type)을 파라미터로 사용할 수 있도록 한다.
  - Java5부터 제네릭 타입이 새로 추가됨

### 1.1. **컴파일 시** 강한 타입 체크를 할 수 있다.

- 자바 컴파일러는 제네릭 코드에 대해 강한 타입 체크를 한다.
  - 코드에서 잘못 사용된 타입 때문에 발생하는 문제점을 제거한다.
  - 실행 시 타입 에러가 나는 것보단 컴파일 시에 미리 체크해서 에러를 사전에 방지하는 것이 좋다.

### 1.2. 타입 변환(Casting)을 제거한다.

- 비제네릭 코드

  ```
  List list = new ArrayList();
  list.add("hello");
  String str = (String) list.get(0); // 타입 변환을 해야 한다.
  ```

- 제네릭 코드
  ```
  List<String> list = new ArrayList<String>();
  list.add("hello");
  String str = list.get(0); // 타입 변환을 하지 않는다.
  ```
  - 제네릭 코드에선 `List`에 저장하는 요소를 `String`타입으로 국한하기 때문에 요소를 찾아올 때 타입 변환을 할 필요가 없어 프로그램 성능이 향상된다.

---

## 2. 제네릭 타입(class<T>, interface<T>)

- 제네릭 타입은 **타입을 파라미터로 가지는 `클래스`와 `인터페이스`를 말한다.**

  ```
  public class 클래스명<T> {...}
  public interface 인터페이스명<T> {...}
  ```

- 제네릭타입을 실제 코드에서 사용하려면 타입 파라미터에 구체적인 타입을 지정해야 한다. 그렇다면 왜 이런 타입 파라미터를 사용해야 할까?

  ```
  public class Box{
    private Object object;
    public void set(Object object) { this.object = object; }
    public Object get() { return object; }
  }
  ```

  - Box의 클래스 필드 타입이 `Object`인데 `Object`클래스는 모든 자바 클래스의 최상위 조상(부모) 클래스이다.
  - 모든 자바 객체는 `Object`타입으로 자동 타입 변환되어 저장된다.(자식 객체는 부모 타입에 대입할 수 있다는 성질)

  ```
  Box box = new Box();
  box.set("hello"); //String타입을 Object타입으로 자동 타입 변환해서 저장
  String str = (String)box.get(); //Object타입을 String 타입으로 강제 타입 변환해서 얻음
  ```

  - 이와 같이 `Object`타입을 사용하면 모든 종류의 자바 객체를 저장할 수 있다는 장점은 있으나 저장하거나 읽어 올 때 **타입 변환**이 발생한다.
  - 타입 변환이 빈번해지면 전체 프로그램 성능에 좋지 못한 결과를 가져올 수 있다.
  - **제네릭을 이용하면 모든 종류의 객체를 저장하면서 타입 변환이 발생하지 않도록 할 수 있다.**

  ```
  public class Box<T> {
    private T t;
    public T get() { return t; }
    public void set(T t) { this.t = t; }
  }
  ```

  - 타입 파라미터 T를 사용해서 Object 타입을 모두 T로 대체했다.
  - T는 Box클래스로 **객체를 생성할 때** 구체적인 타입으로 변경된다.

  ```
  Box<String> box = new Box<String>();
  ```

  - 위와 같이 Box객체를 생성하면 타입 파라미터 T는 String 타입으로 변경되어 Box 클래스의 내부는 자동으로 재구성된다.

---

## 3. 멀티 타입 파라미터(class<K, V, ...>, interface<K, V, ...>)

- 제네릭 타입은 2개 이상의 멀티 타입 파라미터를 사용할 수 있다.

  ```
  public class Product<T, M>{ // Product<T,M> 제네릭 타입 정의
    private T kind;
    private M model;

    public T getKind() { return this.kind; }
    public M getModel() { return this.moderl; }

    public void setKind(T kind) { this.kind = kind; }
    public void setModel(M model) { this.model = model; }
  }
  ```

- 자바7부터 타입 파라미터의 중복 기술을 줄이기 위해 다이아몬드 연산자<>를 제공한다.

  ```
  Product<Tv, String> product = new Product<Tv, String>(); // 자바6 이전, 제네릭 타입 변수 선언과 객체 생성 코드

  Product<Tv, String> product = new Product<>(); // 자바7~
  ```

## 4. 제네릭 메소드(<T, R> R method(T t))

- 제네릭 메소드는 매개 타입과 리턴 타입으로 타입 파라미터를 갖는 메소드를 말한다.

  ```
  public <타입파라미터, ...> 리턴타입 메소드명(매개변수, ...) {...}

  public <T> Box<T> boxing(T t) {...}
  // 리턴타입: 제네릭 타입 Box<T>
  // 타입 파라미터: T
  ```

- 제네릭 메소드의 호출 방법

  ```
  1. 리턴타입 변수 = <구체적인타입> 메소드명(매개값); //명시적으로 구체적 타입을 지정
  Box<Integer> box = <Integer>boxing(100); //타입 파라미터를 명시적으로 Integer로 지정

  2. 리턴타입 변수 = 메소드명(매개값); //매개값을 보고 구체적 타입을 추정
  Box<integer> box = boxing(100); // 타입 파라미터를 Integer로 추정
  ```

---

## 5. 제한된 타입 파라미터(<T extends 최상위타입>)

- 타입 파라미터에 지정되는 구체적인 타입을 제한할 필요가 있을 경우 **상속 및 구현 관계**를 이용해서 타입을 제한한다.

  - 숫자를 연산하는 제네릭 메소드는 매개값으로 `Number`타입 또는 하위 클래스 타입(`Byte, Short, Integer, Long, Double`)의 인스턴스만 가져야 한다.

- 제한된 타입 파라미터를 선언하려면 타입 파라미터 뒤에 `extends`키워드를 붙이고 상위 타입을 명시하면 된다.
  - 상위타입은 클래스뿐만 아니라 인터페이스도 가능하다.
  - 여기선 인터페이스라고 해서 extends 대신 implements를 사용하지 않는다.
  ```
  public <T extends 상위타입> 리턴타입 메소드(매개변수, ...) {...}
  ```
- 타입 파라미터에 지정되는 구체적인 타입은 **상위 타입이거나 하위 또는 구현 클래스만 가능하다.**
- 주의할 점: 메소드의 중괄호{} 안에서 타입 파라미터 변수로 사용 가능한 것은 상위 타입의 멤버(필드, 메소드)로 제한된다.

  - 하위 타입에만 있는 필드와 메소드는 사용할 수 없다.

  - 예) 숫자 타입만 구체적인 타입으로 갖는 제네릭 메소드 compare()

    ```
    public <T extends Number> int compare(T t1, T t2){
    double v1 = t1.doubleValue(); //Number의 doubleValue() 메소드 사용
    doube v2 = t2.doubleValue();
    return Double.compare(v1, v2);
    }
    ```

    - t1, t2가 사용할 수 있는 메소드와 필드는 모두 Number에 있는 것만 사용가능
    - T 자리에는 Number이거나 Number의 자식 클래스면 다 올 수 있는데 Number의 자식클래스만 가지고 있는 필드나 메소드가 {}안에서 사용된다면 Number는 그것을 못쓰니까 {} 안에서는 Number의 하위 타입에만 있는 필드와 메소드는 사용할 수 없다.

---

## 6. 와일드카드 타입(<?>, <? extends ...>, <? super ...>)

- 코드에서 `?`를 일반적으로 `와일드카드`라고 부른다.

- 제네릭 타입을 `매개변수나 리턴타입으로 사용할 때` 타입 파라미터를 제한할 목적으로 쓴다.

  - [비교] `<T extends 상위 클래스 또는 인터페이스>`는 제네릭 타입과 제네릭 메소드를 `선언할 때` 제한을 한다.

- 와일드 카드 타입의 3가지 형태

```
 1. 제네릭타입<?>: Unbounded Wildcard (제한없음)
 - 타입 파라미터를 대치하는 구체적인 타입으로 모든 클래스나 인터페이스 타입이 올 수 있다.

 2. 제네릭타입<? extends 상위타입>: Upper Bounded Wildcards (상위 클래스 제한)
 - 타입 파라미터를 대치하는 구체적인 타입으로 상위 타입이나 하위 타입만 올 수 있다.

 3. 제네릭타입<? super 하위타입>: Lower Bounded Wildcards (하위 클래스 제한)
 - 타입 파라미터를 대치하는 구체적인 타입으로 하위 타입이나 상위 타입이 올 수 있다.

```

- [예시코드]
- 제네릭 타입 `Course`는 과정 클래스로 과정 이름과 수강생을 저장할 수 있는 배열을 가지고 있다. 타입 파라미터 `T`가 적용된 곳은 수강생 타입 부분이다.

  ```
  public class Course<T> {
    private String name; // 과정이름
    private T[] students; // 수강생 배열

    public Course(String name, int capacity){
      this.name = name;
      students = (T[]) (new Object[capacity]);
      // 타입 파라미터로 배열을 생성하려면
      // new T[n] 형태로는 X
      // (T[]) (new Object[n])으로 생성해야 한다.
    }    public String getName() { return name; }
    public T[] getStudents() { return students; }

    public void add(T t){
      for(int i=0; i<students.length; i++){
        if(students[i] == null){ //배열에 비어있는 부분을 찾아서 수강생 추가
          students[i] = t;
          break;
        }
      }
    }
  }
  ```

  - 수강생이 될 수 있는 타입은 다음 4가지 클래스라고 가정하자

    ![수강될 수 있는 타입](https://postfiles.pstatic.net/MjAyMjAxMTRfMTU5/MDAxNjQyMTU4MDc2OTkx.NIMCgj3_HJVPDKYhETUUKSfuzpgAJ5zzvZfU5cP89eUg.SShJlY3zLkdYZ8fXHKdzXxAREO3sfBdS_iwAMibBuzIg.JPEG.chex417/%EC%99%80%EC%9D%BC%EB%93%9C%EC%B9%B4%EB%93%9C.jpg?type=w773)

    - Course<?>
      : 수강생은 모든 타입이 될 수 있다.
    - Course<? extends Student>
      : 수강생은 Student와 HighStudent만 될 수 있다.
    - Course<? super Worker>
      : 수강생은 Worker, Person만 될 수 있다.

  ```
  public class WildCardExample{

    //registerCourseXXX()메소드의 매개값으로 와일드카드 타입을 사용
    // 모든 수강생이 들을 수 있는 과정 등록
    public static void registerCourse( Courer<?> course ){...}

    // 학생만 들을 수 있는 과정 등록
    public static void registerCourseStudent( Course<? extends Student> course ){...}

    // 직장인과 일반인 과정
    public static void registerCourseWorker( Course<? super Worker> course ){...}


    public static void main(String[] args){

      Course<Person> personCourse = new Course<Person>("일반인과정", 5);
      personCourse.add(new Person("일반인"));
      personCourse.add(new Worker("직장인"));
      personCourse.add(new Student("학생"));
      personCourse.add(new HighStudent("고등학생"));

      Course<Worker> workerCourse = new Course<Worker>("직장인과정", 5);
      workerCourse.add(new Worker("직장인"));

      Course<Student> studentCourse = new Course<Student>("학생과정", 5);
      studentCourse.add(new Student("학생"));
      studentCourse.add(new HighStudent("고등학생"));

      Course<HighStudent> highStudentCourse = new Course<HighStudent>("고등학생과정", 5);
      highStudentCourse.add(new HighStudent("고등학생"));


      //모든 과정 등록 가능
      registerCourse(personCourse);
      registerCourse(workerCourse);
      registerCourse(studentCourse);
      registerCourse(highStudentCourse);


      //학생 과정만 등록 가능
      //registerCourseStudent(personCourse); (X)
      //registerCourseStudent(workerCourse); (X)
      registerCourseStudent(studentCourse);
      registerCourseStudent(highStudentCourse);

      //직장인과 일반인 과정만 등록 가능
      registerCourseWorker(personCourse);
      registerCourseWorker(workerCourse);
      //registerCourseWorker(studentCourse); (X)
      //registerCourseWorker(highStudentCourse); (X)
   }
  }
  ```

---

## 7. 제네릭 타입의 상속과 구현

- 제네릭 타입을 부모 클래스로 사용할 경우

  - 타입 파라미터는 자식 클래스에도 기술해야 한다.

    `public class ChildProduct<T,M> extends Product<T,M>{...}`

  - 추가적인 타입 파라미터를 가질 수 있다.

    `public class ChildProduct<T,M,C> extends Product<T,M>{...}`

- 제네릭 인터페이스를 구현할 경우

  - 타입 파라미터는 구현 클래스에도 기술해야 한다.

    `public class StorageImpl<T> implementsStorage<T> {...}`
