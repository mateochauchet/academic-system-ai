## **Problema 1** — Escribir una función recursiva que emita el n-ésimo término de la sucesión de Fibonacci.

  // PRE: n >= 0
  Función Fibo(val n: entero): entero                                                                                                                                          
      Si n >= 2 entonces                                                                                                                                                       
          Fibo ← Fibo(n-1) + Fibo(n-2)                                                                                                                                         
      sino                                                                                                                                                                     
          Fibo ← n
      fSi                                                                                                                                                                      
  fFunc    


## **Problema 2** — Escribir una función recursiva que emita la suma `1+2+3+...+(n-1)+n`.

func sumN2(n int) int {
	if n == 1 {
		return 1
	}
	return n + sumN2(n-1)
}

## **Problema 3** — Escribir una función recursiva para calcular el término n-ésimo de la secuencia de Lucas: `1, 3, 4, 7, 11, 18, 29, 47, ...`

func luces(n int) int {
	if n == 0 {
		return 1
	}

	if n == 1 {
		return 3
	}

	return luces(n-1) + luces(n-2)

}


## **Problema 4** — Función recursiva que devuelva la cantidad de dígitos de un número entero.

func digitos(n int) int {
	if n < 10 {
		return 1
	}
	return 1 + digitos(n / 10)
}


