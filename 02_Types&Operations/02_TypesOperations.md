# 2 Types & Operation

`type` 은 value의 집합과 타입에 대해 이루어질수 있는 오퍼레이션을 describe한다. 이번 챕터에서는 아래와 같은 내용에 대해서 배운다.

- 문자열 타입등 여러타입을 다루는 방법
- 타입을 변환하는 방법과 타입추론
- 튜플 타입

# Type Conversion

```swift
var integer: Int = 100
var decimal: Double = 12.5
integer = decimal
```

스위프트는 타입에 대해 엄격한 언어이다. 일부언어에서는(C언어) 자동으로 형변환을 지원하기도 하지만 스위프트는 그렇지 않다.  다른 타입에 대해 assign해주기 위해서는 `Type()` 으로 감싸주어 명시적 형변환을 해주어야한다. 

```swift
integer = Int(decimal)
```

## Operators with mixed Types

```swift
let hourlyRate: Double = 19.5
let hoursWorked: Int = 10
let totalCost: Double = hourlyRate * hoursWorked
```

Swift는 타입에 엄격하기 떄문에 혼합된 타입에 대한 오퍼레이션 또한 지원하지 않는다. totalCost를 더블로 받고싶다면 hoursWorked를 `Double(hoursWorked)` 로 바꿔줘야한다.

## Type Inferance

Swift는 타입추론을 지원한다. 스위프트가 추론할수 없는 어려운 타입이 아닌경우라면 constant나 variable을 선언할때 type annotation을 생략할수 있다.

```swift
let typeInferredInt = 42
```

- 어떤 타입으로 할당되었는지 확인은 커서를 이름에 가져다대고 option키를 누르면 확인할수 있다.

```swift
let wantADouble = 3
```

스위프트에서 위와 같이 쓰면 기본적으로 타입추론은 Int형으로 된다. Doble로 쓰고싶다면 아래 방법들을 이용할수있다.

```swift
let actuallyDouble = Double(3)
let actuallyDouble: Double = 3
let actuallyDouble = 3 as Double

let wantDouble = 3.0
```

# Strings

텍스트형식은 컴퓨터 프로그래밍에서 보통 `stirng` 으로 저장한다.

## How computers represent strings

기본적으로 cpu는 numerical한 연산을 수행한다. 따라서 문자열도 숫자로 변경될 필요가 있다. 각각의 문자열은 character의 집합이므로 각 character는 미리정해진 숫자로 변환된다. 

이런 변환 형식을 `character set`이라고 하며 가장 많이 쓰이는 형식은 Unicode이다. 유니코드에는 알파벳부터 중국어, 심지어 이모지 까지 모두 숫자로 변호나도니다.

# Strings in Swift

Swift는 `Character` 와 `String` 데이터타입으로 문자열에 직접접근이 가능하다.

## Characters and strings

Character 데이터타입은 하나의 문자만을 저장하며 타입을 따로 적지 않을경우 단일문자는 String타입으로 타입추론된다.

## Concatenation

`+` 연산자를 이용해서 Stirng끼리 concatanate할수있다.

```swift
var message = "Hello" + " my name is "
let name = "Matt"
message += name // "Hello my name is Matt"
```

- Character 타입을 String에 더할수도 있지만 이경우 `String()` 으로 형변환이 필요하다.

## Interpolation

스위프트의 특징적인 문자열 문법이다 이를 이용해서 문자열을 합칠수도 있다.

```swift
message = "Hello my name is \(name)!" // "Hello my name is Matt!"
```

```swift
let oneThird = 1.0 / 3.0
let oneThirdLongString = "One third is \(oneThird) as a decimal."

//One third is 0.3333333333333333 as a decimal.
```

다만 interpolation을 사용하면 precision을 지정하는것과 겉은 불가능하다. 쉽고 가독성도 좋지만 output을 커스텀하지못한다는 점이 있다.

## Multi-line strings

```swift
let bigString = """
  You can have a string
  that contains multiple
  lines
  by
  doing this.
  """
print(bigString)
```

`"""` 연산자를 이용해서 멀티라인 string을 구성할수도 있다.

