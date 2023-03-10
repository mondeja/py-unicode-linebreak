# py-unicode-linebreak

Python bindings for the Rust crate [unicode-linebreak].

## Installation

```bash
pip install unicode-linebreak
```

## Usage

```python
from unicode_linebreak import linebreaks, Allowed, Mandatory

s = 'a b\nc\r\nd e\rf end'
expected_result = [
    (2, Allowed), (4, Mandatory), (7, Mandatory), (9, Allowed),
    (11, Mandatory), (13, Allowed), (16, Mandatory)
]
assert list(linebreaks(s)) == expected_result
```

Returns an iterator which iterates over tuples with the
binary character position of the linebreak and a boolean
indicating whether the linebreak is a mandatory break.

```python
# the end of the string is always a mandatory break
assert list(linebreaks(s))[-1] == (0, Mandatory)

# Mandatory and Allowed are just boolean values
assert expected_result[0][1] is Allowed is False
assert expected_result[-1][1] is Mandatory is True
```

> Note that the binary character position is not the same
> as the readable character index, but the binary position.
> See the Rust method on strings [`char_indices()`].

## Contribute

```bash
python -m virtualenv venv
source venv/bin/activate
pip install -r dev-requirements.txt
maturin develop && python -m unittest
```

[unicode-linebreak]: https://crates.io/crates/unicode-linebreak
[`char_indices()`]: https://doc.rust-lang.org/std/primitive.str.html#method.char_indices
