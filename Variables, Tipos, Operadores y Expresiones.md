# Recopilatorio de Ejercicios — C
**Bloques 2 y 3 — Variables, Tipos, Operadores y Expresiones**

Compilar siempre con:
```bash
gcc -Wall -Wextra -std=c11 -g archivo.c -o programa
```

---

## Índice

| # | Título | Tema |
|---|--------|------|
| 1 | Datos del alumno | Variables / tipos / ternario |
| 2 | Calculadora de descuento | Aritmética / variables intermedias |
| 3 | División entera vs real | Tipos / cast / trampa |
| 4 | Conversión de temperatura | Aritmética / literales float |
| 5 | Precedencia de operadores | Precedencia |
| 6 | Segundos a horas:min:seg | Módulo y división entera |
| 7 | Precio con impuestos | Aritmética / formato |
| 8 | Operadores lógicos | && \|\| ! |
| 9 | Precedencia avanzada | Precedencia / trampa |
| 10 | Intercambio XOR | XOR / bits |
| 11 | XOR — predice la salida | XOR |
| 12 | Clasificador de notas | Ternario encadenado |
| 13 | Calculadora IMC | Ternario / aritmética |
| 14 | Año bisiesto | && \|\| % |
| 15 | Operaciones con bits | Bitwise completo |
| 16 | Precio con IVA 10% | Aritmética / formato |
| 17 | Comprobación de rango | Lógicos / relacional |
| 18 | Conversor de unidades | Aritmética / const |
| 19 | Predice la salida XOR avanzado | XOR |
| 20 | Calculadora completa | Integrador |
| ++ | Serie pre/post incremento | Operadores ++ y -- |
| <<>> | Serie desplazamiento de bits | Bitwise shift |

---

## Ejercicio 1 — Datos del alumno
**Tema:** Variables / tipos / ternario

### Enunciado
Declarar variables para un alumno (nombre, edad, nota media) y mostrarlas con formato adecuado.

### Solución final
```c
#include <stdio.h>

int main(void) {
    char  nombre[50];
    int   edad;
    float media;

    printf("Introduce los siguientes datos:");
    printf("\n[+] Nombre: ");
    scanf("%49s", nombre);
    printf("[+] Edad: ");
    scanf("%d", &edad);
    printf("[+] Nota media: ");
    scanf("%f", &media);

    printf("\nNombre:                 %s\n",  nombre);
    printf("Edad:                   %d\n",    edad);
    printf("Nota media:             %.2f\n",  media);
    printf("Calificacion academica: %s\n",
           media >= 5.0f ? "Aprobado" : "Suspenso");
    return 0;
}
```

### Feedback

| Aspecto | Estado | Nota |
|---------|--------|------|
| `char nombre[49]` con `%49s` | ❌ | Desbordamiento — el array debe ser `[50]` |
| Variable declarada sin usar | ⚠️ | Borrar variables que no se usan (`-Wall` avisa) |
| `int main()` sin `void` | ⚠️ | En C usar siempre `int main(void)` |
| Ternario directo en `printf` | ✅ | `media >= 5.0f ? "Aprobado" : "Suspenso"` |

> 💡 `scanf("%49s")` lee máximo 49 chars. El array necesita 50 bytes (49 chars + `'\0'`).

---

## Ejercicio 2 — Calculadora de descuento
**Tema:** Aritmética / variables intermedias

### Enunciado
Dado precio original y porcentaje de descuento, calcular: descuento, precio final, IVA 21% y total.

### Solución final
```c
#include <stdio.h>

int main(void) {
    float precio_original  = 200.0f;
    float descuento_pct    = 0.15f;
    float iva              = 0.21f;
    float precio_descuento = precio_original * descuento_pct;
    float precio_final     = precio_original - precio_descuento;
    float iva_producto     = precio_final * iva;
    float precio_total     = precio_final + iva_producto;

    printf("Precio original:       %.2f\n", precio_original);
    printf("Descuento (15%%):       %.2f\n", precio_descuento);
    printf("Precio tras descuento: %.2f\n", precio_final);
    printf("IVA (21%%):             %.2f\n", iva_producto);
    printf("Precio total:          %.2f\n", precio_total);
    return 0;
}
```

### Feedback

