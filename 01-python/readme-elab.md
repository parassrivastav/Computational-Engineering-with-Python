# Module 1 - Python as an Engineering Tool: Elaborated Guide

Python is not the goal.

Python is the tool used to model, simulate, analyze, optimize, and understand
reality.

The objective of this module is to develop professional proficiency in Python
for scientific computing, computational engineering, simulation, AI systems, and
technical software development. This elaborated copy expands every concept from
the original module with short descriptions, compact code examples, and
interview-focused tips.

## 1. Python Fundamentals

Python fundamentals are the foundation for writing predictable engineering
software. In interviews, explain not only what a feature does, but also the
trade-offs around memory, precision, mutability, and readability.

### Data Types

Python data types define what kind of value an object stores and what operations
are valid on it.

#### `int`

`int` stores whole numbers with arbitrary precision, limited mainly by available
memory.

```python
samples = 42
large_count = 10**30
print(samples + large_count)
```

Interview tip: Mention that Python integers do not overflow like fixed-width C
integers; they grow as needed, which is safer but can use more memory.

#### `float`

`float` stores double-precision floating-point numbers and is commonly used for
measurements, simulations, and numerical estimates.

```python
time_s = 0.1 + 0.2
print(time_s)          # 0.30000000000000004
print(round(time_s, 2))
```

Interview tip: Floating-point values are approximate. For numerical interviews,
explain tolerance-based comparisons instead of exact equality.

```python
import math

print(math.isclose(0.1 + 0.2, 0.3, rel_tol=1e-9))
```

#### `bool`

`bool` represents truth values: `True` or `False`. It is often used in conditions,
flags, validations, and masks.

```python
is_stable = True
if is_stable:
    print("simulation can continue")
```

Interview tip: `bool` is a subclass of `int`, so `True == 1` is true, but avoid
relying on that in production code because it can reduce clarity.

#### `str`

`str` stores immutable Unicode text.

```python
unit = "m/s"
message = f"velocity unit: {unit}"
print(message)
```

Interview tip: Strings are immutable, so repeated concatenation in large loops
can be inefficient; prefer `join` for many fragments.

#### `complex`

`complex` stores numbers with real and imaginary parts, useful in signals,
control systems, electrical engineering, and frequency-domain analysis.

```python
z = 3 + 4j
print(abs(z))       # magnitude: 5.0
print(z.real, z.imag)
```

Interview tip: Know that Python uses `j` for the imaginary unit and that complex
numbers are built into the language.

#### `bytes`

`bytes` stores immutable binary data, useful for files, network messages, sensor
packets, and encoded data.

```python
payload = b"TEMP=24.5"
print(payload.decode("utf-8"))
```

Interview tip: Distinguish `str` from `bytes`: text is decoded characters;
bytes are raw binary values.

#### Memory representation

Every Python value is an object with identity, type, and value. Objects carry
metadata, which makes Python flexible but more memory-heavy than low-level
languages.

```python
import sys

x = 10
print(id(x))
print(sys.getsizeof(x))
```

Interview tip: For large numerical arrays, explain why NumPy arrays are more
memory-efficient than Python lists of numbers.

#### Mutability

Mutable objects can be changed in place; immutable objects cannot.

```python
values = [1, 2, 3]
values.append(4)       # list is mutable

name = "beam"
name = name.upper()    # creates a new string
```

Interview tip: Common mutable types include `list`, `dict`, and `set`; common
immutable types include `int`, `float`, `bool`, `str`, `tuple`, and `bytes`.

#### Conversions

Conversions transform values from one type to another.

```python
raw = "42"
count = int(raw)
ratio = float("0.125")
label = str(count)
```

Interview tip: Always validate user or file input before converting, because
invalid conversions raise exceptions.

#### Precision limitations

Computers cannot exactly represent every real number. Precision limitations are
especially important in engineering calculations.

```python
from decimal import Decimal

print(0.1 + 0.2)
print(Decimal("0.1") + Decimal("0.2"))
```

Interview tip: Use `math.isclose` for floating-point comparisons and consider
`decimal.Decimal` for financial-style exact decimal arithmetic.

### Variables and References

Variables are names bound to objects. Assignment does not usually copy an object;
it binds another name to the same object.

#### Assignment

```python
a = [1, 2, 3]
b = a
b.append(4)
print(a)  # [1, 2, 3, 4]
```

Interview tip: Assignment copies the reference, not the underlying mutable
object.

#### Object identity

Object identity tells whether two names refer to the exact same object.

```python
a = [1, 2]
b = a
c = [1, 2]
print(a is b)  # True
print(a is c)  # False
print(a == c)  # True
```

Interview tip: Use `is` for identity checks such as `x is None`; use `==` for
value equality.

#### Shallow copy

A shallow copy creates a new outer container but keeps references to nested
objects.

```python
import copy

grid = [[1, 2], [3, 4]]
shallow = copy.copy(grid)
shallow[0][0] = 99
print(grid)  # nested list changed too
```

Interview tip: Shallow copy is fine for flat structures but risky for nested
mutable data.

#### Deep copy

A deep copy recursively copies nested objects.

```python
import copy

grid = [[1, 2], [3, 4]]
deep = copy.deepcopy(grid)
deep[0][0] = 99
print(grid)  # original unchanged
```

Interview tip: Deep copy is safer for nested structures but can be expensive and
may be inappropriate for objects holding files, sockets, or shared resources.

#### Library: `copy`

The `copy` library provides `copy.copy` and `copy.deepcopy`.

```python
import copy

original = {"loads": [10, 20]}
clone = copy.deepcopy(original)
```

Interview tip: Be ready to explain when shallow copy and deep copy produce
different behavior.

