
# Bool

The `Bool` class represents a boolean value: either `true` or `false`. It is a fundamental type used in conditionals, loops, and logical operations.

---

## API Reference

### `#!`

Returns the logical negation of the boolean.

```crystal
bool.! : Bool
```

```crystal
!true  # => false
!false # => true
```

---

#&

Returns the logical AND of two booleans.

```crystal
bool & other : Bool : Bool
```

```crystal
true & true   # => true
true & false  # => false
false & true  # => false
false & false # => false
```

---

#|

Returns the logical OR of two booleans.

```crystal
bool | other : Bool : Bool
```

```crystal
true | true   # => true
true | false  # => true
false | true  # => true
false | false # => false
```

---

#^

Returns the logical XOR (exclusive OR) of two booleans.

```crystal
bool ^ other : Bool : Bool
```

```crystal
true ^ true   # => false
true ^ false  # => true
false ^ true  # => true
false ^ false # => false
```

---

#==

Returns true if two booleans are equal.

```crystal
bool == other : Bool
```

```crystal
true == true   # => true
true == false  # => false
false == false # => true
```

---

#!=

Returns true if two booleans are not equal.

```crystal
bool != other : Bool
```

```crystal
true != true   # => false
true != false  # => true
false != false # => false
```

---

#to_s

Converts a boolean to a string.

```crystal
bool.to_s : String
```

```crystal
true.to_s  # => "true"
false.to_s # => "false"
```

---

#to_i

Converts a boolean to an integer.

```crystal
bool.to_i : Int32
```

```crystal
true.to_i  # => 1
false.to_i # => 0
```

---

#to_u8

Converts a boolean to an unsigned 8-bit integer.

```crystal
bool.to_u8 : UInt8
```

```crystal
true.to_u8  # => 1_u8
false.to_u8 # => 0_u8
```

---

Important Notes

- Bool is a Value type, meaning it's immutable and passed by value.
- Logical operators && and || are control-flow operators that short-circuit, while &, |, and ^ are bitwise operators that always evaluate both operands.

```crystal
true && false   # => false (short-circuits)
true & false    # => false (evaluates both)
```

- Use && and || in conditionals for better performance and readability.
- true and false are the only instances of Bool.

```
```
