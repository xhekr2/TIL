# Functional Programming

Functional Programming의 기본은 형변환이다. 주로 List, Map, Set같은 타입으로  Functional Programming을 진행한다.

```dart
void main() {
	List<String> lolT1 = ['Doran', 'Doran', 'Oner', 'Faker', 'Peyz', 'Keria'];
	
	print(lolT1); // 출력: [Doran, Doran, Oner, Faker, Peyz, Keria]
	print(lolT1.asMap()); // 출력: {0: Doran, 1" Doran, 2: Oner, 3: Faker, 4: Peyz, 5: Keria}
	print(lolT1.toSet()); // 출력: {Doran, Oner, Faker, Peyz, Keria}
	
	Map lolT1Map = lolT1.asMap();
	
	print(lolT1Map.keys); // 출력: (0, 1, 2, 3, 4, 5)
	print(lolT1Values); // 출력: (Doran, Doran, Oner, Faker, Peyz, Keria)
	
	print(lolT1Map.keys.toList()); // 출력: [0, 1, 2, 3, 4, 5]
	print(lolT1Values.toList()); // 출력: [Doran, Doran, Oner, Faker, Peyz, Keria]
	
	Set lolT1Set = Set.from(lolT1);
	
	print(lolT1Set.toList()); // 출력: [Doran, Oner, Faker, Peyz, Keria]
}
```

## 리스트 맵핑

```dart
void main() {
	List<String> lolT1 = ['Doran', 'Oner', 'Faker', 'Peyz', 'Keria'];
	
	final newLolT1 = lolT1.map((x) {
		return 'T1 $x';
	});
	
	print(lolT1); // 출력: [Doran, Oner, Faker, Peyz, Keria]
	print(newLolt1); // 출력: (T1 Doran, T1 Oner, T1 Faker, T1 Peyz, T1 Keria)
	print(newLolT1.toList()); // 출력: [T1 Doran, T1 Oner, T1 Faker, T1 Peyz, T1 Keria]
	
	final newLolT12 = lolT1.map((x) => 'T1 $x'); // arrow 함수
	
	print(newLolt12); // 출력: (T1 Doran, T1 Oner, T1 Faker, T1 Peyz, T1 Keria)
	print(newLolT12.toList()); // 출력: [T1 Doran, T1 Oner, T1 Faker, T1 Peyz, T1 Keria]
	
	print(lolT1 == lolT1); // true
	print(newLolT1 == lolT1); // false
	print(newLolT1 == newLolT12); // false
}
```

`!` Arrow 함수

단 한 줄의 코드만 실행하는 함수를 정의할 때 사용하는 간결한 문법이다. `=>` 기호를 사용하여 코드 가독성을 높이며 함수가 계산한 결과를 자동으로 반환한다.

`(매개변수) => 식;` 으로 사용하며 `=>` 뒤의 식(expression) 결과가 바로 함수의 반환값이다. return을 직접 적지 않고 오직 1줄의 코드(식)만 가능하기 때문에 `{}` 블록 내부에 여러 줄의 코드를 작성할 때는 사용할 수 없다.

짧은 콜백 함수가 필요할 때 자주 사용된다.

## 리스트 맵핑

```dart
void main() {
	Map<String, String> lolT1 = {
		'Doran': '도란',
		'Oner': '오너',
		'Faker': '페이커',
		'Peyz': '페이즈',
		'Keria': '케리아'
	};
	
	final result = lolT1.map(
		(key, value) => MapEntry(
			'T1 $key',
			'티원 $value',
		),
	);
	
	print(lolT1); // 출력: {Doran: 도란, Oner: 오너, Faker: 페이커, Peyz: 페이즈, Keria: 케리아}
	print(result); // 출력: {T1 Doran: 티원 도란, T1 Oner: 티원 오너, T1 Faker: 티원 페이커, T1 Peyz: 티원 페이즈, T1 Keria: 티원 케리아}
	
	final keys = lolT1.keys.map((x) => 'T1 $x');
	
	print(keys); // 출력: (T1 Doran, T1 Oner, T1 Faker, T1 Peyz, T1 Keria)
	
	final keys1 = lolT1.keys.map((x) => 'T1 $x').toList();
	
	print(keys1); // 출력: [T1 Doran, T1 Oner, T1 Faker, T1 Peyz, T1 Keria]
	
	final values = lolT1.values.map((x) => '티원 $x');
	
	print(values); // 출력: (티원 도란, 티원 오너, 티원 페이커, 티원 페이즈, 티원 케리아)
	
	final values1 = lolT1.values.map((x) => '티원 $x');
	
	print(values1); // 출력: [티원 도란, 티원 오너, 티원 페이커, 티원 페이즈, 티원 케리아]
}	
```

