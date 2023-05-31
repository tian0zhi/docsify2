
---
# **编程工具**
---

## **GCC**

[gcc安装&编译连接原理](http://t.csdn.cn/jIP9G)


## **Linux**

- ldd命令，用来查看 .so或 .exe的动态链接依赖
```bash
user:/path# ldd ./build_app/example-app
out:
        linux-vdso.so.1 (0x00007ffdfa9c6000)
        libc10.so => /home/ubuntu/C_plus_plus/libtorch/lib/libc10.so (0x00007f9d1d991000)
        libtorch_cpu.so => /home/ubuntu/C_plus_plus/libtorch/lib/libtorch_cpu.so (0x00007f9d07452000)
        libtorch.so => /home/ubuntu/C_plus_plus/libtorch/lib/libtorch.so (0x00007f9d1d8f4000)
        libgomp.so.1 => /home/ubuntu/C_plus_plus/shard_lib/libgomp.so.1 (0x00007f9d07223000)
        /lib64/ld-linux-x86-64.so.2 (0x00007f9d1d7e7000)
        libc.so.6 => /home/ubuntu/C_plus_plus/shard_lib/libc.so.6 (0x00007f9d06e32000)
        libgcc_s.so.1 => /home/ubuntu/C_plus_plus/shard_lib/libgcc_s.so.1 (0x00007f9d06c1a000)
        libm.so.6 => /home/ubuntu/C_plus_plus/shard_lib/libm.so.6 (0x00007f9d0687c000)
        libstdc++.so.6 => /home/ubuntu/C_plus_plus/shard_lib/libstdc++.so.6 (0x00007f9d064f3000)
        libgomp-52f2fd74.so.1 => /home/ubuntu/C_plus_plus/libtorch/lib/libgomp-52f2fd74.so.1 (0x00007f9d062c0000)
        libpthread.so.0 => /lib/x86_64-linux-gnu/libpthread.so.0 (0x00007f9d060a1000)
        librt.so.1 => /lib/x86_64-linux-gnu/librt.so.1 (0x00007f9d05e99000)
        libdl.so.2 => /lib/x86_64-linux-gnu/libdl.so.2 (0x00007f9d05c95000)
user:/path# ldd ./libtorch/lib/libtorch_cpu.so
out:
        linux-vdso.so.1 (0x00007ffe6a1c0000)
        libgomp-52f2fd74.so.1 => /home/ubuntu/C_plus_plus/./libtorch/lib/libgomp-52f2fd74.so.1 (0x00007ff6a9cd8000)
        libpthread.so.0 => /lib/x86_64-linux-gnu/libpthread.so.0 (0x00007ff6a9ab9000)
        librt.so.1 => /lib/x86_64-linux-gnu/librt.so.1 (0x00007ff6a98b1000)
        libgcc_s.so.1 => /lib/x86_64-linux-gnu/libgcc_s.so.1 (0x00007ff6a9699000)
        libdl.so.2 => /lib/x86_64-linux-gnu/libdl.so.2 (0x00007ff6a9495000)
        libm.so.6 => /lib/x86_64-linux-gnu/libm.so.6 (0x00007ff6a90f7000)
        libc10.so => /home/ubuntu/C_plus_plus/./libtorch/lib/libc10.so (0x00007ff6c0200000)
        libstdc++.so.6 => /usr/lib/x86_64-linux-gnu/libstdc++.so.6 (0x00007ff6a8d6e000)
        libc.so.6 => /lib/x86_64-linux-gnu/libc.so.6 (0x00007ff6a897d000)
        /lib64/ld-linux-x86-64.so.2 (0x00007ff6c0062000)
```

- objdump 命令， 用来查看 .so 或 .exe 中的函数

```bash
user:/path# objdump -tT ./libtorch/lib/libtorch_cpu.so | grep powf
out:
000000000ea9fd90 l     F .text  0000000000000094              _ZN4dnnl4impl3cpu12_GLOBAL__N_118fast_negative_powfEff
00000000105a8b20 l     F .text  000000000000014d              disp_powf4_u10
0000000015a60708 l     O .data  0000000000000008              pnt_powf4_u10
00000000105a9450 l     F .text  000000000000014d              disp_fastpowf4_u3500
0000000015a60690 l     O .data  0000000000000008              pnt_fastpowf4_u3500
00000000105b4600 l     F .text  0000000000000173              disp_fastpowf8_u3500
0000000015a60b40 l     O .data  0000000000000008              pnt_fastpowf8_u3500
00000000105b5680 l     F .text  0000000000000173              disp_powf8_u10
0000000015a60bb8 l     O .data  0000000000000008              pnt_powf8_u10
00000000106414f0 g     F .text  000000000000023d              Sleef_cinz_fastpowf4_u3500sse2
0000000010640ad0 g     F .text  0000000000000a1d              Sleef_cinz_powf4_u10sse2
000000001061d1a0 g     F .text  0000000000000226              Sleef_cinz_fastpowf4_u3500sse4
000000001061c770 g     F .text  0000000000000a25              Sleef_cinz_powf4_u10sse4
00000000105fbf80 g     F .text  00000000000002e4              Sleef_cinz_fastpowf8_u3500avx
00000000105fb370 g     F .text  0000000000000c04              Sleef_cinz_powf8_u10avx
00000000105e30a0 g     F .text  00000000000002cf              Sleef_finz_fastpowf8_u3500fma4
00000000105e2a50 g     F .text  0000000000000648              Sleef_finz_powf8_u10fma4
00000000105cf000 g     F .text  00000000000001db              Sleef_finz_fastpowf4_u3500avx2128
00000000105ceb20 g     F .text  00000000000004d8              Sleef_finz_powf4_u10avx2128
00000000105bcad0 g     F .text  00000000000001db              Sleef_finz_fastpowf8_u3500avx2
00000000105bc5c0 g     F .text  000000000000050e              Sleef_finz_powf8_u10avx2
00000000105b7db0 g     F .text  0000000000000006              Sleef_fastpowf8_u3500
00000000105bc5c0 g     F .text  000000000000050e              Sleef_powf8_u10avx2
00000000105e2a50 g     F .text  0000000000000648              Sleef_powf8_u10fma4
00000000105fb370 g     F .text  0000000000000c04              Sleef_powf8_u10avx
00000000105bcad0 g     F .text  00000000000001db              Sleef_fastpowf8_u3500avx2
00000000105e30a0 g     F .text  00000000000002cf              Sleef_fastpowf8_u3500fma4
00000000105fbf80 g     F .text  00000000000002e4              Sleef_fastpowf8_u3500avx
00000000105aa350 g     F .text  0000000000000006              Sleef_fastpowf4_u3500
00000000105cf000 g     F .text  00000000000001db              Sleef_fastpowf4_u3500avx2128
000000001061d1a0 g     F .text  0000000000000226              Sleef_fastpowf4_u3500sse4
00000000106414f0 g     F .text  000000000000023d              Sleef_fastpowf4_u3500sse2
00000000105ceb20 g     F .text  00000000000004d8              Sleef_powf4_u10avx2128
000000001061c770 g     F .text  0000000000000a25              Sleef_powf4_u10sse4
0000000010640ad0 g     F .text  0000000000000a1d              Sleef_powf4_u10sse2
0000000000000000       F *UND*  0000000000000000              powf
0000000000000000       F *UND*  0000000000000000              cpowf
00000000105b7cc0 g     F .text  0000000000000006              Sleef_powf8_u10
00000000105aa260 g     F .text  0000000000000006              Sleef_powf4_u10
0000000000000000      DF *UND*  0000000000000000  GLIBC_2.27  powf
0000000000000000      DF *UND*  0000000000000000  GLIBC_2.2.5 cpowf
00000000105aa260 g    DF .text  0000000000000006  Base        Sleef_powf4_u10
00000000105ceb20 g    DF .text  00000000000004d8  Base        Sleef_finz_powf4_u10avx2128
00000000105fb370 g    DF .text  0000000000000c04  Base        Sleef_powf8_u10avx
0000000010640ad0 g    DF .text  0000000000000a1d  Base        Sleef_powf4_u10sse2
000000001061c770 g    DF .text  0000000000000a25  Base        Sleef_powf4_u10sse4
00000000105e30a0 g    DF .text  00000000000002cf  Base        Sleef_fastpowf8_u3500fma4
00000000105bc5c0 g    DF .text  000000000000050e  Base        Sleef_powf8_u10avx2
00000000105fb370 g    DF .text  0000000000000c04  Base        Sleef_cinz_powf8_u10avx
00000000105cf000 g    DF .text  00000000000001db  Base        Sleef_finz_fastpowf4_u3500avx2128
00000000105bcad0 g    DF .text  00000000000001db  Base        Sleef_finz_fastpowf8_u3500avx2
00000000105bc5c0 g    DF .text  000000000000050e  Base        Sleef_finz_powf8_u10avx2
00000000105b7cc0 g    DF .text  0000000000000006  Base        Sleef_powf8_u10
00000000106414f0 g    DF .text  000000000000023d  Base        Sleef_cinz_fastpowf4_u3500sse2
000000001061d1a0 g    DF .text  0000000000000226  Base        Sleef_cinz_fastpowf4_u3500sse4
00000000105ceb20 g    DF .text  00000000000004d8  Base        Sleef_powf4_u10avx2128
00000000105cf000 g    DF .text  00000000000001db  Base        Sleef_fastpowf4_u3500avx2128
00000000105b7db0 g    DF .text  0000000000000006  Base        Sleef_fastpowf8_u3500
0000000010640ad0 g    DF .text  0000000000000a1d  Base        Sleef_cinz_powf4_u10sse2
000000001061c770 g    DF .text  0000000000000a25  Base        Sleef_cinz_powf4_u10sse4
00000000105bcad0 g    DF .text  00000000000001db  Base        Sleef_fastpowf8_u3500avx2
00000000105fbf80 g    DF .text  00000000000002e4  Base        Sleef_fastpowf8_u3500avx
00000000105fbf80 g    DF .text  00000000000002e4  Base        Sleef_cinz_fastpowf8_u3500avx
00000000106414f0 g    DF .text  000000000000023d  Base        Sleef_fastpowf4_u3500sse2
000000001061d1a0 g    DF .text  0000000000000226  Base        Sleef_fastpowf4_u3500sse4
00000000105aa350 g    DF .text  0000000000000006  Base        Sleef_fastpowf4_u3500
00000000105e2a50 g    DF .text  0000000000000648  Base        Sleef_powf8_u10fma4
00000000105e30a0 g    DF .text  00000000000002cf  Base        Sleef_finz_fastpowf8_u3500fma4
00000000105e2a50 g    DF .text  0000000000000648  Base        Sleef_finz_powf8_u10fma4
```

- 查看glibc 版本

```bash
user:/path# strings /lib/x86_64-linux-gnu/libc.so.6 | grep GLIBC
out:
GLIBC_2.2.5
GLIBC_2.2.6
GLIBC_2.3
GLIBC_2.3.2
GLIBC_2.3.3
GLIBC_2.3.4
GLIBC_2.4
GLIBC_2.5
GLIBC_2.6
GLIBC_2.7
GLIBC_2.8
GLIBC_2.9
GLIBC_2.10
GLIBC_2.11
GLIBC_2.12
GLIBC_2.13
GLIBC_2.14
GLIBC_2.15
GLIBC_2.16
GLIBC_2.17
GLIBC_2.18
GLIBC_2.22
GLIBC_2.23
GLIBC_2.24
GLIBC_2.25
GLIBC_2.26
GLIBC_2.27
GLIBC_PRIVATE
GNU C Library (Ubuntu GLIBC 2.27-3ubuntu1.6) stable release version 2.27.


user:/path# strings /usr/lib/x86_64-linux-gnu/libstdc++.so.6 | grep GLIBC
out:
GLIBCXX_3.4
GLIBCXX_3.4.1
GLIBCXX_3.4.2
GLIBCXX_3.4.3
GLIBCXX_3.4.4
GLIBCXX_3.4.5
GLIBCXX_3.4.6
GLIBCXX_3.4.7
GLIBCXX_3.4.8
GLIBCXX_3.4.9
GLIBCXX_3.4.10
GLIBCXX_3.4.11
GLIBCXX_3.4.12
GLIBCXX_3.4.13
GLIBCXX_3.4.14
GLIBCXX_3.4.15
GLIBCXX_3.4.16
GLIBCXX_3.4.17
GLIBCXX_3.4.18
GLIBCXX_3.4.19
GLIBCXX_3.4.20
GLIBCXX_3.4.21
GLIBCXX_3.4.22
GLIBCXX_3.4.23
GLIBCXX_3.4.24
GLIBCXX_3.4.25
GLIBC_2.2.5
GLIBC_2.3
GLIBC_2.14
GLIBC_2.4
GLIBC_2.18
GLIBC_2.16
GLIBC_2.3.4
GLIBC_2.17
GLIBC_2.3.2
GLIBCXX_DEBUG_MESSAGE_LENGTH

```