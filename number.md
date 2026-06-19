
# Number

The `Number` type in Crystal is actually a hierarchy of numeric types. All numbers inherit from `Number`, which is a subclass of `Value`. The two main categories are integers and floating-point numbers.

## Integer Types

Crystal provides signed and unsigned integers in various sizes.

| Type | Signed | Size (bits) | Range |
|------|--------|-------------|-------|
| `Int8` | Yes | 8 | -128 to 127 |
| `Int16` | Yes | 16 | -32,768 to 32,767 |
| `Int32` | Yes | 32 | -2,147,483,648 to 2,147,483,647 |
| `Int64` | Yes | 64 | -9,223,372,036,854,775,808 to 9,223,372,036,854,775,807 |
| `Int128` | Yes | 128 | -1.7e38 to 1.7e38 |
| `UInt8` | No | 8 | 0 to 255 |
| `UInt16` | No | 16 | 0 to 65,535 |
| `UInt32` | No | 32 | 0 to 4,294,967,295 |
| `UInt64` | No | 64 | 0 to 18,446,744,073,709,551,615 |
| `UInt128` | No | 128 | 0 to 3.4e38 |

---

## Floating Point Types

| Type | Size (bits) | Precision |
|------|-------------|-----------|
| `Float32` | 32 | Single precision |
| `Float64` | 64 | Double precision |

---

## Number Literals

### Integers

```crystal
123      # Int32
123_i8   # Int8
123_u16  # UInt16
1_000_000 # underscores for readability (Int32)
0x7F     # hexadecimal (Int32)
0o177    # octal (Int32)
0b1010   # binary (Int32)
```

Floats

```crystal
1.23     # Float64
1.23_f32 # Float32
1.5e-10  # scientific notation
```

---

API Reference

#+

Adds two numbers.

```crystal
number + other : Number
```

```crystal
1 + 2   # => 3
1.5 + 2 # => 3.5
```

---

#-

Subtracts two numbers.

```crystal
number - other : Number
```

```crystal
5 - 3   # => 2
5.5 - 2 # => 3.5
```

---

#*

Multiplies two numbers.

```crystal
number * other : Number
```

```crystal
3 * 4   # => 12
3.5 * 2 # => 7.0
```

---

#/

Divides two numbers. Always returns a Float64 or Float32 if either operand is a float.

```crystal
number / other : Number
```

```crystal
10 / 3   # => 3.3333333333333335 (Float64)
10 / 2   # => 5.0
10.0 / 3 # => 3.3333333333333335
```

---

#//

Performs integer division. Returns an integer.

```crystal
number // other : Int
```

```crystal
10 // 3 # => 3
10 // 2 # => 5
```

Raises DivisionByZeroError if other is zero.

---

#%

Returns the remainder of division.

```crystal
number % other : Number
```

```crystal
10 % 3 # => 1
10 % 2 # => 0
```

Raises DivisionByZeroError if other is zero.

---

#**

Raises a number to a power.

```crystal
number ** exponent : Number : Number
```

```crystal
2 ** 3  # => 8
3 ** 2  # => 9
```

---

#abs

Returns the absolute value.

```crystal
number.abs : Number
```

```crystal
-5.abs # => 5
5.abs  # => 5
-3.5.abs # => 3.5
```

---

#abs2

Returns the square of the absolute value.

```crystal
number.abs2 : Number
```

```crystal
-5.abs2 # => 25
3.abs2  # => 9
```

---

#positive?

Returns true if the number is greater than zero.

```crystal
number.positive? : Bool
```

```crystal
5.positive?  # => true
0.positive?  # => false
-5.positive? # => false
```

---

#negative?

Returns true if the number is less than zero.

```crystal
number.negative? : Bool
```

```crystal
-5.negative? # => true
0.negative?  # => false
5.negative?  # => false
```

---

#zero?

Returns true if the number equals zero.

```crystal
number.zero? : Bool
```

```crystal
0.zero?  # => true
5.zero?  # => false
0.0.zero? # => true
```

---

#even?

Returns true if the integer is even.

```crystal
number.even? : Bool
```

```crystal
2.even? # => true
3.even? # => false
```

---

#odd?

Returns true if the integer is odd.

```crystal
number.odd? : Bool
```

```crystal
3.odd? # => true
2.odd? # => false
```

---

#floor

Returns the largest integer less than or equal to the number.

```crystal
number.floor : Number
```

```crystal
3.9.floor # => 3
3.0.floor # => 3
-3.1.floor # => -4
```

