# OOP(Object Oriented Programming, 객체지향 프로그래밍)
Dart OOP에 대해 정리한다. 예시코드를 포함한 모든 정보는 ChatGPT를 사용했습니다.
## 객체지향 프로그래밍(OOP)이란?
- 정의: 객체(데이터 + 메서드)를 중심으로 프로그램을 설계하는 패러다임. 클래스는 객체의 설계도, 인스턴스는 그 설계도로 만든 실체이다.
- Dart에서의 특징: 클래스 기반, 단일 상속, 믹스인(mixin), 모든 클래스는 암묵적 인터페이스로 사용 가능, 추상 클래스 지원, 강한 null-safety, `final`·`const`로 불변성 지원 등이 있다.
- 사용 이유: 복잡한 시스템을 모듈화(캡슐화), 재사용(상속/구성), 확장성(다형성) 있게 설계하여 유지보수·테스트·협업을 쉽게 하기 위함이다.

## Class
- 정의: 객체를 만들기 위한 설계도이며, 필드(상태)와 메서드(행동)를 가진다.
- 기본 문법
  ```dart
  class Person {
  String name;
  int age;

  Person(this.name, this.age); // 생성자(constructor)

  void sayHello() => print('Hi, I am $name');
  }
  ```
- 사용 이유: 관련 데이터와 로직을 한곳에 묶어 책임을 분리하고 재사용·추상화를 쉽게 한다.
- 주의: `_` 접두사는 파일(라이브러리) 단위 비공개이다(같은 파일 안에서 접근은 가능하다).

## Instance
- 정의: 클래스로부터 실제로 생성된 객체(메모리 상의 실체)이다.
- 생성 예
  ```dart
  var p = Person('Alice', 30);
  p.sayHello();
  ```
- 이유: 클래스는 설계도일 뿐이며 인스턴스가 실제 동작과 상태를 가진다. 같은 클래스의 여러 인스턴스는 서로 다른 상태를 가질 수 있다.

## Constructor (생성자)
- 정의: 인스턴스가 생성될 때 초기화하는 특수 메서드이다.
- 종류와 예
  ```dart
  class Point {
  final int x, y;
  Point(this.x, this.y);                     // 기본 생성자
  Point.origin() : x = 0, y = 0;             // 네임드 생성자 + 초기화 리스트
  Point.copy(Point other) : x = other.x, y = other.y; // 복사 생성자
  factory Point.cached(int x, int y) {       // factory: 생성 제어(캐시/싱글턴)
    // 캐시 로직 예시(간단)
    return Point(x, y);
    }
  const Point.constPoint(this.x, this.y);    // const 생성자: 컴파일타임 상수
  }
  ```
- 추가
   - 명명된 매개변수와 `required` 사용:
     ```dart
     class Person {
        final String name;
        final int age;
        Person({required this.name, this.age = 0});
     }
     ```
- 주의: `const` 생성자는 모든 필드가 `final`이어야 한다. `factory` 생성자는 값을 반환해야 한다.

## Immutable programming (불변성)
- 정의: 객체의 상태를 변경하지 않는 방식이다.
- Dart에서 구현: `final` 필드 + `const` 생성자 또는 내부에서 가변 참조를 노출하지 않는다.
  ```dart
  class ImmutablePoint {
  final int x, y;
  const ImmutablePoint(this.x, this.y);
  }
  ```
- 중요: `final`은 참조 불변을 보장하지만, 참조가 가리키는 객체(예: `List`)는 여전히 변경될 수 있다(얕은 불변). 컬렉션 불변을 원하면 `const` 컬렉션 또는 불변 뷰를 사용하거나 복사(copy-on-write) 패턴을 고려해야한다.
- 이유: 동시성 안전성, 예측 가능한 동작, 디버깅/테스트 용이성.

