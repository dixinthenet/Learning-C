# 🧠 C — CHEAT SHEET PERSONAL
*Bloques 1–4 · Referencia personal*

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

> ⚠️ División entera: `int/int` trunca el resultado. Usa `7.0/2` para obtener `3.5` en vez de `3`.

> ✅ Usa `const` en lugar de `#define` para definir constantes con tipo: `const float PI = 3.14159f;`

> ⚠️ `const` y `scanf` no se llevan bien — no puedes leer en una variable `const`. Usa una variable separada.

**`const char *` — puntero a string de solo lectura:**
```c
const char *mensaje  = "Hola";      // ✅ string literal — siempre con const
const char *resultado = (x > 0) ? "Positivo" : "Negativo";  // ✅ ternario

mensaje = "Adios";      // ✅ puede redirigir el puntero
mensaje[0] = 'h';       // ❌ error — no puedes modificar el texto
char *mensaje = "Hola"; // ⚠️ sin const — el compilador puede avisar
```

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
| `%02d` | `int` | Ancho 2, relleno con ceros: `5` → `05` |
| `%.2f` | `double` | Dos decimales: `3.14159` → `3.14` |

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
| `/` | División real | `7.0 / 2` | `3.5` ✅ |
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

**Short-circuit evaluation:**
```c
true  || cualquier_cosa   // → siempre true, el segundo se ignora
false && cualquier_cosa   // → siempre false, el segundo se ignora
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

**Truco para `~a`:**
```c
~a = -(a + 1)   // ~12 = -13 · ~0 = -1 · ~1 = -2
```

**Truco XOR — intercambiar sin variable auxiliar:**
```c
a = a ^ b;
b = a ^ b;
a = a ^ b;
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
| 8 | `&` | Izquierda → derecha |
| 9 | `^` | Izquierda → derecha |
| 10 | `\|` | Izquierda → derecha |
| 11 | `&&` | Izquierda → derecha |
| 12 | `\|\|` | Izquierda → derecha |
| 13 | `?:` | Derecha → izquierda |
| 14 | `=` `+=` `-=` `*=` `/=` `%=` | Derecha → izquierda |
| 15 (menor) | `,` | Izquierda → derecha |

---

## 6. Operador ternario `?:`

```c
condicion ? valor_si_true : valor_si_false

char letra = (nota >= 90) ? 'A' :
             (nota >= 80) ? 'B' :
             (nota >= 70) ? 'C' :
             (nota >= 60) ? 'D' : 'F';

printf("Resultado: %s\n", nota >= 5.0f ? "Aprobado" : "Suspenso");
```

---

## 7. printf y scanf en detalle

### 7.1 printf — modificadores de formato

| Modificador | Efecto | Ejemplo | Salida |
|-------------|--------|---------|--------|
| `%5d` | Ancho mínimo 5 (alineado derecha) | `printf("%5d", 42)` | `   42` |
| `%-5d` | Alineado izquierda | `printf("%-5d\|", 42)` | `42   \|` |
| `%05d` | Relleno con ceros | `printf("%05d", 42)` | `00042` |
| `%02d` | Ancho 2, relleno ceros | `printf("%02d", 5)` | `05` |
| `%+d` | Muestra signo siempre | `printf("%+d", 42)` | `+42` |
| `%.2f` | 2 decimales | `printf("%.2f", 3.14159)` | `3.14` |
| `%8.2f` | Ancho 8, 2 decimales | `printf("%8.2f", 3.14)` | `    3.14` |

**Secuencias de escape:**

| Escape | Significado |
|--------|-------------|
| `\n` | Nueva línea |
| `\t` | Tabulador |
| `\\` | Barra invertida `\` |
| `\"` | Comilla doble `"` |
| `\0` | Carácter nulo (fin de cadena) |

### 7.2 scanf — resumen

```c
scanf("%d", &edad);      // int — & obligatorio
scanf("%lf", &pi);       // double — %lf obligatorio
scanf(" %c", &letra);    // char — espacio antes limpia buffer
scanf("%49s", nombre);   // string — sin &, limita longitud
```

**Limpiar buffer cuando falla `scanf`:**
```c
if (scanf("%d", &n) != 1) {
    while (getchar() != '\n');  // vacía el buffer
    n = 0;
}
```
> ⚠️ Pendiente de profundizar — importante para validación robusta.

---

## 8. Control de flujo — `if` / `else if` / `else`

```c
if (condición_1) {
    // rama 1
} else if (condición_2) {
    // rama 2
} else {
    // ninguna de las anteriores
}
```

### Reglas clave

**En cuanto una condición es verdadera, se saltan todas las demás.**

**Rangos — el orden importa (de mayor a menor):**
```c
// ✅ correcto
if (nota >= 90)       { printf("Sobresaliente\n"); }
else if (nota >= 70)  { printf("Notable\n"); }
else if (nota >= 50)  { printf("Aprobado\n"); }
else                  { printf("Suspenso\n"); }

