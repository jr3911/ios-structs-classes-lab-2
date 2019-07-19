# Structs and Classes Lab - 2


## Question 1

Using the Room struct below, write code that demonstrates that it is a value type.

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

```swift
class Bike {
    var wheelNumber = 2
    var hasBell = false
}

var bikeA = Bike()
var bikeB = bikeA
print(bikeA.hasBell)    //prints false
print(bikeB.hasBell)    //prints false

bikeA.hasBell = true

print(bikeA.hasBell)    //prints true
print(bikeB.hasBell)    //print true

```

## Question 3

a. Given the Animal class below, create a Bird subclass with a new `canFly` property.

```swift
class Animal {
    var name: String = ""
    func printDescription() {
        print("I am an animal named \(name)")
    }
}

class Bird: Animal {
    var canFly: Bool = true
    override func printDescription() {
        print("I am a \(name) and my ability to fly is \(canFly)")
    }
}

class Robin: Bird {
    override var name: String {
        get {
            return "Robin"
        } 
        set {
            super.name = newValue
        }
    }
}
```

b. Override the printDescription method to have the instance of the Bird object print out its name and whether it can fly

```swift
class Bird: Animal {
    var canFly: Bool = true
    override func printDescription() {
        print("I am a \(name) and my ability to fly is \(canFly)")
    }
}
```
c. Create a Robin subclass of Bird.  Its name should always be "Robin".

```swift
class Robin: Bird {
    override var name: String {
        get {
            return "Robin"
        } 
        set {
            super.name = newValue
        }
    }
}
```


## Question 4

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


## Question 5

a. Given the Point object below, complete the `distance method` so that it returns the distance between a given point.

The equation for the distance formula can be found [here](https://www.mathsisfun.com/algebra/distance-2-points.html).

`sqrt` is a method in Swift that gives the square root.  Make sure to have `import Foundation` or `import UIKit` to use this method.

```swift
struct Point {
    let x: Double
    let y: Double
    func distance(to point: Point) -> Double {
        let a = self.x - point.x
        let b = self.y - point.y
        return sqrt(pow(a, 2) + pow(b, 2))
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
        if point.distance(to: center) <= radius {
            return true
        } else {
            return false
        }
    }
    
    func getRandomPoint() -> Point {
        let x = Double(Int.random(in: Int(self.center.x)...Int(self.center.x + self.radius)))
        let y = Double(Int.random(in: Int(self.center.y)...Int(self.center.y + self.radius)))
        let randomPoint = Point(x: x, y: y)
        return randomPoint
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

Hint: Given the radius of a circle and the x value of a point on the circle, the y value of the point is defined by:

```
√(r^2) - (x^2)
```

```swift
func getRandomPoint() -> Point {
    let x = Double(Int.random(in: Int(self.center.x)...Int(self.center.x + self.radius)))
    let y = Double(Int.random(in: Int(self.center.y)...Int(self.center.y + self.radius)))
    let randomPoint = Point(x: x, y: y)
    return randomPoint
}
circleOne.contains(circleOne.getRandomPoint()) //Should always be true
```


## Question 6

a. Create a struct called HangmanModel with 3 properties `targetWord: String`, `numberOfIncorrectGuesses: Int` and `guessedLetters: [Character]`.

b. Add a method called `playerWon` that returns whether all of the characters in `targetWord` are in `guessedLetters`

var model = HangmanModel()
model.targetWord = "hello"
model.guessedLetters = ["h","e","o","l"]
model.playerWon() //true

c. Add a method called `printDisplayVersionOfWord` that prints the `targetWord` replacing characters that are not in `guessedLetters` with "_"

var model = HangmanModel()
model.targetWord = "hello"
model.guessedLetters = ["h","l"]
model.printDisplayVersionOfWord()
//prints h_ll_

d. Add a method called `guess(_:)` that takes in a character as input, and updates `guessedLetters` and `numberOfIncorrectGuesses` as appropriate.

var model = HangmanModel()
model.targetWord = "hello"
model.guess("h")
model.guess("a")
model.guessedLetters // ["h", "a"]
model.numberOfIncorrectGuesses // 1

e. Have `guess(_:)` also print out the current display version of the word, the number of incorrect guesses and if the player has won.

```swift
struct HangmanModel {
    var targetWord: String = String()
    var numberOfIncorrectGuesses: Int = Int()
    var guessedLetters: [Character] = [Character]()

    func playerWon() -> Bool {
        let setTargetWord = Set(targetWord)
        for char in setTargetWord {
            if guessedLetters.contains(char) == true {
                continue
            } else {
                return false
            }
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
