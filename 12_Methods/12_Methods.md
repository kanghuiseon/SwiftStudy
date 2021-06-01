# 12. Methods
> Methods는 structure, class, enum 내부에 추가되는 함수이다.  
> 기존의 함수와 다른 점은 instance를 통해서만 접근이 가능하다는 것이다.  

## Method refresher
Array.removeLast()  는 배열 인스턴스의 마지막 item을 삭제하는 method이다.
```swift
var numbers = [1, 2, 3]
numbers.removeLast()
numbers // [1, 2]
```
<img src=“https://github.com/kanghuiseon/SwiftStudy/blob/master/12_Methods/Resource/0.png” height=250>

removeLast()와 같은 Methods는 structure의 data를 다룰 때 사용된다.
<br/>
<br/>

### Comparing methods to computed properties
앞에서 본 computed properties의 구현을 봤을 때, 메소드와 구현이 비슷한 것을 볼 수 있다. (계산을 한다는 면에서?)

그렇다면 이 둘의 차이점은 무엇일까?

프로퍼티는 기본적으로 값을 저장한다. 반면에 메소드는 어떠한 일을 수행한다.
<img src=“https://github.com/kanghuiseon/SwiftStudy/blob/master/12_Methods/Resource/1.png” height = 230>

둘 중 하나를 선택할 때, 값을 얻는 것 뿐만 아니라 값을 새로 설정하기를 원하지는 않는지를 생각해보자.

만약 메소드로 구현한다고 하면, 외부에서 값을 얻고 설정하기 위한 메소드를  두 개 만들어야한다. 이는 가독성이 떨어질 수 있기 때문에 이런 경우에는 **computed property의 setter** 를 이용한다.

또한,  굉장히 많은 계산을 요구하거나, 어떠한 계산을 위해 데이터베이스에 접근하려고 하는지를 생각해보자.

  *이 경우에는 메소드가 적절하다. 메소드는 미래의 개발자들에게 해당 호출이 오래걸리고 많은 자원을 요구한다는것을 알게 하기 때문이다.*

만약 호출하는데 시간이 오래걸리지 않는다면 (O(1) 같은) computed property를 사용하자.
<br/>
<br/>

### Turning a function into a method
이미 Apple의 Foundation 프레임워크에는 굉장히 잘 만든 Date 클래스가 존재한다. 하지만 메소드를 공부하기 위해서 SimpleDate라는 이름의 model을 생성해보자. 

아래의 코드에서, monthsUntilWinterBreak(date:)를 method로 어떻게 바꿀수 있을까?
```swift
let months = ["January", "February", "March",
              "April", "May", "June",
              "July", "August", "September",
              "October", "November", "December"]

struct SimpleDate {
  var month: String
}

func monthsUntilWinterBreak(from date: SimpleDate) -> Int {
  months.firstIndex(of: "December")! -
  months.firstIndex(of: date.month)!
}
```
우선, method로 만들기 위해서 monthsUntilWinterBreak(date:)를 SimpleDate structure내부에 추가를 한다.
```swift
struct SimpleDate {
  var month: String
  
  func monthsUntilWinterBreak(from date: SimpleDate) -> Int {
    months.firstIndex(of: "December")! -
    months.firstIndex(of: date.month)!
  }
}
```
메소드로 만들기 위해서 따로 추가해야할 것은 없다. 단지 달라진 점은 바로 호출할 수는 없고 dot syntax를 이용해서 인스턴스로 접근을 해야한다는 것이다.
```swift
let date = SimpleDate(month: "October")
date.monthsUntilWinterBreak(from: date) //2
```
프로퍼티와 같이, 메소드 이름을 타이핑하면 자동으로 suggestions를 제공한다.
<img src=“https://github.com/kanghuiseon/SwiftStudy/blob/master/12_Methods/Resource/2.png” height = 200>

가만히 코드를 보니, 좀 이상한 점이 있다. 자기 자신을 파라미터로 넘겨주는 것이다. 
```swift
date.monthsUntilWinterBreak() // Error!
```
<br/>
<br/>


## Introducing self
우리는 앞 챕터에서 struct내부에서 static properties에 접근하기 위해 Self (S가 대문자여야 함)를 사용한 것을 본 적이 있다. 

이번 챕터에서는 self (소문자 s)를 생각해보려고 한다.
structure의 이름의 첫 글자는 대문자여야 한다. 반면에 instance 이름의 첫 글자는 소문자여야 한다.

