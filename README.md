# Módulo 1 de Sistemas Microprocessados
## Primeira Questão Baby
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
## Setima Questão
```assembly

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

