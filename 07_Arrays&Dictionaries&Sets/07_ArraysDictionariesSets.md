# 07. Arrays & Dictionaries & Sets
> collections는 유동적인 **"containers"** 로, 어떤 값들을 저장한다.
<br/>
<br/>
<br/>

## Mutable versus immutable collections
* collection을 만들 때, constant or variable로 선언을 해야 한다.
* 만약 collection의 내용이 이후에 바뀌지 않는다면, 선언은 let을 이용해서 상수로 선언한다. **(immutable)**
* 반대로, 이후에 값을 더 추가하거나 삭제할 경우가 있다면, var을 이용해서 변수로 선언한다. **(Mutable)**
<br/>
<br/>

## Arrays
* Arrays는 가장 흔한 collection type으로, 여러 개의 값을 가지는 list의 형태를 띄고 있다. 
<br/>
<br/>
<br/>

## What is an array?
* array는 순서가 있는 collection으로, array의 요소는**zero-indexed** 이다. index가 0부터 시작하며, 1씩 커진다.
* 따라서, array의 마지막 원소의 인덱스는 array size에 1을 뺀 값이다.
<img src= "https://github.com/kanghuiseon/SwiftStudy/blob/master/07_Arrays%26Dictionaries%26Sets/Resource/0.png" height="200">

* 사진에서보면, 5개의 원소가 있고, 인덱스는 0-4로 이루어져 있다.
* 내부 값의 타입은 String이며, String이 아닌 타입은 추가할 수 없다.
* 또한 같은 값이 여러 개 들어갈 수도 있다.
<br/>
<br/>

## When are arrays useful?
* Arrays는 특정 순서로 요소들을 저장하고 싶을 때 사용하면 좋다.
* 요소를 정렬하고 싶거나, 전체 배열을 iterating없이 index로 접근하고 싶을 때도 사용하면 좋다.
* 예를 들어서, 점수 데이터를 저장하려고 할 때, 순서가 중요할 수 있다. 점수가 가장 높은 순서대로 저장하고 싶을 때 Arrays를 사용한다.
<br/>
<br/>

## Creating arrays
* array를 생성하는 가장 쉬운 방법은 **array literal**을 사용하는 것이다.
* array를 초기화 할 때, 가장 기본적으로는 배열 값을 지정하는 방식을 사용한다. 원하는 값을 대괄호로 감싸고 내부 값들은 콤마로 구분한다.
```swift
let evenNumbers = [2, 4, 6, 8]
```
* 위의 evenNumbers배열은 integers값만 가지기 때문에 다른 타입의 값들은 포함될 수 없다. 
* 위의 evenNumbers배열의 타입은 [Int]이다.
* 대괄호 내부의 타입은 배열 값의 타입을 의미하며, 해당 타입의 값만 넣을 수 있도록 한다.
<br/>
<br/>

```swift
var subscribers: [String] = []
```
* 배열을 초기화하는 몇가지 방법 중에서, 첫 시작을 빈 배열로 시작하고 싶을 때 사용하는 방법이다.
* 만약 빈 배열  [ ] 로 초기화 하고 싶다면, 컴파일러는 해당 배열의 타입을 추론할 수 없기 때문에 꼭 명시적으로 타입을 지정해주어야 한다. **(type annotation)**
```swift
let allZeros = Array(repeating: 0, count: 5) // [0, 0, 0, 0, 0]
```
* 만약 초기값과 그 갯수를 미리 정하고 싶다면 위의 방식을 이용해서 배열을 초기화할 수도 있다.
```swift
let vowels = ["A", "E", "I", "O", "U"]
```
* 만약 배열의 값이 더 이상 변하지 않았으면 할 때는 let을 사용해서 더 이상 추가되거나, 삭제되지 않도록 한다.
<br/>
<br/>
<br/>

## Accessing elements
* 이후에는 배열에 어떤 방식으로 접근하는지를 알아보자!
<br/>

