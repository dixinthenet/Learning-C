# Recopilatorio de Ejercicios — C
**Bloques 2 y 3 — Variables, Tipos, Operadores y Expresiones**

Compilar siempre con:
```bash
gcc -Wall -Wextra -std=c11 -g archivo.c -o programa
```

---

## Índice

| # | Título | Tema | Dificultad |
|---|--------|------|------------|
| 1 | Datos del alumno | Variables / tipos / ternario | ⭐ |
| 2 | Calculadora de descuento | Aritmética / variables intermedias | ⭐ |
| 3 | División entera vs real | Tipos / cast / trampa | ⭐ |
| 4 | Conversión de temperatura | Aritmética / literales float | ⭐ |
| 5 | Precedencia de operadores | Precedencia | ⭐⭐ |
| 6 | Segundos a horas:min:seg | Módulo y división entera | ⭐⭐ |
| 7 | Precio con impuestos | Aritmética / formato | ⭐ |
| 8 | Operadores lógicos | && \|\| ! | ⭐⭐ |
| 9 | Precedencia avanzada | Precedencia / trampas | ⭐⭐⭐ |
| 10 | Intercambio XOR | XOR / bits | ⭐⭐ |
| 11 | XOR — predice la salida | XOR | ⭐⭐ |
| 12 | Clasificador de notas | Ternario encadenado | ⭐⭐ |
| 13 | Calculadora IMC | Ternario / aritmética | ⭐⭐ |
| 14 | Año bisiesto | && \|\| % | ⭐⭐⭐ |
| 15 | Operaciones con bits | Bitwise completo | ⭐⭐⭐ |
| 16 | Precio con IVA 10% | Aritmética / formato | ⭐ |
| 17 | Comprobación de rango | Lógicos / relacional | ⭐⭐ |
| 18 | Conversor de unidades | Aritmética / const | ⭐⭐ |
| 19 | Predice la salida XOR avanzado | XOR | ⭐⭐⭐ |
| 20 | Calculadora completa | Integrador | ⭐⭐⭐ |
| ++ | Serie pre/post incremento | Operadores ++ y -- | ⭐⭐ |
| <<>> | Serie desplazamiento de bits | Bitwise shift | ⭐⭐ |

---

# EJERCICIOS

---

## Ejercicio 1 — Datos del alumno
**Tema:** Variables / tipos / ternario — ⭐

Declara variables para almacenar los datos de un alumno y pídelos por teclado:
- Nombre (máx. 50 caracteres)
- Edad (entero)
- Nota media (decimal con 2 cifras)
- Mostrar si está aprobado o suspenso usando el operador ternario

```c
#include <stdio.h>

int main(void) {
    // Declara las variables aquí

    // Lee los datos con scanf

    // Muestra los resultados con printf
    // Usa el ternario para aprobado/suspenso

    return 0;
}
```

> 💡 Usa `%49s` en `scanf` para evitar desbordamiento del buffer.

---

## Ejercicio 2 — Calculadora de descuento
**Tema:** Aritmética / variables intermedias — ⭐

Dado un precio original (`200.0f`) y un descuento del 15%, calcula y muestra:
- Importe del descuento
- Precio tras el descuento
- IVA del 21% sobre el precio descontado
- Precio total final

```c
#include <stdio.h>

int main(void) {
    float precio_original = 200.0f;
    float descuento_pct   = 0.15f;
    float iva             = 0.21f;

    // Calcula con variables intermedias
    // Muestra los resultados con 2 decimales

    return 0;
}
```

> 💡 Guarda cada resultado en una variable — nunca repitas la misma expresión.

---

## Ejercicio 3 — División entera vs real
**Tema:** Tipos / cast / trampa del paréntesis — ⭐

Predice la salida de cada `printf` **antes de compilar**. Luego verifica:

```c
#include <stdio.h>

int main(void) {
    int   a = 9, b = 4;
    float c = 9.0f;

    printf("%d\n",   a / b);              // ?
    printf("%.2f\n", c / b);              // ?
    printf("%.2f\n", (float)a / b);       // ?
    printf("%d\n",   a % b);              // ?
    printf("%.2f\n", (float)(a / b));     // ?  <- trampa

    return 0;
}
```

> ⚠️ La última línea es una trampa clásica. ¿El cast llega a tiempo?

---

## Ejercicio 4 — Conversión de temperatura
**Tema:** Aritmética / literales float — ⭐

