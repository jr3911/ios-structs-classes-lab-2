# Structs and Classes Lab - 2


## Question 1

Using the Room struct below, write code that demonstrates that it is a value type.
**Worked as a pair
```swift
struct Room {
     let maxOccupancy: Int
     let length: Double
     let width: Double
}

var roomA = Room(maxOccupancy: 5, length: 5, width: 5)
var roomB = roomA
roomA = Room(maxOccupancy: 10, length: 10, width: 10)

print(roomA)
print(roomB)
```

## Question 2

Using the Bike class below, write code that demonstrates that it is a reference type.
**Worked as a pair

```swift
class Bike {
    var wheelNumber = 2
    var hasBell = false
}

var bike1 = Bike()
bike1.wheelNumber = 5
var bike2 = bike1
bike2.wheelNumber = 90
print(bike1.wheelNumber)
print(bike2.wheelNumber)
```

## Question 3

a. Given the Animal class below, create a Bird subclass with a new `canFly` property.
**Worked as a pair
```swift
class Animal {
    var name: String = ""
    func printDescription() {
        print("I am an animal named \(name)")
    }
}

class Bird: Animal {
    var canFly = true
    override func printDescription() {
        print("I am an animal named \(name) and it's \(canFly) that I can fly")
    }
}

```

b. Override the printDescription method to have the instance of the Bird object print out its name and whether it can fly


## Question 4
**Worked as a pair
```swift
class Bike {
  let wheelNumber = 2
  let wheelWidth = 1.3
  var hasBell = true
  func ringBell() {
    if hasBell {
      print("Ring!")
    }
  }
}

class LoudBike: Bike {
    override func ringBell() {
        print("RING!")
    }
    func ringBell(times times: Int) {
        for i in 0..<times {
            ringBell()
        }
    }
}

var bike1 = LoudBike()
bike1.ringBell(times: 5)

```


a. Create a `LoudBike` subclass of Bike.  When you call `ringBell` it should ring the bell in all caps.

b. Give `LoudBike` a new method called `ringBell(times:)` that rings the bell a given number of times


## Question 5
**Worked as a pair
```swift
class Shape {
    var name: String { return "This is a generic shape" }
    var area: Double { fatalError("Subclasses must override the area") }
    var perimeter: Double { fatalError("Subclasses must override the perimeter") }
}
```

a. Given the `Shape` object above, create a subclass `Square` with a property `sideLength` with a default value of 5.

```swift
class Square: Shape {
    var sideLength = 5.0
}
```

b. Override the `area` and `perimeter` computed values so it returns the area/perimeter of the square as appropriate

```swift
class Square: Shape {
    var sideLength = 5.0
    override var area: Double {
        return pow(sideLength, 2)
    }
    override var perimeter: Double {
        return sideLength * 4
    }
}
```

c. Override the `name` property of `Square` so that it returns a String containing its name ("Square") and its area and perimeter

```swift
class Square: Shape {
    var sideLength = 5.0
    override var area: Double {
        return pow(sideLength, 2)
    }
    override var perimeter: Double {
        return sideLength * 4
    }
    override var name: String {
        return "Square, \(area) and \(perimeter)"
    }
}
```

d. Create a class `Rectangle` that subclasses from `Shape`.  Give it a `width` property with a default value of 6 and a `height` property with a default value of 4

```swift
class Rectangle: Shape {
    var width = 6
    var height = 4
}
```

e. Override the `name` property of `Rectangle` so that it returns a String containing its name ("Rectangle") and its area and perimeter.

```swift
class Rectangle: Shape {
    var width = 6.0
    var height = 4.0
    override var perimeter: Double {
        return 2 * width + 2 * height
    }
    override var area: Double {
        return width * height
    }
    override var name: String {
        return "Rectangle, this is the area, \(area) and this is the perimeter \(perimeter)"
    }
}

```

f. (BONUS) What happens when you run the code below?  Explain why.

```swift
var myShapes = [Shape]()

myShapes.append(Square())
myShapes.append(Rectangle())

for shape in myShapes {
    print("This is a \(shape.name) with an area of \(shape.area) and a perimeter of \(shape.perimeter)")
}
```

## Question 6
**Worked as a pair
a. Given the Point object below, complete the `distance` method so that it returns the distance between a given point.

