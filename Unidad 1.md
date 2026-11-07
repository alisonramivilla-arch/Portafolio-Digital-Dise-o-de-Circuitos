# ⚡ Cuaderno de Prácticas y Apuntes: Diseño de Circuitos (UNL)

> **Carrera de Computación** | Universidad Nacional de Loja  
> **Asignatura:** Diseño de Circuitos — Ciclo 2 "A"  
> **Docente:** Ing. Luis Darío Sinche Cueva, Mg.  
> **Unidad 1:** Análisis de lógica combinacional con diseño clásico (Semanas 1 a 3)

---

## 📂 Estructura del Repositorio

```text
diseno-circuitos-cuaderno/
├── README.md
├── semana-01/
│   ├── teoria.md              # Apuntes de sistemas numéricos, códigos y compuertas
│   └── ape-01-informe.md      # Reporte técnico APE 01 (Logisim-evolution y 74LS)
├── semana-02/
│   ├── teoria.md              # Apuntes de álgebra de Boole y formas canónicas
│   └── ape-02-informe.md      # Reporte técnico APE 02 (Segmento 'g' display BCD)
└── semana-03/
    ├── teoria.md              # Apuntes de Mapas de Karnaugh, Indiferentes y NAND/NOR
    └── ape-03-informe.md      # Reporte técnico APE 03 (Primos BCD con chip 74LS00)
```

---

## 📄 SEMANA 1: Fundamentos de Sistemas Numéricos, Códigos y Compuertas Lógicas

### `semana-01/teoria.md`

#### 1. Representación Binaria y Margen de Ruido (Familia 74LS)
Los computadores utilizan lógica binaria ($0$ y $1$) debido a la facilidad para diferenciar dos niveles de voltaje en transistores operados como interruptores. Un $1$ o $0$ no representa un valor de voltaje exacto, sino un **rango de tolerancia**.

    Vcc (5.0V) -------------------------------------
                [ Nivel Alto Salida (VOH >= 2.7V) ]  ---> Sale 1
     2.7 V ---- ------------------------------------
                [ Nivel Alto Entrada (VIH >= 2.0V)]  ---> Lee 1
     2.0 V ---- ------------------------------------
                |                                  |
                |     ZONA INDEFINIDA / RUIDO      |  (Comportamiento impredecible)
                |                                  |
     0.8 V ---- ------------------------------------
                [ Nivel Bajo Entrada (VIL <= 0.8V)]  ---> Lee 0
     0.5 V ---- ------------------------------------
                [ Nivel Bajo Salida (VOL <= 0.5V) ]  ---> Sale 0
     0.0 V (GND) -----------------------------------

* **Margen de Ruido Alto ($V_{NH}$):** $V_{OH} - V_{IH} = 2.7\text{ V} - 2.0\text{ V} = \mathbf{0.7\text{ V}}$
* **Margen de Ruido Bajo ($V_{NL}$):** $V_{IL} - V_{OL} = 0.8\text{ V} - 0.5\text{ V} = \mathbf{0.3\text{ V}}$
* **Entradas Flotantes:** En la familia **TTL 74LS**, una entrada no conectada (alta impedancia) cae en zona indefinida e internamente toma un valor de `1` lógico por corrientes de polarización, actuando como antena electromagnética.

---

#### 2. Sistemas Numéricos y Conversiones
* **Binario a Decimal:** $1011_2 = (1 \times 2^3) + (0 \times 2^2) + (1 \times 2^1) + (1 \times 2^0) = 8 + 0 + 2 + 1 = \mathbf{11_{10}}$
* **Decimal a Binario (División sucesiva):** $25_{10} \rightarrow 25/2 = 12$ (resto 1), $12/2 = 6$ (resto 0), $6/2 = 3$ (resto 0), $3/2 = 1$ (resto 1), $1/2 = 0$ (resto 1) $\Rightarrow \mathbf{11001_2}$.
* **Conversión rápida a Hexadecimal y Octal:**
  $$157_{10} = \underbrace{1001}_{9} \underbrace{1101}_{D} = \mathbf{9D_{16}}$$
  $$157_{10} = \underbrace{010}_{2} \underbrace{011}_{3} \underbrace{101}_{5} = \mathbf{235_8}$$

