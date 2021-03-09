# Deeper Into Go

<br>

## Variable Declarations

<br>

```Go
package main

func main() {
	// var card string = "Ace of Spades"
	card := "Ace of Spades"
}
```

<br>

```Go
var card string = "Ace of Spades"
```

* ```var``` // We're about to create a new variable
* ```card``` // The name of the variable will be `card`
* ```string``` // Only a "string" will ever be assigned to this variable <br>
= <br>
* ```"Ace of Spades"``` // Assign the value "Ace of Spades" to this variabl

#

<br>
<br>
<br>

## Basic Go Types

<br>

| Type | Example |
| - | - |
| bool | true, false |
| string | "Hello", "World" |
| int | 0, -10000, 99999 |
| float64 | 10,000001, 0.00009, -100.003 |

#

<br>
<br>
<br>

## Basic Go Function Structure

<br>

```Go
func newCard() string {

}
```

* ```newCard``` // Define a function called 'newCard'
* ```string``` // When executed, this function will return a value of type 'string' 

<br>

```Go
func newCard() int {

}
```

#

<br>
<br>
<br>

## Arrays & Slices

<br>

* ```Array``` // Fixed length list of things
* ```Slice``` // An array that can grow or shrink

<br>

```Go
package main

import (
    "fmt"
)

func main() {
    cards := []string{"Ace of Diamonds", newCard()}
    cards = append(cards, "Six of Spades")

    fmt.Println(cards)
}

func newCard() string {
    return "Five of Diamonds"
}
```

#

<br>
<br>
<br>

## Iterating of Arrays/Slices Using Range

<br>

```Go
package main

import (
    "fmt"
)

func main() {
    cards := []string{"Ace of Diamonds", newCard()}
    cards = append(cards, "Six of Spades")

    fmt.Println(cards)

    for index, value := range cards {
        fmt.Println(index, value)
    }
}

func newCard() string {
    return "Five of Diamonds"
}
```

<br>

```Go
for index, card := range cards {
    fmt.Println(card)
}
```

<br>

* ```index``` // index of this element in the array
* ```card``` // Current card we're iterating over
* ```range cards``` // Take the slice of 'cards' and loop over it
* ```fmt.Println(card)``` // Run this one time for each card in the slice

#

<br>
<br>
<br>

##

<br>

#

<br>
<br>
<br>

##

<br>

#

<br>
<br>
<br>

##

<br>

#

<br>
<br>
<br>

##

<br>

#

<br>
<br>
<br>

##

<br>

#

<br>
<br>
<br>

##

<br>

#

<br>
<br>
<br>

##

<br>

#

<br>
<br>
<br>

##

<br>

#

<br>
<br>
<br>

##

<br>

#

<br>
<br>
<br>

##

<br>

#

<br>
<br>
<br>

##

<br>

#

<br>
<br>
<br>

##

<br>

#

<br>
<br>
<br>

##

<br>

#

<br>
<br>
<br>

##

<br>

#

<br>
<br>
<br>

##

<br>

#

<br>
<br>
<br>

##

<br>

#

<br>
<br>
<br>

##

<br>

#

<br>
<br>
<br>

##

<br>

#

<br>
<br>
<br>

##

<br>

#

<br>
<br>
<br>

##

<br>

#

<br>
<br>
<br>