instance의 값에 접근하기 위해서 structure 내부에서 **self**를 사용한다.

Swift 컴파일러는 *secret parameter* 로 self를 메소드에 전달한다.
따라서, 위의 잘못된 코드는 아래와 같이 바뀐다.
```swift
// 1
func monthsUntilWinterBreak() -> Int {
  // 2
  months.firstIndex(of: "December")! -
    months.firstIndex(of: self.month)!
}
```
1. method에는 자기 자신을 파라미터로 받는 부분이 사라졌다.
2. 구현할 때, self가 이전의 date를 대신했다.
```swift
date.monthsUntilWinterBreak() // 2
```
이제는 더 이상 자기 자신을 파라미터로 넘겨주지 않아도 된다.!

여기서 추가로, self를 없애는 것도 가능하다. 

self는 instance에 대한 참조로 사용된다. 하지만 Swift 는 self를 사용하지 않아도 충분히 문법을 이해하기 때문에 self를 사용하지 않고도 변수를 사용할 수 있다.

많은 프로그래머들은 self를 local variable과 property가 이름이 같은 경우에 주로 사용한다.
<br/>
<br/>

## Introducing initializers
initializers는 새로운 인스턴스를 생성하기 위해서 호출하는 특별한 메소드이다. 
func 키워드를 생략하고, 심지어 이름까지 생략한다. 대신, init을 사용하고  파라미터를 가질 수 있다. (파라미터는 없어도 됨)

위에서 만든 SimpleDate structure의 instance를 생성해보자.
```swift
let date = SimpleDate(month: "October")
```
실제로 instance를 생성할때, month property의 값을 초기화해주어야 한다.

하지만 구현을 할 때, 파라미터가 없는 것이 좀 더 효율적이라고 생각한다.
```swift
let date = SimpleDate() // error
```
하지만 아래와 같이 파라미터 없이 instance를 생성하면 에러가 발생한다.

원하는 대로 하기 위해서, 우리는 init을 구현하고, 빈 파라미터로 인스턴스를 생성하면, 바로 month에 기본값이 할당되도록 해본다.
```swift
struct SimpleDate {
  var month: String
  
  init() {
    month = "January"
  }
  
  func monthsUntilWinterBreak() -> Int {
    months.firstIndex(of: "December")! -
      months.firstIndex(of: month)!
  }
}
```
코드를 자세히 보자.
1. init() 에는 func 키워드도 없고 이름도 없다. initializer를 호출하기 위해서는 타입의 이름을 사용하기만 하면 된다. (let date = SimpleDate() ) 
2. 함수 같이, initializer는 파라미터 리스트()를 가져야 한다. (파라미터가 없어도)
3. initializer에서, structure의 모든 stored properties에 값을 할당해야 한다.
4. initializer는 절대로 값을 리턴하면 안된다. (initializer의 역할은 새로운 인스턴스를 초기화하는 것이기 때문에)

```swift
let date = SimpleDate()
date.month // January
date.monthsUntilWinterBreak() // 11
```
실제로 새로 인스턴스를 생성하고 month의 값을 출력해보면 January라는 기본값이 할당된 것을 알 수 있다.

초기화를 할 때, month의 값에 현재 날짜를 기반으로 기본 값을 설정하면 좋을 것 같다!
<br/>
<br/>

### Initializers in structures
SimpleDate에 day 프로퍼티를 추가해보자.
```swift
struct SimpleDate {
  var month: String
  var day: Int
  
  init() {
    month = "January"
    day = 1
  }
  
  func monthsUntilWinterBreak() -> Int {
    months.firstIndex(of: "December")! -
    months.firstIndex(of: month)!
  }
}
```
initializers가 모든 stored property를 초기화해야 하기 때문에, init()에서 day를 설정해야 한다.
만약 day에 값을 설정하지 않으면, 컴파일러는 에러를 표출할 것이다.
<br/>

또한, custom initializer를 생성했으니, 기존에 자동으로 생성되던 memberwise initializer는 사용하지 않는다.
```swift
let valentinesDay = SimpleDate(month: "February", day: 14) // Error!
```

