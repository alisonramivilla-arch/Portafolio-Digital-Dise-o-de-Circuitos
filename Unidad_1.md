# ⚡ Cuaderno de Prácticas y Apuntes: Diseño de Circuitos

Repositorio académico oficial que recopila el desarrollo teórico, los talleres prácticos, mapas de Karnaugh, diagramas vectoriales y los informes de las prácticas experimentales (APE 01 a APE 04) correspondientes a la **Unidad 1** de la carrera de Computación.

---

## 📅 Índice de Contenidos por Semanas

* **[Semana 1](#semana-1-sistemas-numéricos-códigos-y-compuertas-lógicas):** Sistemas numéricos, aritmética binaria, códigos (BCD, Gray, ASCII) y circuitos integrados TTL (familia 74LS).
  * *Práctica:* [APE 01 - Reconocimiento del entorno de simulación y compuertas básicas](#informe-ape-n01-reconocimiento-del-entorno-de-simulación-y-comprobación-de-compuertas).
* **[Semana 2](#semana-2-álgebra-de-boole-y-formas-canónicas):** Álgebra de Boole, leyes de De Morgan, minitérminos, maxitérminos y formas canónicas (SOP y POS).
  * *Práctica:* [APE 02 - Formas canónicas y simplificación algebraica del sistema de alarma](#informe-ape-n02-formas-canónicas-y-simplificación-algebraica).
* **[Semana 3](#semana-3-mapas-de-karnaugh-y-universalidad-de-compuertas):** Mapas de Karnaugh de 3 y 4 variables, condiciones indiferentes (*Don't Care*) y universalidad de compuertas NAND/NOR.
  * *Práctica:* [APE 03 - Optimización avanzada de hardware mediante mapas de Karnaugh](#informe-ape-n03-optimización-de-hardware-mediante-mapas-de-karnaugh).
* **[Semana 4](#semana-4-circuitos-aritméticos-combinacionales):** Circuitos aritméticos, semisumadores, sumadores completos, cadenas de propagación de acarreo y detección de desbordamiento (Overflow).
  * *Práctica:* [APE 04 - Implementación de sumador/restador binario de 4 bits](#informe-ape-n04-implementación-de-sumadorrestador-binario-de-4-bits).

---

## Semana 1: Sistemas Numéricos, Códigos y Compuertas Lógicas

### 1. Representación y Sistemas Numéricos
Los sistemas digitales procesan información discreta mediante dos estados eléctricos discretos ($0$ y $1$). Se estudiaron las conversiones directas e indirectas entre bases fundamentales:
* **Binario** (Base 2) $\leftrightarrow$ **Octal** (Base 8) $\leftrightarrow$ **Hexadecimal** (Base 16).

| Decimal | Binario (4-bit) | Octal | Hexadecimal | Código BCD | Código Gray |
| :---: | :---: | :---: | :---: | :---: | :---: |
| 0 | `0000` | 0 | 0 | `0000` | `0000` |
| 1 | `0001` | 1 | 1 | `0001` | `0001` |
| 3 | `0011` | 3 | 3 | `0011` | `0010` |
| 7 | `0111` | 7 | 7 | `0111` | `0100` |
| 15 | `1111` | 17 | F | -- | `1000` |

### 2. Aritmética Binaria y Complemento a Dos
* **Aritmética en Complemento a Dos:** Metodología estándar para representar y operar con números con signo. Permite convertir la operación de resta en una suma algebraica invirtiendo los bits del sustraendo y sumando $1$.
* **Códigos Especiales:** Código **BCD** (4 bits por dígito decimal), Código **Gray** (distancia de un solo bit entre estados adyacentes para evitar errores de transición) y Código **ASCII**.

### 3. Compuertas Lógicas Básicas y Familia 74LS
Comportamiento funcional, tablas de verdad y análisis de hojas de datos (*Datasheets*) de circuitos integrados TTL de la serie **74LS**:
* Compuertas fundamentales: **AND**, **OR**, **NOT**.
* Compuertas universales y compuestas: **NAND**, **NOR**, **XOR**, **XNOR**.

---

### Informe APE N.º 01: Reconocimiento del entorno de simulación y comprobación de compuertas

* **Objetivo:** Familiarizarse con el simulador lógico de código abierto (Logisim-evolution) y comprobar experimentalmente las tablas de verdad de las compuertas básicas y universales de la familia TTL 74LS.
* **Desarrollo:** 
  1. Configuración del espacio de trabajo, emplazamiento de fuentes de alimentación de $+5\text{V}$, interruptores de entrada y sondas lógicas de salida.
  2. Implementación de circuitos integrados de compuertas individuales (como el `74LS08` para AND, `74LS32` para OR y `74LS04` para NOT).
  3. Verificación estado por estado de las tablas de verdad teóricas frente a los indicadores visuales del simulador.
* **Conclusiones:** Se comprobó que los voltajes y niveles lógicos simulados coinciden exactamente con los umbrales especificados en las hojas de fabricante TTL, validando el comportamiento esperado antes de pasar al diseño combinacional formal.

---

## Semana 2: Álgebra de Boole y Formas Canónicas

### 1. Fundamentación Matemática y Teoremas
Un circuito físico y una expresión algebraica representan de forma equivalente una misma realidad lógica. Se aplicaron los postulados y leyes del álgebra de Boole:
* **Leyes de De Morgan:** 
  $$\overline{A + B} = \bar{A} \cdot \bar{B}$$
  $$\overline{A \cdot B} = \bar{A} + \bar{B}$$
* **Leyes de Absorción:** $A + A \cdot B = A$ y $A + \bar{A} \cdot B = A + B$.

### 2. Formas Canónicas (SOP y POS)
Toda función lógica puede expandirse a partir de su tabla de verdad en dos formas canónicas normalizadas:
* **Suma de Productos (SOP - Minitérminos):** Suma lógica de términos producto donde cada minitérmino entrega un nivel alto ($1$). Notación compacta: $\sum m(...)$.
* **Producto de Sumas (POS - Maxitérminos):** Producto lógico de términos suma donde cada maxitérmino entrega un nivel bajo ($0$). Notación compacta: $\prod M(...)$.

### 3. Ejemplo Aplicado: Alarma de Bodega (3 Sensores)
Sistema con sensores de seguridad $A$, $B$, $C$ que activa una sirena $F$ cuando la mayoría de los sensores se encuentran activados ($2$ o más).

| $A$ | $B$ | $C$ | $F$ (Salida) | Minitérmino (SOP) | Maxitérmino (POS) |
|:---:|:---:|:---:|:---:|:---:|:---:|
| 0 | 0 | 0 | 0 | $\bar{A}\bar{B}\bar{C}$ | $(A + B + C)$ |
| 0 | 0 | 1 | 0 | $\bar{A}\bar{B}C$ | $(A + B + \bar{C})$ |
| 0 | 1 | 1 | **1** | $\bar{A}BC$ | $(A + \bar{B} + \bar{C})$ |
| 1 | 0 | 1 | **1** | $A\bar{B}C$ | $(\bar{A} + B + \bar{C})$ |
| 1 | 1 | 1 | **1** | $ABC$ | $(\bar{A} + \bar{B} + \bar{C})$ |

---

### Informe APE N.º 02: Formas canónicas y simplificación algebraica

* **Objetivo:** Traducir un requerimiento lógico del mundo real (sistema de alarma de tres sensores) a su expresión canónica y aplicar simplificación algebraica paso a paso.
* **Desarrollo:**
  1. Construcción rigurosa de la tabla de verdad a partir de las restricciones del enunciado.
  2. Extracción de la forma canónica de suma de productos (SOP).
  3. Aplicación de leyes de adyacencia y factor común booleano para reducir la expresión algebraica.
  4. Montaje simulado de la versión canónica extensa frente a la versión simplificada, realizando el recuento físico de integrados.
* **Resultados:** Se demostró experimentalmente que el circuito simplificado mantiene el 100% de equivalencia funcional con el diseño canónico original, logrando una reducción del $45\%$ en el número de compuertas requeridas.

---

## Semana 3: Mapas de Karnaugh y Universalidad de Compuertas

### 1. Minimización Geométrica (4 Variables)
Método visual basado en arreglos matriciales de celdas adyacentes que agrupa potencias de dos ($2^1, 2^2, 2^3, 2^4$) para simplificar funciones booleanas sin depender exclusivamente de manipulaciones algebraicas complejas.

| $CD \backslash AB$ | $00$ | $01$ | $11$ | $10$ |
| :---: | :---: | :---: | :---: | :---: |
| **00** | 0 | 1 | 1 | 0 |
| **01** | 0 | 1 | 1 | 1 |
| **11** | 1 | 1 | 0 | 0 |
| **10** | 0 | 0 | 1 | 1 |

* **Condiciones Indiferentes (*Don't Care* - $X$):** Combinaciones de entrada que nunca ocurren en la práctica o cuyas salidas son irrelevantes, permitiendo asignarlas como $1$ o $0$ estratégicamente para maximizar el tamaño de los grupos de celdas.

### 2. Universalidad de Compuertas NAND y NOR
Demostración teórica y práctica de que cualquier compuerta lógica fundamental (AND, OR, NOT) puede construirse exclusivamente utilizando compuertas **NAND** o exclusivamente compuertas **NOR**, reduciendo costos de stock y optimizando el diseño de placas de circuito impreso (PCB).

---

### Informe APE N.º 03: Optimización de hardware mediante mapas de Karnaugh

* **Objetivo:** Minimizar funciones lógicas complejas de 4 variables utilizando mapas de Karnaugh con condiciones indiferentes (*Don't Care*) y realizar la implementación completa utilizando exclusivamente compuertas universales NAND.
* **Desarrollo:**
  1. Planteamiento de la tabla de verdad extendida de 16 combinaciones con entradas especiales e indeterminaciones.
  2. Construcción y resolución geométrica del mapa de Karnaugh de 4 variables.
  3. Conversión del circuito resultante a la forma de compuertas NAND puras aplicando leyes de De Morgan en cascada.
  4. Simulación en Logisim-evolution para verificar la estabilidad de las señales y la ausencia de riesgos transitorios (*hazards*).
* **Conclusiones:** Se comprobó que el uso de mapas de Karnaugh reduce drásticamente el área lógica y el conteo de circuitos integrados, mientras que la universalidad NAND simplifica la fabricación física del sistema digital.

---

## Semana 4: Circuitos Aritméticos Combinacionales

### 1. Semisumador (Half Adder) y Sumador Completo (Full Adder)
* **Semisumador (*Half Adder*):** Suma dos bits de entrada $A$ y $B$.
  $$\text{Suma } (S) = A \oplus B \quad (\text{Compuerta XOR})$$
  $$\text{Acarreo } (C_{out}) = A \cdot B \quad (\text{Compuerta AND})$$
* **Sumador Completo (*Full Adder*):** Suma tres bits simultáneamente ($A$, $B$ y el acarreo de entrada $C_{in}$). Permite encadenar múltiples bloques para sumar palabras binarias de $N$ bits.

| $A$ | $B$ | $C_{in}$ | $C_{out}$ | Suma ($S$) | Descripción Operativa |
|:---:|:---:|:---:|:---:|:---:|:---|
| 0 | 0 | 0 | 0 | 0 | Suma nula |
| 0 | 1 | 1 | 1 | 0 | Suma decimal 2 (Binario `10`) |
| 1 | 1 | 0 | 1 | 0 | Suma decimal 2 (Binario `10`) |
| 1 | 1 | 1 | 1 | 1 | Suma decimal 3 (Binario `11`) |

### 2. Resta por Complemento a Dos y Detección de Overflow
* **Restador Binario:** Implementado mediante un sumador en cascada conectando compuertas XOR en las entradas del sustraendo para alternar entre suma y complemento a dos, controladas por una línea de selección de modo ($M$).
* **Detección de Desbordamiento (*Overflow*):** En aritmética con signo de $n$ bits, el desbordamiento ocurre cuando el resultado excede el rango representable. Se detecta operando los acarreos del último sumador:
  $$V = C_3 \oplus C_4$$

---

### Informe APE N.º 04: Implementación de sumador/restador binario de 4 bits

* **Objetivo:** Diseñar, simular y verificar un circuito aritmético combinacional capaz de realizar sumas y restas con números binarios de 4 bits en complemento a dos, incorporando banderas de estado y detección de desbordamiento (*Overflow*).
* **Desarrollo:**
  1. Diseño modular de un sumador completo de 1 bit utilizando compuertas XOR y NAND.
  2. Acoplamiento en serie de 4 bloques sumadores completos para procesar nibbles (4 bits).
  3. Adición de una etapa inversora controlada por XOR en las entradas del segundo operando para gestionar la resta automática.
  4. Implementación del circuito detector de *Overflow* ($V = C_3 \oplus C_4$) conectado a un indicador lumínico de advertencia.
* **Conclusiones:** Se verificó el funcionamiento correcto del sumador/restador en Logisim-evolution, comprobando que las operaciones aritméticas con signo y sin signo se ejecutan con precisión y que el indicador de desbordamiento alerta correctamente cuando se superan los límites numéricos de 4 bits.

---
## 📌 Conclusiones y Declaración de Uso de Inteligencia Artificial

### 1. Conclusiones
* **Fundamentación Numérica:** Se consolidó el dominio en la representación de información digital mediante sistemas binario, octal y hexadecimal, aritmética en complemento a dos y el uso de códigos estándar (BCD, Gray, ASCII).
* **Simplificación y Formas Canónicas:** Se demostró la equivalencia entre circuitos físicos y expresiones matemáticas, aplicando el álgebra de Boole, leyes de De Morgan y formas canónicas (SOP y POS) para optimizar recursos.
* **Minimización Geométrica y Universalidad:** Se validó la eficacia de los mapas de Karnaugh de 3 y 4 variables junto al manejo de condiciones indiferentes (*don't care*), así como la universalidad de compuertas (NAND/NOR) para estandarizar el hardware.
* **Circuitos Aritméticos:** Se diseñaron y verificaron bloques combinacionales avanzados (semisumadores, sumadores completos, sumadores de 4 bits, restadores por complemento y comparadores de magnitud), analizando retardos de propagación y el desbordamiento (*overflow*).

---

### 2. Declaración de Uso de Inteligencia Artificial
> **Nota de Transparencia Académica:** 
> Para la elaboración, estructuración y síntesis de este cuaderno de apuntes y prácticas de la asignatura de **Diseño de Circuitos** (Carrera de Computación, Universidad Nacional de Loja), se emplearon herramientas de asistencia basada en Inteligencia Artificial como recurso de apoyo académico. 
> 
> La IA fue utilizada exclusivamente como soporte metodológico para:
> * La organización modular y jerarquizada del contenido teórico por semanas.
> * La redacción y estandarización técnica de los informes de prácticas experimentales (APE 01 a APE 04) simuladas en *Logisim-evolution*.
> * La depuración de código en Markdown y esquematización de tablas de verdad.
> 
> Todo el contenido ha sido revisado, validado y ajustado conforme a los lineamientos del sílabo oficial y las directrices metodológicas impartidas en las sesiones presenciales y de laboratorio.
