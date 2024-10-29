# Commond 패턴
 
&nbsp;      
&nbsp;    

## Commond 퍠턴이란?
> - 객체의 행위 (메서드) 를 클래스로 만들어 캡슐화하는 패턴

&nbsp;
&nbsp;   

## Commond 패턴의 사용 이유
> -  객체(A) 에서 객체(B)의 메서드를 실행하려면 객체(B)를 참조해야하여 의존성 발생함    
>  이 때 커맨드 패턴을 사용하여 의존성 제거 가능   
> &nbsp;  
> - 기능의 수정이나 변경 시 기존 클래스의 코드 수정 없이 해당 기능에 대한 클래스만 정의하면 되므로   
> 시스템이 확장성과 유연성을 가질 수 있음

&nbsp;
&nbsp;

## 코드 예시
### Commond 패턴 사용 X

```java
public class Light{
    public void lightOn(){
        System.out.println("Light on");
    }
}
```
```java
public class AISpeaker{
    private Light light;
    
    public AISpeaker(Light light){
        this.light = light;
    }
    
    public void talk(){
        light.lightOn();
    }
}
```
```java
public class Client {
    public static void main(String args[]){
    	Light light = new Light();
        AISpeaker aiSpeaker = new AISpeaker(light);
        aiSpeaker.talk();
    }
}
```
**이 상태에서 Heater 를 키는 기능을 가진 Heater 클래스를 추가해보자**

```java
public class Light{
    public void lightOn(){
        System.out.println("Light on");
    }
}
```
```java
public class Heater{
    public void heaterOn(){
        System.out.println("heater on");
    }
}
```
&nbsp;
```java
public class AISpeaker {
	private static String[] modes = {"heater", "light"};
    
	private Light light;
    private Heater heater;
    private String mode;
    
    public AISpeaker(Light light, Heater heater) {
    	this.light = light;
        this.heater = heater;
    }
    
    public void setMode(int index) {
    	this.mode = modes[index];
    }
    
    public void talk() {
    	switch(this.mode) {
        	case "heater":
            	this.heater.heaterOn();
                break;
            case "light":
            	this.light.lightOn();
                break;
        }
    }
}
```
&nbsp;
```java
public class Client {
    public static void main(String args[]){
    	Light light = new Light();
        Heater heater = new Heater();
        AISpeaker aiSpeaker = new AISpeaker(light, heater);
        
        aiSpeaker.setMode(0); // heater
        aiSpeaker.talk();
        
        aiSpeaker.setMode(1); //light
        aiSpeaker.talk();
    }
}
```

> 이런식으로 코드를 작성하다보면 기능이 늘어날 때마다 속성값이 계속 들어날 것이고   
> 기존 코드를 계속해서 수정해야하며 talk 메서드의 분기 또한 하염없이 늘어날 것이다.(OCP 위반)

&nbsp;   

##### 이제 커맨트 패턴을 사용하여 코드를 작성해보겠다.


### Commond 패턴 사용 O

```java
// commond interface 정의
public interface Commond{
    public void run();
}
```
&nbsp;
```java
public class Heater{
    public void heaterOn(){
        System.out.println("heater on");
    }
}
```
```java
// Heater Commond 구현 클래스
public class HeaterOnCommond implements Commond{
    private Heater heater;
    
    public HeaterOnCommond(Heater heater){
        this.heater = heater;
    }
    
    @Override
    public void run(){
        heater.heaterOn();
    }
}
```
&nbsp;
```java
public class Light{
    public void lightOn(){
        System.out.println("Light on");
    }
}
```
```java
public class LightOnCommond implements Commond{
    private Light light;
    
    public LightOnCommond(Light light){
        this.light = light;
    }
    
    @Override
    public void run(){
        light.lightOn();
    }
}
```
&nbsp;
```java
public class AISpeaker {
	private Command command;
    
    public void setCommand(Command command) {
    	this.command = command;
    }
    
    public void talk() {
    	command.run();
    }
}
```
&nbsp;
```java
public class Client {
    public static void main(String args[]){
    	Light light = new Light();
        Heater heater = new Heater();
        
        Command heaterOnCommand = new HeaterOnCommand(heater);
        Command lightOnCommnad = new LightOnCommand(light);
        
        AISpeaker aiSpeaker = new AISpeaker();
        
        aiSpeaker.setCommand(heaterOnCommand);
        aiSpeaker.talk();
        
        aiSpeaker.setCommand(lightOnCommnad);
        aiSpeaker.talk();
    }
}
```
**이 이후에도 새로운 기능을 추가 하고 싶으면 해당 클래스를 추가하면 되기 때문에 OCP에 위반 되지 않는다.**