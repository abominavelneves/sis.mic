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

    mov.w   #0x0001, R12
    mov.w   #0x1208, R13
    

    call    #rot16
    jmp     $
    nop

rot16:

    push    R5
    push    R4
    push    R6
    push    R8
    mov     #12, R8
    mov     #0x2400, R4
    mov     R13, 0(R4)
    mov.b   0(R4), R5

    mov.w   R13, R6      
    and.w   #0xF000, R6
    
shift_loop:
    rra.w   R6
    dec     R8
    jnz     shift_loop


    bit.b   #0xF, 1(R4)
    jz     rot_zeros    
    bit.b   #0xE, 1(R4)
    jz      rot_ones
    bit.b   #0xD, 1(R4)
    jz      rot_arith
    bit.b   #0xB, 1(R4)
    jz      rot_circle
    

rot_zeros:
    cmp     #1, R6
    jz      rot_zeros_dir
    rla     R12
    dec     R5
    jnz     rot_zeros
    jmp     fim
rot_zeros_dir:
    clrc
    rrc     R12
    dec     R5
    jnz     rot_zeros_dir
    jmp     fim

rot_ones:
    cmp     #1, R6
    jnz      rot_ones_dir
    setc    
    rrc     R12
    dec     R5
    jnz     rot_ones
    jmp     fim
rot_ones_dir:
    setc    
    rlc     R12
    dec     R5
    jnz     rot_ones_dir
    jmp     fim

rot_arith:
    cmp     #1, R6
    jnz      rot_arith_dir
    rla     R12
    dec     R5
    jnz     rot_arith
    jmp     fim
rot_arith_dir:
    rra     R12
    dec     R5
    jnz     rot_arith_dir
    jmp     fim

rot_circle:
    cmp     #1, R6
    jnz      rot_circle_dir
    clrc
    rlc     R12
    rlc     R12
    dec     R5
    jnz     rot_circle
    jmp     fim
rot_circle_dir:
    clrc
    rrc     R12
    rrc     R12
    dec     R5
    jnz     rot_circle_dir
    jmp     fim

fim:
    pop     R5
    pop     R4
    pop     R6
    pop     R8
    ret




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
## Décima-Nona  Questão 
```assembly

    .cdecls "msp430.h"
    .global main

    .text

main:

    mov     #v1, R13
    mov.w   #0x89AB, R12
    
    call    #W16_ASC
    jmp     $
    nop


W16_ASC:
    push    R5
    push    R4
    push    R6
    push    R7
    mov.w   R12, R4      
    and.w   #0xF000, R4
    mov.w   R12, R5      
    and.w   #0x0F00, R5
    mov.w   R12, R6      
    and.w   #0x00F0, R6
    mov.w   R12, R7      
    and.w   #0x000F, R7

    call        #shift_loop_12
    call        #shift_loop_8
    call        #shift_loop_4
    call        #shift_loop_0

    pop     R4
    pop     R5
    pop     R6
    pop     R7
    ret

shift_loop_12:
    mov.b   #12, R8
mini_loop_1:
    clrc
    rrc.w   R4
    dec     R8
    jnz     mini_loop_1

    cmp.b   #0x0A, R4
    jhs     maior_que_10_12
    jmp     menor_que_10_12

shift_loop_8:
    mov.b   #8, R8
mini_loop_2:
    clrc
    rrc.w   R5
    dec     R8
    jnz     mini_loop_2

    cmp.b   #0x0A, R5
    jhs     maior_que_10_8
    jmp     menor_que_10_8

shift_loop_4:
    mov.b   #4, R8
mini_loop_3:
    clrc
    rrc.w   R6
    dec     R8
    jnz     mini_loop_3

    cmp.b   #0x0A, R6 
    jhs     maior_que_10_4
    jmp     menor_que_10_4

shift_loop_0:
    cmp.b   #0x0A, R7
    jhs     maior_que_10_0
    jmp     menor_que_10_0

maior_que_10_12:
    sub.b   #0x09, R4
    add.b   #0x40, R4
    mov.b   R4, 0(R13)
    ret
menor_que_10_12:
    add.b   #0x30, R4
    mov.b   R4, 0(R13)
    ret

maior_que_10_8:
    sub.b   #0x09, R5
    add.b   #0x40, R5
    mov.b   R5, 1(R13)
    ret
menor_que_10_8:
    add.b   #0x30, R5
    mov.b   R5, 1(R13)
    ret

maior_que_10_4:
    sub.b   #0x09, R6
    add.b   #0x40, R6
    mov.b   R6, 2(R13)
    ret
menor_que_10_4:
    add.b   #0x30, R6
    mov.b   R6, 2(R13)
    ret

maior_que_10_0:
    sub.b   #0x09, R7
    add.b   #0x40, R7
    mov.b   R7, 3(R13)
    ret

menor_que_10_0:
    add.b   #0x30, R7
    mov.b   R7, 3(R13)
    ret


    .data

v1: .byte  0, 0, 0, 0
```
## Vigesima  Questão 
```assembly

    .cdecls "msp430.h"
    .global main

    .text

main:

    mov     #v1, R12
    call    #ASC_W16
    jmp     $
    nop

ASC_W16:
    push    R4
    push    R5
    push    R6
    push    R7
    push    R8

    call    #seg1
    call    #seg2
    call    #seg3
    call    #seg4

    mov.w   R4, R12
    add.w   R5, R12
    add.w   R6, R12
    add.w   R7, R12
    ret

seg1:

    mov.b   0(R12), R4
    cmp.b   #0x40, R4
    jhs     letra_1
    jmp     numero_1

seg2:

    mov.b   1(R12), R5
    cmp.b   #0x40, R5
    jhs     letra_2
    jmp     numero_2

seg3:

    mov.b   2(R12), R6
    cmp.b   #0x40, R6
    jhs     letra_3
    jmp     numero_3

seg4:

    mov.b   3(R12), R7
    cmp.b   #0x40, R7
    jhs     letra_4
    jmp     numero_4

letra_1:

    add.b   #0x09, R4
    sub.b   #0x40, R4
shift_loop_1:
    mov.b   #12, R8
mini_loop_1:
    rla.w   R4
    dec     R8
    jnz     mini_loop_1
    ret

letra_2:

    add.b   #0x09, R5
    sub.b   #0x40, R5
shift_loop_2:
    mov.b   #8, R8
mini_loop_2:
    rla.w   R5
    dec     R8
    jnz     mini_loop_2
    ret

letra_3:

    add.b   #0x09, R6
    sub.b   #0x40, R6
shift_loop_3:
    mov.b   #4, R8
mini_loop_3:
    rla.w   R6
    dec     R8
    jnz     mini_loop_3
    ret

letra_4:
    add.b   #0x09, R7
    sub.b   #0x40, R7
    ret

numero_1:
    sub.b   #0x30, R4
    jmp     shift_loop_1
numero_2:
    sub.b   #0x30, R5
    jmp     shift_loop_2
numero_3:
    sub.b   #0x30, R6
    jmp     shift_loop_3
numero_4:
    sub.b   #0x30, R7
    ret










    .data

v1: .byte  '8', '9', 'A', 'B'
```