### Operators

Operators express calculations, comparisons, logic, and relationships between
objects.

#### Arithmetic

```python
force = 10.0
area = 2.0
stress = force / area
print(stress)
```

Interview tip: Know `/` returns a float, `//` performs floor division, and `%`
returns the remainder.

#### Comparison

```python
temperature = 350
print(300 <= temperature <= 400)
```

Interview tip: Python supports chained comparisons, which are readable and avoid
repeating the variable.

#### Logical

```python
is_valid = temperature > 0 and stress < 250
```

Interview tip: `and` and `or` short-circuit, so later expressions may not run.

#### Bitwise

```python
READ = 0b001
WRITE = 0b010
permission = READ | WRITE
print(permission & READ != 0)
```

Interview tip: Bitwise operators are useful for flags, masks, permissions, and
low-level data processing.

#### Membership

```python
allowed_units = {"m", "s", "kg"}
print("m" in allowed_units)
```

Interview tip: Membership in sets and dictionaries is usually much faster than
membership in lists for large collections.

#### Identity

```python
result = None
print(result is None)
```

Interview tip: Prefer `is None` and `is not None` instead of `== None`.

## 2. Control Flow

Control flow decides which code runs and how many times it runs.

### Conditional Logic

#### `if`

```python
stress = 120
if stress < 250:
    print("safe")
```

Interview tip: Conditions should be readable; extract complex logic into named
boolean variables or functions.

#### `elif`

```python
if stress < 100:
    category = "low"
elif stress < 250:
    category = "normal"
```

Interview tip: `elif` avoids evaluating unnecessary later branches once a match
is found.

#### `else`

```python
if stress < 250:
    status = "pass"
else:
    status = "fail"
```

Interview tip: Use `else` for the default or fallback path.

#### `match-case`

`match-case` performs structural pattern matching and is useful for cleanly
handling command types, records, or tagged data.

```python
command = ("convert", "m", "cm", 2.5)

match command:
    case ("convert", source, target, value):
        print(f"convert {value} from {source} to {target}")
    case _:
        print("unknown command")
```

Interview tip: `match-case` is not just a switch statement; it can destructure
patterns.

### Loops

#### `for`

```python
forces = [10, 20, 30]
for force in forces:
    print(force * 2)
```

Interview tip: Use `for` when iterating over known collections or iterables.

#### `while`

```python
error = 1.0
iteration = 0
while error > 1e-3 and iteration < 100:
    error *= 0.5
    iteration += 1
```

Interview tip: Use `while` when the stop condition depends on runtime state, but
protect against infinite loops.

#### `break`

```python
for value in [3, 5, -1, 8]:
    if value < 0:
        break
```

Interview tip: `break` exits the nearest loop immediately.

#### `continue`

```python
for value in [3, None, 5]:
    if value is None:
        continue
    print(value)
```

Interview tip: `continue` skips the current iteration and moves to the next one.

#### `else` on loops

A loop `else` runs only if the loop did not terminate with `break`.

```python
for value in [2, 4, 6]:
    if value % 2 == 1:
        print("odd found")
        break
else:
    print("no odd values")
```

Interview tip: Loop `else` is commonly used for search logic, but many teams
prefer a helper function for readability.

## 3. Functions

Functions package behavior into reusable, testable units.

### Function Design

#### Arguments

Arguments are inputs passed to a function.

```python
def kinetic_energy(mass, velocity):
    return 0.5 * mass * velocity**2
```

Interview tip: Good functions have clear names, clear inputs, and one primary
responsibility.

#### Keyword arguments

Keyword arguments pass values by parameter name.

```python
print(kinetic_energy(mass=2.0, velocity=3.0))
```

Interview tip: Keywords improve readability for functions with several numeric
parameters.

#### Positional arguments

Positional arguments are matched by order.

```python
print(kinetic_energy(2.0, 3.0))
```

Interview tip: Positional arguments are concise but can be error-prone when many
parameters share the same type.

#### Default values

Default values make parameters optional.

```python
def pressure(force, area=1.0):
    return force / area
```

Interview tip: Never use mutable objects like `[]` or `{}` as default values;
use `None` and create the object inside.

#### Variable arguments: `*args` and `**kwargs`

`*args` collects extra positional arguments, and `**kwargs` collects extra
keyword arguments.

```python
def summarize(*values, **metadata):
    print(f"count={len(values)}")
    print(metadata)

summarize(1, 2, 3, unit="m")
```

Interview tip: Use variable arguments sparingly; explicit signatures are easier
to understand and test.

### Advanced Functions

#### `lambda`

A `lambda` is a small anonymous function.

```python
areas = [3.0, 1.5, 2.0]
print(sorted(areas, key=lambda area: abs(area - 2.0)))
```

Interview tip: Use `lambda` for short expressions, not complex logic.

#### Closures

A closure is a function that remembers variables from its enclosing scope.

```python
def make_scaler(scale):
    def scale_value(value):
        return scale * value
    return scale_value

double = make_scaler(2)
print(double(5))
```

Interview tip: Closures are useful for configuration, callbacks, and function
factories.

#### Decorators

Decorators wrap functions to add behavior such as timing, logging, validation,
or caching.

```python
import time

def timed(func):
    def wrapper(*args, **kwargs):
        start = time.perf_counter()
        result = func(*args, **kwargs)
        print(f"elapsed={time.perf_counter() - start:.6f}s")
        return result
    return wrapper

@timed
def compute():
    return sum(range(1000))
```

Interview tip: Mention `functools.wraps` in production decorators to preserve
function metadata.

#### Higher-order functions

Higher-order functions accept functions as arguments or return functions.

