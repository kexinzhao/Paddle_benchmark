# Paddle_benchmark

## Description
We want to compare the inference benchmark of float16 vs float32 on the "image_classification" example, where we have Resnet32 and Vgg16 on cifar10 data set.

## Test environment
GPU: V100
CUDNN: 7
CUDA: 9.0
Code: https://github.com/PaddlePaddle/Paddle/pull/9488

## Total time
The average total inference time with different batch sizes on Nvidia V100 GPU.
All times are in ms (millisecond) averaged over 1000 iterations

Resnet32 on cifar10 (image.shape = 3, 32, 32)
|   |    mb=1 |    mb=2 |    mb=4 |    mb=8 |    mb=32 |   mb=64 |   mb=128 |   mb=256 |   mb=512 |
|---|--------:|--------:|--------:|---------:|---------:|---------:|---------:|---------:|---------:|
|CPU| 1.29664 | 2.30658 | 3.84233 | 10.4951  | 20.8305  |  26.2213 |  49.6337 |
|GPU| 2.66379 | 2.81712 | 2.85527 |  2.39371 |  2.39629 |   2.1023 |   2.4629 |
