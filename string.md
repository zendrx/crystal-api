
# String

The `String` class represents a sequence of characters. Strings are immutable and use UTF-8 encoding.

---

## API Reference

### `.new`

Creates a new String from bytes or another string.

```crystal
String.new(bytes) : String
```

Creates a String from a slice of bytes, assuming valid UTF-8 encoding.

```crystal
bytes = Slice(UInt8).new(5) { |i| ('a'.ord + i).to_u8 }
String.new(bytes) # => "abcde"
```

---

#size

Returns the number of bytes in the string. This is equivalent to #bytesize.

```crystal
string.size : Int32
```

```crystal
"Hello".size   # => 5
"😊".size      # => 4 (4 bytes in UTF-8)
```

---

#length

Returns the number of Unicode characters in the string.

```crystal
string.length : Int32
```

```crystal
"Hello".length   # => 5
"😊".length      # => 1
```

---

#bytesize

Returns the number of bytes in the string.

```crystal
string.bytesize : Int32
```

```crystal
"Hello".bytesize # => 5
"😊".bytesize    # => 4
```

---

#[]

Accesses a character or substring at a given index or range.

```crystal
string[index : Int] : Char
string[start : Int, count : Int] : String
string(range : Range(Int, Int)) : String
```

Returns a Char when given a single integer index, or a String substring when given a range or start and count.

```crystal
str = "Hello"
str[0]      # => 'H'
str[-1]     # => 'o'
str[0, 2]   # => "He"
str[1..3]   # => "ell"
```

Raises IndexError if the index is out of bounds.

---

#[]?

Same as #[] but returns nil if the index is out of bounds instead of raising.

```crystal
string[index : Int]? : Char?
string[start : Int, count : Int]? : String?
string(range : Range(Int, Int))? : String?
```

```crystal
str = "Hello"
str[0]?  # => 'H'
str[5]?  # => nil
```

---

#empty?

Returns true if the string has zero length.

```crystal
string.empty? : Bool
```

```crystal
"".empty?      # => true
"Hello".empty? # => false
```

---

#blank?

Returns true if the string is empty or contains only whitespace characters.

```crystal
string.blank? : Bool
```

Whitespace characters include space, tab, newline, carriage return, and others.

```crystal
"".blank?      # => true
"   ".blank?   # => true
"Hello".blank? # => false
```

---

#includes?

Returns true if the string contains the given substring or character.

```crystal
string.includes?(substring : String) : Bool
string.includes?(char : Char) : Bool
```

```crystal
"Hello".includes?("ell") # => true
"Hello".includes?('e')   # => true
"Hello".includes?("xyz") # => false
```

---

#starts_with?

Returns true if the string starts with the given prefix.

```crystal
string.starts_with?(prefix : String) : Bool
```

```crystal
"Hello".starts_with?("He")   # => true
"Hello".starts_with?("ell")  # => false
```

---

#ends_with?

Returns true if the string ends with the given suffix.

```crystal
string.ends_with?(suffix : String) : Bool
```

```crystal
"Hello".ends_with?("lo")   # => true
"Hello".ends_with?("ell")  # => false
```

---

#index

Returns the index of the first occurrence of a substring or character.

```crystal
string.index(substring : String) : Int32?
string.index(char : Char) : Int32?
```

Returns nil if not found.

```crystal
"Hello".index("ell") # => 1
"Hello".index('e')   # => 1
"Hello".index("xyz") # => nil
```

---

#rindex

Returns the index of the last occurrence of a substring or character.

```crystal
string.rindex(substring : String) : Int32?
string.rindex(char : Char) : Int32?
```

```crystal
"Hello Hello".rindex("Hello") # => 6
"Hello".rindex('e')           # => 1
```

---

#upcase

Returns a new string with all characters converted to uppercase.

```crystal
string.upcase : String
```

```crystal
"Hello".upcase # => "HELLO"
```

---

#downcase

Returns a new string with all characters converted to lowercase.

```crystal
string.downcase : String
```

```crystal
"Hello".downcase # => "hello"
```

---

#capitalize