### Using properties and methods
* 카드 게임을 코드로 만들어본다고 할 때, 플레이어의 이름이 담긴 배열을 저장하기를 원한다고 해보자.
* 해당 리스트는 언제든 바뀔수 있다. (새로운 플레이어가 생긴다거나, 게임을 나간다고 할 때)
```swift
var players = ["Alice", "Bob", "Cindy", "Dan"]
```
* 이번 예시에서, players는 mutable array이다. (내부 값들이 변경될 수 있으므로)
* 게임을 시작하기 전에, 게임을 하기 위한 충분한 플레이어가 있다는 것을 확인하기 위해, 
```swift
print(players.isEmpty)
// > false
```
* 배열의 isEmpty 속성을 이용해서, 해당 배열이 비어있는지, 아닌지를 확인한다.
* 이 부분에 대해서는 Chapter 11 "Properties"에서 배울 것이다. 
<br/>
<br/>

* 배열이 비어있지 않다는 것을 확인했으니, 최소 플레이어의 수를 확인해봐야한다.
```swift
if players.count < 2 {
    print("We need at least two players!")
} else{
    print("Let's start!")
}

// > Let's start!
```
* 배열의 count속성을 이용해서, 배열 값의 수를 체크하고 두명 미만이면 "We need at least two players!"를 출력하고 그렇지 않으면 "Let's start!"를 출력하도록 한다.
<br/>
<br/>
<br/>
<br/>

* 이제 게임을 시작해보자!!!!
```swift
var currentPlayer = players.first
```
* 위에서 생성한 players 배열은 알파벳 순으로 정렬이 되어있다. 여기서, 가장 첫번째 플레이어의 이름은 어떻게 얻을 수 있을까?
* 바로 배열의 first 속성을 이용하는 것이다. first속성은 배열의 가장 첫번째 object를 가져오는 역할을 한다.
<br/>

```swift
print(currentPlayer as Any)
// > Optional("Alice")
```
* first속성으로 가져온 데이터를 출력해보면 Optional 형태의 값으로 출력되는 것을 볼 수 있다.
* first 속성은 실제로 *optional*을 리턴하는데, 그 이유는 만약 배열이 비어있는 경우에는 first에 nil값이 포함되어야하기 때문이다.
* 실제로 currentPlayer를 바로 출력을 하면, warning이 뜨게 되는데, 이 warning을 없애기 위해 위와 같이 as Any로 타입을 지정해준다.
* first와 유사하게, 가장 마지막 object를 가져오는 **last** 속성이 있는데, 이것 또한 옵셔널 타입을 리턴한다.
<br/>
<br/>
<br/>

```swift
currentPlayer = players.min()
print(currentPlayer as Any)
// > Optional("Alice")
```
* 배열의 값을 가져오는 또 다른 방법 중 하나는 **min()** 를 호출하는 것이다.
* 이 메소드는 배열에서 가장 작은 작을 가지는 요소를 리턴한다.(가장 낮은 index 아님!)
* 만약 배열이 string 타입을 가진다면, 알파벳 순으로 가장 작은 값을 리턴한다. (위의 예시에서는 "Alice")
* 메소드에 대해서는 Chaper 12 "Methods" 에서 추가로 더 많이 배운다.
<br/>
<br/>

```swift
print([2, 3, 1].first as Any)
// > Optional(2)
print([2, 3, 1].min() as Any)
// > Optional(1)
```
* first 속성이나 min() 메소드를 배열에 바로 사용할 수도 있다. 
* 또한 min메소드가 있듯이 max메소드도 존재한다.!
<br/>
<br/>
<br/>
<br/>

