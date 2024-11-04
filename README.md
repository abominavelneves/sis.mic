# Módulo 1 de Sistemas Microprocessados
## Primeira Questão
```assembly
E1:     MOV     @R5+,R6     ; menor elemento
        MOV     #1,R7       ; FREQUENCIA
        MOV     #5,R8       ; TAMANHO DO ARRAY
loop_menor:
        CALL    #menor_subrotina
        DEC     R8
        JNZ     loop_menor
menor_subrotina:
        CMP     @R5,R6
        JLO     menor_elemento  ; se for menor vai para menor
        JZ      igual_elemento  ; se for igual vai para igual
        INC     R5              ; incrementa R5 manualmente
        RET                     ; se for maior volta para o loop
menor_elemento:
        MOV     @R5,R6
        MOV     #1, R7
igual_elemento:
        INC     R7
```
Ponto Interessante: seria válido por um .B pois são bytes.

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

## Segunda Questão
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
## Quarta Questão
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
