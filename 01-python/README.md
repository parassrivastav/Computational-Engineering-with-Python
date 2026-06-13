# Module 1 - Python as an Engineering Tool

Python is not the goal.

Python is the tool used to model, simulate, analyze, optimize, and understand
reality.

The objective of this module is to develop professional proficiency in Python
for scientific computing, computational engineering, simulation, AI systems, and
technical software development.

## 1. Python Fundamentals

### Data Types

- `int`
- `float`
- `bool`
- `str`
- `complex`
- `bytes`

Know:

- Memory representation
- Mutability
- Conversions
- Precision limitations

### Variables and References

- Assignment
- Object identity
- Shallow copy
- Deep copy

Library:

- `copy`

### Operators

- Arithmetic
- Comparison
- Logical
- Bitwise
- Membership
- Identity

## 2. Control Flow

### Conditional Logic

- `if`
- `elif`
- `else`
- `match-case`

### Loops

- `for`
- `while`
- `break`
- `continue`
- `else` on loops

## 3. Functions

### Function Design

- Arguments
- Keyword arguments
- Positional arguments
- Default values
- Variable arguments

```python
*args
**kwargs
```

### Advanced Functions

- `lambda`
- Closures
- Decorators
- Higher-order functions

Built-ins:

- `map`
- `filter`
- `reduce`
- `zip`
- `enumerate`

## 4. Core Data Structures

### Lists

Built-ins:

- `append`
- `extend`
- `insert`
- `remove`
- `pop`
- `sort`
- `reverse`

### Tuples

Use cases:

- Immutability
- Coordinates
- Records

### Dictionaries

Built-ins:

- `get`
- `setdefault`
- `update`
- `keys`
- `values`
- `items`

### Sets

Operations:

- Union
- Intersection
- Difference
- Symmetric difference

### Collections Library

Know:

```python
collections
```

Especially:

- `Counter`
- `defaultdict`
- `deque`
- `namedtuple`

## 5. Comprehensions

- List comprehensions
- Dict comprehensions
- Set comprehensions
- Generator expressions

## 6. Strings

Methods:

- `split`
- `join`
- `replace`
- `strip`
- `find`
- `startswith`
- `endswith`

Formatting:

```python
f"{value}"
```

## 7. File Handling

Built-in:

```python
open()
```

Modes:

- Read
- Write
- Append
- Binary

Formats:

- Text
- CSV
- JSON

Libraries:

- `csv`
- `json`

## 8. Error Handling

- `try`
- `except`
- `finally`
- `raise`
- Custom exceptions

## 9. Object-Oriented Programming

### Classes

- Attributes
- Methods
- Constructors

### OOP Concepts

- Encapsulation
- Inheritance
- Composition
- Polymorphism

Focus more on:

> Composition over inheritance.

### Dataclasses

Library:

```python
dataclasses
```

Dataclasses are critical for engineering models.

Examples:

- Planet
- Particle
- Vehicle
- City

## 10. Type Hints

Library:

```python
typing
```

Know:

- `Optional`
- `Union`
- `List`
- `Dict`
- `Set`
- `Tuple`
- `Protocol`
- `Generic`
- `TypedDict`

## 11. Iterators and Generators

- `iter`
- `next`
- `yield`

Essential for simulations.

## 12. Context Managers

Built-in:

```python
with
```

Create custom context managers.

Library:

```python
contextlib
```

## 13. Modules and Packages

Know:

- Imports
- Packages
- `__init__.py`
- Relative imports

Library:

- `importlib`

## 14. Testing

Libraries:

- `pytest`
- `unittest`

Know:

- Assertions
- Fixtures
- Mocks

## 15. Logging

Library:

```python
logging
```

Know:

- `debug`
- `info`
- `warning`
- `error`
- `exception`

## 16. Command Line Applications

Libraries:

- `argparse`
- `pathlib`
- `sys`

Build:

- Calculators
- Estimators
- Simulators

## 17. Concurrency

### Threading

Library:

```python
threading
```

### Multiprocessing

Library:

```python
multiprocessing
```

### Async

Library:

```python
asyncio
```

## 18. Performance

Libraries:

- `time`
- `timeit`
- `cProfile`

Concepts:

- Profiling
- Optimization
- Bottleneck analysis

## 19. Numerical Computing

Library:

```python
numpy
```

Must master:

- `ndarray`
- Slicing
- Broadcasting
- Vectorization
- Matrix operations

This is the most important library in computational engineering.

## 20. Data Analysis

Library:

```python
pandas
```

Know:

- DataFrames
- Filtering
- Grouping
- Aggregation
- Cleaning

## 21. Scientific Computing

Library:

```python
scipy
```

Know:

- Optimization
- Integration
- Interpolation
- ODE solvers

## 22. Visualization

Libraries:

- `matplotlib`
- `plotly`

Know:

- Line plots
- Scatter plots
- Histograms
- Animations

## 23. Serialization

Libraries:

- `json`
- `pickle`

Know:

- Saving models
- Saving simulations
- Configuration files

## 24. Engineering Libraries

Become familiar with:

- `numpy`
- `scipy`
- `sympy`
- `pandas`
- `matplotlib`

These form the foundation of scientific Python.

## 25. Professional Python Checklist

A professional computational engineer should be comfortable:

- [ ] Building CLI tools
- [ ] Writing reusable modules
- [ ] Using type hints
- [ ] Using dataclasses
- [ ] Working with NumPy
- [ ] Working with SciPy
- [ ] Profiling code
- [ ] Writing tests
- [ ] Reading documentation
- [ ] Building simulations
- [ ] Building optimization systems
- [ ] Visualizing results
- [ ] Debugging numerical issues
- [ ] Structuring medium-sized projects
- [ ] Using Git effectively

## Project

- Build a Unit Conversion Engine

## Completion Criteria

You have completed Module 1 when you can confidently build:

- Unit Conversion Engine
- Matrix Calculator
- Monte Carlo Simulator
- Projectile Motion Simulator
- City Reality Estimator

without relying heavily on AI assistance.

At that point, Python is no longer something you are learning. It becomes a
tool you use to solve engineering problems.
