# 03. BasicControlFlow
> control flow란, 프로그램의 흐름을 다양한 방법으로 제어하는 방법을 말한다.
<br/>
<br/>

## Comparison operators
* 두 개의 숫자 중, 더 큰 숫자를 무엇이냐!와 같은 문제의 답은 true or false이다. 
* Swift는 Bool이라는 이름의 타입을 가지고 true, false를 다룬다. (Bool은 Boolean의 짧은 말)
```swift
let yes: Bool = true
let no: Bool = false

let yes = true
let no = false
```
* 또한 Swift에서는 타입 추론이 가능하기 때문에, 아래와 같이 타입을 명시하지 않아도 된다.
* Boolean은 true, false만 있다!
<br/>
<br/>

### Boolean operators
* Boolean은 값을 비교하기 위해 자주 사용이 되는데, 예를 들어서, 두 개의 값이 있다고 생각해보자. 만약 그 두 개가 같은 값인지를 알고 싶을 때, Boolean을 사용할 수 있다. (만약 같으면 true, 다르면 false)
* Swift에서는 equality operator를 이용해서, 위의 답을 도출할 수 있다.
```swift
let doesOneEqualTwo = (1 == 2)
```
* Swift 는 doesOneEqualTwo가 Bool임을 추론하고, 1과 2가 다르므로 false를 doesOneEqualTwo 변수에 할당한다.
<br/>

* 유사하게, 아래처럼 두 값이 다른지 아닌지를 판단하고 싶을때는 != operator를 이용하면 된다.
```swift
let doesOneNotEqualTwo = (1 != 2)
```
* 1과 2는 다르므로 true를 doesOneNotEqualTwo에 할당한다.
* ! operator는 not을 의미하며, true를 false로 바꾸거나, false를 true로 바꾸는 역할을 한다.
* 아래와 같이 사용할 수도 있다.
```swift
let alsoTrue = !(1 == 2)
```
* 1과 2는 같이 않기 때문에 false를 도출하고, !가 false를 true로 바꾸기 때문에 alsoTrue에는 true가 할당된다.
<br/>
<br/>
<br/>

* == 과 != 말고도 값을 비교할 수 있는 operators가 있다. '>', '<'는 더 크거나 더 작거나를 결정할 수 있다.
```swift
let isOneGreaterThanTwo = (1 > 2)
let isOneLessThanTwo = (1 < 2)
```
* isOneGreaterThanTwo는 false이고, isOneLessThanTwo는 true이다.
* <= or >= 과 같이 작거나 같고, 크거나 같은 것도 표현할 수 있다.
<br/>
<br/>
<br/>

### Boolean logic
* 위의 예시들은 한가지 조건에 대한 것이었고, 지금부터는 여러개의 조건들을 합치도록 하는 **Boolean logic**에 대해서 배워보자.
* 첫번째 방법은 **AND** 를 사용하는 것이다. 만약 input으로 들어온 Boolean들이 모두 true이면, 그 결과는 true이다. 만약 하나라도 true 가 아니면 false 를 반환한다.
```swift
let and = true && true
```
* Swift에서 AND는 **&&** 으로 표현한다. 
* 위의 경우에는 and에는 true가 될 것이다. 만약 둘 다 and는 false가 될 것이다.
<br/>
<br/>
<br/>

```swift
let or = true || false
```
* OR 을 사용해서, 조건들을 합칠 수도 있다. 만약 두개의 Booleans을 OR로 합친다면, input으로 들어온 Boolean들 중에 하나라도 true이면 true이고, 전체가 false라면 결과는 false가 된다.
* Swift에서는 Boolean OR에 대한 operators는 | |를 사용한다.
* 위의 경우에서, or는 둘 중에 하나가 true기 때문에 true가 된다.
<br/>

```swift
let andTrue = 1 < 2 && 4 > 3
let andFalse = 1 < 2 && 3 > 4

let orTrue = 1 < 2 || 3 > 4
let orFalse = 1 == 2 || 3 == 4
```
* Swift에서는 boolean logic을 이용해서, 여러 개의 조건들을 계산한다. 두 개의 조건문이 true인지 확인하기 위해서는, AND를 사용하고, 하나라도 true를 포함하는지를 확인하고 싶을 때는 OR를 사용한다.
* 물론, 두 개 이상의 조건문을 합치는 것도 가능하다!
<br/>

```swift
let andOr = (1 < 2 && 3 > 4) || 1 < 4
```
* 괄호를 이용해서, 먼저 계산하고 싶은 조건문을 지정할 수도 있다. 괄호에 있는 조건문을 먼저 계산하고, 나머지를 순서대로 계산한다.
<br/>
<br/>

