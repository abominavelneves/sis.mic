# sis.mic
## Primeira Questão do Módulo 1
```assembly
E1:     MOV     @R5+,R6     ;   menor elemento 
        MOV     #1,R7       ;   FREQUENCIA
        MOV     #5,R8       ;   TAMANHO DO ARRAY
loop_menor:   CALL    #menor_subrotina
        DEC     R8
        JNZ     loop
menor_subrotina:    CMP     @R5+,R6
                    JLO     menor_elemento      ; se for menor vai para menor 
                    JZ      igual_elemento      ; se for igual vai para maior
                    RET                         ; se for maior volta para o loop
menor_elemento:     MOV @R5,R6
                    MOV #1, R7
                    RET
igual_elemento:     INC R7
                    RET    

```