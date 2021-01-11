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

# Summary
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
