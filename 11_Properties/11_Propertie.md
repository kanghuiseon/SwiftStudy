# 11. Properties
```swift
struct Car {
  let make: String
  let color: String
}
```
위에서 보는 것과 같이 structure 내부의 값들을 **properties** 라고 부른다. 

Car에서의 두 개의 프로퍼티들은 **stored properties** 라고 하고, 이것은 Car의 각 instance(make, color)에 실제 값을 저장한다는 의미이다. 

stored properties 이외에도, **computed properties** 도 있는데, 이것은 실제로 그 값을 사용하려고 접근할때 계산된다. 그렇지 않으면 메모리에 할당조차 되지 않는다.



## Stored properties
Address book을 생성한다고 가정해보자. 필요한 정보는 아래와 같다.
```swift
struct Contact{
	var fullName: String
	var emailAddress: String
}
```
위에서 생성한 Contact structure는 반복적으로 사용할 수 있다. 그래서 contacts 배열을 하나 만들어, 내부에 각각 다른 정보의 Contact가 들어있게 할 수 있다.  

여기서 properties는 fullName과 emailAddress이다.

<img src=“https://github.com/kanghuiseon/SwiftStudy/blob/master/11_Properties/Resource/0.png” height=200>

각 properties는 타입은 각각 String 으로 지정되어 있지만, 디폴트 값은 설정되어있지 않다. 이런 경우에는 초기화 할 때 각 프로퍼티에 값을 할당한다.

```swift
var person = Contact(fullName: "Grace Murray", emailAddress: "Grace@navy.mil")

person.fullName // Grace Murray
person.emailAddress // grace@navy.mil
```
Swift에서는 structure에서 정의된 프로퍼티를 기준으로 자동으로 initializer를 제공한다.



각 프로퍼티는 dot notation으로 접근이 가능하다.
또한, dot notation을 이용해서, 값을 새롭게 정의할 수도 있다.
```swift
person.fullName = "Grace Hopper"
```
만약 누군가에 의해서 값이 변경되지 않기를 원한다면, property를 상수로 정의하면 된다.
```swift
struct Contact {
  var fullName: String
  let emailAddress: String
}

// Error: cannot assign to a constant
person.emailAddress = "grace@gmail.com
```
만약 이후에 새로 instance를 생성해서 emailAddress값을 새로 바꾸려고 한다면, 에러메세지를 출력할 것이다.
<br/>
<br/>

### Default values
만약 properties의 기본 값을 정해주고 싶다면,  relatinoship과 같이 값을 미리 할당해주면 된다.
```swift
struct Contact {
  var fullName: String
  let emailAddress: String
  var relationship = "Friend"
}
```
만약 이후에 어떤 Contact instance를 생성하면,  해당 contact의 관계는 자동으로 친구가 된다.

만약 친구가 아니라 가족이거나 회사 동료라면, 앞의 dot annotation을 이용해서 값을 변경해주기만 하면 된다.

Swift는 어떤 프로퍼티가 기본 값을 가지는지 인식하고, member-wise initializer를 통해 초기화할 때, 기본값을 가지는 프로퍼티의 경우에는 따로 지정해주지 않아도 된다.
```swift
var person = Contact(fullName: "Grace Murray",
                     emailAddress: "grace@navy.mil")
person.relationship // Friend
// 초기화할때 relationship 지정 안해도 됨.
var boss = Contact(fullName: "Ray Wenderlich",
                   emailAddress: "ray@raywenderlich.com",
                   relationship: "Boss")  
// 필요한 경우에만 지정                   
``` 
> member-wise initializer : parameter로 모든 속성을 초기화하는 방법을 말한다.  
<br/>
<br/>

## Computed properties
Computed properties는 필요한 계산을 수행한 후에 값을 리턴한다.

Stored properties는 constant나 variable로 선언을 할 수 있는 반면에, computed properties는 속성에 접근할때마다 값을 가지기 때문에 항상 var로 선언해야 한다.

컴파일러가 나중에 리턴 값으로 뭘 가져야 할 지 알아야 하기 때문에 Computed properties는 type을 무조건 가져야 한다.

<img src=“https://github.com/kanghuiseon/SwiftStudy/blob/master/11_Properties/Resource/1.png” height = 200>

TV는 computed property를 설명하는데 가장 좋은 예시이다.
실제로 TV산업에서 스크린 크기를 정의할 때 높이, 넓이가 아니라 대각선을 측정한다.
```swift
struct TV {
  var height: Double
  var width: Double
  
  // 1
  var diagonal: Int {
    // 2
    let result = (height * height +
      width * width).squareRoot().rounded()
    // 3
    return Int(result)
  }
}
```
순서대로 보자.!
1. 우선 diagonal property는 Int형을 사용한다. height과 width가 Double이어도 실제 광고에서는 49.52보다 50이 더 깔끔하기 때문이다. 
또한 operator = 으로 값을 할당하는 것이 아니라, 중괄호를 사용해서 computed property의 계산을 하도록 한다.
2. 대각선을 계산하기 위해서 피타고라스의 공식을 이용한다. 구한 값에서 rounded()을 추가하여 소수점을 반올림하도록 한다.
3. 마지막으로 계산된 값을 Int형으로 바꾼 후, 리턴한다.