```python
def apply_model(model, x):
    return model(x)

print(apply_model(lambda x: x**2, 4))
```

Interview tip: Higher-order functions support flexible APIs and functional
programming patterns.

#### Built-in: `map`

```python
values = [1, 2, 3]
print(list(map(lambda x: x * 2, values)))
```

Interview tip: In Python, comprehensions are often more readable than `map`.

#### Built-in: `filter`

```python
values = [1, -2, 3]
print(list(filter(lambda x: x > 0, values)))
```

Interview tip: Filtering with a comprehension is usually clearer:
`[x for x in values if x > 0]`.

#### Built-in: `reduce`

```python
from functools import reduce

print(reduce(lambda a, b: a + b, [1, 2, 3], 0))
```

Interview tip: `reduce` is powerful but can be less readable than loops or
built-ins like `sum`, `min`, and `max`.

#### Built-in: `zip`

```python
names = ["beam", "column"]
loads = [10, 20]
print(list(zip(names, loads)))
```

Interview tip: `zip` pairs iterables and stops at the shortest input unless you
use `itertools.zip_longest`.

#### Built-in: `enumerate`

```python
for index, value in enumerate([10, 20, 30], start=1):
    print(index, value)
```

Interview tip: Prefer `enumerate` over manually incrementing counters.

## 4. Core Data Structures

Core data structures determine how data is stored, accessed, and transformed.

### Lists

Lists are ordered, mutable sequences.

```python
readings = [20.1, 20.4, 20.2]
readings.append(20.5)
```

Interview tip: Lists are dynamic arrays; appending is usually efficient, but
inserting at the front is expensive.

#### List built-ins

```python
values = [3, 1, 2]
values.append(4)
values.extend([5, 6])
values.insert(0, 0)
values.remove(3)
last = values.pop()
values.sort()
values.reverse()
```

Interview tip: `sort` mutates the list and returns `None`; `sorted` returns a new
list.

### Tuples

Tuples are ordered, immutable sequences.

```python
point = (3.0, 4.0)
x, y = point
```

Interview tip: Tuples are useful for fixed records, coordinates, and returning
multiple values.

#### Immutability

```python
coordinate = (1.0, 2.0, 3.0)
# coordinate[0] = 9.0  # TypeError
```

Interview tip: Immutability helps prevent accidental modification.

#### Coordinates

```python
position = (10.0, 5.0)
```

Interview tip: For richer coordinate behavior, consider a dataclass or NumPy
array depending on the task.

#### Records

```python
measurement = ("sensor-a", 24.5, "C")
```

Interview tip: If fields need names, use `namedtuple`, `typing.NamedTuple`, or a
dataclass.

### Dictionaries

Dictionaries store key-value pairs and preserve insertion order in modern
Python.

```python
material = {"name": "steel", "density": 7850}
print(material["density"])
```

Interview tip: Dictionary lookup is average-case O(1), making dictionaries ideal
for mappings, indexes, and caches.

#### Dictionary built-ins

```python
config = {"unit": "m"}
unit = config.get("unit", "SI")
config.setdefault("precision", 3)
config.update({"model": "linear"})
print(config.keys())
print(config.values())
print(config.items())
```

Interview tip: Use `get` when a key may be missing; direct indexing raises
`KeyError`.

### Sets

Sets store unique, unordered values and are optimized for membership tests.

```python
units = {"m", "s", "kg", "m"}
print(units)  # duplicates removed
```

Interview tip: Use sets for deduplication and fast membership checks.

#### Set operations

```python
a = {"m", "s", "kg"}
b = {"s", "A", "K"}
print(a | b)  # union
print(a & b)  # intersection
print(a - b)  # difference
print(a ^ b)  # symmetric difference
```

Interview tip: Set operations are concise ways to compare groups of features,
columns, permissions, or IDs.

### Collections Library

The `collections` library provides specialized containers.

```python
import collections
```

Interview tip: Knowing `collections` shows that you can choose the right data
structure instead of forcing everything into lists and dictionaries.

#### `Counter`

```python
from collections import Counter

counts = Counter(["m", "s", "m"])
print(counts.most_common(1))
```

Interview tip: Use `Counter` for frequency analysis.

#### `defaultdict`

```python
from collections import defaultdict

groups = defaultdict(list)
groups["steel"].append(7850)
```

Interview tip: `defaultdict` avoids repetitive missing-key initialization.

#### `deque`

```python
from collections import deque

queue = deque(["job1", "job2"])
queue.append("job3")
print(queue.popleft())
```

Interview tip: `deque` is efficient for appends and pops at both ends.

#### `namedtuple`

```python
from collections import namedtuple

Point = namedtuple("Point", ["x", "y"])
p = Point(3, 4)
print(p.x, p.y)
```

Interview tip: `namedtuple` gives lightweight named fields, but dataclasses are
more flexible for many modern applications.

## 5. Comprehensions

Comprehensions create collections using compact syntax.

### List comprehensions

```python
squares = [x**2 for x in range(5)]
```

Interview tip: Use list comprehensions for clear transformations; avoid nesting
too deeply.

### Dict comprehensions

```python
unit_scale = {unit: index for index, unit in enumerate(["m", "cm", "mm"])}
```

Interview tip: Dict comprehensions are useful for building lookup tables.

### Set comprehensions

```python
unique_lengths = {len(name) for name in ["beam", "bolt", "column"]}
```

Interview tip: Set comprehensions combine transformation and deduplication.

### Generator expressions

```python
total = sum(x**2 for x in range(1_000_000))
```

Interview tip: Generator expressions are lazy and memory-efficient because they
do not build a full list.

## 6. Strings

