---
title: python-note
tags: [python, note]
---

`__file__` return absolute path if not in sys.path, else return relative path

`__repr__` is designed for programmers while `__str__` is designed for users. `__str__` only changes the result of `print(a)` while `__repr__` changes the result of `a` in command line.

`__new__` is the real constructor. `__init__` is automatically called after `__new__`. See [here](https://juejin.im/post/5add4446f265da0b8d4186af).

Some interesting facts of variables names see [here](https://aji.tw/python你到底是在__底線__什麼啦/).

[Dot before modules](https://www.python.org/dev/peps/pep-0328/) like `from .mod import xxx` means import from the current package.

