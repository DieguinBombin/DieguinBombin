---
layout: post
title:  "Visualización de la Información - Mortandar mundial, un analisis de casos extremos."
description: "ESP32 y visualización web"
date:   2026-5-17 00:51:42 -0300
categories: jekyll update
---

---
# Visualización WEB

> **Evolución de la Mortalidad Mundial:** Un proyecto de visualización de datos multisensorial que explora la tasa bruta de mortalidad global a través del espacio, el tiempo y el sonido.

---

### Enlaces del Proyecto

* **Demo en Vivo (GitHub Pages):** [Visualización Interactiva](https://dieguinbombin.github.io/InfoViz_mortandad_mundial/)
* **Presentación en Video:** [Demo en YouTube](https://www.youtube.com/watch?v=ETtdHJPLbBc) *(Nota: Audio con limitaciones de micrófono)*

---

## Propósito del Proyecto

Representar la evolución histórica de la tasa bruta de mortalidad (muertes anuales por cada 1.000 habitantes) a nivel global, permitiendo a los usuarios identificar patrones espaciotemporales asociados a crisis sanitarias, guerras y dinámicas demográficas (con foco en hitos históricos de África).

El sistema pasa de una exploración macro a micro: desde un *heatmap* global hasta la inspección detallada de países mediante interactividad, animación y sonificación.

---

## Racional de Diseño e Innovación

### 1. Codificación Visual y Metáfora Central
* **Mapamundi + Heatmap:** Aprovecha la dimensión geográfica inherente de los datos para permitir comparaciones regionales rápidas mediante la intensidad del color.
* **Metáfora del Corazón:** Al seleccionar un país, un corazón actúa como codificador secundario. Su tamaño, color y frecuencia de latido escalan proporcionalmente con la tasa de mortalidad.

### 2. Sonificación Emocional y Sensorial
* **Ritmo Audible:** El dato numérico se traduce en el pulso sonoro del corazón. A mayor mortalidad, más rápido e intenso es el latido, generando una conexión empática con los datos sin saturar al usuario.

### 3. Mecanismos de Interacción
* **Navegación Temporal:** Selector de años y cronología global para observar la evolución histórica.
* **Puntos de Interés (Contexto):** Hitos informativos que contextualizan los picos de mortalidad en momentos y lugares específicos.

---

## Origen y Procesamiento de Datos

* **Fuente:** API de World Bank Group (Tasa bruta de mortalidad).
* **Procesamiento:** Scripting en Python (`Google Colab`, `Pandas`, `Requests`).
* **Limpieza:** Integración de identificadores geográficos para el mapeo espacial.
* **Filtrado:** Filtrado temporal y jerárquico (eliminación de agregados continentales) para evitar sobrecarga cognitiva.
* **Sonificación:** Mapeo de pesos para la frecuencia de sonificación.

---

## Proceso de Evaluación e Itinerancia de Diseño

### Evaluación con Usuarios (Thinking Aloud)
Se realizaron pruebas de usabilidad con perfiles diversos (un experto en estadística y un usuario no técnico):
* **Hallazgos:** Los usuarios destacaron la coherencia intuitiva entre la velocidad del latido sonoro y las diferencias de tasa.
* **Necesidad de Contexto:** Surgió la necesidad de entender las causas detrás de las anomalías visuales.

### Mejoras e Impacto de la Retroalimentación
* **Escala del Proyecto:** Se evolucionó de una propuesta local (Chile) a un mapa global interactivo.
* **Inclusión de Contexto:** Se implementaron los puntos de interés e hitos históricos para explicar aumentos atípicos en la mortalidad.
* **Refactorización:** Simplificación del código HTML/JS para optimizar la fluidez de las animaciones y la respuesta sonora.

<br>

---
---

<br>

# Fisicalización del Proyecto

> **Fisicalización de Datos y Dispositivo Háptico (ESP32):** Un sistema de información físico-digital que transpone datos demográficos globales a estímulos táctiles y sonoros mediante un dispositivo vestible (*wearable*) controlado por microcontrolador.

---

## Enlaces del Proyecto

* **Código Fuente (GitHub):** [Repositorio InfoViz ESP32](https://github.com/DieguinBombin/InfoViz_ESP32)
* **Demostración en Video:** [Ver Interacción Física y Sonora en YouTube](https://www.youtube.com/watch?v=MFtW6a-tPfo)

---

## Propósito del Proyecto

El objetivo principal es trasladar un conjunto de datos demográficos abstractos (tasa bruta de mortalidad por cada 1.000 habitantes) hacia un canal somatosensorial continuo y auditivo.

Al conectar la magnitud cuantitativa a una respuesta física directa en el cuerpo del usuario, se disminuye la saturación visual típica de las pantallas bidimensionales y se genera una retención cognitiva más memorable y profunda del indicador analizado.

---

## Arquitectura Técnica y Sistema Háptico

### 1. Interacción Físico-Digital (Hardware & Web Server)
* **Microcontrolador ESP32:** Configurado como servidor web local utilizando el sistema de archivos `LittleFS`.
* **Procesamiento On-Device:** Procesa internamente el archivo `paises_esp32.csv` y sirve dinámicamente la interfaz en un HTML embebido.
* **Comunicación Asíncrona:** La interfaz móvil envía peticiones HTTP GET (`/set?escalar=X`) al hardware en tiempo real al seleccionar un país.

### 2. Fisicalización y Sonificación
* **Dispositivo Háptico de Muñeca:** Traduce la tasa de mortalidad en un patrón de pulsos eléctricos discretos (escala 0 a 20) aplicados en la muñeca del usuario vía actuación de relé.
* **Sonificación por Buzzer Activo:** Un buzzer simula latidos de corazón modulados dinámicamente en frecuencia dentro del bucle principal del firmware, sincronizándose con la tasa de mortalidad.

---

## Procesamiento y Optimización de Datos

* **Consolidación Scripting (Python):** Se procesó la base de datos histórica por país para consolidar registros y adaptar la estructura a las restricciones de memoria (RAM/Flash) y transferencia del ESP32.
* **Normalización Lineal:** Los datos se mapearon a una escala discreta del 0 al 20 directamente interpretable por el hardware.
* **Eficiencia de Red:** Reducción del *payload* en las peticiones HTTP para garantizar una latencia casi nula entre la interacción web y la respuesta física.

---

## Racional de Interacción Háptica (Data Physicalization)

* **Manipulación Directa:** Se basa en la teoría de interacción no convencional para externalizar fenómenos complejos.
* **Distribución de Carga Cognitiva:** Descarga el canal visual al permitir comparar magnitudes a través del sistema nervioso periférico sin necesidad de mirar fijamente una gráfica o escala numérica.

---

## Evaluación de Usabilidad y Retroalimentación

### Pruebas de Usuario (Thinking Aloud)
Se evaluó el prototipo con estudiantes de Ingeniería UC y profesionales del área tecnológica.
* **Percepción Sensorial:** Los usuarios identificaron de forma inmediata los patrones de pulsación al alternar entre países de baja y alta mortalidad.
* **Confirmación Háptica:** Se valoró la coherencia temporal e intuitiva entre la selección digital y la respuesta táctil/sonora en el brazo.

### Iteración y Mejoras Implementadas
* **Calibración de Firmware:** Ajuste de los tiempos de conmutación de los pulsos para suavizar la transición y evitar cambios abruptos en la estimulación.
* **Usabilidad Web Mobile:** Optimización de la legibilidad del selector de países y confirmación visual dinámica del estado de la petición HTTP GET.