### Using subscripting
* 배열의 값에 접근하는 가장 간단한 방법은 subscript syntax를 이용하는 것이다. 
* 이 문법은 배열의 index를 이용해서 바로 해당 값에 접근한다.
```swift
var firstPlayer = players[0]
print("First player is \(firstPlayer)")
// > First player is Alice
```
* 배열은 zero-indexed (index가 0부터 시작) 이기 때문에 [0]은 배열의 가장 첫번째 요소를 가져온다.
* 만약 배열 크기보다 더 큰 숫자로 인덱스 접근을 하게 되면 에러를 발생한다. (players[4] 는 안됨)
<br/>
<br/>
<br/>

### Using countable ranges to make an ArraySlice
* countable ranges를 이용해서 한개 이상의 값을 가져올 수도 있다.
```swift
let upcomingPlayersSlice = players[1...2]
print(upcomingPlayersSlice[1], upcomingPlayersSlice[2])
// > "Bob Cindy\n"
```
<img src="https://github.com/kanghuiseon/SwiftStudy/blob/master/07_Arrays%26Dictionaries%26Sets/Resource/1.png" height="250">

* upcomingPlayersSlice는 원래의 players 배열의  ArraySlice 타입이다. 
* 여기서 알 수 있는 것은 upcomingPlayersSlice는 players의 SubSequence이므로, players의 storage를 공유한다.
* 1...2의 범위는 players의 1,2 인덱스의 값을 의미하므로, upcomingPlayersSlice에는 Bob, Cindy가 들어간다.
* 또한, players의 storage를 공유하므로, 인덱스 또한 palyers와 동일하다.
* 만약 공유하지 않고 아예 새로운 배열로 정의하고 싶다면, 아래와 같이 한다.
```swift
let upcomingPlayersArray = Array(players[1...2])
print(upcomingPlayersArray[0], upcomingPlayersArray[1])
// > "Bob Cindy\n"
```
<br/>
<br/>
<br/>

### Checking for an element
* **contains(_:)** 를 사용해서 특정 요소가 적어도 한번 배열에서 나타나는지를 체크한다.
* 만약 존재한다면 true를 리턴하고, 그렇지 않으면 false를 리턴한다.
```swift
func isEliminated(player: String) -> Bool {
    !player.contains(player)
}
```
<br/>

* 또한 contains 메소드를 이용해서, 특정 범위에 해당 요소가 존재하는지도 체크할 수 있다.
```swift
players[1...3].contains("Bob") // true
```
<br/>
<br/>
<br/>

## Modifying arrays
* mutable arrays는 값을 추가할 수도 제거할 수도 있다. 또한 이미 존재하는 값을 업데이트 할 수도 있고, 값을 다른 위치로 이동할 수도 있다.
<br/>

### Appending elements
* 만약 새로운 플레이어들이 게임을 시작하려고 할 때, 회원가입을 하고 이름을 array에 저장하는 과정을 거쳐야 한다.
* Eli는 게임에 가입하려는 플레이어이고, 우리는 **append(_:)** 메소드를 이용해서 Eli를 추가할 수 있다.
```swift
players.append("Eli")
```
* 만약 String 이외의 타입의 값을 추가하려고 하면 컴파일러는 error를 보여줄 것이다.
* 여기서 중요한 점은 append 메소드는 mutable arrays에서만 사용할 수 있다는 점이다.
<br/>

* 만약 Gina라는 플레이어가 가입을 하려고 한다면, append 메소드가 아니라 아래의 방법으로도 배열에 추가할 수 있다.
* += 을 이용해서 하나 이상의 요소를 추가할 수도 있다.
```swift
players += ["Gina"]
```
<br/>
<br/>

### Inserting elements
* 위의 players배열은 알파벳 순으로 플레이어들의 이름을 저장한다.
* 만약 알파벳 F로 시작하는 Frank가 게임을 가입하게 된다면, 어떻게 배열에 추가를 해야할까?
* 알파벳 순서이므로 Eli와 Gina사이에 넣어야하는데, 이때에는 **insert(_:at:)** 메소드를 이용한다.
```swift
players.insert("Frank", at: 5)
```
* **at** argument에서는 값을 추가할 위치를 지정해준다.
* 배열은 zero-indexed이기 때문에, index 5는 6번째 위치라는 것을 기억해야 한다.
<br/>
<br/>