Pide una temperatura en Celsius y conviértela a Fahrenheit y Kelvin:
- `F = (C × 9.0 / 5.0) + 32`
- `K = C + 273.15`

```c
#include <stdio.h>

int main(void) {
    float c, f, k;

    printf("Introduce la temperatura en Celsius: ");
    scanf("%f", &c);

    // Calcula f y k
    // Muestra los tres valores con 2 decimales

    return 0;
}
```

> ⚠️ Escribe `9.0f / 5.0f`, nunca `9/5` (división entera da 1).

---

## Ejercicio 5 — Precedencia de operadores
**Tema:** Precedencia — ⭐⭐

Predice el resultado de cada expresión **sin compilar**. Razona el orden de evaluación:

```c
#include <stdio.h>

int main(void) {
    int a = 5, b = 3, c = 2;

    printf("%d\n", a + b * c);           // ?
    printf("%d\n", (a + b) * c);         // ?
    printf("%d\n", a * b - c * b);       // ?
    printf("%d\n", a % b * c);           // ?
    printf("%d\n", a / b * b + a % b);   // ?  <- trampa

    return 0;
}
```

> 💡 La última línea aplica la identidad `a = (a/b)*b + a%b`.

---

## Ejercicio 6 — Segundos a horas:minutos:segundos
**Tema:** Módulo y división entera — ⭐⭐

El usuario introduce un número de segundos totales. Conviértelo a formato `horas:minutos:segundos`.

Ejemplo: `3750 segundos → 1:02:30`

```c
#include <stdio.h>

int main(void) {
    int segundos_totales;

    printf("Introduce segundos: ");
    scanf("%d", &segundos_totales);

    // Calcula horas, minutos y segundos restantes
    // Pista: usa / y %

    return 0;
}
```

> 💡 `horas = total / 3600` — `minutos = (total % 3600) / 60` — `segundos = total % 60`

---

## Ejercicio 7 — Precio con impuestos
**Tema:** Aritmética / formato — ⭐

Pide al usuario el precio de un artículo y la cantidad. Calcula y muestra:
- Subtotal
- IVA al 10%
- Precio final

```c
#include <stdio.h>

int main(void) {
    float precio;
    int   cantidad;

    printf("Precio del articulo: ");
    scanf("%f", &precio);
    printf("Cantidad: ");
    scanf("%d", &cantidad);

    // Calcula y muestra los resultados

    return 0;
}
```

> 💡 Para imprimir `%` en `printf` usa `%%`.

---

## Ejercicio 8 — Operadores lógicos
**Tema:** `&&` `||` `!` — ⭐⭐

Dado este código, predice cuáles condiciones son verdaderas (1) y cuáles falsas (0):

```c
#include <stdio.h>

int main(void) {
    int   edad             = 25;
    float salario          = 1800.0f;
    int   tiene_contrato   = 1;
    int   en_periodo_prueba = 0;

    // Beneficios: edad >= 23 Y salario > 1500
    printf("Beneficios:    %d\n", edad >= 23 && salario > 1500.0f);

    // Bonus: tiene contrato O salario > 2000
    printf("Bonus:         %d\n", tiene_contrato || salario > 2000.0f);

    // No está en periodo de prueba
    printf("Consolidado:   %d\n", !en_periodo_prueba);

    // Puede ascender: edad < 30 Y salario > 1600 Y tiene contrato
    printf("Puede ascender:%d\n", edad < 30 && salario > 1600.0f && tiene_contrato);

    return 0;
}
```

> 💡 Recuerda: `0 = FALSO`, `1 = VERDADERO`. Nunca al revés.

---

## Ejercicio 9 — Precedencia avanzada
**Tema:** Precedencia / trampas — ⭐⭐⭐

Predice el resultado de cada expresión. Razona el orden paso a paso:

```c
#include <stdio.h>

int main(void) {
    int a = 6, b = 4, c = 3;

    printf("%d\n", a + b > c && b - c < a);    // ?
    printf("%d\n", !a == !b);                   // ?
    printf("%d\n", a > b > c);                  // ?  <- trampa
    printf("%d\n", a != b || c == b - 1);       // ?
    printf("%d\n", a & b | c);                  // ?  <- bits

    return 0;
}
```

> ⚠️ `a > b > c` NO compara los tres valores. ¿Qué tipo devuelve `a > b`?

