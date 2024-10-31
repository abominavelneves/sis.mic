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
## Segunda Questão
```assembly

```
## Terceira Questão
```assembly

```
## Quarta Questão
```assembly
        mov     #vetor, R5
        mov.w	@R5, R8
        mov.w   @R5+, R6
        mov.w   @R5, R7
        dec	R5
        call    #loop

loop:
        ADD	#2, R5
        cmp	@R5, R7
        jl    	novo_menor

        cmp	@R5, R6
        jge	novo_maior

        dec	R8
	cmp	#0,R8
        jnz     loop
        jmp	$

novo_menor:
        mov   @R5, R7
        dec	R8
        jmp     loop
novo_maior:
        mov   @R5, R6
        dec	R8
        jmp     loop
        nop

.data
vetor:      .word 8, 121, 234, 567, -1990 , 117, 867, 45, -1980
```
