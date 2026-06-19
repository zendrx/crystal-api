
# Array

The `Array` class represents an ordered collection of elements. Arrays can hold any type of value and automatically resize as needed.

---

## API Reference

### `.new`

Creates a new empty array or an array with a given size and initial value.

```crystal
Array.new : Array(T)
Array.new(size : Int, value : T) : Array(T)
Array.new(size : Int, &block : Int32 -> T) : Array(T)
```

```crystal
Array.new                   # => []
Array.new(3, "hello")       # => ["hello", "hello", "hello"]
Array.new(3) { |i| i * 2 }  # => [0, 2, 4]
```

---

#size

Returns the number of elements in the array.

```crystal
array.size : Int32
```

```crystal
[1, 2, 3].size # => 3
[].size         # => 0
```

---

#empty?

Returns true if the array has zero elements.

```crystal
array.empty? : Bool
```

```crystal
[].empty?     # => true
[1, 2].empty? # => false
```

---

#[]

Accesses an element at a given index or range.

```crystal
array[index : Int] : T
array[start : Int, count : Int] : Array(T)
array(range : Range(Int, Int)) : Array(T)
```

Returns a single element when given an integer index, or a new Array when given a range or start and count.

```crystal
arr = [1, 2, 3, 4, 5]
arr[0]     # => 1
arr[-1]    # => 5
arr[0, 3]  # => [1, 2, 3]
arr[1..3]  # => [2, 3, 4]
```

Raises IndexError if the index is out of bounds.

---

#[]?

Same as #[] but returns nil if the index is out of bounds.

```crystal
array[index : Int]? : T?
```

```crystal
arr = [1, 2, 3]
arr[0]? # => 1
arr[5]? # => nil
```

---

#[]=

Assigns a value to a specific index.

```crystal
array[index : Int] = value : T) : T
```

```crystal
arr = [1, 2, 3]
arr[1] = 99
arr # => [1, 99, 3]
```

Raises IndexError if the index is out of bounds.

---

#<<

Appends a value to the end of the array.

```crystal
array << value : T) : self
```

```crystal
arr = [1, 2]
arr << 3
arr # => [1, 2, 3]
```

---

#push

Appends one or more values to the end of the array.

```crystal
array.push(value : T, *values : T) : self
```

```crystal
arr = [1, 2]
arr.push(3, 4, 5)
arr # => [1, 2, 3, 4, 5]
```

---

#pop

Removes and returns the last element.

```crystal
array.pop : T
array.pop(count : Int) : Array(T)
```

Returns the last element when called with no arguments, or an array of the last count elements.

```crystal
arr = [1, 2, 3]
arr.pop    # => 3
arr        # => [1, 2]
arr.pop(2) # => [1, 2]
arr        # => []
```

Raises IndexError if the array is empty.

---

#unshift

Adds a value to the beginning of the array.

```crystal
array.unshift(value : T) : self
```

```crystal
arr = [2, 3]
arr.unshift(1)
arr # => [1, 2, 3]
```

---

#shift

Removes and returns the first element.

```crystal
array.shift : T
array.shift(count : Int) : Array(T)
```

```crystal
arr = [1, 2, 3]
arr.shift    # => 1
arr          # => [2, 3]
arr.shift(2) # => [2, 3]
arr          # => []
```

Raises IndexError if the array is empty.

---

#insert

Inserts a value at a specific index.

```crystal
array.insert(index : Int, value : T) : self
```

```crystal
arr = [1, 3]
arr.insert(1, 2)
arr # => [1, 2, 3]
```

Raises IndexError if the index is out of bounds.

---

#delete

Deletes all occurrences of a value.

```crystal
array.delete(value : T) : T?
```

```crystal
arr = [1, 2, 3, 2, 4]
arr.delete(2)
arr # => [1, 3, 4]
```

---

#delete_at

Deletes the element at a specific index.

```crystal
array.delete_at(index : Int) : T
```

```crystal
arr = [1, 2, 3]
arr.delete_at(1)
arr # => [1, 3]
```

Raises IndexError if the index is out of bounds.

---

#clear

Removes all elements from the array.

```crystal
array.clear : self
```

```crystal
arr = [1, 2, 3]
arr.clear
arr # => []
```

---

#each

Iterates over each element in the array.

```crystal
array.each(&block : T -> ) : self
```

