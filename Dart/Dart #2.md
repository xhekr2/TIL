# 다트 객체 지향 프로그래밍

다트 언어는 높은 완성도로 객체 지향 프로그래밍을 지원한다. 플러터 역시 객체지향 프로그래밍(object-oriented programming, OOP) 중심으로 설계된 프레임워크이다.

객체지향 프로그래밍이 왜 필요할까. 코드를 작성할 때 모든 코드를 main() 함수에서 작성하면 코드 정리가 안 돼 유지보수 및 협업에 상당히 큰 장애물이 된다. 객체지향 프로그래밍을 하면 변수와 메서드를 특정 클래스에 종속되게 코딩할 수 있다. 클래스를 사용해서 서로 밀접한 관계가 있는 함수와 변수를 묶어두면 코드 관리가 용이하기 때문에 객체지향 프로그래밍은 현대 프로그래밍에서 상당히 중요한 부분을 차지한다.

클래스는 일종의 설계도로서 데이터가 보유할 속성과 기능을 정의하는 자료 구조이며 인스턴스화 되어야 실제 사용할 수 있는 데이터가 생성된다.

**인스턴스(instance)** 클래스를 이용해서 객체를 선언하면 해당 객체를 클래스의 인스턴스라고 부른다.

**인스턴스화(instantiation)** 클래스에서 인스턴스(객체)를 생성하는 과정을 말한다.

## 클래스

객체지향 프로그래밍의 기본은 클래스(class)로부터 시작된다.

```dart
// class 키워드를 입력 후 클래스명을 지정해 클래스를 선언한다.
class LoL {
	// 클래스에 종속되는 변수를 지정할 수 있다.
	String name = 'Yone';
	
	// 클래스에 종속되는 함수를 지정할 수 있다.
	// 클래스에 종속되는 함수를 메서드라고 부른다.
	void sayName() {
		// 클래스 내부의 속성을 지칭하고 싶을 때는 this 키워드를 사용하면 된다.
		// 결과적으로 this.name은 LoL 클래스의 name 변수를 지칭한다.
		print('저는 ${this.name}입니다.');
		// 스코프 안에 같은 속성 이름이 하나만 존재한다면 this를 생략할 수 있다.
		print('저는 $name입니다.');
	}
}
```

LoL 클래스를 정의했다. LoL 클래스 안에 종속된 변수로는 name이, 함수로는 sayName()이 있다. 클래스에 종속된 변수를 멤버 변수, 종속된 함수를 메서드라고 부른다. 클래스 내부 속성을 지칭하는 데 this 키워드를 사용한다. this 키워드는 현재 클래스를 의미한다(같은 이름의 속성이 하나만 존재한다면 this를 생략할 수 있다. 하지만 만약 sayName() 함수에 name이라는 변수가 존재한다면 this 키워드를 꼭 사용해야 한다).

**this 키워드**

클래스에 종속되어 있는 값을 지칭할 때 사용된다. 함수 내부에 같은 이름의 변수가 없으면 `this` 키워드를 생략할 수 있다.

`!` 함수는 메서드를 포함하는 더 큰 개념이다. 클래스에 정의된 함수인 메서드는 클래스의 기능을 정의한 함수이다.

클래스를 만들었으니 사용해보자.

```dart
void main() {
	// 변수 타입을 LoL로 지정하고 LoL의 인스턴스를 생성할 수 있다.
	// 인스턴스를 생성할 때는 함수를 실행하는 것처럼 인스턴스화하고싶은 클래스에 괄호를 열고 닫아준다.
	LoL yone = LoL(); // LoL 인스턴스 생성
	
	// 메서드를 실행한다.
	yone.sayName();
}
```

변수 타입을 LoL로 지정해 LoL의 인스턴스를 생성한다. 인스턴스를 생성할 때는 함수를 실행하는 것처럼 인스턴스화하고 싶은 클래스명 뒤에 `()` 를 붙여주면 된다.

## 생성자

생성자(constructor)는 클래스의 인스턴스를 생성하는 메서드이다. `name` 변수의 값을 외부에서 입력할 수 있게 변경해보자.

```dart
class LoL {
	// 생성자에서 입력받는 변수들은 일반적으로 final 키워드 사용
	final String name;
	
	// 생성자 선언
	// 클래스와 같은 이름이어야 하며 함수의 매개변수를 선언하는 것처럼 매개변수를 지정해준다.
	LoL(String name) : this.name = name;
	
	void sayName() {
		print('저는 ${this.name}입니다.');
	}
}
```

