# Rigmarole

Panel de After Effects que graba en MP4 el visor de la comp, con los nulls, los trazados de
movimiento, las cajas de las capas y los tiradores que un render deja fuera. Avanza el work area
fotograma a fotograma, captura la zona de la pantalla donde está la comp y une las capturas en un
vídeo con ffmpeg.

Gratuito, para Windows y macOS.

El nombre es la palabra inglesa *rigmarole*: un procedimiento largo y enrevesado. Empieza por
*rig*, y un rig visto por dentro es justo eso.

## Qué hace

- **Probar antes de grabar.** *Probar* enseña un fotograma tal como saldrá, antes de grabar el
  work area entero.
- **La comp o la ventana entera.** Graba solo la comp, o After Effects entero con el timeline y
  los paneles. Otros monitores y otros programas nunca entran en la captura.
- **Cuatro modos.** Estándar, Wireframe, Pantalla verde y Pantalla azul. Con los dos últimos
  quedan solo los tiradores y los trazados sobre un fondo que se recorta.
- **Con el audio.** Al terminar la captura, After Effects renderiza el audio del work area y se
  une al vídeo. Se puede quitar en Ajustes.
- **Tamaño en píxeles reales.** El vídeo mide lo que la comp en pantalla: la comp por el zoom del
  visor por la escala de la pantalla. El panel dice el tamaño antes de grabar, maximiza el visor
  mientras graba y, si la comp no cabe, propone el mayor tamaño que sí cabe.
- **La comp queda como estaba** al terminar, al cancelar o ante un error: selección de capas,
  zoom, guías, reglas, Fast Previews y Auto Save.
- **Si ffmpeg falla, no se pierde nada.** Los fotogramas capturados se conservan y se puede
  volver a codificar sin volver a grabar.

No graba en tiempo real. Cada fotograma espera a que After Effects termine de dibujarlo, y una
comp de 3 segundos a 24 fps tardó algo más de dos minutos en un equipo de pruebas con Windows. El
visor tiene que verse entero y sin nada encima mientras graba, porque cada fotograma es una
captura de pantalla.

## Requisitos

- After Effects 2022 (22.0) o posterior, en Windows o macOS (Intel o Apple Silicon).
- En macOS, el permiso de Grabación de pantalla para After Effects, en Preferencias del Sistema >
  Seguridad y privacidad. macOS lo pide la primera vez que se prueba un fotograma. Después de
  concederlo hay que reiniciar After Effects.

ffmpeg viene incluido para los dos sistemas. En Ajustes se puede cambiar por el del PATH (en
macOS, también el de Homebrew) o por cualquier otro que se elija.

## Instalación

### Instalación rápida (recomendada)

Cada [release](https://github.com/dony-aep/rigmarole/releases/latest) trae un `.zxp` firmado.
No necesita el modo de depuración ni claves del registro.

1. Descarga e instala el [ZXP/UXP Installer de aescripts + aeplugins](https://aescripts.com/learn/zxp-installer/),
   gratuito, para Windows y macOS.
2. Descarga `rigmarole-vX.Y.Z.zxp` de la última release.
3. Con After Effects cerrado, abre el `.zxp` en el instalador: arrástralo a la ventana o usa
   **File > Open**.
4. Abre After Effects y ve a **Window > Extensions > Rigmarole**.

Si el instalador dice que no encontró ninguna aplicación compatible y marca After Effects con
«Action required», es que el instalador de Adobe necesita la app de Creative Cloud abierta y con
sesión iniciada. Pulsa **Install Anyway**. Si falla, abre los ajustes del instalador (el icono
del engranaje), activa **Install for current user only** y vuelve a instalar.

### Instalación manual (zip)

1. Descarga y descomprime `rigmarole-vX.Y.Z.zip`.
2. Copia la carpeta `com.donyaep.Rigmarole` que trae en tu carpeta de extensiones CEP:
   - Windows: `%APPDATA%\Adobe\CEP\extensions\`
   - macOS: `~/Library/Application Support/Adobe/CEP/extensions/`
3. El zip no está firmado, así que CEP necesita el modo de depuración una vez:
   - Windows: doble clic en el `Add Keys.reg` del zip, o ejecuta
     `reg add "HKCU\Software\Adobe\CSXS.11" /v PlayerDebugMode /t REG_SZ /d 1 /f`
   - macOS: `defaults write com.adobe.CSXS.11 PlayerDebugMode 1 && killall cfprefsd`
4. Reinicia After Effects y abre **Window > Extensions > Rigmarole**.

## Uso

1. Abre una comp en el visor y ve a **Window > Extensions > Rigmarole**.
2. Elige un tamaño en *Tamaño*. Cada opción es un zoom del visor con el tamaño de vídeo que da.
3. Pulsa *Probar* para ver un fotograma y luego *Grabar* para grabar el work area.
4. Al terminar, el panel ofrece *Importar al proyecto*, *Mostrar en la carpeta* y
   *Abrir el vídeo*.

Los vídeos se guardan junto al archivo del proyecto, o en Vídeos (Películas en macOS) mientras el
proyecto no esté guardado. El botón *Ajustes*, arriba a la derecha, cambia la carpeta, qué
grabar, el modo, si se maximiza el visor, la pantalla donde buscar, el audio y ffmpeg.

Si un panel flotante, también el propio Rigmarole, tapa parte de la comp, *Probar* y *Grabar*
lo avisan en lugar de grabarlo encima. Acopla el panel o apártalo del visor.

## Licencia

Rigmarole es gratuito y se puede usar en proyectos personales y comerciales, pero no es de código
abierto: no se permite redistribuirlo ni modificarlo. Las condiciones están en [LICENSE](LICENSE).

Lleva dentro ffmpeg, que es GPL v2 o posterior y se ejecuta como un programa aparte. Su licencia
y de dónde sale su código fuente están en `bin/` dentro de la extensión, y los archivos de su
código fuente se adjuntan a cada release. Las licencias del resto de componentes de terceros
están en `THIRD_PARTY_NOTICES.txt`.
