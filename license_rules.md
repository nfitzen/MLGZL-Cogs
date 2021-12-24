<!-- SPDX-License-Identifier: CC-BY-SA-4.0 -->
<!-- Copyright (C) 2021 nfitzen <https://github.com/nfitzen> -->

# License Rules

These are the recommended procedures for marking licenses and copyright
notices.

## Copyright notices

### The README

There are 2 options for the copyright notice in the [README](README.md):

1. Listing all contributors' names.
2. Using an "and \<project-name\> contributors" notice.

So if this repo had 2 files with:

- Copyright &copy; 2021 nfitzen and Alice
- Copyright &copy; 2022 Joe and Bob

The README's copyright notice would contain both copyright notices verbatim.

Or, alternatively, it could combine them into
"Copyright &copy; 2021-2022 nfitzen and the \<project-name\> contributors."
Such a combination combines the years and names. See the following
section for information on how to list years.

### Copyright notice rules

The list of copyright years must only include all years in which a version
of that file was published.

For instance, a file version published in 2018 and then in 2021 must contain
"Copyright &copy; 2018, 2021 \<names\>."

A consecutive range of years may be denoted with a `-`.
So if one version was published in 2018, one in 2019, and one in 2020,
that file would read "Copyright &copy; 2018-2020 \<names\>."

The copyright notice should only contain years when code currently in the file
was published.

For instance, if nfitzen makes a file with 1 function in 2021, this is what
it'd look like:

```python
# SPDX-FileCopyrightText: AGPL-3.0-or-later
# Copyright (C) 2021 nfitzen <https://github.com/nfitzen>

def add(a: float, b: float):
    "Adds 2 numbers."
    return a + b
```

Then if Bob makes another function in 2022:

```python
# SPDX-FileCopyrightText: AGPL-3.0-or-later
# Copyright (C) 2021 nfitzen <https://github.com/nfitzen>
# Copyright (C) 2022 Bob

def add(a: float, b: float) -> float:
    "Adds 2 numbers."
    return a + b

def foo():
    ...
```

And then Alice makes a third function in 2024:

```python
# SPDX-FileCopyrightText: AGPL-3.0-or-later
# Copyright (C) 2021 nfitzen <https://github.com/nfitzen>
# Copyright (C) 2022 Bob
# Copyright (C) 2024 Alice

def add(a: float, b: float) -> float:
    "Adds 2 numbers."
    return a + b

def foo():
    ...

def bar():
    ...
```

And then when the `foo` function is removed, you take out Bob's
copyright notice.

However, let's say both Bob and I (nfitzen) contributed code
in both 2021 and 2022. This is how it'll look:

```python
# SPDX-FileCopyrightText: AGPL-3.0-or-later
# Copyright (C) 2021, 2022 nfitzen <https://github.com/nfitzen> and bob
# Copyright (C) 2024 Alice

def add(a: float, b: float) -> float:
    "Adds 2 numbers."
    return a + b

def foo():
    ...

def bar():
    ...
```

So you collapse copyright statements when both years align.

When in doubt, leave copyright notices intact. Also, if you're merging
code from another repository (that wasn't a contribution to this one),
then leave that copyright notice separate no matter what.

### Catch-all Statements

If more than 3 people have contributed to a file, it is recommended
to collapse the copyright notices into
"Copyright &copy; \<years\> nfitzen and the \<project-name\> contributors."

This applies for both individual files and the summary notice.

If you wish, you may add your name to a file called `AUTHORS`,
using the format in the [Linux `CREDITS` file][1]. This might make it easier
to contact if needed.

Reproduced is the relevant text:

> The fields are: name (N), email (E), web-address
> (W), PGP key ID and fingerprint (P), description (D), and
> snail-mail address (S).

Such fields are separated by a colon. E.g.:

```
N: nfitzen
W: https://github.com/nfitzen
D: Principal maintainer and contributor.
S: North Carolina
S: United States
```

Keep in mind, though, that the Git blame is often enough. So if there isn't
already an `AUTHORS` file, please be reluctant to create one.

[1]: https://git.kernel.org/pub/scm/linux/kernel/git/torvalds/linux.git/tree/CREDITS

## Marking Licenses

This repo uses [SPDX IDs](https://spdx.dev/ids/) to mark licenses
and is [REUSE] compliant.
SPDX tags should always go at the very top of the file unless
required to be in a different place by the programming language
or environment, such as shebangs. For example, a shell script might have:

```sh
#!/bin/sh
# SPDX-License-Identifier: AGPL-3.0-or-later
# Copyright (C) 2021 nfitzen <https://github.com/nfitzen>

echo "Hello, world!"
```

as opposed to a Python module without a shebang:

```python
# SPDX-License-Identifier: AGPL-3.0-or-later
# Copyright (C) 2021 nfitzen <https://github.com/nfitzen>

def foo():
    ...
```

(If you decide a shebang is worth it even in a Python module, that's also
fine.)

If different parts of a file are licensed differently,
make a comment possibly using either `SPDX-FileNotice` or
`SPDX-FileComment` (with the latter likely being more compliant).
Also try to make a comment in the code.

For instance, if I made a contribution under [`AGPL-3.0-or-later`],
and then merged code from Alice, who licensed her code under [`Apache-2.0`],
the following would be the license header:

```python
# SPDX-License-Identifier: AGPL-3.0-or-later
# SPDX-License-Identifier: Apache-2.0
# SPDX-FileComment: Function bar (C) Alice licensed under Apache-2.0.
# Copyright (C) 2021 nfitzen <https://github.com/nfitzen>
# Copyright (C) 2021 Alice

# written by Alice
def foo():
    ...

# written by nfitzen
def bar():
    ...

```

However, try to avoid such situations. It's usually fairly easy
(and likely cleaner, depending on what you're doing) to extract `foo`
to another file and import/include it.

## Other Rules

The [REUSE] specification provides any rules I didn't mention here,
such as providing license files or using Debian's copyright format
for bulk licensing.

The repo may contain a LICENSE or COPYING file at the root of the repository,
which doesn't make any material representation of the licenses used, or
even whether it's the most strict license used. It most likely
represents what the majority of the code is licensed under.

## Copyright

Copyright &copy; 2021 [nfitzen](https://github.com/nfitzen)

This file is licensed under [CC BY-SA 4.0].

See the HTML comments at the top of the file for the ASCII copyright notice
if in plaintext.

[REUSE]: https://reuse.software/

[CC BY-SA 4.0]: https://creativecommons.org/licenses/by-sa/4.0/ "Creative Commons Attribution-ShareAlike 4.0 International"

[`AGPL-3.0-or-later`]: https://spdx.org/licenses/AGPL-3.0-or-later.html "GNU Affero General Public License v3.0 or later"
[`Apache-2.0`]: https://spdx.org/licenses/Apache-2.0.html "Apache License 2.0"
