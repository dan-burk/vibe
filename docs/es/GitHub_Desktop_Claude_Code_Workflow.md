[Inicio](index.html)

# Use GitHub Desktop con Claude Code

Usted está programando con asistencia de IA. Esta hace cambios en sus archivos. A veces los cambios funcionan perfectamente. A veces no. **El control de versiones es como un botón de deshacer para todo su proyecto.** Cada vez que guarda una instantánea (llamada "commit"), usted crea un punto de restauración. Siempre puede volver atrás.

Cuando combina [GitHub Desktop](https://desktop.github.com) con [Claude Code](https://claude.com/claude-code), obtiene desarrollo a velocidad de IA con control de versiones profesional.

## Conceptos Clave

**Git** rastrea cada cambio en sus archivos en su computadora.

**GitHub** almacena su código en la nube como respaldo.

**GitHub Desktop** hace que Git sea visual - usted hace clic en botones en lugar de escribir comandos.

**Claude Code** es un asistente de programación de IA que escribe código, corrige errores y crea commits por usted.

## Lo Que Hará

Construir una aplicación simple de temporizador con Claude Code y rastrear todos los cambios con GitHub Desktop:
- Crear proyecto y aplicación de temporizador
- Probar y corregir errores
- Hacer commit y push de los cambios
- Descartar cambios malos e intentar de nuevo
- Dejar que Claude automatice los commits

## Lo Que Necesitará

- Haber completado [Instalación de Claude Code en Windows](./Install_CLAUDE_Code_Win) o [Instalación de Claude Code en Mac](./Install_Claude_Code_MacOS)
- Haber completado [Introducción al Control de Versiones](./Github_desktop)
- 20 minutos

## Paso 1: Cree Su Proyecto

- Abra **GitHub Desktop**
- Haga clic en **File** → **New Repository**
- Complete:
  - **Name:** `test_claude`
  - **Description:** `A timer app built with Claude Code`
  - **Local Path:** carpeta Documents
  - **Marque** "Initialize this repository with a README"
- Haga clic en **Create Repository**
- Haga clic en **Publish repository** en la parte superior
- Haga clic en **Publish Repository**

Ahora tiene un proyecto local y un respaldo en la nube en GitHub.

## Paso 2: Solicite a Claude que Cree la Aplicación de Temporizador

- Abra su **terminal**
- Navegue a su proyecto:
  ```
  cd ~/Documents/test_claude
  ```
- Inicie Claude Code:
  ```
  claude
  ```
- Escriba esta solicitud:
  ```
  Create a simple countdown timer app in a single file called timer.html.
  It should have:
  - An input field to set minutes
  - Start and Stop buttons
  - Display showing time remaining in MM:SS format
  - When timer reaches zero, display 'Time's up!'
  Keep it simple with inline CSS and JavaScript.
  ```

Claude crea el archivo `timer.html` (toma 10-30 segundos).

## Paso 3: Pruebe el Temporizador

- En GitHub Desktop, haga clic en **Repository** → **Show in Finder/Explorer**
- **Haga doble clic** en `timer.html` para abrirlo en su navegador
- Pruebe el temporizador:
  - Escriba `1` en el campo de entrada
  - Haga clic en **Start**
  - Observe la cuenta regresiva

**Si funciona:** Continúe al Paso 5.
**Si algo está roto:** Continúe al Paso 4.

## Paso 4: Corrija Errores (Si Es Necesario)

- Abra la consola del navegador (haga clic derecho en la página → **Inspect** → pestaña **Console**)
- Copie cualquier mensaje de error en rojo
- Regrese a Claude Code en su terminal
- Pegue el error:
  ```
  I'm seeing this error: [paste error]. Can you fix it?
  ```
- Actualice el navegador (haga clic en el botón de recarga o clic derecho → **Reload**) y pruebe nuevamente

## Paso 5: Revise los Cambios

- Cambie a **GitHub Desktop**
- **Panel izquierdo:** Muestra los archivos modificados (`timer.html`)
- **Panel derecho:** Muestra el código (verde = agregado)
- Lea para entender lo que Claude creó

Siempre revise el código generado por IA antes de hacer commit.

## Paso 6: Haga Commit Manualmente

- En la parte inferior izquierda, en el campo **Summary**, escriba:
  ```
  Create initial timer app with start/stop functionality
  ```
- Haga clic en **Commit to main**

Ha creado un punto de guardado.

**Buenos mensajes:** "Create initial timer app", "Fix start button"
**Malos mensajes:** "changes", "update", "asdf"

## Paso 7: Haga Push a GitHub

- Haga clic en el botón **Push origin** en la parte superior
- Verifique: **Repository** → **View on GitHub** para ver su código en línea

Su código ahora está respaldado en la nube.

## Paso 8: Agregue Notificación de Sonido

- En el terminal de Claude Code:
  ```
  Add a sound notification when the timer reaches zero. Use the browser's
  built-in beep sound or create a simple audio alert.
  ```
- Pruebe: Actualice el navegador, configure el temporizador para 0.1 minutos, haga clic en Start

**Para este tutorial:** Finja que el sonido no funciona bien. No haga commit todavía.

## Paso 9: Descarte los Cambios Malos

Algunas veces la IA nos lleva por el camino equivocado y necesitamos empezar de nuevo desde nuestro último commit (punto de guardado).

- Abra **GitHub Desktop**
- Haga clic en el menú **Branch** → **Discard All Changes**
- Haga clic en **Discard Changes** para confirmar
- Actualice el navegador - el temporizador funciona sin el sonido

Acaba de desechar código que no funcionaba y volvió a su último punto de guardado.

## Paso 10: Rehaga Desde Cero

- En Claude Code:
  ```
  Add a sound notification when the timer reaches zero. This time, use an HTML5
  audio element with a simple beep sound generated by the Web Audio API. Make
  sure it handles browser autoplay restrictions gracefully.
  ```
- Pruebe inmediatamente (actualice el navegador, configure 0.1 minutos, Start)

**Si funciona:** Continúe al Paso 11.
**Si no:** Pegue el error a Claude o intente de nuevo.

## Paso 11: Permita que Claude Haga Commit y Push

- En Claude Code:
  ```
  commit and push my changes
  ```

Claude verificará los cambios, escribirá un mensaje de commit, hará commit y push (10-20 segundos).

**Cuándo usar:**
- Commits manuales: Cuando está aprendiendo o desea control
- Commits de Claude: Cuando trabaja rápido y desea buenos mensajes

## Paso 12: Solicite a Claude que Resuma los Cambios

- En Claude Code:
  ```
  what files have I changed?
  ```

Claude explica sus cambios en lenguaje sencillo.

**Intente:** `explain what the audio code does` o `show me the last 5 commits`

## Paso 13: Vea el Historial

- En **GitHub Desktop**, haga clic en la pestaña **History**

Verá:
- Initial commit (README)
- Create initial timer app
- Add improved sound notification

Note que el primer intento fallido de sonido no está ahí - lo descartó. Solo el código que funciona llegó a sus commits.

## Desafíos
- Sonido personalizado: Descargue un .mp3 gratuito de [freesound.org](https://freesound.org), póngalo en la carpeta de su proyecto, solicite a Claude que lo use
- Múltiples temporizadores: `Allow users to create and run multiple timers simultaneously`
- Barra de progreso: `Add a progress bar that visually shows how much time remains`

**Recuerde:** Pruebe después de cada característica, haga commit después de cada éxito, descarte los fallos.

**Vea su proyecto en GitHub.com:** Haga clic en **Repository** → **View on GitHub** en GitHub Desktop para ver su historial completo de commits y código en línea.

## Solución de Problemas

**"Authentication failed":** GitHub Desktop → File/Preferences → Accounts → cierre sesión y vuelva a iniciar sesión

**Claude dice "not a git repository":** Asegúrese de estar en la carpeta correcta (`cd ~/Documents/test_claude`)

**El temporizador no funciona:** Abra la consola del navegador (clic derecho → **Inspect** → **Console**), copie los errores, péguelos en Claude

**¿Necesita ayuda?** [Documentación de GitHub Desktop](https://docs.github.com/en/desktop) • [Documentación de Claude Code](https://docs.anthropic.com/en/docs/claude-code)

## El Flujo de Trabajo Completo

- Solicite a Claude que haga cambios
- Pruebe en el navegador
- Si funciona → Revise y haga commit
- Si falla → Descarte e intente de nuevo
- Haga push a GitHub
- Repita

Commits manuales cuando desea control. Commits de Claude cuando desea velocidad. Descarte sin miedo - solo haga commit de código que funciona.

## Próximos Pasos

Intente agregar características a su temporizador:

**Victorias rápidas:**
- Botones preestablecidos para 5, 10, 15 minutos: `Add three preset buttons: "5 min", "10 min", and "15 min"`
- Botón de pausa: `Add a Pause/Resume button that toggles the timer state`
- Mejor estilo: `Improve the visual design with a modern color scheme`

Creado por [Steven Ge](https://www.linkedin.com/in/steven-ge-ab016947/) el 7 de diciembre de 2025.
