#Python即时编译器PyPy 4发布，支持SIMD矢量、性能改进等 

## 摘要：
PyPy是Python的一个即时编译器，PyPy 4.0是其最新发布的一个大版本，带来很多新的特性，诸如支持SIMD矢量、预热时间的改进、以及对Numpy的改进。PyPy声称要比Cpython快6倍以上。

--------------------------------------------------

[PyPy](http://morepypy.blogspot.com.es/2015/10/pypy-400-released-jit-with-simd.html) 是Python的一个即时编译器，PyPy 4.0是其最新发布的一个大版本，带来很多新的特性，诸如支持SIMD矢量、预热时间的改进、以及对Numpy的改进。PyPy[声称](http://speed.pypy.org/)要比Cpython快6倍以上。

PyPy 4的SIMD矢量会在追踪代码时启用，而且会自动探测到可用的SIMD硬件从而[提高常见的向量和矩阵操作](http://morepypy.blogspot.com.es/2015/10/automatic-simd-vectorization-support-in.html)。根据版本的公告，实时矢量相比前置（ahead-of-time）矢量更具有领先优势，因为其更加的容易探测到可能的矢量。

在性能方面，PyPy的内部进行重构从而能够更有效的使用[guards](http://rpython.readthedocs.org/en/latest/glossary.html)。它能够减少20%的内存消耗，而且改进了unrolling，这样可以较少20%的预热时间。

PyPy中的[Numpy](https://bitbucket.org/pypy/numpy)和Python的NumPy扩展是一个道理。Python的NumPy曾经[谈及](http://stackoverflow.com/questions/18946662/why-shouldnt-i-use-pypy-over-cpython-if-pypy-is-6-3-times-faster)，NumPy是能够将使用PyPy的开发者们纠回到Python本身的一个理由。在PyPy 4.0，Numpy带来了新的扩展支持，如ndarray和数字的dtypes，这也就意味着Numpy的功能接近完善。对于record、string、以及unicode dtypes的支持都有所改进。

PyPy 4.0目的是兼容CPython2.7。对于缺少对Python3的支持[被认为](https://news.ycombinator.com/item?id=10470428)是人们采用PyPy的一个限制因素。事实上，PyPy3是兼容Python3.2.5的，而且PyPy团队正在尝试[启动](http://pypy.org/py3donate.html)对Python3.4的支持。

在迁移到PyPy之前还应该考虑另外两个因素，一个是PyPy还缺乏像C Python那样的扩展如Pandas，SciPy等的等量支持，这样的话，若是用户使用了这些扩展的话，PyPy就不如C Python效率更高；另外一个就是，PyPy为其即时编译器带来的好处是对长时间运行的脚本支持，若是简单而短小的脚本的话，预热时间就显得长了点。

更多关于PyPy 4.0的细节请参考其官方[声明](http://morepypy.blogspot.com.es/2015/10/pypy-400-released-jit-with-simd.html)。PyPy 4可以在[这里下载](http://pypy.org/download.html)。

查看英文原文：[Python JIT Compiler PyPy 4 Brings SMD Vectorization,Performance Improvements,and More](http://www.infoq.com/news/2015/11/pypy-4-released)
