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

## Custom Type

<br>

```Go
package main

import (
    "fmt"
)

type deck []string

func main() {
    cards := deck{"King of Hearts"}
    fmt.Println(cards)
}
```

#

<br>
<br>
<br>

## Function Receivers

<br>

```Go
func (d deck) print() {
    for index, card := range d {
        fmt.Println(index, card)
    }
}
```

<br>

* ```d``` // The actual copy of the deck we're working with is available in the function as a variable called 'd'
* ```deck``` // Every variable of type 'deck' can call this function on itself

<br>

* main.go
```Go
package main

func main() {
    cards := deck{}
    cards = append(cards, "Two of Hearts", "King of Hearts", aceOfHearts())
}

func aceOfHearts() string {
    return "Ace of Hearts"
}
```

<br>

* deck.go
```Go
package main

type deck []string

func (d deck) print() {
    for index, card := range d {
        fmt.Println(index, card)
    }
}
```

#

<br>
<br>
<br>

## Slice Range Syntax

<br>

```Go
package main

import (
	"fmt"
)

func main() {
	exampleSlice := []int{1, 2, 3, 4, 5, 6, 7, 8, 9}
	fmt.Println(exampleSlice[:3]) 
    fmt.Println(exampleSlice[2:5])
    fmt.Println(exampleSlice[5:])
    fmt.Println(exampleSlice[:5])
}
```
#

<br>
<br>
<br>

## Multiple Return Values

<br>

* main.go
```Go
package main

import "fmt"

func main() {
	cards := newDeck()
	// cards.print()

	hand, remainingCards := deal(cards, 25)

	fmt.Println("-----")
	hand.print()
	fmt.Println("-----")
	remainingCards.print()
	fmt.Println("-----")
}
```

<br>

* deck.go
```Go
package main

import "fmt"

type deck []string

func newDeck() deck {
	cards := deck{}
	cardSuits := []string{"Spades", "Hearts", "Diamonds", "Clubs"}
	cardValues := []string{"Ace", "Two", "Three", "Four", "Five", "Six", "Seven", "Eight", "Nine", "Ten", "Jack", "Queen", "King"}

	for i := 0; i < len(cardSuits); i++ {
		for j := 0; j < len(cardValues); j++ {
			cards = append(cards, cardValues[j]+" of "+cardSuits[i])
		}
	}

	return cards
}

func (d deck) print() {
	for index, card := range d {
		fmt.Println(index, card)
	}
}

func deal(d deck, handSize int) (deck, deck) {
	return d[:handSize], d[handSize:]
}
```

#

<br>
<br>
<br>

## Type Conversion

<br>

```Go
[]byte("Hi there!")
```

<br>

```[]byte``` // Type we want
```("Hi there!")``` // Value we have

<br>

```Go
package main

func main() {
    greeting := "Hi there!"
    fmt.Println([]byte(greeting))
}
```

<br>

* main.go
```Go
package main

import "fmt"

func main() {
	cards := newDeck()
	// cards.print()

	fmt.Println(cards.toString())
}
```

<br>

* deck.go
```Go
package main

import (
	"fmt"
	"strings"
)

type deck []string

func newDeck() deck {
	cards := deck{}
	cardSuits := []string{"Spades", "Hearts", "Diamonds", "Clubs"}
	cardValues := []string{"Ace", "Two", "Three", "Four", "Five", "Six", "Seven", "Eight", "Nine", "Ten", "Jack", "Queen", "King"}

	for i := 0; i < len(cardSuits); i++ {
		for j := 0; j < len(cardValues); j++ {
			cards = append(cards, cardValues[j]+" of "+cardSuits[i])
		}
	}

	return cards
}

func (d deck) print() {
	for index, card := range d {
		fmt.Println(index, card)
	}
}

func deal(d deck, handSize int) (deck, deck) {
	return d[:handSize], d[handSize:]
}

func (d deck) toString() string {
	return strings.Join([]string(d), ",")
}
```

#

<br>
<br>
<br>

## Save to File

<br>

