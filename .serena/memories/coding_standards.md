# OpenTTD Coding Standards

## General Principles
- Everything must be documented
- Code should be reviewable and understandable by others
- Performance matters, but code clarity is also important
- Documentation helps with code reviews and maintenance

## Functions
- **Naming:** CamelCase without underscores
- **Braces:** Opening `{` on next line
- **Parameters:** Use `Foo()` instead of `Foo(void)`
- **Const:** Prefer const for reference and compound parameters
- **Member functions:** Make const when possible

```cpp
void ThisIsAFunction()
{
}
```

## Variables
- **Naming:** All lowercase with `_` separators
- **Global variables:** Preceded by underscore `_`
- **Class members:** Always reference with `this->`
- **Pointers/References:** Symbol next to name (`Vehicle *v`)
- **Alignment:** Type, name, assignment operator aligned by spaces
- **Declaration:** Upon first usage, iterators in their loop
- **Standard names:** `Vehicle *u, *v, *w; Station *st; Town *t; Window *w; Engine *e`

```cpp
int     number         = 10;
Vehicle *u_first_wagon = v->next;
uint32  _global_variable = 3750;
```

## Enumerations
- **Enum names:** CamelCase
- **Unscoped values:** ALL_CAPS with underscores
- **Scoped values:** CamelCase
- **Values:** Consecutive numbers OR consecutive powers of two (hex or shift operator)
- **Special values:** `_BEGIN`, `_END`, `INVALID_` (invalid = 0xFF/0xFFFF/0xFFFFFFFF)

```cpp
enum DiagDirection {
    DIAGDIR_BEGIN = 0,
    DIAGDIR_NE  = 0,
    DIAGDIR_SE  = 1,
    DIAGDIR_SW  = 2,
    DIAGDIR_NW  = 3,
    DIAGDIR_END,
    INVALID_DIAGDIR = 0xFF,
};
```

## Documentation Requirements
- All code must be documented
- Complex parts require detailed explanations
- Comments should explain WHY, not just WHAT
- Documentation makes code review easier