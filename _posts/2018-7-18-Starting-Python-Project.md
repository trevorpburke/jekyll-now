---
layout: post
title: How I Begin a Python Project
---

Whenever I begin a project that involves more than a simple Python file I have a (somewhat flexible) set of tasks I complete prior to writing any actual code. These steps can be applied to essentially any Python project and I'm sure there are more steps to include. Feel free to comment some suggestions!

0. [Virtual Environment Set Up](###Virtual Environment Set Up)
1. [Git Setup](###Git Setup)
2. [Logging](###Logging)
3. 

### Virtual Environment Set Up

Virtual environments separate your project, its Python version and its dependencies from your machine's Python installation and globally installed dependencies. Within your project's directory run this command:

    python3 -m venv /path/to/your/project

This establishes a Python3 installation within your project. To begin installing packages within this environment:

     source bin/activate
     pip install pandas

### Git Setup
