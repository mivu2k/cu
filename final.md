# lab 7
```asm
[org 0x0100]
mov ax, 15
mov bx, 5
mov cx, ax

start:
    add ax, cx
    sub bx, 1
    cmp bx , 1
    jne start

mov ax, 0x4c00
int 0x21
```
## lab p 7-1

```asm
[org 0x0100]
mov ax, 15      
mov bx, 3       
mov dx, 0      
divide:
    cmp ax, bx   
    jb done       
    sub ax, bx    
    inc dx         
    jmp divide     
done:
    mov ax, 0x4c00 
    int 0x21
```

## lab p 7-2

```asm
[org 0x0100]
mov ax, 10      
mov bx, 2       
mov si, 0x0200  
mov cx, 8      
convert:
    mov dx, 0   
subtract:
    cmp ax, bx  
    jb bitdone  
    sub ax, bx 
    inc dx      
    jmp subtract
bitdone:
    mov [si], dl ;
    inc si       
    mov ax, dx   
    loop convert 
    mov ax, 0x4C00 
    int 0x21
```

# lab 8

```asm
[org 0x0100]
mov bx,num1
mov cx,10
mov ax,0
start:
    add ax, [bx]
    add bx,2
    sub cx,1
    cmp cx,0
    jne start

mov ax, 0x4c00
int 0x21
num1: dw 1,2,3,4,5,6,7,8,9,10
```

## lab 8 p-1

```asm
[org 0x0100]
mov bx, num1    
mov ax, [bx]   
mov cx, 9      
find_max:
    add bx, 2           
    cmp [bx], ax        
    jle not_greater    
    mov ax, [bx]        
not_greater:
    dec cx           
    jne find_max       
    mov [max_num], ax 
    mov ax, 0x4c00 
    int 0x21
num1:    dw 1,2,3,4,5,6,7,8,9,10
max_num: dw 0
```

## lab 8 p-2

```asm
[org 0x0100]
mov si, arr1
mov di, arr2
mov cx , 10
mov dx , 1
c_loop:
    mov ax,[si]
    cmp ax,[di]
    jne n_equal
    add si,2
    add di,2
    loop c_loop
n_equal:
    mov dx,0
done:
    mov cx,dx
    mov ax, 0x4c00
    int 0x21
arr1: dw 1, 2, 3, 4, 5, 6, 7, 8, 9, 10  
arr2: dw 1, 2, 3, 4, 5, 6, 7, 8, 9, 10 
```

## lab 8 p-3

```asm
[org 0x0100]
mov si, arr
mov di, arr+18
mov cx,5
r_loop:
    mov ax,[si]
    mov bx,[di]
    mov [di],ax
    mov [si],bx
    add si,2
    add di,2
    loop r_loop
    mov ax, 0x4c00 
    int 0x21  

arr: dw 1, 2, 3, 4, 5, 6, 7, 8, 9, 10  
```

# lab 9

```asm
[org 0x0100]
mov bx,0
mov ax,0
li:
    add ax, [num1 + bx]
    add bx,2
    cmp bx,20
    jne li
    mov [total] , ax
    mov ax, 0x4c00
num1: dw 10,20,30,40,50,10,20,30,40,50
total: dw 0
```

## lab 9 p-1

```asm
[org 0x0100]
mov si,arr
mov ax, [si]
mov bx, [si]
mov cx,9
f_max:
    add si,2
    cmp [si],ax
    jle c_min
    mov ax, [si]
c_min:
    cmp [si],bx
    jge n_ele
n_ele:
    loop f_max
    mov [max_num], ax
    mov [min_num], bx
mov ax, 0x4c00
int 0x21
arr:    dw 5, 2, 9, 1, 7, 4, 8, 3, 6, 10
max_num:  dw 0
min_num:  dw 0
```

## lab 9 p-2

```asm
[org 0x0100]
mov cx,2
mov si, primes
m_loop:
    mov bx,2
c_div:
    mov ax,cx
    mov dx,0
    div bx
    cmp dx,0
    je n_prime
    inc bx
    cmp bx,cx
    jb c_div
    mov [si],cx
    add si,2
n_prime:
    inc cx
    cmp cx,100
    jbe m_loop
mov ax, 0x4c00    
int 0x21
primes: times 25 dw 0  
```

# lab 10

```asm
[org 0x0100]
    jmp start

data:   dw 60,55,45,50,40,35,25,30,10,0
swap:   db 0

start:
    mov byte [swap], 0     
    mov bx, 0              

loop1:
    mov ax, [data+bx]      
    cmp ax, [data+bx+2]     
    jbe noswap             

  
    mov dx, [data+bx+2]
    mov [data+bx+2], ax
    mov [data+bx], dx
    mov byte [swap], 1      

noswap:
    add bx, 2               
    cmp bx, 18              
    jne loop1             
    cmp byte [swap], 1     
    je start                

    mov ax, 0x4c00          
    int 0x21
```

## lab 10 p-1

```asm
[org 0x0100]

mov ax, 5       
mov bx, 1      

cmp ax, 0      
je done

factorial_loop:
    mul bx       
    mov bx, ax   
    dec ax      
    jnz factorial_loop 

done:
    mov ax, 0x4c00  
    int 0x21
```
## lab 10 p-2