### Removing elements
* 게임 도중에 Cindy와 Gina가 속임수를 써서 게임을 진행한것을 포착했다.
* 우리는 이 둘을 방출해야하는데, 이 때에는 어떻게 해야 할까?
* 우리는 Gina가 배열의 마지막 요소라는 것을 안다. 따라서 **removeLast()** 메소드를 이용해서 쉽게 삭제할 수 있다.
```swift
var removedPlayer = players.removeLast()
print("\(removedPlayer) was removed")
// > Gina was removed
```
* 이 메소드는 두 가지 일을 한다. 첫번째로, 마지막 요소를 삭제하는 것, 두번째로 그것을 return 하는 것!
* 만약 제거된 요소를 이후에 다시 사용하고 싶다면 위의 코드와 같이 removedPlayer라는 변수를 생성하고, removeLast를 이용해서 해당 변수를 저장한다.
<br/>

* 그렇다면, Cindy는 어떻게 삭제를 해야 할까? 
* 우리는 그녀의 이름이 담긴 위치 (index)를 알고 있다. (2)
```swift
removedPlayer = players.remove(at: 2)
print("\(removedPlayer) was removed")
// > Cindy was removed
```
* 이미 알고 있는 index인 2와 **remove(at:)** 메소드를 이용해서 players에서 Cindy를 제거한다.
* 여기서도 출력을 위해 Cindy의 이름이 필요하기 때문에 removedPlayer에 저장한다.
* 위에서는 Cindy의 index를 정확하게 알고 있었지만, 만약 해당 index를 알지 못하는 경우에는 어떻게 할까? 이 때에는 **firstIndex(of:) 메소드를 활용하여서, 해당 요소의 첫번째 인덱스를 알도록 한다. 여기서 왜 첫번째 인덱스냐면, 같은 값의 요소가 여러개 있는 경우도 있을 수 있기 때문에 이것들 중에서 가장 첫번째로 존재하는 요소의 인덱스를 의미하기 때문이다.
<br/>
<br/>

### Updating elements
* Frank는 모두가 그를 Franklin으로 불러줬으면 좋겠다고 생각한다. 그러므로 우리는 배열의 Frank를 Franklin으로 바꿔주어야 한다.
```swift
print(players)
// > ["Alice", "Bob", "Dan", "Eli", "Frank"]
players[4] = "Franklin"
print(players)
// > ["Alice", "Bob", "Dan", "Eli", "Franklin"]
```
* 값을 업데이트 하는 방법은 subscrip syntax를 이용해서 index 접근을 통해 간단하게 할 수 있다.
<br/>

* 게임을 계속하다보면, 여러 명의 플레이어들이 제거되고, 새로운 사람들이 추가될 수도 있다.
* 우리는 여기서도 배열을 업데이트 해야 하는데, range를 이용해서 업데이트 할 수 있다.
```swift
players[0...1] = ["Donna", "Craig", "Brian", "Anna"]
print(players)
// > ["Donna", "Craig", "Brian", "Anna", "Dan", "Eli", "Franklin"]
```
* 위에서, players의 0번째 인덱스와 1번째 인덱스인 Alice, Bob을 "Donna", "Craig", "Brian", "Anna"로 대체한다.
<br/>
<br/>

