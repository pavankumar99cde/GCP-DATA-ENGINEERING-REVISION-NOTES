# 1. Difference between List, Tuple, and Set


| Feature            | List                                                                                | Tuple              | Set                                                                                                   |
| ------------------ | ----------------------------------------------------------------------------------- | ------------------ | ----------------------------------------------------------------------------------------------------- |
| Ordered            | ✅ Yes                                                                               | ✅ Yes              | ❌ No                                                                                                  |
| Mutable            | ✅ Yes                                                                               | ❌ No               | ✅ Yes                                                                                                 |
| Duplicates         | ✅ Allowed                                                                           | ✅ Allowed          | ❌ Not Allowed                                                                                         |
| Indexing           | ✅ Yes                                                                               | ✅ Yes              | ❌ No                                                                                                  |
| Syntax             | `[]`                                                                                | `()`               | `{}`                                                                                                  |
| Memory Usage       | More                                                                                | Less               | Moderate                                                                                              |
| Performance        | Slower than Tuple                                                                   | Faster than List   | Fast lookup                                                                                           |
| Use Case           | Dynamic collection                                                                  | Fixed data         | Unique values                                                                                         |
| **Common Methods** | `append(), extend(), insert(), remove(), pop(), sort(), reverse(), clear(), copy()` | `count(), index()` | `add(), update(), remove(), discard(), pop(), clear(), union(), intersection(), difference(), copy()` |

---

# 2. Difference between List and Array

| Feature            | List                                                                                | Array                                                                                           |
| ------------------ | ----------------------------------------------------------------------------------- | ----------------------------------------------------------------------------------------------- |
| Data types         | Mixed data types                                                                    | Same data type only                                                                             |
| Built-in           | ✅ Yes                                                                               | ❌ (`array` module or NumPy)                                                                     |
| Performance        | Slower                                                                              | Faster for numeric operations                                                                   |
| Memory             | More                                                                                | Less                                                                                            |
| Indexing           | ✅ Yes                                                                               | ✅ Yes                                                                                           |
| Dynamic size       | ✅ Yes                                                                               | ✅ Yes                                                                                           |
| Best for           | General-purpose programming                                                         | Numerical computations                                                                          |
| **Common Methods** | `append(), extend(), insert(), remove(), pop(), sort(), reverse(), clear(), copy()` | `append(), extend(), insert(), remove(), pop(), reverse(), fromlist(), tolist(), buffer_info()` |

---

# 3. Difference between Dictionary and Set

| Feature               | Dictionary                                                                                    | Set                                                                                                                           |
| --------------------- | --------------------------------------------------------------------------------------------- | ----------------------------------------------------------------------------------------------------------------------------- |
| Stores                | Key-Value pairs                                                                               | Unique values                                                                                                                 |
| Duplicate Keys        | ❌ Not Allowed                                                                                 | N/A                                                                                                                           |
| Duplicate Values      | ✅ Allowed                                                                                     | ❌ Not Allowed                                                                                                                 |
| Access                | By key                                                                                        | No indexing                                                                                                                   |
| Ordered (Python 3.7+) | ✅ Yes                                                                                         | ❌ No guaranteed order                                                                                                         |
| Mutable               | ✅ Yes                                                                                         | ✅ Yes                                                                                                                         |
| Syntax                | `{key: value}`                                                                                | `{value}`                                                                                                                     |
| Best for              | Fast key-value lookup                                                                         | Removing duplicates, membership testing                                                                                       |
| **Common Methods**    | `get(), keys(), values(), items(), update(), pop(), popitem(), setdefault(), clear(), copy()` | `add(), update(), remove(), discard(), pop(), clear(), union(), intersection(), difference(), symmetric_difference(), copy()` |


---

# 4. Difference between Mutable and Immutable Data Types

| Feature         | Mutable               | Immutable              |
| --------------- | --------------------- | ---------------------- |
| Can be modified | ✅ Yes                 | ❌ No                   |
| Memory          | Same object           | New object created     |
| Examples        | List, Dictionary, Set | Tuple, String, Integer |

---

# 5. Difference between `==` and `is`

