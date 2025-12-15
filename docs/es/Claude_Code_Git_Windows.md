[Inicio](index.html)

# Claude Code con control de versiones para Windows

Está trabajando con asistencia de IA. Esta realiza cambios en sus archivos. A veces los cambios son brillantes. A veces no lo son. **El control de versiones es como un botón de deshacer para todo su proyecto.** Cada vez que guarda una instantánea (llamada "commit"), crea un punto de restauración al que siempre puede volver. Lo mejor de todo es que puede hacer esto completamente en su computadora y Claude Code lo hace por usted.

## Conceptos Clave

- **WSL (Windows Subsystem for Linux)** - Ejecuta herramientas de Linux como Git de forma nativa en Windows
- **Git** - Rastrea cada cambio en sus archivos en su computadora, creando puntos de restauración a los que puede volver en cualquier momento
- **Commit** - Una instantánea de su proyecto en un punto específico en el tiempo con una descripción de qué cambió
- **Claude Code** - Asistente de codificación de IA que escribe código, corrige errores y maneja operaciones de Git mediante solicitudes simples

## Lo Que Necesitará

- Haber completado [Instalación de Claude Code en Windows](./Install_CLAUDE_Code_Win)
- WSL y Ubuntu instalados
- 20 minutos

## Paso 1: Abra Ubuntu Terminal

- Haga clic en el menú **Start**
- Escriba `Ubuntu`
- Haga clic en **Ubuntu** para abrir la terminal

Verá un símbolo del sistema que termina con `$`.

## Paso 2: Instale Git

- Escriba este comando y presione Enter:
  ```
  sudo apt-get install git
  ```
- Cuando se le solicite, escriba su contraseña y presione Enter
- Espere a que se complete la instalación (10-30 segundos)
- Verifique que Git esté instalado:
  ```
  git --version
  ```

Debería ver algo como `git version 2.34.1`.

## Paso 3: Configure Git con Su Identidad

Git necesita saber quién es usted para los mensajes de commit.

- Configure su nombre y correo electrónico (pueden ser ficticios)
  ```
  git config --global user.name "Your Name"
  git config --global user.email "your.email@example.com"
  ```

Usar su nombre y correo electrónico le ayuda a identificar quién realizó los cambios cuando varias personas trabajan en esto.

## Paso 4: Navegue a una Carpeta de Windows

WSL puede acceder a sus archivos de Windows a través de `/mnt/c/`.

- Navegue a su carpeta de usuario de Windows:
  ```
  cd /mnt/c/Users/YOUR_USERNAME/Documents
  ```
  Reemplace `YOUR_USERNAME` con su nombre de usuario real de Windows.
- Verifique que está en el lugar correcto:
  ```
  pwd
  ```

Debería ver `/mnt/c/Users/YOUR_USERNAME/Documents`.

## Paso 5: Cree una Carpeta de Proyecto

- Cree una carpeta llamada `test_claude`:
  ```
  mkdir test_claude
  ```
- Navegue hacia ella:
  ```
  cd test_claude
  ```

Aquí es donde vivirá su proyecto.

## Paso 6: Inicie Claude Code

- Inicie Claude Code:
  ```
  claude
  ```

Claude Code se ejecuta y espera su solicitud.

## Paso 7: Solicite a Claude que Inicialice Git

- Escriba esta solicitud:
  ```
  Start tracking changes
  ```

Claude inicializa un repositorio de Git en su carpeta (toma 2-5 segundos). ¡Ahora tiene control de versiones!

## Paso 8: Construya la Aplicación de Temporizador

- En Claude Code, escriba:
  ```
  Create a simple countdown timer app in a single file called timer.html.
  It should have:
  - An input field to set minutes
  - Start and Stop buttons
  - Display showing time remaining in MM:SS format
  ```

Claude crea `timer.html` (toma 10-30 segundos) con el código CSS y JavaScript.

## Paso 9: Pruebe el Temporizador

- Abra Windows File Explorer
- Navegue a `Documents\test_claude`
- Haga doble clic en `timer.html` para abrirlo en su navegador
- Pruebe el temporizador:
  - Escriba `1` en el campo de entrada
  - Haga clic en **Start**
  - Observe la cuenta regresiva

**Si algo está roto:** En Claude Code, describa el error: `I'm seeing this error: [describe what happened]. Can you fix it?`

## Paso 10: Solicite a Claude que Haga un Commit

- En Claude Code, escriba:
  ```
  Save these changes.
  ```

Claude hará lo siguiente:
- Verificar qué archivos cambiaron
- Escribir un mensaje de commit descriptivo
- Crear el commit (toma 5-10 segundos)

¡Ha creado su primer punto de guardado! Siempre puede volver a esta versión funcionando.

## Paso 11: Agregue Botones Predefinidos

- En Claude Code, escriba:
  ```
  Add two buttons on the top. If I click on them it automatically starts 1- and 5-minute timers.
  ```
- Actualice la pestaña de su navegador
- Pruebe: Haga clic en el botón **5 min**
- Si funciona, haga commit de los cambios:
  ```
  Save these changes.
  ```