### Moving elements
* 위의 코드 진행 이후에 players 배열 내부를 살펴보니, 우리가 처음에 설정했던 알파벳 순 규칙은 지켜지지 않고 있었다.
* 우리는 이 규칙을 다시 제대로 지키기 위해서, 다양한 방법을 사용할 수 있다.
```swift
// 1
let playerAnna = players.remove(at: 3)
players.insert(playerAnna, at: 0)
print(players)
// > ["Anna", "Donna", "Craig", "Brian", "Dan", "Eli", "Franklin"]


// 2
players.swapAt(1, 3)
print(players)
// > ["Anna", "Brian", "Craig", "Donna", "Dan", "Eli", "Franklin"]


// 3
players.sort()
print(players)
// > ["Anna", "Brian", "Craig", "Dan", "Donna", "Eli", "Franklin"]
```
* 1. 위에서부터 보면, remove메소드를 이용해서 Anna를 현재 위치에서 제거하고, insert 메소드를 이용해서 올바른 위치에 삽입한다.
* 2. 두번째 방법으로는 swapAt 메소드를 활용하는 것인데, 첫번째 위치의 값을 두번째 위치의 값과 위치를 바꾸는 것이다.
* 3. 세번째 방법은 **sort()** 메소드를 이용해서 간단하게 알파벳 순서대로 정렬하는 것이다. 만약 원래의 배열은 그대로 두고 새롭게 정렬된 copy를 가지고 싶다면, **sorted()** 메소드를 이용하면 된다.
<br/>
<br/>
<br/>
<br/>

## Iterating through an array
* 지금 시각이 너무 늦어서, 플레이어들은 현재 점수를 따로 배열에 저장하고, 게임을 멈추고 싶어 한다.
```swift
let scores = [2, 2, 8, 6, 1, 2, 1]
```
<br/>

* 플레이어들이 게임을 중지하기 전에, 그들의 이름을 출력하고 싶어 한다. 우리는 여기서 for-in loop를 이용할 수 있다.
```swift
for player in players {
  print(player)
}
// > Anna
// > Brian
// > Craig
// > Dan
// > Donna
// > Eli
// > Franklin
```
* 위의 코드는 players 배열 내부의 값들을 모두 출력한다.
* 첫번째 iteration의 player는 players의 첫번째 값이고, 두번째 iteration의 player는 두번째 값, 이렇게 해서 players.count-1의 값까지 출력이 된다.
<br/>
<br/>

* 만약 해당 player의 이름과 index를 함께 출력하고 싶다면, 아래와 같이 (index, player)를 통해 index에 접근한다.
```swift
for (index, player) in players.enumerated() {
  print("\(index + 1). \(player)")
}
// > 1. Anna
// > 2. Brian
// > 3. Craig
// > 4. Dan
// > 5. Donna
// > 6. Eli
// > 7. Franklin
```
<br/>
<br/>
<br/>
<br/>

## Running time for array opertaions
* Arrays는 메모리에 연속적인 블록으로 저장이 된다. 만약 배열에 열 개의 값들이 저장되어 있다면, 그 열 개의 값들은 차례대로 메모리에 저장이 되어있다.
* **Accessing elements** : 배열에서 값을 가져오는 것은 시간이 오래 걸리지 않는다. (바로 접근할 수 있기 때문에) 이때, 우리는 constant time이 걸린다고 하는데, 이것은 O(1)로 표현될 수 있다. 배열 내부의 값들은 sequential하게 구성되어있기 때문에 random access가 가능하고, 특정 index의 값에 바로 접근할 수 있다. (이것을 위해서, compiler는 배열이 어디서부터 시작되는지를 알아야 한다.)
* **Inserting elements** : 배열에 새로운 값을 추가할 때에는 추가할 위치에 따라 걸리는 시간이 다르다.
    * 만약 배열의 시작에 넣고자 한다면, 배열의 크기에 따라 걸리는 시간이 달라진다. 그 이유는 새로운 값을 배열의 첫번째에 넣으면, 기존에 있던 값들은 모두 한칸씩 뒤로 밀려나기 때문이다. 여기서 우리는 배열 크기 n만큼의 시간이 걸린다고 해서 O(n)으로 표현할 수 있다.
    * 만약 배열 중간에 새로운 값을 넣고 싶다면, 그 뒤의 값들이 한칸씩 밀려나기 때문에 n/2의 시간이 걸린다. 여전히 running time은 linear하기 때문에 O(n)으로 표현할 수 있다.
    * 만약 배열의 끝에 값을 넣으려고 할 때, 배열에 공간이 있다면, 뒤로 밀려날 값이 없기 때문에 O(1)의 시간이 걸린다. 만약 공간이 없다면 Swift는 공간을 만들어야해서, 전체 배열을 복사하고 새로운 값을 추가하기 때문에 O(n)의 시간이 걸린다. 하지만 평균 case는 O(1)인데, 그 이유는 arrays는 대체적으로 꽉 차 있지 않기 때문이다.
