# seccomp

*Notes as part of module 5 of the 2022 pwn college course I follow*

Modern sandboxes *heavily* restrict permitted system calls trough the use of a kernel-level sandboxing mechanism: seccomp

seccomp allows developers to write complex rules to:

* Allow certain system calls
* Dissallow certain system calls
* Filter allowed and dissallowed system calls based on arguments variables

Seccomp rules are inherted by children!

These rules can be quite complex 
(see http://man7.org/linux/man-pages/man3/seccomp_rule_add.3.html) 

