
# Symbol

A `Symbol` represents an immutable, interned string. Symbols are used as lightweight identifiers, often for keys in hashes or as enum-like values.

---

## API Reference

### `#to_s`

Returns the string representation of the symbol.

```crystal
symbol.to_s : String
```

```crystal
:hello.to_s # => "hello"
:name.to_s  # => "name"
```

---

#inspect

Returns a string representation of the symbol with a colon prefix.

```crystal
symbol.inspect : String
```

```crystal
:hello.inspect # => ":hello"
:name.inspect  # => ":name"
```

---

#==

Returns true if two symbols are equal (compared by identity).

```crystal
symbol == other : Bool
```

```crystal
:hello == :hello   # => true
:hello == :world   # => false
:hello == "hello"  # => false
```

---

#hash

Returns the hash code of the symbol.

```crystal
symbol.hash : Int32
```

```crystal
:hello.hash # => some integer value
```

---

#to_s

Converts the symbol to a string. The result is the symbol's name without the colon.

```crystal
symbol.to_s : String
```

```crystal
:hello.to_s # => "hello"
```

---

#to_sym

Returns the symbol itself (idempotent).

```crystal
symbol.to_sym : Symbol
```

```crystal
:hello.to_sym # => :hello
```

---

#inspect

Returns the symbol with a colon prefix, suitable for debugging.

```crystal
symbol.inspect : String
```

```crystal
:hello.inspect # => ":hello"
```

---

#empty?

Returns true if the symbol is empty.

```crystal
symbol.empty? : Bool
```

```crystal
:empty?.empty?   # => false
:"".empty?       # => true
```

---

#size

Returns the number of characters in the symbol's name.

```crystal
symbol.size : Int32
```

```crystal
:hello.size # => 5
:name.size  # => 4
```

---

#length

Alias for #size.

```crystal
symbol.length : Int32
```

```crystal
:hello.length # => 5
```

---

#bytesize

Returns the number of bytes in the symbol's name.

```crystal
symbol.bytesize : Int32
```

```crystal
:hello.bytesize # => 5
```

---

#starts_with?

Returns true if the symbol's name starts with the given prefix.

```crystal
symbol.starts_with?(prefix : String) : Bool
symbol.starts_with?(prefix : Char) : Bool
```

```crystal
:hello.starts_with?("he") # => true
:hello.starts_with?('h')  # => true
:hello.starts_with?("ab") # => false
```

---

#ends_with?

Returns true if the symbol's name ends with the given suffix.

```crystal
symbol.ends_with?(suffix : String) : Bool
symbol.ends_with?(suffix : Char) : Bool
```

```crystal
:hello.ends_with?("lo") # => true
:hello.ends_with?('o')  # => true
:hello.ends_with?("ab") # => false
```

---

#includes?

Returns true if the symbol's name contains the given substring.

```crystal
symbol.includes?(substring : String) : Bool
symbol.includes?(char : Char) : Bool
```

```crystal
:hello.includes?("ell") # => true
:hello.includes?('e')   # => true
:hello.includes?("xyz") # => false
```

---

#upcase

Returns a new symbol with the name converted to uppercase.

```crystal
symbol.upcase : Symbol
```

```crystal
:hello.upcase # => :HELLO
```

---

#downcase

Returns a new symbol with the name converted to lowercase.

```crystal
symbol.downcase : Symbol
```

```crystal
:HELLO.downcase # => :hello
```

---

#capitalize

Returns a new symbol with the first character capitalized.

```crystal
symbol.capitalize : Symbol
```

```crystal
:hello.capitalize # => :Hello
```

---

#reverse

Returns a new symbol with the name reversed.

```crystal
symbol.reverse : Symbol
```

```crystal
:hello.reverse # => :olleh
```

---

#camelcase

Returns a new symbol converted to CamelCase.

```crystal
symbol.camelcase : Symbol
```

```crystal
:hello_world.camelcase # => :HelloWorld
:helloWorld.camelcase  # => :HelloWorld
```

---

#underscore

Returns a new symbol converted to snake_case.

```crystal
symbol.underscore : Symbol
```

```crystal
:HelloWorld.underscore # => :hello_world
:helloWorld.underscore # => :hello_world
```

---

#dasherize

Returns a new symbol with underscores replaced by dashes.

```crystal
symbol.dasherize : Symbol
```

```crystal
:hello_world.dasherize # => :hello-world
```

---

#to_s

Alias for #to_s.

```crystal
symbol.to_s : String
```

---

#inspect

Alias for #inspect.

```crystal
symbol.inspect : String
```

---

Important Notes

- Symbols are unique and interned. :hello always refers to the same object.
- Symbols are immutable.
- Symbols are often used as hash keys for performance reasons.
- Symbols are not garbage collected (they exist for the lifetime of the program).
- Use symbols for identifiers, not for storing user input.
- Symbols can be created dynamically with String#to_sym.

```crystal
"hello".to_sym # => :hello
```

```
```
