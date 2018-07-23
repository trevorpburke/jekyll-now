---
layout: post
title: An Attempt to Demystify Python Classes
tags: python classes oop object oriented class __init__
---

Grasping the concept of classes in Python confused me for quite a long time. The concept is fairly abstract and I've found most tutorials gloss over some important aspects of classes that make them easier to understand.

Before delving into creating classes I want to begin with an ELI5, Explain Like I'm 5, explanation of [object-oriented programming](https://en.wikipedia.org/wiki/Object-oriented_programming), which Python supports. 

My non CS degree definition of object-oriented programming, hereby referred to as OOP, is a style of programming that promotes the principle of DRY, "don't repeat yourself." With `class` I can create an 'Organism' object that contains information about that organism. In the below example the 'Organism' class contains that organism's species and genus. The `class` is a way of abstracting away aspects of creating an 'Organism' object.

```python
class Organism:
    def __init__(self, species, genus):
        self.species = species
        self.genus = genus

Human = Organism('Homo', 'sapiens')
Cow = Organism('Bos', 'taurus')
Gorilla = Organism('Gorilla', 'gorilla')
Orangutan = Organism('Pongo', 'borneo')

```

Abstraction is a sometimes-confusing computer science term that is essentially equivalent to DRY. By creating an 'Organism' class we've made it very simple, and non-repetitive, to create different 'Organism' objects to store information about them.

In addition to storing information, classes provide functions, or methods, to manipulate or access that information. In the below example we have a `check_diet` method that will check an organism's diet against an inputted diet.

```python
class Organism:
    def __init__(self, species, genus, diet):
        self.species = species
        self.genus = genus
        self.diet = diet

    def check_diet(self, diet):
        return diet.lower() == self.diet.lower()

Human = Organism('Homo', 'sapiens', 'omnivore')

Human.check_diet('herbivore')
# False
Human.check_diet('omnivore')
# True

```

A great real-world example to explore is the DataFrame class that the `pandas` library is built around.

> Flexible and powerful data analysis / manipulation library for Python, providing labeled data structures similar to R data.frame objects, statistical functions, and much more

A `pandas` [DataFrame](https://pandas.pydata.org/pandas-docs/stable/generated/pandas.DataFrame.html) is a labeled, tabular data structure similar in appearance to an Excel Spreadsheet. It can load data from a variety of sources and export to an equally diverse array of output formats. In the documentation you can see a list of the available methods one can employ to play around with the data contained within a DataFrame object.

Here's a bit of the (truncated) [source code](https://github.com/pandas-dev/pandas/blob/master/pandas/core/frame.py) of a `pandas` DataFrame class and a few of its methods. The `shape` method provides the dimensionality of the DataFrame itself.

```python
class DataFrame(NDFrame):
    """
    ...
    """
    def shape(self):
        """
        Return a tuple representing the dimensionality of the DataFrame.
        See Also
        --------
        ndarray.shape
        Examples
        --------
        >>> df = pd.DataFrame({'col1': [1, 2], 'col2': [3, 4]})
        >>> df.shape
        (2, 2)
        >>> df = pd.DataFrame({'col1': [1, 2], 'col2': [3, 4],
        ...                    'col3': [5, 6]})
        >>> df.shape
        (2, 3)
        """
        return len(self.index), len(self.columns)
```

So, classes provide an efficient way to store information and provide tools, or methods, to access or manipulate that information. Classes can actually do a little bit more too; they can inherit attributes and/or methods from other classes. In the above source code for the DataFrame class you'll see an `NDFrame` argument in the class definition. This means that the NDFrame `class` provides some of the structure and foundation to the DataFrame `class`.

Here's an easier to digest example using the 'Organism' class created earlier in this post:

```python
class Organism:
    def __init__(self, species, genus):
        self.species = species
        self.genus = genus

class HumanBeing(Organism):
    def __init__(self, name, age, sex):
        super().__init__('Homo', 'sapiens')
        self.name = name
        self.age = age
        self.sex = sex

Trevor = HumanBeing('Trevor', 25, 'male')
Trevor.age
# 25
Trevor.genus
# 'sapiens'
```

Establishing 'Organism' as a base class prevents me from having to explictly declare the species and genus of every new HumanBeing object I create. The `super` function takes care of that for me by initializing all 'HumanBeing' objects as 'Homo' and 'sapiens'. 

Classes are a crucial aspect of Python and many other OOP languages. In my path to understanding them I've found reading high quality documentation, like the `pandas` documentation to be the most helpful in mastering this concept.


