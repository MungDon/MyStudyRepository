# MVVM 패턴

&nbsp;   
&nbsp;

## MVVM 패턴이란?
> - Model, View, ViewModel 의 약자   
> - 애플리케이션의 비즈니스 로직과 프레젠테이션 로직을 UI로 명확하게 분리하는 패턴


## Model
> - 데이터와 비즈니스 로직을 담당하는 부분
> - 데이터를 저장하거나 가져오는 역할을 수행
> - 보통 데이터베이스, 네트워크 요청 또는 파일 시스템과 같은 데이터 소스와 상호 작용한다.    
> 
> **※ MVC 패턴에서의 Model 과 같음**

&nbsp;   

## View
> - 사용자 인터페이스를 담당하는 부분(UI)
> - 데이터를 화면에 표시
> 
> **※ MVC 패턴에서의 View와 같음**

## ViewModel
> - View 를 표현하기 위해 만들어진 View 만을 위한 Model
> - Model 을 View 에 표시하기 위한 처리를 하는 부분
> - Model 로 부터의 결과를 View 에 통지하고, View 의 요청에 따라 로직을 실행
> 
> **※ ViewModel 의 특징은 Data Binding 과 캡슐화된 [Commond 패턴](https://github.com/MungDon/MyStudyRepository/blob/master/DesignPattern/%5B3%5DCommond_pattern.md)을 이용하여   
> &nbsp;&nbsp;&nbsp;&nbsp; 
> View 와 Model 간 결합도를 없애고 View 와 Model 사이에서 중간 관리자 역할을 수행한다.**


&nbsp;   
&nbsp;

## MVVM 패턴 동작 방식
> 1. View 를 통해 사용자 Action 이 들어온다.
> 2. View 에 Action이 들어오면 Commond 패턴으로 Action 을 ViewModel 에 전달한다.
> 3. ViewModel 은 Model 에 데이터를 요청한다.
> 4. Model 은 응답 데이터를 ViewModel 에 전달한다.
> 5. View 는 ViewModel 과 함께 Data Binding 하여 화면을 나타낸다.


&nbsp;   
&nbsp;


## MVVM 패턴의 장점
> - View 와 Model 의 독립성 유지 가능
> - 독립성을 유지하기 때문에 효율적인 유닛 테스트 가능
> - Data Binding을 통해 View와 ViewModel 간 데이터의 자동 동기화가 이루어져서 수작업 코드가 줄어듬

&nbsp;   

## MVVM 패턴의 단점
> - ViewModel 설계가 쉽지 않다.    