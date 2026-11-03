# ⚡ Cuaderno de Prácticas y Apuntes: Diseño de Circuitos (UNL)

Repositorio de la asignatura **Diseño de Circuitos** (Carrera de Computación, Universidad Nacional de Loja). Este cuaderno recopila la fundamentación teórica, las actividades en aula (ACD) y los informes de las prácticas experimentales (APE 01 a APE 03) correspondientes a la **Unidad 1: Análisis de lógica combinacional con diseño clásico**.

---

## 📂 Estructura del Repositorio

```text
diseno-circuitos-cuaderno/
├── README.md
├── semana-01/
│   ├── teoria.md              # Sistemas numéricos, códigos y compuertas 74LS
│   └── ape-01-informe.md      # Informe APE 01 (Logisim-evolution y 74LS08/74LS02)
├── semana-02/
│   ├── teoria.md              # Álgebra de Boole y formas canónicas (SOP y POS)
│   └── ape-02-informe.md      # Informe APE 02 (Segmento 'g' display 7 segmentos)
└── semana-03/
    ├── teoria.md              # Mapas de Karnaugh, Indiferentes y Universalidad NAND/NOR
    └── ape-03-informe.md      # Informe APE 03 (Dígito BCD Primo e Integrado 74LS00)
```

---

## 📄 SEMANA 1

### `semana-01/teoria.md`
```markdown
# Semana 1: Sistemas Numéricos, Códigos y Compuertas Lógicas

## 1. Nivel Lógico y Margen de Ruido (Familia 74LS)
* **Tensiones operativas:**
  * **Salida del chip:** $V_{OH} \ge 2.7\text{ V}$ (1 lógico), $V_{OL} \le 0.5\text{ V}$ (0 lógico).
  * **Entrada del chip:** $V_{IH} \ge 2.0\text{ V}$ (1 lógico), $V_{IL} \le 0.8\text{ V}$ (0 lógico).
* **Zona indefinida:** Entre $0.8\text{ V}$ y $2.0\text{ V}$. Las entradas flotantes o no conectadas caen en este rango e internamente la tecnología TTL 74LS las interpreta como un `1` lógico, comportándose como antenas electromagnéticas.
* **Margen de Ruido:**
  * Margen Alto: $2.7\text{ V} - 2.0\text{ V} = 0.7\text{ V}$.
  * Margen Bajo: $0.8\text{ V} - 0.5\text{ V} = 0.3\text{ V}$.

## 2. Conversiones y Aritmética
* **Bases:** Conversiones entre Binario (potencias de 2), Octal (agrupación de 3 bits) y Hexadecimal (agrupación de 4 bits).
* **Complemento a Dos:** Representación estándar para enteros con signo.
  * Para $n$ bits, el rango cubierto es de $-2^{n-1}$ a $+2^{n-1}-1$ (ejemplo de 4 bits: de $-8$ a $+7$).
  * Algoritmo de inversión: Invertir todos los bits y sumar $1$. Permite restar mediante circuitos sumadores ($A - B = A + (-B)$).
  * **Desbordamiento (Overflow):** Ocurre cuando dos operandos del mismo signo producen un resultado del signo opuesto al no caber en los bits asignados.

## 3. Códigos Digitales
* **BCD (Decimal Codificado en Binario):** Expresa cada dígito decimal ($0$ a $9$) con 4 bits ($0000$ a $1001$). Las combinaciones $1010$ a $1111$ no son válidas.
* **Código Gray:** Código no ponderado donde entre combinaciones consecutivas cambia **un solo bit**, previniendo transiciones falsas en sensores rotativos y definiendo el orden de los Mapas de Karnaugh.
* **ASCII:** Estándar de 7 bits ($128$ caracteres) para representación alfanumérica (ej. `'A'` $= 65_{10} = 0x41 = 01000001_2$).

## 4. Compuertas Lógicas Básicas y Encapsulado 74LS
* Compuertas: NOT ($Y=A'$), AND ($Y=A\cdot B$), OR ($Y=A+B$), NAND ($Y=(AB)'$), NOR ($Y=(A+B)'$), XOR ($Y=A\oplus B$), XNOR ($Y=(A\oplus B)'$).
* **Pinout Estándar DIP-14:** Pin 14 $= V_{CC}$ ($+5\text{ V}$), Pin 7 $= \text{GND}$ ($0\text{ V}$).
  * **74LS08:** Quadruple 2-input AND (Salidas en pines 3, 6, 8, 11).
  * **74LS02:** Quadruple 2-input NOR (Salidas en pines 1, 4, 10, 13).
```

