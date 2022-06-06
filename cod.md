# Practice_4

#python

import datetime
a, b, c = 0, 3, 3
start = datetime.datetime.now()
for i in range(100000000):
	a += b*2 + c - i
end = datetime.datetime.now()
print(f'a = {a}, {(end-start).microseconds * 1000} ms, {((end-start).microseconds * 1000)/100000000} speed iteration/ms')

#java

public class Main
{
	public static void main(String[] args) {
		int a=0, b=3, c=3;
		long start = System.currentTimeMillis(), end;
		for ( int i=0; i<100000001; i++ ){
            		a += b*2 + c - i;
		}
		end = System.currentTimeMillis();
		System.out.println(a + " = a, " + (end-start) + " ms, " + (end-start)/100000000 + "speed iteration/ms" );		
	}
}

#asm

extern  _printDec
extern  _println
        
        section .data
        
a       dd      0
b       dd      2
c       dd      3
iter    dd      100000000
i       dd      0

        section .text
        global  _start
_start: 

        mov     dword[i], 0

for:    mov     eax, dword[b]
        add     eax, eax
        add     eax, dword[c]
        sub     eax, dword[i]
        add     dword[a], eax

        inc     dword[i]
        mov     eax, dword[iter]
        cmp     dword[i], eax
        jl      for
endfor:
        mov     eax, dword[a]
        call    _printDec
        call    _println

;;; exit
        mov     eax, 1
        mov     ebx, 0
        int     0x80