Creamos un segundo punto de guardado. Esta versión tiene los dos botones funcionando.


## Paso 12: Agregue Otro Botón

- En Claude Code, escriba:
  ```
  Add a 15-minute button.
  ```
- Actualice la pestaña de su navegador
- Pruebe: Haga clic en el botón **15 min**

**Para este tutorial:** Pretenda que el botón de 15 minutos no funciona correctamente. No haga commit todavía—practicaremos descartando cambios malos.

## Paso 13: Descarte los Cambios

A veces el código de la IA no funciona y necesita comenzar de nuevo desde su último punto de guardado.

- En Claude Code, escriba:
  ```
  discard these changes.
  ```
- Claude le pedirá confirmación
- Escriba `yes` y presione Enter
- Actualice su navegador—el botón de 15 minutos desaparece

Claude descarta los nuevos cambios que no nos gustan. ¡El temporizador funciona nuevamente con solo los botones de 1 y 5 minutos!

## Paso 14: Agregue Notificación de Sonido

- En Claude Code, escriba:
  ```
  Add a sound notification when the timer reaches zero.
  ```
- Actualice el navegador y pruebe después de que Claude termine (configure el temporizador para 0.1 minutos)
- Si funciona, haga commit de los cambios:
  ```
  Save these changes.
  ```

## Paso 15: Agregue un Botón de Posponer

- En Claude Code, escriba:
  ```
  The sound should continue until I click a button to snooze it.
  ```
- Actualice el navegador y pruebe después de que Claude termine (configure el temporizador para 0.1 minutos)
- Si funciona, haga commit de los cambios:
  ```
  Save these changes.
  ```

## Paso 16: Vea Su Historial de Commits

- En Claude Code, escriba:
  ```
  show my change history
  ```

Claude muestra sus commits en un formato legible. Verá:
- Su commit inicial de la aplicación de temporizador
- El commit de botones predefinidos (1 min y 5 min)
- El commit de notificación de sonido
- El botón de posponer.

¡Note que el intento del botón de 15 minutos no está ahí—lo descartó!

## Paso 17: Examine el Código

- En el navegador que muestra la aplicación, haga clic derecho y seleccione **View Page Source**
- Puede ver el código fuente para esto.
- En Claude Code, pregunte
  ```
  Explain this code. Just big picture.
  ```

## El Flujo de Trabajo Completo

- Solicite a Claude que realice cambios
- Pruebe
- Si funciona → Solicite a Claude que haga commit
- Si falla → Solicite a Claude que lo corrija.
- Incapaz de corregir → Descarte los cambios e intente nuevamente
- Repita

¡Siempre puede volver a cualquier commit. Descarte sin temor—solo haga commit del código que funciona!

## Próximos Pasos

Intente agregar más características a su temporizador:

- **Botón de 15 minutos:** `Add a working 15-minute preset button` (¡rehaga lo que descartamos!)
- **Botón de pausa:** `Add a Pause/Resume button that toggles the timer state`
- **Mejor estilo:** `Improve the visual design with a modern color scheme and larger fonts`
- **Barra de progreso:** `Add a visual progress bar showing time remaining`

Recuerde: Pruebe después de cada característica, haga commit después de cada éxito, descarte los fallos.

## Solución de Problemas

- **Error "not a git repository":** Asegúrese de estar en la carpeta test_claude (`cd /mnt/c/Users/YOUR_USERNAME/Documents/test_claude`)
- **No puede encontrar timer.html en Windows:** El archivo está en `C:\Users\YOUR_USERNAME\Documents\test_claude\timer.html`
- **Git solicita contraseña:** Escribió mal la contraseña de `sudo`—intente nuevamente con cuidado
- **El temporizador no funciona:** Abra la consola del navegador (haga clic derecho en la página, seleccione **Inspect**, haga clic en la pestaña **Console**), copie cualquier mensaje de error rojo, péguelos en Claude

## Lo Que Puede Preguntarle a Claude

- `what files have I changed?` - Ver cambios sin hacer commit
- `show me the diff` - Ver exactamente qué código cambió
- `explain what the timer code does` - Entender la implementación
- `create a branch called experiment` - Probar cambios riesgosos de manera segura
- `go back to the previous commit` - Deshacer todo desde el último commit

¡Claude maneja todas las operaciones de Git a través del lenguaje natural—no hay comandos que memorizar!

## Resumen del Flujo de Trabajo

- **Configuración:** Instale Git una vez, configure la identidad una vez
- **Desarrollo:** Claude escribe código, usted prueba en el navegador
- **Control de Versiones:** Claude maneja todas las operaciones de Git mediante solicitudes simples
- **Seguridad:** Descarte cambios malos en cualquier momento, vuelva a cualquier commit anterior
- **Local:** Todo permanece en su computadora, no se requiere cuenta ni internet

Creado por [Steven Ge](https://www.linkedin.com/in/steven-ge-ab016947/) el 8 de diciembre de 2025.
