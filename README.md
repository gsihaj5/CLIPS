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




