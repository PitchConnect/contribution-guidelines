# Coding Standards

This document outlines the coding standards for all PitchConnect projects.

## Table of Contents

- [Python Style Guidelines](#python-style-guidelines)
- [Docstrings](#docstrings)
- [Type Hints](#type-hints)
- [Naming Conventions](#naming-conventions)
- [Code Organization](#code-organization)
- [Testing Standards](#testing-standards)
- [Linting and Formatting](#linting-and-formatting)

## Python Style Guidelines

All Python code should follow [PEP 8](https://www.python.org/dev/peps/pep-0008/) with the following specifics:

- Use 4 spaces for indentation (no tabs)
- Maximum line length of 100 characters
- Use single quotes for strings unless double quotes avoid backslashes
- Use parentheses for line continuation rather than backslashes when possible
- Add a blank line at the end of each file
- Use two blank lines before top-level classes and functions
- Use one blank line before class methods

## Docstrings

All modules, classes, and functions should have docstrings. We follow the [Google style docstrings](https://sphinxcontrib-napoleon.readthedocs.io/en/latest/example_google.html) format.

### Module Docstrings

```python
"""Module description.

Detailed description of the module's purpose and functionality.
"""
```

### Function/Method Docstrings

```python
def function_name(param1: type, param2: type) -> return_type:
    """Short description of the function.

    More detailed description of what the function does and any
    important information about its behavior.

    Args:
        param1: Description of param1
        param2: Description of param2

    Returns:
        Description of the return value

    Raises:
        ExceptionType: When and why this exception is raised
    """
```

### Class Docstrings

```python
class ClassName:
    """Short description of the class.

    More detailed description of what the class does and any
    important information about its behavior.

    Attributes:
        attr1: Description of attr1
        attr2: Description of attr2
    """
```

## Type Hints

Use type hints for all function parameters and return values:

```python
def process_data(data: List[Dict[str, Any]], limit: Optional[int] = None) -> Dict[str, List[str]]:
    """Process the input data.

    Args:
        data: The data to process
        limit: Optional limit on processing

    Returns:
        Processed data as a dictionary
    """
```

Common imports for type hints:

```python
from typing import Dict, List, Optional, Union, Any, Tuple, Callable, TypeVar, Generic
```

## Naming Conventions

- **Packages and Modules**: Short, lowercase names. Underscores can be used if needed: `my_package`, `my_module`
- **Classes**: CapWords (PascalCase): `MyClass`, `NetworkClient`
- **Functions and Methods**: lowercase with underscores (snake_case): `my_function`, `calculate_total`
- **Variables**: lowercase with underscores: `my_variable`, `total_count`
- **Constants**: ALL_CAPS with underscores: `MAX_RETRIES`, `DEFAULT_TIMEOUT`
- **Private Methods/Attributes**: Prefix with underscore: `_private_method`, `_internal_attribute`

## Code Organization

Organize imports in the following order, with a blank line between each group:

1. Standard library imports
2. Related third-party imports
3. Local application/library specific imports

Example:

```python
import os
import sys
from datetime import datetime

import requests
from sqlalchemy import Column, Integer

from myproject.models import User
from myproject.utils import format_date
```

## Testing Standards

- All new features should include tests
- Bug fixes should include regression tests
- Use pytest for testing
- Aim for high test coverage of critical functionality
- Tests should be independent and repeatable

### Test Structure

```python
def test_function_name_scenario_being_tested():
    """Test that function_name does X when Y."""
    # Arrange
    input_data = ...
    
    # Act
    result = function_name(input_data)
    
    # Assert
    assert result == expected_output
```

## Linting and Formatting

Use the following tools to ensure code quality:

- **black**: For code formatting
- **isort**: For import sorting
- **flake8**: For linting
- **mypy**: For type checking

Configure these tools in your project's `pyproject.toml` or appropriate configuration files.

Example pre-commit configuration:

```yaml
repos:
-   repo: https://github.com/pre-commit/pre-commit-hooks
    rev: v4.4.0
    hooks:
    -   id: trailing-whitespace
    -   id: end-of-file-fixer
    -   id: check-yaml
    -   id: check-added-large-files

-   repo: https://github.com/psf/black
    rev: 23.3.0
    hooks:
    -   id: black

-   repo: https://github.com/pycqa/isort
    rev: 5.12.0
    hooks:
    -   id: isort

-   repo: https://github.com/pycqa/flake8
    rev: 6.0.0
    hooks:
    -   id: flake8
        additional_dependencies: [flake8-docstrings]

-   repo: https://github.com/pre-commit/mirrors-mypy
    rev: v1.3.0
    hooks:
    -   id: mypy
        additional_dependencies: [types-requests]
```
