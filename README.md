# Módulo 1 de Sistemas Microprocessados
## Primeira Questão Baby/Isaac
```assembly
	mov	#vetor,R5
	mov.b	@R5+,R8
	mov.b	@R5,R6
	mov.b	#1,R7					; Considera que a partir do primeiro momento, ja tera pelo menos a repeticao de qualquer byte menor, como em ABCDE, onde A aparece so 1 vez
	inc	R5
	call	#SUBROT
	jmp	$

SUBROT:
	cmp.b	@R5, R6
	jeq	IGUAL

	cmp.b	@R5,R6
	jge	MENOR

	cmp.b	@R5, R6
	jl	MAIOR

MAIOR:
	dec	R8
	cmp	#0,R8
	jz	NEXT

	inc	R5
	jmp	SUBROT
	nop

IGUAL:
	dec	R8
	cmp	#0,R8
	jz	NEXT
	inc	R7
	inc	R5
	jmp	SUBROT
	nop

MENOR:
	dec	R8
	cmp	#0,R8
	jz	NEXT

	mov.b	@R5,R6
	inc	R5
	mov.b	#1,R7

	jmp	SUBROT

NEXT:
	ret
							; pra retornar a "main"
	.data

vetor:	.byte	7, "zstabra" 				; Ta assim de proposito, assim da pra saber se vai funcionar de forma sequencial porque "s" é menor que z, mas "t" não

```

