# oscomp kernel training
**2025年开源操作系统训练营 oskernel训练**

## 训练邀请：OS kernel设计与实现
- [点击：创建自己的内核赛道训练repo-riscv64](https://classroom.github.com/a/gVahDVzg)
- [点击：创建自己的内核赛道训练repo-loongarch64](https://classroom.github.com/a/MSB8JGTD)
- [点击：创建自己的内核赛道训练repo-aarch64](https://classroom.github.com/a/-g7zNh9w)
- [点击：创建自己的内核赛道训练repo-x86_64](https://classroom.github.com/a/JMgcpmAc)
- [查看训练排行榜单](https://oscontent25.github.io/classroom-grading-template/)

总共有四个赛道，测试用例基本一致。
**注：**
1. **基于Github Classroom，具有在线编程，在线自动评测，在线显示排行榜的特征**
2. **没学过git/github使用、C/Rust语言、基本数据结构和算法、操作系统和与RISC-V相关的组成原理课程的同学，建议先补一下相关知识**

## 内核赛道OS训练repo说明

> 目前支持对2025年全国大学生OS比赛内核赛道的Linux Apps测例的测试，采用形式与比赛大致相同，选手需要在根目录添加一个 Makefile 文件，使用 make all 命令在根目录生成 kernel-qemu 文件，由评测机自动执行。

- 一个基本的能运行的 `kernel demo`： [https://github.com/oscomp/starry-next](https://github.com/oscomp/starry-next)
- 一个能通过所有测例的 `complete kernel reference`：[暂不公布]()

目前已经支持 `libc-test`，`busybox`, `lua`, `iozone` 相关Linux App测例，并且需要分别支持`musl`、`glibc`，测试过程无人工干预，需要由内核自动运行，所有测例文件放在镜像中，内核需要支持 `ext4` 文件系统来读取文件。

## 本地测试

如你写好OS后，想在在本地测试，以riscv为例，评测运行指令如下：

```shell
qemu-system-riscv64 -machine virt -kernel kernel-rv -m 2G -nographic -smp 4 -bios default -drive file=sdcard-riscv64.img,if=none,format=raw,id=x0 \
    -device virtio-blk-device,drive=x0,bus=virtio-mmio-bus.0 -no-reboot -device virtio-net-device,netdev=net -netdev user,id=net \
    -rtc base=utc \
    -drive file=disk.img,if=none,format=raw,id=x1 -device virtio-blk-device,drive=x1,bus=virtio-mmio-bus.1
```

## 在线测试
github的CI对内核进行测试的执行时间设置为 `300` 秒（`5`分钟），超时后程序会被终止，不再继续执行，所得分数为超时前完成的部分的分数。

github的CI执行完毕后，你可以在相应仓库的action中查看详细结果。

## 注意事项
- `QEMU` 版本为 `9.2.1`
- `RUST ToolChain` 版本为 `nightly-2025-01-18`
- 编译目标架构为随测试架构不同而变化
- 内核执行时间为 `5` 分钟
- 内核可用内存大小为 `2G`
- 只有 `main` 分支的提交可以被Github 上的CI评测机处理
- Github 上的CI评测机在初次运行时需要编译 `qemu`，可能需要花费一些时间，请耐心等待
- 如果在实践中碰到问题，请在本repo的 `issues` 栏中发帖子
- 如果有进一步的改进，请给本repo提 `Pull requests`