Strings represent text data such as logs, units, labels, commands, and file
contents.

### String methods

```python
line = "  force,10,N  "
clean = line.strip()
parts = clean.split(",")
joined = " | ".join(parts)
print(joined.replace("force", "load"))
print(clean.find("10"))
print(clean.startswith("force"))
print(clean.endswith("N"))
```

Interview tip: Know that string methods return new strings because strings are
immutable.

### Formatting

```python
value = 9.80665
print(f"gravity = {value:.3f} m/s^2")
```

Interview tip: F-strings are the preferred modern formatting style for readable
Python code.

## 7. File Handling

File handling lets programs read data, write results, and save configuration.

### Built-in: `open()`

```python
with open("results.txt", "w", encoding="utf-8") as file:
    file.write("simulation complete\n")
```

Interview tip: Use `with` so files are closed automatically, even if an error
occurs.

### Modes

```python
# Read: "r"
# Write: "w"
# Append: "a"
# Binary read/write: "rb" or "wb"
```

Interview tip: `w` overwrites existing files; `a` appends to the end; binary
mode returns bytes instead of strings.

### Formats: Text

```python
with open("notes.txt", "r", encoding="utf-8") as file:
    text = file.read()
```

Interview tip: Always specify encoding for portable text processing.

### Formats: CSV

```python
import csv

rows = [{"name": "beam", "load": 10}]
with open("loads.csv", "w", newline="", encoding="utf-8") as file:
    writer = csv.DictWriter(file, fieldnames=["name", "load"])
    writer.writeheader()
    writer.writerows(rows)
```

Interview tip: Use the `csv` module instead of manual splitting when handling
quoted fields or commas inside values.

### Formats: JSON

```python
import json

config = {"unit": "m", "precision": 3}
with open("config.json", "w", encoding="utf-8") as file:
    json.dump(config, file, indent=2)
```

Interview tip: JSON is portable and human-readable, but it does not preserve all
Python-specific types automatically.

## 8. Error Handling

Error handling makes programs robust and debuggable.

### `try` and `except`

```python
try:
    value = float("12.5")
except ValueError:
    value = 0.0
```

Interview tip: Catch specific exceptions; broad `except Exception` can hide bugs.

### `finally`

```python
resource_open = True
try:
    print("use resource")
finally:
    resource_open = False
```

Interview tip: `finally` runs whether or not an exception occurs; context
managers are often cleaner for resource cleanup.

### `raise`

```python
def area(radius):
    if radius < 0:
        raise ValueError("radius must be non-negative")
    return 3.14159 * radius**2
```

Interview tip: Raise errors early when inputs violate assumptions.

### Custom exceptions

```python
class UnitConversionError(Exception):
    """Raised when a unit conversion cannot be completed."""

raise UnitConversionError("unknown unit")
```

Interview tip: Custom exceptions make domain-specific failures easier to catch
and understand.

## 9. Object-Oriented Programming

Object-oriented programming organizes related data and behavior into objects.

### Classes

Classes define object structure and behavior.

```python
class Particle:
    def __init__(self, mass, velocity):
        self.mass = mass
        self.velocity = velocity

    def momentum(self):
        return self.mass * self.velocity
```

Interview tip: Classes are useful when state and behavior belong together.

#### Attributes

Attributes are values stored on an object.

```python
particle = Particle(2.0, 3.0)
print(particle.mass)
```

Interview tip: Instance attributes belong to each object; class attributes are
shared by the class.

#### Methods

Methods are functions attached to classes and usually operate on `self`.

```python
print(particle.momentum())
```

Interview tip: `self` is explicit in Python and refers to the current instance.

#### Constructors

Constructors initialize new objects through `__init__`.

```python
particle = Particle(mass=2.0, velocity=3.0)
```

Interview tip: Keep constructors focused on valid initial state, not heavy work.

### OOP Concepts

#### Encapsulation

Encapsulation groups data and behavior and protects invariants.

```python
class Tank:
    def __init__(self):
        self._volume = 0.0

    def add(self, amount):
        if amount < 0:
            raise ValueError("amount must be positive")
        self._volume += amount
```

Interview tip: Python uses conventions such as a leading underscore for internal
attributes rather than strict private access.

#### Inheritance

Inheritance lets a class reuse and specialize another class.

```python
class Sensor:
    def read(self):
        raise NotImplementedError

class TemperatureSensor(Sensor):
    def read(self):
        return 24.5
```

Interview tip: Use inheritance for true “is-a” relationships, not just code
reuse.

#### Composition

Composition builds objects from other objects.

```python
class Engine:
    def power(self):
        return 100

class Vehicle:
    def __init__(self, engine):
        self.engine = engine
```

Interview tip: Composition is usually easier to test and change than deep
inheritance hierarchies.

#### Polymorphism

Polymorphism allows different objects to support the same interface.

```python
def report(sensor):
    print(sensor.read())

report(TemperatureSensor())
```

Interview tip: Python favors duck typing: if an object has the needed behavior,
it can be used.

#### Composition over inheritance

Prefer composition when behavior can be assembled from independent components.

```python
class Simulator:
    def __init__(self, model, solver):
        self.model = model
        self.solver = solver
```

Interview tip: In interviews, explain that composition reduces tight coupling and
avoids fragile base-class designs.

### Dataclasses

Dataclasses reduce boilerplate for classes that mainly store data.

```python
from dataclasses import dataclass

@dataclass
class ParticleState:
    position: float
    velocity: float
    mass: float
```

Interview tip: Dataclasses automatically generate methods such as `__init__` and
`__repr__`, making engineering models concise.

#### Library: `dataclasses`

