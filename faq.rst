===
FAQ
===

If your question isn't answered below, check `the docs <http://ipython.github.com/ipython-doc/>`_, then ask on the `user mailing list <http://projects.scipy.org/mailman/listinfo/ipython-user>`_.

---------------------------------------------------
Running IPython against multiple versions of Python 
---------------------------------------------------
    I would like to know if there is an easy way to install parallel versions of ipython ? Actually, I would like to be able to use ipython with python 2.4 which is the default on my machine, and with python2.5 (compiled by hand); is changing the python interpreter in the ipython script the only required change ? (I was thinking about having ipython with the default interpreter and ipython2.5 using the python2.5 interpreter) ?
**Answer:** You can install IPython against various interpreters by using the following call::

    $ python2.4 setup.py install --prefix=$HOME/usr
    $ python2.5 setup.py install --prefix=$HOME/usr


In this case, the second call will overwrite the startup script of the first in `$HOME/usr/bin`, but those are the same. The important point is that each Python will find the IPython imports under `$HOME/usr/lib/python2.X/site-packages/IPython`, and assuming you have set up your `$PYTHONPATH` variable accordingly, this will work. The final step is to have aliases to call each of the IPython versions quickly, those can be defined as (using tcsh syntax)::

    alias ip4 "python2.4 $HOME/usr/bin/ipython"
    alias ip5 "python2.5 $HOME/usr/bin/ipython"


or you can just have two copies of the ipython startup script named differently and with their first line changed to point to the actual interpreter.

--------------------------------
IPython crashes under OS X when using the arrow keys
--------------------------------
Under some circumstances, using the arrow keys to navigate your input history can cause a complete crash of the Python interpreter.

**Answer:** This is due to a bug in the readline library from the official builds. There are a few solutions you can take:

 1. Use a different Python version from Apple's default (MacPython or Fink have been reported to work)

 2. You can disable in your ipythonrc file the following lines by commenting them out::

      readline_parse_and_bind "\e[A": history-search-backward
      readline_parse_and_bind "\e[B": history-search-forward

You will lose searching in your history with the arrow keys, but at least Python won't crash.

------------------------------
Does IPython play well with Windows? 
------------------------------
Yes, it most definitely does! There are some things that should be noted: `see the wiki <http://ipython.scipy.org/moin/IpythonOnWindows>`_.

---------------------------
What is the best way to install IPython? 
---------------------------
 * The classic ``python setup.py install`` still works, of course, and is recommended for Linux boxes where you have root privileges.
 * On windows you'll probably want to run the .exe installer to get the shortcuts and ipython.py in \python25\scripts.
 * ``easy_install ipython==dev`` is the easiest way to install the SVN trunk version.
 * ``easy_install ipython`` is a quick way to get ipython without downloading or unzipping anything manually, but you'll miss windows shortcuts, and documentation (man pages, pdf...) will not be where it normally is.
 * If you want to run the latest ipython instead of an older version provided with your linux distro, and don't want to remove/mess with the already existing version, don't have root privileges to install ipython, or just want to run multiple ipython versions for some reason, just untar the source distribution somewhere and launch ipython.py.

--------------------------
Why do I get garbage characters when long information is displayed by the pager? 
--------------------------

The color escapes used by IPython are not correctly interpreted by default by many common pagers ('less' included). The manual describes `here <http://ipython.scipy.org/doc/stable/html/config/initial_config.html#object-details-types-docstrings-source-code-etc>`_ the problem and its solution in detail, but the short version is that your bashrc file should contain::

    export PAGER=less
    export LESS=-r



---------------------------
Why doesn't running doctests from within IPython work?
---------------------------
This is a known problem, but there's a workaround. The reason, deep
down, is a clash between ipython's modification of sys.displayhook so
you get nice output prompts, and the fact that the exec builtin is
internally hardcoded to run sys.displayhook. So ipython collides with
doctest (which uses 'exec') and all hell breaks loose. 

Fernando Perez fperez.net at gmail.com 
Thu Jan 18 01:01:39 CST 2007 

--------------------------------------------------------------------------------

Here's the workaround. First, your error (I called your file 'dtest')::

    In [5]: doctest.testmod(dtest)
    Out[5]: 1
    **********************************************************************  
    File "dtest.py", line 8, in dtest
    Failed example:
        x()
    Expected:
        1
    Got nothing
    **********************************************************************
    1 items had failures:
    1 of   3 in dtest   
    ***Test Failed*** 1 failures.
    Out[5]: (1, 3)


Now the workaround::

    In [6]: iphook = sys.displayhook
    In [7]: sys.displayhook = sys.__displayhook__
    In [8]: doctest.testmod(dtest)

    *** DocTestRunner.merge: 'dtest' in both testers; summing outcomes.
    (0, 3)


Now you can reactivate ipython's displayhook if you want::

    In [9]: sys.displayhook = iphook


You could wrap this little sys.displayhook dance in a utility function
to ease things up.

-----------
Can IPython run under IronPython/PyPy/Jython/other Python interpreters?
-----------

The terminal-based shell should run on any interpreter which complies with
the necessary version of Python. For the 0.11 release, we will require Python 2.6
or above, and as of June 2011, IronPython and PyPy both support this.

The most likely problems would come from Readline and from using the undocumented
sys._getframe() function. On Windows we ship our own `pyreadline <pyreadline.html>`_,
which might also work under IronPython.

If IPython does not work under a supported interpreter, please
`file a bug <https://github.com/ipython/ipython/issues>`_.

