# **Manual Básico de PSpice Orcad en Modo Texto**

## **1. Introducción**
PSpice permite simular circuitos mediante archivos de texto en formato **.CIR**, donde se definen los componentes, conexiones y análisis.

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

### **Explicación**
- `V1 1 0 SIN(0 5 1k)` → Fuente senoidal de **5V pico** y **1kHz**.
- `R1 1 2 1k` → Resistencia de 1kΩ entre los nodos 1 y 2.
- `C1 2 0 1u` → Condensador de 1µF entre los nodos 2 y 0.
- `.TRAN 0.01m 5m` → Simulación de **5ms** con un paso de **0.01ms**.

---

## **6. Correr la Simulación en PSpice**
1. **Abrir PSpice Orcad**.
2. **Crear un nuevo archivo de texto (`.CIR`)** y escribir el circuito.
3. **Guardar el archivo** con extensión `.CIR`.
4. **Abrir PSpice A/D** (el simulador de PSpice).
5. **Cargar el archivo `.CIR`**.
6. **Ejecutar la simulación** (`Run`).
7. **Visualizar los resultados** en `Probe`.

---

## **7. Interpretación de Resultados**
- En **DC**, puedes graficar voltajes y corrientes en función de la variación de la fuente.
- En **AC**, puedes analizar **respuesta en frecuencia**, obteniendo diagramas de **Bode** (magnitud y fase).
- En **Transitorio**, puedes visualizar el comportamiento del circuito en función del tiempo.

---

## **8. Conclusión**
Este manual te permite realizar simulaciones **básicas en DC, AC y Transitorio** usando **modo texto** en PSpice Orcad. Puedes modificar valores y agregar componentes como inductores y transistores según tus necesidades.