```python
from dataclasses import dataclass, field

@dataclass
class Vehicle:
    name: str
    components: list[str] = field(default_factory=list)
```

Interview tip: Use `field(default_factory=list)` for mutable defaults.

#### Engineering model examples

```python
from dataclasses import dataclass

@dataclass
class Planet:
    name: str
    mass_kg: float
    radius_m: float

@dataclass
class Particle:
    x: float
    v: float
    mass: float

@dataclass
class City:
    name: str
    population: int
```

Interview tip: Dataclasses are excellent for `Planet`, `Particle`, `Vehicle`,
and `City` records because they make state explicit and type-friendly.

## 10. Type Hints

Type hints document expected types and help tools catch bugs before runtime.

### Library: `typing`

```python
from typing import Optional, Union, List, Dict, Set, Tuple, Protocol, Generic, TypedDict, TypeVar
```

Interview tip: Type hints are not enforced by CPython at runtime by default;
they are mainly for readability, static analysis, and editor support.

### `Optional`

```python
from typing import Optional

def find_sensor(name: str) -> Optional[str]:
    return name if name == "main" else None
```

Interview tip: `Optional[T]` means `T | None`.

### `Union`

```python
from typing import Union

Number = Union[int, float]
```

Interview tip: In modern Python, `int | float` is often preferred.

### `List`, `Dict`, `Set`, `Tuple`

```python
from typing import Dict, List, Set, Tuple

values: List[float] = [1.0, 2.0]
lookup: Dict[str, float] = {"g": 9.81}
units: Set[str] = {"m", "s"}
point: Tuple[float, float] = (1.0, 2.0)
```

Interview tip: Built-in generics like `list[float]` are standard in modern
Python.

### `Protocol`

```python
from typing import Protocol

class Readable(Protocol):
    def read(self) -> float: ...
```

Interview tip: Protocols express structural interfaces and fit Python duck
typing well.

### `Generic`

```python
from typing import Generic, TypeVar

T = TypeVar("T")

class Box(Generic[T]):
    def __init__(self, value: T):
        self.value = value
```

Interview tip: Generics help write reusable containers and algorithms with type
safety.

### `TypedDict`

```python
from typing import TypedDict

class Config(TypedDict):
    unit: str
    precision: int
```

Interview tip: `TypedDict` is useful for dictionaries with known keys, such as
JSON-like configuration data.

## 11. Iterators and Generators

Iterators and generators support lazy data processing, which is essential for
large simulations and streaming data.

### `iter`

```python
values = iter([1, 2, 3])
print(values)
```

Interview tip: An iterable can produce an iterator; an iterator remembers its
position.

### `next`

```python
values = iter([1, 2, 3])
print(next(values))
print(next(values))
```

Interview tip: `next` raises `StopIteration` when the iterator is exhausted.

### `yield`

```python
def countdown(n):
    while n > 0:
        yield n
        n -= 1

for value in countdown(3):
    print(value)
```

Interview tip: `yield` creates a generator, which produces values lazily instead
of storing all results in memory.

## 12. Context Managers

Context managers manage setup and cleanup around a block of code.

### Built-in: `with`

```python
with open("results.txt", "w", encoding="utf-8") as file:
    file.write("done")
```

Interview tip: `with` is commonly used for files, locks, database sessions, and
temporary resources.

### Custom context managers

```python
class Timer:
    def __enter__(self):
        import time
        self.start = time.perf_counter()
        return self

    def __exit__(self, exc_type, exc, traceback):
        import time
        self.elapsed = time.perf_counter() - self.start
        print(self.elapsed)
```

Interview tip: `__enter__` sets up the resource and `__exit__` handles cleanup.

### Library: `contextlib`

```python
from contextlib import contextmanager

@contextmanager
def managed_message():
    print("start")
    try:
        yield
    finally:
        print("end")
```

Interview tip: `contextlib.contextmanager` is a concise way to create simple
context managers.

## 13. Modules and Packages

Modules and packages organize Python code into reusable files and directories.

### Imports

```python
import math
from pathlib import Path
```

Interview tip: Imports should be explicit and placed at the top of the file.

### Packages

A package is a directory of modules that can be imported together.

```text
engineering/
  __init__.py
  units.py
  solvers.py
```

Interview tip: Good package structure makes medium-sized projects easier to test
and maintain.

### `__init__.py`

`__init__.py` marks a directory as a traditional Python package and can expose a
public API.

```python
# engineering/__init__.py
from .units import convert
```

Interview tip: Keep `__init__.py` lightweight to avoid import side effects.

### Relative imports

```python
# inside engineering/solvers.py
from .units import convert
```

Interview tip: Relative imports are useful inside packages, but absolute imports
are often clearer at application boundaries.

### Library: `importlib`

```python
import importlib

module = importlib.import_module("math")
print(module.sqrt(9))
```

Interview tip: `importlib` is useful for plugin systems and dynamic imports, but
avoid unnecessary dynamic behavior.

## 14. Testing

Testing verifies that code behaves correctly and protects against regressions.

### Libraries: `pytest` and `unittest`

```python
# pytest style
def test_area():
    assert 3.14 < 3.14159 < 3.15
```

```python
# unittest style
import unittest

class AreaTests(unittest.TestCase):
    def test_truth(self):
        self.assertTrue(True)
```

Interview tip: `pytest` is concise and popular; `unittest` is built into the
standard library.

### Assertions

```python
def test_pressure():
    assert 10 / 2 == 5
```

Interview tip: Assertions should check behavior, including edge cases and error
conditions.

### Fixtures

```python
import pytest

@pytest.fixture
def sample_config():
    return {"unit": "m"}

def test_config(sample_config):
    assert sample_config["unit"] == "m"
```

