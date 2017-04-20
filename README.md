# Module 10: Dictionaries
This module covers the second fundamental data structure in Python: **dictionaries**, which represent a collection of _key-value pairs_. They are similar to lists, except that each element in the dictionary is also given a distinct "name" to refer to it by (instead of an index number). Dictionaries are Pythons primary version of **maps**, which is a common and extremely useful way of organizing data in a computer program&mdash;I would argue that maps are the _most useful_ data structure in programming. This module will descibe how to create, access, and utilize dictionaries to organize and struture data.

<!-- START doctoc generated TOC please keep comment here to allow auto update -->
<!-- DON'T EDIT THIS SECTION, INSTEAD RE-RUN doctoc TO UPDATE -->
**Contents**

- [Resources](#resources)
- [Dictionaries](#dictionaries)
  - [Accessing a Dictionary](#accessing-a-dictionary)
- [Dictionary Methods](#dictionary-methods)
  - [Dictionaries and Loops](#dictionaries-and-loops)
- [Nesting Dictionaries](#nesting-dictionaries)
- [Which data structure do I use?](#which-data-structure-do-i-use)

<!-- END doctoc generated TOC please keep comment here to allow auto update -->

## Resources
- [Dictionaries and Data Structures (Sweigart)](https://automatetheboringstuff.com/chapter5/)
- [Dictionaries (Downey)](https://books.trinket.io/pfe/09-dictionaries.html)

## Dictionaries
A **dictionary** is a lot like a _list_, in that it is a (one-dimensional) sequence of values that are all stored in a single variable. However, rather than using _integers_ as the index for each element, a dictionary allows you to use a wide variety of different data types (including _strings_ and _tuples_) as the "index". These "indices" are called **keys**, and each is used to refer to a specific **value** in the collection. Thus a dictionary is an sequence of **key-value pairs**: each element has a "key" that is used to _look up_ (reference) the "value".

- This is a lot like a real-world dictionary or encyclopedia, in which the words (keys) are used to look up the definitions (values). A phone book works te same way (the names are the keys, thephone numbers are the values),

- Dictionaries provide a **mapping** of keys to values: they specify a set of data (the keys), and how that data "transforms" into another set of data (the values).

Dictionaries are written as literals inside _curly braces_ (**`{}`**). Key-value pairs are written with a _colon_ (**`:`**) between the key and the value, and each element (pair) in the dictionary is separated by a  _comma_ (**`,`**):

```python
# a dictionary of ages
ages = {'sarah':42, 'amit':35, 'zhang':13}

# a dictionary of English words and their Spanish translation
english_to_spanish = {'one':'uno', 'two':'dos'}

# a dictionary of integers and their word representation
num_words = {1:'one', 2:'two', 3:'three'}

# like lists, dictionary values can be of different types
# including lists and other dictionaries!
type_examples = {'integer':12, 'string':'dog', 'list':[1,2,3]}

# each dictionary key can also be a different type
type_names = {'hello': 'a string', 598: 'an integer', 3.14: 'a float', (1,2): 'a tuple!'}

# dictionaries can be empty (with no elements)
empty = {}
```

- Dictionary variables are often named as plurals, but can also be named after the mapping they performed (e.g., `english_to_spanish`).
- Be careful not to name a dictionary `dict`, which is a reserved keyword (it's a function used to create dictionaries).

Dictionary _keys_ can be of any [hashable](https://en.wikipedia.org/wiki/Hash_function) type (meaning the computer can consistently convert it into a number). In practice, this means that that keys are most commonly _strings_, _numbers_, or _tuples_. Dictionary _values_, on the other hand, can be of any type that you want!

Dictionary _keys_ must be unique: because they are used to "look up" values, there has to be a single value associated with each key (this is called a [one-to-one mapping] in mathematics). But dictionary _values_ can be duplicated: just like how two words may have the same definition in a real-world dictionary!

```python
double_key = {'a': 1, 'b': 2, 'b': 3}
print(double_key)  # {'a': 1, 'b': 3}

double_val = {'a': 1, 'b': 1, 'c': 1}
print(double_val)  # {'a': 1, 'b': 1, 'c': 1}
```

_Important note:_ dictionaries are an **unordered** collection of key-value pairs! Because you reference a value by its _key_ and not by its position (as you do in a list), the exact ordering of those elements doesn't matter&mdash;the interpreter just goes immediately to the value associated with the key. This almost means that when you print out a dictionary, the order in which the elements are printed may not match the order in which you specified them in the literal (and in fact, may different between script executions or across computers!)

```python
dict_a = {'a':1, 'b;':2}
dict_b = {'b':2, 'a:'1}
dict_a == dict_b  # True
```

The above examples mostly use dictionaries as "lookup tables": they provide a way of "translating" from some set of keys to some set of values. However, dictionaries are also extremely useful for grouping together related data&mdash;for example, information about a specific person:

```python
person = {'first_name': "Ada", 'job': "Programmer", 'salary':78000, 'in_union':True}
```

Using a dictionary allows us to track the differnet values with named keys, rather than needing to remember whether the person's name or title was the first element!

Dictionaries can also be created from _lists_ of keys and values. First use the built-in `zip()` function to create a non-list collection of tuples (each a key-value pair), and then use the built-in `dict()` function to create a dictonary out of that collection. Alternatively the built-in `enumerate()` function will create an collection with the index of each list element as its key.

```python
keys = ['key0', 'key1', 'key2']
values = ['val0', 'val1', 'val2']
dict(zip(keys, values))  # {'key0': 'val0', 'key1': 'val1', 'key2': 'val2'}
dict(enumerate(values))  # {0: 'val0', 1: 'val1', 2: 'val2'}
```

### Accessing a Dictionary
Just as with lists, we retrieve a ___value___ from a dictionary using **bracket notation**, but we put the ___key___ inside the brackets instead of the positional index (since dictionaries are unordered!).

```python
# a dictionary of ages
ages = {'sarah':42, 'amit':35, 'zhang':13}

# get the value for the 'amit' key
amit_age = ages['amit']
print(amit_age)  # 35

# get the value for the 'zhang' key
zhang_age = ages['zhang']
print(zhang_age)  # 13

# accessing a key not in the dictionary will give an error
print(ages['anonymus'])  # KeyError!

# trying to look up by a VALUE will give an error (since it's not a key)
print(ages[42])  # KeyError!
```

- To reiterate: you put the _key_ inside the brackets in order to access the _value_. You cannot directly put in a value in order to determine its key (because it may have more than one!)

  It is worth noting that "looking up" a value by its key is a very "fast" operation (it doesn't take the interpreter a lot of time or effort). But looking up the key for a value takes time: you need to check each and every key in the dictionary to see if it has the value you're interested in!

As with lists, you can put any _expression_ (including variables) inside the brackets as long as it resolves to a valid key (whether that key is a string, integer, or tuple).

As with lists, you can **mutate** (change) the dictionary by assigning values to the bracket-notation variable. This changes the _key-value pair_ to have a different value, but the same key:

```python
person = {'name': "Ada", 'job': "Programmer", 'salary':78000}

# assign a new value to the 'job' key
person['job'] = 'Senior Programmer'
print(person['job'])  # Senior Programmer

# assign value to itself
person['salary'] = person['salary'] * 1.15  # a 15% raise!

# add a new key-value pair by assigning a value a key
# that is not yet in the dictionary
person['shoe_size'] = 7
print(person)  # {'name': 'Ada', 'job': 'Senior Programmer', 'salary': 89700.0, 'shoe_size': 7}
```

Note that adding new elements (key-value pairs) works differently than lists: with a list, you cannot assign a value to an index that is out of bounds: you need to use the `append()` method instead). With a dictionary, you _can_ assign a value to a non-existent key. This _creates_ the key, assigning it the given value.

You can add a _new_ key-value pair to a dictionary by assigning a value _to a key that is not yet in the dictionary_. This is distinct from lists (where you cannot assign out of bounds):


## Dictionary Methods
Dictionaries support a few different [operations and methods](https://docs.python.org/3/library/stdtypes.html#mapping-types-dict), though not as many as lists. These include:

```python
# A sample dictionary to demonstrate with
sample_dict = {'a': 1, 'b': 2, 'c': 3, 'd': 4, 'e': 5}

# The standard `in` operator checks for operands in the keys, not the values!
'b' in sample_dict  # True, dict contains a key `'b'`
2 in sample_dict  # False, dict does not contain a key `2`

# The get() method returns the value for the key, or a "default" value
# if the key is not in the dictionary
default = -598  # a default value
sample_dict.get('c', default)  # 3, key is in dict
sample_dict.get('f', default)  # -598, key not in dict, so return default

# Remove a key-value pair
sample_dict.pop('d')  # removes and returns the `d` key and its value

# Replace values from one dictionary with those from another
other_dict = {'a':10, 'c': 10, 'n':10}
sample_dict.update(other_dict)  # assign values from other to sample
print(sample_dict)  # {'a': 10, 'b': 2, 'c': 10, 'e': 5, 'n': 10}

sample_dict.update(a=20, c=20)  # update also supports named arguments
print(sample_dict)  # {'a': 20, 'b': 2, 'c': 20, 'e': 5, 'n': 10}

# Remove all the elements
sample_dict.clear()
```

Dictionaries also include three methods that return list-like _sequences_ of the dictionary's elements:

```python
sample_dict = {'a': 1, 'b': 2, 'c': 3, 'd': 4, 'e': 5}

# get a "list" of the keys
sample_keys = sample_dict.keys()
print(list(sample_keys))  # ['a', 'b', 'c', 'd', 'e']

# get a "list" of the values
sample_vals = sample_dict.values()
print(list(sample_vals))  # [1, 2, 3, 4, 5]

# get a "list" of the key-value pairs
sample_items = sample_dict.items()
print(list(sample_items))  # [('a', 1), ('b', 2), ('c', 3), ('d', 4), ('e', 5)]
```

The `keys()`, `values()`, and `items()` sequences are not quite lists (they don't have all of the list operantions and methods), but they do support the `in` operator and iteration with `for` loops (see below). And as demonstrated above, they can easily be converted _into_ lists if needed.

- Note that the `items()` method produces a sequence of _tuples_&mdash;each key-value pair is represented as a tuple whose first element is the key and second is the value!


### Dictionaries and Loops
Dictionaries are iterable collections (like lists, ranges, strings, files, etc), and so you can loop through them with a **for loop**. Note that the basic `for ... in ...` syntact iterates through the dictionary's _keys_ (not its values!) Thus it is much more common utilize one of the `keys()`, `values()`, or `items()` sequences.

```python
sample_dict = {'a': 1, 'b': 2, 'c': 3, 'd': 4, 'e': 5}

# loop through the keys (implicitly)
for key in sample_dict:
    print(key, "maps to", sample_dict[key])  # e.g., "'a' maps to 1"

# loop through the keys (explicitly)
for key in sample_dict.keys():
    print(key, "maps to", sample_dict[key])  # e.g., "'a' maps to 1"

# loop through the values. Cannot directly get the key from this
for value in sample_dict.values():
    print("someone maps to", value)  # e.g., "someone maps to 1"

# Loop through the items (each is a tuple)
for item in sample_dict.items():
    print(item[0], "maps to", item[1])  # e.g., "'a' maps to 1"
```

It is _much_ more common to use **multiple assignment** to give the `items()` tuple elements local variable names, allowing you to refer to those elements by name rather than by index:

```python
# Use this format instead!
for key, value in sample_dict.items():  # implicit  `key, value = item`
    print(key, "maps to", value)  # e.g., "'a' maps to 1

# Better yet, name the local variables after their semantic meaning!
for letter, number in sample_dict.items():
    print(letter, "maps to", number)  # e.g., "'a' maps to 1
```

Finally, remember that dictionaries are _unordered_. This means that there is no consistency as to which element will be processed in what order: you might get `a` then `b` then `c`, but you might get `c` then `a` then `b`! If the order is important for looping, a common strategy is to iterate through a _sorted list of the keys_ (produced with the built-in [`sorted()`](https://docs.python.org/3/library/functions.html#sorted) function):

```python
# Sort the keys
sorted_keys = sorted(my_dict.keys())

# Iterate through the sorted keys
for key in sorted_keys:
    print(key, "maps to", my_dict[key])

# Or all in one line!
for key in sorted(my_dict.keys()):
    print(key, "maps to", my_dict[key])
```

## Nesting Dictionaries
Although dictionary _keys_ are limited to hashable types (e.g., strings, numbers, tuples), dictionary _values_ can be of any type&mdash;and this includes lists and other dictionaries!

Nested dictionaries are conceptually similar to nested lists, and are used in a similar manner:

```python
# a dictionary representing a person (spacing is for readability)
person = {
  'first_name': 'Alice',
  'last_name': 'Smith',
  'age': 40,
  'pets': ['rover', 'fluffy', 'mittens'],  # value is an array
  'favorites': {  # value is another dictionary
    'music': 'jazz',
    'food': 'pizza',
    'numbers': [12, 42] # value is an array
  }
}

# can assign lists or dicts to a new key
person['luggage_combo'] = [1,2,3,4,5]

# person['favorite'] is an (anonymous) dictionary, so can get that dict's 'food'
favorite_food = person['favorites']['food'];

# Get to the (anonymous) 'favorites' dictionary in person, and from that get
# the (anonymous) 'numbers' list, and from that get the 0th element
first_fav_number = person['favorite']['numbers'][0];  # 12

# Since person['favorite']['numbers'] is a list, we can add to it
person['favorite']['numbers'].append(7);  # add 7 to end of the list
```

The ability to nest dictionaries inside of dictionaries is incredibly powerful, and allows us to define arbitrarily complex information structurings (schemas). Indeed, most data in computer programs&mdash;as well as public information available on the web&mdash;is structured as a set of nested maps like this (though possibly with some level of abstraction).

The other common format used with nested lists and dictionaries is to define a **list of dictionaries** where each dictionary has _the same keys_ (but different values). For example:

```python
# arbitrary list of people's names, heights, and weights
people = [
    {'name': 'Ada', 'height': 58, 'weight': 115},
    {'name': 'Bob', 'height': 59, 'weight': 117},
    {'name': 'Chris', 'height': 60, 'weight': 120},
    {'name': 'Diya', 'height': 61, 'weight': 123},
    {'name': 'Emma', 'height': 62, 'weight': 126}
]
```

This structure can be seen as a list of **records** (the dictionaries), each of which have a number of different **features** (the key-value pairs). This list of feature records is in fact a common way of understanding a **data table** like you would create as an Excel spreadsheet:

| name | height | weight |
|---|---|---|
| Ada | 58 | 115 |
| Bob | 59 | 117 |
| Chris | 60 | 120 |
| Diya | 61 | 123 |
| Emma | 62 | 126 |

Each dictionary (record) acts as a "row" in the table, and each key (feature) acts as a "column". As long as all of the dictionaries share the same keys, this list of dictionaries _is_ a table!

- When working with large amounts of tabular data, like you might read from a `.csv` file, this is a good structure to use.

In order to analyze this kind of data table, you most often will loop through the elements in the list (the rows in the table), doing some calculations based on _each_ dictionary:

```python
# How many people are taller than 60 inches?
taller_than_60 = 0
for person in people:  # iterate through the list
    # person is a dictionary
    if person['height'] >= 60:  # each dictionary has a 'height' key
        taller_than_60 += 1  # increasement count

print(taller_than_60)  # 3
```

This is effective, but not particularly efficient (or simple). We will discuss more robust and powerful ways of working with this style of data table more in a later module.


## Which data structure do I use?
The last two modules have introduced multiple different **data structures** built into Python: _lists_, _tuples_, and _dictionaries_. They all represent collections of elements, though in somewhat different ways. So when do you each each type?

- Use **lists** for any _ordered_ sequence of data (e.g., if you care about what comes first), or if you are collecting elements of the same general "type" (e.g., a lot of numbers, a lot of strings, etc.). If you're not sure what else to use, a _list_ is a great default data structure.

- Use **tuples** when you need to ensure that a list is _immutable_ (canot be changed), such as if you want it to be a key to a dictionary or a parameter to a function. Tuples are also nice if you just want to store a _small_ set of data (only a few items) that is not going to change. Finally, tuples may arguable provide an "easier" syntax than lists in certain situations, such as when using multiple assignment.

- Use **dictionaries** whenever you need to represent a _mapping_ of data and want to link some set of keys to some set of values. If you want to be able to "name" each value in your collection, you can use a dictionary. If you want to work with key-value pairs, you need to use a dictionary (or some other [dictionary-like data structure](https://docs.python.org/3/library/collections.html#namedtuple-factory-function-for-tuples-with-named-fields))