---

## Ejercicio 10 — Intercambio XOR
**Tema:** XOR / bits — ⭐⭐

Intercambia dos variables enteras usando XOR sin variable auxiliar:

```c
#include <stdio.h>

int main(void) {
    int x, y;
    printf("Introduce x: "); scanf("%d", &x);
    printf("Introduce y: "); scanf("%d", &y);

    printf("Antes:   x=%d, y=%d\n", x, y);

    // Intercambia con XOR — 3 líneas con ^

    printf("Despues: x=%d, y=%d\n", x, y);
    return 0;
}
```

> 💡 Recuerda: `A ^ A = 0` y `A ^ 0 = A`

---

## Ejercicio 11 — XOR predice la salida
**Tema:** XOR — ⭐⭐

Calcula cada resultado a mano en binario. Luego verifica compilando:

```c
#include <stdio.h>

int main(void) {
    int a = 15;   // 1111
    int b = 9;    // 1001
    int c = 6;    // 0110

    printf("%d\n", a ^ b);           // ?
    printf("%d\n", a ^ b ^ a);       // ?
    printf("%d\n", b ^ c ^ b);       // ?
    printf("%d\n", a ^ b ^ b ^ a);   // ?
    printf("%d\n", a ^ 0);           // ?
    printf("%d\n", a ^ a);           // ?

    return 0;
}
```

---

## Ejercicio 12 — Clasificador de notas
**Tema:** Ternario encadenado — ⭐⭐

El usuario introduce una nota (0-10). Usa el operador ternario para clasificarla en letra y mostrar si está aprobado:

| Rango | Letra |
|-------|-------|
| 9-10 | A |
| 7-8 | B |
| 5-6 | C |
| 3-4 | D |
| < 3 | F |

```c
#include <stdio.h>

int main(void) {
    float nota;
    printf("Introduce nota (0-10): ");
    scanf("%f", &nota);

    // Muestra nota, letra y aprobado/suspenso con ternario

    return 0;
}
```

---

## Ejercicio 13 — Calculadora IMC
**Tema:** Ternario / aritmética — ⭐⭐

Pide peso (kg) y altura (m). Calcula el IMC y clasifica:
- `< 18.5` → Bajo peso
- `18.5 – 24.9` → Normal
- `25.0 – 29.9` → Sobrepeso
- `>= 30.0` → Obesidad

```c
#include <stdio.h>

int main(void) {
    float peso, altura, imc;

    printf("[+] Peso (kg): ");  scanf("%f", &peso);
    printf("[+] Altura (m): "); scanf("%f", &altura);

    // Calcula IMC = peso / (altura * altura)
    // Clasifica con ternario encadenado

    return 0;
}
```

---

## Ejercicio 14 — Año bisiesto
**Tema:** `&&` `||` `%` — ⭐⭐⭐

Un año es bisiesto si:
- Es divisible entre 4 **Y** no entre 100, **O bien** es divisible entre 400

```c
#include <stdio.h>

int main(void) {
    int anio;
    printf("Introduce un año: ");
    scanf("%d", &anio);

    // Una sola expresión con && || y %
    // Muestra si es bisiesto o no con ternario

    return 0;
}
```

---

## Ejercicio 15 — Operaciones con bits
**Tema:** Bitwise completo — ⭐⭐⭐

Predice la salida de cada operación **antes de compilar**. Trabájalo en binario:

```c
#include <stdio.h>

int main(void) {
    int a = 12;   // 1100
    int b = 10;   // 1010

    printf("a & b  = %d\n", a & b);    // ?
    printf("a | b  = %d\n", a | b);    // ?
    printf("a ^ b  = %d\n", a ^ b);    // ?
    printf("~a     = %d\n", ~a);        // ?  <- trampa
    printf("a << 1 = %d\n", a << 1);   // ?
    printf("a >> 1 = %d\n", a >> 1);   // ?

    return 0;
}
```

> ⚠️ `~a` invierte los 32 bits — el resultado casi siempre es negativo.

---

## Ejercicio 16 — Precio con IVA 10%
**Tema:** Aritmética / formato — ⭐

Pide precio y cantidad. Calcula subtotal, IVA (10%) y total:

```c
#include <stdio.h>

int main(void) {
    float precio;
    int   cantidad;

    printf("Precio del articulo: "); scanf("%f", &precio);
    printf("Cantidad: ");            scanf("%d", &cantidad);

    // Calcula y muestra subtotal, IVA y total

    return 0;
}
```