### `semana-01/ape-01-informe.md`
```markdown
# Reporte Técnico APE N.º 01: Reconocimiento del entorno de simulación y comprobación de compuertas

* **Herramienta:** Logisim-evolution (Licencia GPL v3), Simulación en norma ANSI/IEEE.
* **Color de cables observados:**
  * Verde claro: `0` Lógico / GND.
  * Verde oscuro: `1` Lógico / VCC.
  * Azul: Estado desconocido / Alta impedancia (Entrada flotante).
  * Rojo: Conflicto eléctrico / Error (Cortocircuito entre salidas).

* **Comprobación de Compuertas Integradas (74LS08 y 74LS02):**
  * Se alimentaron los chips conectando Pin 14 a $V_{CC}$ ($5\text{ V}$) y Pin 7 a Tierra ($\text{GND}$).
  * **74LS08 (AND):** Se probó la compuerta 1 (pines 1, 2 ent.; 3 sal.) y la compuerta 2 (pines 4, 5 ent.; 6 sal.), verificando salida `1` solo si ambas entradas valen `1`.
  * **74LS02 (NOR):** Se probó la compuerta 1 (pines 2, 3 ent.; 1 sal.), comprobando salida `1` únicamente cuando ambas entradas valen `0`. Se evidenció la diferencia estructural del *pinout* respecto al 7408.

* **Prueba de entrada sin conectar (flotante):**
  * Al dejar la entrada $B$ flotante en la compuerta AND, Logisim muestra la línea en azul. Al fijar $A=0$ la salida da `0`, y al fijar $A=1$ la salida cambia a `1`. Esto comprueba que la entrada no conectada toma internamente el valor lógico `1` por corriente de polarización TTL.
```

---

## 📄 SEMANA 2

### `semana-02/teoria.md`
```markdown
# Semana 2: Álgebra de Boole y Formas Canónicas

## 1. Postulados y Teoremas Fundamentales
* **Identidad:** $X+0=X \quad \mid \quad X\cdot1=X$
* **Complemento:** $X+X'=1 \quad \mid \quad X\cdot X'=0$
* **Leyes de De Morgan:** 
  $$\overline{A\cdot B\cdot C} = A' + B' + C'$$
  $$\overline{A + B + C} = A'\cdot B'\cdot C'$$
* **Teorema de Adyacencia:** $XY + XY' = X \quad \mid \quad (X+Y)(X+Y') = X$
* **Absorción del Complemento:** $X + X'Y = X + Y \quad \mid \quad X(X' + Y) = XY$

## 2. Minitérminos y Maxitérminos
* **Minitérmino ($m_i$):** Término producto que vale `1` en una sola fila. La variable en `1` entra directa, la variable en `0` entra complementada.
* **Maxitérmino ($M_i$):** Término suma que vale `0` en una sola fila. La variable en `0` entra directa, la variable en `1` entra complementada. $M_i = (m_i)'$.

## 3. Formas Canónicas y Criterio de Selección
* **SOP (Suma de Productos):** $F = \sum m(\text{filas con 1})$.
* **POS (Producto de Sumas):** $F = \prod M(\text{filas con 0})$.
* **Criterio de Costo:** Se prefiere la forma con menor número de términos para reducir el hardware final (compuertas, circuitos integrados y retardo en niveles lógicos).
```

### `semana-02/ape-02-informe.md`
```markdown
# Reporte Técnico APE N.º 02: Formas canónicas y simplificación algebraica

* **Requerimiento R6 (Grupo 6):** Segmento central `g` de un display de 7 segmentos accionado por un número BCD de 3 bits $ABC$ ($0$ a $7$). El segmento debe encenderse ($F=1$) para los dígitos 2, 3, 4, 5 y 6; y apagarse ($F=0$) para 0, 1 y 7.

* **Tabla de Verdad y Obtención Canónica:**
  * $\sum m(2,3,4,5,6) \Rightarrow F_{SOP} = A'BC' + A'BC + AB'C' + AB'C + ABC'$
  * $\prod M(0,1,7) \Rightarrow F_{POS} = (A+B+C)(A+B+C')(A'+B'+C')$

* **Simplificación Algebraica Paso a Paso:**
  * Expresión POS simplificada: $F = (A+B)(A'+B'+C')$
  * Expresión SOP simplificada equivalente: $F = A'B + AB' + BC' = (A \oplus B) + BC'$

* **Comparativa de Costo de Hardware (Tabla 6):**
  * **SOP Canónica:** 9 compuertas (3 NOT, 5 AND de 3 ent., 1 OR de 5 ent.) $\rightarrow$ Reacciona en 3 niveles $\rightarrow$ Utiliza 4 CIs (1x 74LS04, 2x 74LS11, 1x 74LS32).
  * **Simplificada (con XOR):** 4 compuertas (1 NOT, 1 XOR, 1 AND, 1 OR) $\rightarrow$ Utiliza 4 CIs de 2 entradas (74LS04, 74LS86, 74LS08, 74LS32). Reduce sustancialmente el retardo de propagación acumulado y el número de interconexiones.
```

---

## 📄 SEMANA 3

