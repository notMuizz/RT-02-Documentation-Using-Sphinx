[Research Track II](https://corsi.unige.it/en/off.f/2022/ins/60236)<br>
[Hafiz Muizz Ahmed Sethi](https://github.com/notMuizz)<br>
[M.Sc Robotics Engineering](https://corsi.unige.it/corsi/10635)<br>
**Professor:** [Prof. Carmine Tommaso Recchiuto](https://rubrica.unige.it/personale/UkNDWV1r)

# Documentation for ROS RVIZ GAZEBO C++

## Introduction
In this documentation, [Sphinx](https://www.sphinx-doc.org/en/master/) tool is used. *Sphinx* was originally created for **Python**, but it has now facilities for the documentation of software projects in a range of languages. Sphinx uses [reStructuredText](https://docutils.sourceforge.io/rst.html) as its markup language. 

Here are some of Sphinx’s major features:

* **Output formats:** HTML (including Windows HTML Help), LaTeX (for printable PDF versions), ePub, Texinfo, manual pages, plain text.
* **Extensive cross-references:** semantic markup and automatic links for functions, classes, citations, glossary terms and similar pieces of information.
* **Hierarchical structure:** easy definition of a document tree, with automatic links to siblings, parents and children.
* **Automatic indices:** general index as well as a language-specific module indices.
* **Code handling:** automatic highlighting using the Pygments highlighter.
* **Extensions:** automatic testing of code snippets, inclusion of docstrings from Python modules (API docs) via built-in extensions, and much more functionality via third-party extensions.
* **Themes:** modify the look and feel of outputs via creating themes, and re-use many third-party themes.
* **Contributed extensions:** dozens of extensions contributed by users; most of them installable from PyPI.

## Installation & Running Sphinx tool

To create documentation, *Sphinx* tool is required on your system. To install Sphinx follow the steps given below:

```
sudo apt-get install python3-sphinx
```
*For Docker user execute the aforementioned command without sudo*

```
pip3 install breathe
```
```
pip3 install sphinx-rtd-theme
```
With these three commands, you are installing spinhx, plus breathe, which is a tool for integrating doxygen documentation in sphinx, and thus comment also cpp code, and the ReadTheDocs theme, one of the most used theme for creating documentation.

After installation of *Sphinx*, follow the steps given below:

**Step 1:** 
```
sphinx-quickstart
```

After running the command, accept the defaults. It’ll look something like this: 

![alt text] ![Screenshot from 2023-06-02 17-09-52](https://github.com/notMuizz/RT-02-Documentation-Using-Sphinx/assets/123844091/0cb52818-fa31-4bc9-9cbe-3e22541e7b0a)


Figure above shows that *Separate source and build directories (y/n) [n]: n*. 

**Step 2:** Now, press entre write the ***Project Name, Author Name, Project Release***. as shown in figure below. Also, enter the required details, now choose the language in which documentation to be prepared. 



## Documentation Preparation

After intallation, now you are ready to create documentation. After execution of ```sphinx-quickstart```, you can see ***conf.py*** file in your given directory path, which still needs to be updated. Now add the required things as given below from *line 13*: 

```
import os
import subprocess
import sys
sys.path.insert(0, os.path.abspath('.'))
subprocess.call('doxygen Doxyfile.in', shell=True)
#-- Project information -----------------------------------------------------
```
This is needed to run doxygen, generating an xml file which will be used by sphinx for creating its own documentation, and to make the path absolute, so to be able to find all source code.

Now add the given below extenions at *line 33* in *conf.py*. 

After adding extensions, now make changes in *line 64* of conf.py file such as:
```
highlight_language = 'c++'
source_suffix = '.rst'
master_doc = 'index'
html_theme = 'sphinx_rtd_theme'
```
This will set the ReadTheDocs theme, and let sphinx find the source code.

Finally, we set the configuration of some of the extensions used (intersphinx, todo, and
breathe).

After making the changes in *conf.py* file, run the command given below for ***Doxygen GUI***:
```
doxywizard
```
**Note:** If Doxygen is not installed than installed by using the the commands below:

```
sudo apt-get install –y doxygen
sudo apt-get install doxygen-gui
```
#On Ubuntu (and on the Docker image, but without sudo).

Now, ***Doxygen GUI*** will open as shown in figure below:

![alt text}![Screenshot from 2023-06-02 17-05-47](https://github.com/notMuizz/RT-02-Documentation-Using-Sphinx/assets/123844091/de8242b9-680f-4d42-b3b4-f50ecc528041)


Now choose the ***working directory from which doxygen will run*** in *Step 1* as shown in figure above. After choosing the folder path, Provide some information about the project you are documenting such as: **Project Name, Project synopsis, Project version or id, Project logo** (if any), and so on. After giving the information , now ***specify the directory to scan for source code*** in *Step 2* which means add the source code directory. Mark the box for ***scan recursively***. After this, ***specify the directory where doxygen should put the generated doucmentation*** i.e. ***Destination directory*** as shown in the figure above. In our case, desination directory is *_build*. Save this as ***Doxygen.in***.

Finally, modify the ***index.rst*** script, which will be used by sphinx (together with
conf.py and (indirectly) with Doxygen.in, to build our documentation).

```
Client Module in cpp
====================
.. doxygenfile:: client.cpp
   :project: RT_2 Assingment 1
   
Odometry Module in cpp
======================
.. doxygenfile:: client_sub.cpp
   :project: RT_2 Assingment 1 ............
```
* Note: 
     <ul>
     <li>Module names depends on the nodes that designed during development of the code.</li>
    
     </ul>

Now run the command:
```
make html
```
This command will create ***indext.html*** file which is in folder *_build/html*.

![alt text]![Screenshot from 2023-06-02 16-57-39](https://github.com/notMuizz/RT-02-Documentation-Using-Sphinx/assets/123844091/27c217bd-da77-4b88-93a3-b1ec9aa73e26)


Figure above shows the *html page* of the documentation's created. 

## Outcomes

Now, the generated *HTML* files, inside *_build/html* folder, chevk the detailed documenation of the modules.


## GitHub Page

Finally, update your documentation online on **GitHub**, so that it could be visualized by people using repository.

Use GitHub to publish your doucmentation online. For this, follow the steps given below:

* Create a folder **docs**, containing documentation.

***Note:*** To add files in the *docs* folder, copy the ***html*** & ***latex*** folder drom ***_build*** folder. After that, copy all the files from html & latex folder and delete the empty folder.

* In case of Sphinx documentation, add an empty file, in the docs folder, named **".nojekyll"** (this is needed for using
the sphinx layout).
* Lastly, go to Settings of ***GitHub repository*** (for which you creayed documentation and need to create website link for the same) -> ***Pages***.
* On Pages section, make changes under GitHub Pages -> Branch. Change *branch* from none to ***main***, and */root* folder to ***/docs***. Finally, save the settings and activate an *url* which may be used to visualize the documentation.

## Final Outcome

To view the documentation visit the link given below: 

 https://notmuizz.github.io/RT-02-Documentation-Using-Sphinx/

This the *url* for the Sphinx Documentaion of the Software Architecture for Mobile Robot Control. 
