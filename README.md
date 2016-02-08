dThreads
========


dThreads is a small module for creating object-like dictionaries based on
[Bunch][bunch]. Threads extends Bunch with the ability to both load and dump in
JSON or YAML format.

Installation via `pip`:

```bash
pip install dthreads
```

Quick usage:

```python
>>> from dthreads import Threads
>>> items = Threads(a=0, b=1, c=[0, 2], d=Threads(x=0, y=1, z=2))
>>> items
{'a': 0, 'c': [0, 2], 'b': 1, 'd': {'y': 1, 'x': 0, 'z': 2}}
>>> items.c(1)
2
>>> items.d
{'y': 1, 'x': 0, 'z': 2}
```

dThreads offers serialization to JSON:
--------------------------------------

```python
>>> items = Threads(a=0, b=1, c=[0, 2], d=Threads(x=0, y=1, z=2))
>>> items.json_dumps()
{"a": 0, "c": [0, 2], "b": 1, "d": {"y": 1, "x": 0, "z": 2}}
>>> with open('data.json', 'w') as f:
...     items.json_dump(f)
```

JSON methods supported: `load`, `loads`, `dump`, `dumps`

dThreads offers serialization to YAML:
--------------------------------------

```python
>>> items = Threads(a=0, b=1, c=[0, 2], d=Threads(x=0, y=1, z=2))
>>> items.yaml_dump()
!threads.Threads
a: 0
b: 1
c: !!python/object/new:__main__.Strands
    listitems:
    - 0
    - 2
d: !threads.Threads
    x: 0
    y: 1
    z: 2
```

YAML methods supported: `load`, `load_all`, `safe_load`, `safe_load_all`,
`dump`, `safe_dump`


[bunch]: (https://github.com/dsc/bunch)
