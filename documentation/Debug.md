Debug
==

> Debugfs exists as a simple way for kernel developers to make information available to user space.  Unlike /proc, which is only meant for information about a process, or sysfs, which has strict one-value-per-file rules, debugfs has no rules at all.


    root@edison:~# mount -t debugfs none /sys/kernel/debug

# Links

- https://www.kernel.org/doc/Documentation/filesystems/debugfs.txt
- https://www.kernel.org/doc/Documentation/sysrq.txt