| Aspecto | Estado | Nota |
|---------|--------|------|
| Recalcular expresión en cada `printf` | ❌ | Guardar en variables intermedias y reutilizar |
| Declarar `descuento_pct` y no usarla | ❌ | Usar siempre las variables declaradas |
| Etiqueta no coincide con variable | ❌ | La etiqueta debe coincidir con la variable que imprime |
| `%` sin escapar en `printf` | ❌ | Usar `%%` para imprimir el símbolo `%` |
| Separación cálculo / presentación | ✅ | Bien estructurado en versión final |

---

## Ejercicio 3 — División entera vs real
**Tema:** Tipos / cast / trampa del paréntesis

### Código y resultados
```c
int   a = 9, b = 4;
float c = 9.0f;

printf("%d\n",   a / b);           // 2    división entera — trunca
printf("%.2f\n", c / b);           // 2.25 float/int → float
printf("%.2f\n", (float)a / b);    // 2.25 cast ANTES de dividir
printf("%d\n",   a % b);           // 1    resto de la división
printf("%.2f\n", (float)(a / b));  // 2.00 TRAMPA: divide primero, cast tarde
```

### Concepto clave — cuándo actúa el cast
```c
(float)a / b      // cast ANTES → 9.0f / 4 = 2.25   ✅
(float)(a / b)    // divide primero → (float)2 = 2.00 ❌ ya tarde
```

> 💡 El cast solo convierte lo que tiene inmediatamente al lado. El paréntesis decide qué ocurre primero.

---

## Ejercicio 4 — Conversión de temperatura
**Tema:** Aritmética / literales float

### Solución final
```c
#include <stdio.h>

int main(void) {
    float c, f, k;

    printf("Introduce la temperatura en Celsius: ");
    scanf("%f", &c);

    f = (c * 9.0f / 5.0f) + 32.0f;
    k = c + 273.15f;

    printf("%.2f grados son %.2f Fahrenheit y %.2f Kelvin\n", c, f, k);
    return 0;
}
```

### Feedback

| Aspecto | Estado | Nota |
|---------|--------|------|
| Fórmulas correctas | ✅ | `F=(C*9/5)+32`  `K=C+273.15` |
| `9.0 / 5.0` sin `f` — literales double | ⚠️ | Con variables `float` usar `9.0f / 5.0f` |
| Declarar variables al inicio | ✅ | Corregido en segunda entrega |
| Argumento extra en `printf` sin formato | ❌ | `printf("texto", c)` — `c` sin especificador `%` |

---

## Ejercicio 5 — Precedencia de operadores
**Tema:** Precedencia / izquierda a derecha

### Resultados — a=5, b=3, c=2
```c
a + b * c           // 11  (* antes que +)
(a + b) * c         // 16  (paréntesis primero)
a * b - c * b       //  9  (ambos * se resuelven antes que -)
a % b * c           //  4  (% y * iguales → izq a der: 5%3=2, 2*2=4)
a / b * b + a % b   //  5  (identidad: a = (a/b)*b + a%b)
```

### Tabla de precedencia (mayor → menor)
```
( )              Paréntesis
!  ~             Negación lógica / NOT bit a bit
*  /  %          Multiplicación, división, módulo
+  -             Suma, resta
<  <=  >  >=     Relacionales
==  !=           Igualdad / desigualdad
&                AND bit a bit
^                XOR bit a bit
|                OR bit a bit
&&               AND lógico
||               OR lógico
?:               Ternario
=  +=  -=  ...   Asignación
```

---

## Ejercicio 6 — Segundos a horas:min:seg
**Tema:** Módulo / división entera

### Solución final
```c
#include <stdio.h>

int main(void) {
    int segundos_totales, horas, minutos, segundos;

    printf("Introduce los segundos: ");
    scanf("%d", &segundos_totales);

    horas    = segundos_totales / 3600;
    minutos  = (segundos_totales % 3600) / 60;
    segundos = segundos_totales % 60;

    printf("%d segundos → %d:%02d:%02d\n",
           segundos_totales, horas, minutos, segundos);
    return 0;
}
```

### Lógica — ejemplo con 3750 segundos
```
horas    = 3750 / 3600 = 1
restante = 3750 % 3600 = 150
minutos  = 150  / 60   = 2
segundos = 150  % 60   = 30
resultado: 1:02:30
```