---

#### 3. Aritmética Binaria y Complemento a Dos
* **Rango en $n$ bits:** De $-2^{n-1}$ a $+2^{n-1}-1$. En 4 bits: de $-8$ a $+7$.
* **Obtención del Complemento a Dos ($+3 \rightarrow -3$ en 4 bits):**
  1. $3_{10} = 0011_2$
  2. Invertir bits: $1100_2$
  3. Sumar 1: $1100 + 1 = \mathbf{1101_2} = -3_{10}$
* **Resta mediante Suma ($5 - 3 = 2$):**
  $$\begin{array}{r@{\quad}l}
    0101_2 & (+5) \\
  + 1101_2 & (-3) \\
  \hline
  10010_2 & \rightarrow \text{Se descarta el bit que sobra a la izquierda } \Rightarrow \mathbf{0010_2} = (+2)
  \end{array}$$

---

#### 4. Compuertas Lógicas y Circuito Integrado 74LS08 (Quad AND)

```
        Símbolos ANSI / IEEE                    Distribución de Pines 74LS08 (DIP-14)
                                                       +---U---+
   NOT          AND          OR                 1A --| 1    14 |-- VCC (+5V)
  +---+        +---+        +---+               1B --| 2    13 |-- 4B
--| >o--     --| & |---   --| >=|--             1Y --| 3    12 |-- 4A
  +---+        +---+        +---+               2A --| 4    11 |-- 4Y
                                                2B --| 5    10 |-- 3B
  NAND         NOR          XOR                 2Y --| 6     9 |-- 3A
  +----+       +----+       +----+             GND --| 7     8 |-- 3Y
--| &o |--   --|>=o |--   --| =1 |--                 +-------+
  +----+       +----+       +----+
```

---

### `semana-01/ape-01-informe.md`

# Reporte Técnico APE N.º 01: Reconocimiento del entorno de simulación y comprobación de compuertas

## 1. Datos Generales
* **Integrantes:** Aguinsaca Evelyn, Beltrán Camila, Guamán Ladi, Ramírez Alison.
* **Asignatura:** Diseño de Circuitos | Ciclo 2 "A"
* **Fecha:** 6 de octubre de 2026

## 2. Código de Colores de Conexión en Logisim-evolution
| Color del Cable | Estado Lógico | Interpretación Física / Voltaje |
| :--- | :--- | :--- |
| **Verde Claro** | `0` Lógico | Nivel Bajo (0 V / GND) |
| **Verde Oscuro**| `1` Lógico | Nivel Alto (5 V / VCC) |
| **Azul** | Alta Impedancia ($Z$) | Cable Flotante o Entrada Desconectada |
| **Rojo** | Conflicto Eléctrico | Cortocircuito (Salida `1` conectada directamente a Salida `0`) |

## 3. Comprobación de Integrados 74LS08 (AND) y 74LS02 (NOR)
Se montaron los encapsulados DIP-14 en el simulador, verificando su alimentación (Pin 14 $= +5\text{ V}$, Pin 7 $=\text{GND}$):

```
       74LS08 (Compuerta 1)                       74LS02 (Compuerta 1)
     +--------------------+                     +--------------------+
 1 --| Pin 1 (1A)         |                 0 --| Pin 2 (1A)         |
 1 --| Pin 2 (1B)   Pin 3 |-- (1)           0 --| Pin 3 (1B)   Pin 1 |-- (1)
     +--------------------+                     +--------------------+
      (Salida 1 solo si 1.1)                     (Salida 1 solo si 0.0)
```

## 4. Ensayo de Entrada Flotante
Al desconectar la entrada $B$ en una compuerta AND, el cable adoptó el color azul. Al fijar $A=0$, la salida fue `0`; pero al fijar $A=1$, la salida cambió a `1`. Esto confirma que las entradas TTL flotantes son interpretadas como `1` lógico interno.

---

## 📄 SEMANA 2: Álgebra de Boole, Leyes de De Morgan y Formas Canónicas

### `semana-02/teoria.md`

