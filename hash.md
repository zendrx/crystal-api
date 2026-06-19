
# Hash

The `Hash` class represents a collection of key-value pairs. Keys must be unique and are used to retrieve their associated values.

---

## API Reference

### `.new`

Creates a new empty hash.

```crystal
Hash.new : Hash(K, V)
Hash.new(default_value : V) : Hash(K, V)
Hash.new { |hash, key| ... } : Hash(K, V)
```

```crystal
Hash.new                     # => {}
Hash.new(0)                  # => {} (returns 0 for missing keys)
Hash.new { |h, k| h[k] = 0 } # => {} (sets missing keys to 0)
```

---

#[]

Returns the value associated with a key.

```crystal
hash[key : K] : V
```

```crystal
hash = {"name" => "Alice", "age" => 30}
hash["name"] # => "Alice"
hash["age"]  # => 30
```

Raises KeyError if the key does not exist.

---

#[]?

Same as #[] but returns nil if the key does not exist.

```crystal
hash[key : K]? : V?
```

```crystal
hash = {"name" => "Alice"}
hash["name"]? # => "Alice"
hash["age"]?  # => nil
```

---

#[]=

Assigns a value to a key.

```crystal
hash[key : K] = value : V) : V
```

```crystal
hash = {} of String => Int32
hash["age"] = 30
hash # => {"age" => 30}
```

---

#fetch

Returns the value for a key, or the default value if the key does not exist.

```crystal
hash.fetch(key : K) : V
hash.fetch(key : K, default : V) : V
hash.fetch(key : K) { |key| ... } : V
```

```crystal
hash = {"name" => "Alice"}
hash.fetch("name")            # => "Alice"
hash.fetch("age", 0)          # => 0
hash.fetch("age") { 0 }       # => 0
hash.fetch("age")             # raises KeyError
```

---

#has_key?

Returns true if the key exists.

```crystal
hash.has_key?(key : K) : Bool
```

```crystal
hash = {"name" => "Alice"}
hash.has_key?("name") # => true
hash.has_key?("age")  # => false
```

---

#has_value?

Returns true if the value exists.

```crystal
hash.has_value?(value : V) : Bool
```

```crystal
hash = {"name" => "Alice"}
hash.has_value?("Alice") # => true
hash.has_value?("Bob")   # => false
```

---

#keys

Returns an array of all keys.

```crystal
hash.keys : Array(K)
```

```crystal
hash = {"name" => "Alice", "age" => 30}
hash.keys # => ["name", "age"]
```

---

#values

Returns an array of all values.

```crystal
hash.values : Array(V)
```

```crystal
hash = {"name" => "Alice", "age" => 30}
hash.values # => ["Alice", 30]
```

---

#each

Iterates over each key-value pair.

```crystal
hash.each(&block : K, V -> ) : self
```

```crystal
hash = {"name" => "Alice", "age" => 30}
hash.each { |key, value| puts "#{key}: #{value}" }
# name: Alice
# age: 30
```

---

#each_key

Iterates over each key.

```crystal
hash.each_key(&block : K -> ) : self
```

```crystal
hash = {"name" => "Alice", "age" => 30}
hash.each_key { |key| puts key }
# name
# age
```

---

#each_value

Iterates over each value.

```crystal
hash.each_value(&block : V -> ) : self
```

```crystal
hash = {"name" => "Alice", "age" => 30}
hash.each_value { |value| puts value }
# Alice
# 30
```

---

#map

Returns a new array with the results of applying a block to each key-value pair.

```crystal
hash.map(&block : K, V -> U) : Array(U)
```

```crystal
hash = {"a" => 1, "b" => 2}
hash.map { |key, value| value * 2 } # => [2, 4]
```

---

#select

Returns a new hash containing only key-value pairs for which the block returns true.

```crystal
hash.select(&block : K, V -> Bool) : Hash(K, V)
```

```crystal
hash = {"a" => 1, "b" => 2, "c" => 3}
hash.select { |key, value| value > 1 } # => {"b" => 2, "c" => 3}
```

---

#select!

Modifies the hash to contain only key-value pairs for which the block returns true.

```crystal
hash.select!(&block : K, V -> Bool) : self?
```

Returns nil if no changes were made.