> 💡 `%02d` imprime mínimo 2 dígitos rellenando con cero — por eso `2` sale como `02`.

---

## Ejercicio 7 — Precio con impuestos
**Tema:** Aritmética / scanf / formato

### Solución final
```c
#include <stdio.h>

int main(void) {
    float precio, iva, precio_final, total_neto;
    int   cantidad;

    printf("Precio del articulo: ");
    scanf("%f", &precio);
    printf("Cantidad: ");
    scanf("%d", &cantidad);

    total_neto   = precio * cantidad;
    iva          = total_neto * 0.10f;
    precio_final = total_neto + iva;

    printf("\nSubtotal:      %.2f\n", total_neto);
    printf("IVA (10%%):     %.2f\n",  iva);
    printf("Total a pagar: %.2f\n",  precio_final);
    return 0;
}
```

### Feedback

| Aspecto | Estado | Nota |
|---------|--------|------|
| Variables intermedias bien nombradas | ✅ | `total_neto`, `iva`, `precio_final` |
| `\n` en `scanf` — bloquea el programa | ❌ | `scanf("%f\n ")` causa espera infinita |
| `%%` para imprimir `%` | ✅ | Correcto desde el primer intento |
| Separación cálculo / presentación | ✅ | Bien estructurado |

---

## Ejercicio 8 — Operadores lógicos
**Tema:** `&&` `||` `!`

### Solución final
```c
#include <stdio.h>

int main(void) {
    int   edad             = 25;
    float salario          = 1800.0f;
    int   tiene_contrato   = 1;
    int   en_periodo_prueba = 0;

    printf("Beneficios:    %d\n", edad >= 23 && salario > 1500.0f);
    printf("Bonus:         %d\n", tiene_contrato || salario > 2000.0f);
    printf("Consolidado:   %d\n", !en_periodo_prueba);
    printf("Puede ascender:%d\n", edad < 30 && salario > 1600.0f && tiene_contrato);
    return 0;
}
```

### Resultados
```
Beneficios:     1   (25>=23 ✅ Y 1800>1500 ✅)
Bonus:          1   (tiene_contrato=1 → ya es true, OR no evalúa el segundo)
Consolidado:    1   (!0 = 1)
Puede ascender: 1   (25<30 ✅ Y 1800>1600 ✅ Y 1 ✅)
```

### Feedback

| Aspecto | Estado | Nota |
|---------|--------|------|
| `&&` con dos condiciones | ✅ | |
| `\|\|` — short-circuit | ❌ | Confundió `tiene_contrato=1` con "no tiene contrato" |
| `!` — negación lógica | ✅ | |
| `0=falso / 1=verdadero` | ⚠️ | Confusión recurrente |

> 💡 **Short-circuit:** con `||` si el primero es `true` el segundo no se evalúa. Con `&&` si el primero es `false` tampoco.

---

## Ejercicio 9 — Precedencia avanzada
**Tema:** Precedencia / trampas

### Código y resultados — a=6, b=4, c=3
```c
printf("%d\n", a + b > c && b - c < a);   // 1
printf("%d\n", !a == !b);                  // 1  (!6=0, !4=0 → 0==0=1)
printf("%d\n", a > b > c);                 // 0  TRAMPA
printf("%d\n", a != b || c == b - 1);      // 1
printf("%d\n", a & b | c);                 // 7
```

### La trampa — `a > b > c`
```
(a > b) > c → (6>4) > 3 → 1 > 3 → 0
```
Compara el booleano resultado con `c`. Nunca usar para rangos — usar `a > b && b > c`.

### `a & b | c` paso a paso
```
a=6 → 0110   b=4 → 0100   c=3 → 0011

0110 & 0100 = 0100 = 4   (& tiene mayor precedencia que |)
0100 | 0011 = 0111 = 7
```

---

## Ejercicio 10 — Intercambio XOR
**Tema:** XOR / bits

### Solución final
```c
#include <stdio.h>

int main(void) {
    int x, y;
    printf("Introduce x: "); scanf("%d", &x);
    printf("Introduce y: "); scanf("%d", &y);

    printf("Antes:   x=%d, y=%d\n", x, y);
    x = x ^ y;
    y = x ^ y;
    x = x ^ y;
    printf("Despues: x=%d, y=%d\n", x, y);
    return 0;
}
```

