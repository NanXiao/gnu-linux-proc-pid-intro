[/proc/[pid]/cmdline](#cmdline)  
[/proc/[pid]/cwd](#cwd)  
[/proc/[pid]/environ](#environ)  
[/proc/[pid]/exe](#exe)  
[/proc/[pid]/root](#root)  

## cmdline
`/proc/[pid]/cmdline`是一个只读文件，包含进程的完整命令行信息。如果这个进程是`zombie`进程，则这个文件没有任何内容。举例如下：    

    # ps -ef | grep 2948
    root       2948      1  0 Nov05 ?        00:00:04 /usr/sbin/libvirtd --listen

    # cat /proc/2948/cmdline
    /usr/sbin/libvirtd--listen

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

## root
`/proc/[pid]/root`是进程根目录的符号链接。举例如下： 

    # ls -lt /proc/2948/root
    lrwxrwxrwx 1 root root 0 Nov  9 12:14 /proc/2948/root -> /

