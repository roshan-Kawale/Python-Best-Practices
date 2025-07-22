## Python Docstrings and Comments: Best Practices

Effective documentation is a cornerstone of maintainable, readable, and collaborative Python code. **Docstrings** and **comments** serve distinct but complementary roles in achieving this. This document outlines best practices for using both, with an emphasis on principles often adopted in Google's Python style guide.

### 1. Docstrings (Documentation Strings)

Docstrings are string literals that occur as the first statement in a module, function, class, or method definition. They are used to explain the purpose and usage of the code block they document. Unlike regular comments, docstrings are accessible at runtime via the `__doc__` attribute and are used by tools like `help()` and IDEs for introspection.

#### Purpose:

* To provide a high-level overview of what a module, class, function, or method does.

* To describe its arguments, return values, and any exceptions it might raise.

* To offer usage examples.

#### Placement:

* **Modules**: Immediately after the module's `import` statements.

* **Classes**: Immediately after the class definition line.

* **Functions/Methods**: Immediately after the `def` line.

#### Formatting:

* Always use **triple double quotes (`"""Docstring goes here"""`)**.

* **Single-line docstrings**: For very brief explanations that fit on one line.

  ```python
  def add(a, b):
      """Returns the sum of two numbers."""
      return a + b
  ```

* **Multi-line docstrings**: For more complex explanations.

  * The first line should be a concise summary of the object's purpose, ending with a period.

  * Leave a blank line after the summary.

  * Follow with a more detailed description, including sections for arguments, return values, and exceptions.

#### Content:

Google's Python Style Guide suggests a structured approach for multi-line docstrings, particularly for functions and methods:

* **Summary Line**: A concise, one-line summary of what the function/class does.

* **Detailed Description**: More in-depth explanation if needed.

* **`Args:`**: List each argument by name, followed by its type in parentheses, a colon, and a description.

  * Example: `Args: name (str): The name of the user.`

* **`Returns:`**: Describe the return value, including its type.

  * Example: `Returns: bool: True if the operation was successful, False otherwise.`

* **`Yields:`**: (For generators) Describe what values are yielded.

* **`Raises:`**: List any exceptions that might be raised, followed by a description of the circumstances.

  * Example: `Raises: ValueError: If the input is negative.`

* **`Example:`**: Provide a small code snippet demonstrating usage.

**Example Multi-line Docstring:**

```python
def calculate_area(length, width):
    """Calculates the area of a rectangle.

    This function takes the length and width of a rectangle and returns its area.
    It handles non-positive dimensions by raising a ValueError.

    Args:
        length (float): The length of the rectangle. Must be positive.
        width (float): The width of the rectangle. Must be positive.

    Returns:
        float: The calculated area of the rectangle.

    Raises:
        ValueError: If `length` or `width` is not positive.

    Example:
        >>> calculate_area(5, 10)
        50.0
        >>> calculate_area(0, 5)
        Traceback (most recent call last):
            ...
        ValueError: Dimensions must be positive.
    """
    if length <= 0 or width <= 0:
        raise ValueError("Dimensions must be positive.")
    return length * width

class User:
    """Represents a user in the system.

    Attributes:
        name (str): The name of the user.
        email (str): The email address of the user.
    """
    def __init__(self, name, email):
        """Initializes a new User object.

        Args:
            name (str): The name of the user.
            email (str): The email address of the user.
        """
        self.name = name
        self.email = email
```

### 2. Comments

Comments are used to explain *how* and *why* specific pieces of code work. They are primarily for developers reading the source code and are ignored by the Python interpreter.

#### Purpose:

* To clarify complex or non-obvious logic.

* To explain the reasoning behind a particular design choice.

* To temporarily disable code during development.

* To add notes for future improvements (`TODO`, `FIXME`).

#### When to Use Comments:

* **Complex Algorithms**: Explain the steps of a non-trivial algorithm.

* **Workarounds/Hacks**: Document why a particular workaround is necessary.

* **Assumptions**: State any assumptions made about input data or system state.

* **Future Work**: Use `TODO:` or `FIXME:` to mark areas that need attention.

* **Business Logic**: Explain the real-world context behind a piece of code.

#### When *Not* to Use Comments:

* **Obvious Code**: Don't state the obvious. `x = x + 1 # Increment x` is redundant.

* **Restating Code**: If the code is self-explanatory due to good naming and clear structure, a comment is often unnecessary.

* **Outdated Comments**: Keep comments up-to-date with code changes. Outdated comments are worse than no comments.

#### Formatting:

* Start comments with a hash symbol (`#`).

* Leave at least two spaces before an inline comment.

* For block comments, start each line with `#` and a single space.

* Keep comments concise and to the point.

**Example Comments:**

```python
def process_data(data_list):
    """Processes a list of numerical data."""
    processed_items = []
    # Iterate through each item, skipping any non-numeric entries.
    for item in data_list:
        if not isinstance(item, (int, float)):
            # Log a warning for invalid data types
            print(f"Warning: Skipping non-numeric item: {item}")
            continue

        # Apply a transformation: square the number if it's positive,
        # otherwise negate it. This handles both positive and negative
        # inputs consistently for the next step.
        if item >= 0:
            transformed_item = item ** 2
        else:
            transformed_item = -item

        processed_items.append(transformed_item)

    # TODO: Add error handling for empty data_list before calculating average.
    # This average represents the mean of the transformed values.
    return sum(processed_items) / len(processed_items)
```

### 3. Key Differences: Docstrings vs. Comments

| Feature | Docstrings | Comments |
|---|---|---|
| **Purpose** | Explain *what* a code block does (API). | Explain *how* or *why* specific code works. |
| **Placement** | First statement of a definition. | Anywhere in the code. |
| **Runtime** | Accessible via `__doc__`, used by `help()`. | Ignored by interpreter. |
| **Audience** | Users of the code (APIs) and developers. | Primarily developers maintaining the code. |
| **Tools** | Used by documentation generators (Sphinx). | Not typically used by doc generators. |