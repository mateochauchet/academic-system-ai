
//PRE: n >= 0
Función fact (val n: entero): entero
   Si n > 0 entonces
       fact ← n * fact(n-1) 	// recursión
   sino
       fact ← 1 		// caso base: recordar que 0! = 1
   fSi 
fFunc


//PRE: n >= 0
Función Fibo (val n: entero): entero
	Si n >= 2 entonces
		Fibo ← Fibo(n-1) + Fibo(n-2)
	sino
		Fibo ← n
	fSi 
fFunc 

// PRE n >= 1
Funcion SumaNat (val n: entero): entero
	Si n > 1 entonces
		SumaNat ← n + SumaNat (n-1)
	sino
		SumaNat ← 1
	fSi 
fFunc 

// PRE n >= 0
Funcion Digitos (val x: entero): entero
	Si x DIV 10 > 0 entonces
		Digitos ← 1 + Digitos(x DIV 10)
	sino
		Digitos ← 1
	fSi 
fFunc 


// PRE {tope > 0}
Funcion max (ref x: arreglo[CMAX] de enteros, val tope: entero):entero
	VAR LOC: maximo: entero
	Si tope > 1 entonces
		maximo ← max(x, tope -1)
		Si x[tope] > maximo entonces
			max ← x[tope]
		sino
			max ← maximo 
		fSi 
	sino
		max ← x[1]
	fSi 
fFunc 

// PRE {tope > 0}
Funcion Suma (ref x: arreglo[CMAX] de enteros, val tope: entero): entero
	Si tope > 1 entonces
		Suma ← x[tope] + Suma (x, tope-1)
	sino
		Suma ← x[1] 
	fSi 
fFunc 

// PRE {tope >= 0}
Funcion Existe (ref x: arreglo[CMAX] de entero, val tope, val elem: entero): lógico
	Si tope > 0 entonces
		Si x[tope] = elem entonces
			existe ← verdadero
		sino
			existe ← existe (x, tope-1, elem)
		fSi 
	sino
		existe ← falso
	fSi 
fFunc 