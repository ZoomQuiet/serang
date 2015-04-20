http://www.ferg.org/papers/debugging_in_python.html


Python has a debugger, which is available as a module called pdb  (for "Python DeBugger", naturally!). Unfortunately, most discussions of pdb are not very useful to a Python newbie -- most are very terse and simply rehash the description of pdb in the Python library reference manual. The discussion that I have found most accessible is in the first four pages of Chapter 27 of the Python 2.1 Bible.

So here is my own personal gentle introduction to using pdb. It assumes that you are not using any IDE -- that you're coding Python with a text editor and running your Python programs from the command line.
Some Other Debugger Resources

  * For information on the IDLE interactive debugger, go to http://www.python.org/idle/doc/idle2.html#Debugger
  * For information on the Wing IDE debugger, go to http://wingide.com/psupport/wingide-1.1/node7.html
```
        import pdb#<==
        a = "aaa"
        pdb.set_trace()#<==
        b = "bbb"
        c = "ccc"
        final = a + b + c
        print final

```