```Go
func WriteFile(filename string, data []byte, perm os.FileMode) error
```

<br>

* main.go
```Go
package main

func main() {
	cards := newDeck()
	// cards.print()
	cards.saveToFile("myCards.md")
}

```

<br>

* deck.go
```Go
package main

import (
	"fmt"
	"io/ioutil"
	"strings"
)

type deck []string

func newDeck() deck {
	cards := deck{}
	cardSuits := []string{"Spades", "Hearts", "Diamonds", "Clubs"}
	cardValues := []string{"Ace", "Two", "Three", "Four", "Five", "Six", "Seven", "Eight", "Nine", "Ten", "Jack", "Queen", "King"}

	for i := 0; i < len(cardSuits); i++ {
		for j := 0; j < len(cardValues); j++ {
			cards = append(cards, cardValues[j]+" of "+cardSuits[i])
		}
	}

	return cards
}

func (d deck) print() {
	for index, card := range d {
		fmt.Println(index, card)
	}
}

func deal(d deck, handSize int) (deck, deck) {
	return d[:handSize], d[handSize:]
}

func (d deck) toString() string {
	return strings.Join([]string(d), ",")
}

func (d deck) saveToFile(filename string) error {
	return ioutil.WriteFile(filename, []byte(d.toString()), 0666)
}
```
#

<br>
<br>
<br>

## ReadFile

<br>

```Go
func ReadFile(filename string) ([]byte, error)
```

<br>

```Go
byteSlice, err := ioutil.ReadFile(filename)
```

<br>

```err``` // Value of type 'error'. If nothing went wrong, it will have a value of 'nil'

<br>

* main.go
```Go
package main

func main() {
	cards := newDeckFromFile("myCards.md")
	// cards.print()
	cards.print()
}
```

<br>

```Go
package main

import (
	"fmt"
	"io/ioutil"
	"os"
	"strings"
)

type deck []string

func newDeck() deck {
	cards := deck{}
	cardSuits := []string{"Spades", "Hearts", "Diamonds", "Clubs"}
	cardValues := []string{"Ace", "Two", "Three", "Four", "Five", "Six", "Seven", "Eight", "Nine", "Ten", "Jack", "Queen", "King"}

	for i := 0; i < len(cardSuits); i++ {
		for j := 0; j < len(cardValues); j++ {
			cards = append(cards, cardValues[j]+" of "+cardSuits[i])
		}
	}

	return cards
}

func (d deck) print() {
	for index, card := range d {
		fmt.Println(index, card)
	}
}

func deal(d deck, handSize int) (deck, deck) {
	return d[:handSize], d[handSize:]
}

func (d deck) toString() string {
	return strings.Join([]string(d), ",")
}

func (d deck) saveToFile(filename string) error {
	return ioutil.WriteFile(filename, []byte(d.toString()), 0666)
}

func newDeckFromFile(filename string) deck {
	bs, err := ioutil.ReadFile(filename)
	if err != nil {
		// Option #1 - Log the error and return a call to newDeck()
		// Option #2 - Log the error and entirely quit the program
		fmt.Println("Error:", err)
		os.Exit(1)
	}
	s := strings.Split(string(bs), ",")
	return deck(s)
}
```

#

<br>
<br>
<br>

## Shuffle a Deck

<br>

* main.go
```Go
package main

func main() {
	cards := newDeck()
	// cards.print()
	cards.shuffle()
	cards.print()
}
```

<br>