```asm
[org 0x0100]

mov cx, 50      
mov ax, 0       
mov bx, 2    

sum_loop:
    add ax, bx  
    add bx, 2   
    loop sum_loop 

    mov bx, ax  

    mov ax, 0x4c00 
    int 0x21
```

## lab 11-1

```asm
[org 0x0100]
    jmp start

multiplicand: db 13
multiplier:   db 5
result:       dw 0   

start:
    mov cl, 8      
    mov bl, [multiplicand]
    mov dl, [multiplier]
    mov word [result], 0 

checkbit:
    shr dl, 1        
    jnc skip        

    add [result], bl 

skip:
    shl bl, 1        
    dec cl           
    jnz checkbit      

    mov ax, 0x4c00
    int 0x21
```

## lab 11-2

```asm
[org 0x0100]
    jmp start
dividend: dw 29    
divisor:  dw 5     
result:   dw 0     
remainder:dw 0     
start:
    mov ax, [dividend] 
    mov bx, [divisor]  
    mov cx, 16         
    mov dx,0         
divide:
    shl ax, 1         
    rcl dx, 1          
    cmp dx, bx         
    jb no_sub        
    sub dx, bx      
    inc ax           
no_sub:
    loop divide   
    mov [result], ax  
    mov [remainder], dx 
    mov ax, 0x4c00  
    int 0x21
```

## lab 11 p-1

```asm
[org 0x0100]

mov ax, 6      
mov bx, 0     

mov cl, al     
mov dx, 1     
shl dx, cl      
add bx, dx     

mov ax, 0x4c00  
int 0x21
```
## lab 11 p-2

```asm
[org 0x0100]

mov ax, 0xC5A3  
mov bx, 0   

count_loop:
    mov cx, 0    
    mov dx, ax  

    bit_check:
        shr dx, 1     
        jnc skip_inc  
        inc cx      
    skip_inc:
        cmp dx, 0     
        jne bit_check  

    mov ax, cx   
    inc bx     
    cmp ax, 1  
    ja count_loop 

    mov ax, 0x4c00
    int 0x21
```
# lab 12

```asm
[org 0x0100]
    mov ax, 8h       
    mov bx, 10h      
    and ax, bx       

    mov ax, 8h      
    or ax, bx      

    mov ax, 8fh     
    xor ax, bx    

    mov ax, 00ffh    
    not ax           
    
    mov ax, 0x4c00
    int 0x21
```
## lab 12 p-1

```asm
[org 0x0100]
mov ax, 6      
mov bx, 0   

mov cl, al     
mov dx, 1      
shl dx, cl   
or bx, dx       

mov ax, 0x4c00  
int 0x21
```
## lab 12 p-2

```asm
[org 0x0100]
mov ax, 6       
mov bx, 0xFFFF

mov cl, al      
mov dx, 1
shl dx, cl      
not dx       
and bx, dx     

mov ax, 0x4c00  
int 0x21
```
## lab 12 p-3

```asm
[org 0x0100]
mov ax, 6      
mov bx, 0x00FF 

mov cl, al
mov dx, 1
shl dx, cl      
xor bx, dx     

mov ax, 0x4c00
int 0x21
```
## lab 12 p-3

```asm
[org 0x0100]
mov ax, 0xC5A3  
mov cx, 0  

count_ones:
    mov dx, ax
    and dx, 1      
    jz skip_inc   
    inc cx          
skip_inc:
    shr ax, 1  
    jnz count_ones 

mov ax, cx  
mov ax, 0x4c00
int 0x21
```
## lab 13-1

```asm
[org 0x0100]
    mov ax,3
    call factorial
mov ax,0x4c00
int 0x21
factorial:
    cmp ax,1
    jbe base_case:
    push ax
    dec ax
    call factorial
    pop bx
    mul bx
ret
base_case:
    mov ax,1
ret
```
## lab 13-2

```asm
[org 0x0100]
start:
    mov ax,12
    push ax
    mov ax,0
    push ax
    call find_max
    mov ax,0x4c00
int 0x21
find_max:
    pop bx
    pop cx
    cmp cx,bx
    jge max_no
    mov ax,bx
ret
max_no:
    mov ax,cx
ret
```
## lab 13-3

```asm
[org 0x0100]
start:
    mov ax,2
    push ax
    mov ax,3
    push ax
    mov ax,4
    push ax
    call mul_three
mov ax,0x4c00
int 0x21
mul_three:
    pop cx
    pop bx
    pop dx
    mov ax,dx
    mul bx
    mul cx
ret
```
## lab 13-4

```asm
[org 0x0100]
start:
    mov ax,5
    mov bx,10
    call my_func
mov ax,0x4c00
int 0x21
my_func:
    push ax
    push bx
    mov ax,100
    mov bx,200
    pop bx
    pop ax
ret
```

## lab 13-5
```asm

[org 0x0100]
mov ax,5
push ax
mov ax,7
push ax
call addition 
mov ax,0x4c00
int 0x21
addition:
pop bx
pop cx
add cx,bx
mov ax,cx
ret

```