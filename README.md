

<a name="abcd"></a>
`/proc/[pid]/cmdline`是一个只读文件，包含进程的完整命令行信息。如果这个进程是`zombie`进程，则这个文件没有任何内容。请参考下面例子：    

    # cat /proc/2948/cmdline
    /usr/sbin/libvirtd--listen


[link text](#abcd)
