# sis.mic
## Primeira Questão do Módulo 1
```assembly
E1:     MOV     @R5+,R6     ;   menor elemento 
        MOV     #1,R7       ;   FREQUENCIA
        MOV     #5,R8       ;   TAMANHO DO ARRAY
loop:   CALL    #menor_subrotina
        DEC     R8
        JNZ     loop
menor_subrotina:    CMP     @R5+,R6
                    JLO     menor_elemento
                    JZ      igual_elemento
                    JHS     loop
menor_elemento:     

```
