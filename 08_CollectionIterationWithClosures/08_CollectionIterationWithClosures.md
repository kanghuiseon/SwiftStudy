# 08. Collection Iteration with Closures
> 앞에서 우리는 functions에 대해서 배웠다. 하지만 Swift에서는 관련 코드를 reusable 한 형태로 사용할 수 있는 object를 제공한다. 이것을 **closure** 라고 한다. closure는 특히 collection을 다룰 때, 유용하게 쓰인다.
> closure는 이름이 없는 함수이다. 클로저를 변수에 할당할 수도 있고, 다른 값들 처럼 전달할 수도 있다.
<br/>
<br/>
<br/>

## Closure basics
* 클로저 내부에 상수나 변수를 "close over"(에워싸다) 할 수 있기 때문에 closure라고 이름이 붙여졌다.
* 또한, 클로저 내부에서 정의된 상수나 변수는 클로저에 의해 **캡쳐되었다** 라고도 한다.
* 클로저를 사용하기 위해서는 우선 변수나 상수에 할당을 해야 한다.
```swift
var multiplyClosure: (Int, Int) -> Int
```
* multiplyClosure는 두 개의 Int형 값들을 밭아서 하나의 Int형 값을 리턴한다.
* 클로저는 이름이 없는 함수이기 때문에 클로저의 타입은 함수 타입과 동일하다.
<br/>
<br/>

```swift
var multiplyClosure = { (a: Int, b: Int) -> Int in
  return a * b
}
```
* 언뜻보면, 함수 선언과 유사한다. 살짝 차이점이 있다.
* 클로저에서는 파라미터 리스트와 ->, 리턴 타입이 대괄호로 둘러쌓여있고, 리턴 타입 이후에 in 키워가 있다.
```swift
let result = multiplyClosure(4, 2)
```
* 실제로 사용은 위와 같이 함수처럼 사용하면 된다.
<br/>
<br/>
<br/>

### Shorthand syntax
* 함수와 비교해서, 클로저는 굉장히 간편하게 사용할 수 있도록 만들어졌다.
* 위에서 본 문법보다 더 간단하게 구성할 수 있는데, 첫번째로 만약 클로저가 하나의 리턴 문으로 구성되어있다면 return 키워드를 삭제할 수 있다.
```swift
multiplyClosure = { (a: Int, b: Int) -> Int in
  a * b
}
```
<br/>

* 또한, Swift의 타입 추론을 이용해서, 문법을 줄일 수도 있다.
```swift
multiplyClosure = { (a, b) in
  a * b
}
```
* 위에서 이미 multiplyClosure가 두개의 Int 형 값을 받고, Int형 값을 리턴한다고 타입을 명시해주었으므로, 따로 타입을 명시하지 않아도 된다.
<br/>

* 마지막으로, 파라미터 리스트도 생략할 수 있다.
* Swift는 0부터 시작하는 숫자로 각 파라미터를 지칭할 수도 있다.
```swift
multiplyClosure = {
  $0 * $1
}
```
* 마지막 문법을 보면, 파라미터 리스트, 리턴 타입, in 키워드가 모두 사라져서 원래보다 훨씬 더 짧아졌따.
* 만약 더 많은 파라미터를 받는 경우에는 헷갈릴 수 있기 때문에, 마지막에 숫자 파라미터는 클로저가 짧은 경우에만 사용해야 한다. 
<br/>
<br/>

```swift
func operateOnNumbers(_ a: Int, _ b: Int,
                      operation: (Int, Int) -> Int) -> Int {
  let result = operation(a, b)
  print(result)
  return result
}
```
* operateOnNumbers 함수는 두개의 Int 형 값을 받고, 세번째 파라미터로 operation이라는 이름의 function 타입을 받는다.
* operateOnNumbers 자체는 Int 형을 리턴한다.
<br/>
<br/>

```swift
let addClosure = { (a: Int, b: Int) in
  a + b
}
operateOnNumbers(4, 2, operation: addClosure)
```
* 위에서 생성한 operateOnNumbers의 세번 째 파라미터로 addClosure를 사용한다.
```swift
func addFunction(_ a: Int, _ b: Int) -> Int {
  a + b
}
operateOnNumbers(4, 2, operation: addFunction)
```
* 클로저는 이름이 없는 함수이기 때문에 operateOnNumbers의 세번째 파라미터로 함수를 건네줄 수도 있다.!
* operation이 함수든, 클로저든, operateOnNumbers는 똑같은 방식으로 호출된다.
<br/>
<br/>

