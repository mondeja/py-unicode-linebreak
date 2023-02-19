# py-unicode-linebreak

Python bindings for the Rust crate [unicode-linebreak].

## Installation

```bash
pip install unicode-linebreak
```

## Usage

```python
from unicode_linebreak import linebreaks

string = 'a b\nc\r\nd e\rf end'
expected_result = [
    (2, False), (4, True), (7, True), (9, False),
    (11, True), (13, False), (16, True)
]
assert list(linebreaks(string)) == expected_result
```

Returns an iterator which iterates over tuples with the
binary character position of the linebreak and a boolean
indicating whether the linebreak is a mandatory break.

> Note that the binary character position is not the same
> as the readable character index, but the binary position.
> See the Rust method on strings [`char_indices()`].

Also includes two variables to write a more readable version
of your code:

```python
from unicode_linebreak import Allowed, Mandatory

assert Allowed is False
assert Mandatory is True
```

## Contribute

```bash
python -m virtualenv venv
source venv/bin/activate
pip install -r dev-requirements.txt
maturin develop && python -m unittest
```

[unicode-linebreak]: https://crates.io/crates/unicode-linebreak
[`char_indices()`]: https://doc.rust-lang.org/std/primitive.str.html#method.char_indices
