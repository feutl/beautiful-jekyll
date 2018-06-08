---
layout: post
title: TextMate and Python 3
date: 2011-12-03
tags: [english, technology]
image: /img/2011/textmate.png
---

If you are working on a Apple Mac you probably know Textmate - THE texteditor for Mac. Also if you do start Python Coding you get confronted with Python 2 and Python 3 and do know that Max OS X is using Python 3 per default. The installation of Python 3 is pretty is, if you follow the instructions on the Python Website.

A bigger approach is to set up TextMate to use Python 3 per default for their TextBundles!

A view solutions came up after my research which I want to point out - at the end its your decision which one you like most. But before you start, you have to get some path information, so open Terminal.app to find out the path for your Python interpreters
* `which python` -> for getting python 2 path
* `which python3` -> for getting python 3 path
* `which python3.1` -> letting you know where to find python 3.1 installation

1. Set Up Python 3 to be used on a per Project Base
    * Open a new or existing TextMate Project (File -> New Project or File -> Open)
    * De-select any file in the project list sidebar.
    * Click on the Get Info (i) icon in the sidebar. A Project Information pane appears.
    * Click + to add a new variable.
    * Enter TM_PYTHON in the Variable field and the full path to the desired python in the Value field (for example, /usr/local/bin/python3.1).
    * Close the Information window and save the Project (File -> Save Project As).
2. Set Up Python 3 globally for TextMate
    * From the TextMate menu bar, open TextMate -> Preferences
    * click on the Advanced pane
    * click on the Shell Variable tab
    * click the + to add a new variable
    * enter TM_PYTHON in the Variable field and the full path to the python in the Value field (perhaps /usr/local/bin/python3.1)
3. Hardwire the Python Path within your PY-File using a shebang
    * `#!/usr/local/bin/python3.1` this line at the beginning hard wires python3.1 interpreter to the file

All the above mentioned solutions are pretty easy to realize and working great, but do have one downside! You have to use the Terminal.app to execute the PY-File. That means using CMD+SHIFT+R command. As soon as you use the TextMate integrated Script Engine it will use Python Version 2 instead.

# Using Python 2 or 3 within TextMate
Using Python within TextMates own Script Engine You can add or modify a global PATH shell variable to TextMate -> Preferences (see above) by adding the path to your python3 interpreter.

In my case it is /usr/local/bin which creates an entry for PATH looking like /usr/bin:/bin:/usr/sbin:/sbin:/usr/local/bin

Now you can define which enginge TextMate should use by setting the shebang to #!/usr/bin/env python3 for Python 3 and without the version number it uses the default Mac Python Bundle.

Actually my setup is combining both options to have the Terminal.app and the TextMate Script Engine running Python 3 - at the momemt I am searching for a solution to have the same approach from the the TextMate Script Engine at the Terminal.app as well. Resources

# Resources
*   [Using Python 3.1 with TextMate](http://stackoverflow.com/questions/1775954/using-python-3-1-with-textmate)
*   [Is there a better Python bundle for textmate than the one in the bundle repository?](http://stackoverflow.com/questions/688245/is-there-a-better-python-bundle-for-textmate-than-the-one-in-the-bundle-repositor)
*   [using python 3.0.1](http://old.nabble.com/using-python-3.0.1-td22499054.html)