생성자에서 입력받을 변수를 일반적으로 `final` 로 선언한다. 인스턴스화한 다음에 혹시라도 변수의 값을 변경하는 실수를 막기 위함이다. 클래스 생성자 선언은 클래스와 같은 이름을 사용해야 한다. 이름 뒤에 `()` 를 붙이고 원하는 매개변수를 지정해준다. 네임드 파라미터 및 옵셔널 파라미터도 사용할 수 있다. `:` 기호 뒤에 입력받은 매개변수가 저장될 클래스 변수를 지정해준다.

LoL 클래스로 인스턴스를 만들어보자.

```dart
void main() {
	// name에 '요네' 저장
	Runeterra yone = LoL('요네');
	yone.sayName();
	
	// name에 '야스오' 저장
	LoL yasuo = LoL('야스오');
	yasuo.sayName();
}
```

- 실행 결과
    
    저는  요네입니다.
    
    저는 야스오입니다.
    

LoL 클래스 하나로 여러 LoL 인스턴스를 생성해 중복 코딩 없이 활용할 수 있게 되었다.

생성자의 매개변수를 변수에 저장하는 과정을 생략하는 방법도 있다. 아래 LoL 클래스는 이전 코드의 LoL 클래스와 표현 방식만 다르고 동작은 똑같다.

```dart
class LoL {
	final String name;
	
	// this를 사용할 경우 해당되는 변수에 자동으로 매개변수가 저장된다.
	LoL(this.name);
	
	void sayName() {
		print('저는 ${this.name}입니다.');
	}
}
```

## 네임드 생성자

네임드 생성자(named constructor)는 네임드 파라미터와 상당히 비슷한 개념이다. 일반적으로 클래스를 생성하는 여러 방법을 명시하고 싶을 때 사용한다.

```dart
class LoL {
	final String name;
	final int membersCount;
	
	// 생성자
	LoL(String name, String affiliation)
	// 1개 이상의 변수를 저장하고 싶을 때는 , 기호로 연결해주면 된다.
		: this.name = name,
			this.affiliation = affiliation;
		
		// 네임드 생성자
		// {클래스명, 네임드 생성자명} 형식
		// 나머지 과정은 기본 생성자와 같다.
		LoL.fromMap(Map<String, dynamic> map)
			: this.name = map['name'],
				this.affiliation = map['affiliation'];

	void sayName() {
		print('저는 ${this.name}입니다. ${this.name} 는 ${this.affiliation} 소속입니다.');
	}
}
```

생성자에서 매개변수 2개를 받는다. `,` 기호를 사용하면 하나 이상의 매개변수를 처리할 수 있다. 네임드 생성자를 `{클래스명.네임드 생성자명}` 형식으로 지정하면 된다. 나머지 과정은 기본 생성자와 같다. 키와 값을 갖는 Map 형식으로 매개변수를 받아보았다.

이제 원하는 대로 동작하는지 확인해보자.

```dart
void main() {
	// 기본 생성자 사용
	Lol yone = LoL('요네', '아이오니아');
	yone.sayName();
	
	// fromMap 이라는 네임드 생성자 사용
	LoL yasuo = LoL.fromMap({
		'name' : '야스오',
		'membersCount' : '아이오니아',
	});
	yasuo.sayName();
}
```

- 실행 결과
    
    저는 요네입니다. 요네는 아이오니아 소속입니다.
    
    저는 야스오입니다. 야스오는 아이오니아 소속입니다.
    

## 프라이빗 변수

다트에서의 프라이빗 변수(private variable)는 다른 언어와 정의가 약간 다르다. 일반적으로 프라이빗 변수는 클래스 내부에서만 사용하는 변수를 칭하지만 다트 언어에서는 같은 파일에서만 접근 가능한 변수이다.

```dart
class LoL {
	// _로 변수병을 시작하면 프라이빗 변수를 선언할 수 있다.
	String _name;
	
	LoL(this._name);
}

void main() {
	LoL yone = LoL('요네');
	
	// 같은 파일에서는 _name 변수에 접근할 수 있지만 다른 파일에서는 접근할 수 없다.
	print(yone._name);
}
```