* Computed properties는 실제로 어떠한 값도 저장하지 않는다. 따라서 메모리 공간 또한 가지지 않는다.
* Computed properties는 클래스, 구조체, 열거형에 추가할 수 있다.
* 선언 시점에 기본값이 저장되지 않는다.

실제로 사용을 해보면
```swift
var tv = TV(height: 53.93, width: 95.87)
tv.diagonal // 110
```
Stored property와 같이 접근하는 것이 가능하다.
<br/>
<br/>

### Getter and setter
이전까지 사용했던 computed property는 전부 read-only computed property 였다.
앞에서의 블록은 property의 값을 계산하기 위한 블록이며, 이것은 getter 라고도 불린다.

read-write computed property 로 생성하는 것도 가능하다.
이것은 setter 라고 한다.
Computed property가 값을 저장하기 위한 메모리 공간이 없기 때문에, setter는 보통 다른 stored properties의 값을 설정할 때 많이 쓰인다.
```swift
struct TV {
  var height: Double
  var width: Double
	var diagonal: Int {
  		// 1
  		get {
  	 		// 2
    		let result = (height * height +
      		width * width).squareRoot().rounded()
    		return Int(result)
  		}
  		set {
    	// 3
    		let ratioWidth = 16.0
    		let ratioHeight = 9.0
    		// 4
    		let ratioDiagonal = (ratioWidth * ratioWidth +
      	ratioHeight * ratioHeight).squareRoot()
    		height = Double(newValue) * 	ratioHeight / ratioDiagonal
    		width = height * ratioWidth / ratioHeight
  		}
	}
}
```
위에서부터 차례대로 보면,
1. 우선 diagonal에 getter 와 setter를 위한 get, set 블록을 생성한다. 
2. get블록은 위의 코드와 동일하게 구현한다.
3. Setter에서는 diagonal 속성으로 전달되는 값을 newValue라는 이름으로 사용한다. 
> newValue 상수는 해당 프로퍼티로 전달되는 값을 의미한다. (tv.diagonal = 120 에서 120이 newValue가 됨)  
4. Setter에서 newValue와 ratioWidth, ratioHeight의 값을 이용해서 기존의 height, width 값을 새로 설정할 수 있다.

setter에는 return이 없다. - 다른 stored properties를 설정하는 것만 가능
```swift
tv.diagonal = 70
tv.height // 34.32...
tv.width // 61.01...
```
tv.diagonal을 70으로 설정했더니, height의 값이 53.93에서 34.32로, width의 값이 95.87에서 61.01로 다시 바뀐 것을 알 수 있다.

* 만약 set을 따로 사용하지 않으면 해당 프로퍼티는 읽기 전용이 된다.
<br/>
<br/>

## Type properties
이전까지는 인스턴스마다의 프로퍼티 값이 다르게 설정이 될 수 있었다. 
하지만 type properties 는 인스턴스마다가 아니라 인스턴스 모두가 공유하는 하나의 프로퍼티를 말한다.

많은 레벨을 가진 게임을 생각해보자. 각 레벨은 몇개의 stored properties를 가진다. 
```swift
struct Level {
	static var highestLevel = 1
  let id: Int
  var boss: String
  var unlocked: Bool
}

let level1 = Level(id: 1, boss: "Chameleon", unlocked: true)
let level2 = Level(id: 2, boss: "Squid", unlocked: false)
let level3 = Level(id: 3, boss: "Chupacabra", unlocked: false)
let level4 = Level(id: 4, boss: "Yeti", unlocked: false)
```
여기서 highestLevel은 type property로 player들 각 레벨을 통과할때 게임의 진행사항을 저장하기 위한 property이다.
> type property는 가장 앞에 static을 붙여주어야 한다.   
> class의 경우에는 static 대신에 class 키워드를 붙여도 된다.  
highestLevel은 Level 자체의 속성이기 때문에 인스턴스로 접근하는 것이 아니라 타입으로 접근해야 한다.
```swift
// Error: you can’t access a type property on an instance
let highestLevel = level3.highestLevel

// Instead
Level.highestLevel // 1
```
> type properties는 기본적으로 지연 속성이기 때문에, property에 처음 접근하는 시점에 초기화된다. 위에서는 highestLevel에 접근할때 초기화됐다고 생각하면 된다.  
> 또한 type 자체에는 생성자가 없기 때문에 무조건 기본 값을 설정해주어야 한다.  
<br/>
<br/>


## Property observers
 위의 Level 구현에서, 플레이어가 새로운 레벨을 깰때마다 highestLevel을 자동으로 새로 설정하면 좋을 것 같다.
 
이때, 사용하는것이 property observers이다.

Property observers는 property값이 바뀌기 전과 후에 호출된다.

**willSet** observer는 프로퍼티에 값이 저장되기 전에 호출된다. 

**didSet** observer는 프로퍼티에 값이 저장된 후에 호출된다.

