# 01. Closure
> Closure란? 코드 블록!
<br/>

## 클로저 표현 (Closure Expressions)
- 클로저는 기존의 우리가 알고 있는 함수의 형태와, 좀 더 축약된 문법으로 사용되는 형태가 있다.
- 우리가 밑에서 배울 클로저는 후자에 속하며, Swift에서는 최적화를 통해, 굉장히 간결하게 클로저를 사용할 수 있도록 한다.
```swift
// 1. 
{ (parameters) -> Return Type in
    statements
}

// 2.
let closure = { (parameters) -> Return Type in
    statements
}
closure()

//3. 
func closureFunction(closure: (parameters) -> return type){
    closure()
}

closureFunction(closure: { (parameters) -> return type in
    statements
})
```
* 1. 클로저는 기본적으로 파라미터, 리턴 타입, in 키워드, 코드부분의 형태를 가진다. 
* 2. 이 클로저를 변수에 저장하여, 실행도 할 수 있다.
* 3. 클로저는 함수의 파라미터로도 전달이 가능하다. 여기서 클로저는 실제 함수를 호출할때, 실행된다.
<br/>

예시를 가지고 클로저를 사용해보자.!
```swift
let names = ["kangheeseon", "choihonggyu", "kimdoeun", "limsungjun", "kimdomin", "baeksooyoung", "wonsanghyuck"]
let sortedNames = names.sorted(by: { (name1: String, name2: String) -> Bool in
    return name1 < name2
})
print(sortedNames)

// print -> 
// ["baeksooyoung", "choihonggyu", "kangheeseon", "kimdoeun", "kimdomin", "limsungjun", "wonsanghyuck"]
```
* sorted메소드는 클로저를 파라미터로 받아서, 배열의 값들을 정렬한다.
* String 타입의 이름 두 개를 파라미터로 받고, Bool 타입의 리턴 형태를 지정한다.
* sortedNames에는 names를 알파벳순으로 정렬한 값이 들어가는 것을 확인할 수 있다.
<br/>
<br/>

## 타입 추론 (Inferring Type)
* 위에서 사용한 sorted는 Swift framework에 저장이 되어있다. 따라서, 컴파일러는 해당 프레임워크를 통해 파라미터와 리턴 타입을 추론할 수 있다. 
* 컴파일러가 추론을 할 수 있기 때문에, 우리는 코드를 작성할때 해당 부분을 생략해도 된다.
* 위의 예시를 가지고 생략을 해보자!
```swift
// 생략된 최종 버전
let names = ["kangheeseon", "choihonggyu", "kimdoeun", "limsungjun", "kimdomin", "baeksooyoung", "wonsanghyuck"]
let sortedNames = names.sorted { $0 < $1 }
print(sortedNames)

// print -> 
// ["baeksooyoung", "choihonggyu", "kangheeseon", "kimdoeun", "kimdomin", "limsungjun", "wonsanghyuck"]
```
* 최종버전을 살펴보면 다음의 경우가 생략된 것을 볼 수 있다.
1. 파라미터 이름, 파라미터 타입
2. 리턴 타입
3. (by: )
4. in 키워드, return 키워드
* 파라미터와 리턴 타입은 컴파일러가 추론할 수 있기 때문에 생략을 해도 된다. 
* 또한 Swift는 **Shorthand Arguments Names**를 제공하여, 인자 이름을 축약해서 나타낼 수 있다. ($0, $1, $2, ...)
* 파라미터와 리턴 타입을 생략했으므로, in 키워드도 생략할 수 있다.
* 만약 클로저가 마지막 파라미터로 들어온다면, trailing closure로 작성을 하여서, ( ) 또한 없애도 된다.
<br/>

위의 버전을 더 축약할 수도 있다!!!!
```swift
// 생략된 최종 버전
let names = ["kangheeseon", "choihonggyu", "kimdoeun", "limsungjun", "kimdomin", "baeksooyoung", "wonsanghyuck"]
let sortedNames = names.sorted(by: <)
print(sortedNames)

// print -> 
// ["baeksooyoung", "choihonggyu", "kangheeseon", "kimdoeun", "kimdomin", "limsungjun", "wonsanghyuck"]
```
* Swift에서는 String타입 연산자로, String끼리 비교할 수 있는 비교 연산자를 이미 구현을 해뒀다. 그래서 < 라고만 써도 된다!
<br/>
<br/>

