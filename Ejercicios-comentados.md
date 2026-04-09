


## 1. Estructuras Condicionales (if / else if / else)

### Ejercicio 1 — Positivo, negativo o cero
```c
#include <stdio.h>  // librería necesaria para printf y scanf

int main(void) {    // punto de entrada del programa, void = no recibe parámetros
    int entero;     // declaramos la variable que almacenará el número del usuario
    printf("Introduce un entero: ");  // mensaje al usuario
    scanf("%d", &entero);             // leemos un entero — & indica la dirección de memoria donde guardarlo

    if (entero > 0) {                        // si es mayor que cero
        printf("%d es un numero positivo\n", entero);
    } else if (entero == 0) {                // si no es mayor, comprobamos si es exactamente cero
        printf("Es cero\n");
    } else {                                 // si no es positivo ni cero, solo puede ser negativo
        printf("%d es un numero negativo\n", entero);
    }

    return 0;  // indica que el programa terminó correctamente
}
```

### Ejercicio 2 — Par o impar
```c
#include <stdio.h>

int main(void) {
    int num;
    printf("Introduce un numero: ");
    scanf("%d", &num);

    if (num % 2 == 0) {          // % devuelve el resto de la división
        printf("%d es par\n", num);   // si el resto es 0, es divisible entre 2 → par
    } else {
        printf("%d es impar\n", num); // cualquier otro resto → impar
    }

    return 0;
}
```

### Ejercicio 3 — Mayor de dos números
```c
#include <stdio.h>

int main(void) {
    int num1, num2;
    printf("Introduce el primer numero: ");
    scanf("%d", &num1);
    printf("Introduce el segundo numero: ");
    scanf("%d", &num2);

    if (num1 > num2) {                          // si num1 es mayor
        printf("%d es mayor que %d\n", num1, num2);
    } else if (num1 == num2) {                  // si no es mayor, comprobamos si son iguales
        printf("Los dos numeros son iguales\n");
    } else {                                    // si no es mayor ni igual, num2 es mayor
        printf("%d es mayor que %d\n", num2, num1);
    }

    return 0;
}
```

### Ejercicio 4 — Clasificación de notas
```c
#include <stdio.h>

int main(void) {
    int nota;
    printf("Introduce tu nota (0-100): ");
    scanf("%d", &nota);

    if (nota < 0 || nota > 100) {   // validamos primero — early return
        printf("Nota invalida\n");   // || significa OR — cualquiera de las dos condiciones basta
        return 1;                    // return 1 indica error y sale del programa
    } else if (nota >= 90) {        // de mayor a menor — si llegamos aquí ya sabemos que es válida
        printf("Sobresaliente\n");
    } else if (nota >= 70) {        // si no es >= 90 y es >= 70, está en el rango 70-89
        printf("Notable\n");
    } else if (nota >= 50) {        // si no es >= 70 y es >= 50, está en el rango 50-69
        printf("Aprobado\n");
    } else {                        // si no cumple ninguna condición anterior, es < 50
        printf("Suspenso\n");
    }

    return 0;
}
```

### Ejercicio 5 — Calculadora simple
```c
#include <stdio.h>

int main(void) {
    double numero1, numero2, resultado;  // double para decimales
    char operador;                       // char para almacenar el símbolo de operación

    printf("Primer numero: ");
    scanf("%lf", &numero1);              // %lf es el especificador de double en scanf
    printf("Segundo numero: ");
    scanf("%lf", &numero2);
    printf("Operacion (+ - * /): ");
    scanf(" %c", &operador);            // espacio antes de %c limpia el \n que queda en el buffer

    if (operador == '+') {              // comparamos el char con su literal entre comillas simples
        resultado = numero1 + numero2;
        printf("%.2f + %.2f = %.2f\n", numero1, numero2, resultado);  // %.2f = dos decimales
    } else if (operador == '-') {
        resultado = numero1 - numero2;
        printf("%.2f - %.2f = %.2f\n", numero1, numero2, resultado);
    } else if (operador == '*') {
        resultado = numero1 * numero2;
        printf("%.2f * %.2f = %.2f\n", numero1, numero2, resultado);
    } else if (operador == '/') {
        if (numero2 == 0) {            // antes de dividir comprobamos el divisor — si es 0, error
            printf("Error: division por cero\n");
            return 1;
        }
        resultado = numero1 / numero2;
        printf("%.2f / %.2f = %.2f\n", numero1, numero2, resultado);
    } else {
        printf("Operador no permitido: %c\n", operador);  // cualquier otro carácter es inválido
        return 1;
    }

    return 0;
}
```