Interview tip: Fixtures reduce duplicate setup code in tests.

### Mocks

```python
from unittest.mock import Mock

sensor = Mock()
sensor.read.return_value = 24.5
print(sensor.read())
```

Interview tip: Use mocks to isolate code from slow or external dependencies, but
do not over-mock simple logic.

## 15. Logging

Logging records runtime information for debugging, monitoring, and operations.

### Library: `logging`

```python
import logging

logging.basicConfig(level=logging.INFO)
logger = logging.getLogger(__name__)
logger.info("simulation started")
```

Interview tip: Prefer logging over `print` in production applications.

### Levels: `debug`, `info`, `warning`, `error`, `exception`

```python
logger.debug("internal value")
logger.info("normal progress")
logger.warning("unexpected but recoverable")
logger.error("operation failed")
try:
    1 / 0
except ZeroDivisionError:
    logger.exception("division failed")
```

Interview tip: `logger.exception` should be called inside an exception handler;
it includes traceback information.

## 16. Command Line Applications

Command line applications make engineering tools scriptable and reusable.

### Libraries: `argparse`, `pathlib`, and `sys`

```python
import argparse
from pathlib import Path
import sys

parser = argparse.ArgumentParser()
parser.add_argument("input", type=Path)
args = parser.parse_args()
print(args.input)
print(sys.version)
```

Interview tip: `pathlib.Path` is preferred over manual string path handling.

### Build: Calculators

```python
def unit_calculator(value, scale):
    return value * scale
```

Interview tip: Calculator CLIs should validate inputs and print clear errors.

### Build: Estimators

```python
def estimate_cost(quantity, unit_cost):
    return quantity * unit_cost
```

Interview tip: Estimators should document assumptions because estimates are only
as good as their model.

### Build: Simulators

```python
def step(position, velocity, dt):
    return position + velocity * dt
```

Interview tip: Simulators need clear state, time-step logic, and numerical
stability checks.

## 17. Concurrency

Concurrency allows programs to handle multiple tasks, but the right model depends
on whether work is I/O-bound or CPU-bound.

### Threading

`threading` runs multiple threads in one process and is useful for I/O-bound
work.

```python
import threading

def worker():
    print("working")

thread = threading.Thread(target=worker)
thread.start()
thread.join()
```

Interview tip: Due to the Global Interpreter Lock, Python threads usually do not
speed up CPU-heavy pure Python code.

### Multiprocessing

`multiprocessing` runs separate processes and can use multiple CPU cores.

```python
from multiprocessing import Pool

with Pool() as pool:
    print(pool.map(abs, [-1, -2, 3]))
```

Interview tip: Multiprocessing is useful for CPU-bound tasks but has overhead
from process startup and data serialization.

### Async

`asyncio` handles many waiting tasks efficiently in a single thread.

```python
import asyncio

async def main():
    await asyncio.sleep(0.1)
    print("done")

asyncio.run(main())
```

Interview tip: Async is best for high-concurrency I/O, not for making CPU-heavy
code magically faster.

## 18. Performance

Performance work should be measurement-driven, not guess-based.

### Libraries: `time`, `timeit`, and `cProfile`

```python
import time

start = time.perf_counter()
sum(range(100000))
print(time.perf_counter() - start)
```

```python
import timeit

print(timeit.timeit("sum(range(1000))", number=1000))
```

```python
import cProfile

cProfile.run("sum(range(100000))")
```

Interview tip: Use `timeit` for small snippets and `cProfile` to find where a
program spends time.

### Profiling

Profiling measures runtime behavior.

```python
# Run from shell:
# python -m cProfile script.py
```

Interview tip: Profile first, optimize the bottleneck second.

### Optimization

Optimization improves speed, memory use, or scalability.

```python
# Prefer this:
total = sum(values)

# Over manual loops when built-ins are clearer and optimized.
```

Interview tip: Maintain correctness and readability; premature optimization can
create bugs.

### Bottleneck analysis

Bottleneck analysis identifies the slowest or most resource-heavy part.

```python
# If 90% of runtime is in one function, optimize that function first.
```

Interview tip: A small improvement in the bottleneck often beats large changes
elsewhere.

## 19. Numerical Computing

Numerical computing uses arrays and vectorized operations to solve engineering
problems efficiently.

### Library: `numpy`

```python
import numpy as np
```

Interview tip: NumPy is the foundation for most scientific Python tools.

### `ndarray`

```python
import numpy as np

x = np.array([1.0, 2.0, 3.0])
print(type(x), x.dtype, x.shape)
```

Interview tip: NumPy arrays store homogeneous data compactly, unlike Python
lists of arbitrary objects.

### Slicing

```python
matrix = np.array([[1, 2, 3], [4, 5, 6]])
print(matrix[:, 1])
```

Interview tip: NumPy slices are often views, not copies; modifying them can
modify the original array.

### Broadcasting

```python
values = np.array([1, 2, 3])
print(values + 10)
```

Interview tip: Broadcasting applies operations across compatible shapes without
manual loops.

### Vectorization

```python
velocity = np.array([1.0, 2.0, 3.0])
energy = 0.5 * 2.0 * velocity**2
```

Interview tip: Vectorization is usually faster and clearer than Python loops for
array math.

### Matrix operations

```python
A = np.array([[1, 2], [3, 4]])
b = np.array([5, 6])
print(A @ b)
```

Interview tip: Use `@` for matrix multiplication and `*` for elementwise
multiplication.

## 20. Data Analysis

Data analysis turns raw tabular data into useful information.

### Library: `pandas`

```python
import pandas as pd
```

