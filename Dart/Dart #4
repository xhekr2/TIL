# Async 프로그래밍

다트 언어는 동기/비동기 프로그래밍을 지원한다. 동기는 요청하고 나서 응답이 올 때까지 더는 코드를 진행하지 못하고 기다렸다가 응답을 받으면 그제서야 다음 코드를 진행한다. 반면에 비동기는 요청하고 나서 응답을 받지 않았는데도 대기하지 않고 다음 코드를 진행한다. 언제든 응답이 오면 즉시 응답을 처리하게 된다.

## Future

Future 클래스는 미래 라는 단어의 의미대로 미래에 받아올 값을 뜻한다. List나 Set처럼 제네릭으로 어떤 미래의 값을 받아올지를 정할 수 있다.

```dart
Future<String> name; // 미래에 받을 String값
Future<int> number; // 미래에 받을 int값
Future<bool> isOpened // 미래에 받을 boolean값
```

비동기 프로그래밍은 서버 요청과 같이 오래 걸리는 작업을 기다린 후 값을 받아와야 하기 때문에 미래값을 표현하는 Future 클래스가 필요하다. 특정 기간 동안 아무것도 하지 않고 기다리는 Future.delayed()를 사용해보겠다.

```dart
void main() {
	addNumbers(1, 1);
}

void addNumbers(int number1, int number2) {
	print('$number1 + $number2 계산 시작');
	
	// Future.delayed()를 사용하면 일정 시간 후에 콜백 함수를 실행할 수 있다.
	Future.delayed(Duration(seconds: 3)), () {
		print('$number1 + $number2 = ${number1 + number2}');
		
	});
	
	print('$number1 + $number2 계산 끝');
}
```

- 실행 결과
    
    1 + 1 계산 시작
    
    1 + 1 계산 끝
    
    1 + 1 = 2
    

첫 번째 매개변수에 대기할 기간을 입력하고 두 번째 매개변수에 대기 후 실행할 콜백 함수를 입력하면 된다. addNumbers() 함수는 print() 함수를 실행하고 Future.dealyed()를 통해 3초간 대기한다. 그 다음 마지막 print() 함수를 실행하고 함수를 마친다. 하지만 Future.delayed()는 비동기 연산이기 때문에 CPU가 3초간 대기해야 한다는 메시지를 받으면 리소스를 허비하지 않고 다음 코드를 바로 실행한다. 그래서 작성한 코드의 순서와 다르게 값이 출력된다. 결과적으로 CPU가 아무것도 하지 않으면 낭비할 뻔한 시간(여기서는 3초) 동안 다른 작업을 할 수 있어 더 효율적으로 CPU 리소스를 사용했다.

## async와 await

그런데 코드가 작성된 순서대로 실행되지 않는다면 개발자 입장에서 헷갈릴 수 있다. 이때 async와 await 키워드를 사용하면 비동기 프로그래밍을 유지하면서도 코드 가독성을 유지할 수 있다.

```dart
void main() {
	addNumbers(1, 1);
}

// async 키워드는 함수 매개변수 정의와 바디 사이에 입력한다.
Future<void> addNumbers(int number1, int number2) async {
	print('$number1 + $number2 계산 시작');
	
	// await는 대기하고 싶은 비동기 함수 앞에 입력한다.
	await Future.delayed(Duration(seconds: 3)), () {
		print('$number1 + $number2 = ${number1 + number2}');
	});
	
	print('$number1 + $number2 계산 끝');
}
```

- 실행 결과
    
    1 + 1 계산 시작
    
    1 + 1 = 2
    
    1 + 1 계산 끝끝
    

함수를 async로 지정해주고 나서 대기하고 싶은 비동기 함수를 실행할 때 await 키워드를 사용하면 코드는 작성한 순서대로 실행된다. async와 await 키워드를 사용하면 비동기 프로그래밍 특징을 그대로 유지함 코드가 작성된 순서대로 프로그램을 실행한다. addNumbers() 함수를 두 번 실행해보겠다.

```dart
void main() {
	addNumbers(1, 1);
	addNumbers(2, 2);
}
// 아래 코드는 생략
```

- 실행 결과
    
    1 + 1 계산 시작
    
    2 + 2 계산 시작
    
    1 + 1 = 2
    
    1 + 1 계산 끝
    
    2 + 2 = 4
    
    2 + 2 계산 끝
    

addNumbers() 함수는 두 번 실행되었다. 그러니 출력 결과를 함수별로 나눠서 보면 각 addNumbers() 함수의 실행 결과가 예상한 코드 순서대로 시작되었다. 그런데 addNumbers(1, 1)가 끝나기 전에 addNumbers(2, 2)가 실행되었다. 그 이유는 addNumbers() 함수가 비동기 프로그래밍으로 실행되었기 때문이다. addNumbers(1, 1)의 Future.delayed() 가 실행되며 3초를 기다려야 할 때 CPU의 리소스가 낭비되지 않고 바로 다음 실행할 코드인 addNumbers(2, 2)를 실행한 것이다.

만약 addNumbers(1, 1)과 addNumbers(2, 2)가 순차적으로 실행되길 원한다면 아래와 같이 async와 await 키워드를 추가해주면 된다.

