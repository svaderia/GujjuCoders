---
layout: post
title: Script to genrate python scripts
author: sym
tags: [Python]
image: /assets/python.png
---

Recently I got habit of writing `shebang` and my name in all the python script I create. It was getting very repetitive to copy and paste it every time, so to decrease my work created a small python script that does that for me.

```python
#!/usr/bin/env python3
# @author = 01010011 01101000 01111001 01100001 01101101 01100001 01101100 
# date	  = 08/06/2017

# Import the modules needed to run the script.
from os.path import exists
from time import strftime
import sys

def main():
    # Checks if version is specified, if not it will write the default version in shebang.
    version = -1    
    if len(sys.argv) > 1:
        if sys.argv[1] in ['2','3']:
            version = int(sys.argv[1])
    
    title = input("Enter a title for your script: ")

    # Add .py to the end of the script.
    title = title + '.py'

    # Convert all letters to lower case.
    title = title.lower()

    # Remove spaces from the title.
    title = title.replace(' ', '_')

    # Check to see if the file exists to not overwrite it.
    if exists(title):
        print("\nA script with this name already exists.")
        exit(1)

    # My name in binary. You can ask user as well
    name = "01010011 01101000 01111001 01100001 01101101 01100001 01101100 "

    # Create a file that can be written to.
    filename = open(title, 'w')

    # Set the date automatically.
    date = strftime("%d/%m/%Y")

    # Write the data to the file.
    if version > 0:
        filename.write('#!/usr/bin/env python{}'.format(str(version)))
    else:
        filename.write('#!/usr/bin/env python')
        
    filename.write('\n# @author = ' + name)
    filename.write('\n# date\t  = ' + date)
    filename.write('\n'*9)                      # this 9 line are here just to make it look nice
    filename.write('def main():\n')
    filename.write('    pass\n')
    filename.write('\nif __name__ == "__main__":\n')
    filename.write('    main()')

    # Close the file after writing to it.
    filename.close()

if __name__ == "__main__":
	main()

```

I gave execute permission to my script using `chmod +x pyscript.py` 
and added `alias py = '~/pyscript.py'` in my `.bashrc`. Now if I execute `py 2` in any folder it will create a new 
python script with the following format.

```python
#!/usr/bin/env python2
# @author = 01010011 01101000 01111001 01100001 01101101 01100001 01101100 
# date	  = 28/06/2017








def main():
    pass

if __name__ == "__main__":
    main()
```