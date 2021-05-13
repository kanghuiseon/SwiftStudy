# 04. Advanced Control Flow
> 이번 챕터에서는 for loop를 배울 것이다. 또한 switch 문도 배우는데, 둘 다 Swift에서는 굉장히 중요한 문법들이다. 
<br/>
<br/>
<br/>

## Countable ranges
* for loop문을 공부하기 전에, **Countable Range**라는 데이터 타입에 대해 알아야 한다. 이것은 어떤 범위내에서의 정수들의 순서를 표현하는 타입인데 아래의 예시를 보자.
```swift
let closedRange = 0...5
```
* 위의 코드에서 세 개의 점들은 범위를 나타낸다. 위에서는 0 부터 5까지의 범위를 나타낸다. (0, 1, 2, 3, 4, 5)
<br/>
<br/>

```swift
let halfOpenRange = 0..<5
```
* ..<는 **countable half-open range**라고 한다.
* 점 세개 말고도 범위를 나타낼 수 있다. ..<는 마지막 숫자를 제외한 범위를 의미한다. 위의 예시에서는 (0, 1, 2, 3, 4)를 의미한다.
<br/>
<br/>

* open, half-open ranges 둘 다 항상 증가해야 한다. 즉, 왼쪽의 숫자는 항상 오른쪽의 숫자보다 작아야 한다. 
* Countable ranges는 흔히 for loop, switch 문에서 사용된다.
<br/>
<br/>

### A random interlude
* 프로그래밍에서는 랜덤 숫자가 필요한 경우가 있다. Swift는 간단하게 생성할 수 있도록 한다.
```swift
while Int.random(in: 1...6) != 6 {
  print("Not a six")
}
```
* 위의 예시에서, Int 타입의 타입 메소드인 random in 에 위에서 배운 countable ranges를 사용해서, 1과 6사이의 랜덤 숫자를 도출하도록 한다. 6이 나올때까지 while문 내부를 반복한다.
<br/>
<br/>
<br/>
<br/>

## For loops
* for문은 굉장히 많이 사용되는 문법이다. 다음의 모습을 가진다.
```swift
for <CONSTANT> in <COUNTABLE RANGE> {
  <LOOP CODE>
}

let count = 10
var sum = 0
for i in 1...count {
  sum += i
}
```
* 우선 for 키워드로 시작하고, loop constant 를 다음에 쓴다. 이후에 in을 쓰고, 그 다음에 countable range를 쓴다.
* 예시에서, for loop는 1부터 count까지 반복되고, 첫번째 iteration에서, i는 1부터 시작해서, 각 iteration마다 1씩 증가한다. (count까지)
* 만약 ... 이 아니라 ..<을 사용한다면, count-1까지 반복된다.
* 위의 코드를 실행시키면, loop내부에서 i 를 sum에 계속해서 더한다. (i가 10일 때, sum 은 45가 되고 for문은 끝이 난다.)
* 여기서도 scope의 개념을 볼 수 있는데, i는 for 문에서만 사용될 수 있는 for constant이므로, for문 밖에서는 사용할 수 없다.
<br/>
<br/>

```swift
sum = 0
for i in 1...count where i % 2 == 1 {
  sum += i
}
```
* for문에도 조건을 달 수 있는데, where을 이용해서 where에 해당하는 조건이 true일 때만 for문 내부의 코드를 실행하도록 하고, 그렇지 않으면 다음 iteration으로 넘어간다.
<br/>
<br/>
<br/>

## Continue and labeled statements
* 때때로, for문 전체를 실행하지 않고, iteration을 건너뛸 수도 있다. **continue**문을 사용하면 되는데, continue를 사용하면 밑의 코드를 실행시키지 않고 바로 다음 iteration으로 넘어간다.
```swift
sum = 0

for row in 0..<8 {
  if row % 2 == 0 {
    continue
  }

  for column in 0..<8 {
    sum += row * column
  }
}
```
* 위의 코드를 보면, 만약 row가 2로 나누어 진다면 아래의 for문을 실행시키지 않고, 다음 iteration으로 넘어간다. 만약 2로 나누어 떨어지지 않는다면 아래의 for문을 실행시킨다.
<br/>
<br/>
<br/>

```swift
sum = 0

rowLoop: for row in 0..<8 {
  columnLoop: for column in 0..<8 {
    if row == column {
      continue rowLoop
    }
    sum += row * column
  }
}
```
* 위의 코드에서, 각 block전에 이름을 붙인 것을 **labeled statements**라고 한다. 
* 첫번째 for문의 이름을 rowLoop라고 붙이고, 두번째 for문의 이름을 columnLoop라고 붙여서, 만약 row와 column이 같다면, 아래의 sum += row * column코드는 실행되지 않고 바로 rowLoop의 다음 iteration이 실행된다.
<br/>
<br/>
<br/>
<br/>

## Switch statements
```swift
let number = 10

switch number {
case 0:
  print("Zero")
default:
  print("Non-zero")
}
```
* switch문은 상수나 변수의 값에 따라서 코드를 다르게 실행한다.
* 만약 number가 0인 경우에는 Zero를 출력하고, 그렇지 않으면 Non-zero를 출력한다.
<br/>
<br/>