* 클로저는 굉장히 유용하게 사용될 수 있다. 따로 함수나 클로저를 생성해서 파라미터로 넘겨줄 수도 있지만 아래와 같이 세번째 파라미터로 클로저를 바로 정의할 수도 있다.
```swift
operateOnNumbers(4, 2, operation: { (a: Int, b: Int) -> Int in
  return a + b
})
```
* 클로저를 따로 정의할 필요도 없고, 지역변수나 상수로 할당할 필요도 없다. 파라미터로 넘겨줄때, 그냥 바로 클로저를 생성해서 넘기면 된다.
<br/>
<br/>

* 여기서도 클로저 문법을 단순하게 할 수 있다.
```swift
operateOnNumbers(4, 2, operation: { $0 + $1 })
```
<br/>

* 실제로, 위의 코드보다 더 간단하게도 할 수 있다. + operator는 두개의 arguments를 받아서 하나의 값을 리턴하는 함수이기 때문에 + 를 바로 써도 된다.
```swift
operateOnNumbers(4, 2, operation: +)
```
<br/>

* 만약 클로저가 함수의 마지막 파라미터라면 아래와 같이 괄호밖으로 클로저를 옮길 수도 있다.
```swift
operateOnNumbers(4, 2) {
  $0 + $1
}
```
* operation label을 지우고, 괄호 밖으로 클로저를 옮기는 것이다. 이 클로저를 **trailing closure** 라고 하며, 한국말로는 후위 클로저라고 한다.
<br/>
<br/>
<br/>

### Multiple trailing closures syntax
* 만약 함수가 여러 개의 클로저를 input으로 받는다면, 특별한 방법으로 클로저를 파라미터값으로 보낼 수 있다.
* 아래와 같이 두 개의 클로저를 파라미터로 받는 함수가 있다고 생각해보자.
```swift
func sequenced(first: ()->Void, second: ()->Void) {
  first()
  second()
}
```
* Swift는 아래와 같은 방식으로 위의 함수를 호출하도록 할 수 있다.
```swift
sequenced {
  print("Hello, ", terminator: "")
} second: {
  print("world.")
}
```
* 위의 호출은 "Hello, world"를 출력할 것이다.
<br/>
<br/>

### Closures with no return value
* 만약 파라미터도 없고 리턴값도 없는 클로저를 생성하려고 한다면, 아래와 같이 클로저를 생성하면 된다.
```swift
let voidClosure: () -> Void = {
  print("Swift Apprentice is awesome!")
}
voidClosure()
```
* 클로저의 타입은 ( )->Void 이고, 빈 괄호는 파라미터가 없다는 것을 의미한다. 리턴 타입은 무조건 있어야 하므로, Void라는 이름의 타입을 지정해준다. (리턴타입이 없다는 의미)
    * Void 는 실제로 ( )의 typealias이다. 따라서 ( )->( )와 같은 의미를 가진다. 하지만 함수의 파라미터 리스트는 무조건 괄호로 생성해야 하므로 Void -> ( ) or Void -> Void는 유효하지 않다.
<br/>
<br/>

### Capturing from the enclosing scope
* 클로저는 자체 scope 에 정의된 상수나 변수에 접근할 수 있다.
* 예를 들어서, 아래의 코드를 보자.
```swift
var counter = 0
let incrementCounter = {
  counter += 1
}
```
* incrementCounter 는 counter 변수를 1씩 증가시킨다. 
* counter 변수는 closure바깥에 정의된 변수이다. 클로저는 해당 변수에 접근할 수 있는데, 그 이유는 클로저가 counter변수와 같은 위치에 정의되었기 때문이다.
<br/>

