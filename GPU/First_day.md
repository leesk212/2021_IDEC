# GPU 강의 overview
* 코딩을 하는 이유는 gpu의 구조를 더욱 잘 이해하기 위해서!!

## CPU vs GPU
* Multi-core vs Many-core
* CPU-pipeline vs Graphics pipeline : Fetch,Decode 등등.. GPU는 병렬차원이 다름
* Memory Hierachy : 코어의 상태가 다른만큼, memory 계층구조가 다름!!

## CUDA
* Basic한 개념을 위주로 공부

## Book
* Programming Massively Parallel Processors

# Introduction to GPU Computing
* AMD가 코어를 늘리면서 intel이 따라간 형태 지금은 hyperthreading을 통해 최대 24thread까지 사용되고 있다.
* Intel -> AMD (시대의 변화)
* 1000개 이상의 코어를 many core라 칭함
* 연산 단위로 **FLOPS**를 많이 쓴다. 
  * 8.9 TFLOPS(1080X) -> 10.1 TFLOPS(2080) ....
  * GPU는 어떻게 이렇게 많은 코어들을 다룰 수 있는가?

## FLOPS
* Floating point Operations Per Second
* Integer의 연산에서 더욱 연산이 복잡해진다.
* 초당 float형을 두개 곱하는 연산을 얼마나 빨리 수행하는가를 기준으로 연산을 진행한다.

## Supercomputers in the world
* 미국의 ibm의 컴퓨터에 일본의 슈퍼컴퓨터에게 밀리게 되었다.
* 새로나온 일본의 슈퍼컴퓨터가 gpu를 사용하지 않고 cpu를 사용한다.
* 그 CPU가 ARM이기에, ARM 만으로 intel을 

## Why massively parallel processing
* 초창기의 CPU와 GPU가 많이 차이나지 않았지만 ( CPU를 기반으로 GPU를 만들었기 때문에!! )
* 그래픽처리라는 특징으로, (순차적으로 잘라서 수행하는 방법) ---> 증가적으로 GPU의 성능을 올리는 방법중 하나가 되어버림
* CPU는 전용 메모리를 달고 나온다.( DDR4, ...)
* GPU는 HVM 이라고 하는 High Bandwitdh Memory를 사용하겍 된다. 고성능 전용 메모리를 탑재를 한다.

## Original Purpose of GPU
* 물체를 조금 더 정교하게 표현하는 것이 주된 목적 ( Rendering Task ) 
* 각각의 삼각형 하나에 대해서 병렬처리를 쭉 하게 되면, 삼각형이 작아질수록 더욱 정교하게 표현을 할 수 있고, 그러면서 더 고성능이 필요한 GPU가 필요하게돼
* GPU는 computation Intensive, 병렬처리에 특화된 프로세서이다.

## GPU Use-case?
* 암호화폐 체굴
  * 전력소모가 매우 심함, 발렬도 매우 많이 나오기 때문에 쉽지 않음
  * GPU 가격 폭등의 원인
* 게임
* Supercomputers

## GPU for Parallel Computing 
* 기본적으로 18배~150배까지 성능차이가 CPU보다 좋음을 확인할 수 있음
* CPU 보다 GPU가 더욱 우얼한 성능을 갖고 있음을 모든 지표에서 확인할 수 있음

## Summary
* 원래는 그래픽 렌더링하기 위해서 ( 광원, 시점, 재질 )에 따라서 쓰였다!
* GPU의 특성상 병렬처리가 잘되다 보니까, 게이밍에 그래픽 프로세싱을 Mining하는데 매우 많이 쓰이게 되었다.
  * Mining 단순한 해쉬 함수를 풀어가지고, 코인을 무상으로 받는데, 계속해서 유지하는 거싱 BlockChain인데, 단순한 연산이기 때문에 아예 그 코인을 위한 Basic이 활용이 되고 있음!! 단순연산을 반복하는 과정이 있기 때문에 Mining에 많이 쓰이게 되었다.!!!
* 그러다 머신러닝의 과정 중에 GPU를 이용하게 되었다.
* CPU보다 100배 이상의 성능을 갖게 되었다.

# How's CPU performance imporved?
* example
> a = x * x + y * y + z * z
```
mul r0, r0, r0
mul r1, r1, r1
...
```
* single core에서 5번의 clock이 걸리게 되는데 이를 어떻게 빠르게 증가시킬 수 있을까?
## Instruction Level Parallelism
* Increasing ILP
* * 과 +를 일정부분만 증가시킴으로써 clock을 5->3으로 바꿀 수 있다.   
![그림](./IMG/1.png)

## Single-thread Performance Scaling
* 이런 ILP의 증가는 2007년 이후로 크게 퍼포먼스가 증가하지 않았다.
* 왜냐하면, Instruction수를 늘려서 연산을 빠르게 수행하는 것임으로, window를 늘려도 dependency가 걸리기 때문에, 성능 저하가 생기게 된다.
* ILP scaling limit -> Increasing frequency
* 하지만 frequency를 늘려도 결국엔 한계에 다다랐다. (이때 Intel이 약간의 이득을 봤다)
* 결국 transitor의 갯수만 늘리게 되었는데 그래도 한계가 생기게 될 것이다.
  * Moore's law가 끝이 될 것 같은가..?
  * 아직은 아니다.
* frequency가 증가되지 않을때쯤, 코어수를 늘리게 되어 transitor의 집적도 계산이 크게 늘어나게 되었다.

