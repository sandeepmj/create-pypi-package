# Creating a PyPI Package: my_functions_demo_sandeepj

At some point you realize that you are using the same functions for different coding projects. For example you might use a ```timer``` function to slow down your scrape.

Instead of copying and pasting the timer code every time, let's simply pip install it 


---

## Step 1: Create Project Structure

Create the following folder structure:

```
my_functions_demo/
├── src/
│   └── my_functions_demo/
│       ├── __init__.py
│       └── functions.py
├── pyproject.toml
├── README.md
└── LICENSE
```

---

## Step 2: Create Package Files

### File: `src/my_functions_demo/__init__.py`

```python
"""Demo package with utility functions."""
__version__ = "0.1.0"

from .functions import addNumbers, timer

__all__ = ["addNumbers", "timer"]
```

### File: `src/my_functions_demo/functions.py`

```python
import time
from random import uniform


def addNumbers(number1, number2):
    """
    Provide two numbers and I'll add them together
    """
    return (number1 + number2)


def timer(start_time, end_time):
    """
    Timer to snooze while scraping
    Para_1: start_time: integer for minimum seconds snooze
    Para_2: end_time: integer for maximum seconds snooze
    """
    snoozer = uniform(start_time, end_time)
    print(f"Snoozing for {snoozer} seconds!")
    time.sleep(snoozer)
```

---

## Step 3: Create Configuration File

### File: `pyproject.toml`

```toml
[build-system]
requires = ["setuptools>=61.0", "wheel"]
build-backend = "setuptools.build_meta"

[project]
name = "my_functions_demo_sandeepj"
version = "0.1.0"
authors = [
    {name = "Your Name", email = "your.email@example.com"}
]
description = "Demo package with utility functions"
readme = "README.md"
requires-python = ">=3.7"
classifiers = [
    "Programming Language :: Python :: 3",
    "License :: OSI Approved :: MIT License",
    "Operating System :: OS Independent",
]

[project.urls]
Homepage = "https://github.com/yourusername/my-functions-demo"
```

---

## Step 4: Create README.md

Create a `README.md` file for your package:

```markdown
# my_functions_demo

A simple demo package with utility functions.

## Installation

```bash
pip install my_functions_demo_sandeepj
```

## Usage

### Add Numbers
```python
from my_functions_demo import addNumbers

result = addNumbers(5, 10)
print(result)  # Output: 15
```

### Timer (for scraping delays)
```python
from my_functions_demo import timer

# Sleep for random time between 1 and 3 seconds
timer(1, 3)
```

## Functions

- `addNumbers(number1, number2)`: Adds two numbers together
- `timer(start_time, end_time)`: Sleeps for random duration between start_time and end_time seconds
```

---

## Step 5: Create LICENSE File

Create a `LICENSE` file with MIT License text. You can get the full text from [https://choosealicense.com/licenses/mit/](https://choosealicense.com/licenses/mit/)

---

## Step 6: Install Build Tools

```bash
pip install build twine
```

---

## Step 7: Build Your Package

From the `my_functions_demo/` directory, run:

```bash
python -m build
```

This creates a `dist/` folder with `.whl` and `.tar.gz` files.

---

## Step 8: Create PyPI Accounts

Register for both accounts:

- **Test PyPI**: [https://test.pypi.org/account/register/](https://test.pypi.org/account/register/)
- **Real PyPI**: [https://pypi.org/account/register/](https://pypi.org/account/register/)

---

## Step 9: Upload to Test PyPI (Recommended)

```bash
python -m twine upload --repository testpypi dist/*
```

Enter your Test PyPI username and password when prompted.

---

## Step 10: Test Installation

```bash
pip install --index-url https://test.pypi.org/simple/ my_functions_demo_sandeepj
```

Test the functions:

```python
from my_functions_demo import addNumbers, timer

print(addNumbers(10, 5))  # Should print 15
timer(1, 2)  # Should sleep for 1-2 seconds
```

---

## Step 11: Upload to Real PyPI

```bash
python -m twine upload dist/*
```

Enter your PyPI credentials when prompted.

---

## Step 12: Install from Anywhere!

```bash
pip install my_functions_demo_sandeepj
```

Now anyone can use your functions:

```python
from my_functions_demo import addNumbers, timer

# Add numbers
result = addNumbers(100, 50)
print(result)  # 150

# Random delay between 2-5 seconds (useful for web scraping)
timer(2, 5)
```

---

## Quick Command Reference

```bash
# Build the package
python -m build

# Upload to Test PyPI
python -m twine upload --repository testpypi dist/*

# Test install
pip install --index-url https://test.pypi.org/simple/ my_functions_demo_sandeepj

# Upload to real PyPI
python -m twine upload dist/*

# Final install (from anywhere!)
pip install my_functions_demo_sandeepj
```

---

## Important Notes

- Package names must be unique on PyPI
- Consider using API tokens instead of passwords (available in PyPI account settings)
- Add a `.gitignore` file to exclude: `dist/`, `build/`, `*.egg-info/`, `__pycache__/`
- Users don't need to import `time` or `random` - these are handled inside your package
- Both functions will work immediately after pip install with no additional setup

---

## Congratulations! 🎉

Your package is now available worldwide via pip!
