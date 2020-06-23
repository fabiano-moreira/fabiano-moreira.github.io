---
title: "Web Sraping in Python"
date: 2019-05-20
categories: 
        - blog
tags: 
    - Python programming
    - Sraping
    - Job test
---

Hello there. How you doing?! 

In this post, I'm sharing some code in Python. This code was a job test.

That test consists of a Python script, whit a scrapy function. 

This scrapy looking for some entry in an online dictionary named Michaelis.

Here is the code.



``` python

#!/usr/bin/env python3
# -*- coding: utf-8 -*-

# Make a virtual environment and install the packages. Don't mess up your environment.
#   python3 -m venv .venv
#   source .venv/bin/activate
# You will need the packages beautifulsoup and requests:
#   python3 -m pip install requests
#   python3 -m pip install beautifulsoup4


import requests
from bs4 import BeautifulSoup
import sys

# To ask the argument, in this case the entry (the word "verbete" is the entry).
verbete = sys.argv[1]

url = 'https://michaelis.uol.com.br/moderno-portugues/busca/portugues-brasileiro/' + verbete


page = requests.get(url)

# Create a object BeautifulSoup.
soup = BeautifulSoup(page.text, 'html.parser')

# Take a text in your entry's div bs-component.
vocabulos = soup.find(class_='verbete bs-component')

# Take the all texts of all instances inside the tags, inside the div BodyText. There is no tag inside the entry text.
vocabulos_items = vocabulos.find_all('acn')
vocabulos_items2 = vocabulos.find_all('div')
vocabulos_items3 = vocabulos.find_all('rn')
vocabulos_items4 = vocabulos.find_all('ra')

# Create a loop and print all entries meanings.


for vocabulos in vocabulos_items or vocabulos_items2 or vocabulos_items3 or vocabulos_items4:
    print(vocabulos.next_sibling)

```