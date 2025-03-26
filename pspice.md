# **Manual Básico de PSpice Orcad**

## **1. Introducción**

PSpice permite simular circuitos en **modo texto** y **modo esquemático**. Este manual cubre ambos métodos para realizar análisis **DC, AC y Transitorio**.

# **Parte 1: Simulación en Modo Texto**

## **2. Estructura de un Archivo de Simulación**

Cada archivo de simulación en **modo texto** sigue la siguiente estructura:

1. **Título del circuito** (primera línea)
2. **Definición de nodos y componentes**
3. **Comandos de análisis** (`.DC`, `.AC`, `.TRAN`, etc.)
4. **Línea de finalización** (`.END`)

---

## **3. Simulación en DC**

Para hacer un análisis DC, se usa el comando **.DC** para analizar cómo varía una respuesta (tensión o corriente) al modificar un parámetro como una fuente de voltaje o corriente.

### **Ejemplo de Simulación DC**

Archivo: `circuito_dc.cir`

```plaintext
* Circuito DC con fuente variable
V1 1 0 DC 10      ; Fuente de 10V conectada entre nodo 1 y 0
R1 1 2 1k         ; Resistencia de 1kΩ entre nodos 1 y 2
R2 2 0 2k         ; Resistencia de 2kΩ entre nodos 2 y 0

.DC V1 0 20 1     ; Variar V1 de 0V a 20V en pasos de 1V
.PROBE            ; Habilita visualización de resultados
.END
```

---

## **4. Simulación en AC**

Para hacer un análisis en frecuencia, se usa el comando **.AC**.

### **Ejemplo de Simulación AC**

Archivo: `circuito_ac.cir`

```plaintext
* Circuito AC con análisis de frecuencia
V1 1 0 AC 1       ; Fuente de voltaje AC con amplitud de 1V
R1 1 2 1k         ; Resistencia de 1kΩ
C1 2 0 1u         ; Capacitor de 1µF

.AC DEC 10 10 10k ; Barrido logarítmico de frecuencia de 10Hz a 10kHz
.PROBE            ; Habilita visualización de resultados
.END
```

---

## **5. Simulación Transitoria**

Para analizar la respuesta del circuito en función del tiempo, se usa el comando **.TRAN**.

### **Ejemplo de Simulación Transitoria**

Archivo: `circuito_tran.cir`

```plaintext
* Circuito con análisis transitorio
V1 1 0 SIN(0 5 1k) ; Fuente senoidal de 5V pico y 1kHz
R1 1 2 1k          ; Resistencia de 1kΩ
C1 2 0 1u          ; Capacitor de 1µF

.TRAN 0.01m 5m     ; Simulación de 5ms con paso de 0.01ms
.PROBE             ; Habilita visualización de resultados
.END
```

---

## **6. Uso de una Resistencia Variable (Potenciómetro)**

Para modelar un potenciómetro en **modo texto**, se puede usar el comando `.STEP` para variar su valor durante la simulación.

### **Ejemplo de Resistencia Variable**

Archivo: `potenciometro.cir`

```plaintext
* Circuito con potenciómetro
V1 1 0 DC 10        ; Fuente de 10V
R1 1 2 {RVAL}       ; Resistencia variable entre nodos 1 y 2
R2 2 0 1k           ; Resistencia fija de 1kΩ

.PARAM RVAL = 500   ; Valor inicial de la resistencia variable
.DC V1 0 10 1
.STEP PARAM RVAL LIST 500 1k 2k 5k ; Variar RVAL en diferentes valores
.PROBE
.END
```

En el modo esquemático, se puede utilizar un potenciómetro desde la librería de PSpice (`R_var`) y modificar su valor en la simulación.

---

# **Parte 2: Simulación en Modo Esquemático**

## **7. Creación de Circuitos en el Editor Esquemático**

1. **Abrir OrCAD Capture**.
2. **Crear un nuevo proyecto**:
   - Selecciona `File` > `New` > `Project`.
   - Escoge `Analog or Mixed A/D` y asigna un nombre.
   - Elige una ubicación y presiona `OK`.
3. **Agregar componentes**:
   - Haz clic en `Place` > `Part` o usa el icono de `Agregar Componente`.
   - Busca los componentes en la biblioteca y agrégales valores.
   - Conéctalos con el `Wire Tool`.
4. **Agregar fuentes de alimentación**:
   - Para análisis DC: `SOURCE` > `VDC`.
   - Para análisis AC: `SOURCE` > `VAC`.
   - Para transitorio: `SOURCE` > `VSIN`.
5. **Agregar resistencias variables (potenciómetros)**:
   - Busca en la biblioteca `R_var` o `POT`.
   - Configura los valores en `Properties`.
6. **Agregar sondas (`PROBE`)** para medir voltajes o corrientes.
7. **Guardar el circuito**.

---

## **8. Configuración de Simulación**

1. **Abrir PSpice** (`PSpice` > `New Simulation Profile`).
2. **Configurar el tipo de análisis**:
   - **DC Sweep**: `Analysis` > `DC Sweep` y configurar la fuente.
   - **AC Sweep**: `Analysis` > `AC Sweep` y definir el rango de frecuencia.
   - **Transitorio**: `Analysis` > `Time Domain (Transient)` y definir el tiempo de simulación.
   - **Parámetro Variable (`STEP`)**: Agregar `Step Parameter` para variar la resistencia.
3. **Ejecutar la simulación** (`Run`).

---

## **9. Interpretación de Resultados**

- **DC Sweep**: Ver variaciones de voltajes y corrientes respecto a una fuente variable.
- **AC Sweep**: Analizar respuestas en frecuencia (diagramas de Bode).
- **Transitorio**: Observar la respuesta del circuito en el tiempo.
- **Parámetro Variable**: Ver cómo cambia la respuesta con diferentes valores de resistencia.

---

## **10. Conclusión**

Este manual cubre la simulación de circuitos en **modo texto y modo esquemático** en PSpice Orcad, incluyendo el uso de una resistencia variable (potenciómetro). Para simulaciones más avanzadas, puedes incluir componentes como transistores, amplificadores operacionales y elementos no lineales.