대신, 파라미터를 받는 initializer를 정의해야 한다. (아래의 코드를 init() 바로 밑에다가 추가한다.)
```swift
init(month: String, day: Int) {
  self.month = month
  self.day = day
}
```
여기에서 봐야할 점은 self이다. 현재 프로퍼티 파라미터의 이름이 같기 때문에 프로퍼티를 나타내기 위해 self를 사용해서 컴파일러에게 local parameter가 아니라 property를 참조한 것이라고 알려준다.
(init()에서는 안해줘도 됨)

```swift
let valentinesDay = SimpleDate(month: "February", day: 14)
valentinesDay.month // February
valentinesDay.day // 14
```
새로운 initializer를 만들었기 때문에 위의 코드처럼 사용할 수 있게 된다.
<br/>
<br/>

### Default values and initializers
argument initializer를 만들지 않는 방법이 있다.

파라미터에 대한 기본값을 설정하면 automatic member wise initializer가 그것을 사용한다.

위의 structure에서 두 개의 initializers를 지우고 month 와 day에 기본값을 추가해보자.
```swift
struct SimpleDate {
  // 1
  var month = "January"
  var day = 1
  
  //2
  
  func monthsUntilWinterBreak() -> Int {
    months.firstIndex(of: "December")! -
    months.firstIndex(of: month)!
  }
}
```
코드를 자세히 보자.
1. 두 개의 프로퍼티들이 각각 January와 1이라는 기본 값을 가진다.
2. 두 개의 initializers가 사라졌다.
<img src=“https://github.com/kanghuiseon/SwiftStudy/blob/master/12_Methods/Resource/3.png” height =200>

비록 initializer가 사라졌지만 여전히 initializer style을 사용할 수 있다.
```swift
let newYearsDay = SimpleDate()
newYearsDay.month // January
newYearsDay.day // 1

let valentinesDay = SimpleDate(month: "February", day: 14)
valentinesDay.month // February
valentinesDay.day // 14
```
Automatic memberwise initializer가 init(month:day)를 제공하기 때문에 custom initializer를 만들지 않아도 된다.

하지만 init()은 어떻게 사용할 수 있을까?

이미 각 프로퍼티들에 기본 값이 할당되었기 때문에 initializer를 따로 생성하지 않아도 된다. 

이런 이유로 다시 설정하고 싶은 프로퍼티만 전달하게도 할 수 있다.
```swift
let octoberFirst = SimpleDate(month: "October")
octoberFirst.month // October
octoberFirst.day // 1

let januaryTwentySecond = SimpleDate(day: 22)
januaryTwentySecond.month // January
januaryTwentySecond.day // 22
```
위의 코드를 보면 month만 전달해도 되고 day만 전달해도 된다.
<br/>

## Introducing mutating methods
structure에서 메소드는 **mutating**을 명시하지 않으면 instance의 값을 바꿀 수 없다.
```swift
mutating func advance() {
  day += 1
}
```
mutating 키워드는 메소드가 structure의 값을 바꿀 수 있도록 한다.
structure는 value type이기 때문에 복사되서 사용된다.

만약 메소드가 어떤 프로퍼티의 값을 변경하려고 한다면, 원래의 instance와 copied instance는 더 이상 같지 않게 된다.

mutating을 추가하게 되면, instance를 let으로 선언하면 안된다. 만약 그렇게 하면 컴파일러는 에러를 나타낼 것이다. 

Mutating methods에서 secret self 값은 inout parameter처럼 사용된다. 즉, mutating method내부에서 값을 변경하면 type내부의 값에 영향을 끼칠 수 있다는 것이다.

> 여기서 inout 파라미터를 보자. 실제로 파라미터는 상수 값이다. 하지만 inout표시를 해주면 변수로 바뀌어서 값을 변경할 수가 있다.  
> ```swift  
> func f(_ x: inout Int){  
> 	x = 10  
> }  
> var a = 1
> f(&a)
> print(a) // 10
> ```  
<br/>
<br/>

## Type methods
Type properties처럼 **type methods** 를 사용할 수 있다. 타입 메소드는 모든 인스턴스들이 접근할 수 있으며, 타입 자체로 접근해야 한다. 이것도 **static** 을 붙여준다.
<br/>

Type methods는 특정 인스턴스가 아니라 type 자체에 대한 함수를 생성할때 유용하게 사용이 된다.
 
