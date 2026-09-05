# entrega3


Este módulo documenta el desarrollo y la implementación interactiva de un sintetizador multimodular diseñado en el entorno de programación visual **Max/MSP** (v9.1.5).

📋 Descripción del Proyecto

El proyecto consiste en un parche interactivo enfocado en el procesamiento de señales de audio en tiempo real y técnicas de síntesis. Integra tres módulos principales:
1. **Síntesis por Modulación de Amplitud (AM)** aplicada a un archivo de audio de entrada.
2. **Síntesis por Modulación de Frecuencia (FM)** aplicada a un segundo archivo de audio.
3. **Módulo de Grabación y Reproducción de Voz en Vivo**, que permite capturar entrada desde micrófono y manipular la velocidad de reproducción.


## 🛠️ Arquitectura y Componentes del Parche (`sintetizador.maxpat`)

### 1. Módulo Síntesis AM
- **Carga de Audio:** Utiliza `buffer~ cancion1` y `groove~ cancion1` para reproducir muestras locales mediante comandos de lectura (`open`, `loop 1`).
- **Modulador:** Un oscilador `cycle~` cuya frecuencia se controla dinámicamente mediante un Dial mapped con `scale 0. 127 1. 200.`.
- **Procesamiento:** Multiplicación de señales (`*~`) entre la señal del `groove~` y el modulador.
- **Salida:** Control de nivel dinámico mediante `live.gain~` directo al convertidor digital-analógico `dac~`.

 2. Módulo Síntesis FM
- **Carga de Audio:** Utiliza `buffer~ cancion2` y `groove~ cancion2`.
- **Modulador:** Generación de portadora y moduladora utilizando `scale 0 127 0.1 5.` conectado a `cycle~`.
- **Procesamiento:** Suma y multiplicación de señales en tiempo real (`+~`, `*~`) para alternar las frecuencias transportadoras del playback.
- **Salida:** Control de ganancia independiente con `live.gain~` y salida estéreo a `dac~`.

 3. Módulo Grabadora de Voz y Manipulación
- **Entrada de Audio:** Captura directa mediante `adc~`.
- **Almacenamiento:** Graba señales en tiempo real en un búfer de 15 segundos (`buffer~ grabadora 15000`) utilizando el objeto `record~`.
- **Reproducción y Control:** Uso de `groove~ grabadora` con un dial y un `scale 0 127 -2. 2.` para modificar la velocidad/pitch de reproducción (permitiendo reproducción normal, acelerada, desacelerada e inversa).
