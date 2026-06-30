# Sistema Discriminador de Frecuencias de Audio (Mixed-Signal System)

Este repositorio contiene el diseño, análisis y simulación de un sistema electrónico embebido capaz de discriminar señales de audio en tiempo real basándose en su frecuencia. El circuito integra hardware analógico de filtrado y acondicionamiento con control digital para activar selectivamente actuadores periféricos bajo una única fuente de alimentación de 5V.

## 🎯 Especificaciones de Diseño
* **Frecuencia de activación:** 1,000 Hz (Supera el umbral crítico de activación)
* **Frecuencia de rechazo:** 2,500 Hz (Atenuada por debajo del umbral para evitar activaciones)
* **Frecuencia de corte diseñada:** ~1.3 kHz
* **Alimentación del sistema:** Fuente única de 5V

## 🛠️ Herramientas y Componentes
* **Entorno de Simulación:** Labcenter Proteus V8.13
* **Microcontrolador:** Microchip PIC16F887 (Frecuencia de reloj a 4 MHz)
* **Software de Desarrollo:** MPLAB X IDE & Compilador XC8
* **Topología Analógica:** Filtro Activo Sallen-Key Pasa-Bajas de 2do orden (pendiente de 40 dB/década)

## 📐 Arquitectura del Sistema
El sistema procesa la señal de audio de manera secuencial a través de las siguientes etapas:

1. **Filtrado Analógico (Sallen-Key):** Asegura que la señal de 1 kHz pase con casi toda su potencia, mientras que la de 2.5 kHz se sitúe en la zona de atenuación profunda.
2. **Acondicionamiento (Detector de Envolvente):** Un diodo rectificador rápido y una red de capacitor de filtrado con resistencia a tierra extraen la amplitud de la señal alterna (AC), transformándola en un nivel de voltaje continuo (DC) estable para evitar vibraciones en la salida.
3. **Comparador de Voltaje:** Compara la señal rectificada contra un umbral de referencia muy bajo (~0.1V - 0.2V) configurado mediante un divisor de tensión (Resistencia superior de 5.1 kΩ) para garantizar una alta sensibilidad ante señales reales.
4. **Control y Salida Digital:** La salida del comparador ingresa al pin RA0 del PIC16F887. El firmware procesa el estado lógico y conmuta un arreglo de LEDs en el Puerto B.

## 📈 Resultados Obtenidos
* **A 1,000 Hz:** El voltaje del filtro supera el umbral de 0.1V, el comparador entrega un "1" lógico al microcontrolador y el PIC activa las salidas del Puerto B.
* **A 2,500 Hz:** La señal se atenúa profundamente por debajo de la referencia, el comparador entrega un "0" lógico y el sistema permanece completamente apagado y protegido contra activaciones accidentales.

## 📂 Estructura del Repositorio
* `/Simulacion`: Contiene el archivo de proyecto de Proteus (`ProyectoFinal.pdsprj`) y los archivos de audio de prueba a 1 kHz y 2.5 kHz utilizados para estimular el circuito.
* `/Documentacion`: Contiene el reporte técnico final en formato PDF con el desarrollo teórico detallado.

---
*Proyecto de ingeniería desarrollado por Ricardo Somoza Rueda y Javier Ocampo González para la asignatura de Electrónica Integrada (Mayo 2026).*
