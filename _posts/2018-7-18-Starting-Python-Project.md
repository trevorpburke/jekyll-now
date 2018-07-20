---
layout: post
title: How I Begin a Python Project
tags: python virtual environment git linter logging pep8 
---

Whenever I begin a project that involves more than a simple Python file I have a (somewhat flexible) set of tasks I complete prior to writing any actual code. These steps can be applied to essentially any Python project and I'm sure there are more steps to include. Feel free to comment some suggestions!

0. [Virtual Environment Set Up](#venv)
1. [Git Setup](#git)
2. [Linter](#linter)
3. [Logging](#logging)
4. [Conclusion](#conclusion)


### <a name="venv"></a> Virtual Environment Set Up

Virtual environments separate your project, its Python version and its dependencies from your machine's Python installation and globally installed dependencies. Within your project's directory run this command:

```bash
python3 -m venv /path/to/your/project
```

This establishes a Python3 installation within your project. To begin installing packages within this environment:
```bash
source bin/activate
pip install pandas
```
When you're not working on your project you can deactivate the environment with simply `deactivate`


### <a name="git"></a> Git Setup

There are loads of great tutorials on learning how to use Git and I'd recommend checking out [Atlassian's Git tutorials](https://www.google.com/search?q=atlassian+git+tutorial&ie=utf-8&oe=utf-8&client=firefox-b-1-ab).

Typically - this is mostly just preference - I initiate a Git repository locally on my machine, commit often (with detailed descriptions), and eventually push that local repository to a remote repository on GitHub, GitLab, or wherever.

My first few commits usually invovle some housekeeping tasks:
  * Creating a basic README for the project
  * Generating a [.gitignore](https://github.com/github/gitignore/blob/master/Python.gitignore) with Python-specific entries
  * If working on a personal project I'll attach an open source friendly license

From here I will write code, commit code, and create branches when I think of a totally different way to tackle my problem or project.


### <a name="linter"></a> Linter

Adhering to a style guide keeps code clean, maintainable, and enjoyable to work with; extra emphasis on that last descriptor. As a self-taught developer I constantly reread the [Python Style Guide, aka PEP8)](https://www.python.org/dev/peps/pep-0008/?) so I'm consistently following industry best practices; ingraining these practices in my brain! 

It's tough to remember all the conventions of PEP8, so linters come to save the day. With a simple `pip install` (within your virtual environment, of course) you can run a simple `pylint your_program.py` and you'll get a human-readable output of where your code can be improved and an overall code rating.

Just like with your `~/.bashrc` or `~/.pgpass` you can customize `pylint` to what rules and convetions matter most to you.


### <a name="logging"></a> Logging

All the previous steps are present in almost every blog post about starting a Python project, but many authors neglect to mention the `logging` module within the Python standard library. 

Because I've worked primarily as a Data Analyst I'm no stranger to messing around with Linux servers, which rely heavily on logging to deliver information or errors to its users. PRO TIP: `tail -f file.log` will stream logs to your terminal.

In essence, the `logging` module provides a way to track events and errors based on a scale of severity (lowest to highest):

     * DEBUG
     * INFO
     * WARNING
     * ERROR
     * CRITICAL

This module is extremely powerful and offers tons of configuration options, but I've found that the most effective method is creating a dictionary logging object, importing that dictionary into your application, and logging to a simple text file.
```python
# logging_config.py
config = {
    'version': 1,
    'formatters': {
        'simple': {
            'format': '%(asctime)s %(levelname)s %(name)s: %(message)s'
        },
    },
    'handlers': {
        'file': {
            'level': 'INFO',
            'formatter': 'simple',
            'class': 'logging.FileHandler',
            'filename': 'logs/errors.log'
        },
    },
    'loggers': {
        'errors': {
            'handlers': ['file'],
            'level': 'INFO',
            'propagate': True
        },
    }
}
```
I'll eventually write a more detailed post about the `logging` module, but to keep this post succinct I'll briefly explain what's happening here. This config contains information about how the log is formatted to its handler, which in this case is a file, 'logs/errors.log'. Also, I've established that I only care about errors from the INFO level and above; this will ignore DEBUG errors. DEBUG errors can end up clogging logs and defeat the purpose of logs.

Now, in order to actually log events:

```python
# app.py
import logging
import logging.config
from logging_config import config
from other_module import pull_data

logging.config.dictConfig(config)
logger = logging.getLogger('errors')

def get_data():
    """
    Fake function to get data
    """ 
    try:
        conn = pull_data()
    except DataError as e:
        logger.warning(e)
```

I created a psuedo-codey function here to illustrate how one can funnel the error from an Exception into a log file. 

In this example, the `logger` instance object is calling the `warning` method, but if I wanted to simply note an event, not an error, I could call the `info` method.


### <a name="conclusion"></a> Conclusion

This process for beginning a Python project is constantly evolving for me and I imagine there are many more steps I could add; feel free to suggest any ideas in the comments. I've been thinking about learning about Docker and other container technologies too! Perhaps I'll update this post when I've learned more about Docker.