## Segunda Questão Baby
```assembly
	mov		#vetor,R5
	mov.w	@R5,R8
	add		#2,R5
	mov		@R5,R6
	add		#2,R5
	mov.b	#1,R7		;Considera que a partir do primeiro momento, ja tera pelo menos a repeticao de qualquer byte menor, como em ABCDE, onde A aparece so 1 vez
	call	#SUBROT
	jmp		$

SUBROT:
	cmp.w		@R5, R6
	jeq		IGUAL

	cmp.w		@R5, R6
	jl		MAIOR

	cmp.w		@R5,R6
	jge		FDS
MAIOR:
	dec		R8
	cmp		#0,R8
	jz		NEXT
	mov		@R5,R6
	add		#2,R5
	mov.b		#1,R7
	jmp		SUBROT
	nop

IGUAL:
	dec		R8
	cmp		#0,R8
	jz		NEXT
	inc		R7
	add		#2,R5
	jmp		SUBROT
	nop

FDS:
	dec		R8
	cmp		#0,R8
	jz		NEXT
	add		#2,R5
	jmp		SUBROT

NEXT:
	ret						;pra retornar a "main"



		.data
vetor:      .byte	6, 0,"JOJOZZMJOSE",0

```
## Terceira Questão
```assembly

```
## Quarta Questão Baby
```assembly
        mov     #vetor, R5
        mov.w	@R5+, R8
        mov.w   @R5, R6
        mov.w   @R5, R7
        sub.w	#2,R5
        call    #loop
		jmp		$

loop:
		ADD		#2, R5
		cmp		#0,R8
        jz     	NEXT


        cmp		@R5, R7
        jl    	novo_maior

        cmp		@R5, R6
        jge		novo_menor

        jmp		NEXT2

NEXT2:
		dec		R8
		jmp		loop


NEXT:
		ret


novo_maior:
        mov   @R5, R7
        dec		R8
        jmp     loop
novo_menor:
        mov   @R5, R6
        dec		R8
        jmp     loop
        nop

.data
vetor:      .word 8, 121, 234, 567, 0 , 117, 867, 45, -1
```
## Quinta Questão Baby
```assembly
mov		#0x2420, R7
	mov		#vetor1, R5
	mov		#vetor2, R6
	mov		@R5, R8
	add		#2, R5
	add		#2, R6

	call	#loop
	jmp		$


loop:

	cmp		#0, R8
	jz		NEXT

	jmp		SOMA

SOMA:
	mov		@R5, R9
	add		@R6, R9
	mov		R9, 0(R7)
	add		#2, R5
	add		#2, R6
	add		#2, R7
	dec		R8


	jmp		loop



NEXT:
	ret


			.data

vetor1:		.word	7, 65000, 50054, 26472, 53000, 60606, 814, 41121
vetor2:		.word	7, 226, 3400, 26472, 470, 1020, 44444, 12345

```
## Quinta Questão Isaac
```assembly
e1:		mov	#vetor1,R5	;alocando o vetor1 para R5
		mov	@R5+,R8		;alocando o tamanho do vetor em R8
		mov	#vetor2,R6	;alocando o vetor2 para R6
		incd	R6
		mov	#0,R7		;iniciando o resultado em 0
		call	#SUM16
		jmp		$

SUM16:		add	@R5+,R7
		add	@R6+,R7
		dec	R8
		cmp	#0,R8
		jnz	SUM16
		ret

			.data
vetor1: 	.word 7, 65000, 50054, 26472, 53000, 60606, 814, 41121
vetor2: 	.word 7, 226, 3400, 26472, 470, 1020, 44444, 12345
```
Obs: resolver o problema do Overflow. A somatória excede a quantidade que o registrador é capaz de armazenar
## Sexta Questão
```assembly

```
## Setima Questão Isaac/Baby
```assembly
    .cdecls "msp430.h"
    .global main
    .text 
main:
    clr     R4
    mov     #0x2400,R4
    mov.w   #0,0(R4)
    mov.w   #1,2(R4)
    add     #2,R4
    mov.b   #18,R13
    call    #fib
    jmp     $
    nop
fib:
    add     #2,R4
    mov.w   -4(R4),0(R4)
    add.w   -2(R4),0(R4)
    dec     R13
    jnz     fib
    ret

```
## Oitava Questão
```assembly

```
## Nona Questão
```assembly

```
## Decima Questão
```assembly

```
## Decima Primeira Questão
```assembly

```
## Questao_07pontos
```assembly

NUM .equ 	3999
	mov		#0x2400,R10
	MOV 	#NUM, R5
	MOV		#0,	R4		;MIL
	MOV		#0,	R6		;CEM
	MOV		#0,	R7		;DEZ
	MOV		#0,	R8		;UM
	CALL 	#ALG_ROM
	JMP 	$
	NOP

ALG_ROM:

	call	#MIL
	JMP		$

MIL:
	cmp		#1000, R5
	jl		CEM
	add		#1,R4
	sub		#1000, R5
	jmp		MIL



CEM:
	cmp		#100, R5
	jl		DEZ
	add		#1,R6
	sub		#100, R5
	jmp		CEM


DEZ:
	cmp		#10, R5
	jl		UM
	add		#1,R7
	sub		#10, R5
	jmp		DEZ



UM:
	cmp		#0, R5
	jz		REFAZ_MIL
	cmp		#1, R5
	add		#1,R8
	sub		#1, R5
	jz		REFAZ_MIL
	jmp		UM


REFAZ_MIL:
	cmp		#0, R4
	jz		REFAZ_CEM

	mov.b	#'M', 0(R10)
	inc		R10
	dec 	R4
	jmp		REFAZ_MIL


REFAZ_CEM:
	cmp		#0, R6
	jz		REFAZ_DEZ
	cmp		#9, R6
	jz		CM
	cmp		#8, R6
	jz		DCCC
	cmp		#7, R6
	jz		DCC
	cmp		#6, R6
	jz		DC
	cmp		#5, R6
	jz		D
	cmp		#4, R6
	jz		CD

	mov.b	#'C',0(R10)
	inc		R10
	dec		R6
	jmp		REFAZ_CEM


CM:
	mov.b	#'C', 0(R10)
	inc		R10
	mov.b	#'M', 0(R10)
	inc		R10
	jmp		REFAZ_DEZ
DCCC:
	mov.b	#'D', 0(R10)
	inc		R10
	mov.b	#'C', 0(R10)
	inc		R10
	mov.b	#'C', 0(R10)
	inc		R10
	mov.b	#'C', 0(R10)
	inc		R10
	jmp		REFAZ_DEZ
DCC:
	mov.b	#'D', 0(R10)
	inc		R10
	mov.b	#'C', 0(R10)
	inc		R10
	mov.b	#'C', 0(R10)
	inc		R10
	jmp		REFAZ_DEZ
DC:
	mov.b	#'D', 0(R10)
	inc		R10
	mov.b	#'C', 0(R10)
	inc		R10
	jmp		REFAZ_DEZ
D:
	mov.b	#'D', 0(R10)
	inc		R10
	jmp		REFAZ_DEZ
CD:
	mov.b	#'C', 0(R10)
	inc		R10
	mov.b	#'D', 0(R10)
	inc		R10
	jmp		REFAZ_DEZ

REFAZ_DEZ:
	cmp		#0, R7
	jz		REFAZ_UM
	cmp		#9, R7
	jz		XC
	cmp		#8, R6
	jz		LXXX
	cmp		#7, R6
	jz		LXX
	cmp		#6, R6
	jz		LX
	cmp		#5, R6
	jz		L
	cmp		#4, R6
	jz		XL

	mov.b	#'X',0(R10)
	inc		R10
	dec		R7
	jmp		REFAZ_CEM


XC:
	mov.b	#'X', 0(R10)
	inc		R10
	mov.b	#'C', 0(R10)
	inc		R10
	jmp		REFAZ_UM
LXXX:
	mov.b	#'L', 0(R10)
	inc		R10
	mov.b	#'X', 0(R10)
	inc		R10
	mov.b	#'X', 0(R10)
	inc		R10
	mov.b	#'X', 0(R10)
	inc		R10
	jmp		REFAZ_UM
LXX:
	mov.b	#'L', 0(R10)
	inc		R10
	mov.b	#'X', 0(R10)
	inc		R10
	mov.b	#'X', 0(R10)
	inc		R10
	jmp		REFAZ_UM
LX:
	mov.b	#'L', 0(R10)
	inc		R10
	mov.b	#'X', 0(R10)
	inc		R10
	jmp		REFAZ_UM
L:
	mov.b	#'L', 0(R10)
	inc		R10
	jmp		REFAZ_UM
XL:
	mov.b	#'X', 0(R10)
	inc		R10
	mov.b	#'L', 0(R10)
	inc		R10
	jmp		REFAZ_UM

REFAZ_UM:
	cmp		#0, R8
	jz		NEXT
	cmp		#9, R8
	jz		IX
	cmp		#8, R8
	jz		VIII
	cmp		#7, R8
	jz		VII
	cmp		#6, R8
	jz		VI
	cmp		#5, R8
	jz		VA
	cmp		#4, R8
	jz		IV

	mov.b	#'I',0(R10)
	inc		R10
	dec		R8
	jmp		REFAZ_UM


IX:
	mov.b	#'I', 0(R10)
	inc		R10
	mov.b	#'X', 0(R10)
	inc		R10
	jmp		NEXT
VIII:
	mov.b	#'V', 0(R10)
	inc		R10
	mov.b	#'I', 0(R10)
	inc		R10
	mov.b	#'I', 0(R10)
	inc		R10
	mov.b	#'I', 0(R10)
	inc		R10
	jmp		NEXT
VII:
	mov.b	#'V', 0(R10)
	inc		R10
	mov.b	#'I', 0(R10)
	inc		R10
	mov.b	#'I', 0(R10)
	inc		R10
	jmp		NEXT
VI:
	mov.b	#'V', 0(R10)
	inc		R10
	mov.b	#'I', 0(R10)
	inc		R10
	jmp		NEXT

VA:
	mov.b	#'V', 0(R10)
	inc		R10
	jmp		NEXT
IV:
	mov.b	#'I', 0(R10)
	inc		R10
	mov.b	#'V', 0(R10)
	inc		R10
	jmp		NEXT


NEXT:

	RET

		.data
RESP: 	.byte 	0


```
