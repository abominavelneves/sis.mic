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

    .cdecls "msp430.h"
    .global main
    .text 
main:
    clr     R12
    mov.w   #0,R12
    mov.w   #1,R13   
    call    #fib

    jmp     $
    nop

fib:

    push    R4
    push    R5
    push    R6
    push    R7

    mov.w   R12, R4
    mov.w   R13, R5
    clr     R6
    call    #loop

    mov.w   R7, R12

    pop     R4
    pop     R5
    pop     R6
    pop     R7
    ret

loop: 
    
    mov.w   R4, R6
    mov.w   R5, R7
    add.w   R5, R6
    mov.w   R6, R5
    mov.w   R7, R4
    jnc     loop
    ret

    

	
```
## Nona Questão 
```assembly
    .cdecls "msp430.h"
    .global main
    .text 
main:
    clr     R12
    mov.w   #0,R12 
    mov.w   #1,R13
    mov.w   #0, R14
    mov.w   #0, R15   
    call    #fib

    jmp     $
    nop

fib:

    push    R4  ;metade alta anterior (R12)
    push    R5  ;metade alta atual (R13)
    push    R6  ;metade baixa anterior (R14)
    push    R7  ;metade baixa atual (R15)

    push    R8  ;DE REFERENCIA alta
    push    R10 ;DE REFERENCIA baixa



    mov.w   R12,R4
    mov.w   R13,R5
    mov.w   R14,R6
    mov.w   R15,R7

    call    #loop

    mov.w   R5, R12
    mov.w   R6, R13

    pop     R4
    pop     R5
    pop     R6
    pop     R7
    pop     R8
    pop     R10
    ret

loop:

    ;baixa 
    mov.w   R4, R8
    mov.w   R5, R4
    add.w   R5, R8
    mov.w   R8, R5

    addc.w  #0,R7
    mov.w   R6,R10
    mov.w   R7, R6
    add.w   R7, R10
    mov.w   R10, R7
    jnc     loop
    jc      carry

carry:
    ret    
	
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

    mov.w   #v, R12
    mov.b   #10,R13

    call    #soma
    jmp     $
    nop

soma:
    push    R4 
    push    R5

    push    R6
    push    R7

    mov.w   R12, R4
    mov.b   R13, R5

    clr     R6
    clr     R7


loop:
    add.w   0(R4),R6
    addc.w  #0, R7   

    add     #2,R4
    dec     R5
    jnz     loop



    mov.w   R6, R12
    mov.w   R7, R13

    pop     R4
    pop     R5
    pop     R6
    pop     R7

    ret


    .data
v:  .word   65535,65535,1, 65535, 65535, 40000, 20000, 1, 2, 3
	
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

                .cdecls "msp430.h"
                .global main
                .text 
main:

    mov     #v1, R5
    mov     #v2, R6   
    mov     #s, R7
    mov     #8, R8

    call    #mapSum16

    jmp     $
    nop

mapSum16:

    mov.w   0(R5), 0(R7)
    add.w   0(R6), 0(R7)

    add     #2, R5
    add     #2, R6
    add     #2, R7

    dec     R8
    jnz     mapSum16
    ret



    

 
                .data

v1:             .word 7, 65000, 50054, 26472, 53000, 60606, 814, 41121   ;a
v2:             .word 7, 226, 3400, 26472, 470, 1020, 44444, 12345      ;b
s:              .word 7, 0, 0, 0, 0, 0, 0, 0 
	
```
## Décima-Quarta Questão 
```assembly
    .cdecls "msp430.h"
    .global main

    .text

main:

    mov     #v1, R12
    mov     #6, R13

    call    #m2m4

    jmp     $
    nop

m2m4:

    push    R4
    push    R5
    push    R6
    push    R7

    clr     R6
    clr     R7

    mov     R12, R4
    mov     R13, R5

    call     #loop_m2

    mov     R6, R12
    mov     R7, R13

    push    R4
    push    R5
    push    R6
    push    R7

    ret



loop_m2:

    bit.b     #0x01, 0(R4)
    jz      loop_m4
    inc     R4     
    dec     R5
    jnz     loop_m2
    jmp     fim

loop_m4:

    inc     R6
    bit.b     #0x03, 0(R4)
    jz      eosdois
    inc     R4
    dec     R5
    jnz     loop_m2
    jmp     fim

eosdois:
    inc     R7
    inc     R4
    dec     R5
    jnz     loop_m2

fim:
    ret



    .data

v1: .byte   10, 7, 4, 5, 12, 9
	
```

## Décima-Sexta  Questão 
```assembly

    .cdecls "msp430.h"
    .global main

    .text

main:

    mov     #v1, R12
    mov     #10, R13

    call    #menor

    jmp     $
    nop

menor:
    push    R4
    push    R5  
    push    R6 
    push    R7

    mov     R12, R4
    mov     R13, R5
    mov.b   0(R12), R6
    clr     R7

    cmp     #0, R5
    jz      fim1

    cmp     #1, R5
    jz      fim2

    jmp     loop

loop:


    cmp.b   0(R4), R6
    jz      continua_menor
    jge     novo_menor



    inc     R4
    dec     R5
    jnz     loop
    jmp     fim0

novo_menor:
    mov     #1, R7
    mov.b   0(R4), R6
    inc     R4

    dec     R5
    jnz     loop
    jmp     fim0  

continua_menor:
    inc     R7
    inc     R4
    dec     R5
    jnz     loop
    jmp     fim0


fim0:

    mov     R6, R12
    mov     R7, R13
    pop    R4
    pop    R5  
    pop    R6 
    pop    R7
    ret

fim1:
    mov     #0, R12
    mov     #0, R13
    pop    R4
    pop    R5  
    pop    R6 
    pop    R7
    ret

fim2:
    mov     0(R4), R12
    mov     #1, R13
    pop    R4
    pop    R5  
    pop    R6 
    pop    R7
    ret



  



    .data

v1: .byte   10, 7, 4, 5, 4, 9, 10, 2, 9, 10
```