* 클로저는 여기서 counter 변수를 **capture** 했다고 할 수 있다. 값을 캡쳐한다는게 처음에는 무슨 의미인지 와닿지 않을 수 있는데, 아래의 예시를 보면 알 수 있다.
```swift
func countingClosure() -> () -> Int {
  var counter = 0
  let incrementCounter: () -> Int = {
    counter += 1
    return counter
  }
  return incrementCounter
}
```
* countingClosure함수는 파라미터를 받지 않고, ( ) -> Int 타입의 클로저를 리턴한다.
* 이 함수에서 리턴되는 클로저는 호출될때마다 내부 counter 변수를 증가시킬 것이다.
```swift
let counter1 = countingClosure()
let counter2 = countingClosure()

counter1() // 1
counter2() // 1
counter1() // 2
counter1() // 3
counter2() // 2
```
* countingClosure의 리턴값을 저장하는 두 개의 상수를 생성하였다.
* 그리고 나서, 각각의 상수를 두 번 이상 호출해보았더니, 각각 다른 값을 리턴하였다.
* 일반적으로 생각했을 때는 새로운 함수가 계속해서 호출되는 것이므로, 1이 리턴될 것이라고 생각하는데, 그렇지 않다.
* 실제로 incrementCounter 클로저는 counter라는 값을 캡쳐해서 가지고 있는 상태이기 때문에 호출될 때마다 가지고 있던 값을 가지고 1씩 증가시킨다. 
* 또한 counter1과 counter2는 각각 다른 클로저를 받았으므로, 따로 counter값을 증가시킨다.
<br/>
<br/>
<br/>

## Custom sorting with closures
```swift
let names = ["ZZZZZZ", "BB", "A", "CCCC", "EEEEE"]
names.sorted()
// ["A", "BB", "CCCC", "EEEEE", "ZZZZZZ"]
```
* Chapter 7에서 array의 sort메소드를 사용해서 배열을 정렬했다. closure를 이용해서, 어떤 식으로 정렬할지를 커스터마이징할 수 있다.
* sorted()를 호출하면 배열의 정렬된 버전을 얻을 수 있다.
* 커스텀 클로저를 이용하면, 배열이 정렬되는 방식을 바꿀 수 있다.
```swift
names.sorted {
  $0.count > $1.count
}
// ["ZZZZZZ", "EEEEE", "CCCC", "BB", "A"]
```
* 후위 클로저를 사용해서 기존의 오름차순이 아닌 내림차순으로 값을 정렬하도록 설정할 수도 있다.
<br/>
<br/>
<br/>
<br/>

## Iterating over collections with closures
* Swift에서, collection은 **functional programming**의 특징을 이용해서 collection에 대한 작업을 수행하도록 구현한다.
* 여기서 작업은 특정 값들을 필터링하거나 각 값들을 변형시키거나와 같은 것을 포함한다.
<br/>

### forEach
* 첫번째는 collection의 값들을 차례대로 접근하는 작업이다.
```swift
let values = [1, 2, 3, 4, 5, 6]
values.forEach { 
  print("\($0): \($0*$0)")
}
```
* forEach 는 collection 내부의 각 값들을 차례대로 접근하도록 한다.
<br/>
<br/>

### filter
```swift
var prices = [1.5, 10, 4.99, 2.30, 8.19]

let largePrices = prices.filter {
  $0 > 5
}
```
* 또 다른 함수인 filter는 원하는 값을 필터링하도록 한다.
* $5보다 큰 값을 저장하기 위해서 filter 함수를 사용하였다.
* 여기서 filter 함수를 자세히 살펴보자.
```swift
func filter(_ isIncluded: (Element) -> Bool) -> [Element]
```
* filter는 (Element) -> Bool 타입의 클로저를 파라미터로 받아서 [Element] 를 리턴 타입으로 가진다.
* 여기서 Element는 배열 내부의 값들의 타입을 의미하며, 여기서는 Doubles 이다.
* 클로저는 배열 내부의 값이 조건을 만족하는지 아닌지를 Bool값으로 알려준다.
* filter에서 리턴된 배열은 closure가 true를 리턴한 요소들로만 이루어져 있다. 여기서는 10, 8.19
<br/>
<br/>

### first(where:)
* 만약  해당 조건을 만족하는 첫번째 요소만 알고 싶다면, first(where: )를 이용하면 된다.
```swift
let largePrice = prices.first {
  $0 > 5
}
```
* 여기서 largePrice는 10이다.
<br/>
<br/>

