---
title: "🚓🚨 경찰아저씨 Java 빨리 자바주세요 🚨🚓"
date: 2023-12-22T11:30:03+00:00
# weight: 1
# aliases: ["/first"]
tags: ["Java"]
categories: ["Java"]
author: "Me"
# author: ["Me", "You"] # multiple authors
showToc: true
TocOpen: false
draft: false
hidemeta: false
comments: false
description: "Desc Text."
canonicalURL: "https://canonical.url/to/page"
disableHLJS: true # to disable highlightjs
disableShare: false
disableHLJS: false
hideSummary: false
searchHidden: true
ShowReadingTime: true
ShowBreadCrumbs: true
ShowPostNavLinks: true
ShowCodeCopyButtons: true
ShowWordCount: true
ShowRssButtonInSectionTermList: true
UseHugoToc: true
cover:
    image: cover/java.png
    alt: "<alt text>" # alt text
    caption: "<text>" # display caption under cover
    relative: false # when using page bundles set this to true
    hidden: false # only hide on current single page
editPost:
    URL: "https://github.com/<path_to_repo>/content"
    Text: "Suggest Changes" # edit text
    appendFilePath: true # to append file path to Edit link
---
# < 01. 객체 지향 프로그래밍 >

### [ ⬇︎ static ⬇︎ ]

~~~
class MyOop {
    public void A() {                           // m1 인스턴스 때문에 static 제거
        System.out.println("A");
    }
}
public class Oop {
    public static void main(String[] args) {
        MyOop m1 = new MyOop();                 // m1 == 인스턴스
        m1.A();                                 // A 출력
    }
}
~~~

---
---

# < 02. 상속 >

### [ ⬇︎ Overriding && Overloading ⬇︎ ]
~~~
class Cal {
    public int sum(int v1, int v2) {            // c라는 인스턴스 때문에 static 제거
        return v1 + v2;
    }
    // Overloading
    // 기존 메소드에 기능을 추가하는 것
    // 메소드에 사용되는 이름을 절약할 수 있음
    public int sum(int v1, int v2, int v3) {    // c라는 인스턴스 때문에 static 제거
        return v1 + v2 + v3;
    }
}
class Cal3 extends Cal {
    public int minus(int v1, int v2) {          // c3라는 인스턴스 때문에 static 제거
        return v1 - v2;
    }
    // Overriding
    // 기존 메소드를 재정의하여 덮어씌움
    public int sum(int v1, int v2) {            // c3라는 인스턴스 때문에 static 제거
        System.out.println("test")              // Overriding 테스트용
        return v1 + v2;
    }
}
public class Inheritance {
    public static void main(String[] args) {
        Cal c = new Cal();
        System.out.println(c.sum(2, 1));
        
        Cal3 c3 = new Cal3();
        System.out.println(c3.sum(2, 1));       // test와 1 출력
        System.out.println(c3.minus(2, 1));     
    }
}
~~~

---

### [ ⬇︎ this && super ⬇︎ ]

~~~
class Cal {
    public int sum(int v1, int v2) {
        return v1 + v2;
    }
    // Overloading
    // 기존 메소드에 기능을 추가하는 것
    // 메소드에 사용되는 이름을 절약할 수 있음
    public int sum(int v1, int v2, int v3) {
        return this.sum(v1, v2) + v3;           // 본인의 sum 함수를 받아옴
    }
}
class Cal3 extends Cal {
    public int minus(int v1, int v2) {
        return v1 - v2;
    }
    // Overriding
    // 기존 메소드를 재정의하여 덮어씌움
    public int sum(int v1, int v2) {
        return super.sum(v1 + v2);              // 부모의 sum 함수를 받아옴
    }
}
public class Inheritance {
    public static void main(String[] args) {
        Cal c = new Cal();
        System.out.println(c.sum(2, 1));
        
        Cal3 c3 = new Cal3();
        System.out.println(c3.sum(2, 1, 1));    // Overloading된 sum 함수를 이용해 4 출력
        System.out.println(c3.minus(2, 1));     
    }
}
~~~

---

### [ ⬇︎ 상속 && 생성자 ⬇︎ ]

~~~
class Cla {
    int v1, v2;
    // 생성자
    Cal(int v1, int v2) {
        System.out.println("Cal");
        this.v1 = v1;
        this.v2 = v2;
    }
    public int sum() {
        return this.v1 + v2;
    }
}
class Cal3 extends Cal {
    // 부모 클래스의 생성자를 실행 (안하면 오류)
    Cal3(int v1, int v2) {
        System.out.println("Cal3");
        super(v1, v2);
    }
    public int minus() {
        return this.v1 - v2;
    }
}
public class Inheritance {
    public static void main(String[] args) {
        Cal c = new Cal(2, 1);                  // Cal 출력
        Cal3 c3 = new Cal(2, 1);                // 부모 생성자의 Cal과 본인의 Cal3 출력
                                                // Cal, Cal, Cal3
        System.out.println(c3.sum());           // 3        
        System.out.println(c3.minus());         // 1
    }                                           
}
~~~

---
---

# < 03. Interface >

### [ ⬇︎ 인터페이스의 형식 ⬇︎ ]

~~~
interface Calculable {                                   // 인터페이스는 class의 형태를 규정함 (약속)
    double PI = 3.14;                                    // 인터페이스에서 변수를 정의할때는 내용 O
    int sum(int v1, int v2);
}
interface Printable {
    void print();                                        // 인터페이스에서 메소드를 정의할때는 내용은 X
}
class RealCal implements Calculable, Printable {         // implements 한다면,
    public int sum(int v1, int v2) {                     // interface에 있는 메소드를 반드시 구현해야함
        return v1 + v2;
    }
    public void print() {
        System.out.println("Hello");                     // Printable의 print() 메소드를 구현
    }
}
class DummyCal implements Calculable {                   // implements 한다면,
    public int sum(int v1, int v2) {                     // interface에 있는 메소드를 반드시 구현해야함
        return 3;
    }
}
public class InterfaceApp {
    public static void main(String[] args) {
        RealCal c = new RealCal();
        System.out.println(c.sum(2, 1));                 // 3 출력
        c.print();                                       // Hello 출력
        System.out.println(c.PI);                        // 3.14 출력
    }
}
~~~

---

### [ ⬇︎ 다형성 ⬇︎ ]

~~~
interface Printable {
    void print();
}
class AdvancedPrint implements Printable {
    public void print() {
        System.out.println("Hello");
    }
}
public class InterfaceApp {
    public static void main(String[] args) {
        Printable c = new AdvancedPrint();      // 클래스가 데이터 타입을 뭘로 하냐에 따라 다양한 결과를 얻어낼 수 있게됨
        c.print();
    }
}
~~~

---
---