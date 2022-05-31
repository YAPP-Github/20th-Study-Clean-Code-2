## 자료구조 vs 객체

- 자료구조
    - 데이터 그 자체
    - 자료를 공개
    
- 객체
    - 비즈니스 로직을 가지고 있음
    - 자료를 숨기고 추상화 → 자료를 다루는 함수만 공개
    
<br>

### 자료 추상화

자료구조에서 get/set 메서드만 이용해서 프로퍼티에 접근하는 방법은 좋지 않다!

```swift
struct Car {
    private var fuelTankCapacityInGallons: Int
    private var gallansOfGasoline: Int
    
    // 👎
    
    func getFuelTankCapacityInGallons() {
        
    }
    
    func getGallansOfGasoline() {
        
    }
    
    // 👍
    
    func getPercentFuelRemaining() {
        
    }
}
```

<br>

### 자료구조 / 객체 비대칭

```swift
protocol Shape {
    
}

struct Square: Shape {
    var topLeft: Double
    var side: Double
}

struct Rectangle: Shape {
    var topLeft: Double
    var side: Double
    var width: Double
}

struct Circle: Shape {
    var center: Double
    var radius: Double
}

struct Geometry {
    var PI: Double
    
    func area(object: Shape) {
        if let object = object as? Square {
            // Square logic
        } else if let object = object as? Rectangle {
            // Rectangle logic
        } else if let object = object as? Circle {
            // Circle logic
        }
    }
}
```

→ 절차적인 코드는 기존 자료구조를 변경하지 않으면서 새함수를 추가하기 쉽다.  
하지만 새로운 자료구조를 추가하기는 어렵다 ( 함수를 고쳐야 함 )

<br>

```swift
protocol Shape {
    func area()
}

struct Square: Shape {
    var topLeft: Double
    var side: Double
    
    func area() {
        // Square logic
    }
}

struct Rectangle: Shape {
    var topLeft: Double
    var side: Double
    var width: Double
    
    func area() {
        // Rectangle logic
    }
}
```
→ 객체 지향 코드는 새로운 클래스를 추가하기 쉽다.  하지만 새로운 함수를 추가하긴 어렵다

<br>

### 결론: 상황에 맞는 선택을 하라

<br>

## 객체 디미터의 법칙

모듈은 자신이 조작하는 객체의 속사정을 몰라야한다.

→ 객체는 get함수로 내부 구조를 공개하면 안된다!  
→ 위 객체에서 허용된 메서드가 반환하는 객체의 메서드는 호출하면 안된다.  
→ 낯선 사람은 경계하고 친구랑만 놀아라~  

<br>

### 기차 충돌

```swift
// 객체인 경우 - 기차 충돌
var output: String = ctxt.getOptions().getScatchDIR().getAbsolutePath()

// 자료구조는 OK
var output: String = ctxt.options.scratchDir.absolutePath
```

<br>

### 잡종 구조

절반은 객체, 절반은 자료구조인 잡종 구조가 나올 수 있다  
→ 이런 잡종 구조는 새로운 함수는 물론이고 새로운 자료구조도 추가하기 어렵게 된다 따라서 잡종구조는 되도록 피하자

<br>

## DTO

다른 계층 간 데이터를 교환할 때 사용
- 로직없이 필드만 가짐
- getter/setter를 갖기도 한다
→ 요새는 getter나 setter를 붙이지 않고 프로퍼티를 public하게 만들어서 접근할 수 있게 합니다

<br>

## Active Record

데이터 베이스 row를 객체에 맵핑하는 패턴

- 비즈니스 로직 메서드를 추가하여 객체로 취급하는 것은 바람직하지 않음
- 비즈니스 로직을 담으면서 내부자료를 숨기는 객체는 따로 생성

→ entity에 간단한 메서드를 추가하여 

<br>

### Active Record vs Data Mapper

- Active Record
    - 객체가 row를 담을 뿐만 아니라 database에 접근
    - 프로퍼티를 담고 생성 수정도 객체 내에서 수행
    
- Data Mapper
    - row를 담는 객체와 database에 접근하는 객체가 분리
    - 프로퍼티만 담고, 생성 수정은 mapper에서 담당
