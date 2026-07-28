# Trópico Eternal

Proyecto universitario de un mod jugable de *Doom II*, ambientado en un escenario tropical, ejecutado directamente en el navegador mediante WebAssembly.

## Descripción

Trópico Eternal es una página web que permite jugar un mod personalizado de Doom II sin necesidad de instalar nada. La página carga el motor **PrBoom-plus** (compilado a WebAssembly con Emscripten), descarga los archivos del juego (IWAD, texturas y mapas), y los inyecta en el motor para iniciar la partida dentro de un `<canvas>`.

La interfaz está diseñada como un terminal táctico de campo/bunker tropical: encabezado tipo dossier militar, panel de "registro de arranque" con el progreso de carga en tiempo real, la pantalla del juego enmarcada con brackets de mira, botón de pantalla completa y un panel con los controles de teclado y ratón.

## Objetivo

**Objetivo general**

Desarrollar y desplegar en un navegador web un mod jugable de Doom II, integrando un motor de videojuegos compilado a WebAssembly con una interfaz web personalizada, aplicando conocimientos de desarrollo web (HTML, CSS, JavaScript) en la construcción de una experiencia interactiva multimedia.

**Objetivos específicos**

- Integrar el motor PrBoom-plus (compilado con Emscripten) dentro de una página web, sin requerir instalación local.
- Diseñar mapas y niveles personalizados (PWAD) con contenido original ambientado en un escenario tropical.
- Construir una interfaz web que cargue dinámicamente los archivos del juego (IWAD, texturas y mapas) vía JavaScript y los escriba en el sistema de archivos virtual del motor.
- Ofrecer retroalimentación visual del estado de carga y una guía de controles, para que cualquier persona pueda jugar sin conocimientos previos del proyecto.
- Aplicar buenas prácticas de diseño frontend (estética coherente, responsividad, accesibilidad básica).

## Estructura del proyecto

```
├── index.html            # Página web: interfaz, carga de archivos y arranque del motor
├── index.js              # Glue code generado por Emscripten (define la función prboom)
├── index.wasm            # Motor PrBoom-plus compilado a WebAssembly
├── index.data            # Recursos internos del motor (prboom-plus.wad + config por defecto)
├── doom2.wad              # IWAD base de Doom II (recursos comerciales originales)
├── s.wad                 # PWAD con texturas personalizadas
└── TROPICOETERNAL.wad     # PWAD con los mapas/niveles del mod
```

> Los tres primeros archivos (`index.js`, `index.wasm`, `index.data`) deben provenir siempre del mismo build de Emscripten — no son intercambiables entre versiones distintas del motor.

## Cómo ejecutarlo

El juego debe servirse desde un servidor web (no funciona abriendo el HTML directamente como archivo local, porque usa `fetch()` para cargar los `.wad`).

1. Copia toda la carpeta del proyecto a `htdocs` de XAMPP (o a cualquier servidor web local/remoto).
2. Verifica que **todos los archivos estén en la misma carpeta** que `index.html`, con los nombres exactos en minúsculas donde corresponda (`doom2.wad`, `s.wad`, `TROPICOETERNAL.wad`).
3. Inicia Apache desde el panel de control de XAMPP.
4. Abre en el navegador `http://localhost/<carpeta-del-proyecto>/index.html`.
5. Espera a que el panel de "registro de arranque" indique que el sistema está listo, haz clic sobre la pantalla del juego para enfocarlo y comienza a jugar.

## Controles

| Tecla        | Acción            |
|--------------|-------------------|
| `W A S D`    | Movimiento        |
| Ratón        | Apuntar / vista   |
| `Ctrl`       | Disparar          |
| `Espacio`    | Usar / abrir      |
| `Shift`      | Correr            |
| `Tab`        | Mapa táctico      |
| `1` – `7`    | Cambiar arma      |
| `Esc`        | Menú              |

## Tecnología utilizada

- **PrBoom-plus** — motor de código abierto compatible con Doom/Doom II.
- **Emscripten** — compilador usado para llevar el motor (C) a WebAssembly.
- **HTML / CSS / JavaScript** — interfaz web, carga de archivos y comunicación con el motor vía `Module.FS` y `Module.callMain`.

## Nota

Este es un proyecto académico, sin fines comerciales. `doom2.wad` corresponde al IWAD comercial original de Doom II y no se redistribuye como parte del código del proyecto; se asume que cada usuario dispone de su propia copia legítima del juego.
