[/proc/[pid]/auxv](#auxv)  
[/proc/[pid]/cmdline](#cmdline)  
[/proc/[pid]/comm](#comm)  
[/proc/[pid]/cwd](#cwd)  
[/proc/[pid]/environ](#environ)  
[/proc/[pid]/exe](#exe)  
[/proc/[pid]/maps](#maps)  
[/proc/[pid]/root](#root)  

## auxv
`/proc/[pid]/auxv`包含传递给进程的`ELF`解释器信息，格式是每一项都是一个`unsigned long`长度的`ID`加上一个`unsigned long`长度的值。最后一项以连续的两个`0x00`开头。举例如下：  

    # hexdump -x /proc/2948/auxv
    0000000    0021    0000    0000    0000    0000    1a82    7ffd    0000
    0000010    0010    0000    0000    0000    dbf5    1fc9    0000    0000
    0000020    0006    0000    0000    0000    1000    0000    0000    0000
    0000030    0011    0000    0000    0000    0064    0000    0000    0000
    0000040    0003    0000    0000    0000    2040    4326    7f4a    0000
    0000050    0004    0000    0000    0000    0038    0000    0000    0000
    0000060    0005    0000    0000    0000    0009    0000    0000    0000
    0000070    0007    0000    0000    0000    f000    4303    7f4a    0000
    0000080    0008    0000    0000    0000    0000    0000    0000    0000
    0000090    0009    0000    0000    0000    8e67    4327    7f4a    0000
    00000a0    000b    0000    0000    0000    0000    0000    0000    0000
    00000b0    000c    0000    0000    0000    0000    0000    0000    0000
    00000c0    000d    0000    0000    0000    0000    0000    0000    0000
    00000d0    000e    0000    0000    0000    0000    0000    0000    0000
    00000e0    0017    0000    0000    0000    0000    0000    0000    0000
    00000f0    0019    0000    0000    0000    3de9    1a80    7ffd    0000
    0000100    001f    0000    0000    0000    4fe5    1a80    7ffd    0000
    0000110    000f    0000    0000    0000    3df9    1a80    7ffd    0000
    0000120    0000    0000    0000    0000    0000    0000    0000    0000
    0000130
解析这个文件可以参考这段[代码](http://www.wienand.org/junkcode/linux/read-auxv.c)。

## cmdline
`/proc/[pid]/cmdline`是一个只读文件，包含进程的完整命令行信息。如果这个进程是`zombie`进程，则这个文件没有任何内容。举例如下：    

    # ps -ef | grep 2948
    root       2948      1  0 Nov05 ?        00:00:04 /usr/sbin/libvirtd --listen

    # cat /proc/2948/cmdline
    /usr/sbin/libvirtd--listen

## comm
`/proc/[pid]/comm`包含进程的命令名。举例如下：  

    # cat /proc/2948/comm
    libvirtd

##cwd  
`/proc/[pid]/cwd`是进程当前工作目录的符号链接。举例如下：  

    # ls -lt /proc/2948/cwd
    lrwxrwxrwx 1 root root 0 Nov  9 12:14 /proc/2948/cwd -> /


## environ  
`/proc/[pid]/environ`显示进程的环境变量。举例如下：  

    # strings /proc/2948/environ
    LANG=POSIX
    LC_CTYPE=en_US.UTF-8
    PATH=/usr/local/sbin:/usr/local/bin:/usr/sbin:/usr/bin:/sbin:/bin
    NOTIFY_SOCKET=@/org/freedesktop/systemd1/notify
    LIBVIRTD_CONFIG=/etc/libvirt/libvirtd.conf
    LIBVIRTD_ARGS=--listen
    LIBVIRTD_NOFILES_LIMIT=2048

## exe
`/proc/[pid]/exe`为实际运行程序的符号链接。举例如下：  

    # ls -lt /proc/2948/exe
    lrwxrwxrwx 1 root root 0 Nov  5 13:04 /proc/2948/exe -> /usr/sbin/libvirtd

## maps
`/proc/[pid]/maps`显示进程的内存区域映射信息。举例如下：  

    # cat /proc/2948/maps
    ......
    address                   perms offset  dev   inode                      pathname
    7f4a2e2ad000-7f4a2e2ae000 rw-p 00006000 08:14 6505977                    /usr/lib64/sasl2/libsasldb.so.3.0.0
    7f4a2e2ae000-7f4a2e2af000 ---p 00000000 00:00 0
    7f4a2e2af000-7f4a2eaaf000 rw-p 00000000 00:00 0                          [stack:94671]
    7f4a2eaaf000-7f4a2eab0000 ---p 00000000 00:00 0
    7f4a2eab0000-7f4a2f2b0000 rw-p 00000000 00:00 0                          [stack:94670]
    ......
    7f4a434d0000-7f4a434d5000 rw-p 0006e000 08:14 4292988                    /usr/sbin/libvirtd
    7f4a4520a000-7f4a452f7000 rw-p 00000000 00:00 0                          [heap]
    7ffd1a7e4000-7ffd1a805000 rw-p 00000000 00:00 0                          [stack]
    7ffd1a820000-7ffd1a821000 r-xp 00000000 00:00 0                          [vdso]
    ffffffffff600000-ffffffffff601000 r-xp 00000000 00:00 0                  [vsyscall]

其中注意的一点是`[stack:<tid>]`是线程的堆栈信息，对应于`/proc/[pid]/task/[tid]/`路径。  

## root
`/proc/[pid]/root`是进程根目录的符号链接。举例如下： 

    # ls -lt /proc/2948/root
    lrwxrwxrwx 1 root root 0 Nov  9 12:14 /proc/2948/root -> /