* **Deleting elements** : 값을 제거할때에는 만약 가장 마지막 요소를 제거한다면 O(1)이 걸리지만, 그렇지 않다면, 뒤에 있는 요소들을 앞으로 땡겨줘야하기 때문에 O(n)의 시간이 걸린다.
* **Searching for an element** : 만약 배열의 첫번째 요소를 검색한다면, 한번의 operation만 하고 끝난다. 만약 요소가 존재하지 않는다면, 우리는 N 번의 operations 후, 값이 없다는 것을 알고 검색을 끝낸다. 평균적으로 n/2 operations을 수행하기 때문에 시간 복잡도는 O(n)이다.
<br/>
<br/>
<br/>
<br/>

## Dictionaries
* dictionary는 순서가 없는 pair의 collection이다. 여기서 pair는 **key**,  **value**를 가진다.
<img src="https://github.com/kanghuiseon/SwiftStudy/blob/master/07_Arrays%26Dictionaries%26Sets/Resource/2.png" height="250">

* 위의 사진에서 보는것과 같이 key는 **unique** 해야 한다. 같은 key는 존재할 수 없으며, 같은 value는 존재할 수 있다.
* 또한 모든 key는 같은 type을 가져야 하고, 모든 값들은 같은 타입을 가져야 한다.
* Dictionaries는 identifier을 이용해서 값을 찾으려고 할 때, 유용하게 쓰인다.
* 그렇다면 앞에서 배운 배열과는 어떻게 다를까? array는 integer index(sequential한)로만 접근할 수 있었다면, dictionary에서는 key는 어떤 타입도 가질 수 있으며, 순서는 필요없다.  
<br/>
<br/>

## Creating dictionaries
* dictionary를 생성하는 방법은 **dictionary literal**를 사용하는 것이다.
* 콤마로 key-value pair를 구분하고, 이것을 대괄호로 감싼다.
* 앞에서 봤던 card game를 dictionary로 표현한다면, 아래와 같이 플레이어 이름과 점수를 동시에 표현할 수 있다.
```swift
var namesAndScores = ["Anna": 2, "Brian": 2, "Craig": 8, "Donna": 6]
print(namesAndScores)
// > ["Craig": 8, "Anna": 2, "Donna": 6, "Brian": 2]

namesAndScores = [:]
```
* 위의 예시에서 컴파일러는 namesAndScores의 타입을 [Stirng: Int]로 추론할 수 있다.
* 이것을 출력해보면 **무작위로** pairs가 구성된것을 볼 수 있다. 
* 또한 빈 딕셔너리로 초기화하고 싶다면 **[:]** 를 사용한다.
<br/>

* 만약 빈 딕셔너리를 가진 새로운 딕셔너리를 생성하고 싶다면, 아래와 같이 타입을 명시하고 선언한다.
```swift
var pairs: [String: Int] = [:]
pairs.reserveCapacity(20)
```
* 딕셔너리를 생성한 이후에, reserveCapacity()를 이용해서 capacity도 지정할 수 있다.
<br/>
<br/>

