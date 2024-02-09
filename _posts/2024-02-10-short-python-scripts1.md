---
layout: post
title:  "Short, kinda useful Python scripts"
date:   2024-02-08 00:00:00 -1000
categories: it python
image: lazy-python.jpg
---

These are small utilities for future me to use when I want to do things the lazy way with scripts. As with all scripts, run at your own risk. :) I don't develop or write Python for optimization; I write it enough that it works for my specific scenarios.

[Scripts found here.](github.com/sudoyashi/python_progress)

## Create folders with whatever is in a .csv

Wherever the script is, create a file called `directory.csv` and hard write the values 'CDs, software, drivers' in rows. Then, read that `.csv` and create folders based on those values. To create other folders, just edit the list of names in `directory.write`

```python
# Creates a list of directories if they do not exist. This creates
# the CDs, software, and drivers directories, as indicated by directory.csv
import os
import csv
from pathlib import Path

# create the file directory.csv

with open('directory.csv', 'w') as directory:
    directory.write('CDs,software,drivers')

# setup variable that loads all *.csv information
    
pathName = os.getcwd()
directoryFiles = os.listdir(pathName)
csvFiles = []
for file in directoryFiles:
    if file.endswith(".csv"):
        csvFiles.append(file)

with open('directory.csv') as csvfile:
    reader = csv.reader(csvfile, delimiter=',')
    for row in reader:
        for column in row:
            print(column)
            p = pathName + '\\' + column
            Path(p).mkdir(parents=True, exist_ok=True)
```



## Removing Title and Author metadata from .docx files

The issue I had to solve was that the title property of a .docx was showing in Acrobat rather than the actual filename. One of our users thought this was a phishing or virus, and rightfully so. It was a slight problem with metadata, but still a problem.

The '*.docx' wildcard is not the best, but I'm unsure how else to write the solution. It opens the directory and recursively checks all folders and files for .docx files. Then, edit the properties to change the Author and Title. Of course, you can change anything else: modify the core_properties variable. The script does NOT cover .doc files; you would have to use something to convert .doc files into .docx. 

```python
# Open all the documents and check to see if the document has a title, if so, remove it.
# Open all the documents and change the Author
import os
import fnmatch
from docx import Document

# Select all the docx
cwd = os.getcwd()
for dirpath, dirs, files in os.walk(cwd):
    for filename in fnmatch.filter(files, '*.docx'):
        # use print if you want to see what files will be modified
        # print (os.path.join(dirpath, filename)) 
        editFile = (os.path.join(dirpath, filename))
        document = Document(editFile)
        core_properties = document.core_properties
        # If the author filed is not my email, change it
        if (core_properties.author != 'joshua...email'):
            core_properties.author = 'joshua...newEmail'
        # Check if title is not empty, make it empty
        if (core_properties.title != ''):
            core_properties.title = ''
        # Save the file with the original name
        document.save(editFile)
        print ('Saved ', editFile)	
```

### You will have issues if these are server files!

- A couple of issues:
  - During actual testing, Python-docx cannot modify the metadata of .doc files. You will get a package not found error.
  - The packages did not load properly because my files were on a UNC path (server path). You need to add the package to the server's local directory and then do a local import. The following submodules .py were affected and had to be modified:
    - api.py
    - phys_pkg.py
    - package.py
    - pkgreader.py

For each file above, append the following to the beginning list of imports:

```
# mymodule.py
import os
import sys
# Add the parent directory of mypackage to the Python path
sys.path.append(os.path.abspath(os.path.join(os.path.dirname(__file__), '..')))
```

Then you can import the package using:

```
from docx import Document
```

Depending on the directory setup, it may take a couple of tries to read the errors. You may also have to replace any __ init__.py with empty files. For more information, read the issue on [Attempted relative import with no known parent package](https://net-informations.com/q/py/known.html).

## This does not modify .doc files

Yeah. Only .docx.

## Convert XML files to Excel (.xlsx)

Find all `.xml` files in the current working directory, convert them to `.xlsx`, and save the converted files in an existing folder called `.xlsx`.

```python

# This script finds all files that end with .xml and puts them into a list. In that list,
# extract the xml value pairs, remove duplicates and write the pairs into sheet1 
# of a new Excel sheet within columns B:Z
# Finally, save the XML as an XLSX into the xlsx directory.

import xml.etree.ElementTree as ETree
import pandas as pd
import os
import pathlib
from os import listdir, path
from pathlib import Path

cwd = os.getcwd()
files = []
for file in listdir(cwd):
    if file.endswith('.xml'):
        files.append(path.join(cwd, file))

for xml in files:
    fileroot = Path(xml).stem
    tree = ETree.parse(xml)
    root = tree.getroot()
    valuePairs = []  # empty array assigned to A
    for elements in root:
        valuePair = {}  # empty array; store data values in key:value pair
        for element in list(elements):
            valuePair.update({element.tag: element.text})  # updating dictionary with(tag -> Columns, text -> Rowdata)
            valuePairs.append(valuePair)  # Append key:value pair to A list
        df = pd.DataFrame(valuePairs)  # Create dataframe (df)
        df.drop_duplicates(keep='first', inplace=True)  # Only keep first, ignore all others
        df.reset_index(drop=True, inplace=True)
        writer = pd.ExcelWriter(cwd + '\\' + 'xlsx' + '\\' + fileroot + '.xlsx', engine='xlsxwriter')
        df.to_excel(writer, sheet_name='sheet1')
        worksheet = writer.sheets['sheet1']
        worksheet.set_column('B:Z', 30)  # Set column char to 30 for columns from B to Z
        writer._save()
    print(df)
    print('XML file has been parsed. Open at ' + fileroot + '.xlsx...')
```

## **Write a script if it's faster than doing it manually.** 

I am not trying to edit 300+ files within each directory to rename the file to something else. That's what you make a script! These are housekeeping scripts that help make things fast and consistent. Python is useful for automating tedious menial tasks. I could optimize them, but at the tiny scale I have them, I don't need to right now. Thank goodness for modern hardware. 

And if it's not faster, you don't need a script. Just do it, ya lazy.