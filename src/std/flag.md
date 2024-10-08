# std/flag

## Traits

```jule
trait CommonFlag {
    // Returns name of flag.
    fn Name(self): str

    // Returns short name of flag.
    fn Short(self): rune

    // Returns description of flag.
    fn What(self): str

    // Resets data to default.
    fn Reset(mut self)
}
```
Common behaviors of flags.

## Structures

```jule
struct FlagSet
```
Flag parser for command-line arguments.

**Methods:**

`static fn New(): &FlagSet`\
Returns new flagset.

`fn FindFlag(mut self, name: str): CommonFlag`\
Returns flag by name, returns nil if not exist.

`fn FindFlagShort(mut self, name: rune): CommonFlag`\
Returns flag by short name, returns nil if not exist.

`fn Flags(mut self): []CommonFlag`\
Returns all flags.

`fn Parse(mut self, args: []str)!: []str`\
Parse arguments and process flags. Returns non-flag content. Exceptional always is string and holds error message.

**Syntax:**

<ul>
Long names can be used with double dash (` -- `). Short names can be used with a single dash ( `-` ). When Boolean flags are used, they use the opposite of their default values. Floating-point values are the same as the `ParseFloat` function provided by the `std/conv` package. Decimal, octal, binary and hexadecimal formats are supported for signed and unsigned integer types. String types accept values ​​directly.

Octal values are represented by starts with 0o or `0` prefix. Hexadecimal values are represented by starts with `0x` prefix. Binary values are represented by starts with `0b` prefix.

 A space is required to give a value. When a single dash (-) is used, all following characters are considered short names and thus collective use is allowed. If the short name flags used need values, the values ​should follow respectively.
</ul>

`fn Reset(mut self)`\
Resets all flags to default value.

`fn Add[T: i64 | u64 | f64 | bool | str](mut self, name: str, short: rune, default: T, what: str): &T`\
Adds new flag and returns allocated reference variable. Panics if name or short name is alreadys exist. Zero (0) short names will be ignored. Panics if used unsupported type.

**Supported types are:**
- `i64`
- `u64`
- `f64`
- `str`
- `bool`

`fn AddVar[T: i64 | u64 | f64 | bool | str](mut self, mut var: &T, name: str, short: rune, what: str)`\
Same with add method but do not allocates new reference, uses existing.