### Ejercicio 6 — Año bisiesto
```c
#include <stdio.h>

int main(void) {
    int año;
    printf("Introduce el año: ");
    scanf("%d", &año);

    // condición en una sola línea — paréntesis explícitos para claridad
    // regla: divisible entre 4 Y NO entre 100, O divisible entre 400
    if ((año % 4 == 0 && año % 100 != 0) || (año % 400 == 0)) {
        printf("El año %d es bisiesto\n", año);
    } else {
        printf("El año %d no es bisiesto\n", año);
    }

    return 0;
}
```

### Ejercicio 7 — Triángulo válido y tipo
```c
#include <stdio.h>

int main(void) {
    int lado1, lado2, lado3;
    printf("Lado uno: ");
    scanf("%d", &lado1);
    printf("Lado dos: ");
    scanf("%d", &lado2);
    printf("Lado tres: ");
    scanf("%d", &lado3);

    // la suma de dos lados cualesquiera debe ser mayor que el tercero
    // si no se cumple alguna, no es triángulo válido
    if (lado1 + lado2 > lado3 && lado1 + lado3 > lado2 && lado2 + lado3 > lado1) {
        printf("Triangulo valido\n");

        if (lado1 == lado2 && lado2 == lado3) {      // los tres iguales
            printf("Equilatero\n");
        } else if (lado1 == lado2 || lado1 == lado3 || lado2 == lado3) {  // dos iguales
            printf("Isosceles\n");
        } else {                    // por descarte — si no es equilátero ni isósceles, es escaleno
            printf("Escaleno\n");
        }
    } else {
        printf("No es un triangulo valido\n");
    }

    return 0;
}
```

### Ejercicio 8 — IMC
```c
#include <stdio.h>

int main(void) {
    double peso, altura, imc;
    printf("Peso (kg): ");
    scanf("%lf", &peso);
    printf("Altura (m): ");
    scanf("%lf", &altura);

    if (peso <= 0 || altura <= 0) {  // validamos antes de calcular — evita división por cero
        printf("Error: datos invalidos\n");
        return 1;
    }

    imc = peso / (altura * altura);  // fórmula del IMC

    printf("IMC: %.2f\n", imc);

    if (imc < 18.5) {
        printf("Bajo peso\n");
    } else if (imc < 25.0) {        // límites exactos según la tabla — 18.5 a 24.9
        printf("Normal\n");
    } else if (imc < 30.0) {        // 25.0 a 29.9
        printf("Sobrepeso\n");
    } else {                         // 30.0 en adelante
        printf("Obesidad\n");
    }

    return 0;
}
```

### Ejercicio 9 — Día de la semana
```c
#include <stdio.h>

int main(void) {
    int numero;
    printf("Introduce un dia (1-7): ");
    scanf("%d", &numero);

    if (numero < 1 || numero > 7) {  // validación early return
        printf("Error: numero fuera de rango\n");
        return 1;
    }

    // detectamos fin de semana antes de los nombres — lógica separada
    if (numero > 5) {
        printf("Fin de semana: ");
    } else {
        printf("Laborable: ");
    }

    // cadena larga de else if — cada valor exacto tiene su nombre
    if (numero == 1)      printf("Lunes\n");
    else if (numero == 2) printf("Martes\n");
    else if (numero == 3) printf("Miercoles\n");
    else if (numero == 4) printf("Jueves\n");
    else if (numero == 5) printf("Viernes\n");
    else if (numero == 6) printf("Sabado\n");
    else                  printf("Domingo\n");  // por descarte — solo puede ser 7

    return 0;
}
```

