# 11. Properties
```swift
struct Car {
  let make: String
  let color: String
}
```
위에서 보는 것과 같이 structure 내부의 값들을 properties 라고 부른다. 
Car에서의 두 개의 프로퍼티들은 stored properties 라고 하고, 이것은 Car의 각 instance(make, color)에 실제 값을 저장한다는 의미이다. 

stored properties 이외에도, computed properties 도 있는데, 이것은 실제로 그 값을 사용하려고 접근할때 계산된다. 그렇지 않으면 메모리에 할당조차 되지 않는다.



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

<img src="https://github.com/kanghuiseon/SwiftStudy/blob/master/11_Properties/Resource/0.png0" height="200">

각 properties는 타입은 각각 String 으로 지정되어 있지만, 디폴트 값은 설정되어있지 않다. 이런 경우에는 초기화 할 때 각 프로퍼티에 값을 할당한다.

