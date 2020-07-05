# Factorial-de-potencia
[ACDB2-15%] Foro2
package potencia;

import java.util.Scanner;

/**
 * @author User
 */
public class potencia {

    public static void main(String[] args) 

def potencia(b,n):
    """ Precondición: n debe ser mayor o igual que cero.
        Devuelve: b\^n. """

    # Caso base
    if n <= 0:
        return 1

    # n par
    if n % 2 == 0:
        pot = potencia(b, n/2)
        return pot * pot
    # n impar
    else:
        pot = potencia(b, (n-1)/2)
        return pot * pot * b

El uso de la variable pot en este caso no es optativo, ya que es una de las ventajas principales de esta implementación: se aprovecha el resultado calculado en lugar de tener que calcularlo dos veces. Vemos que este código funciona correctamente:

>>> potencia(2,10)
1024
>>> potencia(3,3)
27
>>> potencia(5,0)
1

El orden de las llamadas, haciendo un seguimiento simplificado de la función será:
potencia(2,10)

    pot = potencia(2,5)               # b → 2 n → 10
        pot = potencia(2,2)           # b → 2 n → 5
            pot = potencia(2,1)       # b → 2 n → 2
                pot = potencia(2,0)   # b → 2 n → 1
                    return 1          # b → 2 n → 0
                return 1 * 1 * 2      # b → 2 n → 1 pot → 1
            return 2 * 2              # b → 2 n → 2 pot → 2
        return 4 * 4 * 2              # b → 2 n → 5 pot → 4
    return 32 * 32                    # b → 2 n → 10 pot → 32

Para transformar este algoritmo recursivo en un algoritmo iterativo, es necesario simular la pila de llamadas a funciones mediante una pila que almacene los valores que sean necesarios. En este caso, lo que apilaremos será si el valor de n es par o no.

def potencia(b,n):
    """ Precondición: n debe ser mayor o igual que cero.
        Devuelve: b^n. """

    pila = []
    while n > 0:
        if n % 2 == 0:
            pila.append(True)
            n /= 2
        else:
            pila.append(False)
            n = (n-1)/2

    pot = 1
    while pila:
        es_par = pila.pop()
        if es_par:
            pot = pot * pot
        else:
            pot = pot * pot * b

    return pot