## Accessing values
### Using subscripting
* 딕셔너리는 value에 접근하기 위해 subscripting을 지원한다. 배열과는 달리, 인덱스로 접근하지 않고, key로 접근한다.
```swift
namesAndScores = ["Anna": 2, "Brian": 2, "Craig": 8, "Donna": 6]
// Restore the values

print(namesAndScores["Anna"]!) // 2
```
* 여기서, namesAndScores["Anna"]의 값이 optional인 것을 확인할 수 있다.
* 딕셔너리에서는 해당 key값이 존재하지 않을 수도 있다. 따라서, 해당 key값이 존재하는지 우선 확인하고 value를 리턴한다.
* 만약 존재하지 않는 key값으로 접근하면 nil이 리턴된다.
<br/>
<br/>

### Using properties and mothods
* arrays와 같이 Dictionaries에서는 Swift의 Collection protocol을 채택한다. 그래서 공통되는 프로퍼티를 가진다.
```swift
namesAndScores.isEmpty  //  false
namesAndScores.count    //  4
```
* 예시로, isEmpty와 count 프로퍼티가 있다. 
<br/>
<br/>
<br/>
<br/>

## Modifying dictionaries
### Adding pairs
* Bob이 게임을 하길 원한다고 해보자.
<img src= "https://github.com/kanghuiseon/SwiftStudy/blob/master/07_Arrays%26Dictionaries%26Sets/Resource/3.png" height="200">

* Bob을 가입시키기 전에 그의 인적사항을 보자.
```swift
var bobData = [
  "name": "Bob",
  "profession": "Card Player",
  "country": "USA"
]
```
* 이 딕셔너리는 [String: String] 타입이고, mutable이다. 
* 만약 Bob에 대해서 더 많은 정보를 알고 싶고 딕셔너리에 추가하기를 원한다면 아래의 코드를 추가해야 한다.
```swift
bobData.updateValue("CA", forKey: "state")
```
* 위의 코드는 아래와 같이 더 짧게 쓸 수도 있다.
```swift
bobData["city"] = "San Francisco
```
<br/>
<br/>

### Updating values
* 만약 Bob이 게임 내에서 다른 이름으로 활동하고 싶다고 한다면, 우리는 아래와 같이 Bob의 이름을 Bobby로 바꿔줄 수 있다.
```swift
bobData.updateValue("Bobby", forKey: "name") // Bob
```
* updateValue는 만약 forKey 에 해당하는 key 값이 존재한다면 해당 key의 value의 값을 업데이트하고 old value를 리턴한다. 존재하지 않는다면 새로운 key를 생성하고 nil을 리턴한다.
* 위의 방식 말고 더 간단하게도 값을 업데이트할 수 있다.
```swift
bobData["profession"] = "Mailman"
```
<br/>
<br/>

### Removing paris
* Bobby는 자신의 정보가 많이 드러나는 것을 원하지 않아서 본인이 사는 곳에 대한 정보를 지우고 싶어한다.
```swift
bobData.removeValue(forKey: "state")
```
* removeValue 메소드는 key state와 그에 해당하는 값을 지운다.
* 이것도 간단하게 쓴느 방법이 있다.
```swift
bobData["city"] = nil
```
* key값에 nil를 할당하면, 딕셔너리에서 해당 pair를 삭제한다. 
* 만약 key값은 그대로 남겨두고 싶다면 updateValue 메소드를 이용해서 nil값을 설정한다.
<br/>
<br/>

### Iterating through dictionaries
* for-in loop를 이용해서 딕셔너리 값에 접근할 수 있다.
* 딕셔너리 값은 pair이기 때문에 tuple을 이용해서 key, value에 접근한다.
```swift
for (player, score) in namesAndScores {
  print("\(player) - \(score)")
}
// > Craig - 8
// > Anna - 2
// > Donna - 6
// > Brian - 2
```
<br/>

* 또한 key값에만 접근할 수도 있다. 
```swift
for player in namesAndScores.keys {
  print("\(player), ", terminator: "") // no newline
}
print("") // print one final newline
// > Craig, Anna, Donna, Brian, 
```
<br/>
<br/>
<br/>