| Feature             | `==`                                      | `is`                                       |
| ------------------- | ----------------------------------------- | ------------------------------------------ |
| Checks              | Value equality                            | Object identity                            |
| Compares            | Values                                    | Memory address                             |
| Returns `True` when | Values are equal                          | Both variables refer to the same object    |
| Common use          | Compare data                              | Compare objects (especially `None`)        |
| Example             | `a=[1,2]`<br>`b=[1,2]`<br>`a == b → True` | `a=[1,2]`<br>`b=[1,2]`<br>`a is b → False` |


---

# 6. Difference between `append()` and `extend()`

| Feature            | `append()`                                              | `extend()`                                            |
| ------------------ | ------------------------------------------------------- | ----------------------------------------------------- |
| Adds               | One element                                             | Multiple elements                                     |
| List inside list   | ✅ Yes                                                   | ❌ No                                                  |
| Argument           | Any object                                              | Iterable                                              |
| List size increase | +1                                                      | By number of elements                                 |
| Example            | `a=[1,2]`<br>`a.append([3,4])`<br>Output: `[1,2,[3,4]]` | `a=[1,2]`<br>`a.extend([3,4])`<br>Output: `[1,2,3,4]` |

---

# 7. Difference between `remove()`, `pop()`, and `del`

| Feature                        | `remove()`                                            | `pop()`                                                            | `del`                                             |
| ------------------------------ | ----------------------------------------------------- | ------------------------------------------------------------------ | ------------------------------------------------- |
| Removes                        | By value                                              | By index                                                           | By index/object                                   |
| Returns removed value          | ❌ No                                                  | ✅ Yes                                                              | ❌ No                                              |
| Deletes variable               | ❌ No                                                  | ❌ No                                                               | ✅ Yes                                             |
| Raises error if item not found | ✅ Yes                                                 | ✅ Yes                                                              | ✅ Yes                                             |
| Example                        | `a=[10,20,30]`<br>`a.remove(20)`<br>Output: `[10,30]` | `a=[10,20,30]`<br>`a.pop(1)`<br>Returns: `20`<br>Output: `[10,30]` | `a=[10,20,30]`<br>`del a[1]`<br>Output: `[10,30]` |

---

# 8. Difference between `sort()` and `sorted()`

| Feature                | `sort()`                                            | `sorted()`                                                                       |
| ---------------------- | --------------------------------------------------- | -------------------------------------------------------------------------------- |
| Original list modified | ✅ Yes                                               | ❌ No                                                                             |
| Returns                | `None`                                              | New sorted list                                                                  |
| Works on               | Lists only                                          | Any iterable                                                                     |
| Memory usage           | Less                                                | More (creates new list)                                                          |
| Example                | `a=[3,1,2]`<br>`a.sort()`<br>`print(a)` → `[1,2,3]` | `a=[3,1,2]`<br>`b=sorted(a)`<br>`print(a)` → `[3,1,2]`<br>`print(b)` → `[1,2,3]` |


---

# 9. Difference between Shallow Copy and Deep Copy

| Feature               | Shallow Copy | Deep Copy |
| --------------------- | ------------ | --------- |
| Copies nested objects | ❌ No         | ✅ Yes     |
| Shares references     | ✅ Yes        | ❌ No      |
| Memory usage          | Less         | More      |

---

# 10. Difference between `copy.copy()` and `copy.deepcopy()`

| Feature               | `copy.copy()` | `copy.deepcopy()` |
| --------------------- | ------------- | ----------------- |
| Copy type             | Shallow       | Deep              |
| Nested objects copied | ❌ No          | ✅ Yes             |
| Performance           | Faster        | Slower            |

---

# 11. Difference between Function and Method

| Feature      | Function      | Method          |
| ------------ | ------------- | --------------- |
| Belongs to   | Module        | Class/Object    |
| Called using | Function name | Object/Class    |
| Example      | `len()`       | `list.append()` |

---

# 12. Difference between `*args` and `**kwargs`

| Feature | `*args`              | `**kwargs`        |
| ------- | -------------------- | ----------------- |
| Accepts | Positional arguments | Keyword arguments |
| Type    | Tuple                | Dictionary        |
| Syntax  | `*`                  | `**`              |

---

# 13. Difference between Local, Global, and Nonlocal Variables

