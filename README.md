# Sistema Discriminador de Frecuencias de Audio (Mixed-Signal System)

Este repositorio contiene el diseño, análisis y simulación de un sistema electrónico embebido capaz de discriminar señales de audio en tiempo real basándose en su frecuencia. [cite_start]El circuito integra hardware analógico de filtrado y acondicionamiento con control digital para activar selectivamente actuadores periféricos bajo una única fuente de alimentación de 5V[cite: 12, 13].

## 🎯 Especificaciones de Diseño
**Frecuencia de activación:** 1,000 Hz (Supera el umbral crítico de activación) [cite: 16, 98]
***Frecuencia de rechazo:** 2,500 Hz (Atenuada por debajo del umbral para evitar activaciones) [cite: 16, 99]
***Frecuencia de corte diseñada:** ~1.3 kHz [cite: 27]
**Alimentación del sistema:** Fuente única de 5V [cite: 13]

## 🛠️ Herramientas y Componentes
* **Entorno de Simulación:** Labcenter Proteus V8.13 [cite: 110]
* **Microcontrolador:** Microchip PIC16F887 (Frecuencia de reloj a 4 MHz) [cite: 12, 107]
***Software de Desarrollo:** MPLAB X IDE & Compilador XC8 [cite: 113]
***Topología Analógica:** Filtro Activo Sallen-Key Pasa-Bajas de 2do orden (pendiente de 40 dB/década) [cite: 21]

## 📐 Arquitectura del Sistema
El sistema procesa la señal de audio de manera secuencial a través de las siguientes etapas[cite: 89, 91, 93, 94, 95]:

1. **Filtrado Analógico (Sallen-Key):** Asegura que la señal de 1 kHz pase con casi toda su potencia, mientras que la de 2.5 kHz se sitúe en la zona de atenuación profunda[cite: 28].
2. **Acondicionamiento (Detector de Envolvente):** Un diodo rectificador rápido y una red de capacitor de filtrado con resistencia a tierra extraen la amplitud de la señal alterna (AC), transformándola en un nivel de voltaje continuo (DC) estable para evitar vibraciones en la salida[cite: 22, 32, 91, 92].
3. **Comparador de Voltaje:** Compara la señal rectificada contra un umbral de referencia muy bajo (~0.1V - 0.2V) configurado mediante un divisor de tensión (Resistencia superior de 5.1 kΩ) para garantizar una alta sensibilidad ante señales reales[cite: 23, 35, 36, 37].
4. **Control y Salida Digital:** La salida del comparador ingresa al pin RA0 del PIC16F887[cite: 94]. El firmware procesa el estado lógico y conmuta un arreglo de LEDs en el Puerto B[cite: 24, 95].

## 📈 Resultados Obtenidos
* **A 1,000 Hz:** El voltaje del filtro supera el umbral de 0.1V, el comparador entrega un "1" lógico al microcontrolador y el PIC activa las salidas del Puerto B[cite: 98].
* **A 2,500 Hz:** La señal se atenúa profundamente por debajo de la referencia, el comparador entrega un "0" lógico y el sistema permanece completamente apagado y protegido contra activaciones accidentales[cite: 99, 103].

## 📂 Estructura del Repositorio
* `/Simulacion`: Contiene el archivo de proyecto de Proteus (`ProyectoFinal.pdsprj`) y los archivos de audio de prueba a 1 kHz y 2.5 kHz utilizados para estimular el circuito[cite: 90].
* `/Documentacion`: Contiene el reporte técnico final en formato PDF con el desarrollo teórico detallado[cite: 1].

---
*Proyecto de ingeniería desarrollado por Ricardo Somoza Rueda y Javier Ocampo González para la asignatura de Electrónica Integrada (Mayo 2026).* [cite: 3, 5, 7, 9]
