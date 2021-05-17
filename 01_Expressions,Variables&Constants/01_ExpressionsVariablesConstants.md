# 1 Expressions, Variables & Constants

중략

# Getting started with Swift

## Code Comments

프로그램을 작성할때는 방향성을 잃지 않도록 document하는게 중요하다.

```swift
// This is also a comment.
// Over multiple lines.
```

`//` 를 이용해서 주석작성이 가능하다.

```swift
/* This is also a comment.
   Over many..
   many...
   many lines. */
```

여러줄 주석은 `/*` 로 열고 `*/` 로 닫아서 사용가능하다.

```swift
/* This is a comment.
 
 /* And inside it 
 is 
 another comment.
 */
 
 Back to the first.
 */
```

nested된 주석도 이용가능하다.

# Printing out

```swift
print("Hello, Swift Apprentice reader!")
```

# Arithmatic operation

## Simple operation

```swift
2 + 6
10 - 2
2 * 4
24 / 3
```

```swift
2+6   // OK
2 + 6 // OK
2 +6  // ERROR
2+ 6  // ERROR
```

둘다 띄우거나 붙이는건 가능하지만 한쪽만 붙여쓰는것은 불가능하다.

## Decimal number

```swift
22 / 7
```

식이 intege로만 구성되어 있기 때문에 결과는 3이다. 

```swift
22.0 / 7.0
```

식을 실수로 구성하면 결과는 3.14~가 나온다.

## The remainder operation

```swift
28 % 10
```

모듈로 연산이다.

```swift
(28.0).truncatingRemainder(dividingBy: 10.0)
```

실수에대해 모듈로 연산을 적용하고 싶으면 위 방법으 쓰면된다.

## Shift operations

```swift
1 << 3

32 >> 2
```

쉬프트연산이다. 2진법에서 자리를 좌우로 쉬프트해준다.

## Order of operations

사칙연산 순서를 따른며 괄호를 추가해서 우선순위르 ㄹ부여할수도 있다.

```swift
((8000 / (5 * 10)) - 32) >> (29 % 5)
```

# Math finctions

Swift는 다양한 수학함수를 제공한다.

```swift
sin(45 * Double.pi / 180)
// 0.7071067811865475

cos(135 * Double.pi / 180)
// -0.7071067811865475
```

삼각함수와 스위프트가 제공하는 constant `Double.pi` 를 이용할수 있다.

```swift
(2.0).squareRoot()
// 1.414213562373095
```

양의 제곱근은 위와같이 이용가능하다.

```swift
max(5, 10)
// 10

min(-5, -10)
// -10

max((2.0).squareRoot(), Double.pi / 2)
// 1.570796326794897
```

max,min 함수도 제공하며 다른 함수와 결합가능하다.

# Naming data

## Constants

```swift
let number: Int = 10
let pi: Double = 3.14159
number = 0
```

let을이용하며 뒤에 타입을 지정한다. 실수의 경우 Float도 있지만 대부분 Double을 이용한다.

- 재할당이 불가능하다.

## Variables

```swift
var variableNumber: Int = 42
variableNumber = 0
variableNumber = 1_000_000
```

var 키워드를 쓴다는 점외에는 constant와 동일하다. 

- `_` 를 사용해서 수를 나타낼수도 있는데 특별한 차이가 있는것은 아니나 가독성을 위해 붙일수도 있다. complier는 그냥 무시한다.

## Using meaningful names

Swift는 ``Camel Case` 를 이용한다.

**좋은예**

- `personAge`
- `numberOfPeople`
- `gradePointAverage`

**나쁜예**

- `a`
- `temp`
- `average`

명명규칙은 아래와 같다.

- 소문자로 시작해야한다.
- 여러단어로 이루어지면 다음단어의 첫번째 문자를 대문자로 쓴다.
- 만일 단어중하나가 약자면 다른 모든경우에도 해당약자를 사용한다.(e.g.: `sourceURL` and `urlDescription`)

```swift
var 🐶💩: Int = -1
```

- 심지어 이모티콘도 이름으로 사용가능하나 그다지 좋은 선택은 아니다.

# Increment and decrement

```swift
var counter: Int = 0

counter += 1
// counter = 1

counter -= 1
// counter = 0

counter = 10

counter *= 3  // same as counter = counter * 3
// counter = 30

counter /= 2  // same as counter = counter / 2
// counter = 15
```

위와같은 연산자가 사용가능하다.