| Feature                     | Local    | Global        | Nonlocal       |
| --------------------------- | -------- | ------------- | -------------- |
| Scope                       | Function | Entire module | Outer function |
| Accessible outside function | ❌ No     | ✅ Yes         | ❌ No           |
| Keyword                     | None     | `global`      | `nonlocal`     |

---

# 14. Difference between `break`, `continue`, and `pass`

| Feature                 | `break` | `continue` | `pass` |
| ----------------------- | ------- | ---------- | ------ |
| Stops loop              | ✅ Yes   | ❌ No       | ❌ No   |
| Skips current iteration | ❌ No    | ✅ Yes      | ❌ No   |
| Placeholder             | ❌ No    | ❌ No       | ✅ Yes  |

---

# 15. Difference between `return` and `yield`

| Feature         | `return`                                                     | `yield`                                                                                                 |
| --------------- | ------------------------------------------------------------ | ------------------------------------------------------------------------------------------------------- |
| Purpose         | Returns the final result and exits the function              | Produces one value at a time without exiting the function                                               |
| Function Type   | Normal function                                              | Generator function                                                                                      |
| Execution       | Ends immediately after `return`                              | Pauses execution and resumes on the next iteration                                                      |
| Values Returned | Single value (or multiple values at once)                    | One value at a time                                                                                     |
| Memory Usage    | Higher (stores all results if created together)              | Lower (generates values lazily)                                                                         |
| Best For        | Small datasets, simple functions                             | Large datasets, streaming data, pipelines                                                               |
| Reusability     | Function must be called again                                | Continues from the previous state                                                                       |
| Example         | `def square(x):`<br>  `return x*x`<br><br>`square(5)` → `25` | `def square(n):`<br>  `for i in range(n):`<br>    `yield i*i`<br><br>`list(square(5))` → `[0,1,4,9,16]` |


---

# 16. Difference between Generator and Iterator

| Feature          | Generator | Iterator |
| ---------------- | --------- | -------- |
| Created using    | `yield`   | `iter()` |
| Easier to create | ✅ Yes     | ❌ No     |
| Memory efficient | ✅ Yes     | ✅ Yes    |

---

# 17. Difference between Iterable, Iterator, and Generator

| Feature          | Iterable   | Iterator | Generator |
| ---------------- | ---------- | -------- | --------- |
| Can be looped    | ✅ Yes      | ✅ Yes    | ✅ Yes     |
| Has `__iter__()` | ✅ Yes      | ✅ Yes    | ✅ Yes     |
| Has `__next__()` | ❌ No       | ✅ Yes    | ✅ Yes     |
| Created using    | Collection | `iter()` | `yield`   |

---

# 18. Difference between Module and Package

| Feature  | Module            | Package               |
| -------- | ----------------- | --------------------- |
| Meaning  | Single `.py` file | Collection of modules |
| Contains | Functions/Classes | Multiple modules      |
| Example  | `math.py`         | `numpy`               |

---

# 19. Difference between Multithreading and Multiprocessing

| Feature      | Multithreading  | Multiprocessing |
| ------------ | --------------- | --------------- |
| Uses         | Threads         | Processes       |
| Memory       | Shared          | Separate        |
| Best for     | I/O-bound tasks | CPU-bound tasks |
| GIL affected | ✅ Yes           | ❌ No            |

---

# 20. Difference between Class Variable and Instance Variable

| Feature | Class Variable | Instance Variable   |
| ------- | -------------- | ------------------- |
| Shared  | All objects    | Individual object   |
| Defined | Inside class   | Inside `__init__()` |
| Memory  | One copy       | One per object      |

---

# 21. Difference between `range()` and `xrange()`

| Feature               | `range()`    | `xrange()`            |
| --------------------- | ------------ | --------------------- |
| Python version        | Python 3     | Python 2              |
| Returns               | Range object | Generator-like object |
| Available in Python 3 | ✅ Yes        | ❌ No                  |

---

# 22. Difference between Python 2 and Python 3

| Feature  | Python 2  | Python 3 |
| -------- | --------- | -------- |
| Print    | Statement | Function |
| Unicode  | Limited   | Default  |
| Division | Integer   | Float    |
| Support  | Ended     | Active   |

---

# 23. Difference between `@staticmethod`, `@classmethod`, and Instance Method