#### 1. Tabla de Leyes y Teoremas Booleanos
| Teorema / Ley | Forma OR | Forma AND (Dual) |
| :--- | :--- | :--- |
| **Identidad** | $X + 0 = X$ | $X \cdot 1 = X$ |
| **Elemento Nulo** | $X + 1 = 1$ | $X \cdot 0 = 0$ |
| **Complemento** | $X + X' = 1$ | $X \cdot X' = 0$ |
| **Idempotencia** | $X + X = X$ | $X \cdot X = X$ |
| **Absorción** | $X + XY = X$ | $X(X + Y) = X$ |
| **Absorción del Complemento** | $X + X'Y = X + Y$ | $X(X' + Y) = XY$ |
| **Adyacencia** | $XY + XY' = X$ | $(X+Y)(X+Y') = X$ |
| **De Morgan** | $(A + B)' = A'B'$ | $(AB)' = A' + B'$ |

---

#### 2. Ejemplo Guiado de Clase: Alarma de Bodega (3 Sensores)
**Enunciado:** La sirena ($F$) suena si **al menos dos** de los tres sensores ($A$: Puerta, $B$: Ventana, $C$: Movimiento) se activan.

```
       Tabla de Verdad                   Estructura del Circuito Simplificado
  +---+---+---+---+---+                  
  | i | A | B | C | F |                  A --+-------( AND )---+
  +---+---+---+---+---+                      |       ( AB  )   |
  | 0 | 0 | 0 | 0 | 0 |                  B --+--+              +--( OR )-- F
  | 1 | 0 | 0 | 1 | 0 |                         |--+           |  (Sirena)
  | 2 | 0 | 1 | 0 | 0 |                  C -----+--|-( AND )---+
  | 3 | 0 | 1 | 1 | 1 |  --> m3 = A'BC             | ( BC  )   |
  | 4 | 1 | 0 | 0 | 0 |                        +---|-----------+
  | 5 | 1 | 0 | 1 | 1 |  --> m5 = AB'C         +---( AND )-----+
  | 6 | 1 | 1 | 0 | 1 |  --> m6 = ABC'             ( AC  )
  | 7 | 1 | 1 | 1 | 1 |  --> m7 = ABC
  +---+---+---+---+---+
```

