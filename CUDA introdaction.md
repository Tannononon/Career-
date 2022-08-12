# CUDA introdaction

CUDA (Compute Unified Device Architecture)，由英伟达公司2007年开始推出，初衷是为 GPU 增加一个易用的编程接口，让开发者无需学习复杂的着色语言或者图形处理原语。

cpu调用gpu核函数时是通过PCI总线进行信息传输的

<img width="638" alt="image" src="https://user-images.githubusercontent.com/99408013/183680339-f0169ccf-1d21-4cd3-84d8-694827d0e915.png">

## 1.CUDA程序处理流程
1. 将cpu内存中的数据通过总线拷贝到gpu内存中
2. 加载gpu程序并执行，在gpu芯片山缓存数据以提升性能
3. 将结果从gpu内存中拷贝到cpu中

## 2. 流计算方式

相对于传统计算方式来说，流计算方式可以对大规模流动性不断运动的过程中进行实时分析，捕捉可用信息，并将可用信息传输给下个节点。通过这种方式，数据集可以被拆解为数据流，而一个kernel function可以操作处理其中的一个元素，而多流多处理器（Mutiple streaming Multiprocessor）可以并行操作多个元素。因此这种计算方式十分适合并行的运算场景。

## 3. CUDA的硬件和软件架构

<img width="788" alt="image" src="https://user-images.githubusercontent.com/99408013/183695244-12a62651-0c6b-479e-ae10-8a39aba3c281.png">

图为硬件架构，GPU中包括内存和多个SMP（streaming multiple processor），而一个SMP由多个可以独立工作的GPU核组成，并且这些核有共享的cache，也叫做共享内存，除此以外还有调度程序和寄存器。

软件架构对应为：
GPU被抽象为由线程块（Thread Block）组成的网格（Grid），每个Block对应硬件架构中的一个SMP，每个线程对应于一个GPU core，Blocks可以被抽象为1D，2D或3D。

## 4. CUDA的向量变量

dim2, dim3, dim4
dim3 my_xyz (x_value, y_value, z_value);

## 5. block，grid大小

Block 大小不能大于1024
Grid y和z纬度size不能大于65535，1D Grid size不能大于2147483647
Block size最好能呗32整除，这样比较有利于wrap的调度作业

## 5. kernel函数

__global__前缀需要加在gpu函数的定义中
在核函数中调用另一个核函数，则需要在该函数前加__device__前缀
在核函数前加__host__ __device__前缀后，该函数可被主机和设备共同调用
* 核函数通常返回void

## 6.gpu上的内存管理函数

cudaMalloc(&a, N * sizeof(float)) // 申请设备内存
cudafree(a) // 释放设备内存
cudaMemcpy(array distination, array origin, N * sizeof(float), cudapara) // 内存拷贝函数，四个参数分别是：目的地址，始发地址，拷贝内存大小，控制参数
* 控制参数 ∈ {cudaMemcpyHostToDevice, cudaMemcpyDeviceToHost} // 分别表示从主机拷贝到设备，和从设备拷贝到主机

## 7.静态申请内存
int a[N]; (cpu)  -->  __device__ int a[N]; (gpu)
* cudaMemCopyToSymbol(d_a, a, size);  // 将主机上a地址的size内存拷贝到device上的d_a变量中
* cudaMemcpyFromSymbol(c, d_c, size);  // 将device上的变量d_c拷贝到主机上地址c的size大小的内存中
* cudaDeviceSynchronise();  //  让主机等待知道kernel函数执行结束

## 8. 