### String equality
* 두 개의 string 이 똑같은지를 알고 싶을때도 비교 연산자를 사용할 수 있다.
```swift
let guess = "dog"
let dogEqualsCat = guess == "cat"

let order = "cat" < "dog"
```
* == 을 이용해서, 두 개의 string이 동일한지를 판단할 수 있다.
* guess인 dog와 cat은 다른 문자열이므로, dogEqualsCat에는 false가 반환된다.
* string을 알파벳순으로 비교할 때에도 비교 연산자를 사용할 수 있다.
* 위의 예시에서, 사전순으로 봤을 때, cat보다 dog가 더 앞에 있기 때문에, order에는 true가 반환된다.
<br/>
<br/>

### Toggling a Bool
```swift
var switchState = true
switchState.toggle() // switchState = false
switchState.toggle() // switchState = true
```
* Bool은 **on** or **off**의 상태를 나타내기도 한다. 상태를 변환시킬때 사용된다.
* 예를 들어서, light switch의 상태를 나타낼 때 Bool을 사용할 수 있다. 
* 또한 이 값을 이용해서, on일 때 off, off일 때 on과 같이 현재 상태를 toggle할 수도 있다.
* 처음에 switchState는 true이고, toggle이후 false로 바꼈다가 다시 toggle하여 다시 true가 되었다.
<br/>
<br/>

## The if statement
```swift
if 2 > 1 {
  print("Yes, 2 is greater than 1.")
}
```
* 프로그램의 흐름을 제어하는 방법 중 하나는 **if statement** 이다.
* if의 조건문이 true이면 if 이후 괄호의 내부 코드를 실행한다.
* 만약 조건문이 false이면 괄호 내부의 코드를 실행하지 않고 바로 다음으로 넘어간다.
<br/>
<br/>

```swift
let animal = "Fox"

if animal == "Cat" || animal == "Dog" {
  print("Animal is a house pet.")
} else {
  print("Animal is not a house pet.")
}
```
* if 문의 조건과 다른 조건을 추가할 수도 있는데, 그럴 때는 **else clause**를 사용한다.
* 만약 if 문의 조건을 만족하지 않으면, 무조건 else문 의 코드를 실행시킨다.
* animal은 "Fox"기 때문에 if 문의 조건은 만족하지 않는다. 그러므로 else문 내부의 코드를 실행한다.
* 물론, 두 개의 조건만 볼 수 있는 것은 아니다. else-if문을 이용해서 조건문을 더 많이 추가할 수도 있다. 아래의 코드를 보자.
```swift
let hourOfDay = 12
var timeOfDay = ""
if hourOfDay < 6 {
  timeOfDay = "Early morning"
} else if hourOfDay < 12 {
  timeOfDay = "Morning"
} else if hourOfDay < 17 {
  timeOfDay = "Afternoon"
} else if hourOfDay < 20 {
  timeOfDay = "Evening"
} else if hourOfDay < 24 {
  timeOfDay = "Late evening"
} else {
  timeOfDay = "INVALID HOUR!"
}
print(timeOfDay)
```
<br/>
<br/>
<br/>

### Short-circuiting
* if 문에서도 AND, OR를 이용해서 여러 개의 조건을 넣을 수 있다.
```swift
if 1 > 2 && name == "Matt Calloway" {
    // ...
}
```
* if 문의 첫번째 조건은 false여서, &&에 의해 전체 조건이 false가 되었다.
* 만약 &&가 아니라 | | 였다면, name이 Matt Calloway라면 true가 되어서 if 문 내부가 실행된다.
<br/>
<br/>
<br/>

### Encapsulating variables
* if 문에서 **scope**이라는 개념을 볼 수 있는데, 괄호를 사용해서, 값들을 encapsulate하는 방식이다. 
* 다음의 문장을 if문으로 표현해보자. "만약 하루에 40시간을 일하면 시간 당 25원을 벌고 그 이후 부터는 시간당 50원을 번다."
```swift
var hoursWorked = 45

var price = 0
if hoursWorked > 40 {
  let hoursOver40 = hoursWorked - 40
  price += hoursOver40 * 50
  hoursWorked -= hoursOver40
}
price += hoursWorked * 25

print(price)
```
* 위의 코드는 일한 시간이 40시간을 넘는지 아닌지를 체크한다. 만약 40시간을 넘기면 추가 시간을 확인하고, 그 시간에 대해서 50원을 곱하여서 추가금에 대해 계산한다. 결과적으로 마지막 price는 1250원이 된다.
* if 문 내부의 코드를 보면, 새로운 상수인 hoursOver40이 선언되는데, 이 상수는 괄호를 벗어나면 사용할 수 없다. 오직 if 문 내부에서만 사용할 수 있다.
* 각 scope마다는 또 외부에 scope이 있을 수 있는데, 외부 scope에서 선언된 상수나 변수는 그 내부의 scope에서는 사용할 수 있다. 하지만 내부 scope에서 선언된 상수나 변수는 외부 scope에서는 사용할 수 없다.
<br/>
<br/>
<br/>

