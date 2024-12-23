## <a id="title_qemu">在 qemu-system-riscv64 模拟器上运行</a>
首先，确保 `qemu-system-riscv64` 已经下载到您的机器上并且加到了环境变量中；  
其次，需要一个 FAT32 磁盘镜像文件；
```bash
make fs
```
这会生成一个镜像文件 `fs.img` ，编译一些用户程序（如 `shell`）并拷贝至镜像中。只要 `fs.img` 存在并且不需要修改，您不必每次运行前都执行这个命令。

最后，开始运行：
```bash
make run platform=qemu
```

Ps: 按 `Ctrl + A` 然后 `X` 退出 `qemu`。     

## 添加用户程序
1. 在 `xv6-user/` 目录下新建一个 C 文件，如 `myprog.c`，然后写入您的代码；
2. 您可以引入 `user.h` 头文件，以使用其中提供的函数，如 `open`、`gets` 和 `printf`等；
3. 在 `Makefile` 中添加一行 “`$U/_myprog\`”，具体如下：
    ```Makefile
    UPROGS=\
        $U/_init\
        $U/_sh\
        $U/_cat\
        ...
        $U/_myprog\      # 请不要忽略开头的 '_'
    ```
4. 然后执行：
    ```bash
    make userprogs
    ```
    如果没有出错，您应该可以在 `xv6-user/` 中看到 `_myprog` 文件。最后，您需要将它拷贝到SD卡(参考<a href="#title_k210">此处</a>)
    或磁盘镜像(参考<a href="#title_qemu">此处</a>)中。

## 进度
- [x] 多核启动
- [x] 裸机 printf
- [x] 内存分配
- [x] 页表
- [x] 时钟中断
- [x] S 态外部中断
- [x] 接收 `UARTHS` 串口数据
- [x] SD card 驱动
- [x] 进程管理
- [x] 文件系统
- [x] 用户程序
- [X] 稳定的键盘输入（k210）

## TODO