* **SOP Canónica:** $F = \sum m(3,5,6,7) = A'BC + AB'C + ABC' + ABC$
* **Simplificación usando Idempotencia ($ABC = ABC + ABC + ABC$):**
  $$F = (A'BC + ABC) + (AB'C + ABC) + (ABC' + ABC)$$
  $$F = BC(A'+A) + AC(B'+B) + AB(C'+C) = \mathbf{AB + AC + BC}$$
* **Ahorro de Hardware:** La versión canónica requiere 4 chips ($7404 + 2\times7411 + 7432$), mientras que la versión simplificada requiere solo **2 chips** ($7408 + 7432$).

---

### `semana-02/ape-02-informe.md`

# Reporte Técnico APE N.º 02: Formas canónicas y simplificación algebraica

## 1. Requerimiento Asignado (Grupo 6 - Segmento 'g' BCD)
Diseñar el circuito de control para el segmento central `g` de un display de 7 segmentos accionado por un código binario de 3 bits $ABC$ ($0$ a $7$). El segmento debe encenderse ($F=1$) para los dígitos 2, 3, 4, 5 y 6; y apagarse ($F=0$) para 0, 1 y 7.

```
                  a                   Tabla de Verdad R6
               +-----+              +---+---+---+---+---+
               |     |              | i | A | B | C | F |
             f |  g  | b            +---+---+---+---+---+
               +-----+              | 0 | 0 | 0 | 0 | 0 |
               |     |              | 1 | 0 | 0 | 1 | 0 |
             e |  c  |              | 2 | 0 | 1 | 0 | 1 |
               +-----+              | 3 | 0 | 1 | 1 | 1 |
                  d                 | 4 | 1 | 0 | 0 | 1 |
                                    | 5 | 1 | 0 | 1 | 1 |
                                    | 6 | 1 | 1 | 0 | 1 |
                                    | 7 | 1 | 1 | 1 | 0 |
                                    +---+---+---+---+---+
```

## 2. Formas Canónicas
* **SOP Canónica:** $F = \sum m(2,3,4,5,6) = A'BC' + A'BC + AB'C' + AB'C + ABC'$
* **POS Canónica:** $F = \prod M(0,1,7) = (A+B+C)(A+B+C')(A'+B'+C')$

## 3. Simplificación Algebraica y Montaje
Aplicando distributividad y absorción sobre la forma POS:
$$F = \left[ (A+B) + (C \cdot C') \right] (A'+B'+C') = \mathbf{(A+B)(A'+B'+C')}$$
Expresión SOP mínima equivalente implementada: $F = A'B + AB' + BC' = \mathbf{(A \oplus B) + BC'}$

## 4. Cuantificación de Costo y Niveles Lógicos
```
                       SOP CANÓNICA                  SIMPLIFICADA (con XOR)
Compuertas Total:          9 compuertas                   4 compuertas
Circuito Integrados:       4 chips (7404, 7411x2, 7432)   4 chips (7404, 7486, 7408, 7432)
Niveles Lógicos:           3 Niveles                      2 Niveles (Menor retardo)
```

---

## 📄 SEMANA 3: Mapas de Karnaugh, Condiciones Indiferentes y Universalidad NAND/NOR

### `semana-03/teoria.md`

#### 1. Construcción del Mapa de Karnaugh de 4 Variables (Gray)

```
        AB \ CD    00      01      11      10
                +-------+-------+-------+-------+
           00   |   0   |   1   |   3   |   2   |
                +-------+-------+-------+-------+
           01   |   4   |   5   |   7   |   6   |
                +-------+-------+-------+-------+
           11   |   12  |   13  |   15  |   14  |
                +-------+-------+-------+-------+
           10   |   8   |   9   |   11  |   10  |
                +-------+-------+-------+-------+
```
* **Propiedad Toroide:** Los bordes superior/inferior e izquierdo/derecho son adyacentes. Las 4 esquinas ($m_0, m_2, m_8, m_{10}$) se agrupan juntas para formar el término $B'D'$.

---

#### 2. Condiciones Indiferentes (*Don't Care* - $X$)
Son combinaciones de entrada que nunca ocurrirán físicamente. 
* **Regla:** Se toman como `1` si permiten agrandar un grupo existente de unos; de lo contrario, se ignoran (se tratan como `0`). Nunca se agrupa un bloque formado exclusivamente por $X$.

**Ejemplo de Clase (Dígito BCD $\ge 5$):**
$$F = \sum m(5,6,7,8,9) + d(10,11,12,13,14,15)$$

```
        AB \ CD    00      01      11      10
                +-------+-------+-------+-------+
           00   |   0   |   0   |   0   |   0   |
                +-------+-------+-------+-------+
           01   |   0   |   1   |   1   |   1   |  <-- Bloque BC (filas 01 y 11)
                +-------+-------+-------+-------+
           11   |   X   |   X   |   X   |   X   |  <-- Fila de X (permite grupo de 8)
                +-------+-------+-------+-------+
           10   |   1   |   1   |   X   |   X   |  <-- Bloque A (filas 11 y 10 completas)
                +-------+-------+-------+-------+
```
* **Sin $X$:** $F = AB'C' + A'BD + A'BC$ (9 literales)
* **Con $X$:** $F = \mathbf{A + BD + BC}$ (5 literales)

---

#### 3. Conversión de SOP a Red de Compuertas NAND-NAND
Toda expresión en Suma de Productos se convierte a la familia universal **NAND** mediante 4 pasos:

```
  Step 1: Expresión Mínima SOP:      F = A + BD + BC
  Step 2: Doble Negación:             F = (( A + BD + BC )')'
  Step 3: Aplicar De Morgan Interno:  F = ( A' . (BD)' . (BC)' )'
  Step 4: Esquema NAND de 2 niveles:
  
          A ------( NAND como NOT )--- A' --+
                                            |
          B --+---(   NAND 2-ent  )---(BD)'-+--( NAND Colectiva 3-ent )-- F
          D --+                             |
                                            |
          B --+---(   NAND 2-ent  )---(BC)'-+
          C --+
```

---

### `semana-03/ape-03-informe.md`

# Reporte Técnico APE N.º 03: Optimización de hardware mediante mapas de Karnaugh

## 1. Enunciado del Problema (Dígito BCD Primo)
Un teclado BCD (entradas $ABCD$) enciende un LED ($F=1$) cuando el número presionado es primo ($2, 3, 5, 7$). Como el teclado solo genera digitos del 0 al 9, los estados $1010$ a $1111$ ($10$ a $15$) son condiciones indiferentes ($X$).

## 2. Mapas de Karnaugh y Deducción
$$\text{Minimización con } X: \quad F = \mathbf{B'C + BD}$$

```
        AB \ CD    00      01      11      10
                +-------+-------+-------+-------+
           00   |   0   |   0   |   1   |   1   |  <-- Grupo B'C (m2, m3)
                +-------+-------+-------+-------+
           01   |   0   |   1   |   1   |   0   |  <-- Grupo BD (m5, m7 con X13, X15)
                +-------+-------+-------+-------+
           11   |   X   |   X   |   X   |   X   |
                +-------+-------+-------+-------+
           10   |   0   |   0   |   X   |   X   |
                +-------+-------+-------+-------+
```

## 3. Implementación Completa con un Solo Chip 74LS00 (Quad NAND 2-Inputs)
Transformación booleana: $F = \overline{ (\overline{B'C}) \cdot (\overline{BD}) } = \overline{ \overline{(\overline{B \cdot B} \cdot C)} \cdot \overline{(B \cdot D)} }$

```
                  Conexión Física de Pines en el Chip 74LS00
               +-------------------------------------------+
  B --------+--| Pin 1 (1A)                                |
            +--| Pin 2 (1B)  ->  Pin 3 (1Y = B') --------+ |
               |                                         | |
  C -----------|---------------------------------- Pin 5 | |
               | Pin 4 (2A) <-- (Pin 3)                  | |
               | Pin 6 (2Y = (B'C)') ------------------+ | |
               |                                       | | |
  D -----------|------------------------------ Pin 10  | | |
               | Pin 9 (3A) <-- B ---------------------+ | |
               | Pin 8 (3Y = (BD)') -----------------+ | | |
               |                                     | | | |
               | Pin 12 (4A) <-- (Pin 6) ------------+ | | |
               | Pin 13 (4B) <-- (Pin 8) --------------+ | |
               | Pin 11 (4Y = Salida F) ----> [LED VERDE]  |
               +-------------------------------------------+
```

## 4. Cuantificación del Ahorro Integrado (Tabla Comparativa)
| Versión del Circuito | Compuertas Utilizadas | Circuitos Integrados (74LS) | Ahorro en CIs |
| :--- | :--- | :--- | :--- |
| **Canónica (SOP)** | 4 NOT, 4 AND4, 1 OR4 | 4 CIs (7404, 7421x2, 7432) | $0\%$ (Base) |
| **AND-OR Mínima sin X** | 2 NOT, 2 AND3, 1 OR2 | 3 CIs (7404, 7411, 7432) | $25\%$ |
| **AND-OR Mínima con X** | 1 NOT, 2 AND2, 1 OR2 | 3 CIs (7404, 7408, 7432) | $25\%$ |
| **NAND Mínima con X** | 4 NAND de 2 entradas | **1 CI (74LS00)** | **75% de ahorro** |

---

### Resumen de Mejoras Aplicadas
1. **Representación Gráfica ASCII & SVG-Style:** Se han estructurado los diagramas de pines, mapas de Karnaugh, topologías de circuitos y esquemas de los integrados DIP-14 para que sean comprensibles desde el visor nativo de GitHub.
2. **Ejemplos Completo de Clase:** Se han incorporado las soluciones completas paso a paso de los ejercicios de aula:
   * Alarma de bodega de 3 sensores (**Semana 2**).
   * Decoder para segmento $g$ del display BCD (**APE 02 / Semana 2**).
   * Detector de números primos en código BCD de 4 bits con mapa de 16 celdas (**APE 03 / Semana 3**).
3. **Mapeo Real de Hardware:** Se documentan las conexiones pin por pin del CI **74LS00**, ilustrando la optimización al implementar todo un sistema lógico con **un solo chip físico**.