맵 자체를 맵핑을 해서 새로운 맵으로 만들 때 아래와 같은 식으로 진행을 한다.

```dart
final result = lolT1.map(
		(key, value) => MapEntry(
			'T1 $key',
			'티원 $value',
		),
	);
```

key 값만 리스트 형태로 바꾸고 value 값만 리스트 형태로 바꿀 수도 있다.

```dart
final keys = lolT1.keys.map((x) => 'T1 $x');
	
print(keys); // 출력: (T1 Doran, T1 Oner, T1 Faker, T1 Peyz, T1 Keria)
	
final keys1 = lolT1.keys.map((x) => 'T1 $x').toList();
	
print(keys1); // 출력: [T1 Doran, T1 Oner, T1 Faker, T1 Peyz, T1 Keria]
```

## 셋 맵핑

```dart
void main() {
	Set lolT1Set = {
		'Doran',
		'Oner',
		'Faker',
		'Peyz',
		'Keria',
	};
	
	final newSet = lolT1Set.map((x) => 'T1 $x').toSet();
	
	print(newSet); // 출력: {T1 Doran, T1 Oner, T1 Faker, T1 Peyz, T1 Keria}
}
```

## where()

where는 일종의 필터링을 할 수 있다.

```dart
void main() {
	List<Map<String, String>> people = [
		{
			'name': 'Doran',
			'team': 'T1',
		},
		{
			'name': 'Peyz',
			'team': 'T1',
		},
		{
			'name': 'Zeus',
			'team': 'HLE',
		}
		{
			'name': 'Gumayusi',
			'team': 'HLE',
		},
	];
	
	print(people); // 출력: [{name: Doran, team: T1}, {name: Peyz, team: T1}, {name: Zeus, team: HLE}, {name: Gumayusi, team: HLE}]
	
	final lolT1 = people.where((x) => x['team'] == 'T1');
	
	print(lolT1); // 출력: ({name: Doran, team: T1}, {name: Peyz, team: T1})
	
	final lolT11 = people.where((x) => x['team'] == 'T1').toList();
	
	print(lolT11); // 출력: [{name: Doran, team: T1}, {name: Peyz, team: T1}]
}
```

## reduce()

```dart
void main() {
	List<int> numbers = [
		1,
		3,
		5,
		7,
		9
	];
	
	final result = numbers.reduce((prev, next) {
		print('----------')
		print('prev: $prev');
		print('next: $next');
		print('total: ${prev + next}');
		
		return prev + next;
	});
	
	print(result); // 출력: 25
}
```

prev에는 가장 처음에만 1이 들어가고 그 다음부턴 함수가 반환해준(여기서는 prev + next) 값이 들어간다. 아래 코드는 이해를 돕기 위해 작성된 코드이다.

```dart
print('----------') // 구분선, 매번 새로운 loop라는 것을 증명하기 위함이다
print('prev: $prev');
print('next: $next');
print('total: ${prev + next}'); // 리턴값을 보여준다
```

```dart
// 출력
----------
prev: 1
next: 3
total: 4
----------
prev: 4
next: 5
total: 9
----------
prev: 9
next: 7
total: 16
----------
prev: 16
next: 9
total: 25
```

또한 위에서 아래와 같은 코드

```dart
final result = numbers.reduce((prev, next) {
	return prev + next;
});
```

는 아래와 같이 써도 된다.

```dart
final result = numbers.reduce((prev, next) => prev + next);
```

이번엔 글자를 더해보겠다.

```dart
void main() {
	List<String> words = [
		'안녕하세요 ',
		'저는 ',
		'이동윤입니다.',
	];
	
	final sentence = words.reduce((prev, next) => prev + next);
	
	print(sentence); // 출력: 안녕하세요 저는 이동윤입니다.
}
```

