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