## 후위 클로저 (Trailing Closures)
* 위에서 잠깐 설명했듯이, 만약 함수의 마지막 파라미터로 클로저를 받는다면, 후위 클로저로 작성할 수 있다.
```swift
func functionWithClosure(closure: () -> Void){
    closure()
}

functionWithClosure() {
    print("Hello, World!")
}

// print->
// Hello, World!
```
* 만약 클로저외에 다른 파라미터를 받지 않는다면, ( ) 도 생략 가능하다.
<br/>
<br/>

## 값 캡쳐 (Capturing Values)
* 클로저는 값을 캡쳐할 수 있다. 무슨 의미냐면 어떠한 값을 클로저가 사용할때, 해당 값이 사라져도 클로저 내부에서는 여전히 사용할 수 있다는 말!
* 값 캡쳐에는 두 가지 종류가 있는데, 1. 값 캡쳐, 2. 참조 캡쳐가 있다. Swift는 두번째 방식을 사용하며, 첫번째는 Object-C에서 사용한다.
* 1번은 원본값의 복사본을 사용해서, 값을 변경해도 원본값의 값은 변하지 않는다. 하지만, 2번은 참조를 캡쳐하는 것이기 때문에, 값을 변경하면, 원본값도 바뀐다. (해당 변수나, 상수의 주소를 캡쳐해서, 해당 주소의 값을 변경한다고 생각하면 될듯?)
* 예를 보자!
```swift
// 1
func makeIncrementer(forIncrement amount: Int) -> () -> Int {
    var runningTotal = 0
    func increment() -> Int {
        runningTotal += amount
        return runningTotal
    }
    return increment
}

// 2
let incrementByTen = makeIncrementer(forIncrement: 10)
incrementByTen()
incrementByTen()
incrementByTen()

// 최종적으로 30 반환
```
1.
* 위의 함수는 함수 내부에서 함수를 호출하는 중첩 함수의 형태이다.
* 파라미터 타입은 Int이고, 리턴 타입은 ( ) ->  Int이다.
* 클로저 내부에서 외부에 있는 값에 접근을 하면 값을 캡쳐하기 때문에, 내부 함수인 increment에서 runningTotal, amount가 선언되어있지 않지만 사용할 수 있다.
* 
2.
* makeIncrementer의 리턴 값을 저장하는 InrementByTen 상수를 생성한다.
* 저장되어있는 클로저를 여러 번 실행해보면 누적된 값인 30을 반환하는 것을 알 수 있다.
* 그 이유는 클로저 내에서는 runningTotal 과 amount의 값을 캡쳐해서 사용하기 때문에, 외부 함수의 실행이 끝나도, 해당 변수들은 메모리에서 사라지지 않고, 그대로 있는다.
* 따라서 다음의 실행되는 클로저들도 해당 위치의 값을 사용하기 때문에 누적된 값이 나오는 것이다.
<br/>
<br/>

## 이스케이핑 클로저 (Escaping Closures)
* 만약 함수가 끝이 나도 여전히 클로저를 실행하고 싶다면, @escaping 키워드를 붙인다.
```swift
func escapingClosure(closure: @escaping ()->()){
    DispatchQueue.main.asyncAfter(deadline: .now() + 5) {
        closure()
    }
    print("end")
}

escapingClosure{
    print("closure!")
}

// print ->
// end
// 5초후
// closure!
```
* escapingClosure내부의 dispatchqueue부분은 함수가 끝나고 5초후에 파라미터로 전달된 내용이 실행된다.
* @escaping으로 선언된 클로저는 실제로 클로저가 실행되고 끝나기 전까지는 외부 함수가 끝이나도 사라지지 않는다. 
* 그래서 함수가 끝이나도 사용될 수 있는 것이다.
<br/>
<br/>

## 자동 클로저 (Autoclosures)
```swift
var customersInLine = ["Chris", "Alex", "Ewa", "Barry", "Daniella"]
func serve(customer: customerProvider: @autoclosure () -> String){
    print("Now serving \(customerProvider())!")
}

serve(customer: customersInLine.remove(at: 0))

// print->
// Now serving Chris!
```
* autoclosure 키워드를 입력하면, 파라미터 값을 넘겨줄때, 클로저를 바로 넘겨주면 안된다.
* 클로저 형태( { } )를 뺀 나머지 부분만 넣어준다. 그 이유는 autoclosure로 설정했기때문에 자동으로 클로저 형태로 wrapping되어서 전달되기 때문이다.
* 자동 클로저를 너무 많이 사용하면, 코드가 어려워질 수 있어서 남용하면 안된다.!
<br/>
<br/>
<br/>
<br/>
<br/>
<br/>

[출처 : Swift 공식 문서](https://jusung.gitbook.io/the-swift-language-guide/language-guide/07-closures)
