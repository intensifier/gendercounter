# Gendercounter
A program for counting the occurrence of male and female Swedish names in a text file.

Try the live web version: [genuskollen.se](http://genuskollen.se)


## Functionality
A series of functions for counting gendered Swedish names in text.
Import the gendercounter.py script along with the tsv files containing names and frequencies:

    female250.tsv
    male250.tsv

The first two dictionaries list female and male names respectively, along with the frequency of occurrence according to Statistics Sweden (2015).
Also, the following pronouns can be counted.

1. hen/henom/hens
2. hon/henne/hennes
3. han/honom/hans


## Usage

```python
import gendercounter # Just import as usual.

example = """Karl och Lisa promenerar på gatan och
            tycker om Ove och Stina och Bertil.
            Hon, han, hen, henom. Hon hens"""
```

### Usage example 1: initialize a text object from a string

```python
text = gendercounter.from_string(example)

text.genderfrequency()
```

{'Men': 3, 'Women': 2}

```python
text.pronounfrequency()
```
{'han': 1,
 'hans': 0,
 'hen': 1,
 'henne': 0,
 'hennes': 0,
 'henom': 1,
 'hens': 1,
 'hon': 2,
 'honom': 0}

```python
# Returns names and the number of people with that name in Sweden.
text.names()
```
{'Men': {'Bertil': '68261', 'Karl': '209908', 'Ove': '33731'},
 'Women': {'Lisa': '31611', 'Stina': '19071'}}

### Usage 2: From a text file

```python
textfile = gendercounter.from_textfile("testtext.txt")

textfile.genderfrequency()
```

{'Men': 15, 'Women': 7}

### Usage 3: Do both as a single line of code

```python
gendercounter.from_textfile("testtext2.txt").genderfrequency()
```

{'Men': 43, 'Women': 29}

### Usage 4: Iterate over multiple files, example

```python
from os import listdir

for file in listdir('.'):
    if file.endswith('txt'):
        print(file)
        for k, v in gendercounter.from_textfile(file).genderfrequency().items():
            print(k, v)
        for k, v in gendercounter.from_textfile(file).pronounfrequency().items():
            print(k, v)
        print("-" * 10)
```

testtext2.txt
Men 43
Women 29
han 1
henom 0
hennes 0
henne 0
hon 0
hen 0
honom 0
hens 0
hans 0

testtext.txt
Men 15
Women 7
han 1
henom 2
hennes 2
henne 2
hon 2
hen 2
honom 0
hens 2
hans 0

## Concurrency

If you work with large datasets, check out the ``concurrency.ipynb`` notebook for an example of concurrent computing. 

## Sources of error
- Some names are also frequent Swedish words, for example "De".
- Uncommon names (less than 250 occurrences) were excluded.
- Some names are gender neutral ("Charlie", "Mario", "Alex" etc.)
- With the pronoun counter, the words "Han" and "Hans" can also be Swedish male names.
- ??? (Please let me know if you find other sources of error)

## Removed names
- "De"
- "Del"

## Similar programs
* [SexMachine](https://pypi.python.org/pypi/SexMachine/) (English language, written in Python)