```dart
void main() async {
	await addNumbers(1, 1);
	await addNumbers(2, 2);
}

// async 키워드는 함수 매개변수 정의와 바디 사이에 입ㄺ한다.
Future<void> addNumbers(int number1, int number2) async {
	print('$number1 + $number2 계산 시작');
	
	// await는 대기하고 싶은 비동기 함수 앞에 입력한다.
	await Future.delayed(Duration(seconds: 3), () {
		print('$number1 + $number2 = ${number1 + number2}');
	});
	
	print('$number1 + $number2 계산 끝');
}	
```

- 실행 결과
    
    1 + 1 계산 시작
    
    1 + 1 = 2
    
    1 + 1 코드 실행 끝
    
    2 + 2 계산 시작
    
    2 + 2 = 4
    
    2 + 2 계산 끝
    

main() 함수에 async 키워드를 적용하고 addNumbers(1, 1)과 addNumbers(2, 2)에 await 키워드를 적용했기 때문에 코드는 작성한 순서대로 실행되었다.

## 결괏값 반환받기

async와 await 키워드를 사용한 함수에서도 결괏값을 받아낼 수 있다. 이때 Future 클래스를 사용한다. addNumbers() 함수의 코드를 수정해 자세히 알아보자.

```dart
void main() async {
	final result = await addNumbers(1, 1);
	print('결괏값 $result'); // 일반 함수와 동일하게 반환값을 받을 수 있음
	final result2 = await addNumbers(2, 2);
	print('결괏값 $result2');
}

Future<int> addNumbers(int number1, int number2) async {
	print('$number1 + $number2 계산 시작');
	
	await Future.delayed(Duration(seconds: 3), () {
		print('$number1 + $number2 = ${number1 + number2}');
	});
	
	print('$number1 + $number2 계산 끝');
	
	return number1 + number2;
}
```

- 실행 결과
    
    1 + 1 계산 시작
    
    1 + 1 = 2
    
    1 + 1 계산 끝
    
    결괏값 2
    
    2 + 2 계산 시작
    
    2 + 2 = 4
    
    2 + 2 계산 끝
    
    결괏값 4
    

await 키워드를 적용해도 일반 함수처럼 변수에 반환값을 저장하고 활용할 수 있다.

## Stream

Future는 반환값을 딱 한 번 받아내는 비동기 프로그래밍에 사용한다. 지속적으로 값을 반환받을 때는 Stream을 사용한다. Stream은 한 번 리슨(listen)하면 Stram에 주입되는 모든 값들을 지속적으로 받아온다.

## 기본 사용법

스트림(Stream)을 사용하려면 플러터에서 기본으로 제공하는 dart:async 패키지를 불러와야 한다. 그 다음 dart:async 패키지에서 제공하는 StreamController를 listen()해야 값을 지속적으로 반환받을 수 있다.

```dart
import 'dart:async';

void main() {
	final controller = StreamController(); // StreamController 선언
	final stream = controller.stream; // Stream 가져오기
	
	// Stream에 listen() 함수를 실행하면 값이 주입될 때마다 콜백 함수를 실행할 수 있다.
	final streamListener1 = stream.listen((val) {
		print(var);
	});
	
	// Stream 값을 주입하기
	controller.sink.add(1);
	controller.sink.add(2);
	controller.sink.add(3);
	controller.sink.add(4);
}
```

- 실행 결과
    
    1
    
    2
    
    3
    
    4
    

## 브로드캐스트 스트림

스트림은 단 한번만 listen()을 실행할 수 있다. 하지만 때때로 하나의 스트림을 생성하고 여러 번 listen() 함수를 실행하고 싶을 때 브로드캐스트 스트림(broadcast stream)을 사용하면 여러 번 listen()하도록 변환할 수 있다.

```dart
import 'dart:async';

void main() {
	final controller = StreamController();
	
	// 여러 번 리슨할 수 있는 Broadcast Stream 객체 생성
	final stream = controller.stream.asBroadcastStream();
	
	// 첫 번째 listen() 함수
	final streamListener1 = stream.listen((val) {
		print('listening 1');
		print(val);
	});
	
	// 두 번째 listen() 함수
	final streamListener2 = stream.listen((val) {
		print('listening 2');
		print(val);
	});
	
	// add()를 실행할 때마다 listen()하는 모든 콜백 함수에 값이 주입된다
	controller.sink.add(1);
	controller.sink.add(2);
	controller.sink.add(3);
}
```

- 실행 결과
    
    listening 1
    
    1
    
    listening 2
    
    1
    
    listening 1
    
    2
    
    listening 2
    
    2
    
    listening 1
    
    3
    
    listening 2
    
    3
    

## 함수로 스트림 반환하기

StreamController를 직접 사용하지 않고도 직접 스트림을 반환하는 함수를 작성할 수도 있다. Future를 반환하는 함수는 async로 함수를 선언하고 return 키워드로 값을 반환하면 된다. 스트림을 반환하는 함수는 async* 로 함수를 선언하고 yield 키워드로 값을 반환해주면 된다.

```dart
import 'dart:async';

// Stream을 반환하는 함수는 async*로 선언한다.
Stream<String> calculate(int number) async* {
	for (int i = 0; i < 5; i++) {
		// StreamController의 add()처럼 yield 키워드를 이용해서 값 반환
		yield 'i = $i';
		await  Future.delayed(Duration(seconds: 1));
	}
}

void playStream() {
	// StreamController와 마찬가지로 listen() 함수로 콜백 함수 입력
	calculate(1).listen((val) {
		print(val);
	});
}

void main() {
	playStream();
}
```

- 실행 결과
    
    i = 0
    
    i = 1
    
    i = 2
    
    i = 3
    
    i = 4
