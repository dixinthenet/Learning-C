# Chuleta de C
**Bloques 1, 2 y 3 — Referencia rápida**

---

## 1. Estructura básica de un programa C

```c
#include <stdio.h>

int main(void) {
    printf("Hola, mundo!\n");
    return 0;
}
```

Compilación recomendada:
```bash
gcc -Wall -Wextra -std=c11 -g programa.c -o programa
```

---

## 2. Tipos de datos fundamentales

| Tipo | Descripción | Ejemplo |
|------|-------------|---------|
| `int` | Número entero | `int edad = 25;` |
| `char` | Carácter / entero pequeño | `char letra = 'A';` |
| `float` | Punto flotante simple (32-bit) | `float precio = 3.14f;` |
| `double` | Punto flotante doble (64-bit) | `double pi = 3.14159265358979;` |
| `void` | Ausencia de tipo | `void funcion(void) { ... }` |
| `long` | Entero largo | `long poblacion = 8000000000L;` |
| `unsigned int` | Entero sin signo (≥ 0) | `unsigned int cont = 0;` |

> ⚠️ División entera: `int/int` trunca el resultado. Usa `7.0f/2` para obtener `3.5` en vez de `3`.

> ✅ Usa `const` en lugar de `#define` para definir constantes con tipo: `const float PI = 3.14159f;`

---

## 3. Especificadores de formato (printf / scanf)

| Especificador | Tipo | Notas |
|---------------|------|-------|
| `%d` / `%i` | `int` | Entero decimal con signo |
| `%u` | `unsigned int` | Entero sin signo |
| `%f` | `float` / `double` | En `printf` sirve para ambos |
| `%lf` | `double` | Obligatorio en `scanf` para double |
| `%e` / `%E` | `float` / `double` | Notación científica |
| `%c` | `char` | Usar espacio antes en scanf: `" %c"` |
| `%s` | `char[]` | Cadena. Usar `%49s` para limitar a 49 chars |
| `%o` | `int` | Octal |
| `%x` / `%X` | `int` | Hexadecimal (minúsculas / mayúsculas) |
| `%ld` | `long int` | Entero largo |
| `%lld` | `long long int` | Entero muy largo |
| `%%` | — | Imprime el símbolo `%` literal |

> ⚠️ `scanf` con `%c` después de `%d`: añade un espacio antes → `scanf(" %c", &letra)` para limpiar el `\n` del buffer.

---

## 4. Operadores

### 4.1 Aritméticos

| Op. | Operación | Ejemplo | Resultado |
|-----|-----------|---------|-----------|
| `+` | Suma | `5 + 3` | `8` |
| `-` | Resta | `5 - 3` | `2` |
| `*` | Multiplicación | `5 * 3` | `15` |
| `/` | División entera | `7 / 2` | `3` ⚠️ |
| `/` | División real | `7.0f / 2` | `3.5` ✅ |
| `%` | Módulo (resto) | `7 % 2` | `1` |

### 4.2 Relacionales

| Op. | Significado | Ejemplo (a=5, b=3) | Resultado |
|-----|-------------|---------------------|-----------|
| `==` | Igual a | `a == b` | `0` (falso) |
| `!=` | Distinto de | `a != b` | `1` (verdadero) |
| `>` | Mayor que | `a > b` | `1` (verdadero) |
| `<` | Menor que | `a < b` | `0` (falso) |
| `>=` | Mayor o igual | `a >= 5` | `1` (verdadero) |
| `<=` | Menor o igual | `a <= 2` | `0` (falso) |

### 4.3 Lógicos

| Op. | Nombre | Descripción | Ejemplo |
|-----|--------|-------------|---------|
| `&&` | AND | Verdadero si AMBOS son verdaderos | `(a>0 && b>0)` |
| `\|\|` | OR | Verdadero si AL MENOS UNO es verdadero | `(a>0 \|\| b>0)` |
| `!` | NOT | Invierte el valor lógico | `!(a > b)` |

**En C: `0 = FALSO`, cualquier otro valor = `VERDADERO`**

```c
!(4 > 3)   // 4>3 es verdadero → 1, luego !1 → 0
```

### 4.4 Asignación compuesta

| Op. | Equivalente a | Ejemplo (x=10) |
|-----|---------------|----------------|
| `x += 3` | `x = x + 3` | x vale `13` |
| `x -= 3` | `x = x - 3` | x vale `7` |
| `x *= 3` | `x = x * 3` | x vale `30` |
| `x /= 3` | `x = x / 3` | x vale `3` |
| `x %= 3` | `x = x % 3` | x vale `1` |

