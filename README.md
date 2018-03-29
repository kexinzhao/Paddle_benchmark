# Paddle_benchmark

## Description
We want to compare the inference benchmark of float16 vs float32 on the "image_classification" example on V100 GPU, where we can enable the tensor core computation for float16 mode, where we have Resnet32 and Vgg16 on cifar10 data set.

For more details about tensor core, please refer to https://devblogs.nvidia.com/programming-tensor-cores-cuda-9/

## Test environment
GPU: V100
CUDNN: 7
CUDA: 9.0
Code: https://github.com/PaddlePaddle/Paddle/pull/9488 (Tensor core is enabled for float16 mode)


## Total time
The average total inference time with different batch sizes on Nvidia V100 GPU.
All times are in ms (millisecond) averaged over 1000 iterations

Vgg16 on cifar10 (image.shape = [3, 32, 32]):

|       | mb=1 | mb=2 | mb=4 | mb=8 | mb=32 | mb=64 | mb=128 | mb=256 | mb=512 |
|-------|-----:|-----:|-----:|-----:|------:|------:|-------:|-------:|-------:| 
|float32| 3.94 | 4.10 | 4.08 | 4.48 | 6.90  | 9.03  | 14.04  | 24.63  | 45.36  | 
|float16| 3.78 | 3.68 | 3.76 | 3.79 | 4.14  | 4.64  | 6.45   | 10.29  | 17.90  |
|Speedup| 1.04 | 1.12 | 1.09 | 1.18 | 1.67  | 1.95  | 2.18   | 2.39   | 2.53   |


Resnet32 on cifar10 (image.shape = [3, 32, 32]):

|       | mb=1 | mb=2 | mb=4 | mb=8 | mb=32 | mb=64 | mb=128 | mb=256 | mb=512 |
|-------|-----:|-----:|-----:|-----:|------:|------:|-------:|-------:|-------:| 
|float32| 5.30 | 4.87 | 4.77 | 4.98 | 5.26  | 5.80  | 8.10   | 12.91  | 22.2   |
|float16| 5.77 | 5.77 | 5.29 | 5.80 | 5.74  | 5.03  | 5.23   | 7.37   | 11.53  | 
|Speedup|      |      |      |      |       | 1.15  | 1.55   | 1.75   | 1.93   |
