---
title: Packaging
---

Packaging
---------

Once we've made a working program, we'd like to be able to share it with others.

A good cross-platform build tool is the most important thing: you can always
have collaborators build from source.

Distribution tools
------------------

Distribution tools allow one to obtain a working copy of someone else's package.

Language-specific tools: PyPI, Ruby Gems, CPAN, CRAN
Platform specific packagers e.g. brew, apt/yum

Windows doesn't have anything like `brew install` or `apt-get`
You have to build an 'installer'.

Laying out a project
--------------------

When planning to package a project for distribution, defining a suitable
project layout is essential.

{{ bashfile('tree.sh') }}

Using setuptools
----------------

To make python code into a package, we have to write a `setupfile`:

{{ notebookfile('greetings/setup.py') }}

We can now install this code with

``` bash
sudo python setup.py install
``` 

And the package will be then available to use everywhere on the system:

``` python
import greetings
print greetings.greet("James","Hetherington")
```

And the scripts are now available as command line commands:

{{ bashfile('greetings_installed.sh') }}


Installing from GitHub
----------------------

We could now submit "greeter" to PyPI for approval, so everyone could `pip install` it.

However, when using git, we don't even need to do that: we can install directly from any git URL:

```
sudo pip install git+git://github.com/jamespjh/greeter
greet Humphry Appleby --title Sir
```

Try it!

Convert the script to a module
------------------------------

Of course, there's more to do when taking code from a quick script and turning it into a proper module:

{{ notebookfile('greetings/greetings/greeter.py') }}

Write an executable script
--------------------------

{{ notebookfile('greetings/greetings/command.py') }}

Write an entry point script stub
--------------------------------

{{ notebookfile('greetings/greetings/greeter')}}

Write a readme file
-------------------

{{ notebookfile('greetings/greetings/README.md')}}

Write a license file
-------------------

{{ notebookfile('greetings/greetings/LICENSE.md')}}

Write a citation file
-------------------

{{ notebookfile('greetings/greetings/CITATION.md') }}

Define packages and executables
-------------------------------

{{ bashfile('setup_greetings_module.sh') }}

Write some unit tests
---------------------

Separating the script from the logical module made this possible:

{{ notebookfile('greetings/greetings/test/test_greeter.py')}}

{{ notebookfile('greetings/greetings/test/fixtures/examples.yaml') }}

Developer Install
-----------------

If you modify your source files, you would now find it appeared as if the program doesn't change.

That's because pip install **copies** the file.

(On my system to /Library/Python/2.7/site-packages/: this is operating
system dependent.)

If you want to install a package, but keep working on it, you can do

```
sudo python setup.py develop
```

Distributing compiled code
--------------------------

If you're working in C++ or Fortran, there is no language specific repository.
You'll need to write platform installers for as many platforms as you want to
support.

Typically:

* `dpkg` for `apt-get` on Ubuntu and Debian
* `rpm` for `yum` on Redhat and Fedora
* `homebrew` on OSX (Possibly `macports` as well)
* An executable `msi` installer for Windows.

Homebrew
--------

Homebrew: A ruby DSL, you host off your own webpage

See my [installer for the cppcourse example](http://github.com/jamespjh/homebrew-reactor)

If you're on OSX, do:

``` bash
brew tap jamespjh/homebrew-reactor
brew install reactor
```
