# Recipe Recommendator

## 1. TEMPLATE
Sebelum membuat program rekomendasi kita harus
mendeklarasikan model-model yang terkait

ada 2 template atau model yang terlibat 
1. User
1. Recipe

```jess
(deftemplate Recipe
   (slot name)
   (slot cuisine)
   (slot difficulty)
   (slot ingredients)
   (slot instructions)
)

(deftemplate User
   (slot name)
   (slot cuisine-preference)
   (slot difficulty-preference)
   (slot ingredient-preference)
)
```

## 2. RULES
setelah membuat preferences, rules yang akan terlibat
dalam konteks ini adalah

### 1. GetUserPreferences -> untuk menerima input user
apa syarat untuk menerima user input ?

syarat nya adalah -> tidak ada fakta user di dalam kumpulan fakta

*IF* there is no user *THEN* get input

``` jess
(defrule GetUserPreferences
    (not (User (name ?name)))
    =>
    ; inputs for user
    (printout t "insert your name !")
    (bind ?name (read))
    (printout t "Welcome, " ?name ". Let's find you a recipe!" crlf)
    (printout t "What cuisine do you prefer? ")
    (bind ?cuisine-pref (read))
    (printout t "How difficult should the recipe be? (Easy, Intermediate, Difficult) ")
    (bind ?difficulty-pref (read))
    (printout t "Do you have any specific ingredient preferences? ")
    (bind ?ingredient-pref (read))
    ; create new user fact
    (assert (User 
        (name ?name)
        (difficulty-preference ?difficulty-pref)
        (cuisine-preference ?cuisine-pref)
        (ingredient-preference ?ingredient-pref)
    ))
)
```

### 2. RecommendRecipe
rules RecommendRecipe akan digunakan untuk menentukan
resep yang cocok untuk user berdasarkan inputnya

*IF* the user preferences match with recipes *THEN*
recommend the recipe

``` jess
(defrule RecommendRecipe
    (User 
        (name ?name)
        (cuisine-preference ?cuisine-pref)
        (difficulty-preference ?difficulty-pref)
        (ingredient-preference ?ingredient-pref)
    )
    (Recipe 
        (name ?recipe)
        (cuisine ?cuisine)
        (difficulty ?difficulty)
        (ingredients ?ingredients)
    )
    (test (eq ?cuisine ?cuisine-pref))
    (test (eq ?difficulty ?difficulty-pref))
    (test (str-compare ?ingredients ?ingredient-pref))
    =>
    (printout t "Based on your preferences, we recommend: " ?recipe crlf)
    (printout t "Ingredients: " ?ingredients crlf)
    (printout t "Enjoy your meal!" crlf)
    ;(retract (User (name ?name)))
    ;(retract (Recipe (name ?recipe)))
)
```

### 3. ExitRecommendation
hanya rules untuk memberi kata penutup saja