* deck.go
```Go
package main

import (
	"fmt"
	"io/ioutil"
	"math/rand"
	"os"
	"strings"
	"time"
)

type deck []string

func newDeck() deck {
	cards := deck{}
	cardSuits := []string{"Spades", "Hearts", "Diamonds", "Clubs"}
	cardValues := []string{"Ace", "Two", "Three", "Four", "Five", "Six", "Seven", "Eight", "Nine", "Ten", "Jack", "Queen", "King"}

	for i := 0; i < len(cardSuits); i++ {
		for j := 0; j < len(cardValues); j++ {
			cards = append(cards, cardValues[j]+" of "+cardSuits[i])
		}
	}

	return cards
}

func (d deck) print() {
	for index, card := range d {
		fmt.Println(index, card)
	}
}

func deal(d deck, handSize int) (deck, deck) {
	return d[:handSize], d[handSize:]
}

func (d deck) toString() string {
	return strings.Join([]string(d), ",")
}

func (d deck) saveToFile(filename string) error {
	return ioutil.WriteFile(filename, []byte(d.toString()), 0666)
}

func newDeckFromFile(filename string) deck {
	bs, err := ioutil.ReadFile(filename)
	if err != nil {
		// Option #1 - Log the error and return a call to newDeck()
		// Option #2 - Log the error and entirely quit the program
		fmt.Println("Error:", err)
		os.Exit(1)
	}
	s := strings.Split(string(bs), ",")
	return deck(s)
}

func (d deck) shuffle() {
	source := rand.NewSource(time.Now().UnixNano())
	r := rand.New(source)

	for i := range d {
		newPosition := r.Intn(len(d) - 1)
		d[i], d[newPosition] = d[newPosition], d[i]
	}
}
```

#

<br>
<br>
<br>

## Testing With Go

<br>

* main.go
```Go
package main

func main() {
	cards := newDeck()
	// cards.print()
	cards.shuffle()
	cards.print()
}
```

<br>

* deck.go

```Go
package main

import (
	"fmt"
	"io/ioutil"
	"math/rand"
	"os"
	"strings"
	"time"
)

type deck []string

func newDeck() deck {
	cards := deck{}
	cardSuits := []string{"Spades", "Hearts", "Diamonds", "Clubs"}
	cardValues := []string{"Ace", "Two", "Three", "Four", "Five", "Six", "Seven", "Eight", "Nine", "Ten", "Jack", "Queen", "King"}

	for i := 0; i < len(cardSuits); i++ {
		for j := 0; j < len(cardValues); j++ {
			cards = append(cards, cardValues[j]+" of "+cardSuits[i])
		}
	}

	return cards
}

func (d deck) print() {
	for index, card := range d {
		fmt.Println(index, card)
	}
}

func deal(d deck, handSize int) (deck, deck) {
	return d[:handSize], d[handSize:]
}

func (d deck) toString() string {
	return strings.Join([]string(d), ",")
}

func (d deck) saveToFile(filename string) error {
	return ioutil.WriteFile(filename, []byte(d.toString()), 0666)
}

func newDeckFromFile(filename string) deck {
	bs, err := ioutil.ReadFile(filename)
	if err != nil {
		// Option #1 - Log the error and return a call to newDeck()
		// Option #2 - Log the error and entirely quit the program
		fmt.Println("Error:", err)
		os.Exit(1)
	}
	s := strings.Split(string(bs), ",")
	return deck(s)
}

func (d deck) shuffle() {
	source := rand.NewSource(time.Now().UnixNano())
	r := rand.New(source)

	for i := range d {
		newPosition := r.Intn(len(d) - 1)
		d[i], d[newPosition] = d[newPosition], d[i]
	}
}
```

<br>

* deck_test.go
```Go
package main

import (
	"os"
	"testing"
)

func TestNewDeck(t *testing.T) {
	d := newDeck()

	if len(d) != 52 {
		t.Errorf("Expected length of 52, but got %v", len(d))
	}

	if d[0] != "Ace of Spades" {
		t.Errorf("Expected first card of Ace of Spades, but got %v", d[0])
	}

	if d[len(d)-1] != "King of Clubs" {
		t.Errorf("Expected last card of Four of Clubs, but got %v", d[len(d)-1])
	}

}

func TestSaveToDeckAndNewDeckFromFile(t *testing.T) {
	os.Remove("_decktesting")

	deck := newDeck()
	deck.saveToFile("_decktesting")

	loadedDeck := newDeckFromFile("_decktesting")

	if len(loadedDeck) != 52 {
		t.Errorf("Expected 52 cards in deck, got %v", len(loadedDeck))
	}

	os.Remove("_decktesting")
}
```

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