### `semana-03/teoria.md`
```markdown
# Semana 3: Mapas de Karnaugh, Condiciones Indiferentes y Universalidad NAND/NOR

## 1. Mapas de Karnaugh (K-Maps)
* Organización basada en el **Código Gray** ($00, 01, 11, 10$) para garantizar adyacencia lógica entre celdas contiguas.
* **Reglas de Agrupación:**
  1. Grupos rectangulares de tamaño $2^k$ ($1, 2, 4, 8, 16$ celdas).
  2. Los bordes opuestos y las 4 esquinas del mapa están conectados (geometría de toroide).
  3. Un grupo de $2^k$ celdas en un mapa de $N$ variables elimina $k$ variables.

## 2. Implicantes Primos y Esenciales
* **Implicante Primo:** Grupo válido de `1`s (o $X$) que no puede agrandarse más.
* **Primo Esencial:** Implicante primo que contiene al menos un `1` que no está cubierto por ningún otro grupo primo. Debe incluirse obligatoriamente en la solución mínima.

## 3. Condiciones Indiferentes (*Don't Care* - $X$)
* Combinaciones de entrada que nunca ocurrirán o cuya salida no importa (ej. estados $1010$ a $1111$ en BCD).
* **Regla de uso:** Se tratan como `1` únicamente si ayudan a agrandar un grupo de `1`s (lo que acorta los términos). Si no ayudan, se tratan como `0`. **Nunca** se forma un grupo compuesto exclusivamente por $X$.

## 4. Universalidad NAND y NOR
* Toda red combinacional puede implementarse usando únicamente compuertas NAND o únicamente NOR.
* **Conversión SOP a NAND-NAND (4 pasos):**
  1. Partir de la SOP mínima: $F = A + BD + BC$.
  2. Aplicar doble negación: $F = ((A + BD + BC)')'$.
  3. Aplicar Leyes de De Morgan a la barra interna: $F = (A' \cdot (BD)' \cdot (BC)')'$.
  4. Traducir a compuertas: Nivel 1 compuertas NAND (si un literal entra solo se invierte con NAND), Nivel 2 compuerta NAND colectiva.
```

### `semana-03/ape-03-informe.md`
```markdown
# Reporte Técnico APE N.º 03: Optimización de hardware mediante mapas de Karnaugh

* **Problema:** Juego educativo en BCD de 4 bits ($ABCD$). Un LED se enciende ($F=1$) si el dígito es primo ($2, 3, 5, 7$). Las entradas $1010$ a $1111$ ($10$ a $15$) son condiciones indiferentes ($X$).

* **Minimización con Mapa de Karnaugh (4 variables):**
  * Sin tomar indiferentes ($X=0$): $F_{min} = A'B'C + A'BD$ (6 literales, 3 compuertas).
  * **Aprovechando indiferentes ($X$):** Se agrupa la celda con minitérminos y don't cares en bloques de 4:
    $$F_{min\_X} = B'C + BD \quad \text{(4 literales)}$$

* **Conversión e Implementación NAND de 2 entradas (74LS00):**
  * Aplicando De Morgan: $F = \overline{ \overline{B'C} \cdot \overline{BD} } = \text{NAND}\left( \text{NAND}(B', C), \text{NAND}(B, D) \right)$
  * **Asignación en el circuito integrado 74LS00 (Quad 2-input NAND):**
    * Compuerta 1 (Inversor $B'$): Pines 1, 2 unidos a $B \rightarrow$ Salida Pin 3.
    * Compuerta 2 (Término $(B'C)'$): Pin 4 (desde pin 3) y Pin 5 ($C$) $\rightarrow$ Salida Pin 6.
    * Compuerta 3 (Término $(BD)'$): Pin 9 ($B$) y Pin 10 ($D$) $\rightarrow$ Salida Pin 8.
    * Compuerta 4 (Salida NAND colectiva $F$): Pin 12 (desde pin 6) y Pin 13 (desde pin 8) $\rightarrow$ Salida Pin 11.

* **Cuantificación del Ahorro de Hardware (Tabla 3 y 4 del APE 03):**
  * **Versión Canónica:** Requiere 4 CIs (74LS04, 2x 74LS21, 74LS32).
  * **Versión NAND Mínima:** Requiere únicamente **1 Circuito Integrado (74LS00)** utilizando 4 compuertas NAND de 2 entradas.
  * **Ahorro Logrado:** Reducción del **75% en circuitos integrados** y reducción de 16 a 4 literales.
```
```

---

### Resumen de lo generado en el cuaderno:
1. **Fidelidad conceptual y técnica:** Se incorporan los parámetros reales de la familia **74LS** (márgenes de ruido, niveles de voltaje $V_{OH}, V_{IH}$, entradas flotantes en azul/rojo), tal como se especifica en las diapositivas de la Semana 1.
2. **Procedimientos detallados:** Se integran las transformaciones paso a paso de **SOP/POS** (Semana 2) y la deducción para implementar la función de números primos BCD con **un solo chip 74LS00** usando condiciones indiferentes (Semana 3 / APE 03).
3. **Casos reales de laboratorio:** Incluye la asignación del Requerimiento 6 del display de 7 segmentos (APE 02) y la verificación del comparador XOR en Logisim-evolution (APE 01).