| Feature                   | Static Method | Class Method | Instance Method |
| ------------------------- | ------------- | ------------ | --------------- |
| First parameter           | None          | `cls`        | `self`          |
| Access class variables    | ❌ No          | ✅ Yes        | ✅ Yes           |
| Access instance variables | ❌ No          | ❌ No         | ✅ Yes           |

---

# 24. Difference between Inheritance, Encapsulation, Polymorphism, and Abstraction

| Concept           | Purpose                                                        | Key Idea                                                        | Example                                                              |
| ----------------- | -------------------------------------------------------------- | --------------------------------------------------------------- | -------------------------------------------------------------------- |
| **Inheritance**   | Reuse code from an existing class                              | Child class acquires properties and methods of the parent class | `class Dog(Animal):`                                                 |
| **Encapsulation** | Protect data by restricting direct access                      | Bundle data and methods together using classes                  | Private variable: `self.__salary`                                    |
| **Polymorphism**  | Use the same method name with different behaviors              | One interface, multiple implementations                         | `animal.sound()` calls different implementations for `Dog` and `Cat` |
| **Abstraction**   | Hide implementation details and expose only essential features | Show *what* to do, hide *how* it is done                        | Abstract class with `@abstractmethod`                                |


---

# 25. Difference between `__str__()` and `__repr__()`

| Feature     | `__str__()`          | `__repr__()`           |
| ----------- | -------------------- | ---------------------- |
| Purpose     | User-friendly output | Developer/debug output |
| Used by     | `print()`            | `repr()`               |
| Readability | High                 | Detailed               |

---

# 26. Difference between Exception and Error

| Feature        | Exception      | Error                         |
| -------------- | -------------- | ----------------------------- |
| Can be handled | ✅ Yes          | Usually ❌ No                  |
| Causes         | Runtime issues | Serious system/program issues |
| Examples       | `ValueError`   | `SyntaxError`, `MemoryError`  |

---

# 27. Difference between `try-except` and `try-finally`

| Feature                 | `try-except`   | `try-finally`             |
| ----------------------- | -------------- | ------------------------- |
| Handles exceptions      | ✅ Yes          | ❌ No                      |
| Always executes cleanup | ❌ No           | ✅ Yes                     |
| Common use              | Error handling | Closing files/connections |

---

# 28. Difference between Threading and Asyncio

| Feature           | Threading          | Asyncio                                              |
| ----------------- | ------------------ | ---------------------------------------------------- |
| Concurrency model | Multiple threads   | Single-threaded event loop                           |
| Best for          | Blocking I/O       | Non-blocking I/O                                     |
| Context switching | OS-managed         | Event loop-managed                                   |
| Uses              | `threading` module | `async` / `await`                                    |
| GIL affected      | ✅ Yes              | Runs in a single thread (not parallel CPU execution) |

---

# 29. Difference between `copy.copy()` and Assignment (`=`)

| Feature               | Assignment (`=`) | `copy.copy()` |
| --------------------- | ---------------- | ------------- |
| Creates new object    | ❌ No             | ✅ Yes         |
| Shares nested objects | ✅ Yes            | ✅ Yes         |
| Type                  | Reference        | Shallow copy  |

---

# 30. Difference between List Comprehension and Dictionary Comprehension

| Feature               | List Comprehension                                      | Dictionary Comprehension                                             |
| --------------------- | ------------------------------------------------------- | -------------------------------------------------------------------- |
| Purpose               | Used to create a **list** in a single line.             | Used to create a **dictionary (key-value pairs)** in a single line.  |
| Output Type           | `list`                                                  | `dict`                                                               |
| Syntax                | `[expression for item in iterable]`                     | `{key: value for item in iterable}`                                  |
| Stores                | Values only                                             | Key-Value pairs                                                      |
| Duplicate Values      | ✅ Allowed                                               | Values can duplicate, but **keys must be unique**                    |
| Conditional Filtering | ✅ Supported                                             | ✅ Supported                                                          |
| Best For              | Creating or transforming lists                          | Creating lookup tables or mappings                                   |
| Example               | `[x*x for x in range(5)]`<br>Output: `[0, 1, 4, 9, 16]` | `{x: x*x for x in range(5)}`<br>Output: `{0:0, 1:1, 2:4, 3:9, 4:16}` |

