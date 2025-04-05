# Módulo 1 de Sistemas Microprocessados
## Primeira Questão 
```assembly
	
```
## Segunda Questão 
```assembly
	
```
## Terceira Questão 
```assembly
    .cdecls "msp430.h"
    .global main

    .text

main:

    clr     R12
    mov.w   #0xFFAF, R4 
    mov.w   #0x0001, R5

    mov.w   R4, R12
    add.w   R5, R12
    jc     limitador
    jmp     fim


limitador:
    mov.w   #0xFFFF, R12
    jmp     fim


fim:
    jmp     $
    nop
	
```
## Quarta Questão 
```assembly
    .cdecls "msp430.h"
    .global main
    .text 
main:
    mov.b   #3,R4
    mov.b   #2,R5
    clr     R6
mult:
    add     R4,R6
    dec     R5
    jnz     mult
    jmp     $
    nop
	
```
## Quinta Questão 
```assembly
    .cdecls "msp430.h"
    .global main

    .text

main:

    mov.b       #5, R4
    mov.b       #-5, R5
    clr         R6
    mov.b       R4, R6
    add.b       R5, R6
    jz          zero
    jn          negative
    jmp         positive

zero:
    jmp         fim

negative:
    sub.b       #1, R6
    jmp         fim

positive:
    add.b       #1, R6
    jmp         fim

fim:
    jmp         $
    nop



	
```
## Sexta Questão 
```assembly
    .cdecls "msp430.h"
    .global main
    .text 
main:

    mov.b     #10,R12
    mov.b     #10,R13

    call      #subrot
    jmp       $
    nop

subrot:

    push      R4
    push      R5
    push      R6

    mov.b     R12, R4
    mov.b     R13, R5
    


    cmp       #0,R5
    jz        zeros
    cmp       #0,R4
    jz        zeros

loop:


    mov.b     R4,R6
   
    add.b     R6,R4
    dec       R5 
    jnz       loop

    mov.b     R4, R12
    mov.b     R5, R13

    pop       R4
    pop       R5
    pop       R6

    ret

zeros:
    clr       R12
    pop       R4
    pop       R5
    pop       R6
    ret
	
```
## Setima Questão 
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
## Décima Questão 
```assembly
    .cdecls "msp430.h"
    .global main

    .text

main:

    mov.w   #v, R12
    mov.b   #10,R13
    clr     R14

    call    #soma
    mov.w   R14, R12
    jmp     $
    nop

soma:

    add.b   0(R12),R14
    inc     R12
    dec     R13
    jnz     soma
    ret




    .data
v:  .byte   1,2,3,4,5,6,7,8,9,10
	
```
## Décima-Primeira Questão 
```assembly
                .cdecls "msp430.h"
                .global main
                .text 
main:
    mov     #v, R12     
    mov     #2, R13          
    call    #reduceSum16     

    jmp     $
    nop 

reduceSum16:
    mov     #0, R14        
    mov     #0, R15
    jmp     loop16          
loop16:
    cmp     #0, R13
    jz      fim16
    mov     @R12+, R10     
    add     R10, R14     
    addc    #0, R15         
    dec     R13           
    jnz     loop16
fim16:
    mov     R14, R12      
    mov     R15, R13        
    ret



                .data 
v:              .word 65535,5
	
```
## Décima-Segunda  Questão 
```assembly
                .cdecls "msp430.h"
                .global main
                .text 
main:

    mov     #s, R12
    mov     #v1, R13     
    mov     #v2, R14
    mov.b   #3, R15          
    call    #mapSub8   

    jmp     $
    nop 

mapSub8:
    push    R4
    push    R15
    call    #loop
    pop     R4
    pop     R15
    ret          
loop:
    clr     R4
    cmp     #0, R15
    jz      fim
    mov.b   @R13+, R4
    sub.b   0(R14), R4
    mov.b   R4,0(R12)
    inc     R14
    inc     R12
    dec     R15
    jnz     loop   


fim:
    ret
    

 
                .data
s:              .byte 0, 0, 0   ;Vetor nulo para soma 
v1:             .byte 50,100,30   ;a
v2:             .byte 10,20,20   ;b
	
```
## Décima-Terceira Questão 
```assembly
	
```
## Décima-Quarta Questão 
```assembly
	
```

