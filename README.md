# CLIPS 

`(exit)` shutdown

`(clear)` clear rules and facts

`(reset)` removes facts but not rules

`(run)` start execute

### Facts

facts declaration 
`(assert (colour green))`

every assert create a fact `<Fact-0>`, the number will increment

facts retract -> cancel a fact

`(retract 0)`

this means retracting facts at index 0


`(facts)` to list all facts inserted

### Rules

`(rules)` to list all rules inserted

```
(defrule duck
    (animal-is duck)
    =>
    (assert (sound-is quack))
)
```

`defrule duck` -> duck is rules name

`animal-is duck` -> similar to IF 'if duck bla bla bla'

`=>` -> then

`assert (sound-is quack)` -> this is the action taken if the condition true


try run the program using `(run)`

nothing will appear, but the there is new facts. 
check it out with `(facts)`

### chaining rules

we already have the `duck` rules

now add 1 more rules 
```
(defrule is-it-a-duck
    (animal-has webbed-feet)
    (animal-has feathers)
    =>
    (assert (animal-is duck))
)
```

try `(reset)` the facts to restart. 

now assert 2 facts the `webbed-feet` and `feathers`

after run there should be 4 facts

from this examples we know that this program producing facts
and governed by rules.


### print out something !

redeclare the rules and try it on your own!

```
(defrule duck
    (animal-is duck)
    =>
    (assert (sound-is quack))
    (printout t "it’s a duck" crlf)
)
```

## Persistent facts

with this we can always get the same fact even after reset

`(deffacts startup (animal dog) (animal duck) (animal haddock))`

now populate facts with more facts

```
(deffacts startup (animal dog) (animal cat) (animal duck) (animal turtle) (warm-blooded dog) (warm-blooded cat)
(warm-blooded duck) (lays-eggs duck) (lays-eggs turtle) (child-of dog puppy) (child-of cat kitten)
(child-of turtle hatchling))
```

### wild cards

```
(defrule animal
(animal ?)
=>
(printout t "animal found" crlf))
```
those wildcards can be used to check multiple condition

try and run it

### variables

while utilizing wild card add identifier to declare it as variables

`?name`

while calling `?name` again it will act as variables

calling rules and get the facts

first rules

```
(defrule mammal
(animal ?name)
(warm-blooded ?name)
(not (lays-eggs ?name))
=>
(assert (mammal ?name))
(printout t ?name " is a mammal" crlf))
```

second rule
```
(defrule remove-mammals
?fact <- (mammal ?)
=>
(printout t "retracting " ?fact crlf)
(retract ?fact))
```

on this second rule, the result from `mammals` rule is injected to a variable called `?fact`


### logic and math

```
(defrule take-umbrella
(or (weather raining)
(weather snowing))
=>
(assert (umbrella required)))
```

math ...

```
(+ 5 7) -> 12

(- 5 7) -> -2

(* 5 7) -> 35

(/5 7) -> 0.714...
```

### user input

it will prompt user to input if there is `read` keyword

```
(defrule what-is-child
(animal ?name)
(not (child-of ?name ?))
=>
(printout t "What do you call the child of a " ?name "?")
(assert (child-of ?name (read))))
```

multi wild cards `$?`

multi-field variables `$?members`

assigning value to variables `bind ?total (+ ?x ?y)`

all these variables are local

this is global variable
```
(defglobal
?*var1* = 17
?*oranges* = "seven"
)
```



