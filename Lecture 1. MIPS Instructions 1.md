## Lecture 1. MIPS Instructions \# 1

# Instructions

instructions: the words of a computer's language

instruction set: the collection of instructions

Different CPUs have different instruction sets



# CISC vs RISC

## CISC: Complex Instruction Set Computer

One instruction does many (complex) jobs: 하나의 명령어가 복수개의 일 수행 (ex. 하나의 instruction으로 덧셈 가능)

Variable length instruction: 명령어의 길이가 가변적

x86 (Intel, AMD) 등이 CISC 사용

## RISC: Reduced Instruction Set Computer

Each instruction does a small (unit) job: 하나의 명령어가 하나의 일 수행 (ex. 덧셈시 여러개의 instruction 필요: 피연산자 가져오기, 더하기, 더한 값 저장하기..)

Fixed-length instruction: 고정된 길이 32-bit

MIPS, ARM 등이 RISC 사용



# MIPS (RISC) Design Principles

Simplicity favors regularity: 단순하게 만들기 위해서 규칙성을 만들자

Smaller is faster: 작을수록 빠르게 디자인 가능 (어휘체계가 단순해지기 때문에)

Make the common case fast: 자주 사용하는 경우를 빠르게 돌아가게 만들자

Good design demands good compromises: 약간의 타협은 필요하다 (instruction format 개수를 1이 아닌 3으로 타협함)



# Stored Program Concept

Instructions and data are stored in memory: 명령어와 데이터는 binary 형태로 메모리에 저장되어 있음

CPU fetches instructions and data to execute: storage(hard disc)에 저장된 프로그램이 main memory에 로딩되면 프로그램 실행 가능. CPU가 bus를 통해서 프로그램 실행 코드와 데이터를 읽어들인다.



# MIPS Instructions

stored program을 사용하는 CPU에게 필요한 instruction 종류들 (format과는 별개)

- Data processing instructions (Arithmetic and Logical): 산술/논리 연산
- Memory access instructions (Load/Store): 메모리 접근 명령어
- Branch instructions: 분기 명령어



# Arithmetic Operations

모든 산술 명령어는 세 개의 operand로 구성: 하나의 destination + 두 개의 source

Operands 는 register나 immediate filed(상수) 사용

`add a, b, c	# a gets b + c`



# Registers

CPU 내부에 위치한 빠르고 작은 저장공간 

MIPS에는 32개의 register 있음, 각각의 register 크기는 32-bit (1 word)

registers are implemented with flip-flops: 32-bit 크기의 register 하나는 32개의 flip-flop으로 구성됨



# MIPS Register File

register는 CPU안의 register file이라는 공간에 위치: 이 공간은 programmer-visible 하다. (직접 접근 가능)

- 32 32-bit registers: 32개의 reg로 구성
- Two read ports: 두 개의 src (32-bit, output)
- One write port: 한 개의 dst (32-bit, input)
- 세 개의 주소 port: src 위치 두 개, dst 위치 한 개 (5-bit, input)

Register file can be implemented with flip-flops or SRAM: 회사에서는 SRAM을 많이 사용, 우리는 flip-flop으로 만들거임



# A Memory Hierarchy

빠른 메모리일수록 용량이 작고 비쌈 (용량이 클 수록 한 번에 많은 데이터 불러옴)

Reg File < Main Memory(DRAM) < Secondary Storage(Disk)

Register file access is much faster than main memory or cache because there is a very limited number of registers and they reside inside CPU: reg file은 아주 적은 수의 reg가 CPU안에 존재하니까 엄청 빠를 수밖에



# MIPS Assembler Register Names

| Register Number | Register Name | Usage                                           |
| :-------------- | ------------- | ----------------------------------------------- |
| 0               | $zero         | hardwired 0: readonly(쓰기 불가능): 자주 씀 333 |
| 1               | $at           | reserved by the assembler                       |
| 2 - 3           | $vo - $v1     | return value and expression evaluation          |
| 4 - 7           | $a0 - $a3     | arguments                                       |
| 8 - 15          | $t0 - $t7     | temporary values: 자주 씀 111                   |
| 16 - 23         | $s0 - $s7     | saved values: 자주 씀 222                       |
| 24 - 25         | $t8 - $t9     | more temporary values                           |
| 28              | $ gp          | global pointer                                  |
| 29              | $sp           | stack pointer                                   |
| 30              | $fp           | frame pointer                                   |
| 31              | $ra           | return address                                  |