### map
* 만약 prices의 값들에 대해 90% 할인을 해주고 싶다면, **map** 함수를 이용하면 된다.
```swift
let salePrices = prices.map {
  $0 * 0.9
}
```
* map 함수는 closure를 받아서, 배열의 각 값들에 대해 원하는 행동을 취하고, 마지막에, 변환된 값들을 가진 배열을 리턴한다.
* 여기서 salePrices는 [1.35, 9, 4.491, 2.07, 7.371] 이다.
* map 함수는 또한 타입을 변환시킬 때도 사용이 된다.
```swift
let userInput = ["0", "11", "haha", "42"]

let numbers1 = userInput.map {
  Int($0)
}
```
* "haha" 와 같이 Int로 변환할 수 없을 때도 있을 수 있기 때문에 리턴되는 값은 optional 타입이어야 한다. haha는 nil로 저장된다.
<br/>
<br/>

### compactMap
* 만약 mission value에 대해서 필터링 하고 싶다면, compactMap 함수를 이용한다.
```swift
let numbers2 = userInput.compactMap {
  Int($0)
}
```
* compactMap 함수는 map과 거의 유사한데, 다른 점이 있다면, nil값은 포함시키지 않는다는 것이다.
<br/>
<br/>

### flatMap
```swift
let userInputNested = [["0", "1"], ["a", "b", "c"], ["🐕"]]
let allUserInput = userInputNested.flatMap {
  $0
}
```
* 여기서 allUserInput은 ["0", "1", "a", "b", "c", "🐕"]이다.
* flatMap은 input으로 들어오는 모든 collection을 풀어서 하나의 collection으로 리턴한다.
<br/>
<br/>

### reduce
* reduce함수는 시작 값과 클로저를 파라미터로 받는다. 클로저는 두 개의 값을 받는다. (현재 값과 배열의 값).
```swift
let sum = prices.reduce(0) {
  $0 + $1
}
```
* initial 값은 0이고, 차례대로 현재의 값과 배열의 값을 더한다. 마지막에는 배열의 모든 값을 더한 값이 리턴된다. 여기서는 26.98이다.
<br/>
<br/>

* 위에서 배운 함수들은 딕셔너리에서도 사용할 수 있다. 
* 주식 가격과 아이템들의 개수가 매핑되어있는 딕셔너리를 생각해보자.
* 주식의 전체 값을 계산하기 위해서 reduce 함수를 사용할 수 있다. 여기서 결과는 384.5 이다.
```swift
let stock = [1.5: 5, 10: 2, 4.99: 20, 2.30: 5, 8.19: 30]
let stockSum = stock.reduce(0) {
  $0 + $1.key * Double($1.value)
}
```
<br/>
<br/>

### reduce(into:_:)
* reduce의 다른 형태로 reduce(into:_:) 가 있다.
* collection을 축소하는 결과가 array or dictionary일 때 사용한다. 예시를 보면,
```swift
let farmAnimals = [🐎": 5, "🐄": 10, "🐑": 50, "🐶": 1]
let allAnimals = farmAnimals.reduce(into: []) {
    (result, this: (key: String, value: Int)) in
    for _ in 0 ..< this.value {
        result.append(this.key)
    }
}
> print(["🐄", "🐄", "🐄", "🐄", "🐄", "🐄", "🐄", "🐄", "🐄", "🐄", "🐶", "🐎", "🐎", "🐎", "🐎", "🐎", "🐑", "🐑", "🐑", "🐑", "🐑", "🐑", "🐑", "🐑", "🐑", "🐑", "🐑", "🐑", "🐑", "🐑", "🐑", "🐑", "🐑", "🐑", "🐑", "🐑", "🐑", "🐑", "🐑", "🐑", "🐑", "🐑", "🐑", "🐑", "🐑", "🐑", "🐑", "🐑", "🐑", "🐑", "🐑", "🐑", "🐑", "🐑", "🐑", "🐑", "🐑", "🐑", "🐑", "🐑", "🐑", "🐑", "🐑", "🐑", "🐑", "🐑"]
)
```
```swift
let ddd = [2, 3, 4]
let fff = ddd.reduce(into: []) { result, value in
    for i in 0 ..< value{
        result.append(i)
    }
}
print(fff)

> print([0, 1, 0, 1, 2, 0, 1, 2, 3])
```
* reduce 함수는 farmAnimals를 돌면서 클로저를 실행시키지만, 어떤 값을 리턴하지는 않는다.
* 대신에 into: 에 원하는 값을 append 한다.
* 위의 예시에서는 배열 [ ] dksdp farmAnimals의 key와 value를 가지고, value의 개수만큼 key값을 result 배열에 추가하였다.
* 아래의 예시에서도 0부터 ddd의 각 값보다 작은 숫자를 result배열에 추가하였다.
* 결과값을 한 배열에 모두 합치고 싶을 때, 유용하게 사용된다.
<br/>
<br/>


