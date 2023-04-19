# Emerging JavaScript

## Declaring Variables in ES6
- const
- let
- template strings
  ```JavaScript
  const lastName = "Ferrell"
  const middleName = "William"
  const firstName = "John"

  // string concatenation
  console.log(lastName + ", " + firstName + " " + middleName)
  // ES6 template strings
  console.log(`${lastName}, ${firstName} ${middleName}`)
  ```
## Default Parameters
## Arrow functions
- Regular Function
  ```JavaScript
  // Regular Function

  var lordify = function(firstname) {
    return `${firstname} of Canterbury`
  }

  console.log( lordify("Dale") )
  console.log( lordify("Daryle") )
  ```
- Arrow Function
  ```JavaScript
  // Arrow Function

  var lordify = firstname => `${firstname} of Canterbury`

  console.log( lordify("Dana") )
  console.log( lordify("Daphne") )
  ```
- Arrow Function - Multiple Args
  ```JavaScript
  // Arrow Function

  var lordify = (firstName, land) => `${firstName} of ${land}`

  console.log( lordify("Debbie", "Texas") )
  console.log( lordify("Daphne", "Susanville") )
  ```
- Multiple Args - One Line
  ```JavaScript
  // Arrow Function

  var lordify = (firstName, land) => `${firstName} of ${land}`

  console.log( lordify("Debbie", "Texas") )
  console.log( lordify("Daphne", "Susanville") )
  ```
- setTimeout with .bind
   ```JavaScript
   // Function Solution with bind
  var tahoe = {
    resorts: ["Kirkwood","Squaw","Alpine","Heavenly","Northstar"],
    print: function(delay=1000) {

      setTimeout(function() {
        console.log(this.resorts.join(","))
      }.bind(this), delay)

    }
  }

  tahoe.print()
   ```
- setTimeout with Arrow Function
  ```JavaScript
  // Arrow Function
  var tahoe = {
    resorts: ["Kirkwood","Squaw","Alpine","Heavenly","Northstar"],
    print: function(delay=1000) {

      setTimeout(
        () => console.log(this.resorts.join(",")),
        delay
      )

    }
  }

  tahoe.print()
   ```
- Showing 'this' problem
  ```JavaScript
  // Arrow Functions know when to use them.
  var tahoe = {
    resorts: ["Kirkwood","Squaw","Alpine","Heavenly","Northstar"],
    print: function(delay=1000) {

      setTimeout(() => {
        console.log(this === window)
      }, delay)

    }
  }

  tahoe.print(); // true
  ```

## Objects and Arrays
- Destructuring Assignment
  ```JavaScript
  // Destructuring Assignment

  var sandwich =  {
        bread: "dutch crunch",
        meat: "tuna",
        cheese: "swiss",
        toppings: ["lettuce", "tomato", "mustard"]
  }

  var {bread, meat} = sandwich

  console.log(bread, meat)

  bread = "garlic"
  meat = "turkey"

  console.log(bread,meat)
  console.log(sandwich.bread, sandwich.meat)
  ```
- Destructuring with Arguments
  ```JavaScript
  // Function with object arguments

  var lordify = regularPerson => {
    console.log(`${regularPerson.firstname} of Canterbury`)
  }

  var regularPerson = {
    firstname: "Bill",
    lastname: "Wilson"
  }

  lordify(regularPerson)
  ```
- Destructured Object Arguments
  ```JavaScript
  // Destructuring object arguments

  var lordify = ({firstname}) =>
    console.log(`${firstname} of canterbury`)

  var regularPerson = {
    firstname: "Dale",
    lastname: "Smith"
  }

  lordify(regularPerson)
  ```
- Destructuring Arrays
  ```JavaScript
  // Destructuring Arrays

  var [firstResort] = ["Kirkwood", "Squaw", "Alpine"]

  console.log(firstResort)
  ```
- Destructuring with Comma Placeholders
  ```JavaScript
  // More Array Destructuring

  var [,,thirdResort] = ["Kirkwood", "Squaw", "Alpine"]

  console.log(thirdResort)
  ```

## Object Literal Enhancement
- Object Literal Enhancement
  ```JavaScript
  // Literal Enhancements

  var name = "Tallac"
  var elevation = 9738

  var funHike = { name,elevation }

  console.log(funHike)
  ```
- Object Literal Enhancements with Functions
  ```JavaScript
  // Literal Enhancements with functions

  var name = "Tallac"
  var elevation = 9738
  var print = function() {
    console.log(`Mt. ${this.name} is ${this.elevation} feet tall`)
  }

  var funHike = { name,elevation,print }

  funHike.print()
  ```
- Literal Enhancements: The Old Way
  ```JavaScript
  // Object literals... the old way
  var name = "Léo Taillefer"
  var sound = "Kahh"

  var skier = {
    name: name,
    sound: sound,
    powderYell: function() {
    var yell = this.sound.toUpperCase()
    console.log(`${yell} ${yell} ${yell}!!!`)
  },
    speed: function(mph) {
      this.speed = mph
      console.log('speed:', mph)
    }
  }

  skier.powderYell()
  skier.speed("hair on fire")
  console.log(JSON.stringify(skier))
  ```