### Por qué funciona — ejemplo x=9, y=10
```
x=9→1001  y=10→1010

paso 1: x = 1001^1010 = 0011 = 3
paso 2: y = 0011^1010 = 1001 = 9   (y recupera el x original)
paso 3: x = 0011^1001 = 1010 = 10  (x recupera el y original)
```

---

## Ejercicio 11 — XOR predice la salida
**Tema:** XOR

### Código y resultados — a=15, b=9, c=6
```c
// 15→1111   9→1001   6→0110

printf("%d\n", a ^ b);           //  6   (1111^1001=0110)
printf("%d\n", a ^ b ^ a);       //  9   ((a^b)^a = b)
printf("%d\n", b ^ c ^ b);       //  6   ((b^c)^b = c)
printf("%d\n", a ^ b ^ b ^ a);   //  0   (todo se cancela)
printf("%d\n", a ^ 0);           // 15   (A^0=A)
printf("%d\n", a ^ a);           //  0   (A^A=0)
```

---

## Ejercicio 12 — Clasificador de notas
**Tema:** Ternario encadenado

### Solución final
```c
#include <stdio.h>

int main(void) {
    float nota;
    printf("Introduce nota (0-10): ");
    scanf("%f", &nota);

    printf("Nota %.1f → %s → letra %s\n",
        nota,
        nota >= 5.0f ? "Aprobado" : "Suspenso",
        (nota >= 9.0f) ? "A" :
        (nota >= 7.0f) ? "B" :
        (nota >= 5.0f) ? "C" :
        (nota >= 3.0f) ? "D" : "F");
    return 0;
}
```

---

## Ejercicio 13 — Calculadora IMC
**Tema:** Ternario / aritmética

### Solución final
```c
#include <stdio.h>

int main(void) {
    float peso, altura, imc;

    printf("[+] Peso (kg): ");  scanf("%f", &peso);
    printf("[+] Altura (m): "); scanf("%f", &altura);

    imc = peso / (altura * altura);

    printf("\nTu IMC es %.2f → %s\n", imc,
        (imc < 18.5f)  ? "bajo peso" :
        (imc <= 24.9f) ? "normal"    :
        (imc <= 29.9f) ? "sobrepeso" : "obesidad");
    return 0;
}
```

### Feedback

| Aspecto | Estado | Nota |
|---------|--------|------|
| Fórmula IMC correcta | ✅ | `peso / (altura * altura)` |
| `\n` en `scanf` | ❌ | Bloquea el programa |
| `const char *` | ⚠️ | Olvidado — usar siempre con strings literales |
| Límite `< 29.9` en vez de `<= 29.9` | ❌ | Excluía el valor exacto |

---

## Ejercicio 14 — Año bisiesto
**Tema:** `&&` `||` `%`

### Solución final
```c
#include <stdio.h>

int main(void) {
    int anio;
    printf("Introduce un año: ");
    scanf("%d", &anio);

    printf("El año %d es %s\n", anio,
        ((anio % 4 == 0 && anio % 100 != 0) || (anio % 400 == 0))
        ? "bisiesto" : "no bisiesto");
    return 0;
}
```

### Condición completa
```c
(anio % 4 == 0 && anio % 100 != 0) || (anio % 400 == 0)
```

```
2024 → 2024%4=0 ✅  2024%100≠0 ✅  → bisiesto
1900 → 1900%4=0 ✅  1900%100=0 ❌  → no bisiesto
2000 → 2000%400=0 ✅               → bisiesto
```

---

## Ejercicio 15 — Operaciones con bits
**Tema:** Bitwise completo

### Código y resultados — a=12, b=10
```c
// a=12→1100   b=10→1010

printf("a & b  = %d\n", a & b);    //  8  (1100&1010=1000)
printf("a | b  = %d\n", a | b);    // 14  (1100|1010=1110)
printf("a ^ b  = %d\n", a ^ b);    //  6  (1100^1010=0110)
printf("~a     = %d\n", ~a);        // -13 (invierte 32 bits)
printf("a << 1 = %d\n", a << 1);   // 24  (×2)
printf("a >> 1 = %d\n", a >> 1);   //  6  (÷2)
```

### Truco para `~a`
```c
~a = -(a + 1)   // fórmula rápida
~12 = -13
~0  = -1
```