---

## Ejercicio 17 — Comprobación de rango
**Tema:** Lógicos / relacional — ⭐⭐

El usuario introduce un número entero. Comprueba y muestra:
- Si está entre 1 y 100 (inclusive)
- Si es múltiplo de 3 O de 5
- Si es par Y mayor que 50
- Si NO está en el rango 10-20

```c
#include <stdio.h>

int main(void) {
    int numero;
    printf("Introduce un numero entero: ");
    scanf("%d", &numero);

    // Escribe las 4 comprobaciones con printf y ternario

    return 0;
}
```

---

## Ejercicio 18 — Conversor de unidades
**Tema:** Aritmética / `const` — ⭐⭐

Pide una distancia en kilómetros y conviértela a metros, millas y pies:
- Metros: `× 1000`
- Millas: `÷ 1.60934`
- Pies: `× 3280.84`

```c
#include <stdio.h>

int main(void) {
    float km;
    printf("Distancia en km: ");
    scanf("%f", &km);

    // Declara constantes con const para los factores
    // Calcula y muestra las tres conversiones

    return 0;
}
```

> 💡 Usa `const float METROS_POR_KM = 1000.0f;` en vez de hardcodear los números.

---

## Ejercicio 19 — Predice la salida XOR avanzado
**Tema:** XOR — ⭐⭐⭐

Traza la ejecución paso a paso en binario. Predice cada `printf`:

```c
#include <stdio.h>

int main(void) {
    int x = 7;    // 0111
    int y = 5;    // 0101

    x = x ^ y;
    printf("x=%d y=%d\n", x, y);   // ?

    y = x ^ y;
    printf("x=%d y=%d\n", x, y);   // ?

    x = x ^ y;
    printf("x=%d y=%d\n", x, y);   // ?

    return 0;
}
```

> ⚠️ Traza los tres pasos en binario para entenderlo.

---

## Ejercicio 20 — Calculadora completa
**Tema:** Integrador — ⭐⭐⭐

Programa completo que pide dos números y muestra:

```
--- Calculadora ---
[+] Numero A: 15
[+] Numero B: 4

Operaciones aritmeticas:
  A + B = 19
  A - B = 11
  A * B = 60
  A / B = 3      (entera)
  A / B = 3.75   (real)
  A % B = 3

Operaciones de bits:
  A & B = ?
  A | B = ?
  A ^ B = ?

Comparaciones:
  A > B  = 1
  A == B = 0
  A != B = 1

Clasificacion de A:
  Par/Impar: Impar
  Signo:     Positivo
```

> 💡 Usa ternario para Par/Impar y Positivo/Negativo/Cero.

---

## Serie — Operadores `++` y `--`
**Tema:** Pre y post incremento/decremento — ⭐⭐

### La regla fundamental
```c
post (x++)  →  asigna el valor ACTUAL, luego modifica x
pre  (++x)  →  modifica x PRIMERO, luego asigna el nuevo valor
```

### Ejercicio A — x = 3
```c
int x = 3;
int a, b, c, d, e;

a = x++;   // a = ?  x = ?
b = x++;   // b = ?  x = ?
c = ++x;   // c = ?  x = ?
d = x--;   // d = ?  x = ?
e = --x;   // e = ?  x = ?
```

### Ejercicio B — x = 1
```c
int x = 1;
int a, b, c, d, e;

a = ++x;   // a = ?  x = ?
b = ++x;   // b = ?  x = ?
c = x--;   // c = ?  x = ?
d = x--;   // d = ?  x = ?
e = ++x;   // e = ?  x = ?
```

### Ejercicio C — con operaciones aritméticas, x = 5
```c
int x = 5;
int a, b, c, d;

a = x++ * 2;   // a = ?  x = ?
b = ++x * 3;   // b = ?  x = ?
c = x-- - 4;   // c = ?  x = ?
d = --x + 1;   // d = ?  x = ?
```

### Ejercicio D — x = 10
```c
int x = 10;
int a, b, c, d;

a = x-- + 5;   // a = ?  x = ?
b = --x - 2;   // b = ?  x = ?
c = x++ * 2;   // c = ?  x = ?
d = ++x + x;   // d = ?  x = ?  ⚠️ trampa
```