## Concurrency Revolution
* CPU -> multicore / GPU -> manycore 의 방향으로 이동되고 있다.
* CPU도 이제는 병렬처리에 쓸 수 있다. 
* 프로그래는 반드시 multiple core programming을 잘 알아야한다.
* Parallel Computing ( Supercomputing -> normal programmer ) 
  * ssd Conroller .. 등등
  
## The "New" Moore's law
* 더이상 컴퓨터는 빨라지는 것이 아니라, 병렬화의 시대로 넘어가게 되었다.
* 모든 알고리즘을 parallel 하게 사용해야만 한다.

## Cuda
* GPU <-> CPU 동기화 제공 및 연결 관리 가능

## Generic Many-core Chip (GPU)
![2](./IMG/2.png)  
* Global Memory -> HBM2 ,  GDDR6 
* On-chip memory -> near processors, cache,Ram
* Shared global memory space

## Design philosophy
* Latency-oriented cores -> CPU가 처리하고 싶은 것
* 몇개의 연산을 한번에 처리할 수 있는가 -> GPU가 처리하고 싶은 것
* ALU를 엄청 많이 넣고, Control과 Cache는 부분은 작아지는 형태이다.

## Lessons from Graphics Pipeline
* Throughput is the most important factor!!!
  * 병렬적으로 처리할 수 있는 큰 특징을 갖고 있기에 Scalability도 좋다.
  * 즉, 늘리기만 하면 성능도 같이 매우 늘어난다.
* FPS --> threads very rapidly 
  * 60FPS
* Multi-threading을 사용하기 위해서 !!!

## Current Parallel Processing Models
* CUDA
  * Nvidia architecture가 있어야만 GPU 코딩을 할 수 있음
  * ARM CPU -> Cuda를 내장 시키는 그런 과정이 있을 수도 있음
  * 
* OpenCL
  * 병렬적으로 데이터 처리를 할 수 있고 CPU,GPU모두 쓸 수 있음
  * 더 대중화가 될 수 있다.

# Parallel Computing History and CUDA Model

## 3D Graphics Pipeline
### Computer Graphics
* 더 큰 이미지를 만듦, 더 실제적인 이미들을 만들기 위해서 컴퓨터 그래픽 분야가 발전했기 때문이다.
* 사진으로 만들어내는 것이랑, 게임에서 처리하는 것은 조금 다른 분야다.
* 하드웨어를 더 많이 때려박는 방식으로 쓰였다. --> 결국 아깝기에, 컴퓨팅 디바이스로 쓰이게 되었다.
### Graphics Pipeline
#### Stage
* 1. Fetch
  -  특정 좌표값을 받아서 메모리를 로드 하는 단계
  - (x,y,z)로 되어있는 배열 값임
* 2. vertex Processor
  - 3차원의 공간의 어떤 위치에 존재하는지를 만들어준다.
  - (x,y,z)를 연결하면 면을 만들 수있다.
  - vertex shader: 3D에서 실제로 볼 부분말을 뽑는 것!!!
* 3. Rasterizer 
  - 이들을 모두 fragment로 만든다.
* 4. Fragment Processor
  - 이후 Fragment들을 병렬처리를 진행한다. ( 광원이나 시점에 따라서 색 값을 정해준게 된다. )
  - Fragment shader: 색, 광원 시점 을 Fragment정해준다.
* 5. Output Merging  
  - 마지막으로 Output Merging을 통해 Depth test를 진행을 한다.
  - Depth test, 특정 부분은 보이지 않는 부분일 것이다. (즉, 날릴 부분들을 날리고, 프로세싱할 부분들은 프로세싱하면 된다.)
  - 3차원이기에 그런 특징을 표현할 것이다.
* 6. Famebuffer
  - fragment들을 각각의 해상도에 맞게 표시를 진행해주는 것!!
#### 1nd gen
> vertex -> Rasterize -> Pixel -> Test & Blend -> Framebuffer
* Fixed data flow만 가능하다.
* 전혀 Flexibility가 없는 구조이었다.
#### 2nd gen
* 모드(안개, 빛세기, 재질)들을 많이 추가 해보고 싶다!
* 모든 모드를 지원하기 위해서는 하드웨어가 비대해질 것이다.
#### 3rd gen
* vertex나 pixel shading하는 부분들을 프로그래밍 가능하도록 만들어졌다.
* 직접 C로 프로그래밍 하듯이, 자유롭게 만들 수 있게 해주었다. 
#### 4th gen
* CPU처럼 instruction set을 이용할 수 있도록 만들어주었다.
* 그것이 CUDA이다.
* FULL ISA (C언어로 만듦으로써 Flexibility가 매우 증가하였다.)
* 지금도 매우 제한적인 개수를 갖고 있다.
* Optimization: 최적화가 잘되어있다 --> 그래픽 프로그래밍이 최적화가 매우 잘 되어있다라는 뜻이다.

## Why GPU scale so nicely
* Parallelism에 다양한 활용 부분들이 있기 때문이다. (Workload, Programming Model) 
* 병렬적으로 vertices들을 처리를 하고, 동일하게 실행가능하다.
* serialization bottleneck에대한 하드웨어들을 더 효율적으로 다룰 수 있다.


# Simple CUDA Program Scenario
* CPU가 먼저 main memroy에서 vram으로 데이터를 주고
* vRam에서 GPU로 연산을 한다.
* consistency나 memcpy등을 cpu가 진행한다.
* 
