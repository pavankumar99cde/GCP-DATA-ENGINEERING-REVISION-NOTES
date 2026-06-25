# 1. Difference between List, Tuple, and Set

| Feature    | List      | Tuple     | Set           |
| ---------- | --------- | --------- | ------------- |
| Ordered    | ✅ Yes     | ✅ Yes     | ❌ No          |
| Mutable    | ✅ Yes     | ❌ No      | ✅ Yes         |
| Duplicates | ✅ Allowed | ✅ Allowed | ❌ Not Allowed |
| Indexing   | ✅ Yes     | ✅ Yes     | ❌ No          |
| Syntax     | `[]`      | `()`      | `{}`          |

---

# 2. Difference between List and Array

| Feature     | List            | Array                         |
| ----------- | --------------- | ----------------------------- |
| Data types  | Mixed           | Same type                     |
| Built-in    | ✅ Yes           | ❌ (`array` module or NumPy)   |
| Performance | Slower          | Faster for numeric operations |
| Memory      | More            | Less                          |
| Best for    | General-purpose | Numerical computations        |

---

# 3. Difference between Dictionary and Set

| Feature        | Dictionary      | Set             |
| -------------- | --------------- | --------------- |
| Stores         | Key-Value pairs | Unique values   |
| Duplicate keys | ❌ No            | ❌ No duplicates |
| Access         | By key          | No indexing     |
| Syntax         | `{key:value}`   | `{value}`       |

---

# 4. Difference between Mutable and Immutable Data Types

| Feature         | Mutable               | Immutable              |
| --------------- | --------------------- | ---------------------- |
| Can be modified | ✅ Yes                 | ❌ No                   |
| Memory          | Same object           | New object created     |
| Examples        | List, Dictionary, Set | Tuple, String, Integer |

---

# 5. Difference between `==` and `is`

| Feature    | `==`           | `is`            |
| ---------- | -------------- | --------------- |
| Checks     | Value equality | Object identity |
| Compares   | Values         | Memory address  |
| Common use | Compare data   | Compare objects |

---

# 6. Difference between `append()` and `extend()`

| Feature          | `append()`  | `extend()`        |
| ---------------- | ----------- | ----------------- |
| Adds             | One element | Multiple elements |
| List inside list | ✅ Yes       | ❌ No              |
| Argument         | Any object  | Iterable          |

---

# 7. Difference between `remove()`, `pop()`, and `del`

| Feature          | `remove()` | `pop()`  | `del`           |
| ---------------- | ---------- | -------- | --------------- |
| Removes          | By value   | By index | By index/object |
| Returns value    | ❌ No       | ✅ Yes    | ❌ No            |
| Deletes variable | ❌ No       | ❌ No     | ✅ Yes           |

---

# 8. Difference between `sort()` and `sorted()`

| Feature                | `sort()`   | `sorted()`        |
| ---------------------- | ---------- | ----------------- |
| Original list modified | ✅ Yes      | ❌ No              |
| Returns                | None       | New sorted object |
| Works on               | Lists only | Any iterable      |

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

| Feature          | `return`     | `yield`   |
| ---------------- | ------------ | --------- |
| Ends function    | ✅ Yes        | ❌ No      |
| Returns          | Single value | Generator |
| Memory efficient | ❌ No         | ✅ Yes     |

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

| Concept       | Purpose                             |
| ------------- | ----------------------------------- |
| Inheritance   | Reuse existing class                |
| Encapsulation | Hide data                           |
| Polymorphism  | One interface, many implementations |
| Abstraction   | Hide implementation details         |

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

# 30. Difference between List Comprehension and Generator Expression

| Feature    | List Comprehension    | Generator Expression |
| ---------- | --------------------- | -------------------- |
| Syntax     | `[]`                  | `()`                 |
| Memory     | More                  | Less                 |
| Evaluation | Immediate             | Lazy                 |
| Best for   | Small/medium datasets | Large datasets       |
