~~~~~~~~
Download
~~~~~~~~

Stable Releases
---------------

Our `downloads <http://ipython.scipy.org/dist>`_ directory for source distributions
for Linux, Unix, Mac OS X and binaries for Windows.

The current stable release, version 0.10.2, can be downloaded directly as:

* A `compressed source archive in .tar.gz <http://ipython.scipy.org/dist/0.10.2/ipython-0.10.2.tar.gz>`_ format.
* A `compressed source archive in .zip <http://ipython.scipy.org/dist/0.10.2/ipython-0.10.2.zip>`_ format.
* An `egg for Python 2.6 <http://ipython.scipy.org/dist/0.10.2/ipython-0.10.2-py2.6.egg>`_.
* A `binary Windows installer <http://ipython.scipy.org/dist/0.10.2/ipython-0.10.2.win32-setup.exe>`_ (an executable setup file).


Note that most major Unix distributions now include IPython in their package
systems (Ubuntu, Debian, Fedora, SUSE, fink, FreeBSD, OpenBSD,...). It is also
available `on PyPI <http://pypi.python.org/pypi/ipython>`_, so it can be installed
with tools such as ``easy_install`` and ``pip``.

The same `downloads <http://ipython.scipy.org/dist>`_ directory contains links to older versions.

Installation instructions
-------------------------

Like most Python packages, IPython can be installed from source with the command
``python setup.py install``. Full installation instructions can be found in our official 
`documentation <http://ipython.github.com/ipython-doc/stable/html/install/install.html>`_. 

Readline
--------

IPython relies on the readline library for features like tab completion.

* Most Linux distributions will have readline already.
* For Mac OS X, readline can be installed `from PyPI <http://pypi.python.org/pypi/readline>`_.
  The alternative (libedit) shipped with OS X is known to cause problems in IPython.
* Under Windows, the functionality is provided by the `PyReadline <pyreadline.html>`_
  project, also hosted on this site.