```crystal
hash = {"a" => 1, "b" => 2, "c" => 3}
hash.select! { |key, value| value > 1 }
hash # => {"b" => 2, "c" => 3}
```

---

#reject

Returns a new hash containing key-value pairs for which the block returns false.

```crystal
hash.reject(&block : K, V -> Bool) : Hash(K, V)
```

```crystal
hash = {"a" => 1, "b" => 2, "c" => 3}
hash.reject { |key, value| value > 1 } # => {"a" => 1}
```

---

#reject!

Modifies the hash to contain only key-value pairs for which the block returns false.

```crystal
hash.reject!(&block : K, V -> Bool) : self?
```

Returns nil if no changes were made.

```crystal
hash = {"a" => 1, "b" => 2, "c" => 3}
hash.reject! { |key, value| value > 1 }
hash # => {"a" => 1}
```

---

#merge

Returns a new hash with the contents of another hash merged in.

```crystal
hash.merge(other : Hash(K, V)) : Hash(K, V)
hash.merge(other : Hash(K, V)) { |key, old_value, new_value| ... } : Hash(K, V)
```

```crystal
hash1 = {"a" => 1, "b" => 2}
hash2 = {"b" => 3, "c" => 4}
hash1.merge(hash2)                        # => {"a" => 1, "b" => 3, "c" => 4}
hash1.merge(hash2) { |key, old, new| old + new } # => {"a" => 1, "b" => 5, "c" => 4}
```

---

#merge!

Merges another hash into the current hash.

```crystal
hash.merge!(other : Hash(K, V)) : self
hash.merge!(other : Hash(K, V)) { |key, old_value, new_value| ... } : self
```

```crystal
hash = {"a" => 1, "b" => 2}
hash.merge!({"b" => 3, "c" => 4})
hash # => {"a" => 1, "b" => 3, "c" => 4}
```

---

#delete

Deletes the key-value pair for a specific key.

```crystal
hash.delete(key : K) : V?
hash.delete(key : K) { |key| ... } : V
```

```crystal
hash = {"a" => 1, "b" => 2}
hash.delete("a")      # => 1
hash                  # => {"b" => 2}
hash.delete("c") { 0 } # => 0
```

---

#delete_if

Deletes key-value pairs for which the block returns true.

```crystal
hash.delete_if(&block : K, V -> Bool) : self
```

```crystal
hash = {"a" => 1, "b" => 2, "c" => 3}
hash.delete_if { |key, value| value > 1 }
hash # => {"a" => 1}
```

---

#empty?

Returns true if the hash has zero key-value pairs.

```crystal
hash.empty? : Bool
```

```crystal
{}.empty?     # => true
{"a" => 1}.empty? # => false
```

---

#size

Returns the number of key-value pairs in the hash.

```crystal
hash.size : Int32
```

```crystal
{"a" => 1, "b" => 2}.size # => 2
```

---

#clear

Removes all key-value pairs from the hash.

```crystal
hash.clear : self
```

```crystal
hash = {"a" => 1, "b" => 2}
hash.clear
hash # => {}
```

---

#invert

Returns a new hash with keys and values swapped.

```crystal
hash.invert : Hash(V, K)
```

```crystal
hash = {"a" => 1, "b" => 2}
hash.invert # => {1 => "a", 2 => "b"}
```

---

#to_s

Returns a string representation of the hash.

```crystal
hash.to_s : String
```

```crystal
hash = {"a" => 1, "b" => 2}
hash.to_s # => "{\"a\" => 1, \"b\" => 2}"
```

---

#inspect

Returns a string representation of the hash showing internal structure.

```crystal
hash.inspect : String
```

```crystal
hash = {"a" => 1, "b" => 2}
hash.inspect # => "{\"a\" => 1, \"b\" => 2}"
```

---

#to_h

Returns the hash itself.

```crystal
hash.to_h : Hash(K, V)
```

```crystal
hash = {"a" => 1, "b" => 2}
hash.to_h # => {"a" => 1, "b" => 2}
```

---

Important Notes

- Hashes are mutable and grow dynamically.
- Keys must be unique. If you assign a value to an existing key, it overwrites the previous value.
- Key types must support #hash and #== (most built-in types do).
- The order of insertion is preserved (since Crystal 1.0).
- Use #fetch over #[] when you want to handle missing keys gracefully.
- The ! suffix indicates an in-place mutation.