프라이빗 변수는 변수명을 `_` 기호로 시작해 선언할 수 있다. 일반적으로 클래스 선언과 사용하는 파일이 다르다. 다른 파일에서는 `_name` 변수에 접근할 수 없다.

## getter / setter

게터(getter)는 말 그대로 값을 가져올 때 사용되고 세터(setter)는 값을 지정할 때 사용된다. 가변(mutable)변수를 선언해도 직접 값을 가져오거나 지정할 수 있지만 게터와 세터를 사용하면 어떤 값이 노출되고 어떤 형태로 노출될지 그리고 어떤 변수를 변경 가능하게 할지 유연하게 정할 수 있다.

객체지향 프로그래밍을 할 때 변수의 값에 불변성(Immutable)(인스턴스화 후 변경할 수 없는)을 특성으로 사용하기 때문에 세터는 거의 사용하지 않는다. 하지만 게터는 종종 사용한다.

```dart
class LoL {
	String _name = '요네';
	
	// get 키워드를 사용해서 게터임을 명시한다.
	// 게터는 메서드와 다르게 매개변수를 전혀 받지 않는다.
	String get name {
		return this._name;
	}
	
	// 세터는 set이라는 키워드를 사용해서 선언한다.
	// 세터는 매개변수로 딱 하나의 변수를 받을 수 있다.
	set name(String name) {
		this._name = name;
	}
}
```

게터는 메서드를 선언하는 문법과 상당히 유사하지만 매개변수는 정의하지 않는다. 현재 Runeterra 클래스의 name 변수는 프라이빗으로 선언되어 있기 때문에 다른 파일에서 name 변수에 접근할 수 없다. 이럴 때 name 게터를 선언하면 외부에서도 간접적으로 _name 변수를 접근할 수 있다. 세터는 set 키워드를 사용해 지정하며 매개변수를 하나만 받는다. 이 매개변수는 멤버 변수에 대입되는 값이다.

게터와 세터는 모두 변수처럼 사용하면 된다. 즉 사용할 때 메서드명 뒤에 `()` 를 붙이지 않는다.

```dart
void main() {
	LoL ynoe = LoL();
	yone.name = '야스오'; // 세터
	print(yone.name); // 게터
}
```

- 실행 결과
    
    야스오
    

_name의 초깃값이 요네이다. 세터로 야스오를 대입하고 게터로 확인해보니 야스오로 저장되어 있다.

## 상속

extends 키워드를 사용해 상속(inheritance)할 수 있다. 상속은 어떤 클래스의 기능을 다른 클래스가 사용할 수 있게 하는 기법이다. 기능을 물려주는 클래스를 부모 클래스, 물려받는 클래스를 자식 클래스라고 한다. 아래와 같은 LoL 클래스가 있다고 가정해보자.

```dart
class LoL {
	final String name;
	final String affiliation;
	
	LoL(this.name, this.affiliation);
	
	void sayName() {
		print('저는 ${this.name}입니다.');
	}
	
	void sayAffiliation() {
		print('${this.name} 소속은 ${this.affiliation}입니다.');
	}
}
```

LoL 클래스를 상속하는 Valorant클래스를 만들어보겠다. LoL 클래스는 멤버 변수로 name과 affiliation, 메서드로는 sayName(), sayAffiliation()을 가지고 있다.

```dart
// extends 키워드를 사용해서 상속받는다.
// class 자식 클래스 extends 부모 클래스 순서이다.
class Valorant extends LoL {
	// 상속받은 생성자
	Valorant(
			String name,
			String affiliation,
			) : super( // super는 부모 클래스를 지칭한다.
		name,
		affiliation,
);

	// 상속받지 않은 기능
	void sayGame() {
		print('저는 발로란트 캐릭터 입니다.');
	}
}
```

extends 키워드를 사용해 상속을 받는다. `{class 자식 클래스 extends 부모 클래스}` 순서로 지정하면 된다. 자식 클래스는 부모 클래스의 모든 기능을 상속받는다. 클래스 상속을 하다 보면 super라는 키워드를 자주 사용한다. 현재 클래스를 지칭하는 this와 달리 super는 상속한 부모 클래스를 지칭한다. 부모 클래스인 LoL클래스에 기본 생성자가 있는 만큼 Valorant에서는 LoL 클래스의 생성자를 실행해줘야 한다. 그렇지 않으면 LoL 클래스의 모든 기능을 상속받아도 변숫값들을 설정하지 않아서 기능을 제대로 사용할 수 없다. 상속받지 않은 메서드나 변수를 새로 추가할 수도 있다. 저는 발로란트 캐릭터 입니다를 출력하는 간단한 메서드를 새로 만들어보았다.