### The ternary conditional operator
```swift
let a = 5
let b = 10

let min: Int
if a < b {
  min = a
} else {
  min = b
}

let max: Int
if a > b {
  max = a
} else {
  max = b
}
```
* min값과 max값을 계산하고자 할 때 위와 같이 if문을 이용해서 계산할 수 있다. 하지만 너무 길기 때문에 이것을 좀 줄일 필요가 있다.
* 이때, 사용하는 것이 ternary conditional operator이다.
* 모양은 (<CONDITION>) ? <TRUE VALUE> : <FALSE VALUE> 이다.
* CONDITION이 true라면 ? 뒤의 값으로 할당하고, 그렇지 않다면 : 뒤의 값으로 min, max값에 할당한다.
* 위의 조건문을 위의 모습으로 바꾼다면 아래와 같이 짧게 바꿀 수 있다.
```swift
let a = 5
let b = 10

let min = a < b ? a : b
let max = a > b ? a : b
```
* 코드를 보자면, a는 b보다 작기 때문에 위의 조건문은 true이다. 따라서 min에는 a값이 할당된다.
* 아래의 조건문은 false이기 때문에, : 뒤의 값인 b가 max에 할당된다.
<br/>
<br/>
<br/>

## Loops
* Loops는 코드를 여러번 실행하기 위해서 사용된다.
<br/>
<br/>

### While loops
```swift
while <CONDITION> {
  <LOOP CODE>
}
```
* while loop에서는 조건이 true일 때, 코드 블록을 반복해서 실행한다.
* 여기서는 모든 iteration마다 조건을 확인해서 조건이 true이면 다시 실행하고, 다시 조건을 확인해서 true면 다시 실행하고, 이 작업을 반복한다. 만약 조건이 false라면 while문을 빠져나오게 된다.
```swift
while true { }
```
* 위의 코드에서는, 조건이 항상 true이기 때문에, loop가 끝나지 않는다. 이것을 **infinite loop(무한루프)**라고 하며, 프로그램이 끝나지 않기 때문에 이런 방식은 절대로 사용하면 안된다. 
<br/>
<br/>

```swift
var sum = 1

while sum < 1000 {
  sum = sum + (sum + 1)
}
```
* 위의 loop를 순서대로 설명해보자면,
* iteration 1 전에는 sum=1이기 때문에, loop condition은 true이다.
* iteration 1 이후에는 sum = 3 이기 때문에, loop condition은 true이다.
* iteration 2 이후에는 sum = 7 이기 때문에, loop condition은 true이다.
* iteration 3 이후에는 sum = 15 이기 때문에, loop condition은 true이다.
* iteration 4 이후에는 sum = 31 이기 때문에, loop condition은 true이다.
* iteration 5 이후에는 sum = 63 이기 때문에, loop condition은 true이다.
* iteration 6 이후에는 sum = 127 이기 때문에, loop condition은 true이다.
* iteration 7 이후에는 sum = 255 이기 때문에, loop condition은 true이다.
* iteration 8 이후에는 sum = 511 이기 때문에, loop condition은 true이다.
* iteration 9 이후에는 sum = 1023 이기 때문에, loop condition은 false이다.
* 9번의 iteration 이후에 sum은 1023이 되었기 때문에 조건을 충족시키지 않아서, loop가 정지된다.
<br/>
<br/>

### Repeat-while loops
```swift
repeat {
  <LOOP CODE>
} while <CONDITION>
```
* Repeat-while loops는 while loop의 변형이다. while문을 앞에 두지 않고, 뒤에 두고 무조건 먼저 한번 실행되어야 한다면 repeat-while loop를 사용한다.
```swift
sum = 1

repeat {
  sum = sum + (sum + 1)
} while sum < 1000
```
* 위의 코드에서도 sum이 먼저 sum + 1과 더해지고나서 while문을 실행한다.
<br/>
<br/>
<br/>

## Breaking out of a loop
* 만약 loop를 더 빨리 끝내고 싶다면, break문을 사용할 수 있다. 이것을 이용해서 loop 실행을 바로 멈추고 loop 이후의 코드를 계속해서 실행한다.
```swift
sum = 1

while true {
  sum = sum + (sum + 1)
  if sum >= 1000 {
    break
  }
}
```
* 우선 조건이 true기 때문에 while문은 계속해서 실행될 것이다. 하지만 만약 sum이 1000보다 같거나 커지게 된다면 if 문 내부의 break를 실행해서 while문을 중지하고 나간다.
<br/>
<br/>
<br/>
<br/>