### Ejercicio E — serie larga, x = 10
```c
int x = 10;
int a, b, c, d, e, f;

a = x++;   // a = ?  x = ?
b = ++x;   // b = ?  x = ?
c = x--;   // c = ?  x = ?
d = --x;   // d = ?  x = ?
e = x++;   // e = ?  x = ?
f = ++x;   // f = ?  x = ?
```

---

## Serie — Desplazamiento de bits `<<` `>>`
**Tema:** Bitwise shift — ⭐⭐

### Concepto
```
a << n  →  desplaza bits a la izquierda  →  multiplica por 2^n
a >> n  →  desplaza bits a la derecha   →  divide por 2^n (entera)
```

### Ejercicio A — a = 4 (0000 0100)
```
a << 1 = ?    a << 2 = ?    a << 3 = ?
a >> 1 = ?    a >> 2 = ?
```

### Ejercicio B — a = 32 (0010 0000)
```
a >> 1 = ?    a >> 2 = ?    a >> 5 = ?
a << 1 = ?    a << 2 = ?
```

---

# SOLUCIONES

---

## Solución 1 — Datos del alumno

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

**Errores cometidos:**

| Aspecto | Estado | Nota |
|---------|--------|------|
| `char nombre[49]` con `%49s` | ❌ | Desbordamiento — el array debe ser `[50]` |
| Variable declarada sin usar | ⚠️ | Borrar variables que no se usan |
| `int main()` sin `void` | ⚠️ | Usar siempre `int main(void)` |
| Ternario directo en `printf` | ✅ | Bien usado |

---

## Solución 2 — Calculadora de descuento

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

**Errores cometidos:**

| Aspecto | Estado | Nota |
|---------|--------|------|
| Recalcular la misma expresión en cada `printf` | ❌ | Guardar en variables intermedias |
| Declarar `descuento_pct` y no usarla | ❌ | Usar las variables declaradas |
| Etiqueta no coincide con variable | ❌ | La etiqueta debe coincidir con lo que imprime |
| `%` sin escapar | ❌ | Usar `%%` |

---

## Solución 3 — División entera vs real

```c
printf("%d\n",   a / b);           // 2    división entera — trunca
printf("%.2f\n", c / b);           // 2.25 float/int → float
printf("%.2f\n", (float)a / b);    // 2.25 cast ANTES de dividir
printf("%d\n",   a % b);           // 1    resto
printf("%.2f\n", (float)(a / b));  // 2.00 TRAMPA — divide primero, cast tarde
```

**Concepto clave:**
```c
(float)a / b      // cast ANTES → 2.25  ✅
(float)(a / b)    // divide primero → 2.00  ❌
```

---

## Solución 4 — Conversión de temperatura

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

**Errores cometidos:**

| Aspecto | Estado | Nota |
|---------|--------|------|
| Literales `9.0` / `5.0` sin `f` | ⚠️ | Con `float` usar `9.0f / 5.0f` |
| Argumento extra en `printf` sin `%` | ❌ | `printf("texto", c)` — `c` sin especificador |

---

## Solución 5 — Precedencia de operadores

```c
a + b * c           // 11  (* antes que +)
(a + b) * c         // 16  (paréntesis primero)
a * b - c * b       //  9  (ambos * antes que -)
a % b * c           //  4  (5%3=2, luego 2*2=4)
a / b * b + a % b   //  5  (identidad: a = (a/b)*b + a%b)
```

**Errores cometidos:**

| Aspecto | Estado | Nota |
|---------|--------|------|
| `a * b - c * b` | ❌ | Calculó 20 — los dos `*` van antes que `-` |
| `a % b * c` | ❌ | `5%3=2`, luego `2*2=4` — no 6 |

---

## Solución 6 — Segundos a horas:min:seg

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

**Errores cometidos:**

| Aspecto | Estado | Nota |
|---------|--------|------|
| No usar el operador `%` | ❌ | Era el concepto clave del ejercicio |
| Usar `float` en vez de `int` | ❌ | Horas/min/seg son enteros |
| Typo `3600.2f` | ❌ | Error de escritura |

---

## Solución 7 — Precio con impuestos

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

**Errores cometidos:**

| Aspecto | Estado | Nota |
|---------|--------|------|
| `\n` en `scanf` | ❌ | Bloquea el programa esperando más input |
| `%%` para `%` | ✅ | Correcto desde el primer intento |

