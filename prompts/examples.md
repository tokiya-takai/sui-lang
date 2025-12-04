# Sui Code Generation Examples

## Example Prompts and Expected Outputs

### Example 1: Simple Loop

**Prompt:**
```
Generate Sui code that prints numbers from 1 to 10
```

**Expected Output:**
```sui
= v0 1
: 0
> v1 v0 10
? v1 1
. v0
+ v0 v0 1
@ 0
: 1
```

---

### Example 2: Sum of Array

**Prompt:**
```
Generate Sui code that creates an array [1,2,3,4,5] and calculates the sum
```

**Expected Output:**
```sui
[ g0 5
{ g0 0 1
{ g0 1 2
{ g0 2 3
{ g0 3 4
{ g0 4 5
= g1 0
= v0 0
: 0
< v1 v0 5
! v2 v1
? v2 1
] v3 g0 v0
+ g1 g1 v3
+ v0 v0 1
@ 0
: 1
. g1
```

---

### Example 3: Factorial

**Prompt:**
```
Generate Sui code for factorial function and calculate 5!
```

**Expected Output:**
```sui
# 0 1 {
< v0 a0 2
! v1 v0
? v1 1
^ 1
: 1
- v2 a0 1
$ v3 0 v2
* v4 a0 v3
^ v4
}
= g0 5
$ g1 0 g0
. g1
```

---

### Example 4: Find Maximum

**Prompt:**
```
Generate Sui code that finds the maximum value in array [3, 7, 2, 9, 1]
```

**Expected Output:**
```sui
[ g0 5
{ g0 0 3
{ g0 1 7
{ g0 2 2
{ g0 3 9
{ g0 4 1
] g1 g0 0
= v0 1
: 0
< v1 v0 5
! v2 v1
? v2 1
] v3 g0 v0
> v4 v3 g1
! v5 v4
? v5 2
= g1 v3
: 2
+ v0 v0 1
@ 0
: 1
. g1
```

---

### Example 5: Prime Check

**Prompt:**
```
Generate Sui code for a function that checks if a number is prime
```

**Expected Output:**
```sui
# 0 1 {
< v0 a0 2
? v0 1
= v1 2
: 0
* v2 v1 v1
> v3 v2 a0
? v3 2
% v4 a0 v1
~ v5 v4 0
? v5 1
+ v1 v1 1
@ 0
: 2
^ 1
: 1
^ 0
}
= g0 17
$ g1 0 g0
. g1
```

---

## Few-Shot Prompt Template

Use this template for consistent code generation:

```
You are a Sui code generator. Here are examples:

Task: Print "Hello"
Code:
. "Hello"

Task: Add 5 and 3, print result
Code:
= v0 5
= v1 3
+ v2 v0 v1
. v2

Task: [YOUR TASK HERE]
Code:
```

---

## Common Patterns

### If-Else Pattern
```sui
; if (condition) { A } else { B }
< v0 [condition]
! v1 v0
? v1 else_label
[A code]
@ end_label
: else_label
[B code]
: end_label
```

### While Loop Pattern
```sui
; while (condition) { body }
: start_label
< v0 [condition]
! v1 v0
? v1 end_label
[body]
@ start_label
: end_label
```

### For Loop Pattern
```sui
; for i in range(n)
= v0 0
: start_label
< v1 v0 n
! v2 v1
? v2 end_label
[body using v0 as i]
+ v0 v0 1
@ start_label
: end_label
```

### Function Pattern
```sui
; def func(arg):
;     return result
# func_id arg_count {
[body]
^ result
}
```

### Python FFI Pattern
```sui
; Call Python function
P result "module.func" arg1 arg2

; Math
P v0 "math.sqrt" 16
P v1 "math.pow" 2 10

; Builtins
P v2 "len" "hello"
P v3 "abs" -42
P v4 "max" 1 2 3

; Random
P v5 "random.randint" 1 100

; Type conversion
P v6 "int" "123"
P v7 "float" "3.14"
P v8 "str" 42
```