사용법은 부모 클래스와 같다.

```dart
void main() {
	Valorant chamber = Valorant('체임버'); // 생성자로 객체 생성
	
	chamber.sayName(); // 부모한테 물려받은 메서드
	chamber.sayGame(); // 자식이 새로 추가한 메서드
}
```

- 실행 결과
    
    저는 체임버입니다.
    
    저는 발로란트 캐릭터 입니다.
    

sayName()은 부모한테 물려받은 메서드이다. sayGame()은 자식이 새로 추가한 메서드이다. 사용 방식은 둘 다 같다.

부모 클래스에 공통으로 사용하는 변수와 메서드를 정의해 상속받으면 결과적으로 자식 코드들은 해당 값들을 사용할 수 있어서 중복 코딩하지 않아도 된다. 그렇다면 LoL 클래스를 Overwatch클래스가 상속받았다고 가정하자. 부모가 같다면 Overwatch 클래스의 객체는 Valorant에 새로 추가한 sayGame() 메서드를 호출할 수 있을까? 정답은 호출할 수 없다 이다.

## 오버라이드

오버라이드(override)는 부모 클래스 또는 인터페이스에 정의된 메서드를 재정의할 때 사용된다. 다트에서는 override 키워드를 생략할 수 있기 때문에 override 키워드를 사용하지  않고도 메서드를 재정의할 수 있다.

상속에서 사용한 LoL 클래스를 상속받아서 메서드 오버라이드를 해보겠다.

```dart
class Overwatch extends LoL {
	// 아래처럼 생성자의 매개변수로 직접 super 키워드를 사용해도 된다.
	Overwatch(
		super.name,
		super.affiliation,
	);
	
	// override 키워드를 사용해 오버라이드 한다.
	@override
	void sayName() {
		print('저는 오버워치 세계관 ${this.name}입니다.');
	}
}
```

부모 클래스에 이미 존재하는 메서드를 자식 클래스에서 재정의할 경우 override 키워드를 사용해 메서드를 다시 정의한다. 메서드 재정의라고도 한다.

LoL 클래스에 메서드가 두 개였다. 하나는 오버라이드를 했고 하나는 그러지 않았다. 사용할 때 어떻게 적용되는지 확인해보자.

```dart
void main() {
	Overwatch widowmaker = Overwatch('위도우메이커', '탈론');
	
	widowmaker.sayName(); // 자식 클래스의 오버라이드된 메서드 사용
	
	// sayAffiliation는 오버라이드하지 않았기 때문에 그대로 LoL 클래스의 메서드가 실행된다.
	talon.sayAffiliation); // 부모 클래스의 메서드 사용
}
```

- 실행 결과
    
    저는 오버워치 세계관 위도우메이커 입니다.
    
    위도우메이커 소속은 탈론입니다.
    

sayName() 메서드는 오버라이드되었으므로 Overwatch 클래스에 재정의된 sayName() 메서드가 실행된다. sayAffiliation() 메서드는 오버라이드하지 않았으므로 LoL 클래스에 정의된 sayAffilitaion 메서드를 사용한다.

한 클래스에 이름이 같은 메서드가 존재할 수 없기 때문에 부모 클래스나 인터페이스에 이미 존재하는 메서드명을 입력하면 override 키워드를 생략해도 메서드가 덮어써진다. 하지만 직접 명시하는 게 협업 및 유지보수에 유리하다.

## 인터페이스

상속은 공유되는 기능을 이어받는 개념이지만 인터페이스(Interface)는 공통으로 필요한 기능을 정의만 해두는 역할을 한다. 상속에서 사용한 LoL 클래스를 인터페이스로 사용하겠다. 다트에는 인터페이스를 지정하는 키워드가 따로 없다. 상속은 단 하나의 클래스만 할 수 있지만 인터페이스는 적용 개수에 제한이 없다. 여러 인터페이스를 적용하고 싶으면 `,` 기호를 사용하여 인터페이스를 나열해 입력해주면 된다.