---

## Ejercicio 16 — Precio con IVA 10%
**Tema:** Aritmética / formato

### Solución final
```c
#include <stdio.h>

int main(void) {
    float precio, iva, precio_final, total_neto;
    int   cantidad;

    printf("Precio del articulo: "); scanf("%f", &precio);
    printf("Cantidad: ");            scanf("%d", &cantidad);

    total_neto   = precio * cantidad;
    iva          = total_neto * 0.10f;
    precio_final = total_neto + iva;

    printf("\nSubtotal:      %.2f\n", total_neto);
    printf("IVA (10%%):     %.2f\n",  iva);
    printf("Total a pagar: %.2f\n",  precio_final);
    return 0;
}
```

---

## Ejercicio 17 — Comprobación de rango
**Tema:** Lógicos / relacional

### Solución final
```c
#include <stdio.h>

int main(void) {
    int numero;
    const char *rango, *multiplo, *par, *segundo_rango;

    printf("Introduce un numero entero: ");
    scanf("%d", &numero);

    rango         = (numero >= 1 && numero <= 100)
                    ? "dentro del rango 1-100" : "fuera del rango";
    multiplo      = (numero % 3 == 0 || numero % 5 == 0)
                    ? "es multiplo de 3 o de 5" : "NO es multiplo de 3 o de 5";
    par           = (numero % 2 == 0 && numero > 50)
                    ? "es par y mayor que 50" : "es impar O menor o igual a 50";
    segundo_rango = !(numero >= 10 && numero <= 20)
                    ? "NO esta entre 10 y 20" : "esta entre 10 y 20";

    printf("[+] El numero %d esta %s.\n", numero, rango);
    printf("[+] El numero %d %s.\n",      numero, multiplo);
    printf("[+] El numero %d %s.\n",      numero, par);
    printf("[+] El numero %d %s.\n",      numero, segundo_rango);
    return 0;
}
```

---

## Ejercicio 18 — Conversor de unidades
**Tema:** Aritmética / `const`

### Solución final
```c
#include <stdio.h>

int main(void) {
    const float METROS_POR_KM = 1000.0f;
    const float KM_POR_MILLA  = 1.60934f;
    const float PIES_POR_KM   = 3280.84f;
    float km;

    printf("Distancia en km: ");
    scanf("%f", &km);

    printf("%.2f km son:\n", km);
    printf("  %.2f metros\n", km * METROS_POR_KM);
    printf("  %.2f millas\n", km / KM_POR_MILLA);
    printf("  %.2f pies\n",   km * PIES_POR_KM);
    return 0;
}
```

### Feedback

| Aspecto | Estado | Nota |
|---------|--------|------|
| `const` para factores de conversión | ✅ | Buena idea |
| `const` en variable leída con `scanf` | ❌ | `const` no se puede modificar |
| Nombres de constantes descriptivos | ❌ | `metros=1000` no describe qué es — usar `METROS_POR_KM` |

---

## Ejercicio 19 — Predice la salida XOR avanzado
**Tema:** XOR — traza completa

### Código — x=7, y=5
```c
// x=7→0111   y=5→0101

x = x ^ y;   // 0111^0101 = 0010 = 2   → x=2, y=5
y = x ^ y;   // 0010^0101 = 0111 = 7   → x=2, y=7  (y recupera el x original)
x = x ^ y;   // 0010^0111 = 0101 = 5   → x=5, y=7  (x recupera el y original)
```

---

## Ejercicio 20 — Calculadora completa
**Tema:** Integrador

### Solución final
```c
#include <stdio.h>

int main(void) {
    int a, b;
    const char *par, *signo;

    printf("--- Calculadora ---\n");
    printf("[+] Numero A: "); scanf("%d", &a);
    printf("[+] Numero B: "); scanf("%d", &b);

    printf("\nOperaciones aritmeticas:\n");
    printf("  A + B = %d\n",   a + b);
    printf("  A - B = %d\n",   a - b);
    printf("  A * B = %d\n",   a * b);
    printf("  A / B = %d\n",   a / b);
    printf("  A / B = %.2f\n", (float)a / b);
    printf("  A %% B = %d\n",  a % b);

    printf("\nOperaciones de bits:\n");
    printf("  A & B = %d\n", a & b);
    printf("  A | B = %d\n", a | b);
    printf("  A ^ B = %d\n", a ^ b);

    printf("\nComparaciones:\n");
    printf("  A > B  = %d\n", a > b);
    printf("  A == B = %d\n", a == b);
    printf("  A != B = %d\n", a != b);

    printf("\nClasificacion de A:\n");
    par   = (a % 2 == 0) ? "Par"      : "Impar";
    signo = (a >= 0)     ? "Positivo" : "Negativo";
    printf("  Par/Impar: %s\n", par);
    printf("  Signo:     %s\n", signo);
    return 0;
}
```

