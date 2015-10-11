Debug
==

> Debugfs exists as a simple way for kernel developers to make information available to user space.  Unlike /proc, which is only meant for information about a process, or sysfs, which has strict one-value-per-file rules, debugfs has no rules at all.


    root@edison:~# mount -t debugfs none /sys/kernel/debug


    Kernel hacking
        [*] Kernel debugging
        [*]   Magic SysRq key
        [*]   Debug filesystem
        [*]   Detect Soft Lockups
        [ ]   Collect scheduler statistics
        [*]   Debug slab memory allocations
        [*]     Memory leak debugging
        [*]   Mutex debugging, deadlock detection
        [*]   Spinlock debugging
        [*]   Sleep-inside-spinlock checking
        [ ]   kobject debugging
        [ ]   Highmem debugging
        [ ]   Compile the kernel with debug info
    
# Links

- https://www.kernel.org/doc/Documentation/filesystems/debugfs.txt
- https://www.kernel.org/doc/Documentation/sysrq.txt