reduce는 반환되는 값들의 타입이 각각의 태초가 된 리스트의 타입과 같아야한다. 위의 코드를 예로 들어보면, words 리스트는 타입이 String이므로 reduce를 통해 반환된 값의 타입은 String이 되어야한다. 아래와 같이 reduce로 글자 수를 더하려고 하면..

```dart
void main() {
	List<String> words = [
		'안녕하세요 ',
		'저는 ',
		'이동윤입니다.',
	];
	
	final sentence = words.reduce((prev, next) => prev + next);
	
	print(sentence); // 출력: 안녕하세요 저는 이동윤입니다.
	
	final sentenceLength = words.reduce((prev, next) => prev.length + next.length); // 오류
}
```

위의 코드를 보면..

`final sentenceLength = words.reduce((prev, next) => prev.length + next.length);`

이 코드는 에러가 발생한다. words 리스트의 타입은 String인데, 리턴값은 int가 나오기 때문이다.

## fold()

fold는 제네릭으로 반환받을 값의 타입을 적어줘야하며, 두개의 파라미터를 받는다.

```dart
void main() {
	List<int> numbers = [1, 3, 5, 7, 9];
	
	final sum = numbers.fold<int>(0, (prev, next) {
		print('----------');
		print('prev: $prev');
		print('next: $next');
		print('total: ${prev + next}');
		
		return prev + next;
	});
	
	print(sum); // 출력: 25
}
```

reduce와는 다르게 처음 prev에는 첫 번째 파라미터값(여기서는 0)이 들어가고 next에 첫 번째 값이 들어간다. 그 다음부터는 reduce와 똑같이 실행된다. reduce 코드에서 설명했듯, 아래는 이해를 돕기 위해 작성된 코드이다.

```dart
print('----------') // 구분선, 매번 새로운 loop라는 것을 증명하기 위함이다
print('prev: $prev');
print('next: $next');
print('total: ${prev + next}'); // 리턴값을 보여준다
```

```dart
// 출력
----------
prev: 0
next: 1
total: 1
----------
prev: 1
next: 3
total: 4
----------
prev: 4
next: 5
total: 9
----------
prev: 9
next: 7
total: 16
----------
prev: 16
next: 9
total: 25
```

마찬가지로 위에서 아래와 같은 코드

```dart
final sum = numbers.fold<int>(0, (prev, next) {
	return prev + next
});
```

는 아래와 같이 써도 된다

```dart
final sum = numbers.fold<int>(0, (prev, next) => prev + next);
```

reduce처럼 fold로 글자를 더해보겠다.

```dart
void main() {
	List<String> words = [
		'안녕하세요 ',
		'저는 ',
		'이동윤입니다.',
	];
	
	final sentence = words.fold<String>('', (prev, next) => prev + next);
	
	print(sentence); // 출력: 안녕하세요 저는 이동윤입니다.
}
```

fold의 장점은 아무 형태나 반환받을 수 있다는 것이다. 아래는 reduce에서는 오류가 났던 코드이다.

```dart
void main() {
	List<String> words = [
		'안녕하세요 ',
		'저는 ',
		'이동윤입니다.',
	];
	
	final sentenceLength = words.fold<int>(0, (prev, next) => prev + next.length);
	
	print(sentenceLength); // 출력: 16
}
```

reduce에서는 prev에서도 .length를 써야 했다(물론 reduce에서 썼던 코드는 오류가 맞다). prev값에는 안녕하세요 가 들어갈 테니까. 하지만 fold는 시작값이 정해져있기 때문에(여기서는 0) prev에는 .length를 사용하지 않는다.

## 캐스케이딩 연산자

여러개의 리스트를 하나로 합칠 때 많이 사용한다. `...` 을 사용한다

```dart
void main() {
	List<int> even = [2, 4, 6, 8];
	List<int> odd = [1, 3, 5, 7];
	
	print([even, odd]); // 출력: [[2, 4, 6, 8], [1, 3, 5, 7]]
	print([...even, ...odd]); // 출력: [2, 4, 6, 8, 1, 3, 5, 7]
```

완전히 새로운 리스트를 만들어 값을 풀어넣기 때문에…

```dart
void main() {
	List<int> num = [1, 2, 3, 4, 5];
	
	print(num); // 출력: [1, 2, 3, 4, 5]
	print([...num]); // 출력: [1, 2, 3, 4, 5]
	print(num == [...num]); // 출력: false
```