---

## Serie — Operadores `++` y `--`
**Tema:** Pre y post incremento/decremento

### La regla fundamental
```c
post (x++)  →  asigna el valor ACTUAL, luego modifica x
pre  (++x)  →  modifica x PRIMERO, luego asigna el nuevo valor
```

### Ejercicio 1 — x = 3

```c
a = x++;   // a = ?  x = ?
b = x++;   // b = ?  x = ?
c = ++x;   // c = ?  x = ?
d = x--;   // d = ?  x = ?
e = --x;   // e = ?  x = ?
```

<details>
<summary>Solución</summary>

```c
a = x++;   // a=3,  x=4
b = x++;   // b=4,  x=5
c = ++x;   // c=6,  x=6
d = x--;   // d=6,  x=5
e = --x;   // e=4,  x=4
```
</details>

---

### Ejercicio 2 — x = 1

```c
a = ++x;   // a = ?  x = ?
b = ++x;   // b = ?  x = ?
c = x--;   // c = ?  x = ?
d = x--;   // d = ?  x = ?
e = ++x;   // e = ?  x = ?
```

<details>
<summary>Solución</summary>

```c
a = ++x;   // a=2,  x=2
b = ++x;   // b=3,  x=3
c = x--;   // c=3,  x=2
d = x--;   // d=2,  x=1
e = ++x;   // e=2,  x=2
```
</details>

---

### Ejercicio 3 — con operaciones, x = 5

```c
a = x++ * 2;   // a = ?  x = ?
b = ++x * 3;   // b = ?  x = ?
c = x-- - 4;   // c = ?  x = ?
d = --x + 1;   // d = ?  x = ?
```

<details>
<summary>Solución</summary>

```c
a = x++ * 2;   // a=10, x=6
b = ++x * 3;   // b=21, x=7
c = x-- - 4;   // c=3,  x=6
d = --x + 1;   // d=6,  x=5
```
</details>

---

### Ejercicio 4 — x = 10

```c
a = x-- + 5;   // a = ?  x = ?
b = --x - 2;   // b = ?  x = ?
c = x++ * 2;   // c = ?  x = ?
d = ++x + x;   // ⚠️ trampa
```

<details>
<summary>Solución</summary>

```c
a = x-- + 5;   // a=15, x=9
b = --x - 2;   // b=6,  x=8
c = x++ * 2;   // c=16, x=9
d = ++x + x;   // ⚠️ COMPORTAMIENTO INDEFINIDO — nunca usar
```
</details>

---

### Ejercicio 5 — serie larga, x = 10

```c
a = x++;   b = ++x;   c = x--;
d = --x;   e = x++;   f = ++x;
```

<details>
<summary>Solución</summary>

```c
a = x++;   // a=10, x=11
b = ++x;   // b=12, x=12
c = x--;   // c=12, x=11
d = --x;   // d=10, x=10
e = x++;   // e=10, x=11
f = ++x;   // f=12, x=12
```
</details>

---

### Reglas de uso seguro
```c
// ✅ Seguro
a = x++;
b = ++x * 3;

// ❌ Comportamiento indefinido
a = x++ + x++;
d = ++x + x;

// En for — equivalentes
for (int i = 0; i < 10; i++)    // ✅
for (int i = 0; i < 10; ++i)    // ✅ idéntico
```

---

## Serie — Desplazamiento de bits `<<` `>>`

### Concepto
```
a << n  →  desplaza izquierda n posiciones  →  multiplica por 2^n
a >> n  →  desplaza derecha  n posiciones  →  divide por 2^n (entera)
```

### Ejercicio 1 — a = 4 (0000 0100)

```
a << 1 → ?    a << 2 → ?    a << 3 → ?
a >> 1 → ?    a >> 2 → ?
```