The equation for the distance formula can be found [here](https://www.mathsisfun.com/algebra/distance-2-points.html) and is give by:

```swift
let horizontalDistance = pointOneXValue - pointTwoXValue
let verticalDistance = pointOneYValue - pointTwoYValue
let distanceBetweenTwoPoints = sqrt(horizontalDistance * horizontalDistance + verticalDistance * verticalDistance)
```

`sqrt` is a method in Swift that gives the square root.  Make sure to have `import Foundation` or `import UIKit` to use this method.

```swift
struct Point {
    let x: Double
    let y: Double
    func distance(to point: Point) -> Double {
        let horizontalDistance = self.x - point.x
        let verticalDistance = self.y - point.y
        let distanceBetweenTwoPoints = sqrt(horizontalDistance * horizontalDistance + verticalDistance * verticalDistance)
        return distanceBetweenTwoPoints
    }
}

let pointOne = Point(x: 0, y: 0)
let pointTwo = Point(x: 10, y: 10)

print(pointOne.distance(to: pointTwo)) //Prints 14.142135623730951
```


b. Given the above Point object, and Circle object below, add a `contains` method that returns whether or not a given point is on the circle

```swift
struct Circle {
    let radius: Double
    let center: Point
    
    func contains(_ point: Point) -> Bool {
        return self.center.distance(to: point) == self.radius 
    }
}

let pointOne = Point(x: 0, y: 0)
let circleOne = Circle(radius: 5, center: pointOne)
let pointTwo = Point(x: 5, y: 0)
let pointThree = Point(x: 4, y: 0)
let pointFour = Point(x: sqrt(12.5), y: sqrt(12.5))
circleOne.contains(pointTwo) //true
circleOne.contains(pointThree) // false
circleOne.contains(pointFour) //true
```

c. Add another method to `Circle` that returns a random point on the circle
**Worked on solo
Hint: Given the radius of a circle and the x value of a point on the circle, the y value of the point is defined by:

```
√(r^2) - (x^2)
```

```swift
func getRandomPoint() -> Point {
    let x = Double.random(in: -radius...radius)
    let y = sqrt(pow(self.radius, 2) - pow(x, 2))
    return Point(x: x, y: y)
}
circleOne.contains(circleOne.getRandomPoint()) //Should always be true
```


## Question 7
**Worked on solo

```swift
struct HangmanModel {
    var targetWord: String = String()
    var numberOfIncorrectGuesses: Int = Int()
    var guessedLetters: [Character] = [Character]()

    func playerWon() -> Bool {
        let setTargetWord = Set(targetWord)
        for char in setTargetWord where guessedLetters.contains(char) == false {
            return false
        }
        return true
    }

    func printDisplayVersionOfWord() {
        var newWord = ""
        for char in targetWord {
            if guessedLetters.contains(char) {
                newWord.append(String(char))
            } else {
                newWord.append("_")
            }
        }
        print(newWord)
    }

    mutating func guess(_ charInput: Character) {
        self.guessedLetters.append(charInput)
        if targetWord.contains(charInput) == false {
            self.numberOfIncorrectGuesses += 1
        }
        self.printDisplayVersionOfWord()
        print("Number of wrong guesses: \(self.numberOfIncorrectGuesses)\n")
        if playerWon() {
            print("Congratulations! You won!")
        }
    }
}
```
a. Create a struct called HangmanModel with 3 properties `targetWord: String`, `numberOfIncorrectGuesses: Int` and `guessedLetters: [Character]`.

```swift
struct HangmanModel {
    var targetWord: String = String()
    var numberOfIncorrectGuesses: Int = Int()
    var guessedLetters: [Character] = [Character]()
}
```

b. Add a method called `playerWon` that returns whether all of the characters in `targetWord` are in `guessedLetters`

```swift
func playerWon() -> Bool {
    let setTargetWord = Set(targetWord)
    for char in setTargetWord where guessedLetters.contains(char) == false {
        return false
    }
    return true
}

var model = HangmanModel()
model.targetWord = "hello"
model.guessedLetters = ["h","e","o","l"]
model.playerWon //true
```

c. Add a method called `printDisplayVersionOfWord` that prints the `targetWord` replacing characters that are not in `guessedLetters` with "\_"

```swift
func printDisplayVersionOfWord() {
    var newWord = ""
    for char in targetWord {
        if guessedLetters.contains(char) {
            newWord.append(String(char))
        } else {
            newWord.append("_")
        }
    }
    print(newWord)
}

var model = HangmanModel()
model.targetWord = "hello"
model.guessedLetters = ["h","l"]
model.printDisplayVersionOfWord
//prints h_ll_
```

d. Add a method called `guess(_:)` that takes in a character as input, and updates `guessedLetters` and `numberOfIncorrectGuesses` as appropriate.

```swift
mutating func guess(_ charInput: Character) {
    //updates guessedLetters
    self.guessedLetters.append(charInput)
    
    //updates numberOfIncorrectGuesses
    if targetWord.contains(charInput) == false {
        self.numberOfIncorrectGuesses += 1
    }
}

var model = HangmanModel()
model.targetWord = "hello"
model.guess("h")
model.guess("a")
model.guessedLetters // ["h", "a"]
model.numberOfIncorrectGuesses // 1
```

e. Have `guess(_:)` also print out the current display version of the word, the number of incorrect guesses and if the player has won.

```swift
mutating func guess(_ charInput: Character) {
    //updates guessedLetters
    self.guessedLetters.append(charInput)
    
    //updates numberOfIncorrectGuesses
    if targetWord.contains(charInput) == false {
        self.numberOfIncorrectGuesses += 1
    }
    
    //prints out the current display version of the word
    self.printDisplayVersionOfWord()
    
    //prints out the number of incorrect guesses
    print("Number of wrong guesses: \(self.numberOfIncorrectGuesses)\n")
    
    //prints out if the play has won
    if playerWon() {
        print("Congratulations! You won!")
    }
}
```
