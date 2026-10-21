# Registro de cambios

Todos los cambios notables de Rigmarole se documentan en este archivo.

El formato está basado en [Keep a Changelog](https://keepachangelog.com/es-ES/1.1.0/),
y este proyecto sigue el [Versionado Semántico](https://semver.org/lang/es/).

## [1.0.0] - 2026-10-21

Primera versión.

### Añadido

- **Grabar el visor en MP4.** La comp se graba tal como se ve en el visor, con los nulls, los trazados de movimiento, las cajas de las capas y los tiradores que un render deja fuera: un fotograma de vídeo por cada fotograma del work area, a los fps de la comp y en H.264.
- **Probar un fotograma antes.** *Probar* enseña un fotograma tal como saldrá, para comprobar el encuadre y el tamaño antes de grabar el work area entero.
- **La comp o la ventana entera.** Graba solo la comp, o After Effects entero con el timeline y los paneles. Otros monitores y otros programas nunca entran en la captura.
- **Cuatro modos.** Estándar, Wireframe, Pantalla verde y Pantalla azul. Con los dos últimos quedan solo los tiradores y los trazados sobre un fondo que se recorta.
- **Encuentra la comp solo.** Funciona en cualquier monitor y con cualquier escala de pantalla, sin indicarle esquinas ni pantalla. El tamaño del vídeo se elige con el zoom del visor y se ve en píxeles reales antes de grabar, y el visor se maximiza mientras graba para que quepan tamaños mayores. Si la comp no cabe, el panel dice cuánto sitio queda y propone el mayor tamaño que cabe. Si un panel flotante tapa parte de la comp, lo avisa en lugar de grabarlo encima.
- **Cada fotograma completo.** Cada fotograma se captura cuando After Effects ha terminado de dibujarlo, también cuando pinta primero los tiradores y la imagen un momento después, así que no se cuela ni un fotograma a medias ni el anterior. Los fotogramas iguales al anterior, como una pausa, se copian sin esperar.
- **Audio.** Al terminar la captura, After Effects renderiza el audio de la comp en el work area y se une al vídeo. Se puede quitar en Ajustes.
- **La comp queda como estaba.** La selección de capas, el zoom, las guías, las reglas, Fast Previews y Auto Save vuelven a su estado al terminar, al cancelar o ante un error. Si After Effects se cierra a mitad de una grabación, Auto Save se reactiva la próxima vez que se abre el panel.
- **Si ffmpeg falla, no se pierde nada.** Los fotogramas capturados se conservan y la codificación se puede reintentar sin volver a grabar.
- **Dónde va el vídeo.** Encima del botón Grabar se ven la carpeta y el nombre del archivo. Si ya existe, el panel pregunta antes: guardarlo con un número («Comp 1 2.mp4») o reemplazarlo. Al terminar, el vídeo se puede importar al proyecto, mostrar en su carpeta o abrir.
- **El progreso mientras graba.** El último fotograma capturado y el tiempo que falta, calculado con los fotogramas ya grabados.
- **ffmpeg incluido.** Uno mínimo para Windows y uno universal para macOS (Intel y Apple Silicon), sin instalar nada. En Ajustes se puede cambiar por el del PATH, el de Homebrew en macOS o cualquier otro.
- **Windows y macOS en un mismo paquete.** En macOS, si After Effects no tiene permiso de Grabación de pantalla, el panel lo dice y explica dónde concederlo.
- **Los ajustes sobreviven a las actualizaciones.** Se guardan fuera de la caché de After Effects, así que actualizarlo o limpiar los archivos temporales no los borra.
- **El panel sigue a la comp activa.** Ve cuándo se abre, se cierra o se cambia de comp sin tener que hacer clic en él.

[1.0.0]: https://github.com/dony-aep/rigmarole/releases/tag/v1.0.0
