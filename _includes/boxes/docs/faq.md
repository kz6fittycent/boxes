# FAQ

These are the frequently asked questions about the *boxes* program and their answers.

These questions are *actually* "frequently asked". For general information on the *boxes* program, installation instructions, and information on box design creation please refer to the [*boxes* documentation]({{ site.baseurl }}/docs/).


<a class="bxOffsetAnchor" name="q1"></a>

### Q. 1. What is a text filter program?

There is a [separate page]({{ site.baseurl }}/docs/filters.html) explaining this. *Boxes* is mostly used as such a filter program. 


<a class="bxOffsetAnchor" name="q2"></a>

### Q. 2. I have compiled and installed boxes, but when I run it, I get an error message "input in flex scanner failed"!

Upgrade to version 1.0.1 or later. Versions prior to 1.0.1 gave this error message when the config file they were trying to read was in fact a directory. The global config file name is */usr/share/boxes* on most systems. This is the name of the file, not the name of a directory into which a config file would be placed.


<a class="bxOffsetAnchor" name="q3"></a>

### Q. 3. Boxes destroys my tabs!

By default, all tab characters are replaced by spaces. However, you can change this behavior using the `-t` option (since version 1.1). The `-t` option only affects leading tabs. Tabs which end up inside the box are *always* converted into spaces.
Note that you can also set the tab stop distance (== how many spaces per tab) using the `-t` option.


<a class="bxOffsetAnchor" name="q4"></a>

### Q. 4. "Can't read file C:\TEMP\VIO44.TMP" when calling boxes from vim

On Windows, this error message may appear instead of a box when *boxes* is called from vim. This is not a problem of *boxes*. In fact, it's a misleading message from the vim editor which is supposed to tell you that *boxes* is not in your PATH. Solution: Copy *boxes.exe* and *boxes.cfg* to a directory which is in your PATH. (thanks *Jeff Lanzarotta*, 05-Jul-00)


<a class="bxOffsetAnchor" name="q5"></a>

### Q. 5. Compilation

The current version includes changes to solve all compilation issues reported to the author. So please check that you are using the most current version. Still, there are many different systems out there, so here's a short list of things to try:

- `-traditional` flag for regexp package:
  Some systems may require you to set or clear the `-traditional` flag from the `CFLAGS` definition in *src/regexp/Makefile*.

- Warnings from flex or bison:
  If you get warnings from flex or bison, do a `make clean ; make` from the top level directory. The following warning is harmless:

      lexer.l:1309: warning: `yy_flex_realloc' defined but not used

  It's a known bug in flex, and has no impact on boxes. You can safely ignore this warning.

- `Bad address` on *boxes* execution after compiling on a 64bit system:
  This may happen when the system you are compiling on is 64bit. Boxes is only a 32bit program, so the compiler may have to be forced to 32bit by adding the `-m32` option. (Thanks to <span class="atmention">[@stefanow](https://github.com/stefanow)</span> for [supplying](https://github.com/{{ site.github }}/issues/7) this information!)
  In order to do this, use the following command line (works with current sources):

      make CFLAGS_ADDTL=-m32 LDFLAGS_ADDTL=-m32