```dart
// implements 키워드를 사용하면 원하는 클래스 인터페이스로 사용할 수 있다.
class Overwatch implements LoL {
	final String name;
	final String affiliation;
	
	Overwatch(
		this.name,
		this.membersCount,
		);
		
	void sayName() {
		print('저는 오버워치 세계관 ${this.name}입니다.');
	}
	
	void sayAffiliation() {
		print('${this.name} 소속은 ${this.membersCount}입니다.');
	}
}
```

Overwatch 클래스는 LoL 클래스가 정의한 모든 기능을 다시 정의했다. 상속받을 때는 부모 클래스의 모든 기능이 상속되므로 재정의할 필요가 없었다. 반면 인터페이스는 반드시 모든 기능을 다시 정의해줘야 한다. 귀찮아 보이지만 애초에 반드시 재정의할 필요가 있는 기능을 정의하는 용도가 인터페이스이기 때문이다. 그렇게 하면 실수로 빼먹는 일을 방지할 수 있다.

인터페이스 사용법은 클래스와 같다.

```dart
void main() {
	Overwatch widowmaker = Overwatch('위도우메이커', '탈론');
	
	Overwatch.sayName();
	Talon.sayAffiliation();
}
```

- 실행 결과
    
    저는 오버워치 세계관 위도우메이커입니다.
    
    위도우메이커 소속은 탈론입니다.
    

## 믹스인

믹스인(mixin)은 특정 클래스에 원하는 기능들만 골라 넣을 수 있는 기능이다. 특정 클래스를 지정해서 속성들을 정의할 수 있으며 지정한 클래스를 상속하는 클래스에서도 사용할 수 있다. 그리고 인터페이스처럼 한 개의 클래스에 여러 개의 믹스인을 적용할 수도 있다. 인터페이스와 마찬가지로 여러 믹스인을 적용하고 싶으면 `,` 기호로 열거하면 된다. 상속에서 사용한 LoL 클래스를 사용해 믹스인하는 방법을 알아보자.

```dart
mixin LoLUltMixin on LoL{
	void Ult() {
		print('${this.name}가 궁극기를 사용합니다.');
	}
}

// 믹스인을 적용할 때는 with 키워드 사용
class Valorant extends LoL with LoLUltMixin{
	Multiverse(
		super.name,
		super.affiliation,
	);
	
	void sayGame() {
		print('저는 발로란트 캐릭터 입니다.');
	}
}

void main() {
	Valorant chamber = Valorant('체임버')
	
	// 믹스인에 정의된 Ult() 함수 사용 가능
	chamber.ult();
}
```

- 실행 결과
    
    체임버가 궁극기를 사용합니다.
    

## 추상

추상(abstract)은 상속이나 인터페이스로 사용하는 데 필요한 속성만 정의하고 인스턴스화할 수 없도록 하는 기능이다. 인터페이스 예제와 같이 LoL 클래스를 인터페이스로 사용하고 LoL 클래스를 따로 인스턴스화할 일이 없다면, LoL 클래스를 추상 클래스로 선언해서 LoL 클래스의 인스턴스화를 방지하고 메서드 정의를 자식 클래스에 위임할 수 있다. 또한 추상 클래스는 추상 메서드를 선언할 수 있으며 추상 메서드는 함수의 반환 타입, 이름, 매개변수만 정의하고 함수 바디의 선언을 자식 클래스에서 필수로 정의하도록 강제한다. LoL 추상 클래스를 작성해보겠다(위의 코드와 연관이 없다).

```dart
// abstract 키워드를 사용해 추상 클래스 지정
abstract class LoL (
	final String name;
	final String affiliation;
	
	LoL(this.name, this.affiliation); // 생성자 선언
	
	void sayName(); // 추상 메서드 선언
	void sayAffiliation(); // 추상 메서드 선언
}
```

abstract 키워드로 추상 클래스를 지정했다. 생성자를 비롯해 메서드도 선언만 하며 어떻게 동작하는지 정의가 없다. 이처럼 추상 클래스는 선언까지만 해주면 된다.

추상 클래스를 구현(implements)하는 클래스를 만들어보겠다.

```dart
// implements 키워드를 사용해 추상 클래스를 구현하는 클래스
class OverWatch implements LoL {
	final String name;
	final String affiliation;
	
	Overwatch(
		this.name,
		this.affiliation,
	);
	
	void sayName() {
		print('저는 오버워치 세계관 ${this.name}입니다.');
	}
	
	void sayAffiliation() {
		print('${this.name} 소속은 ${this.affiliation}입니다.');
	}
}
```