- Literal Enhancements Now
  ```JavaScript
  // Object literal enhancements

  var name = "Julia Mancuso"
  var sound = "go fast"

  const skier = {
    name,
    sound,
    powderYell() {
      let yell = this.sound.toUpperCase()
      console.log(`${yell} ${yell} ${yell}!!!`)
    },
    speed(mph) {
      this.speed = mph
      console.log('speed:', mph)
    }
  }

  skier.powderYell()
  skier.speed(350)
  console.log(JSON.stringify(skier))
  ```

## The Spread Operator
- Spread Operator with Arrays
  ```JavaScript
  // Spread Operator

  var peaks = ["Tallac", "Ralston", "Rose"]
  var canyons = ["Ward", "Blackwood"]
  var tahoe = [...peaks, ...canyons]

  console.log(tahoe.join(', '))
  ```

- Array Destructuring with .reverse()
  ```JavaScript
  // .reverse() mutates the peaks array

  var peaks = ["Tallac", "Ralston", "Rose"]
  var [last] = peaks.reverse()

  console.log(last)
  console.log(peaks.join(', '))
  ```

- Spread Operator with Destructuring and .reverse()
  ```JavaScript
  // duplicate peaks with spread and revers the duplicate

  var peaks = ["Tallac", "Ralston", "Rose"]
  var [last] = [...peaks].reverse()

  console.log(last) // Rose
  console.log(peaks.join(', '))
  ```

- Destructuring and the Spread Operator
  ```JavaScript
  // Destructuring with the spread operator

  var lakes = ["Donner", "Marlette", "Fallen Leaf", "Cascade"]

  var [first, ...rest] = lakes

  console.log(rest.join(", "))
  ```

- Directions Functions
  ```JavaScript
  // Convert arguments to an array with the spread operator
  //    pick an array apart with spreads

  function directions(...args) {
    var [start, ...remaining] = args
    var [finish, ...stops] = remaining.reverse()

    console.log(`drive through ${args.length} towns`)
    console.log(`start in ${start}`)
    console.log(`the destination is ${finish}`)
    console.log(`stopping ${stops.length} times in between`)
  }

  directions("Truckee", "Tahoe City", "Sunnyside", "Homewood", "Tahoma")
  ```

- Spread Operator with Objects
  ```JavaScript
  // Spread operator works with objects too

  var morning = {
    breakfast: "oatmeal",
    lunch: "peanut butter and jelly"
  }

  var dinner = "mac and cheese"

  var backpackingMeals = {
    ...morning,
    dinner
  }

  console.log(backpackingMeals)
  ```

## Promises
- getFakeMembers
```JavaScript
const getFakeMembers = count => new Promise((resolves, rejects) => {
  const api = `https://api.randomuser.me/?nat=US&results=${count}`
  const request = new XMLHttpRequest()
  request.open('GET', api)
  request.onload = () =>
       (request.status === 200) ?
        resolves(JSON.parse(request.response).results) :
        reject(Error(request.statusText))
  request.onerror = (err) => rejects(err)
  request.send()
})

getFakeMembers(5).then(
  members => console.log(members),
  err => console.error(
      new Error("cannot load members from randomuser.me"))
)
```
- fetch members
```JavaScript
fetch("https://api.randomuser.me/?nat=US&results=10")
  .then(response => response.json())
  .then(members => console.log(members))
  .catch(err => console.error(err))
```

## ES6 Class Syntax
- The Constructor and the Prototype
  ```JavaScript
  // Constructor and the prototype, the old way

  function Vacation(destination, length) {
    this.destination = destination
    this.length = length
  }

  Vacation.prototype.print = function() {
      console.log(this.destination + " will take " + this.length + " days")
  }

  var maui = new Vacation("Maui", 7)

  maui.print()
  ```
- Classes
  ```JavaScript
  // The new way... with classes

  class Vacation {

    constructor(destination, length) {
      this.destination = destination
      this.length = length
    }

    print() {
      console.log(`${this.destination} will take ${this.length} days.`)
    }

  }

  const trip = new Vacation("Santiago, Chile", 9)

  trip.print()
  ```
- Class Inheritance
  ```JavaScript
  // Inheritance

  class Vacation {

    constructor(destination, length) {
      this.destination = destination
      this.length = length
    }

    print() {
      console.log(`${this.destination} will take ${this.length} days.`)
    }

  }

  class Expedition extends Vacation {

    constructor(destination, length, gear) {
    super(destination, length)
    this.gear = gear
    }

    print() {
      super.print()
      console.log(`bring your ${this.gear.join(" and your ")}`)
    }
  }

  const trip = new Expedition(
    "Mt. Whitney",
    3,
    ["sunglasses", "prayer flags", "camera"]
  )

  trip.print()
  ```