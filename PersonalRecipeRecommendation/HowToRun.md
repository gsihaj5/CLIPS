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

```

### 2. RecommendRecipe
rules RecommendRecipe akan digunakan untuk menentukan
resep yang cocok untuk user berdasarkan inputnya

*IF* the user preferences match with recipes *THEN*
recommend the recipe

### 3. ExitRecommendation
hanya rules untuk memberi kata penutup saja