### dropFirst
```swift
let removeFirst = prices.dropFirst()
let removeFirstTwo = prices.dropFirst(2)
```
* dropFirst 함수는 하나의 파라미터를 받고, 디폴트 값은 1이다.
* 또한 파라미터로 받은 숫자만큼 앞에서부터 자른 후의 결과를 배열에 집어넣고 리턴한다.
* 위의 결과값은, removeFirst = [10, 4.99, 2.30, 8.19], removeFirstTwo = [4.99, 2.30, 8.19] 
<br/>
<br/>

### dropLast
* dropFirst가 있듯이 dropLast도 있다.
* 이것도 이름처럼뒤에서부터 잘라서 그 결과 값을 배열로 리턴한다.
```swift
let removeLast = prices.dropLast()
let removeLastTwo = prices.dropLast(2)
```
* 결과는 removeLast = [1.5, 10, 4.99, 2.30], removeLastTwo = [1.5, 10, 4.99] 이다.
<br/>
<br/>

### prefix, suffix
```swift
let firstTwo = prices.prefix(2)
let lastTwo = prices.suffix(2)
```
* prefix는 가장 앞에서부터 원하는 숫자만큼 가져온다.
* suffix는 가장 뒤에서부터 원하는 숫자만큼 가져온다.
<br/>
<br/>

### removeAll()
```swift
prices.removeAll() { $0 > 2 } // prices is now [1.5]
prices.removeAll() // prices is now an empty array
```
* 만약 collection의 내용을 전부 지우고 싶다면 removeAll( ) 함수를 사용한다.
* 또한 클로저를 이용해서 지울 조건도 설정할 수 있다.
<br/>
<br/>
<br/>

## Lazy collections
* 만약 collection이 엄청 큰 경우 (심지어는 무한 정도?)에 collection에 접근하기를 원한다면, **lazy collection** 를 생각해보자.
```swift
func isPrime(_ number: Int) -> Bool {
  if number == 1 { return false }
  if number == 2 || number == 3 { return true }

  for i in 2...Int(Double(number).squareRoot()) {
    if number % i == 0 { return false }
  }

  return true
}

var primes: [Int] = []
var i = 1
while primes.count < 10 {
  if isPrime(i) {
    primes.append(i)
  }
  i += 1
}
primes.forEach { print($0) }
```
* 위의 isPrime 함수는 소수인지 아닌지를 체크한다. 1부터 시작해서 소수 배열인 primes의 개수가 10개일때까지 while문을 진행한다.
* 하지만 10개의 소수를 찾을때까지 while문을 실행하는 것은 효율적이지 못하다.
* 여기서 사용할 수 있는 방법이 **lazy**이다.
```swift
let primes = (1...).lazy
  .filter { isPrime($0) }
  .prefix(10)
primes.forEach { print($0) }
```
* 우선 1부터 Int형이 가질 수 있는 최대까지의 무한한 수를 가지고 시작한다.
* 그리고 나서, lazy를 사용해서, Swift에게 lazy collection을 원한다고 말해준다.
* 그리고 나서, filter를 가지고 isPrime() 이 true인것만 걸러낸다.
* 첫 10개의 소수를 얻기 위해서 prefix(10) 함수를 사용한다.
* 여기서 봐야할 점은, sequence는 처음 primes를 생성할 때 연산되지 않는다. forEach를 통해 primes에 접근했을 때 sequence가 계산되고, 첫 10개의 소수가 출력된다.
* lazy는 collection이 굉장히 큰 경우에 유용하게 사용될 수 있다. 필요할때를 제외하고는 연산이 되지 않기 때문이다.