구조체에 타입 메소드를 추가해보자.
```swift
struct Math {
  // 1
  static func factorial(of number: Int) -> Int {
    // 2
    (1...number).reduce(1, *)
  }
}
// 3
Math.factorial(of: 6) // 720
```
팩토리얼같은 custom한 계산을 할 수가 있는데, 각 인스턴스들이 따로 가질 수 있는 함수를 생성하는 것이 아니라, 구조체 내부에서 관련 있는 함수들을 함께  type methods로 모아 놓을 수도 있다.

이 구조체는 **namespace** 와 같은 역할을 한다.
> namespace : 관련되어 있는 것들을 모아 놓은 공간  

코드를 자세히 보자.
1. static으로 선언해서 타입 메소드라고 명시했다. 
2. 고차 함수인 reduce를 사용해서 구현했다. for문을 사용해서 팩토리얼을 계산할 수도 있지만 고차함수를 이용해서 좀 더 깔끔하게 코드를 짰다.
3. 타입 메소드를 호출할 때, Math. 으로 호출했다.
<img src = “https://github.com/kanghuiseon/SwiftStudy/blob/master/12_Methods/Resource/4.png” height="200">
<br/>
<br/>

## Adding to an existing structure with extensions
구조체에 기능을 더 추가하고 싶은데, 더 추가했다가는 구조체가 지저분해질 것 같다. 그리고 소스 코드에 접근을 하지 못해서 기능을 추가할 수 없는 경우도 있다. 
<br/>

**extension**을 이용하면 소스코드를 가지고 있지 않아도 해당 구조체를 열어서 메소드나 initializers, Computed properties를 추가하는 것이 가능하게 된다.
(Chapter 18, “Access Control and Code Organization”에서 더 자세하게 다룰 예정이다.)

아래의 코드는 extension을 이용해서 원래의 Math 구조체가 아니라 외부에서 primeFactors(of:) 타입 메소드를 추가하였다.
```swift
extension Math {
  static func primeFactors(of value: Int) -> [Int] {
    // 1
    var remainingValue = value
    // 2
    var testFactor = 2
    var primes: [Int] = []
    // 3
    while testFactor * testFactor <= remainingValue {
      if remainingValue % testFactor == 0 {
        primes.append(testFactor)
        remainingValue /= testFactor
      }
      else {
        testFactor += 1
      }
    }
    if remainingValue > 1 {
      primes.append(remainingValue)
    }
    return primes
  }
}
```
이 메소드는 value값을 이용해서 소인수를 찾는다.
예를 들어, 81이면 [3, 3, 3, 3]을 리턴한다.
1. value는 mutable variable인 remainingValue에 할당되어서 계산할때 값을 변경할 수 있다.
2. testFactor는 2로 시작해서 remainingValue에 나눠진다.
3. remainingValue가 testFactor*testFactor 보다 작아질때까지 loop를 진행한다.
<br/>

### Keeping the compiler-generated initializer using extensions
```swift
let months = ["January", "February", "March",
              "April", "May", "June",
              "July", "August", "September",
              "October", "November", "December"]

struct SimpleDate {
    var month: String
    var day:Int
  
  func monthsUntilWinterBreak() -> Int {
    months.firstIndex(of: "December")! -
    months.firstIndex(of: month)!
  }
  
  mutating func advance() {
    day += 1
  }
}

extension SimpleDate {
    init(){
        month = "January"
        day = 1
    }
}
```
SimpleDate 구조체에서, init()을 추가했더니, compiler-generated memberwise initializer는 없어진 것을 알 수 있었다.

만약 extension을 이용해서 SimpleDate에 init()을 추가한다면 둘 다 유지할 수 있다.

<img src=“https://github.com/kanghuiseon/SwiftStudy/blob/master/12_Methods/Resource/5.png” height=250>

<br/>

- - - -
## Key points
* Methods는 type과 관련된 함수이다.
* Methods는 타입의 기능을 정의한다.
* method는 self를 이용해서 instance의 데이터에 접근할 수 있다.
* **Initializers** 는 타입의 새로운 instance를 생성한다. 
* **type methods** 는 instance가 공동으로 사용할 수 있는 메소드이다.
* extension을 이용해서 기존의 구조체를 열어서 메소드, initializer, computed properties를 추가할 수 있다.
* extension으로 custom initializer을 추가하면 member-wise initializer가 사라지지 않고 그대로 사용할 수 있다.
* Methods는 이름이 있는 타입에서 존재할 수 있다. - structures, classes, enumerations.

