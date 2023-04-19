## Lecture 5. MIPS Instructions \# 5



# MIPS Logical Instructions

- Logical instructions operate **bit-by-bit** on 2 source operands and write the result to the destination register

- **and:** 
  - 둘 다 1이면 1
  - 1 -> copy, 0 -> 0으로 채움
- **or:** 
  - 하나라도 1이면 1
  - 1 -> 1로 채움, 0 -> copy
- **xor:**
  - 다르면 1, 같으면 0
  - 1-> 반전, 0-> 그대로

- **nor:**
  - 둘 다 0이면 1 (or의 반대)
  - 0 -> 0으로 채움, 1-> 반전

# and, or, nor

- R format instruction

  `and (or, or)  rd, rs, rt`

- Examples:

  ```
  and	$t0, $t1, $t2	# $t0 = $t1 & $t2
  or	$t0, $t1, $t2	# $t0 = $t1 | $t2
  nor  $t0, $t1, $t2   # $t0 = not ($t1 | $t2)
  ```

  

# andi, ori

- I format instruction

  `andi (ori)  rt, rs, imm`

- Example:

  ```
  andi	$t0, $t1, 0xFF00	# $t0 = $t1 & 0000_0000_0000_ff00
  ori		$t0, $t1, oxFF00	# $t0 = $t1 | 0000_0000_0000_ff00
  ```

- **zero extension**: 보통은 sign extension 하지만 logical operation의 경우에만 zero extension함

  

***

# Shifting

- shift left: multiply by powers of 2
- shift right: divide by powers of 2: 소수점 이하는 flow 처리

## Logical Shift

- 부호 없는 숫자로 취급: 한 쪽은 없어지고 생겨나는 공간은 0으로 채움
- logical shift left
  - MSB: shifted out
  - LSB: shifted in with a 0
- logical shift right
  - MSB: shifted in with a 0
  - LSB: shifted out

## Arithmetic Shift

- arithemetic shift left == logical shift left
- arithmetic shift right
  - MSB: Retain its sign bit: 기존의 MSB로 채움; 부호 유지 위해
  - LSB: shifted out



# sll, srl, sra

- R format instructions

- 31bit까지 shift 가능: 5-bit shamt field 이용

  `sll (srl, sra)	 rd, rt, shamt`

  > 주의: src가 rs가 아닌 rt field 씀
  >
  > variable-shift에서 shamt자리에 rs 와서 그런듯

- Examples:

  ```
  sll	$t0, $s1, 4		# $t0 = $s1 << 4 (16 곱해짐)
  srl	$t2, $s0, 8		# $t2 = $s0 >> 8 (256 나눠짐)
  sra	$s3, $s1, 4		# $s3 = $s1 >>> 4 (4곱해짐, sign-extension)
  ```

  

# sllv, srlv, srav

- R format instructions

- variable-shift instructions

  `sllv (srlv, srav)  rd, rt, rs`

- Examples:

  ```
  sllv	$s3, $s1, $s2		# $s3 = $s1 << $s2
  srlv	$s4, $s1, $s2		# $s4 = $s1 >> $s2
  srav	$s5, $s1, $s2		# $s5 = $s1 >>> $s2
  ```

- **$rs[4:0]** 만 사용: 최대 32bit shift 가능하기 때문에



***

# How to load a 32-bit constant?

- Use 2 instructions

  - **lui** (load upper immediate)
  - **ori** (or immediate)

- Example: `0x12345678`을 `$t0`에 저장해보자

  ```'
  lui	$t0, 0x1234		# $t0: 0x1234_0000
  ori	$t0, $t0, 0x5678 # 0x1234_0000 | 0x0000_5678 = 0x1234_5678
  ```

## Pseudo Instructions

lui와 ori를 합쳐서 li라는 가짜 instruction으로 작성하면, MIPS 어셈블러가 li명령어를 lui와 ori로 분해해서 실행시킴

```
li	$t0, 0x12345678
```

> 위의 예시를 다음과 같이 pseudo instruction으로 작성할 수 있다.