Returns a new string with the first character capitalized and the rest lowercase.

```crystal
string.capitalize : String
```

```crystal
"hello".capitalize # => "Hello"
"HELLO".capitalize # => "Hello"
```

---

#reverse

Returns a new string with the characters in reverse order.

```crystal
string.reverse : String
```

```crystal
"Hello".reverse # => "olleH"
```

---

#strip

Returns a new string with leading and trailing whitespace removed.

```crystal
string.strip : String
```

```crystal
"  Hello  ".strip # => "Hello"
```

---

#lstrip

Returns a new string with leading whitespace removed.

```crystal
string.lstrip : String
```

```crystal
"  Hello  ".lstrip # => "Hello  "
```

---

#rstrip

Returns a new string with trailing whitespace removed.

```crystal
string.rstrip : String
```

```crystal
"  Hello  ".rstrip # => "  Hello"
```

---

#chomp

Returns a new string with a trailing newline removed, if present.

```crystal
string.chomp : String
```

```crystal
"Hello\n".chomp # => "Hello"
"Hello".chomp   # => "Hello"
```

---

#split

Splits the string into an array of substrings.

```crystal
string.split(delimiter : String) : Array(String)
string.split(delimiter : Char) : Array(String)
string.split : Array(String)
```

With no arguments, splits on whitespace.

```crystal
"apple,banana".split(",")     # => ["apple", "banana"]
"a b c".split                 # => ["a", "b", "c"]
```

---

#join

Joins an array of strings using the string as a separator.

```crystal
string.join(items : Array(String)) : String
```

```crystal
", ".join(["apple", "banana"]) # => "apple, banana"
```

---

#gsub

Returns a new string with all occurrences replaced.

```crystal
string.gsub(pattern : String, replacement : String) : String
string.gsub(pattern : Regex, replacement : String) : String
```

```crystal
"Hello World".gsub("World", "Crystal") # => "Hello Crystal"
"hello hello".gsub("hello", "hi")      # => "hi hi"
```

---

#sub

Returns a new string with only the first occurrence replaced.

```crystal
string.sub(pattern : String, replacement : String) : String
string.sub(pattern : Regex, replacement : String) : String
```

```crystal
"hello hello".sub("hello", "hi") # => "hi hello"
```

---

#scan

Returns an array of matches for a regular expression.

```crystal
string.scan(pattern : Regex) : Array(Regex::MatchData)
```

```crystal
"hello 123 world 456".scan(/\d+/).map(&.[0]) # => ["123", "456"]
```

---

#each_char

Iterates over each character in the string.

```crystal
string.each_char(&block : Char -> ) : Nil
```

```crystal
"Hello".each_char { |c| puts c }
# H
# e
# l
# l
# o
```

---

#each_byte

Iterates over each byte in the string.

```crystal
string.each_byte(&block : UInt8 -> ) : Nil
```

```crystal
"Hello".each_byte { |b| puts b }
# 72
# 101
# 108
# 108
# 111
```

---

#to_slice

Returns the string's bytes as a Slice(UInt8).

```crystal
string.to_slice : Slice(UInt8)
```

```crystal
"Hello".to_slice # => Bytes[72, 101, 108, 108, 111]
```

---

#to_s

Returns the string itself.

```crystal
string.to_s : String
```

---

#inspect

Returns a string with escaped characters.

```crystal
string.inspect : String
```

```crystal
"Hello\nWorld".inspect # => "Hello\nWorld" (shows escape sequences)
```

---

Class Methods

String.build

Efficiently builds a string using a block.

```crystal
String.build(capacity : Int = 64) { |io| ... } : String
```

```crystal
str = String.build do |io|
  io << "Hello"
  io << " "
  io << "World"
end
# => "Hello World"
```

---

Important Notes

- Strings are immutable. All transformation methods return new strings.
- Strings use UTF-8 encoding and are Unicode-aware.
- #size and #bytesize are equivalent – both return bytes.
- #length returns the number of Unicode characters.
- Indexing uses byte offsets, not character offsets. For Unicode-safe indexing, use #each_char or #char_at.
