# 추상 클래스 VS 인터페이스

## 인터페이스 VS 추상클래스 비교
|              | **추상클래스**| **인터페이스**         |   
|:-------------|:------------|:------------------|
| **사용 키워드**   | abstract| interface         |
| **사용 가능 변수** | 제한 없음| static final( 상수 ) |
|**사용 가능 접근제어자**| 제한 없음|public|
|**사용 가능 메서드**| 제한 없음 |abstract method, default method, static method, private method|
|**상속 키워드**| extends|implements|
|**다중 상속 가능 여부**| 불가능  |가능(클래스의 다중 구현, 인터페이스 끼리의 다중 상속)|


|         | **추상클래스** / **인터페이스**                                                                                                                                                                     |   
|:--------|:------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| **공통점** | 1. 추상 메소드를 가지고 있어야 한다. <br><br>  2.인스턴스화 할 수 없다 (new 생성자 사용 X) <br>  <br> 3. 인터페이스 혹은 추상 클래스를 상속받아 구현한 구현체의 인스턴스를 사용해야 한다. <br>  <br> 4. 인터페이스와 추상클래스를 구현, 상속한 클래스는 추상 메소드를 반드시 구현하여야 한다. |

&nbsp;   
&nbsp;   

## 추상클래스를 사용하는 경우
> - 상속 받을 클래스들이 공통으로 가지는 메소드와 필드가 많아 `중복 멤버 통합`을 할 때
> - 멤버에 public 이외의 접근자(private, protected) 선언이 필요한 경우
> - non-static, non-final 필드 선언이 필요한 경우  
>  **(각 인스턴스에서 상태 변경을 위한 메소드가 필요한 경우)**
> - 추상 클래스는 이를 상속할 각 객체들의 공통점을 찾아 추상화시켜 놓은 것으로,    
> 상속 관계를 타고 올라갔을 때 같은 부모 클래스를 상속하며 부모 클래스가 가진 기능들을 구현해야할 경우 사용한다.
#### 예시 코드
```java
abstract class Exam { // 추상클래스
    int kor;
    int eng;
    int math;

    abstract void total();
    abstract void avg();
}

class NewlecExam extends Exam { //상속
    int com;

     @Override
    void total(){
        int sum = kor + eng + math + com;
        System.out.println("NewlecExam 총점: " + sum);
    }

    @Override
    void avg(){
        int sum = kor + eng + math + com;
        double average = sum / 4.0; // 과목 개수 4로 나눔
        System.out.println("NewlecExam 평균: " + average);
    }
}

class YBMExam extends Exam { // 상속
    int toeic;

    @Override
    void total(){
        int sum = kor + eng + math + toeic;
        System.out.println("YBMExam 총점: " + sum);
    }

    @Override
    void avg(){
        int sum = kor + eng + math + toeic;
        double average = sum / 4.0; // 과목 개수 4로 나눔
        System.out.println("YBMExam 평균: " + average);
    }
}
```

&nbsp;   
&nbsp;   

## 인터페이스를 사용하는 경우
> - 어플리케이션의 기능을 정의 해야하지만 그 구현 방식이나 대상에 대해 추상화 할 때
> - 서로 관련성이 없는 클래스들을 묶어 주고 싶을 때 (형제 관계)
> - `다중 상속(구현)`을 통한 추상화를 설계해야 할 때
> - 특정 데이터 타입의 행동을 명시하고 싶은데,  
>   어디서 그 행동이 구현되는지 신경 쓰지 않는 경우.
> - 클래스와 별도로 `구현 객체가 같은 동작을 한다`는 것을 보장하기 위해 사용
#### 예시 코드
```java
public interface Animal {
    void sound(); // 인터페이스 메서드 (추상 메서드)
    void eat();
} 
```
```java
public class Dog implements Animal {
    @Override
    public void sound() {
        System.out.println("Bark");
    }
    
    @Override
    public void eat() {
        System.out.println("Dog is eating");
    }
}


public class Cat implements Animal {
    @Override
    public void sound() {
        System.out.println("Meow");
    }

    @Override
    public void eat() {
        System.out.println("Cat is eating");
    }
}
```
```java
public class Main {
    public static void main(String[] args) {
        Animal dog = new Dog(); // Animal 인터페이스 타입으로 Dog 객체 생성
        Animal cat = new Cat(); // Animal 인터페이스 타입으로 Cat 객체 생성
        
        dog.sound(); // 출력: Bark
        dog.eat();   // 출력: Dog is eating
        
        cat.sound(); // 출력: Meow
        cat.eat();   // 출력: Cat is eating
    }
}
```


&nbsp;   
&nbsp;

### 정리하자면..
> **인터페이스는 규칙(규약/강제)에 따라 다른 클래스들이 다양한 방식으로 기능을 구현할 수 있게 하고,   
>  추상 클래스는 공통 기능을 미리 구현하여 중복을 줄이고 코드 재사용을 높이는 역할을 한다는 것 같다**