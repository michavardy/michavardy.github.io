---
title: "python module vs script"
date: 2023-01-10
---


# Python Module vs Python Script 

#### why is this a thing?

![](../images/earth_rise.jpg)


# Motivation:
I am working on debugging a dirty github repo because I promised someone that we could use this code for identifiying animals using ML.

Its very large spagetti repo and has become way more boring than my work, :(

I have come across a weird thing where the python script was instantiated with the following syntax 
```
python -m ./python310/Lib/moduleName.scriptname -flag1
```

the command was working, but I couldn't find the flag in the script, which prompted this blog post.
# Reddit Post
I posed this question to reddit and recieved a grumpy comment about formatting, and a very lazy google search link from someone.  the google search link sparked an interesting conversation that different people have different search results, so he should just link the article.

# Resource:
**Resource**: [stack overflow of same problem](https://stackoverflow.com/questions/22241420/execution-of-python-code-with-m-option-or-not)
I briefly read this confusing stack overflow post and sort of understood that when you run with module flag it runs a ``__main__.py `` file in the repo.
# Questions: 
- #### what happens when you run a python module with ``-m`` flag?
- #### why would anyone want to do this?
# Setup:
I set up a little test to answer my questions:
## Project Structure
```bash
`-- mod_test
    |-- __init__.py
    |-- __main__.py
    `-- test.py
```

## Path
```
C:\Users\micha.vardy\AppData\Local\Programs\Python\Python310\Lib
```

## Scripts

### ``__init__.py``

```python
print("initialize project file")

if __name__ == "__main__":
    print('init file main')
```

### ``__main__.py``
```python
print("main project code")

if __name__ == "__main__":
    print('main file main')
```
### ``test.py``
```python
import sys
print(sys.executable)

if __name__ == "__main__":
    print('test file main')
```
# Results:
#### Running with ``-m`` flag
```bash
$ python -m mod_test.test

initialize project file
C:\Users\micha.vardy\AppData\Local\Programs\Python\Python310\python.exe
test file main
```
#### Running without ``-m`` flag
```bash
$ python ~/AppData/Local/Programs/Python/Python310/Lib/mod_test/test.py

C:\Users\micha.vardy\AppData\Local\Programs\Python\Python310\python.exe
test file main
```
#### Results Summery
- So I guess the ``-m`` flag doesn't run ``__main__.py`` but it does run ``__init__.py``.  
- Also I guess the ``-m`` flag does invoke ``if __name__ == __main__:`` of script
# Discussion:
#### Why would anyone want to do this?
####
#### Possible Use Case: setting up multiple scripts
I guess if you want to run a number of different scripts with the same setup, you could make a directory of scripts with the same setup in ``__init__.py`` and save yourself the step of setting up every script.



