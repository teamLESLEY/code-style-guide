# Team LES-Ley Code Style Guide
Heavily inpsired by [Clean Code](https://www.goodreads.com/book/show/3735293-clean-code) by Robert C. Martin, [PEP 8](https://www.python.org/dev/peps/pep-0008/), and [Black](https://github.com/psf/black/blob/master/docs/the_black_code_style.md). In general, most things in PEP 8 apply.

For clarity, `()` are parentheses, `[]` are brackets, and `{}` are braces. Justification is sometimes given when there are good reasons, other times things are arbitrary but a choice had to be made.

## Rule #1
Clarity and consitency is the goal. If a rule is getting in the way of writing clear code, ignore the rule. On the other hand, think very carefully before ignoring a rule.

## The Basics
- Indent two spaces
- Use the One True Brace Style everywhere, including method declarations:
  ```c++
  if (foo) {
     bar;
  }
  ```
- Short lines are good. Soft limit at 80 characters and hard limit at 100 characters
- Explicit is better than implicit, clear is more important than concise.
- Refactor, refactor, refactor
- Prefer to keep physical quantities in SI units (kg, m, s, J, and so on). For the love of god, never use imperial units.
- The compiler is smarter than you. If you can do the same task in a long, clear way or a shorter but possibly faster way, choose the longer way every time. The compiler will almost certainly optimize away any difference between the two.
- Avoid manual memory management if you can at all help it. That way lies bugs and madness: around 70% of bugs in [Chrome](https://www.chromium.org/Home/chromium-security/memory-safety) and [Microsoft](https://www.zdnet.com/article/microsoft-70-percent-of-all-security-bugs-are-memory-safety-issues/) are memory errors.

## Names
- Names should be descriptive. A variable name should tell me what the variable is, a function name should tell me what it does.
  - For example, `x` tells me nothing, while `canWidth` tells that the variable is the width of a can.
  - A single letter is almost never a good variable name (the obvious exception is `i` for an index counter in a loop).
- Don't go crazy, but make names as long as needed to be clear.
- Avoid abbreviations except for extremely common ones (e.g. "num" for "number"). 

Casing conventions
- Variables: `camelCase`
- Constants: `ALL_CAPS`
- Functions: `snake_case`
- Classes and namespaces: `UpperCamelCase`
- Methods: `camelCase`
- Files: `lowerCamelCase.ext`

## Spacing
- Always put a space on either side of a binary operator: `a + b`, not `a+b`
- Never put a space between a unary operator and its operand: `~a`, not `~ a`
- Never put a space before a function call or array indexing: `foo()` and `bar[i]`, not `foo ()` and `bar []`
- Never put spaces before commas, after an opening parenthesis, or before a closing parenthesis
- Don't use extra spaces to align multiple assignments or similar. This is irritating to maintain in the long run and provides only arguable readability.
  ```c++
  // Good
  int i = 0;
  int foo = 1;
  int spam = 2;
  int heyThisIsAReallyLongName = 3;
  
  // Bad
  int i                        = 0;
  int foo                      = 1;
  int spam                     = 2;
  int heyThisIsAReallyLongName = 3;
  ```
- If a line is getting too long, prefer to break before a binary operand rather than after:
  ```c++
  // Good
  int a = (foo + bar + baz
           + qux + spam + eggs);
          
  // Bad
  int a = (foo + bar + baz +
           qux + spam + eggs)
  ```
- Break long lists (whether array initializers, function arguments, or some other list) with one element per line and the closing punctuation on its own line.
  ```c++
  char* lyrics[] = {
    "When the cold of winter comes",
    "Starless night will cover day",
    "In the veiling of the sun",
    "We will walk in bitter rain",
    "But in dreams",
    "I can hear your name",
    "And in dreams",
    "We will meet again",
    "When the seas and montains fall",
    "And we come to end of days",
    "In the dark I hear a call",
    "Calling me there",
    "I will go there",
    "And back again"
  };
  ```
  - If the individual elements aren't very long or there's a natural grouping, combine and vertically align them as reasonable.
    ```c++
    int wholeNumbers[] = {
       0,  1,  2,  3,  4,  5,  6,  7,  8,  9,
      10, 11, 12, 13, 14, 15, 16, 17, 18, 19,
      20, 21, 22, 23, 24, 25, 26, 27, 28, 29
    };
    ```
- Vertical whitespace (blank lines) is your friend. Use a single blank line to visually separate logically distinct parts of the code.
  - In general, avoid blank lines in a function. If a function is long enough that a blank line improves readability, that is a sign it does too much.
  
## Declarations and types
- Declare one variable per line. This avoids unexpected type issues with pointers.
- Use `unsigned` when it doesn't make sense for a variable to have a negative value.
- When declaring a pointer or reference, the `*` or `&` goes on the type, not the name:
  ```c++
  int* spam; // Good
  int *spam; // Bad
  ```

## Flow control
- Always put a space between the control keyword and opening parenthesis and between the closing parenthesis and opening brace
- Always put braces around the scope of a keyword, even if it is only one line.
- Use cuddled else

```c++
if (foo) {
  bar();
  baz();
} else {
  qux();
}
```

## Functions and methods
- A function should do one thing only.
- Avoid side-effects.
- Functions should be short - a general rule of thumb is less than 15 lines
- The name of the function should describe everything it does (but not *how* it does it). If the function name is really long because of this rule, that's a good sign the function is doing too many things.
- It's OK to have functions that are only called once
- Every single time an array is passed to a function, it's length must also be passed:
  ```c++
  int sum(int numbers[], unsigned int length) {
    //...
  }
  ```

Nitpicky bits
- The opening brace goes on the same line as the function declaration
- When giving an argument a default value, don't put spaces around the `=`

```c++
int power(int base, unsigned int exponent=2) {
  // ...
}
```

## Classes
- Obey the single responsibility principle: a class should do one thing only. If a class gets too big and starts doing multiple things, break it up into smaller classes. Don't be afraid to refactor!
- Declare parameters and methods in order of decreasing privacy.
- Don't indent privacy specifiers.
  ```c++
  class Foo {
    int bar;
    int Baz();
  
  protected:
    char Foo();
    
  public:
    C();
    C(int spam);
  }
- Always use public inheritance (this is how you would expect inheritance to work from Java and Python).
- A class that consists of a constructor and a method is not a class, it is a function (see https://www.youtube.com/watch?v=o9pEzgHorH0).

## Namespaces
- Consider putting groups of related classes and functions in a namespace to help avoid name clashes.
- On the other hand, remember that the purpose of namespaces is to avoid name clashes between modules, not to establish hierarchies (unlike Java packages).
- Consider very carefully before `using namespace Foo;` and never `using namespace std;`. Strongly prefer just using the namespace every time or `using Foo::Bar;` instead.
  - Never `using namespace Foo;` in a header file: this dumps the entire contents of Foo into the global namespace of that header, every file that includes that header, and every file that includes a file that includes that header
  - The excpetion to avoiding `using namespace Foo;` is in the `foo.cpp` file implementing the names defined in `foo.hpp`.
  - Best
    ```c++
    #include "foo.hpp"
    
    int main() {
      Foo::Bar();
    }
    ```
  - Acceptable
    ```c++
    #include "foo.hpp"
    using Foo::Bar;
    
    int main() {
      Bar();
    }
    ```
  - Almost never
    ```c++
    #include "foo.hpp"
    using namespace Foo;
    
    int main() {
      Bar();
    }
    ```

## Miscellaneous
- Avoid macros (`#define`) like the plague. Macro functions especially are almost always evil.
- Only use unary increment and decrement in their own statement:
  ```c++
  // Do this
  list[i];
  i++;
  
  // Not this
  list[i++];
  list[++i];
  ```
  It's difficult to remember whether the value of the expression is taken before or after the variable is incremented, so avoid the issue entirely.
- All files should be encoded UTF-8.
