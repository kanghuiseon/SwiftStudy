# 02. Optional
> Optional을 배우기 전에는 무조건 상수, 변수를 초기화했어야 했다.
> 하지만 값이 없는 경우에는 어떻게 해야 할까? 이럴때 사용하는게 Optional!
<br/>
<br/>

```swift
let bookNumber: Int
print(bookNumber)
```
* 위의 코드는 에러를 발생시킨다. 왜냐하면 book가 초기화 되지않은 상태에서 접근을 했기 때문!
* 이때 책을 한 권도 가지고 있지 않는 경우도 표현을 하고 싶다면, 아래와 같이 Int뒤에 ?를 붙여서 옵셔널 Int로 타입을 지정해준다.
```swift
let bookNumber: Int? = nil
print(bookNumber)
// print -> nil
```
<br/>
<br/>

* 만약 상수나 변수를 nil로 초기화하고 싶다면, 1번이 아니라, 2번처럼 **타입을 명시**해주어야 한다.
```swift
//1
let bookNumber = nil
//2
let bookNumber: Int? = nil
```
<br/>
<br/>

* 위의 옵셔널 Int 타입의 상수 bookNumber를 또 다른 상수인 bookNumber2에 할당해보자.
* 여기서 bookNumber2는 bookNumber와 마찬가지로 옵셔널 Int 타입이다. 
* 또한 bookNumber2를 출력해보면 Optional(12) 의 값을 얻게 되는데, Int값을 Optional로 감쌌다고 생각하면 된다.(wrapping)
```swfit
var bookNumber2 = bookNumber
bookNumber2 = 12
print(bookNumber2)
```
<br/>
<br/>

* 만약 Optional(12)가 아니라, 그 안의 값을 가지고 싶다면, Optional Binding을 통하거나, 강제 언래핑을 해주면 된다. 강제 언래핑은 !를 변수 뒤에 붙여주기만 하면 된다. 하지만 강제 언래핑은 해당 상수나 변수가 nil 인 경우에는 에러를 발생시키기 때문에 사용하지 않는 것이 좋다.
```swift
print(bookNumber2!) // 12 출력
```
<br/>
<br/>
<br/>
<br/>

## Optional Binding
* 위에서 말했듯이, 강제 언래핑은 좋지 않다. 상수나 변수가 nil인 경우에는 에러를 발생시키기 때문이다.
* 강제 언래핑 대신에, Optional Binding을 사용하자.
* 옵셔널 바인딩이란, 강제 언래핑 !을 사용하지 않고, 해당 값이 nil인지 아닌지를 판단하여 안전하게 언래핑하는 방식이다.
* 아래의 코드 중 상황에 맞게 사용하면 되는데, 잠깐 보자면, 1번과 2번의 경우에는 만약 optionalValue가 nil이 아니면, 언래핑하여서, valueName에 저장한다. 그리고나서 valueName을 { } 내부에서 사용한다.
* 2번의 경우에는, 만약 optionalValue가 nil이 아니면, valueName에 언래핑된 값이 저장되고 그 다음줄부터 실행이 된다. nil이면, else 문이 실행된다.
* 아래의 세가지 방법을 이용해서, 강제 언래핑으로 인한 에러를 막을 수 있다.
* let 이 아니라 var로도 사용 가능!
* 4번에서, if let 구문에서는 변수를 나열할 수도 있고, 조건을 작성해도 된다.
```swift
// 1
if let valueName: Type = optionalValue{
    ...
}

// 2
guard let valueName: Type = optionalValue else { ... }

// 3
while let valueName: Type = optionalValue{
    ...
}

// 4
let one: Int? = 1
let two: Int? = 2
if let num1 = one, let num2 = two, num1 < num2 {

}
```
<br/>
<br/>
<br/>

## nil 병합 연산자
* 만약 사용하고자 하는 값이 nil인 경우에, nil을 그대로 반환하지 않고 기본값을 반환하고 싶으면
* ?? 를 사용한다. 
* 만약 ?? 왼쪽의 값이 nil이라면 오른쪽의 값으로 설정을 하고, nil이 아니라면, 언래핑을 하여서, b에 저장한다.
```swift
var a: Int?
var b = a ?? 3
```
<br/>
<br/>
<br/>

## Optional Chaining
* 옵셔널을 여러개 연결한 것을 옵셔널 체이닝이라고 한다.
* 아래의 예시에서, 여러개의 옵셔널이 . 으로 연결이 되어있다. 이 중에서 하나라도 nil을 반환하면 연결된 전체를 nil로 본다.
* 옵셔널 체이닝에서, 가장 먼저 나오는 값 (아래에서는 residence or address)이 옵셔널이면, 연결된 어떤 값이 옵셔널이 아니더라고 같이 연결되어있기 때문에 옵셔널 값이 된다.
* 옵셔널 체이닝을 이용하면 무조건 옵셔널을 반환한다.
* 옵셔널 체이닝의 마지막 값이 옵셔널이더라도, ?를 붙여주지 않는다.
```swift
if let johnsStreet = john.residence?.address?.street {
    print("John's street name is \(johnsStreet).")
} else {
    print("Unable to retrieve the address.")
}
// Prints "Unable to retrieve the address."
```
<br/>
<br/>
<br/>

### 메소드 옵셔널
* 1 : 만약 옵셔널을 리턴하는 함수의 경우, 아래의 코드에서 buildingIdentifier( )?와 같이, 괄호 뒤에 ?를 붙여준다.
* 2 : 하지만 함수 자체가 옵셔널인 경우도 있는데, 이 때에는 괄호 뒤가 아니라 앞에 ?를 붙여주어야 한다.f는 함수 자체가 옵셔널이기 때문에, f바로 뒤에도 ?를 붙여주고, 옵셔널을 리턴하기 때문에, ()뒤에도 ?를 붙여주어야 한다.

```swift
// 1
if let beginsWithThe = john.residence?.address?.buildingIdentifier()?.hasPrefix("The") {

}

//2
let f: (() -> String?)? = address?.buildingIdentifier
f?()?
```