// ❌ incorrecto — >= 50 captura todo antes que >= 70
if (nota >= 50) { ... }
else if (nota >= 70) { ... }   // nunca se alcanza
```

**Validación primero — early return:**
```c
if (valor < 0 || valor > 100) {
    printf("Error\n");
    return 1;
}
// código principal sin anidar
```

**`if` sin llaves — trampa crítica:**
```c
// ❌
if (x > 0)
    printf("positivo\n");
    printf("esto SIEMPRE se ejecuta\n");  // NO forma parte del if

// ✅ siempre llaves
if (x > 0) {
    printf("positivo\n");
}
```
> ⚠️ Un `if` sin llaves **solo afecta a la línea inmediatamente siguiente**.

**Modificar variables dentro de `if`:**
```c
int es_primo = 1;   // valor por defecto

if (numero % i == 0) {
    es_primo = 0;   // ✅ puedes cambiar el valor desde cualquier bloque
    break;
}
```

**Comparar floats — no usar `==`:**
```c
// ❌ puede fallar por redondeo
if (f == 0.3f) { ... }

// ✅ comparar con tolerancia
if (f - 0.3f < 1e-6f && 0.3f - f < 1e-6f) { ... }
```

---

## 9. Control de flujo — `switch`

```c
switch (expresión) {
    case valor1:
        // código
        break;
    case valor2:
        // código
        break;
    default:
        // si ningún case coincide
        break;
}
```

### Reglas clave

**`break` es obligatorio** — sin él el código cae al siguiente `case` (*fallthrough*).

**Solo funciona con enteros y `char`** — no con `double` ni cadenas.

**Variables dentro de `case` — necesitan llaves:**
```c
case 1: {
    int temp = 42;   // ✅
    break;
}
```

**Fallthrough intencional — agrupar casos que hacen lo mismo:**
```c
case 'a':
case 'A':
case 'e':
case 'E':
    printf("vocal\n");
    break;
```

**`default` — incluirlo siempre:**
```c
default:
    printf("Error: opcion no valida\n");
    break;
```

### `if` vs `switch`

| Situación | Usa |
|-----------|-----|
| Valores exactos, menús | `switch` |
| Rangos (`x > 10`, `x <= 5`) | `if` |
| Condiciones con `&&`, `\|\|` | `if` |
| Comparar cadenas | `if` + `strcmp` |

---

## 10. Control de flujo — Bucles

### `while`
```c
while (condición) {
    // se repite mientras condición sea verdadera
    // si es falsa desde el principio, nunca entra
}
```

### `do while`
```c
do {
    // se ejecuta al menos una vez
    // la condición se evalúa AL FINAL
} while (condición);
```

**Uso típico — validar entrada:**
```c
do {
    printf("Introduce un numero (1-100): ");
    scanf("%d", &numero);
    if (numero < 1 || numero > 100)
        printf("Error, intentalo de nuevo\n");
} while (numero < 1 || numero > 100);
```

### `for`
```c
for (inicialización; condición; actualización) {
    // cuerpo
}

for (int i = 0; i < 10; i++) {
    printf("%d\n", i);
}
```

**Variables declaradas en el `for` — ámbito limitado al bloque:**
```c
for (int i = 0; i < 10; i++) {
    int doble = i * 2;   // existe solo dentro de esta iteración
}
// i y doble ya no existen aquí
```

**Equivalencia `for` ↔ `while`:**
```c
for (int i = 0; i < 5; i++) { printf("%d\n", i); }

int i = 0;
while (i < 5) { printf("%d\n", i); i++; }
```

### ¿Cuál usar?

```
¿Sabes cuántas veces se repite?
   SÍ → for
   NO → ¿necesita ejecutarse al menos una vez?
           SÍ → do while
           NO → while