Interview tip: Pandas is powerful for labeled tabular data but may be excessive
for simple arrays.

### DataFrames

```python
df = pd.DataFrame({"sensor": ["a", "b"], "temp": [24.5, 25.1]})
print(df.head())
```

Interview tip: A DataFrame is like a table with labeled rows and columns.

### Filtering

```python
hot = df[df["temp"] > 25]
```

Interview tip: Pandas filtering uses boolean masks.

### Grouping

```python
df = pd.DataFrame({"material": ["steel", "steel", "wood"], "load": [10, 20, 5]})
print(df.groupby("material"))
```

Interview tip: `groupby` splits data into groups before aggregation or
transformation.

### Aggregation

```python
print(df.groupby("material")["load"].mean())
```

Interview tip: Aggregation summarizes many rows into fewer results.

### Cleaning

```python
df = pd.DataFrame({"temp": [24.5, None, 25.1]})
clean = df.dropna()
filled = df.fillna({"temp": df["temp"].mean()})
```

Interview tip: Always understand missing data before dropping or filling it.

## 21. Scientific Computing

Scientific computing provides tested algorithms for engineering mathematics.

### Library: `scipy`

```python
import scipy
```

Interview tip: SciPy builds on NumPy and provides higher-level numerical
algorithms.

### Optimization

```python
from scipy.optimize import minimize

def objective(x):
    return (x[0] - 3) ** 2

result = minimize(objective, x0=[0])
print(result.x)
```

Interview tip: Know the difference between objective functions, constraints, and
initial guesses.

### Integration

```python
from scipy.integrate import quad

area, error = quad(lambda x: x**2, 0, 1)
print(area, error)
```

Interview tip: Numerical integration returns an estimate and often an error
estimate.

### Interpolation

```python
from scipy.interpolate import interp1d

f = interp1d([0, 1, 2], [0, 10, 20])
print(f(1.5))
```

Interview tip: Interpolation estimates between known data points; extrapolation
outside known data can be risky.

### ODE solvers

```python
from scipy.integrate import solve_ivp

def decay(t, y):
    return [-0.5 * y[0]]

solution = solve_ivp(decay, (0, 10), [1.0])
print(solution.y[:, -1])
```

Interview tip: For ODEs, be clear about state variables, time span, initial
conditions, and solver tolerances.

## 22. Visualization

Visualization helps communicate behavior, results, uncertainty, and trends.

### Libraries: `matplotlib` and `plotly`

```python
import matplotlib.pyplot as plt
```

Interview tip: Use static plots for reports and interactive plots for
exploration or dashboards.

### Line plots

```python
plt.plot([0, 1, 2], [0, 1, 4])
plt.xlabel("time")
plt.ylabel("position")
plt.close()
```

Interview tip: Line plots are best for continuous trends or ordered sequences.

### Scatter plots

```python
plt.scatter([1, 2, 3], [2, 4, 5])
plt.close()
```

Interview tip: Scatter plots show relationships between paired variables.

### Histograms

```python
plt.hist([1, 1, 2, 3, 3, 3])
plt.close()
```

Interview tip: Histograms show distributions, not time trends.

### Animations

```python
from matplotlib.animation import FuncAnimation

fig, ax = plt.subplots()
point, = ax.plot([], [], "o")

def update(frame):
    point.set_data([frame], [frame**2])
    return point,

animation = FuncAnimation(fig, update, frames=range(5))
plt.close(fig)
```

Interview tip: Animations are useful for simulations, but keep them separate
from the core numerical model.

## 23. Serialization

Serialization saves and loads data so results, configurations, and model states
can be reused.

### Libraries: `json` and `pickle`

```python
import json
import pickle
```

Interview tip: JSON is portable and readable; pickle is Python-specific and can
execute unsafe code if loaded from untrusted sources.

### Saving models

```python
model = {"slope": 2.0, "intercept": 1.0}
with open("model.json", "w", encoding="utf-8") as file:
    json.dump(model, file)
```

Interview tip: Save enough metadata to reproduce the model, such as units,
parameters, and version information.

### Saving simulations

```python
state = {"time": 1.0, "position": 3.2}
with open("state.pkl", "wb") as file:
    pickle.dump(state, file)
```

Interview tip: Use pickle only for trusted data and compatible Python
environments.

### Configuration files

```python
config = {"dt": 0.01, "steps": 1000}
with open("config.json", "w", encoding="utf-8") as file:
    json.dump(config, file, indent=2)
```

Interview tip: Configuration should be explicit, documented, and validated.

## 24. Engineering Libraries

Scientific Python libraries form the practical foundation for computational
engineering.

### `numpy`

NumPy provides arrays, vectorized math, and linear algebra.

```python
import numpy as np
print(np.linalg.norm([3, 4]))
```

Interview tip: NumPy is usually the first tool for numerical arrays.

### `scipy`

SciPy provides optimization, integration, interpolation, signal processing, and
more.

```python
from scipy import optimize
print(optimize.brentq(lambda x: x**2 - 4, 0, 3))
```

Interview tip: Use SciPy when you need robust algorithms instead of writing your
own from scratch.

### `sympy`

SymPy provides symbolic mathematics.

```python
import sympy as sp

x = sp.symbols("x")
print(sp.diff(x**2, x))
```

Interview tip: Symbolic math is useful for derivations, exact algebra, and
checking formulas.

### `pandas`

Pandas provides high-level data analysis tools.

```python
import pandas as pd
print(pd.Series([1, 2, 3]).mean())
```

Interview tip: Pandas is strong for tabular data, but NumPy may be better for
large dense numerical arrays.

### `matplotlib`

Matplotlib provides plotting and visualization.

