# Sandboxing notes

#### pwncollege module 5 (for week 3-4)

First part:

The problem initially was that every program run on bare metal. Eventually this lead to the creation of memory seperation, with things like user mode and kernel mode and eventually scripting languages around the 1990s. <br>

Browser hacking:<br>

Browsers are a example of all functionality basically stuffed together to keep up with the demands of an ever expanding web.

Personal note: this is still the thing, for example look at the modern implementations of 3D application withing modern web-browsers, and things like WebAssembly etc.

Most of these applications also have (or had) the priblem that it run with the permission given to the user  the program ran as. If these is root or any other high-privileged user, this can in turn cause problems.

The solution to this was, and is:

- Untrusted code (i.e. downloaded JavaScript, PNGs, PDFs, etc) should live in a process wiht *almost zero permissions*.

Spawing chid-parent processes where one has the needed permissions, and the other is sandboxed, where a child ask the parent to perform, is also something implemented noadays. (This is also the ideal sandbox design).

Chroot:

Traditional sandbox: chroot jail:

* Chroot() first appeared in Unix in 1979 and then spread to BSD and later Linux etc.
* Changes the meaning of "/" for a process (and it's children)
* ```chroot("/tmp/jail")``` will disallow processes from getting out of jail
* used to be the de-facto sandboxing utility
* No syscall filtering and no isolation used

```chroot("/tmp/jail")``` has two effects:

* For this process: change the meaning of "/" to mean "/tmp/jail"
	* and everything under that: "/flag" becomes "/tmp/jail/flag"
* For this this process, change "/tmp/jail/..." to go to "/tmp/jail"

```chroot("/tmp/jail")``` does _*NOT*_:

* Close resources that are outside of the jail
* ```cd (chdir())``` into the jail
* Do antyhing else!!