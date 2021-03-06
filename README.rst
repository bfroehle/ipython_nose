ipython_nose
------------

This little IPython extension gives you the ability to discover and
run tests using Nose in an IPython Notebook. To use it:

* make sure your IPython Notebook server can import ipython_nose.py
  (e.g. copy it to a directory in your ``PYTHONPATH``, or modify
  ``PYTHONPATH`` before starting IPython Notebook)

* add a cell containing::

    %load_ext ipython_nose

  somewhere in your notebook

* write tests that conform to Nose conventions, e.g.::

    def test_arithmetic():
        assert 1+1 == 2

* add a cell consisting of::

    %nose

  to your notebook and run that cell. That will discover your
  ``test_*`` functions, run them, and report how many passed and
  how many failed, with stack traces for each failure.


Caveats
-------

* There's no way to pass various Nose options, e.g. a custom
  regex for finding test functions, or selecting tests. Fixable.

* Renaming tests leaves behind the old name: you might only see N
  test methods in your notebook, but Nose will discover and run N+1
  tests. Not sure how to fix this one.

* There are no links between the stack traces and the code: for
  example, a stack trace that looks like::

    Traceback (most recent call last):
      File "/usr/lib/python2.7/dist-packages/nose/case.py", line 197, in runTest
        self.test(*self.arg)
      File "<ipython-input-10-a3ae96abafeb>", line 2, in test_myfunc
        assert myfunc() == 42
    AssertionError

  has the information you need to jump to the failing code, but does
  nothing with it. In particular, that synthetic filename
  (ipython-input-10-a3ae96abafeb) means that test_myfunc() is in
  cell #10 of your notebook. Go to that cell, then line 2, and you
  find the failing test. ipython_nose needs some UI magic to make
  this transparent.

TODO
----

* Display passing tests (like ``nose -v``).
* Have a cell magic to only run test-like things in the current cell, e.g.::

    %%nose
    
    def test_just_this():
        assert True


Authors
-------

* Taavi Burns <taavi at taaviburns dot ca>
* Greg Ward <greg at gerg dot ca>

Thanks to Fernando Perez and Greg Wilson for tips, ideas, etc.


Get the code
------------

::

  git clone https://github.com/taavi/ipython_nose.git


Copyright
---------

Copyright (c) 2012, Taavi Burns, Greg Ward.

All rights reserved.

Redistribution and use in source and binary forms, with or without
modification, are permitted provided that the following conditions are met:

Redistributions of source code must retain the above copyright notice, this
list of conditions and the following disclaimer.

Redistributions in binary form must reproduce the above copyright notice, this
list of conditions and the following disclaimer in the documentation and/or
other materials provided with the distribution.

Neither the name of the developers nor the names of contributors may
be used to endorse or promote products derived from this software
without specific prior written permission.

THIS SOFTWARE IS PROVIDED BY THE COPYRIGHT HOLDERS AND CONTRIBUTORS "AS IS" AND
ANY EXPRESS OR IMPLIED WARRANTIES, INCLUDING, BUT NOT LIMITED TO, THE IMPLIED
WARRANTIES OF MERCHANTABILITY AND FITNESS FOR A PARTICULAR PURPOSE ARE
DISCLAIMED.  IN NO EVENT SHALL THE COPYRIGHT OWNER OR CONTRIBUTORS BE LIABLE
FOR ANY DIRECT, INDIRECT, INCIDENTAL, SPECIAL, EXEMPLARY, OR CONSEQUENTIAL
DAMAGES (INCLUDING, BUT NOT LIMITED TO, PROCUREMENT OF SUBSTITUTE GOODS OR
SERVICES; LOSS OF USE, DATA, OR PROFITS; OR BUSINESS INTERRUPTION) HOWEVER
CAUSED AND ON ANY THEORY OF LIABILITY, WHETHER IN CONTRACT, STRICT LIABILITY,
OR TORT (INCLUDING NEGLIGENCE OR OTHERWISE) ARISING IN ANY WAY OUT OF THE USE
OF THIS SOFTWARE, EVEN IF ADVISED OF THE POSSIBILITY OF SUCH DAMAGE.
