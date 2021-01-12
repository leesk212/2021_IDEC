## Matrix Multiplication
* triple for - loop을 써야만 한다.
* A와 B행렬이 있고 multiply를 하게되면
  * C31 = A30~A34 * B01~B41의 연산이다.
* Cuda의 연산에서는 각각의 Cx,y마다 thread(x,y)가 연산을 하도록 진행해준다.

## Cuda Matrix Multiplication: Memory usage
* A[i*WIDTH + K] / B[k* WIDTH + j]
* 계산하는 부분이 thread가 될 것이다.
* for문을 제거해주고, thread에 올려준다. 
* block dimension을 없애고 진행한다.
* 2D kernel에 대한 기존 CPU에 대한 차이점 kernel has a for loop

## CUDA thread again

# CUDA H/W Architecture
* GeForce 8800 이상부터 graphic뿐만 아니라 computing을 위한 개발을 위해서 만들었다.
* 각 thread는 data cache를 공유한다.
* global memory는 DRAM이다.
* 가장 큰 단위는 TPC를 묶어논 SPA(Streaming Processor Array)
* SPA->TPC(TEX,SM)->(SP[streaming Processor])
  * SPA 1~8개의 TPC로 이루어져있고
  * TPC는  2SM과 TEX로 이뤄져있다.
  * 
  * SP => CUDA Core
  * SFU는 sin, cos square등등의 특별한 연산을 위해서 구성된 unit이다.
* SM이 연산하는 기본 단위가 되었다.
  * Scalability가 고정이 되기 때문에
  * GPU가 나올때마다 그 단위가 달라지게 되면, cuda 프로그램 코드가 작아지면 제대로 돌아가지 않는 그런 문제가 발생할 수 있게 된다.
  * 굉장히 low-end-device에서도 SM을 하나만 넣고!! 여러가지를 Scalable한 platform을 만들게 되었다.
  
