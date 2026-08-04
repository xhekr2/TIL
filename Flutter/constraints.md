> [Flutter layout and constraints](https://www.youtube.com/watch?v=z8bY3XVAzgI&list=PLjxrf2q8roU2bqkohF-r9TNmo8HWSu0TG&index=6) 영상을 참고

# 플러터의 제약조건
Flutter Layout의 대원칙은 아래와 같다.

1. Constraints go down
2. Sizes go up
3. Parent sets the position

부모가 자식에게 제약을 전달하면 자식이 자신의 크기 결정 후 부모에게 전달한다. 그러면 부모가 자식의 위치를 결정한다.

## Constraints (제약)
Flutter에서 Constraint는 부모 위젯이 자식 위젯에게 넘겨주는 크기의 허용 범위이다. 단순히 width, height값 하나를 넘기는 게 아닌, 최소/최대 너비, 높이(총 4개의 값)을 넘겨준다.
```dart
import 'package:flutter/material.dart';

void main() {
  runApp(MaterialApp(home: ConstraintsGoDown()));
}

class ConstraintsGoDown extends StatelessWidget {
  const ConstraintsGoDown({super.key});

  @override
  Widget build(BuildContext context) {
    return Scaffold(
      body: Container(
        width: 300,
        height: 300,
        color: Colors.blue,
        child: Container(width: 100, height: 100, color: Colors.red),
      ),
    );
  }
}
```
Constraints go down이란 **부모 위젯이 자식 위젯에게 Constraint를 전달하는 것**을 의미한다. 이때 전달되는 Constraint는 Tight Constraint일 수도 있고 Loose Constraint일 수도 있다.

위 예제에서는 부모 Container가 width와 height를 명시했기 때문에 Tight Constraint가 전달된다.
### Tight Constraint

위의 코드를 다시 보면, 부모 Container는 너비 300, 높이 300이라는 크기를 가진다. 이때 플러터의 대원칙 **Constraints go down(제약은 아래로(부모에서 자식으로) 내려간다)**이 발동한다.

부모 Container는 자식 Container에게 최소 너비 300, 최대 너비 300, 최소 높이 300, 최대 높이 300이라는 Constraint를 전달한다. 즉 자식은 반드시 300×300 크기를 가져야 하며, 이를 Tight Constraint라고 한다.

`!` **Container자체가 항상 Tight Constraint를 만드는 건 아니다.** 위의 코드를 보면, Container의 width와 height를 **직접 명시**했기 때문에 Tight Constraint가 생긴 것이다.

이것이 **Tight Constraint**이며 특징은 **최소 크기 == 최대 크기** 이다.

### Loose Constraint

Center는 Loose Constraint를 전달하는 대표 위젯이다.

위의 코드를 아래와 같이 수정해보면
```dart
import 'package:flutter/material.dart';

void main() {
  runApp(MaterialApp(home: Constraint1()));
}

class Constraint1 extends StatelessWidget {
  const Constraint1({super.key});

  @override
  Widget build(BuildContext context) {
    return Scaffold(
      body: Container(
        width: 300,
        height: 300,
        color: Colors.blue,
        child: Center(
          child: Container(width: 100, height: 100, color: Colors.red),
        ),
      ),
    );
  }
}
```
Container와 Container 사이에 Center 위젯을 추가해주었다.

Center는 부모로부터 받은 최대 크기 범위 안에서 자식이 자유롭게 크기를 정할 수 있도록 Loose Constraint를 전달한다. 자식 Container가 크기를 정해서 위로 알려주면(Sizes go up), Center가 배치를 해준다(Parent sets position).
### Unbounded Constraints
부모가 자식한테 크기에 대해 완전한 자유를 준다면 어떻게 될까?
```dart
import 'package:flutter/material.dart';

void main() {
  runApp(MaterialApp(home: Constraint2()));
}

class Constraint2 extends StatelessWidget {
  const Constraint2({super.key});

  @override
  Widget build(BuildContext context) {
    return Scaffold(
      body: Column(
        children: [
          Text('Unbounded Constraint', style: TextStyle(fontSize: 24)),
          ListView.builder(
            itemCount: 20,
            itemBuilder: (context, index) =>
                ListTile(title: Text('Tile $index')),
          ),
        ],
      ),
    );
  }
}
```
ListView.builder를 사용해 20개의 타일을 생성했지만, 화면에 정상적으로 표시되지 않는다.

Column은 세로 한계가 없는 unbounded, 즉 자식에게 세로 한계를 강제하지 않는 위젯이다. ListView는 스크롤 가능한 영역이라 가능한 만큼 최대한 커지려고 하는데 부모인 Column이 크기를 정해주지 않아서 ListView는 자신의 크기를 계산하지 못해 Constraint 충돌이 발생한다.

### Bounded Constraints
위의 코드를 아래와 같이 수정해보면
```dart
import 'package:flutter/material.dart';

void main() {
  runApp(MaterialApp(home: Constraint2()));
}

class Constraint2 extends StatelessWidget {
  const Constraint2({super.key});

  @override
  Widget build(BuildContext context) {
    return Scaffold(
      body: Column(
        children: [
          Text('Unbounded Constraint', style: TextStyle(fontSize: 24)),
          Expanded(
            child: ListView.builder(
              itemCount: 20,
              itemBuilder: (context, index) =>
                  ListTile(title: Text('Tile $index')),
            ),
          ),
        ],
      ),
    );
  }
}
```
ListView를 Expanded로 감싸면..

가장 먼저 고정 크기를 계산한다. 부모 Column은 자식들 중 Expanded가 아닌 자식들의 크기를 계산하고, 남은 물리적 공간을 계산한 후에 Expanded는 자식 ListView에게 새로운 Constraint를 내려준다.

결과적으로 Expanded는 부모 Column이 내려준 Unbounded를 물리적인 공간을 계산해 자식에게 Bounded Constraint으로 변환해서 내려준 것이다.
## Constraint를 다루는 위젯 (Constraint Control Widget)
### Flex 공간 할당 위젯 (남은 공간 분배)
Row나 Column 같은 Flex 기반 레이아웃 안에서 가용 공간(Available Space)을 어떻게 나눠가질지 결정한다.
- Expanded (강제 공간 채움)
  - 동작 원리: 부모의 남은 공간을 모두 계산한 뒤, 자식에게 Tight Constraint를 내린다.
  - 오버플로우를 막을 때 1순위로 사용한다.
- Flexible (최대 한계치 부여)
  - 동작 원리: 부모의 남은 공간을 모두 계산한 뒤, 자식에게 Loose Constraint를 내린다.
  - 자식 위젯의 본래 크기가 남은 공간보다 작다면, 억지로 팽창시키지 않고 원래 크기만 유지한다는 점에서 Expanded와 차이가 있다.

### 명시적 크기 제어 위젯
부모가 내려주는 제약을 바탕으로, 개발자가 원하는 수치를 직접 개입시킬 때 사용한다.
- SizedBox (절대 크기 강제)
  - 동작 원리: 자식에게 정확한 width와 height을 강제한다.
  - 자식이 없다면 그 크기만큼의 투명한 빈 공간이 되어 여백을 만드는 용도로 쓰인다.
- ConstrainedBox (최소/최대 한계선 설정)
  - 동작 원리: BoxConstraints(minWidth, maxWidth, …) 객체를 사용하여 자식이 가질 수 있는 크기의 범위를 디테일하게 제한한다.
  - 모바일 화면 크기에 따라 UI가 너무 커지거나 작아지는 것을 막을 때 유용하다.
### 제약 완화 및 정렬 위젯
부모가 제약을 강제할 때, 그 압력을 풀어주는 역할을 한다.
- Center / Align
  - 동작 원리: 부모의 Tight Constraint를 자신이 대신 흡수하여 부모의 크기만큼 팽창한 후, 자식에게 Loose Constraint를 내려준 뒤 결정된 크기를 바탕으로 Positioning만 수행한다.
