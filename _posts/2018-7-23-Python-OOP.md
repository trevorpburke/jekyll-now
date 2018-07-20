---
layout: post
title: An Attempt to Demystify Python Classes
tags: python classes oop object oriented 
---

Grasping the concept of classes in Python confused me for quite a long time. The concept is fairly abstract and I've found most tutorials gloss over some important aspects of classes that make them easier to understand.

Before delving into creating classes I want to begin with an ELI5, Explain Like I'm 5, explanation of [object-oriented programming](https://en.wikipedia.org/wiki/Object-oriented_programming, which Python supports. 

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

Abstraction is a sometimes-confusing computer science term that is essentially equivalent to DRY. By creating an 'Organism' class we've made it very simple, and non-repetitive, to create different 'Organisms' objects to store information about them.

SECTION ABOUT METHODS/ATTRIBUTES

```python
class Organism:
    def __init__(self, species, genus, diet):
        self.species = species
        self.genus = genus
        self.diet = diet

    def check_diet(self, diet):
        return diet.lower() == self.diet.lower()

```

SECTION ABOUT INHERITANCE 

```python
class HumanBeing(Organism):
    def __init__(self, name, age, sex):
        super().__init__('Homo', 'sapiens')
        self.name = name
        self.age = age
        self.sex = sex
```
