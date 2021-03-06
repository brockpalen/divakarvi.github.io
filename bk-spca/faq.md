## Frequently Asked Questions

#### Why not use GNU's gcc/g++ instead of Intel compilers?

Good question. When I started working on the book around 2010, my initial choice was gcc/g++. I switched to Intel for two main reasons. First, around 2010, the Intel compilers were optimizing loops better. Second, the advanced computing sites I used, [ARC at Michigan](http://arc.umich.edu/) and [TACC at Texas](https://www.tacc.utexas.edu/), defaulted to Intel compilers. In addition, the Intel compilers make it very easy to link Intel's own Math Kernel Library. The Intel compilers are also free for students.

However, I don't believe Intel optimizes loops (such as in dense matrix multiplication or transpose) better than gcc/g++ any more. The new YMM/ZMM registers have raised the difficulty of optimization considerably, and neither compiler does a good job on recent machines with YMM/ZMM registers.

In my own research, I mainly use gcc/g++. At one point, I tried to create a gcc branch in the git repository using only open source tools but could not find the time to complete it. If someone takes the time to move all the Makefiles to gcc, I will be happy to pull their branch.

Free and open source models have contributed enormously in keeping the playing field somewhat level. There is a lot of great software in the open source world. Beyond well-known examples such as Linux, gcc, and Python, the ctypes library in Python is a lesser known example that comes to mind. The volume of investment required can be huge, however, and commercialization is essential. Companies like ATT (now defunct), Intel, and IBM have come up with many remarkable innovations that are foundational to the world of computing.

#### Should I code in assembly?

In 2010, I would have answered no most of the time. However, the situation today is more complicated. Even the best C/C++ compilers don't do a decent job with the new YMM/ZMM registers, and if Intel keeps changing its architectures to  better compete with GPUs, it may be difficult for compilers to catch up. There is a much stronger case for coding in assembly today.


#### I am getting very different timings. Is something wrong?

No. Different timings are to be expected. For example, if you run the Leibniz programs from [here](https://github.com/divakarvi/bk-spca/blob/master/proc/compiler/leibniz.cpp), you will get different numbers. The only way to resolve this matter is to look at the instruction stream generated, a point that is emphasized in the [discussion](https://divakarvi.github.io/bk-spca/spca.html#toc-Subsection-3.2.2).

In the [discussion](https://divakarvi.github.io/bk-spca/spca.html#toc-Subsection-3.2.5) of matrix multiplication, it is noted that the same Intel compiler does a much better job on the older SSE2 than the newer AVX2 for multIJKX(). Compilers can be quite unpredictable, and that will not change.

We can attempt to be rational about the connection between the instruction stream and program speed. However, the passage from C/C++ to the instruction stream is always subject to the whims of the compiler.