---

## Solución 8 — Operadores lógicos

```
Beneficios:     1   (25>=23 ✅ Y 1800>1500 ✅)
Bonus:          1   (tiene_contrato=1 → ya es true, OR no evalúa el segundo)
Consolidado:    1   (!0 = 1)
Puede ascender: 1   (25<30 ✅ Y 1800>1600 ✅ Y tiene_contrato=1 ✅)
```

**Errores cometidos:**

| Aspecto | Estado | Nota |
|---------|--------|------|
| Confundió `tiene_contrato=1` con "no tiene contrato" | ❌ | `1=verdadero`, `0=falso` — nunca al revés |
| `!en_periodo_prueba` | ✅ | Correcto |

---

## Solución 9 — Precedencia avanzada

```c
a + b > c && b - c < a   // 1   (> y < antes que &&)
!a == !b                  // 1   (!6=0, !4=0 → 0==0=1)
a > b > c                 // 0   TRAMPA: (6>4)=1 > 3 → 0
a != b || c == b - 1      // 1
a & b | c                 // 7   (& antes que |: 0110&0100=0100=4, 0100|0011=0111=7)
```

**La trampa de `a > b > c`:**
```
(a > b) > c → (6>4) > 3 → 1 > 3 → 0
```
Nunca usar para rangos — usar `a > b && b > c`.

---

## Solución 10 — Intercambio XOR

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

**Por qué funciona — x=9, y=10:**
```
paso 1: x = 1001^1010 = 0011 = 3
paso 2: y = 0011^1010 = 1001 = 9   (y recupera el x original)
paso 3: x = 0011^1001 = 1010 = 10  (x recupera el y original)
```

---

## Solución 11 — XOR predice la salida

```c
// a=15→1111   b=9→1001   c=6→0110

a ^ b         //  6   (1111^1001=0110)
a ^ b ^ a     //  9   ((a^b)^a = b — el a se cancela)
b ^ c ^ b     //  6   ((b^c)^b = c — el b se cancela)
a ^ b ^ b ^ a //  0   (todo se cancela: (a^a)=0, (b^b)=0)
a ^ 0         // 15   (A^0=A)
a ^ a         //  0   (A^A=0)
```

**Errores cometidos:**

| Aspecto | Estado | Nota |
|---------|--------|------|
| `a ^ b ^ b ^ a` | ❌ | Sustituyó `b` dos veces en lugar de una |

---

## Solución 12 — Clasificador de notas

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

## Solución 13 — Calculadora IMC

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

**Errores cometidos:**

| Aspecto | Estado | Nota |
|---------|--------|------|
| `\n` en `scanf` | ❌ | Bloquea el programa |
| `const char *` olvidado | ⚠️ | Usar siempre con strings literales |
| `< 29.9` en vez de `<= 29.9` | ❌ | Excluía el valor exacto |

---

## Solución 14 — Año bisiesto

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

**Verificación:**
```
2024 → 2024%4=0 ✅  2024%100≠0 ✅  → bisiesto
1900 → 1900%4=0 ✅  1900%100=0 ❌  → no bisiesto
2000 → 2000%400=0 ✅               → bisiesto
```

---

## Solución 15 — Operaciones con bits

```c
// a=12→1100   b=10→1010

a & b  =  8   (1100 & 1010 = 1000)
a | b  = 14   (1100 | 1010 = 1110)
a ^ b  =  6   (1100 ^ 1010 = 0110)
~a     = -13  (invierte 32 bits → negativo: ~a = -(a+1))
a << 1 = 24   (1100 → 11000, ×2)
a >> 1 =  6   (1100 → 0110, ÷2)
```

---

## Solución 16 — Precio con IVA 10%

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

## Solución 17 — Comprobación de rango

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

## Solución 18 — Conversor de unidades

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

**Errores cometidos:**

| Aspecto | Estado | Nota |
|---------|--------|------|
| `const` en variable leída con `scanf` | ❌ | `const` no se puede modificar |
| Nombres de constantes poco descriptivos | ❌ | Usar `METROS_POR_KM` no `metros` |

---

## Solución 19 — Predice la salida XOR avanzado