- 마지막줄의 """의 스페이싱을 기준으로 다른줄의 스페이싱을 제거하기 때문에 최소 저 기준만큼은 띄어써야한다.

# Tuples

tuple은 하나이상의 여러타입으로 구성된(단일타입일수도 있다) 묶음이다. 

```swift
let coordinates: (Int, Int) = (2, 3)
```

coordinates의 타입은 `(Int, Int)`  가 된다.

```swift
let coordinates = (2, 3)
let coordinatesMixed = (2.1, 3)
// Inferred to be of type (Double, Int)
```

타입추론도 동일하게 가능하며 다른타입끼리 묶는것도 가능하다.

```swift
let x1 = coordinates.0
let y1 = coordinates.1
```

접근은 index를 이용해 접근할수 있다. 0부터 시작한다.

```swift
let coordinatesNamed = (x: 2, y: 3)
// Inferred to be of type (x: Int, y: Int)

let x2 = coordinatesNamed.x
let y2 = coordinatesNamed.y
```

이름을 지정할수도 있으며 이경우 이름으로 접근이 가능하다.

```swift
let coordinates3D = (x: 2, y: 3, z: 1)
let (x3, y3, z3) = coordinates3D
```

각각의 원소에 접근하고 싶으면 위와같은 간단한 문법도 존재한다.

```swift
let coordinates3D = (x: 2, y: 3, z: 1)
let (x3, y3, _) = coordinates3D

```

일부원소는 무시하고 받고 싶으면 `_`  을 이용하면 된다. 

# A whole lot of number types

storage사이즈에 따라 1,2,4,8 바이트의 Int는 각각 Int8 Int16 Int32 Int64 로 나뉜다. 부호가 없는 Unsigned의 경우 양수만 표현하기 때문에 maximum값이 그냥 singned에 비해 2배이다.

![2%20Types%20&%20Operation%20eb6eeb93e1204cd7bfb75c5df93513f5/Untitled.png](2%20Types%20&%20Operation%20eb6eeb93e1204cd7bfb75c5df93513f5/Untitled.png)

Swift의 Int형은 최근 하드웨어에서는 64bit로 이전 옛날 하드웨어에서는 32비트로 표현된다. 다른 컴퓨터의 소프트웨어와 교류해야하거나 정확한 사이즈가 필요한 겨웅에는 위에 나열된 숫자가 붙은 Int형을 사용하면 된다.

4바이트의 경우 Float실수형, 8바이트의 경우 Double실수형이다. 최근의 하드웨어는 모두 더블형을 기준으로 최적화되있으므로 Swift에서는 Double형만을 생각하면 된다. 바이트수가 두배기때문에 precision면에서 Double이 두배의 precision을 나타낼수 있다. 

![2%20Types%20&%20Operation%20eb6eeb93e1204cd7bfb75c5df93513f5/Untitled%201.png](2%20Types%20&%20Operation%20eb6eeb93e1204cd7bfb75c5df93513f5/Untitled%201.png)

- 다른 인트형들을 이용해 연산을 하고싶을땐 형변환을 해주면 된다.

```swift
let a: Int16 = 12
let b: UInt8 = 255
let c: Int32 = -100000

let answer = Int(a) + Int(b) + Int(c)  // answer is an Int
```

# Type aliases

자신만의 타입을 만들수있는 스위프트의 편리한 기능이다. 정확히말하면 기존 타입에 새로운 이름을 붙이는 것이다. 실제로는 다른타입이지만 컴파일러가 type aliases문을 보면 앞으로 적는 새로운 이름의 타입을 기존타입처럼 다룬다.

```swift
typealias Animal = String
let myPet: Animal = "Dog"

typealias Coordinates = (Int, Int)
let xy: Coordinates = (2, 4)
```

# A peek behind the curtains

지금까지 배운 여러타입들이 있지만 사용하는건 그렇게 어렵지 않다. 이는 스위프트가 여러 타입에 대한 공통적인 특성을 공유하기 때문인데 이 type commonality를 가능하게하는 기능을 `protocol` 이라고 한다.

![2%20Types%20&%20Operation%20eb6eeb93e1204cd7bfb75c5df93513f5/Untitled%202.png](2%20Types%20&%20Operation%20eb6eeb93e1204cd7bfb75c5df93513f5/Untitled%202.png)

모든 타입의 모든 protocol을 나타낸것은 아니지만 대략적으로 타입들은 위와같은 protocol을 따른다.

Swift는 first protocol-based langage라는것만 알고 일단 넘어가자

## **Key points**

- Type conversion allows you to convert values of one type into another.
- Type conversion is required when using an operator, such as the basic arithmetic operators (`+`, ``, ``, `/`), with mixed types.
- Type inference allows you to omit the type when Swift already knows it.
- **Unicode** is the standard for mapping characters to numbers.
- A single mapping in Unicode is called a **code point**.
- The `Character` data type stores single characters. The `String` data type stores collections of characters, or strings.
- You can combine strings by using the addition operator.
- You can use **string interpolation** to build a string in-place.
- You can use tuples to group data into a single data type.
- Tuples can either be unnamed or named. Their elements are accessed with index numbers for unnamed tuples, or programmer given names for named tuples.
- There are many kinds of numeric types with different storage and precision capabilities.
- Type aliases can be used to create a new type that is simply a new name for another type.
- Protocols are how types are organized in Swift. They describe the common operations that multiple types share.