### Ejercicio 10 — Autenticación simple
```c
#include <stdio.h>
#include <string.h>  // necesaria para strcmp

int main(void) {
    char user;  // array de chars para almacenar el usuario — tamaño máximo 50
    int pin;

    printf("Usuario: ");
    scanf("%49s", user);   // %49s limita a 49 caracteres + \0 — evita desbordamiento
    printf("PIN: ");
    scanf("%d", &pin);

    // combinamos ambas condiciones con && para cubrir los cuatro casos posibles
    if (strcmp(user, "admin") == 0 && pin == 1234) {  // strcmp devuelve 0 si son iguales
        printf("Acceso concedido\n");
    } else if (strcmp(user, "admin") == 0 && pin != 1234) {  // usuario ok, pin mal
        printf("PIN incorrecto\n");
    } else if (strcmp(user, "admin") != 0 && pin == 1234) {  // pin ok, usuario mal
        printf("Usuario incorrecto\n");
    } else {                                                   // ambos incorrectos
        printf("Usuario y PIN incorrectos\n");
    }

    return 0;
}
```

---

## 2. Estructura de Selección Múltiple (switch)

### Ejercicio 1 — Mes del año
```c
#include <stdio.h>

int main(void) {
    int mes;
    printf("Introduce un numero del 1 al 12: ");
    scanf("%d", &mes);

    if (mes < 1 || mes > 12) {  // validamos antes de entrar al switch — early return
        printf("Error: mes no valido\n");
        return 1;
    }

    switch (mes) {              // evaluamos mes una sola vez
        case 1:  printf("Enero\n");      break;  // break evita el fallthrough
        case 2:  printf("Febrero\n");    break;
        case 3:  printf("Marzo\n");      break;
        case 4:  printf("Abril\n");      break;
        case 5:  printf("Mayo\n");       break;
        case 6:  printf("Junio\n");      break;
        case 7:  printf("Julio\n");      break;
        case 8:  printf("Agosto\n");     break;
        case 9:  printf("Septiembre\n"); break;
        case 10: printf("Octubre\n");    break;
        case 11: printf("Noviembre\n");  break;
        case 12: printf("Diciembre\n");  break;
        default: break;  // nunca llega aquí — ya validamos arriba, pero por convención
    }

    return 0;
}
```

### Ejercicio 2 — Estación del año
```c
#include <stdio.h>

int main(void) {
    int numero;
    printf("Introduce un numero del 1 al 4: ");
    scanf("%d", &numero);

    switch (numero) {
        case 1: printf("Primavera -> flores\n");  break;
        case 2: printf("Verano -> calor\n");      break;
        case 3: printf("Otono -> lluvia\n");      break;
        case 4: printf("Invierno -> nieve\n");    break;
        default:                                   // si no es 1-4, error
            printf("Error: numero no valido\n");
            break;
    }

    return 0;
}
```

### Ejercicio 3 — Calculadora con switch
```c
#include <stdio.h>

int main(void) {
    double numero1, numero2, resultado;
    char operador;

    printf("Primer numero: ");
    scanf("%lf", &numero1);
    printf("Segundo numero: ");
    scanf("%lf", &numero2);
    printf("Operacion (+ - * /): ");
    scanf(" %c", &operator);  // espacio antes de %c limpia el buffer

    switch (operador) {       // switch sobre char — cada case es un carácter exacto
        case '+':
            resultado = numero1 + numero2;
            printf("%.2f + %.2f = %.2f\n", numero1, numero2, resultado);
            break;
        case '-':
            resultado = numero1 - numero2;
            printf("%.2f - %.2f = %.2f\n", numero1, numero2, resultado);
            break;
        case '*':
            resultado = numero1 * numero2;
            printf("%.2f * %.2f = %.2f\n", numero1, numero2, resultado);
            break;
        case '/':
            if (numero2 == 0) {      // if anidado dentro del case — validación específica
                printf("Error: division por cero\n");
                return 1;
            }
            resultado = numero1 / numero2;
            printf("%.2f / %.2f = %.2f\n", numero1, numero2, resultado);
            break;
        default:                     // cualquier otro carácter es inválido
            printf("Operador no valido\n");
            return 1;
    }

    return 0;
}
```

