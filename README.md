# 🎙️ Motor de Lipsync Modular en Web Audio API (Costo Cero / CPU Pura)

Este repositorio contiene las pruebas operativas y el código base del sistema de sincronización labial (lipsync) modular desarrollado para **Xenogénesis / El Rincón de Sarah**. 

El objetivo es eliminar la dependencia de tarjetas gráficas dedicadas (NVIDIA) y servicios en la nube de pago por segundo (D-ID, HeyGen, etc.), sustituyéndolos por un pipeline desacoplado que corre directamente sobre el navegador o en OBS Studio con consumo marginal de CPU.

---

## ⚡ Demostraciones en Línea (GitHub Pages)

Puedes probar las dos versiones directamente en tu navegador sin instalar nada:

* 🟢 **[Nivel 1: Lipsync Reactivo de 2 Sprites (Umbral RMS)](https://tu-usuario.github.io/tu-repo/01_lipsync_sprites/)**
* 🟣 **[Nivel 2: Mapeo de 5 Visemas Fonéticos (FFT / A-E-I-O-U)](https://tu-usuario.github.io/tu-repo/02_lipsync_visemas/)**

---

## 🛠️ Arquitectura Técnica

1. **Desacoplamiento de Capas:** A diferencia de los modelos neuronales que redibujan el escenario y derriten la fisonomía del personaje, este sistema bloquea el fondo maestro y superpone únicamente los recortes PNG de los labios.
2. **Análisis de Señal Local:** Utiliza `Web Audio API` nativa:
   - **Nivel 1:** Calcula el valor cuadrático medio (RMS) del búfer de audio en tiempo real.
   - **Nivel 2:** Implementa `analyser.getByteFrequencyData()` para clasificar la energía espectral en bandas formantes (graves, medias y agudas) y proyectar la vocal correspondiente.
3. **Cero Dependencias:** Todo está escrito en HTML5, CSS3 y JavaScript vanilla. Sin Node.js ni librerías externas pesadas.

---

## 📁 Estructura del Repositorio

```text
├── index.html                  # Menú selector principal
├── 01_lipsync_sprites/         # Prototipo Nivel 1 (2 sprites)
│   ├── index.html
│   ├── app.js
│   └── assets/                 # PNGs boca abierta/cerrada y audio WAV
└── 02_lipsync_visemas/         # Prototipo Nivel 2 (5 visemas fonéticos)
    ├── index.html
    ├── app.js
    └── assets/                 # Sprites vocálicos (A, E, I, O, U)