## getter / setter
- 정의: 필드 접근을 캡슐화하는 특수 메서드로 계산된 값 제공·입력 검증 등에 사용한다.
- 문법
  ```dart
  class Rectangle {
  double _width, _height; // private (파일 단위)
  Rectangle(this._width, this._height);

  double get area => _width * _height; // 계산된 getter

  double get width => _width;
  set width(double value) { // setter로 검증 가능
    if (value <= 0) throw ArgumentError('width must be > 0');
    _width = value;
    }
  }
  ```
- 주의: 계산 비용이 큰 getter는 캐싱을 고려, 불필요한 setter는 불변성 원칙과 충돌하므로 주의해야 한다.

## Inheritance (상속)
- 정의: 한 클래스가 다른 클래스의 구현(필드/메서드)을 물려받는 것. Dart는 단일 상속(extends)을 사용한다.
- 문법/예
  ```dart
  class Animal {
  void speak() => print('...');
  }
  class Dog extends Animal {
  @override
  void speak() => print('bark');
  }
  ```
- 사용 이유: 공통 동작 재사용, 다형성 제공.
- 주의: 과도한 상속은 결합도를 높이므로 가능하면 composition over inheritance 권장한다(필요 시 `implements`나 `mixin` 사용).

## method vs function
- 정의:
 - Method: 클래스의 멤버 함수(인스턴스/정적)이다.
 - Function: 독립 함수(top-level 또는 로컬)이다.
- 예
  ```dart
  // top-level function
  int add(int a, int b) => a + b;

  class Calculator {
  int multiply(int a, int b) => a * b; // instance method
  static int square(int x) => x * x;  // static method
  }
  ```
- 언제 사용: 상태와 연관된 동작은 메서드, 독립적인 유틸리티는 top-level 함수(또는 extension)를 권장한다.

## Override (`@override`)
- 정의: 상위클래스(또는 인터페이스)의 메서드를 하위클래스에서 재정의할 때 사용하며, 애너테이션은 선택이지만 권장된다.
- 예
  ```dart
  class Animal {
  void speak() => print('...');
  }
  class Cat extends Animal {
  @override
  void speak() => print('meow');
  }
  ```
- 이유: 의도를 명확히 하고 컴파일러의 시그니처 일치 검사 도움.

## Static
- 정의: 클래스 인스턴스가 아닌 클래스 자체에 속하는 멤버(필드/메서드). 인스턴스 상태를 참조할 수 없다.
- 예
  ```dart
  class Util {
  static int square(int x) => x * x;
  }
  class Counter {
  static int total = 0;
  Counter() { total++; }
  }
  ```
- 사용 이유: 공용 유틸, 클래스 단위 상태 관리(테스트 주의).
- 주의: 전역 상태(`static` 변수)는 테스트·병렬성·부작용 측면에서 문제를 일으킴.

## Implements / Interface
- 정의:
   - Interface: Dart에서는 모든 클래스가 인터페이스로 사용될 수 있다(암묵적 인터페이스).
   - implements: 특정 클래스(또는 추상클래스)가 제공하는 멤버 시그니처를 강제 구현하도록 요구(기본 구현 상속 없음).
- 예
  ```dart
  abstract class Logger {
  void log(String msg);
  }
  class ConsoleLogger implements Logger {
  @override
  void log(String msg) => print(msg);
  }
  ```
- 사용 이유: 구현과 API(계약)를 분리하여 느슨한 결합을 만들고 테스트 더블(Mock)을 쉽게 만들기 위해.

## Generic (제네릭)
- 정의: 타입 매개변수를 사용해 코드 재사용과 타입 안전성을 높이는 기법이다.
- 예
  ```dart
  class Box<T> {
  T value;
  Box(this.value);
  }
  var intBox = Box<int>(123);
  ```
- 이유: 런타임 캐스팅을 줄이고 컴파일 타임에 타입 오류를 잡기 위함.
- 주의(variance): 컬렉션 타입 캐스팅 문제에 주의. 예를 들어 `List<Cat>`을 `List<Animal>`로 바로 취급할 수 없다.