생성자를 비롯한 모든 메서드를 정의했다. 하나라도 정의하지 않으면 에러가 난다. 사용 방법은 클래스와 같다.

```dart
void main() {
	Overwatch widowmaker = Overwatch('위도우메이커', '탈론');
	
	widowmaker.sayName();
	widowmaker.sayAffiliation();
}
```

- 실행 결과
    
    저는 오버워치 세계관 위도우메이커입니다.
    
    위도우메이커 소속은 탈론입니다.
    

추상 메서드는 부모 클래스를 인스턴스화할 일이 없고, 자식 클래스들에 필수적 또는 공통적으로 정의돼야 하는 메서드가 존재할 때 사용된다.

## 제네릭

제네릭(generic)은 클래스나 함수의 정의를 선언할 때가 아니라 인스턴스화하거나 실행할 때로 미룬다. 특정 변수의 타입을 하나의 타입으로 제한하고 싶지 않을 때 자주 사용한다.

Map, List, Set 등에서 사용한 `<>` 사이에 입력되는 값이 제네릭 문자이다. 예를 들어 List<String>이라고 입력하면 String값들로 구성된 리스트를 생성하겠다는 뜻인데, List 클래스는 제네릭이므로 인스턴스화를 하기 전 어떤 타입으로 List가 생성될지 알지 못한다. Map과 Set 또한 마찬가지다.

직접 코드로 구현하며 알아보자.

```dart
// 인스턴스화할 때 입력받을 타입을 T로 지정한다.
class Cache<t> {
	// data의 타입을 추후 입력될 T 타입으로 지정한다.
	final T data;
	
	Cache({
		required this.data,
	});
}

void main() {
	// T의 타입을 List<int>로 입력한다.
	final cache = Cache<List<int>>(
		data: [1, 2, 3],
	);
	
	// 제네릭에 입력된 값을 통해 data 변수의 타입이 자동으로  유추한다.
	print(cache.data.reduce((vlaue, element) => value + element));
}
```

- 실행 결과
    
    6
    

흔히 사용되는 제네릭 문자들

T: 변수 타입을 표현할 때 흔히 사용한다.

E: 리스트 내부 요소들의 타입을 표현할 때 흔히 사용한다.

K: 키를 표현할 때 흔히 사용한다.

V: 값을 표현할 때 흔히 사용한다.

> 어떤 문자를 사용해서 어떤 값을 표현해도 프로그램적으로 상관없지만 일반적으로 개발자들이 많이 사용하는 문자들이 존재한다.

## 스태틱

지금까지 작성한 변수와 메서드 등 모든 속성은 각 클래스의 인스턴스에 귀속되었다. 하지만 static 키워드를 사용하면 클래스 자체에 귀속된다.

```dart
class Counter {
	// static 키워드를 사용해서 static 변수 선언
	static int i = 0;
	
// static 키워드를 사용해서 static 변수 선언
	Counter() {
		i++;
		print(i++);
	}
}

void main() {
	Counter count1 = Counter();
	Counter count2 = Counter();
	Counter count3 = Counter();
}
```

- 실행 결과
    
    1
    
    2
    
    3
    

변수 i를 스태틱으로 지정했다(스태틱 변수 또는 정적 변수라고 부른다). Counter 클래스에 귀속되기 때문에 인서턴스를 호출할 때마다 1씩 증가한다. 생성자에 this.i가 아니고 i로 명시했다. static 변수는 클래스에 직접 귀속되기 때문에 생성자에서 static값을 지정하지 못한다. 결과적으로 static 키워드는 인스턴스끼리 공유해야 하는 정보에 지정하면 된다.

## 캐스케이드 연산자

캐스케이드 연산자(cascade operator)는 인스턴스에서 해당 인스턴스의 속성이나 멤버 함수를 연속해서 사용하는 기능이다. 캐스케이드 연산자는 `..` 기호를 사용한다. 상속에서 사용한 LoL 클래스를 사용해보겠다.

```dart
void main() {
	// cascade operator (..)을 사용하면 선언한 변수의 메서드를 연속으로 실행할 수 있다.
	LoL yone = LoL('요네', '아이오니아')
		..sayName()
		..sayAffiliation();
}
```

- 실행 결과
    
    저는 요네입니다.
    
    요네는 아이오니아 소속입니다.
    

이처럼 캐스케이드 연산자를 사용하면 더 간결한 코드를 작성할 수 있다.