```c
// x=7→0111   y=5→0101

x = x ^ y;   // 0111^0101 = 0010 = 2   → x=2, y=5
// printf → x=2 y=5

y = x ^ y;   // 0010^0101 = 0111 = 7   → x=2, y=7
// printf → x=2 y=7

x = x ^ y;   // 0010^0111 = 0101 = 5   → x=5, y=7
// printf → x=5 y=7
```

Resultado final: x e y quedan intercambiados (7 y 5 → 5 y 7).

---

## Solución 20 — Calculadora completa

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

    par   = (a % 2 == 0) ? "Par"      : "Impar";
    signo = (a >= 0)     ? "Positivo" : "Negativo";
    printf("\nClasificacion de A:\n");
    printf("  Par/Impar: %s\n", par);
    printf("  Signo:     %s\n", signo);
    return 0;
}
```

**Errores cometidos:**

| Aspecto | Estado | Nota |
|---------|--------|------|
| Operaciones de bits `\|` y `^` | ❌ | Faltaban en primera entrega |
| Comparaciones mezcladas con bits | ❌ | Deben ir en bloque separado |

---

## Solución Serie ++ / --

### Ejercicio A — x = 3
```c
a = x++;   // a=3,  x=4
b = x++;   // b=4,  x=5
c = ++x;   // c=6,  x=6
d = x--;   // d=6,  x=5
e = --x;   // e=4,  x=4
```

### Ejercicio B — x = 1
```c
a = ++x;   // a=2,  x=2
b = ++x;   // b=3,  x=3
c = x--;   // c=3,  x=2
d = x--;   // d=2,  x=1
e = ++x;   // e=2,  x=2
```

### Ejercicio C — x = 5
```c
a = x++ * 2;   // a=10, x=6
b = ++x * 3;   // b=21, x=7
c = x-- - 4;   // c=3,  x=6
d = --x + 1;   // d=6,  x=5
```

### Ejercicio D — x = 10
```c
a = x-- + 5;   // a=15, x=9
b = --x - 2;   // b=6,  x=8
c = x++ * 2;   // c=16, x=9
d = ++x + x;   // ⚠️ COMPORTAMIENTO INDEFINIDO — nunca usar
```

### Ejercicio E — x = 10
```c
a = x++;   // a=10, x=11
b = ++x;   // b=12, x=12
c = x--;   // c=12, x=11
d = --x;   // d=10, x=10
e = x++;   // e=10, x=11
f = ++x;   // f=12, x=12
```

---

## Solución Serie `<<` `>>`

### Ejercicio A — a = 4
```
a << 1 → 0000 1000 =  8   (×2)
a << 2 → 0001 0000 = 16   (×4)
a << 3 → 0010 0000 = 32   (×8)
a >> 1 → 0000 0010 =  2   (÷2)
a >> 2 → 0000 0001 =  1   (÷4)
```

### Ejercicio B — a = 32
```
a >> 1 → 0001 0000 = 16
a >> 2 → 0000 1000 =  8
a >> 5 → 0000 0001 =  1
a << 1 → 0100 0000 = 64
a << 2 → 1000 0000 = 128
```

---

## ⚠️ Puntos débiles — repasar antes del Bloque 4

### 1. `const char *` con strings literales
Olvidado en ejercicios 13, 17, 18 y 20:
```c
const char *mensaje = "Hola";   // ✅
char *mensaje = "Hola";         // ⚠️ sin const
```

### 2. Literales `double` con variables `float`
Olvidado en ejercicios 4, 13 y 18:
```c
float f = 9.0 / 5.0;    // ⚠️ literales double
float f = 9.0f / 5.0f;  // ✅
```

### 3. `0 = falso / 1 = verdadero`
Confusión en ejercicio 8:
```c
int tiene_contrato = 1;   // SÍ tiene contrato ✅
int tiene_contrato = 0;   // NO tiene contrato ✅
```

### 4. `\n` en `scanf`
Olvidado en ejercicios 7 y 13:
```c
scanf("%f\n", &x);   // ❌ bloquea
scanf("%f", &x);     // ✅
```

### 5. Pre/post incremento
Tardó varias rondas — regla para recordar:
```c
a = x++;   // usa x AHORA, modifica DESPUÉS
a = ++x;   // modifica PRIMERO, usa el nuevo valor
```

### 6. Trampa `a > b > c`
Error en ejercicio 9:
```c
a > b > c        // ❌ compara booleano con c
a > b && b > c   // ✅
```

---

*Programación en C — Bloques 2 y 3 · Referencia personal*
