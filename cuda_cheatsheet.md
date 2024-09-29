* `cudaMalloc()` - Allocate memory on the device
* `cudaMemcpy()` - Copy memory from host to device and vice versa
* Writing a kernel:

```cuda
__global__ void add(int *a, int *b, int *c, int n) {
    int i = threadIdx.x + blockIdx.x * blockDim.x;
    if(i < n)
        c[i] = a[i] + b[i];
}
```

* Launching a kernel:

```cuda
#define TOTAL_THREADS (2048*2048)
#define THREADS_PER_BLOCK 512
// Allocate host memory
// Allocate device memory
// Copy host memory to device memory
add<<<TOTAL_THREADS/THREADS_PER_BLOCK, THREADS_PER_BLOCK>>>(d_a, d_b, d_c);
// Copy device memory to host memory
```

* Memory types:
    * global memory
    * shared memory: on-chip memory. low latency, high bandwidth. Shared between threads in a block. Declared as `__shared__` and user managed.
* `__syncthreads()` - Synchronize all threads in a block

* 1D stencil example:

```cuda
__global__ void stencil_1d(int *in, int *out) {
    __shared__ int temp[BLOCK_SIZE + 2 * RADIUS];
    int gindex = threadIdx.x + blockIdx.x * blockDim.x;
    int lindex = threadIdx.x + RADIUS;
    
    // Read input elements into shared memory
    temp[lindex] = in[gindex];
    if(threadIdx.x < RADIUS) {
        temp[lindex - RADIUS] = in[gindex - RADIUS];
        temp[lindex + BLOCK_SIZE] = in[gindex + BLOCK_SIZE];
    }
    
    __syncthreads();

    int result = 0;
    for(int offset = -RADIUS; offset <= RADIUS; offset++)
        result += in[lindex + offset];
    
    out[gindex] = result;
}
```