```swift
switch number {
case 10:
  print("It’s ten!")
default:
  break
}
```
* 위의 경우에서는 number가 10이기 때문에, It's ten!이 출력된다.
* 만약 어떤 경우에 코드를 실행시키고 싶지 않다면, **break**문을 사용하면 된다. 이것은 더 이상 실행시킬 코드가 없다고 알려주는 것이다.
* case들은 절대로 비어있으면 안되기 때문에, 만약 실행시킬 코드가 없다면 꼭 break를 사용한다.
<br/>
<br/>

```swift
let string = "Dog"

switch string {
case "Cat", "Dog":
  print("Animal is a house pet.")
default:
  print("Animal is not a house pet.")
}
```
* string에 대해서도 switch문을 사용할 수 있는데, 위의 예시에서, 만약 string이 Cat or Dog이면 해당 case문의 코드를 실행한다는 것이다.
* string 이 Dog이기 때문에, Animal is a house pet이 실행된다.

### Advanced switch statements
```swift
let hourOfDay = 12
var timeOfDay = ""

switch hourOfDay {
case 0, 1, 2, 3, 4, 5:
  timeOfDay = "Early morning"
case 6, 7, 8, 9, 10, 11:
  timeOfDay = "Morning"
case 12, 13, 14, 15, 16:
  timeOfDay = "Afternoon"
case 17, 18, 19:
  timeOfDay = "Evening"
case 20, 21, 22, 23:
  timeOfDay = "Late evening"
default:
  timeOfDay = "INVALID HOUR!"
}

print(timeOfDay)
```
* switch문에서도 여러 개의 Case문을 사용할 수 있다. 
* 위의 예시에서는, hourOfDay가 12기 때문에 세번째 case문이 실행되어서, timeOfDay는 Afternoon이 된다.
* 여기서도 ranges를 사용할 수 있는데, 위의 코드를 아래와 같이 변경할 수 있다.
```swift
switch hourOfDay {
case 0...5:
  timeOfDay = "Early morning"
case 6...11:
  timeOfDay = "Morning"
case 12...16:
  timeOfDay = "Afternoon"
case 17...19:
  timeOfDay = "Evening"
case 20..<24:
  timeOfDay = "Late evening"
default:
  timeOfDay = "INVALID HOUR!"
}
```
* 여러 개의 case들이 있다면, 해당되는 case문 하나만 실행이 된다. 
<br/>
<br/>
<br/>

```swift
switch number {
case let x where x % 2 == 0:
  print("Even")
default:
  print("Odd")
}
```
* 위의 switch 문은 let-where 문법을 사용했다. 만약 특정 조건이 true일 때, 해당 case문이 실행된다.
* let 부분에서는 위의 number라는 value를 x라는 이름으로 묶고, 만약 해당 x가 where이후의 조건을 만족하면, 해당 case문이 실행된다.
* 이렇게 조건에 기반해서 value를 매칭시키는 방법을 **pattern matching**이라고 한다. 

```swift
switch number {
case _ where number % 2 == 0:
  print("Even")
default:
  print("Odd")
}
```
* 이 전의 예시에서는 조건문을 위해 불필요한 상수인 x를 만들었다. 위의 코드는 x를 사용하지않고 number를 바로 사용하기 위해서 x 대신에 **_** 를 사용해서, 불필요한 상수를 만들지 않도록 한다.
<br/>
<br/>
<br/>

### Partial matching
```swift
let coordinates = (x: 3, y: 2, z: 5)

switch coordinates {
case (0, 0, 0): // 1
  print("Origin")
case (_, 0, 0): // 2
  print("On the x-axis.")
case (0, _, 0): // 3
  print("On the y-axis.")
case (0, 0, _): // 4
  print("On the z-axis.")
default:        // 5
  print("Somewhere in space")
}
```
* 위의 코드처럼 언더바를 이용해서 switch문을 구성하는 것을 **partial matching** 이라고 한다. 
* 차례대로 설명을 해보자면
1. x, y, z가 모두 0인 경우에 Origin을 출력한다.
2. y, z가 0이고, x는 어떤 수여도 상관없다면, On the x-axis를 출력한다.
3. x, z가 0이고 y는 어떤 수여도 상관없다면, On the y-axis를 출력한다.
4. x, y가 0이고 z는 어떤 수여도 상관없다면, On the z-axis를 출력한다.
5. 그 외에는 Somewhere in space를 출력한다.
<br/>

* 어떤 값이라도 상관이 없을 때 언더바를 사용할 수 있다.

```swift
switch coordinates {
case (0, 0, 0):
  print("Origin")
case (let x, 0, 0):
  print("On the x-axis at x = \(x)")
case (0, let y, 0):
  print("On the y-axis at y = \(y)")
case (0, 0, let z):
  print("On the z-axis at z = \(z)")
case let (x, y, z):
  print("Somewhere in space at x = \(x), y = \(y), z = \(z)")
}
```
* 만약 값을 무시하고 싶지 않다면, binding하여서 switch 문에서 사용할 수 있다.
* 위의 코드에서 해당 값을 case문 내에서 사용하고 싶을 때 let 을 사용하였다. 
* 위의 코드에서는 마지막 case문이 default역할을 하였기 때문에 따로 default가 사용되지 않았다. 
* 만약 switch 문이 모든 가능성있는 값들의 case를 작성했다면 따로 default는 필요없다.
<br/>
<br/>



