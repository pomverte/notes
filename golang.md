# Golang

## En résumé

- langage compilé
- statiquement typé
- permet de générer des binaires autoportant multi-plateformes
- version 1.17.5
- première version en 10 novembre 2009
- créé par Google

## Installation

```
$ brew install go
```

## Initialisation

```
$ mkdir my_project
$ go mod init my_project
```

## Hello, World !

```go
// main.go
package main

import "fmt"

func main() {
   fmt.Println("Hello, world !")
}
```

```
$ go run main.go
```

## Variables

```go
var x int
x = 2

var x int = 2

//inférence de type
y := 2

// z vaut 0 (zero value)
var z int
```

## Typage

string, int (...), bool

## Opérateur

- arithmétique : `+ - / * ^ %`
- logique : `== != >= <= && ||`

https://golang.org/ref/spec#Operators

## Condition

```go
if x == 0 {
    // ...
} else if {
    // ...
}
```

## Boucle

```go
for i := 0; i < 3; i++ {
    // ...
}
```

```go
i := 0
for i < 3 {
    i++
}
```

```go
i := 0
for {
    if i >= 3 {
        break
    }
    i++
}
```

```go
i := 0
for ; i < 3; i++ {
    if i %2 == 1 {
        continue
    }
    fmt.Println(x)
}
```

## Tableau

### Array

```go
var myList [2]int
myList[0] = 10
myList[1] = 20

// déclaration par inférence
myList := [...]int{10, 20}

for k, v := range myList {
    fmt.Printf("The value %d is at position number %d\n", v, k)
}

for _, v := range myList { // on n'utilise pas k => _
    fmt.Println(v)
}
```
### Slice

"Tableau de taille dynamique"

```go
var sli []int

for i := 0; i < 3; i++ {
    sli = append(sli, i)
}
```

## Map

```go
myMap := map[string]int{
    "un": 1,
    "deux": 2,
}
fmt.Println(myMap["deux"])

result, found := myMap["trois"]    // wtf, ça me renvoie "0, false" !
```

## Fonction

```go
func hello(name string) {
    fmt.Println("Hello %v !", name)
}

func getFullName(firstName, lastName string) string {
    return firstName + " " + lastName
}
```

## Fonction anonyme

anonymous, nameless function

```go
x := func hello(name string) {
    fmt.Println("Hello %v !", name)
}()


y := func heya(name string) {
    fmt.Println("HEYA !!!")
}
y()
```

## Gestion d’erreur

```go
func getFullName(firstName, lastName string) (string, error) {
    if firstName == "" || lastName == "" {
        return "", errors.New("firstName/lastName empty ?")
   }
   return firstName + " " + lastName, nil
}
```

"C'est d'la merde", Karadoc

## Pointeur

```go
var i int = 12
var p *int                // pointeur

p = &i                    // référence à une adresse mémoire

fmt.Println("%v",*p)    // déréférencement
```

## Type structure

```go
type octo struct {
    poly   string
    tribu  string
    niveau int
}

var o1 octo
o2 := octo{"HVLE", "OPS", 3}
o3 := octo{poly: "NVO", niveau: 3, tribu: "OPS"}
o4 := new(octo) // pointeur
```

## Type alias

```go
type Entier = int
var x Entier
```

## User defined Type

```go
type entier int

var x entier = 2
var y int

y = entier(x) // casting
```

## Function with receiver

On propose une fonction à un objet (qui reçoit la fonction)

```go
func (u *user) aging(years int) {
   // u est le receiver
   // aging est l'identifier de la fonction
   // si on ne met pas le pointeur, Go fait une copie de l’objet
   u.age += years
}
u.aging(15)
```

## Interface

Définition de comportement

```go
type printable interface {
   toto() string
}

// tout objet qui implémente une fonction toto
// et retourne une string sera de type printable
func (u user) toto() string {
   return "toto"
}
```

## pass by value