```

### `break` y `continue`

```c
break;      // sale del bucle inmediatamente
continue;   // salta al siguiente ciclo, ignora el resto del cuerpo
```

```c
for (int i = 0; i < 10; i++) {
    if (i == 5) break;
    if (i % 2 == 0) continue;
    printf("%d\n", i);   // imprime: 1 3
}
```

### Bucle infinito
```c
while (1) {
    // se repite hasta que haya un break
}
```

---

## 11. Cadenas — `strcmp`

```c
#include <string.h>

strcmp(cadena1, cadena2);
// devuelve 0 si son iguales, distinto de 0 si no
```

```c
// ❌ == compara direcciones de memoria, no contenido
if (nombre == "admin") { ... }

// ✅ strcmp compara carácter a carácter
if (strcmp(nombre, "admin") == 0) { ... }
```

---

## 12. `char` y ASCII

Los `char` son internamente números (tabla ASCII):
```
'A' = 65 ... 'Z' = 90
'a' = 97 ... 'z' = 122
'0' = 48 ... '9' = 57
```

```c
// Detectar rango de letras con comparación numérica
if ((letra >= 'a' && letra <= 'z') || (letra >= 'A' && letra <= 'Z'))
    printf("es una letra\n");
```

---

## 13. Números aleatorios

```c
#include <stdlib.h>
#include <time.h>

srand(time(NULL));              // semilla — llamar solo una vez
int n = rand() % 100 + 1;      // número entre 1 y 100
```

---

## 14. Patrones frecuentes

**Acumulador:**
```c
int suma = 0;
while (...) { suma += numero; }
```

**Acumulador multiplicativo (factorial, potencia):**
```c
int resultado = 1;
while (...) { resultado *= base; }
```

**Variable de estado (primo, perfecto...):**
```c
int es_primo = 1;   // asume verdadero
for (int i = 2; i < numero; i++) {
    if (numero % i == 0) { es_primo = 0; break; }
}
if (es_primo) { printf("es primo\n"); }
```

**Early return — validar y salir:**
```c
if (entrada_invalida) {
    printf("Error\n");
    return 1;
}
// código principal sin anidar
```

---

## 15. Sistema binario

### Decimal → Binario
```
13 ÷ 2 = 6  resto 1
 6 ÷ 2 = 3  resto 0
 3 ÷ 2 = 1  resto 1
 1 ÷ 2 = 0  resto 1
             ↑ leer de abajo a arriba → 1101 = 13
```

### Binario → Decimal
```
1  1  0  1
↑  ↑  ↑  ↑
8  4  2  1   →   8 + 4 + 0 + 1 = 13
```

### Potencias de 2
```
2⁰=1 · 2¹=2 · 2²=4 · 2³=8 · 2⁴=16 · 2⁵=32 · 2⁶=64 · 2⁷=128
```

---

## 16. Operadores bit a bit — usos prácticos

```c
estado = estado | 0b0100;    // activar bit 2
estado = estado & ~0b0100;   // desactivar bit 2
estado = estado ^ 0b0100;    // alternar bit 2
if (estado & 0b0100) { ... } // comprobar bit 2

int x = 4;
x = x << 1;   // x = 8  (× 2)
x = x >> 1;   // x = 4  (÷ 2)
```

**Sistema de permisos:**
```c
#define LEER     0b100
#define ESCRIBIR 0b010
#define EJECUTAR 0b001

int permisos = LEER | ESCRIBIR;
if (permisos & LEER) { ... }
permisos = permisos & ~ESCRIBIR;
```

---

## 17. Errores comunes

| Error | Incorrecto | Correcto |
|-------|------------|----------|
| División entera | `float r = 9/5;` → `1` | `float r = 9.0/5.0;` → `1.8` |
| `=` en vez de `==` | `if (x = 5)` | `if (x == 5)` |
| `if` sin llaves | Solo afecta línea siguiente | Siempre usar `{}` |
| `\n` en `scanf` | `scanf("%f\n", &x)` | `scanf("%f", &x)` |
| `break` en `switch` | Fallthrough no deseado | Añadir `break` en cada `case` |
| Variable sin inicializar | `while (n != 0)` sin init | Inicializar antes |
| `scanf` en `const` | `const int n; scanf("%d", &n)` | Variable separada |
| Comparar float con `==` | `if (f == 0.3f)` | Comparar con tolerancia |
| `scanf` double | `scanf("%f", &d)` | `scanf("%lf", &d)` |
| `int main()` | `int main()` | `int main(void)` |

---

*Programación en C — Bloques 1–4 · Referencia personal*
