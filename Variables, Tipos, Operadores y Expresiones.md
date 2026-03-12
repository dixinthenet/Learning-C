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
| ++ | Serie pre/post incremento | Operadores ++ y -- |

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
    printf("Edad:                   %d\n",  edad);
    printf("Nota media:             %.2f\n", media);
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

> ⚠️ `int main()` acepta argumentos desconocidos. `int main(void)` es la forma correcta en C moderno.

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

> 💡 Separar siempre el bloque de cálculos del bloque de `printf`. Más legible y fácil de mantener.

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

> ⚠️ `9/5 = 1` (entera). `9.0/5.0 = 1.8` pero son `double`. Con `float` usar siempre `9.0f/5.0f`.

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

> 💡 Cuando `*` y `/` aparecen juntos se evalúan de izquierda a derecha (misma precedencia).

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

### Lógica del algoritmo — ejemplo con 3750 segundos
```
horas    = 3750 / 3600 = 1
restante = 3750 % 3600 = 150
minutos  = 150  / 60   = 2
segundos = 150  % 60   = 30
resultado: 1:02:30
```

### Feedback

| Aspecto | Estado | Nota |
|---------|--------|------|
| Uso del operador `%` | ❌ | Primera entrega no usó módulo |
| Formato entero `horas:min:seg` | ❌ | Primera entrega usó `float` |
| Typo `3600.2f` en lugar de `3600` | ❌ | Error de escritura |
| Algoritmo correcto con `/` y `%` | ✅ | Resuelto tras explicación |

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

> ⚠️ Nunca pongas `\n` ni espacios al final del formato en `scanf` — bloquea el programa.

---

## Serie — Operadores `++` y `--`
**Tema:** Pre y post incremento/decremento

### La regla fundamental
```c
post (x++)  →  asigna el valor ACTUAL, luego modifica x
pre  (++x)  →  modifica x PRIMERO, luego asigna el nuevo valor
```

---

### Ejercicio 1 — predice la salida, x = 3
```c
int x = 3;
int a, b, c, d, e;

a = x++;   // a = ?  x = ?
b = x++;   // b = ?  x = ?
c = ++x;   // c = ?  x = ?
d = x--;   // d = ?  x = ?
e = --x;   // e = ?  x = ?
```

<details>
<summary>Solución</summary>

```c
a = x++;   // a=3,  x=4   post: asigna 3, luego sube
b = x++;   // b=4,  x=5   post: asigna 4, luego sube
c = ++x;   // c=6,  x=6   pre:  sube a 6, asigna 6
d = x--;   // d=6,  x=5   post: asigna 6, luego baja
e = --x;   // e=4,  x=4   pre:  baja a 4, asigna 4
```
</details>

---

### Ejercicio 2 — predice la salida, x = 1
```c
int x = 1;
int a, b, c, d, e;

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

### Ejercicio 3 — con operaciones aritméticas, x = 5
```c
int x = 5;
int a, b, c, d;

a = x++ * 2;   // a = ?  x = ?
b = ++x * 3;   // b = ?  x = ?
c = x-- - 4;   // c = ?  x = ?
d = --x + 1;   // d = ?  x = ?
```

<details>
<summary>Solución</summary>

```c
a = x++ * 2;   // a=10, x=6   usa 5, luego sube → 5*2=10
b = ++x * 3;   // b=21, x=7   sube a 7 primero  → 7*3=21
c = x-- - 4;   // c=3,  x=6   usa 7, luego baja  → 7-4=3
d = --x + 1;   // d=6,  x=5   baja a 5 primero   → 5+1=6
```
</details>

---

### Ejercicio 4 — x = 10
```c
int x = 10;
int a, b, c, d;

a = x-- + 5;   // a = ?  x = ?
b = --x - 2;   // b = ?  x = ?
c = x++ * 2;   // c = ?  x = ?
d = ++x + x;   // d = ?  x = ?  ⚠️ trampa
```

<details>
<summary>Solución</summary>

```c
a = x-- + 5;   // a=15, x=9   usa 10+5=15, luego baja
b = --x - 2;   // b=6,  x=8   baja a 8 primero → 8-2=6
c = x++ * 2;   // c=16, x=9   usa 8*2=16, luego sube
d = ++x + x;   // ⚠️  COMPORTAMIENTO INDEFINIDO — nunca usar
```
</details>

---

### Ejercicio 5 — serie larga, x = 10
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
// ✅ Seguro — una sola operación ++/-- por expresión
a = x++;
b = ++x * 3;

// ❌ Comportamiento indefinido — nunca hacer esto
a = x++ + x++;
d = ++x + x;

// En bucles for — pre y post son equivalentes
for (int i = 0; i < 10; i++)    // ✅
for (int i = 0; i < 10; ++i)    // ✅ idéntico
```

> ⚠️ Más de un `++`/`--` sobre la misma variable en la misma expresión = comportamiento indefinido.

---

## Errores más frecuentes

| Error | Solución |
|-------|----------|
| `char nombre[49]` + `scanf %49s` | Array debe ser `[50]` — necesita sitio para `'\0'` |
| Recalcular la misma expresión en cada `printf` | Guardar en variable intermedia y reutilizar |
| Declarar variables y no usarlas | Si no se usa, borrar. Si se usa, referenciar |
| `9/5` en lugar de `9.0f/5.0f` | Con `float` usar siempre literales con `f` |
| `(float)(a/b)` — cast tarde | `(float)a/b` — el cast debe ir antes de dividir |
| `\n` al final del formato en `scanf` | Nunca poner `\n` en `scanf` — bloquea el programa |
| `%` sin escapar en `printf` | Usar `%%` para imprimir el símbolo `%` |
| `int main()` sin `void` | `int main(void)` — forma correcta en C moderno |
| `x++ + x++` en una expresión | Un solo `++`/`--` por expresión |
| Etiqueta `printf` no coincide con variable | Verificar siempre que etiqueta y variable coinciden |

---

## Progresión

- Separación cálculo/presentación: aplicada de forma natural desde el ejercicio 3.
- Nombres de variables: descriptivos y consistentes desde el primer intento.
- Uso de `%%` para el símbolo `%`: correcto sin necesitar recordatorio.
- Variables al inicio del bloque: corregido y mantenido desde el ejercicio 4.
- Operadores `++`/`--`: dominados tras serie de ejercicios progresivos.
- Punto de mejora: literales `double` (`9.0`) en vez de `float` (`9.0f`).
