# Strategy Pattern
객체들이 할 수 있는 행위 각각에 대해 전략 클래스를 생성하고, 유사한 행위들을 캡슐화 하는 인터페이스를 정의하여,
객체의 행위를 동적으로 바꾸고 싶은 경우 직접 행위를 수정하지 않고 전략을 바꿔주기만 함으로써 행위를 유연하게 확장하는 방법

-> 메소드 별로 나뉘어 의존관계를 주입한 모델

# Model
![strategy pattern](https://github.com/hohwanm1234/Study/assets/46438755/0c31bf49-d64b-4a01-a9d9-684eec0cdf78)

-> Context -> strategy 의존관계
-> Context는 바뀔일이 없음
-> 의존관계 주입(예시)
* 클래스가 계속 변화할 경우 (OCP - 개방/폐쇄 원칙 위배)

# Template - CallBack Pattern
전략패턴의 변형된 형태로써, 전략패턴의 기본적 구조에 변화되는 부분을 매번 클래스로 만들지 않고, 익명 내부 클래스를 바로 생성하여 사용

-> 템플릿-콜백 패턴이란 정해진 틀 안에서, 변화되는 부분만 유동적으로 받아 수행하는 패턴

# 예시 소스
class MyClass {
    void myMethod(PrintB printB) {
        a();
        printB.b();
        c();
    }

    void a() {
        System.out.println("A");
    }

    void c() {
        System.out.println("C");
    }
}

interface PrintB {
    void b();
}

public class Main {
    public static void main(String[] args) {
        MyClass myClass = new MyClass();

        myClass.myMethod(()-> System.out.println("B1"));
        myClass.myMethod(()-> System.out.println("B2"));
    }
}

