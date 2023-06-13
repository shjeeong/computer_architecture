## *16. Cache 2*



# Performance

 CPU time = \#insts x CPI x T = #cycles x T

  = (\# CPU-execution cycles + \#Memory-stall cycles) x T

>  Example: A processor with
>
> - I$ miss rate = 0.02
> - D$ miss rate = 0.04
>   - \# lw or sw insts / \# insts = 0.36
> - Miss penalty = 100 cycles
> - Base CPI with an ideal cache = 1 cycle / inst
>
> \#insts = n
>
> CPU-execution cycles = n
>
> \# Memory-stall cycles = \# stall cycles in I$ + \# stall cycles in D$ = 3.44n cycles
>
> - \# stall cycles in I$: n x 0,02 x 100 cycles = 2n cycles
>
> - \# stall cycles in D$: 0.36n x 0.04 x 100cycles = 1.44n cycles
>
> \# cycles = n + 3.44n = 4.44n cycles



# Average Memory Access Time (AMAT)

평균 메모리 접근 시간

`AMAT = Hit time + Miss rate x Miss penalty`

- `Hit time`: Hit 발생시 걸리는 메모리 접근 시간 (Base)
- `Miss rate x Miss penalty`: Miss 발생시 부가적으로 걸리는 시간

따라서 캐시의 성능을 향상시키려면 `Miss rate`를 줄이거나 `Miss penalty`를 줄여야 함

- `miss rate` 줄이기: 동일한 캐시 블럭에 대한 경쟁 줄이기
- `miss penalty` 줄이기: 캐시를 계층적으로 배치.  L1 cache의 miss penalty는 L2 cache에 접근하는 시간



# Reducing Cache Miss Rates: Associative Cache

- Direct mapped cache: 메모리 한 블럭 -> 캐시의 특정 위치. 1-way set associate cache.
- Fully associative cache: 메모리 한 블럭 -> 캐시의 어디에나 저장 가능. 캐시의 크기 만큼의 선택지
  - index 없음, block addr 자체가 tag와 같음
- n-way set associative cache: 메모리 한 블럭 -> 캐시의 n개의 위치 중 하나에 저장 가능.
  - set addr: (block addr) mod (\#sets in cache) 

# Replacement Policy

set associative cache는 비어있는 공간에 먼저 채운다. 근데 해당 set addr의 방이 다 차있다면?

- **Least-recently used(LRU)**: 가장 오랫동안 사용하지 않은 것을 방출한다. 
  - 하드웨어는 한 세트 안에서 각 블럭이 몇 번 째로 들어온 것인지 기록해야한다. 2-way의 경우 set 당 1-bit만 있으면 되지만, 4-way의 경우 4!=24개의 경우를 저장하기 위해 5-bit가 필요하다.
- Random: 랜덤으로 방출한다. 성능 나름 괜찮다.



# Reducing Cache Miss Penalty

- 계층화된 캐시를 사용한다.

> - Given
>   - base CPI = 1
>   - clock frequency = 4GHz
>   - Main memory access time = 100ns
> - L1$만 있을 때
>   - L1$ access time = 0.25 ns / cycle
>   - L1 miss pealty = 100ns/ 0.25ns == 400cyles
>   - Miss rate / inst = 2%
>   - CPI: 1 + 0.02 x 400 = 9CPI
> - L2$가 추가되면
>   - Lw$ access time = 5ns
>   - global miss to main memory = 0.05%
>   - L1 miss with L2 miss: 400cycles
> - CPI: 1 + 0.02 x 20 + 0,005  x 400 = 3.4CPI