```crystal
[1, 2, 3].each { |n| puts n }
# 1
# 2
# 3
```

---

#each_with_index

Iterates over each element and its index.

```crystal
array.each_with_index(&block : T, Int32 -> ) : self
```

```crystal
["a", "b", "c"].each_with_index { |letter, i| puts "#{i}: #{letter}" }
# 0: a
# 1: b
# 2: c
```

---

#map

Returns a new array with the results of applying a block to each element.

```crystal
array.map(&block : T -> U) : Array(U)
```

```crystal
[1, 2, 3].map { |n| n * 2 } # => [2, 4, 6]
```

---

#map!

Applies a block to each element and modifies the array in place.

```crystal
array.map!(&block : T -> T) : self
```

```crystal
arr = [1, 2, 3]
arr.map! { |n| n * 2 }
arr # => [2, 4, 6]
```

---

#select

Returns a new array containing only elements for which the block returns true.

```crystal
array.select(&block : T -> Bool) : Array(T)
```

```crystal
[1, 2, 3, 4, 5].select { |n| n.even? } # => [2, 4]
```

---

#select!

Modifies the array to contain only elements for which the block returns true.

```crystal
array.select!(&block : T -> Bool) : self?
```

Returns nil if no changes were made.

```crystal
arr = [1, 2, 3, 4, 5]
arr.select! { |n| n.even? }
arr # => [2, 4]
```

---

#reject

Returns a new array containing elements for which the block returns false.

```crystal
array.reject(&block : T -> Bool) : Array(T)
```

```crystal
[1, 2, 3, 4, 5].reject { |n| n.even? } # => [1, 3, 5]
```

---

#reject!

Modifies the array to contain only elements for which the block returns false.

```crystal
array.reject!(&block : T -> Bool) : self?
```

Returns nil if no changes were made.

```crystal
arr = [1, 2, 3, 4, 5]
arr.reject! { |n| n.even? }
arr # => [1, 3, 5]
```

---

#find

Returns the first element for which the block returns true.

```crystal
array.find(&block : T -> Bool) : T?
```

```crystal
[1, 2, 3, 4, 5].find { |n| n > 3 } # => 4
[1, 2, 3].find { |n| n > 10 }      # => nil
```

---

#index

Returns the index of the first occurrence of a value or where the block returns true.

```crystal
array.index(value : T) : Int32?
array.index(&block : T -> Bool) : Int32?
```

```crystal
["a", "b", "c"].index("b")          # => 1
[1, 2, 3, 4].index { |n| n > 2 }   # => 2
[1, 2, 3].index(99)                # => nil
```

---

#rindex

Returns the index of the last occurrence of a value or where the block returns true.

```crystal
array.rindex(value : T) : Int32?
array.rindex(&block : T -> Bool) : Int32?
```

```crystal
[1, 2, 3, 2, 1].rindex(2)          # => 3
[1, 2, 3, 4].rindex { |n| n > 2 }  # => 3
```

---

#include?

Returns true if the array contains the given value.

```crystal
array.include?(value : T) : Bool
```

```crystal
[1, 2, 3].include?(2) # => true
[1, 2, 3].include?(5) # => false
```

---

#first

Returns the first element of the array.

```crystal
array.first : T
array.first(count : Int) : Array(T)
```

```crystal
[1, 2, 3].first    # => 1
[1, 2, 3].first(2) # => [1, 2]
```

Raises IndexError if the array is empty.

---

#last

Returns the last element of the array.

```crystal
array.last : T
array.last(count : Int) : Array(T)
```

```crystal
[1, 2, 3].last    # => 3
[1, 2, 3].last(2) # => [2, 3]
```

Raises IndexError if the array is empty.

---

#reverse

Returns a new array with the elements in reverse order.

```crystal
array.reverse : Array(T)
```

```crystal
[1, 2, 3].reverse # => [3, 2, 1]
```

---

#reverse!

Reverses the array in place.

```crystal
array.reverse! : self
```

```crystal
arr = [1, 2, 3]
arr.reverse!
arr # => [3, 2, 1]
```

---

#sort

Returns a new array with the elements sorted.

```crystal
array.sort : Array(T)
array.sort(&block : T, T -> Int32) : Array(T)
```

```crystal
[3, 1, 2].sort # => [1, 2, 3]
[3, 1, 2].sort { |a, b| b <=> a } # => [3, 2, 1]
```

---

#sort!

