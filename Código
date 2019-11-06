section .data:

	msgInicial1: db 'Informe as cooordenadas de partida X e Y:', 10, 0
	msgInicial2: db 'Informe as coordenadas de destino X e Y:', 10,0
	msgInicial3: db 'Informe a quantidade de pontos a ser perfurada:', 10, 0
	msgloop: db 'Digite (S) para continuar OU (n) para sair:', 10, 0
	msgfim: db 'Programa encerrado.', 10, 0
	msgespaco: db ' ', 0
	out_format: db '%.2lf', 0
	inX_float:  db '%f', 0
	inY_float:  db '%f', 0
	outX_float: db '%f', 0
	outY_float: db '%f', 0
	furos_int:  db '%d', 0
	format_char:db '%c', 0
	
	sim: dd 's',10 ,0

section .bss

	x1:       resb 4
	x1Aux:    resb 8
	y1:       resb 4
	y1Aux:    resb 8
	x2:       resb 4 ;dword
	y2:       resb 4
	qFuros:   resd 1
	aux:      resb 8 
	aux2:     resb 8
	res:      resb 4
	distX:    resb 8
	distY:    resb 8
	resAux:   resb 8 ;guarda o valor de res como qword
	somaAuxX: resb 4
	somaAuxY: resb 4
	somaX:    resb 8
	somaY: 	  resb 8
	SouN:     resd 1
	enter_:   resb 1	

section .text

	global main
	extern printf 
	extern scanf
main:

loop_inicial:

	push msgInicial1
	call printf
	add esp, 4
	
	push x1
	push inX_float
	call scanf
	add esp, 8

	push y1
	push inY_float
	call scanf
	add esp, 8

	push msgInicial2
	call printf
	add esp, 4
	
	push x2
	push outX_float
	call scanf
	add esp, 8
	
	push y2
	push outY_float
	call scanf
	add esp, 8
	
	push msgInicial3
	call printf
	add esp, 4

	push qFuros
	push furos_int
	call scanf
	add esp, 8

	fld dword[x1]
	fstp qword[x1Aux]

	push dword[x1Aux+4]
	push dword[x1Aux]
	push out_format
	call printf
	add esp, 8
	
	push msgespaco
	call printf
	add esp, 4

	fld dword[y1]
	fstp qword[y1Aux]

	push dword[y1Aux+4]
	push dword[y1Aux]
	push out_format
	call printf
	add esp, 12

	push msgespaco
	call printf
	add esp, 4
       
	 ;subrai um da quantidade de furos
	mov eax, [qFuros]
	sub eax, 1
	mov [res], eax
	
	;para imprimir o resultado da subtração
;	push dword[res]
;	push furos_int
;	call printf
;	add esp, 8

	
	finit
	fild dword [res]
	fstp qword [resAux]

	finit
	;subtração de x2 - x1 	
	fld dword[x2] ;vai ser empilhado primeiro
	fld dword[x1] ;vai ficar no topo
	fsub
	fstp qword[aux]
	
	;imprimindo o result dos pontos flutuantes
;	push dword[aux+4] ;para impressão do 4 bits menos significativos
;	push dword[aux]   ;para impressão dos mais
;	push out_format
;	call printf
;	add esp, 12
	
	finit
	fld qword[aux]
	fdiv qword[resAux]
	fstp qword[distX]

;	push dword[distX+4]
;	push dword[distX]
;	push out_format
;	call printf
;	add esp, 12

	;subtração de y2 - y1 	
	fld dword[y2] ;vai ser empilhado primeiro
	fld dword[y1] ;vai ficar no topo
	fsub
	fstp qword[aux2]
	
	;imprimindo o result dos pontos flutuantes
;	push dword[aux2+4] ;para impressão do 4 bits menos significativos
;	push dword[aux2]   ;para impressão dos mais
;	push out_format
;	call printf
;	add esp, 12
	
	finit
	fld qword[aux2]
	fdiv qword[resAux]
	fstp qword[distY]

;	push dword[distY+4]
;	push dword[distY]
;	push out_format
;	call printf
;	add esp, 12

;coordenada x

	finit
	fld dword[x1]
	fadd qword[distX]
	fstp dword[somaAuxX]

	fld dword[somaAuxX]
	fstp qword[somaX]

	push dword[somaX+4]
	push dword[somaX]
	push out_format
	call printf
	add esp, 12

	push msgespaco
	call printf
	add esp, 4
	
	fld dword[somaAuxX]
	fstp dword[x1]

;coordenada y

	finit
	fld dword[y1]
	fadd qword[distY]
	fstp dword[somaAuxY]

	fld dword[somaAuxY]
	fstp qword[somaY]

	push dword[somaY+4]
	push dword[somaY]
	push out_format
	call printf
	add esp, 12

	push msgespaco
	call printf
	add esp, 4
		
	fld dword[somaAuxY]
	fstp dword[y1]
	
	mov ebx, 1
	
	loop_coordenadas:
	
;coordenada x

	finit
	fld dword[x1]
	fadd qword[distX]
	fstp dword[somaAuxX]

	fld dword[somaAuxX]
	fstp qword[somaX]

	push dword[somaX+4]
	push dword[somaX]
	push out_format
	call printf
	add esp, 12
	
	push msgespaco
	call printf
	add esp, 4

	fld dword[somaAuxX]
	fstp dword[x1]

;coordenada y

	finit
	fld dword[y1]
	fadd qword[distY]
	fstp dword[somaAuxY]

	fld dword[somaAuxY]
	fstp qword[somaY]

	push dword[somaY+4]
	push dword[somaY]
	push out_format
	call printf
	add esp, 12
	
	push msgespaco
	call printf
	add esp, 4

	fld dword[somaAuxY]
	fstp dword[y1]
	
	inc ebx
	cmp ebx, [res]
	jl loop_coordenadas
	
	push msgloop
	call printf
	add esp, 4

	push enter_
	push format_char
	call scanf
	add esp, 8

	push SouN
	push format_char
	call scanf
	add esp, 8

	mov ecx, [SouN]
	cmp ecx, [sim]
	je loop_inicial

	push msgfim
	call printf
	add esp, 4