```swift
struct Level {
  static var highestLevel = 1
  let id: Int
  var boss: String
  var unlocked: Bool {
    didSet {
      if unlocked && id > Self.highestLevel {
        Self.highestLevel = id
      }
    }
  }
}
```
플레이어가 새로운 레벨을 통과할 때마다 highestLevel type property가 업데이트 되어야 한다.
여기서 봐야할 점은
* didSet observer에서 unlocked의 값에 접근할 수 있다. 
* highestLevel은 타입 프로퍼티이지만 타입 내부에 있기 때문에 Level.highestLevel 이 아니라 Self.highestLevel로 값에 접근한다. 이렇게 되면 type이름을 Level에서 GameLevel로 바꿔도 그대로 사용이 가능하게 된다.

willSet 과 didSet observer는 stored properties에서만 사용가능하다. 만약 computed property의 값의 변화를 알고 싶다면 setter를 추가하면 된다.

 맨 처음에 property를 초기화할 때에는 willSet과 didSet이 호출되지 않는다.
 
하지만 dot notation으로 새로운 값을 할당할 때 호출된다.

이 말의 의미는 property observers는 variable properties에서만 사용가능하다는 의미이다. constant는 초기화 이후에 값이 변경되지 않아서 감시가 필요하지 않다.
<br/>
<br/>

### Limiting a variable
variable의 값을 제한하는 경우에도 property observers를 사용할 수 있다.

필라멘트를 통과하는 최대 전류 제한을 가진 전구를 생각해보자.
```swift
struct LightBulb {
  static let maxCurrent = 40
  var current = 0 {
    didSet {
      if current > LightBulb.maxCurrent {
        print("""
              Current is too high,
              falling back to previous setting.
              """)
        current = oldValue
      }
    }
  }
}
```
만약 현재 전류가 최대 값을 초과하면 가장 최근에 성공한 값으로 값을 교체하도록 한다.

여기서는 didSet의 oldValue를 사용한다. didSet은 속성에 값이 저장된 후에 호출이되는데, 이 때, 이 전의 값이 파라미터로 전달이 된다. (만약 파라미터가 생략되면 oldValue로 사용)
```swift
var light = LightBulb()
light.current = 50
light.current // 0
light.current = 40
light.current // 40
```
만약 current값을 50으로 설정하면 최대 전류의 값을 초과하였기 때문에 current에는 이전값인 0이 저장된다.
> property observer가 되기 위해서는 willSet, didSet 둘 중 하나는 무조건 구현해야 한다.  

<br/>
<br/>

## Lazy properties
만약 실제로 프로퍼티가 필요할때까지 초기화되기를 원하지 않는다면 lazy stored property를 사용한다.

사용자의 프로필 사진을 다운로드 받거나, 굉장히 복잡한 계산을 요할때 유용하다.

다음의 Circle structure의 예시를 보자.
```swift
struct Circle {
  lazy var pi = {
    ((4.0 * atan(1.0 / 5.0)) - atan(1.0 / 239.0)) * 4.0
  }()
  var radius = 0.0
  var circumference: Double {
    mutating get {
      pi * radius * 2
    }
  }
  init(radius: Double) {
    self.radius = radius
  }
}

var circle = Circle(radius: 5) // got a circle, pi has not been run

circle.circumference // 31.42
// also, pi now has a value
```
pi를 직접 계산해본다고 하자. 

Circle의 인스턴스인 circle은 생성되었지만 lazy 프로퍼티인 pi는 아직 계산되지 않았다.

pi의 계산은 실제로 필요할 때까지 수행하지 않고, pi의 값이 필요한 circumference에 접근했을 때 비로소 계산이 수행된다.

여기서 주목해야할 점은 lazy에서 { }( )부분이다. 이 클로저 부분은 pi 값의 계산이 수행되는 시점에 호출이 된다. 그리고 내부에서 리턴되는 값이 pi의 값이 된다고 생각하면 된다.

pi는 lazy이기 때문에 이 클로저의 호출도 함께 지연된다.

circumference는 computed property이기 때문에 접근할때마다 계산이 된다. 하지만 lazy stored property인 lazy는 처음으로 접근될때만 계산되고 그 이후에는 메모리에 저장이 된다.

Lazy property는 무조건 variable이어야 한다. 그 이유는 lazy는  인스턴스 초기화 이후에 항상 초기화되기 때문에 let으로 선언하면 안된다.

> circumference getter는 무조건 **mutating** 으로 선언되어야 한다. structure의 값을 직접 바꾸는 것이기 때문이다.
> 
> pi도 structure의 stored property이기 때문에 radius만 사용할 수 있는 initializer를 만들어야 한다. (structure의 자동 초기화기는 모든 stored properties를 포함하기 때문에)
	
<br/>
<br/>
<br/>
<br/>

## Key points
* Properties는 variables 또는 constants이다.
* Stored properties는 값을 저장하기 위한 메모리를 할당한다.
* Computed properties 요청할 때마다 계산되고, 메모리에 할당되지 않는다.
* static 은 type property 를 의미한다. 이것은 모든 인스턴스들이 공통으로 사용할 수 있다.
* lazy는 stored property의 값이 처음으로 사용되기 전까지 계산되는 것을 방지한다. 