### Ejercicio 4 — Vocales y consonantes
```c
#include <stdio.h>

int main(void) {
    char letra;
    printf("Introduce una letra: ");
    scanf(" %c", &letra);

    switch (letra) {
        case 'a': case 'A':   // fallthrough intencional — varios case comparten el mismo bloque
        case 'e': case 'E':   // mayúscula y minúscula hacen lo mismo
        case 'i': case 'I':
        case 'o': case 'O':
        case 'u': case 'U':
            printf("'%c' es una vocal\n", letra);
            break;
        default:
            // si llegamos aquí no es vocal — comprobamos si es consonante
            if ((letra >= 'a' && letra <= 'z') || (letra >= 'A' && letra <= 'Z')) {
                printf("'%c' es una consonante\n", letra);
            } else {
                printf("'%c' no es una letra\n", letra);  // ni vocal ni consonante
            }
            break;
    }

    return 0;
}
```

---

## 3. Estructuras de Repetición (Bucles)

### Ejercicio 1 — Cuenta atrás (while)
```c
#include <stdio.h>

int main(void) {
    int numero;
    printf("Introduce un numero: ");
    scanf("%d", &numero);

    if (numero <= 0) {          // validamos — solo tiene sentido con positivos
        printf("Error: introduce un numero positivo\n");
        return 1;
    }

    while (numero != 0) {       // mientras numero no sea 0, seguimos
        printf("%d\n", numero); // imprimimos primero
        numero--;                // luego decrementamos
    }

    return 0;
}
```

### Ejercicio 4 — Tabla de multiplicar (for)
```c
#include <stdio.h>

int main(void) {
    int numero;
    printf("Introduce un numero: ");
    scanf("%d", &numero);

    for (int i = 1; i <= 10; i++) {     // sabemos exactamente cuántas veces — for
        int resultado = numero * i;      // variable declarada dentro del for
        printf("%d x %d = %d\n", numero, i, resultado);
    }

    return 0;
}
```

### Ejercicio 8 — Pirámide (for anidado)
```c
#include <stdio.h>

int main(void) {
    int n;
    printf("Introduce el numero de filas: ");
    scanf("%d", &n);

    for (int fila = 1; fila <= n; fila++) {     // bucle externo — controla las filas
        for (int col = 1; col <= fila; col++) { // bucle interno — imprime tantos * como indica fila
            printf("*");
        }
        printf("\n");                            // salto de línea al terminar cada fila
    }

    return 0;
}
```

---

## Ejercicios Extra Seleccionados

### Ejercicio E — Adivina el número (Random)
```c
#include <stdlib.h>
#include <stdio.h>
#include <time.h>

int main(void) {
    srand(time(NULL));              // semilla basada en el tiempo
    int secret = rand() % 100 + 1; // número aleatorio entre 1 y 100
    int intentos = 1;              // contador de intentos
    int num;

    printf("##### Adivina el numero #####\n\n");

    do {
        printf("Introduce un numero: ");
        scanf("%d", &num);

        if (num < secret)       printf("El numero secreto es mayor\n");
        else if (num > secret)  printf("El numero secreto es menor\n");
        else                    printf("¡Acertaste en %d intentos!\n", intentos);

        intentos++;             
    } while (num != secret);

    return 0;
}
```

### Ejercicio G — Fibonacci
```c
#include <stdio.h>

int main(void) {
    int numero;
    printf("¿Cuantos numeros quieres ver? ");
    scanf("%d", &numero);

    if (numero < 0) {
        printf("Error: introduce un numero positivo\n");
        return 1;
    }

    int a = 0, b = 1;          // los dos primeros valores de la serie
    int resultado;

    printf("%d\n%d\n", a, b);  // imprimimos los dos primeros

    for (int i = 2; i < numero; i++) {
        resultado = a + b;      // calculamos el siguiente
        a = b;                  // desplazamos
        b = resultado;          
        printf("%d\n", resultado);
    }

    return 0;
}