```python
import matplotlib.pyplot as plt
plt.plot([0, 1], [0, 1])
plt.close()
```

Interview tip: Visualization is part of analysis, not decoration; label axes and
units.

## 25. Professional Python Checklist

A professional computational engineer should be comfortable with the following
skills.

### Building CLI tools

Create command line interfaces for repeatable workflows.

```python
# Example command idea: python convert.py 10 m cm
```

Interview tip: Discuss input validation, help text, exit codes, and automation.

### Writing reusable modules

Organize logic into importable files rather than one-off scripts.

```python
# units.py
def meters_to_centimeters(value):
    return value * 100
```

Interview tip: Reusable modules separate core logic from user interfaces.

### Using type hints

Add type hints to clarify function contracts.

```python
def convert(value: float, scale: float) -> float:
    return value * scale
```

Interview tip: Type hints improve maintainability and enable static checking.

### Using dataclasses

Use dataclasses for structured model data.

```python
from dataclasses import dataclass

@dataclass
class LoadCase:
    name: str
    force_n: float
```

Interview tip: Mention `default_factory` for mutable fields.

### Working with NumPy

Use NumPy for array-based numerical work.

```python
import numpy as np
print(np.array([1, 2, 3]) * 10)
```

Interview tip: Explain vectorization and broadcasting.

### Working with SciPy

Use SciPy for reliable scientific algorithms.

```python
from scipy.integrate import quad
print(quad(lambda x: x, 0, 1)[0])
```

Interview tip: Prefer tested library algorithms for optimization, integration,
and ODE solving.

### Profiling code

Measure before optimizing.

```python
# python -m cProfile your_script.py
```

Interview tip: Identify bottlenecks with evidence.

### Writing tests

Write automated tests for critical behavior.

```python
def test_convert():
    assert convert(1, 100) == 100
```

Interview tip: Include edge cases, invalid inputs, and numerical tolerances.

### Reading documentation

Use official documentation to understand APIs and edge cases.

```python
help(dict.get)
```

Interview tip: Strong engineers know how to learn from docs quickly.

### Building simulations

Represent state, update rules, and outputs clearly.

```python
position = 0.0
velocity = 10.0
dt = 0.1
position += velocity * dt
```

Interview tip: Discuss stability, units, validation, and reproducibility.

### Building optimization systems

Define objective functions, constraints, variables, and stopping criteria.

```python
def objective(x):
    return (x - 5) ** 2
```

Interview tip: Optimization results depend heavily on modeling assumptions and
initial guesses.

### Visualizing results

Turn results into interpretable charts.

```python
import matplotlib.pyplot as plt
plt.plot([0, 1, 2], [0, 1, 4])
plt.close()
```

Interview tip: Always label axes, units, and assumptions.

### Debugging numerical issues

Investigate NaN, infinity, conditioning, tolerances, and units.

```python
import math

value = float("nan")
print(math.isnan(value))
```

Interview tip: Numerical bugs often come from scale, precision, invalid inputs,
or unstable algorithms.

### Structuring medium-sized projects

Separate source code, tests, documentation, and scripts.

```text
project/
  src/
  tests/
  docs/
  scripts/
```

Interview tip: Structure helps teams collaborate and prevents scripts from
becoming unmaintainable.

### Using Git effectively

Use version control to track, review, and collaborate on changes.

```bash
git status
git add .
git commit -m "Add unit conversion engine"
```

Interview tip: Understand branches, commits, pull requests, and meaningful commit
messages.

## Project

### Build a Unit Conversion Engine

A unit conversion engine converts values between compatible units while
preserving correctness and clarity.

```python
SCALES_TO_METER = {
    "m": 1.0,
    "cm": 0.01,
    "mm": 0.001,
}

def convert_length(value, source_unit, target_unit):
    meters = value * SCALES_TO_METER[source_unit]
    return meters / SCALES_TO_METER[target_unit]

print(convert_length(2, "m", "cm"))
```

Interview tip: Discuss unit categories, validation, error messages, tests,
floating-point tolerance, and extensibility.

## Completion Criteria

You have completed Module 1 when you can confidently build the following without
relying heavily on AI assistance.

### Unit Conversion Engine

Build a tool that converts between units and rejects incompatible conversions.

```python
print(convert_length(100, "cm", "m"))
```

Interview tip: Validate units and avoid silent incorrect conversions.

### Matrix Calculator

Build a calculator for matrix addition, multiplication, determinants, and linear
systems.

```python
import numpy as np

A = np.array([[1, 2], [3, 4]])
b = np.array([5, 6])
print(np.linalg.solve(A, b))
```

Interview tip: Know the difference between elementwise operations and matrix
operations.

### Monte Carlo Simulator

Build a simulator that uses random sampling to estimate uncertainty or
probability.

```python
import random

inside = 0
samples = 10_000
for _ in range(samples):
    x, y = random.random(), random.random()
    inside += x*x + y*y <= 1
print(4 * inside / samples)
```

Interview tip: Discuss randomness, reproducibility with seeds, convergence, and
confidence intervals.

### Projectile Motion Simulator

Build a simulator for position and velocity under gravity.

```python
def projectile_y(v0, t, g=9.81):
    return v0 * t - 0.5 * g * t**2
```

Interview tip: Be clear about units, assumptions such as no air resistance, and
numerical versus analytical solutions.

### City Reality Estimator

Build an estimator that combines data and assumptions to approximate city-level
metrics.

```python
def population_density(population, area_km2):
    return population / area_km2
```

Interview tip: Explain assumptions, data quality, sensitivity analysis, and
uncertainty.

At that point, Python is no longer something you are learning. It becomes a tool
you use to solve engineering problems.