<details>
<summary>Solución</summary>

```
a << 1 → 0000 1000 =  8   (×2)
a << 2 → 0001 0000 = 16   (×4)
a << 3 → 0010 0000 = 32   (×8)
a >> 1 → 0000 0010 =  2   (÷2)
a >> 2 → 0000 0001 =  1   (÷4)
```
</details>

---

### Ejercicio 2 — a = 32 (0010 0000)

```
a >> 1 → ?    a >> 2 → ?    a >> 5 → ?
a << 1 → ?    a << 2 → ?
```

<details>
<summary>Solución</summary>

```
a >> 1 → 0001 0000 = 16
a >> 2 → 0000 1000 =  8
a >> 5 → 0000 0001 =  1   (el único 1 llega a posición 0)
a << 1 → 0100 0000 = 64
a << 2 → 1000 0000 = 128
```
</details>

---

## Errores más frecuentes

| Error | Solución |
|-------|----------|
| `char nombre[49]` + `scanf %49s` | Array debe ser `[50]` — necesita sitio para `'\0'` |
| Recalcular la misma expresión en cada `printf` | Guardar en variable intermedia y reutilizar |
| Declarar variables y no usarlas | Si no se usa, borrar |
| `9/5` en lugar de `9.0f/5.0f` | Con `float` usar siempre literales con `f` |
| `(float)(a/b)` — cast tarde | `(float)a/b` — el cast debe ir antes de dividir |
| `\n` al final del formato en `scanf` | Nunca poner `\n` en `scanf` |
| `%` sin escapar en `printf` | Usar `%%` para imprimir el símbolo `%` |
| `int main()` sin `void` | `int main(void)` |
| `x++ + x++` en una expresión | Un solo `++`/`--` por expresión |
| Etiqueta `printf` no coincide con variable | Verificar siempre que coinciden |
| `char *` sin `const` para strings | Usar siempre `const char *` |
| `const` en variable leída con `scanf` | `const` no se puede modificar |
| `a > b > c` para comprobar rangos | Usar `a > b && b > c` |
| Variables declaradas tras código ejecutable | Declarar siempre al inicio del bloque |

---

## Progresión

- Separación cálculo/presentación: natural desde el ejercicio 3.
- Nombres de variables: descriptivos y consistentes desde el primer intento.
- `%%` para el símbolo `%`: correcto sin recordatorio.
- Lógica matemática y condiciones: sólida desde el principio.
- Bits y XOR: comprendidos con buena progresión.
- Operadores `++`/`--`: dominados tras serie de ejercicios.

---

## ⚠️ Puntos débiles — repasar antes del Bloque 4

Estos errores aparecieron más de una vez. Conviene repasarlos antes de continuar.

### 1. `const char *` con strings literales
Olvidado en ejercicios 13, 17, 18 y 20:

```c
const char *mensaje = "Hola";   // ✅ siempre así
char *mensaje = "Hola";         // ⚠️ sin const — el compilador puede avisar
```

### 2. Literales `double` con variables `float`
Olvidado en ejercicios 4, 13 y 18:

```c
float f = 9.0 / 5.0;    // ⚠️ 9.0 y 5.0 son double
float f = 9.0f / 5.0f;  // ✅
```

### 3. `0 = falso / 1 = verdadero`
Confusión en ejercicio 8:

```c
int tiene_contrato = 1;   // 1 = SÍ tiene contrato ✅
int tiene_contrato = 0;   // 0 = NO tiene contrato ✅
// Nunca al revés
```

### 4. `\n` en `scanf`
Olvidado en ejercicios 7 y 13:

```c
scanf("%f\n", &x);   // ❌ bloquea el programa
scanf("%f", &x);     // ✅
```

### 5. Pre/post incremento
Tardó varias rondas en afianzarse. Regla para recordar:

```c
a = x++;   // usa x AHORA, modifica DESPUÉS
a = ++x;   // modifica PRIMERO, usa el nuevo valor
```

### 6. Trampa `a > b > c`
Error en ejercicio 9:

```c
a > b > c        // ❌ compara (a>b) con c — da 0 o 1, no lo que esperas
a > b && b > c   // ✅ esto es lo que realmente quieres
```

---

*Programación en C — Bloques 2 y 3 · Referencia personal*