Sorts the array in place.

```crystal
array.sort! : self
array.sort!(&block : T, T -> Int32) : self
```

```crystal
arr = [3, 1, 2]
arr.sort!
arr # => [1, 2, 3]
```

---

#uniq

Returns a new array with duplicate elements removed.

```crystal
array.uniq : Array(T)
```

```crystal
[1, 2, 2, 3, 3, 3].uniq # => [1, 2, 3]
```

---

#uniq!

Removes duplicate elements in place.

```crystal
array.uniq! : self?
```

Returns nil if no duplicates were found.

```crystal
arr = [1, 2, 2, 3]
arr.uniq!
arr # => [1, 2, 3]
```

---

#concat

Appends the elements of another array to the array.

```crystal
array.concat(other : Array(T)) : self
```

```crystal
[1, 2].concat([3, 4]) # => [1, 2, 3, 4]
```

---

#+

Returns a new array containing the elements of both arrays.

```crystal
array + other : Array(T) : Array(T)
```

```crystal
[1, 2] + [3, 4] # => [1, 2, 3, 4]
```

---

#&

Returns a new array containing elements common to both arrays (intersection).

```crystal
array & other : Array(T) : Array(T)
```

```crystal
[1, 2, 3] & [2, 3, 4] # => [2, 3]
```

---

#|

Returns a new array containing all unique elements from both arrays (union).

```crystal
array | other : Array(T) : Array(T)
```

```crystal
[1, 2] | [2, 3] # => [1, 2, 3]
```

---

#-

Returns a new array containing elements from the first array that are not in the second (difference).

```crystal
array - other : Array(T) : Array(T)
```

```crystal
[1, 2, 3] - [2, 3] # => [1]
```

---

#&.

Returns a new array containing elements common to both arrays (intersection). Alias for #&.

```crystal
array &. other : Array(T) : Array(T)
```

---

#sample

Returns a random element from the array.

```crystal
array.sample : T?
```

```crystal
[1, 2, 3].sample # => 2 (could be any)
```

---

#shuffle

Returns a new array with the elements randomly shuffled.

```crystal
array.shuffle : Array(T)
```

```crystal
[1, 2, 3].shuffle # => [3, 1, 2] (could be any)
```

---

#shuffle!

Shuffles the array in place.

```crystal
array.shuffle! : self
```

```crystal
arr = [1, 2, 3]
arr.shuffle!
arr # => [3, 1, 2] (could be any)
```

---

#flatten

Returns a new array with all nested arrays recursively flattened.

```crystal
array.flatten : Array
```

```crystal
[[1, 2], [3, 4]].flatten # => [1, 2, 3, 4]
```

---

#flatten!

Flattens the array in place.

```crystal
array.flatten! : self?
```

Returns nil if no change was needed.

```crystal
arr = [[1, 2], [3, 4]]
arr.flatten!
arr # => [1, 2, 3, 4]
```

---

#reduce

Combines all elements using a binary operation.

```crystal
array.reduce(initial : U) { |acc, element| ... } : U
array.reduce(&block : T, T -> T) : T?
```

```crystal
[1, 2, 3, 4].reduce(0) { |acc, n| acc + n } # => 10
[1, 2, 3, 4].reduce { |acc, n| acc + n }     # => 10
[].reduce { |acc, n| acc + n }               # => nil
```

---

#join

Converts the array to a string by joining elements with a separator.

```crystal
array.join(separator : String = "") : String
array.join(separator : String = "", &block : T -> String) : String
```

```crystal
[1, 2, 3].join(", ")                     # => "1, 2, 3"
[1, 2, 3].join { |n| n.to_s * 2 }        # => "112233"
```

---

#to_s

Returns a string representation of the array.

```crystal
array.to_s : String
```

```crystal
[1, 2, 3].to_s # => "[1, 2, 3]"
```

---

#inspect

Returns a string representation of the array showing internal structure.

```crystal
array.inspect : String
```

```crystal
[1, 2, 3].inspect # => "[1, 2, 3]"
```

---

Important Notes

- Arrays are mutable and grow dynamically.
- Arrays can hold any type, including mixed types if declared as Array(Any).
- Indexing with #[] returns the element, not a copy.
- #size and #length are both available and equivalent
- Many methods have both a #method (returns a new array) and a #method! (modifies in place) version.
- The ! suffix indicates an in‑place mutation.

