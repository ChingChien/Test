# Python Style Guide

## Introduction
Python is the a scripting language used at. This style guide is a list of dos and don'ts 
for Python programs. In particular, it is based on [PEP 0008](https://www.python.org/dev/peps/pep-0008/) 
and the practice guide of [Google Python style guide](https://google.github.io/styleguide/pyguide.html).

In overall, *readability* and *consistency* are the keys for Python developers, in coding 
style. To help you format code correctly with Eclipse IDE, we've created a settings file 
`eclipse`. So that , you can import and let Eclipse apply the appropriate 
Additionally, it's highly recommended using pylint for style and syntax validation. 

## Table of Contents

  1. [Semicolons](#semicolons)
  1. [Line Length](#line-length)
  1. [Indentation](#indentation)
  1. [Blank Lines](#blank-lines)
  1. [Whitespace](#whitespace)
  1. [Comments](#comments)
  1. [Imports](#imports)
  1. [Naming](#naming)
  1. [Strings](#strings)
  1. [Source File Encoding](#source-file-encoding)
  1. [Programming Recommendations](#programming-recommendations)

## Semicolons

  - Do not terminate your lines with semicolons and do not use semicolons to put two or 
    more commands on the same line. However, you may put the result of a test on the same 
    line as the test only if the entire statement fits on one line.

**[⬆ back to top](#table-of-contents)**

## Line Length

  - Maximum line length is 80 characters.

  - Exceptions: 
  	* Long import statements
  	* URLs in comments
    
  - Avoid using backslash line continuation. The preferred way of wrapping long lines is 
    by using Python's implied line continuation inside parentheses, brackets and braces. 
    Long lines can be broken over multiple lines by wrapping expressions in parentheses.
    
    ```python
    # Examples of implicit line join inside parentheses, brackets and braces.
    foo = function_name(var_one, var_two,
                        var_three, var_four)
                                 
    if (temperature == 78 and city == 'LA' and
        wind == 10):
        
    my_str = ('This will create a very long long '
              'long long long long long long long string')
    ```

**[⬆ back to top](#table-of-contents)**

## Indentation

  - Use 4 spaces per indentation level. Never use tabs or mix tabs and spaces. 
    In cases of implied line continuation, you should align wrapped elements either 
    vertically, or using a hanging indent of 4 spaces, in which case there should be no 
    argument on the first line.
    
    ```python
    # Aligned vertically with opening delimiter
    foo = function_name(var_one, var_two,
                        var_three, var_four)
                             
	# Aligned with 4-space hanging indent; nothing (i.e., no argument) on first line
    foo = function_name(
        var_one, var_two, var_three,
        var_four)
    ```

**[⬆ back to top](#table-of-contents)**

## Blank Lines

  - Surround top-level function and class definitions with two blank lines.
  - Method definitions inside a class are surrounded by a single blank line.
  - Use blank lines in functions, sparingly, to indicate logical sections.
  
**[⬆ back to top](#table-of-contents)**

## Whitespace

  - Follow standard typographic rules for the use of spaces.
    * No whitespace inside parentheses, brackets or braces.
    
    ```python
    # Good 
    spam(ham[1], {eggs: 2}, [])

    # Bad
    spam( ham[ 1 ], { eggs: 2 }, [ ] )
    ```
    
    * No whitespace before a comma, semicolon, or colon. 
    
    ```python
    # Good 
    if x == 6:
        print x, y

    # Bad
    if x == 6:
        print x , y
    ```
    * No whitespace before the open paren/bracket that starts an argument list, indexing 
      or slicing.
    
    ```python
    # Good 
    spam(1)
    dict['key'] = list[2]

    # Bad
    spam (1)
    dict['key'] = list [2]
    ```    
    * Surround binary operators with a single space on either side for assignment (=), 
      comparisons (==, <, >, !=, <>, <=, >=, in, not in, is, is not), and Booleans (and, 
      or, not).
    
    ```python
    # Good 
    x == 1

    # Bad
    x==1
    ```    
    * Don't use spaces around the '=' sign when used to indicate a keyword argument or a 
      default parameter value.
    
    ```python
    # Good 
    def function_name(real, imag=0.0): return another_function(r=real, i=imag)

    # Bad
    def function_name(real, imag = 0.0): return another_function(r = real, i = imag)
    ```
    
    * Avoid trailing whitespace anywhere.
    

**[⬆ back to top](#table-of-contents)**

## Comments

	Comments should be complete sentences. If a comment is a phrase or sentence, its first 
	word should be capitalized, unless it is an identifier that begins with a lower case 
	letter. If a comment is short, the period at the end can be omitted. Block comments 
	generally consist of one or more paragraphs built out of complete sentences, and each 
	sentence should end in a period.
	
  - Inline Comments: An inline comment is a comment on the same line as a statement. 
    Inline comments should be separated by at least two spaces from the statement. They 
    should start with a # and a single space.
    
  - Block Comments: Block comments generally apply to some (or all) code that follows 
  	them, and are indented to the same level as that code. Each line of a block comment 
  	starts with a # and a single space (unless it is indented text inside the comment). 
  	Paragraphs inside a block comment are separated by a line containing a single # .
  
  - Documentation Strings (a.k.a. "docstrings"): Write docstrings for all public modules, 
    functions, classes, and methods. Docstrings are not necessary for non-public methods, 
    but you should have a comment that describes what the method does. This comment should
    appear after the def line. Use the three double-quote """ format for doc strings.
    
    ```python
    # Example for functions and methods 
    def fetch_db_rows(table_name, keys):
    """Fetches rows from a table.

    Retrieves rows pertaining to the given keys from the table instance

    Args:
        table_name: A table instance.
        keys: A string representing the key of each table row
            to fetch.        

    Returns:
        A dict mapping keys to the corresponding table row data
        fetched. Each row is represented as a tuple of strings. For
        example:

        {'temperature': ('celsius', 'fahrenheit'),
         'wind': ('km', 'mile')}

        If a key from the keys argument is missing from the dictionary,
        then that row was not found in the table.

    Raises:
        IOError: An error occurred accessing the table object.
    """
    pass
    ```
    
    ```python
    # Example for classes 
    class Weather(object):
    """Summary of Weather class here.

    Additional class information....
    Additional class information....

    Attributes:
        temperature: A numeric value indicating current weather temperature.
    """

    def __init__(self, temperature):
        """Inits Weather with blah."""
        self.temperature = temperature

    def public_method_get_temperature(self):
        """Performs operation blah."""
    ```

  - TODO Comments: Use TODO comments for code that is temporary, a short-term,  
    good-enough, but not perfect solution. TODOs should include the string TODO in all 
    caps, followed by the e-mail address (in parentheses), or other identifier of the 
    person who can provide context about the problem referenced by the TODO. 
    A comment explaining what there is to do is required. The main TODO purpose is 
	to have a consistent format that can be searched to find the person who can provide 
	more details upon request. Note a TODO is not a commitment that the person referenced 
	will fix the problem.
	
	```python
    # TODO(xyz@surfline.com): Improve this algorithm using advanced sorting approach.
    ```
  	
**[⬆ back to top](#table-of-contents)**

## Imports

  - Imports should be on separate lines and are always put at the top of the file, just 
    after any module comments and doc strings and before module globals and constants. 
    Imports should be grouped with the order being most generic to least generic as below.
    * standard library imports
    * related third-party imports
    * local application-specific imports
    You should put a blank line between each group of imports.
    
  - Absolute imports are recommended, as they are usually more readable and tend to be 
    better behaved (or at least give better error messages).
    
    ```python
    import surfline.weather
    from surfline.weather import wind
    ```

  - Avoid using wildcard imports.

**[⬆ back to top](#table-of-contents)**

## Naming

  - Overall Naming Convention:
  	* Prepending a single underscore `(_)` has some support for protecting module variables 
  	  and functions (not included with import * from)
  	* Prepending a double underscore `(__)` to an instance variable or method effectively 
  	  serves to make the variable or method private to its class.
  	* Place related classes and top-level functions together in a module.
  	* Use CapWords for class names, but lower_with_under.py for module names.
  	
  - Naming Summary (guidelines derived from Guido's recommendations):
  
	Type		               | Pubic	    		| Internal			   |	
	-------------------------- | ------------------ | -------------------- |
	Packages	               | lower_with_under   | 					   | 	
	Modules		               | lower_with_under   | _lower_with_under    |
	Classes		               | CapWords		    | _CapWords		       |	
	Exceptions				   | CapWords           | _lower_with_under    |  	
	Functions		  		   | lower_with_under() | _lower_with_under()  |
	Global/Class Constants     | CAPS_WITH_UNDER    | _CAPS_WITH_UNDER     |	
	Global/Class Variables	   | lower_with_under   | _lower_with_under    |	
	Instance Variables		   | lower_with_under   | _lower_with_under (protected) or __lower_with_under (private)   |	
	Method Names		       | lower_with_under() | _lower_with_under() (protected) or __lower_with_under() (private)   |	
	Function/Method Parameters | lower_with_under   | _lower_with_under    |	
	Local Variables		       | lower_with_under   | _lower_with_under    |
	
	Note: "Internal" means internal to a module or protected or private within a class.
				
**[⬆ back to top](#table-of-contents)**

## Strings

  - Single-quoted strings and double-quoted strings are the same. PEP 8 does not make a 
    recommendation for this. However, in general, you should apply the following rules.
    * Use double quotes for text
    * Use single quotes for anything that behaves like an identifier (i.e., symbol-like 
      strings)

  - When a string contains single or double quote characters, use the other one to avoid 
    backslashes in the string. It improves readability.
    
  - Use the format method or the % operator for formatting strings. Use your best 
    judgement to decide between + and % (or format) though.
    
    ```python
    x = a + b
    x = '%s, %s!' % (message1, message2)
    x = '{}, {}!'.format(message1, message2)
    x = 'name: %s; score: %d' % (name, n)
    x = 'name: {}; score: {}'.format(name, n)    
    ```

**[⬆ back to top](#table-of-contents)**

## Source File Encoding

  - Code in the core Python distribution should always use UTF-8.
  
    ```python
    # In source header you can declare encoding as below.
    # -*- coding: utf-8 -*-
    ```
    
**[⬆ back to top](#table-of-contents)**

## Programming Recommendations

  The following recommendations includes a subset from [PEP 0008](https://www.python.org/dev/peps/pep-0008/#programming-recommendations) 
  and [Google Python style guide](https://google.github.io/styleguide/pyguide.html#Python_Language_Rules).

  - Comparisons to singletons like `None` should always be done with `is` or `is not` , 
    never the equality operators.
  - Use `is not` operator rather than `not ... is` .
  - Always use a `def` statement instead of an assignment statement that binds a `lambda` 
    expression directly to an identifier.
  - Derive exceptions from `Exception` rather than `BaseException`.
  - Use exception chaining appropriately.
  - When raising an exception in Python 2, use `raise ValueError('message')` instead of 
    the older form `raise ValueError, 'message'` .
  - When catching exceptions, mention specific exceptions whenever possible instead of 
    using a bare `except:` clause. 
  - When a resource is local to a particular section of code, use a `with` statement to 
    ensure it is cleaned up promptly and reliably after use. A `try/finally` statement 
    is also acceptable.
  - Use `''.startswith()` and `''.endswith()` instead of string slicing to check for 
    prefixes or suffixes.
  - Don't write string literals that rely on significant trailing whitespace. 
  - Object type comparisons should always use isinstance() instead of comparing types 
    directly.
    
    ```python
    # Good
    if isinstance(obj, int):
    
    # Bad
    if type(obj) is type(1):
    ```
    
  - Don't compare boolean values to True or False using == .
  	
  	```python
    # Good
    if greeting:
    
    # Bad
    if greeting == True:
    ```

  - Run `pylint` or `pep8` over your code.
  - Avoid global variables.
  - List comprehensions are okay to use for simple cases. Complicated list comprehensions 
    or generator expressions can be hard to read.
  
    
**[⬆ back to top](#table-of-contents)**

