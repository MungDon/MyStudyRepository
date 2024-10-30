# OOP의 4가지 특성

&nbsp;   
&nbsp;   

## 캡슐화
> - 연관된 데이터와 기능을 하나로 묶고, 불필요한 요소를 외부에 노출되지 않도록 설계하는 방식
> - 자바에서는 접근 제어자(private, protected, default, public)를 통해 캡슐화를 구현 가능
> - 캡슐화를 통해 객체 간의 결합도를 낮추고, 코드의 재사용성을 높이며, 정보 은닉을 통해 안정성이 향상 된다.
#### 예시 코드
```java
public class Student{
    private int id;
    private String name;
    
    //getter
    public int getId(){
        return id;
    }
    
    public String getName(){
        return name;
    }
    
    //setter
    public void setId(int id){
        this.id = id;
    }
    
    public void setName(String name){
        this.name = name;
    }
}
```
```java
public class Main{
    public static void main(String[] args){
        Student student = new Student();
        
        // student.id = 1;
        // student.name = "민형";
        // Student 객체의 필드변수는 접근제어자가 private 이기 때문에 외부에서 접근 불가능하다.
        
        student.setId(1);
        student.setName("민형");
        // 이처럼 접근제어자가 public 인 set 메서드를 통해서 값을 저장할 수 있다. 
    }
}
```


&nbsp;   
&nbsp;   

## 추상화
> - 클래스들의 공통적인 요소를 뽑아내 상위 클래스를 만들어 내는 것
> - 공통적인 속성과 기능을 정의함으로 코드의 중복을 줄이고, 클래스 간 관계를 효과적으로 설정하여 유지보수를 용이하게함
> - 자바에서는 [추상 클래스와 인터페이스]()라는 요소를 통해 추상화를 구현 가능
#### 예시 코드
```java
// Car 인터페이스
public interface Car{
    void engine();
    void drive();
    void refuel();
}
```
```java
public class BMWX6 implements Car{
    @Override
    public void engine(){
        System.out.println("V8 엔진");
    }
    
    @Override
    public void drive(){
        System.out.println("4륜구동");
    }
    
    @Override
    public void refuel(){
        System.out.println("가솔린");
    }
}
```
```java
public class BenzGLS implements Car{
    @Override
    public void engine(){
        System.out.println("V8 엔진");
    }
    
    @Override
    public void drive(){
        System.out.println("4륜구동");
    }
    
    @Override
    public void refuel(){
        System.out.println("가솔린");
    }
}
```

&nbsp;   
&nbsp;   

## 상속
> - 부모클래스의 속성과 기능을 그대로 이어받아 사용할 수 있게하고    
    기능의 일부분을 변경해야 할 경우 상속받은 자식 클래스에서 해당 기능만 다시 정의하여 사용 할 수 있게 하는것
> - 상속을 통해 기존에 작성된 클래스를 재활용 할 수 있게되고, 공통된 필드 변수나 메서드를 부모 클래스에 작성해 놓으면 코드의 중복을 줄일 수 있다.
>   또한, 클래스 간의 계층적 관계를 구성함으로 다형성의 문법적 토대를 마련한다.
#### 예시 코드
```java
// 부모 클래스
public class Animal {
    protected String name; 

    public Animal(String name) {
        this.name = name;
    }

    public void speak() {
        System.out.println(name + "가 소리를 냅니다.");
    }
}
```
```java
// 자식 클래스
public class Dog extends Animal {
    public Dog(String name) {
        super(name); // 부모 클래스의 생성자 호출
    }

    @Override
    public void speak() {
        System.out.println(name + "가 멍멍하고 짖습니다.");
    }
}
```
```java
// 사용 예시
public class Main {
    public static void main(String[] args) {
        Dog dog = new Dog("바둑이");
        dog.speak(); // "바둑이 가 멍멍하고 짖습니다." 출력
    }
}
```

&nbsp;   
&nbsp;   

## 다형성
> - 하나의 객체나 메서드가 다양한 형태로 동작할 수 있는 능력
> - 상속 관계에서 부모 클래스 타입으로 자식 클래스 객체를 다룰 수 있으며(업캐스팅),    
> 이를 통해 다양한 자식 클래스의 객체를 일관된 방식으로 처리 가능하여 코드의 유연성과 재사용성이 증가함
> - 다형성의 형태로는 메서드 오버로딩(컴파일 타임 다형성), 메서드 오버라이딩(런타임 다형성), 업캐스팅 등이 있음
#### 예시 코드
```java
// 부모 클래스
public class Animal {
    public void speak() {
        System.out.println("동물이 소리를 냅니다.");
    }
}
```
```java
// 자식 클래스
public class Cat extends Animal {
    @Override
    public void speak() {
        System.out.println("야옹!");
    }
}
```
```java
// 자식 클래스
public class Dog extends Animal {
    @Override
    public void speak() {
        System.out.println("멍멍!");
    }
}
```
```java
// 사용 예시
public class Main {
    public static void main(String[] args) {
        Animal myAnimal; // 부모 클래스 타입으로 선언

        myAnimal = new Dog(); // Dog 객체를 부모 클래스 타입으로 참조
        myAnimal.speak(); // "멍멍!" 출력

        myAnimal = new Cat(); // Cat 객체를 부모 클래스 타입으로 참조
        myAnimal.speak(); // "야옹!" 출력
    }
}
```


&nbsp;   
&nbsp;   


### 오버라이딩
> - 부모 클래스에서 상속 받은 메서드를 자식 클래스에서 재정의 하는것
> - 오버라이딩 하고자 하는 메서드의 이름, 매개변수, 리턴값이 모두 같아야 함.
#### 예시 코드
```java
// 부모 클래스
public class Animal {
    public void speak() {
        System.out.println("동물이 소리를 냅니다.");
    }
}
```
```java
// 자식 클래스
public class Cat extends Animal {
    @Override
    public void speak() {
        System.out.println("야옹!");
    }
}
```

&nbsp;


### 오버로딩
> - 한 클래스 내에서 동일한 이름을 가진 여러 메서드를 정의할 수 있으며,    
> 이때 매개변수의 타입, 개수, 순서가 다르면 서로 다른 메서드로 간주됨.
> - 메서드 오버로딩을 통해 같은 이름의 메서드를 사용하더라도   
> 다양한 입력에 대해 다른 동작을 수행할 수 있어 코드의 가독성과 유지보수성을 높일 수 있음.
> - 오버로딩의 대표적인 예로는 System.out.println() 메서드와 생성자 오버로딩이 있으며,   
> 이 메서드는 다양한 데이터 타입을 인자로 받아 서로 다른 동작을 수행함.

#### 예시 코드
```java
public class OverloadExample {
    // 정수형 매개변수를 받는 add 메서드
    public int add(int a, int b) {
        return a + b;
    }

    // 실수형 매개변수를 받는 add 메서드
    public double add(double a, double b) {
        return a + b;
    }

    // 세 개의 정수형 매개변수를 받는 add 메서드
    public int add(int a, int b, int c) {
        return a + b + c;
    }
}
```