### Running time for dictionary operations
* 딕셔너리가 어떻게 작동하는지를 이해하기 위해서는 **hashing** 에 대해서 우선 알아볼 필요가 있다.
* Hashing은 value(String, Int, Double, Bool, etc)를 nemueric value (hash value)로 바꿔주는 과정이다. 
* Swift 에서 딕셔너리의 keys는 무조건 Hashable이어야한다. 
* 운이 좋게도, Swift에서 기본 타입들은 모두 Hashable을 채택하고 있고, hash value를 가진다. 이 값은 deterministic 해야 하는데, 이것은 주어진 값은 *항상* 동일한 hash value를 리턴해야 한다는 의미이다.
<br/>
<br/>

> 딕셔너리도 다양한 operation이 있는데 이것들의 성능을 알아보자.
* **Accessing elements** : key에 대한 값을 얻는 것은 O(1)의 시간이 걸린다.
* **Inserting elements** : 값을 추가하기 위해서, 딕셔너리는 key의 hash value를 계산하고, 딕셔너리에 저장한다. 이것도 O(1)의 시간이 걸린다.
* **Deleting elements** : 딕셔너리는 지우려는 값이 어디 있는지를 파악하고 지우는데, 이것도 O(1) 이 걸린다.
* **Searching for an element** : 값에 접근하는게 상수의 시간이 걸리므로 검색하는것도 O(1)의 시간이 걸린다.
<br/>
<br/>
<br/>
<br/>

## Sets
* set은 같은 타입의 unique value들의 **순서가 없는** 집합이다. 
* 이것은 값이 한 번 이상 존재하지 않는 것을 보장해줘서 매우매우 유용하게 쓰인다.
<img src="https://github.com/kanghuiseon/SwiftStudy/blob/master/07_Arrays%26Dictionaries%26Sets/Resource/4.png" height="250">

* 그림에서는 4 strings가 존재하고, 순서가 존재하지 않는 것을 볼 수 있다.
<br/>
<br/>

### Creating sets
* set은 꺽쇠를 이용해서 타입을 지정하고 대괄호로 값을 지정한다.
```swift
let setOne: Set<Int> = [1]
```
<br/>
<br/>

### SEt literals
* Sets는 own literals가 없기 때문에 array lieterals를 사용해서 set를 만든다.
```swift
let someArray = [1, 2, 3, 1]

// 1
var explicitSet: Set<Int> = [1, 2, 3, 1]

// 2
var someSet = Set([1, 2, 3, 1])

print(someSet)
// > [2, 3, 1] but the order is not defined
```
* 맨 위의 array 리터럴에서 Set<Int> 타입을 따로 지정해주면 set이 된다.
* 또한 타입을 명시하지 않아도 두번째 방법처럼 set을 생성할 수도 있다.
* 이것을 출력하면, 중복은 사라지고, 순서 없이 출력이 된 것을 볼 수 있다.
<br/>
<br/>
<br/>

### Accessing elements
* contains(_:)를 이용해서 특정 값의 존재를 확인할 수도 있다.
```swift
print(someSet.contains(1))
// > true
print(someSet.contains(4))
// > false
```
* 또한, first, last 프로퍼티도 사용할 수 있다. 하지만 순서가 없기 때문에 어떤 아이템인지는 알 수 없다.
<br/>
<br/>

### Adding and removing elements
* insert(_:)를 이용해서 set에 값을 추가할 수도 있다. 만약 이미 존재한다면 메소드는 아무 일도 하지 않는다.
* 또한 remove를 이용해서 요소를 제거하고 해당 값을 리턴할 수도 있다. 만약 존재하면 제거된 값이 리턴되고 존재하지 않으면 nil을 리턴한다.
```swift
someSet.insert(5)

let removedElement = someSet.remove(1)
print(removedElement!)
// > 1
```
<br/>
<br/>

### Running time for set operations
* Sets는 딕셔너리와 유사하게 값들이 hashable이어야 한다. 모든 running time은 딕셔너리와 동일하다.