---

#ceil

Returns the smallest integer greater than or equal to the number.

```crystal
number.ceil : Number
```

```crystal
3.1.ceil # => 4
3.0.ceil # => 3
-3.1.ceil # => -3
```

---

#round

Rounds to the nearest integer.

```crystal
number.round : Number
number.round(decimals : Int) : Number
```

```crystal
3.5.round # => 4
3.4.round # => 3
3.14159.round(2) # => 3.14
```

---

#truncate

Truncates the decimal part.

```crystal
number.truncate : Number
number.truncate(decimals : Int) : Number
```

```crystal
3.9.truncate # => 3
-3.9.truncate # => -3
3.14159.truncate(2) # => 3.14
```

---

#to_i

Converts a number to an integer.

```crystal
number.to_i : Int32
number.to_i8 : Int8
number.to_i16 : Int16
number.to_i32 : Int32
number.to_i64 : Int64
number.to_i128 : Int128
```

```crystal
3.9.to_i # => 3
3.0.to_i # => 3
```

---

#to_f

Converts a number to a float.

```crystal
number.to_f : Float64
number.to_f32 : Float32
number.to_f64 : Float64
```

```crystal
3.to_f # => 3.0
```

---

#to_s

Converts a number to a string.

```crystal
number.to_s : String
```

```crystal
123.to_s # => "123"
3.14.to_s # => "3.14"
```

---

#to_s(base : Int)

Converts a number to a string in the given base.

```crystal
number.to_s(base : Int) : String
```

```crystal
255.to_s(16) # => "ff"
8.to_s(2)    # => "1000"
```

---

#to_i(base : Int)

Parses a string as an integer in the given base and returns an integer.

```crystal
String.to_i(base : Int) : Int32
```

```crystal
"ff".to_i(16) # => 255
"1000".to_i(2) # => 8
```

---

#clamp

Clamps a number between a minimum and maximum value.

```crystal
number.clamp(min, max) : Number
```

```crystal
5.clamp(1, 10) # => 5
15.clamp(1, 10) # => 10
0.clamp(1, 10) # => 1
```

---

#step

Yields a sequence of numbers from the current number to a limit.

```crystal
number.step(limit, step = 1) { |n| ... } : Nil
number.step(limit, step = 1) : Iterator(Number)
```

```crystal
1.step(5) { |n| puts n } # prints 1, 2, 3, 4, 5
1.step(10, 2) { |n| puts n } # prints 1, 3, 5, 7, 9
```

---

Comparison Operators

#==

Returns true if two numbers are equal.

```crystal
number == other : Bool
```

```crystal
3 == 3 # => true
3 == 4 # => false
```

---

#!=

Returns true if two numbers are not equal.

```crystal
number != other : Bool
```

```crystal
3 != 3 # => false
3 != 4 # => true
```

---

#>

Returns true if the number is greater than the other.

```crystal
number > other : Bool
```

```crystal
5 > 3 # => true
3 > 5 # => false
```

---

#<

Returns true if the number is less than the other.

```crystal
number < other : Bool
```

```crystal
3 < 5 # => true
5 < 3 # => false
```

---

#>=

Returns true if the number is greater than or equal to the other.

```crystal
number >= other : Bool
```

```crystal
5 >= 3 # => true
5 >= 5 # => true
3 >= 5 # => false
```

---

#<=

Returns true if the number is less than or equal to the other.

```crystal
number <= other : Bool
```

```crystal
3 <= 5 # => true
5 <= 5 # => true
5 <= 3 # => false
```

---

#<=>

Returns -1, 0, or 1 depending on the comparison.

```crystal
number <=> other : Int32?
```

```crystal
3 <=> 5 # => -1
5 <=> 3 # => 1
5 <=> 5 # => 0
```

---

Constants

Int#MIN

Minimum value of the integer type.

```crystal
Int32::MIN # => -2147483648
Int8::MIN  # => -128
```

---

Int#MAX

Maximum value of the integer type.

```crystal
Int32::MAX # => 2147483647
Int8::MAX  # => 127
```

---

Float#INFINITY

Represents infinity.

```crystal
Float64::INFINITY # => Infinity
```

---

Float#NAN

Represents "Not a Number".

```crystal
Float64::NAN # => NaN
```

---

Important Notes

- Integer division with / returns a float.
- Use // for integer division.
- Overflow behavior depends on the integer type.
- Floats can represent Infinity, -Infinity, and NaN.
- Type inference in Crystal handles numeric literals intelligently.

```
```