### 4.5 Incremento y decremento

| Op. | Nombre | Comportamiento | Ejemplo (i=5) |
|-----|--------|----------------|---------------|
| `i++` | Post-incremento | Usa i (5), luego suma 1 → i=6 | `j = i++;` → j=5, i=6 |
| `++i` | Pre-incremento | Suma 1 primero → i=6, luego usa i | `j = ++i;` → j=6, i=6 |
| `i--` | Post-decremento | Usa i (5), luego resta 1 → i=4 | `j = i--;` → j=5, i=4 |
| `--i` | Pre-decremento | Resta 1 primero → i=4, luego usa i | `j = --i;` → j=4, i=4 |

> ⚠️ Nunca uses dos `++`/`--` sobre la misma variable en la misma expresión — comportamiento indefinido.

### 4.6 Operadores a nivel de bits (bitwise)

| Op. | Nombre | Descripción |
|-----|--------|-------------|
| `&` | AND bit a bit | 1 solo si AMBOS bits son 1 |
| `\|` | OR bit a bit | 1 si AL MENOS UN bit es 1 |
| `^` | XOR bit a bit | 1 si los bits son DISTINTOS |
| `~` | NOT bit a bit | Invierte todos los bits |
| `<<` | Desplazamiento izquierda | Multiplica por 2^n |
| `>>` | Desplazamiento derecha | Divide por 2^n |

**Tabla XOR:**

| A | B | A ^ B |
|---|---|-------|
| 0 | 0 | 0 |
| 0 | 1 | 1 |
| 1 | 0 | 1 |
| 1 | 1 | 0 |

Propiedades clave:
```c
A ^ A = 0   // consigo mismo → siempre cero
A ^ 0 = A   // con cero → no cambia
```

**Truco XOR — intercambiar dos variables sin variable temporal:**
```c
int a = 3, b = 4;
a = a ^ b;   // a = a XOR b
b = a ^ b;   // b = valor original de a
a = a ^ b;   // a = valor original de b
```

---

## 5. Precedencia de operadores (mayor → menor)

| Prioridad | Operadores | Asociatividad |
|-----------|------------|---------------|
| 1 (mayor) | `()` `[]` `->` `.` | Izquierda → derecha |
| 2 | `!` `~` `++` `--` `+(unario)` `-(unario)` | Derecha → izquierda |
| 3 | `*` `/` `%` | Izquierda → derecha |
| 4 | `+` `-` | Izquierda → derecha |
| 5 | `<<` `>>` | Izquierda → derecha |
| 6 | `<` `<=` `>` `>=` | Izquierda → derecha |
| 7 | `==` `!=` | Izquierda → derecha |
| 8 | `&` (bitwise AND) | Izquierda → derecha |
| 9 | `^` (bitwise XOR) | Izquierda → derecha |
| 10 | `\|` (bitwise OR) | Izquierda → derecha |
| 11 | `&&` (AND lógico) | Izquierda → derecha |
| 12 | `\|\|` (OR lógico) | Izquierda → derecha |
| 13 | `?:` (ternario) | Derecha → izquierda |
| 14 | `=` `+=` `-=` `*=` `/=` `%=` | Derecha → izquierda |
| 15 (menor) | `,` | Izquierda → derecha |

> ✅ Cuando dos operadores tienen la misma precedencia (como `*` y `/`), la asociatividad decide: de izquierda a derecha.

---

## 6. Operador ternario `?:`

Alternativa compacta a `if/else`. Sintaxis:
```c
condicion ? valor_si_true : valor_si_false
```

Ejemplo — convertir nota numérica a letra:
```c
char letra = (nota >= 90) ? 'A' :
             (nota >= 80) ? 'B' :
             (nota >= 70) ? 'C' :
             (nota >= 60) ? 'D' : 'F';
```

Uso directo en `printf`:
```c
printf("Resultado: %s\n", nota >= 5.0f ? "Aprobado" : "Suspenso");
```

> ⚠️ El ternario anidado puede dificultar la lectura. Úsalo con moderación.

---

## 7. printf y scanf en detalle

### 7.1 printf — salida formateada

Sintaxis: `printf("formato", arg1, arg2, ...);`

