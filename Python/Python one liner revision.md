|	#	| Interview Question                              | One-Line Answer                                                               |
|	----------	| ----------------------------------------------- | ----------------------------------------------------------------------------- |
|	1	| What are Python decorators?                     | Functions that modify another function's behavior without changing its code.  |
|	2	| What is a generator?                            | A function that yields values one at a time using `yield`.                    |
|	3	| Why use generators instead of lists?            | They save memory by generating values lazily.                                 |
|	4	| What is the purpose of the `yield` keyword?     | It pauses execution and returns a value while preserving state.               |
|	5	| What is a lambda function?                      | An anonymous function written in a single expression.                         |
|	6	| When would you use a lambda function?           | For short, one-time functions passed to functions like `map()` or `filter()`. |
|	7	| What are list comprehensions?                   | A concise way to create lists using a single expression.                      |
|	8	| What is dictionary comprehension?               | A concise way to create dictionaries in one line.                             |
|	9	| What is set comprehension?                      | A concise way to create sets using an expression.                             |
|	10	| What is exception handling?                     | A mechanism to handle runtime errors using `try` and `except`.                |
|	11	| What is the purpose of the `finally` block?     | It executes whether an exception occurs or not.                               |
|	12	| What is the `else` block in exception handling? | It runs only if no exception occurs.                                          |
|	13	| What is a custom exception?                     | A user-defined exception created by inheriting from `Exception`.              |
|	14	| What is `*args`?                                | It allows passing a variable number of positional arguments.                  |
|	15	| What is `**kwargs`?                             | It allows passing a variable number of keyword arguments.                     |
|	16	| What is variable unpacking?                     | Assigning multiple variables from an iterable in one statement.               |
|	17	| What is iterable in Python?                     | An object that can be looped over.                                            |
|	18	| What is an iterator?                            | An object that returns elements one at a time using `next()`.                 |
|	19	| What is the `iter()` function?                  | It converts an iterable into an iterator.                                     |
|	20	| What is the `next()` function?                  | It returns the next item from an iterator.                                    |
|	21	| What is the purpose of `enumerate()`?           | It returns both index and value during iteration.                             |
|	22	| What is `zip()` used for?                       | It combines multiple iterables element by element.                            |
|	23	| What does `map()` do?                           | It applies a function to every element of an iterable.                        |
|	24	| What does `filter()` do?                        | It returns elements that satisfy a condition.                                 |
|	25	| What does `reduce()` do?                        | It reduces an iterable to a single value by applying a function repeatedly.   |
|	26	| Where is `reduce()` available?                  | In the `functools` module.                                                    |
|	27	| What is the purpose of `sorted()`?              | It returns a new sorted list without modifying the original.                  |
|	28	| What does the `key` parameter in `sorted()` do? | It specifies the function used for sorting.                                   |
|	29	| What is the purpose of `any()`?                 | Returns `True` if at least one element is true.                               |
|	30	| What is the purpose of `all()`?                 | Returns `True` only if all elements are true.                                 |
|	31	| What is the purpose of `isinstance()`?          | Checks whether an object belongs to a specific class.                         |
|	32	| What is the purpose of `type()`?                | Returns the type of an object.                                                |
|	33	| What is the purpose of `id()`?                  | Returns the memory identity of an object.                                     |
|	34	| What is the purpose of `range()`?               | Generates a sequence of numbers.                                              |
|	35	| What is the purpose of `pass`?                  | It acts as a placeholder statement.                                           |
|	36	| What is the purpose of `continue`?              | Skips the current iteration of a loop.                                        |
|	37	| What is the purpose of `break`?                 | Exits the nearest loop immediately.                                           |
|	38	| What is the purpose of `assert`?                | Used to verify assumptions during debugging.                                  |
|	39	| What is a docstring?                            | A string used to document modules, classes, or functions.                     |
|	40	| What is the `__name__ == "__main__"` block?     | It ensures code runs only when the file is executed directly.                 |
|	41	| What are modules in Python?                     | Files containing reusable Python code.                                        |
|	42	| What are packages?                              | Collections of related Python modules.                                        |
|	43	| What is a virtual environment?                  | An isolated Python environment for project dependencies.                      |
|	44	| What is PEP 8?                                  | Python's official style guide for writing readable code.                      |
|	45	| What is garbage collection in Python?           | Automatic memory management by removing unused objects.                       |
|	46	| What is reference counting?                     | Python's primary memory management mechanism.                                 |
|	47	| What is circular reference?                     | Objects referencing each other, preventing immediate cleanup.                 |
|	48	| Which module manages garbage collection?        | The `gc` module.                                                              |
|	49	| What is serialization?                          | Converting an object into a storable or transmittable format.                 |
|	50	| What is the `pickle` module?                    | A module used for Python object serialization.                                |
|	51	| Why is `pickle` unsafe for untrusted data?      | It can execute arbitrary code during deserialization.                         |
|	52	| What is JSON serialization?                     | Converting Python objects into JSON format.                                   |
|	53	| What is a context manager?                      | An object that manages resources using the `with` statement.                  |
|	54	| What methods define a context manager?          | `__enter__()` and `__exit__()`.                                               |
|	55	| Why use the `with` statement?                   | It automatically releases resources like files or locks.                      |
|	56	| What is multithreading?                         | Running multiple threads within a single process.                             |
|	57	| What is multiprocessing?                        | Running multiple independent processes simultaneously.                        |
|	58	| When is multiprocessing preferred?              | For CPU-intensive tasks.                                                      |
|	59	| When is multithreading preferred?               | For I/O-bound tasks.                                                          |
|	60	| What is asynchronous programming?               | Running tasks without blocking execution using `async` and `await`.           |
|	61	 | How does Python manage memory internally?    | Using reference counting and cyclic garbage collection.                          |
|	62	 | What causes memory leaks in Python?          | Lingering references or improperly handled circular references.                  |
|	63	 | What is object interning?                    | Python reuses certain immutable objects to improve performance.                  |
|	64	 | What is bytecode?                            | Intermediate instructions executed by the Python Virtual Machine.                |
|	65	 | What is the Python Virtual Machine (PVM)?    | The runtime that executes Python bytecode.                                       |
|	66	 | What is compilation in Python?               | Source code is compiled into bytecode before execution.                          |
|	67	 | What are `.pyc` files?                       | Cached compiled bytecode files.                                                  |
|	68	 | When are `.pyc` files generated?             | After importing or executing Python modules.                                     |
|	69	 | What are magic methods?                                   | Special methods like `__init__` and `__str__` that customize object behavior.       |
|	70	 | What is `__init__`?                                       | The constructor called when an object is created.                                   |
|	71	 | What is `__str__`?                                        | Returns a user-friendly string representation of an object.                         |
|	72	 | What is `@staticmethod`?                                  | A method that doesn't access class or instance data.                                |
|	73	 | What is `@classmethod`?                                   | A method that receives the class as its first argument.                             |
|	74	 | What is method chaining?                                  | Returning `self` to allow multiple method calls in one statement.                   |
|	75	 | What is object serialization?                             | Converting an object into a byte stream or JSON.                                    |
|	76	 | What is deserialization?                                  | Reconstructing an object from serialized data.                                      |
|	77	 | What is shallow copy?                                     | Copies the outer object while sharing nested objects.                               |
|	78	 | What is deep copy?                                        | Recursively copies both outer and nested objects.                                   |
|	79	 | Which module performs deep copying?                       | The `copy` module.                                                                  |
|	80	 | What is object identity?                                  | The unique memory location of an object.                                            |
|	81	 | What is object mutability?                                | Whether an object's value can change after creation.                                |
|	82	 | What is variable shadowing?                               | A local variable hides a variable with the same name from an outer scope.           |
|	83	 | What is the LEGB rule?                                    | Python searches variables in Local, Enclosing, Global, then Built-in scopes.        |
|	84	 | What does the `global` keyword do?                        | It allows modifying a global variable inside a function.                            |
|	85	 | What does the `nonlocal` keyword do?                      | It modifies a variable in the enclosing function's scope.                           |
|	86	 | What are first-class functions?                           | Functions that can be assigned, passed, and returned like any other object.         |
|	87	 | Can functions be stored in variables?                     | Yes, because functions are objects in Python.                                       |
|	88	 | Can a function return another function?                   | Yes, enabling closures and decorators.                                              |
|	89	 | What is the `collections` module?                         | Provides specialized container data structures.                                     |
|	90	 | What is lazy evaluation?                                  | Values are computed only when needed.                                               |
|	91	 | Which Python features use lazy evaluation?                | Generators, iterators, and `map()` objects.                                         |
|	92	 | What is `Counter`?                                        | Counts occurrences of hashable objects.                                             |
|	93	| What are Python's namespaces?                   | Containers that map names to objects.                                         |
|	94	| What is an event loop?                          | The engine that schedules and runs asynchronous tasks.                        |
|	95	| What is the `asyncio` module?                   | Python's built-in framework for asynchronous programming.                     |
|	96	| What is function caching using `lru_cache`?     | Automatically caches previous function results.                               |
|	97	| What is dynamic typing?                         | Variable types are determined at runtime.                                     |
|	98	| What is monkey patching?                        | Modifying classes or modules at runtime.                                      |
|	99	| What is duck typing?                            | If an object behaves like the expected type, Python accepts it.               |
|	100	| What is introspection?                          | Examining an object's type and attributes at runtime.                         |
|	101	| What is reflection?                             | Dynamically inspecting and modifying objects during execution.                |
|	102	| What is memoization?                            | Caching function results to avoid repeated computations.                      |
|	103	| What is recursion?                              | A function calling itself to solve a problem.                                 |
|	104	| What is tail recursion?                         | Recursive call made as the last operation of a function.                      |
|	105	| Does Python optimize tail recursion?            | No, Python does not perform tail recursion optimization.                      |
|	106	| What is function annotation?                    | Metadata added to function parameters and return values.                      |
|	107	| What are type hints?                            | Optional annotations indicating expected data types.                          |
|	108	| What is a closure?                              | An inner function that remembers variables from its outer scope.              |
|	109	| What is lexical scoping?                        | Inner functions can access variables from enclosing scopes.                   |
|	110	| What is the Global Interpreter Lock (GIL)?      | A lock allowing only one thread to execute Python bytecode at a time.         |
|	111	| Does the GIL affect multiprocessing?            | No, each process has its own Python interpreter and GIL.                      |