| Modificador | Efecto | Ejemplo | Salida |
|-------------|--------|---------|--------|
| `%d` | Entero básico | `printf("%d", 42)` | `42` |
| `%5d` | Ancho mínimo 5 (alineado derecha) | `printf("%5d", 42)` | `   42` |
| `%-5d` | Alineado izquierda | `printf("%-5d\|", 42)` | `42   \|` |
| `%05d` | Relleno con ceros | `printf("%05d", 42)` | `00042` |
| `%+d` | Muestra signo siempre | `printf("%+d", 42)` | `+42` |
| `%.2f` | 2 decimales | `printf("%.2f", 3.14159)` | `3.14` |
| `%8.2f` | Ancho 8, 2 decimales | `printf("%8.2f", 3.14)` | `    3.14` |
| `%e` | Notación científica | `printf("%e", 12345.6)` | `1.234560e+04` |
| `%s` | Cadena de texto | `printf("%s", "Hola")` | `Hola` |
| `%10s` | Cadena alineada derecha | `printf("%10s", "Hola")` | `      Hola` |
| `%-10s` | Cadena alineada izquierda | `printf("%-10s\|", "Hola")` | `Hola      \|` |
| `%%` | Imprime `%` literal | `printf("100%%")` | `100%` |

**Secuencias de escape más usadas:**

| Escape | Significado |
|--------|-------------|
| `\n` | Nueva línea |
| `\t` | Tabulador horizontal |
| `\\` | Barra invertida literal `\` |
| `\"` | Comilla doble literal `"` |
| `\0` | Carácter nulo (fin de cadena) |

### 7.2 scanf — entrada formateada

Sintaxis: `scanf("formato", &var1, &var2, ...);` → **SIEMPRE `&` salvo arrays/strings**

| Uso | Código | Notas |
|-----|--------|-------|
| Leer `int` | `scanf("%d", &edad);` | El `&` es obligatorio |
| Leer `float` | `scanf("%f", &precio);` | Solo `%f` para float en scanf |
| Leer `double` | `scanf("%lf", &pi);` | `%lf` obligatorio para double |
| Leer `char` | `scanf(" %c", &letra);` | Espacio antes de `%c` — limpia buffer |
| Leer string | `scanf("%49s", nombre);` | Sin `&` en arrays. Limita a 49 chars |
| Leer dos valores | `scanf("%d %d", &a, &b);` | El espacio acepta cualquier separador |
| Leer con formato fijo | `scanf("%d/%d/%d", &d, &m, &y);` | Espera exactamente `12/05/2025` |

> ⚠️ `scanf` NO pone el `&` con arrays de char: `scanf("%49s", nombre)` → `nombre` ya ES una dirección.

> ✅ El valor devuelto por `scanf` indica cuántas variables se leyeron correctamente:
> ```c
> if (scanf("%d", &n) != 1) { /* error de lectura */ }
> ```

**Problema clásico — mezclar `%d` y `%c`:**
```c
int n; char c;
scanf("%d", &n);    // el \n queda en el buffer
scanf(" %c", &c);  // ✅ espacio antes consume el \n
```

**Leer línea completa con espacios → usa `fgets` en vez de `scanf`:**
```c
char nombre[50];
fgets(nombre, sizeof(nombre), stdin);  // incluye \n al final
```

---

## 8. Errores clásicos a evitar

| Error | Incorrecto | Correcto |
|-------|------------|----------|
| División entera | `float r = 9/5;` → `1` | `float r = 9.0f/5.0f;` → `1.8` |
| `scanf %c` tras `%d` | `scanf("%d%c", &n, &c)` | `scanf("%d %c", &n, &c)` |
| String sin límite | `scanf("%s", nombre)` | `scanf("%49s", nombre)` |
| `scanf` double | `scanf("%f", &d)` | `scanf("%lf", &d)` |
| Confundir `=` y `==` | `if (x = 5) { ... }` | `if (x == 5) { ... }` |
| Usar `#define` | `#define PI 3.14` | `const float PI = 3.14f;` |
| Nombre de variable vago | `float x = 100.0f;` | `float precio_base = 100.0f;` |
| Cast tarde | `(float)(a / b)` | `(float)a / b` |
| `int main()` sin void | `int main()` | `int main(void)` |
| `\n` en scanf | `scanf("%f\n", &x)` | `scanf("%f", &x)` |

---

*Programación en C — Bloques 1, 2, 3 · Referencia personal*
