[Inicio](index.html)

# Claude Code: Operaciones Básicas

Aprender a programar con asistencia de IA puede resultar abrumador al principio. Piense en Claude Code como un colega experto sentado junto a usted: usted describe lo que desea en español sencillo, y Claude le ayuda a llegar allí. Este tutorial le enseña las operaciones esenciales que utilizará diariamente, desde iniciar conversaciones hasta gestionar su espacio de trabajo.

## Conceptos Clave

- **Workspace** - Si inicia Claude Code desde una carpeta, esa es el espacio de trabajo de la sesión.
- **REPL (Read-Eval-Print Loop)** - Una sesión interactiva donde usted escribe comandos, Claude responde, y la conversación continúa hasta que usted salga.
- **Context** - La cantidad de código e historial de conversación que Claude recuerda; como memoria de trabajo que se llena con el tiempo.
- **Slash Commands** - Atajos incorporados que comienzan con `/` y realizan acciones específicas como limpiar el historial o mostrar ayuda.

## Lo Que Necesitará

- [Claude Code instalado](https://code.claude.com/docs/en/quickstart) con una suscripción activa a Claude Pro/Max o clave API
- Familiaridad básica con el uso de una terminal o símbolo del sistema
- Conexión a Internet
- 15-20 minutos

## Paso 1: Abra Su Terminal

- **Windows**: Presione la tecla Windows, escriba `Terminal` o `PowerShell`, y presione Enter
- **Mac**: Presione `Cmd+Space`, escriba `Terminal`, y presione Enter
- **Linux**: Presione `Ctrl+Alt+T` o encuentre Terminal en su menú de aplicaciones

Se abrirá una ventana de texto donde puede escribir comandos.

## Paso 2: Obtenga el Proyecto de Demostración

Utilizaremos un proyecto real de ciencia de datos para explorar las características de Claude Code. Puede clonarlo con Git o descargarlo directamente.

**Opción A: Clonar con Git (si tiene Git instalado):**

```
git clone https://github.com/gexijin/data_projects
cd data_projects
```

**Opción B: Descargar sin Git:**

- Visite [https://github.com/gexijin/data_projects](https://github.com/gexijin/data_projects) en su navegador web
- Haga clic en el botón verde **Code** cerca de la parte superior derecha
- Haga clic en **Download ZIP**
- Extraiga el archivo ZIP a una ubicación que recordará (como su Escritorio o carpeta Documentos)
- En su terminal, navegue a la carpeta extraída:
  - **Windows**: `cd C:\Users\SuNombre\Downloads\data_projects-main`
  - **Mac/Linux**: `cd ~/Downloads/data_projects-main`

Reemplace `SuNombre` con su nombre de usuario real y ajuste la ruta si lo extrajo en otro lugar.

## Paso 3: Inicie Claude Code desde la Carpeta

En su terminal (asegúrese de estar dentro de la carpeta data_projects), escriba:

```bash
claude
```

Verá un mensaje de bienvenida y el prompt de Claude Code.

## Paso 4: Haga Preguntas Sobre Su Proyecto

Claude Code lee automáticamente sus archivos cuando es necesario. Pruebe estas preguntas para entender su proyecto:

**Pregunte sobre la estructura de carpetas:**

```
What is the folder structure of this project?
```

**Pregunte sobre tecnologías:**

```
What technologies and libraries does this project use?
```

**Pregunte sobre cambios recientes:**

```
What was the last change made to this project?
```

Claude verificará el historial de Git (si está disponible) y le informará sobre los commits recientes.

Puede preguntarle a Claude cualquier cosa sobre su código en lenguaje natural. Claude lee archivos según sea necesario para responder sus preguntas.

## Paso 5: Slash Commands Esenciales

Escriba `/` y presione Enter para ver todos los comandos disponibles. Estos son los más importantes:

**Ver todos los comandos:**

```
/
```

Esto muestra un menú de todos los slash commands. Use las teclas de flecha para navegar, presione Enter para seleccionar, o presione Esc para cancelar.

**Obtener ayuda:**

```
/help
```
Muestra documentación sobre el uso de Claude Code.



**Verificar el uso de contexto:**
Es importante gestionar el contexto, la "memoria de trabajo" de Claude.

```
/context
```

**Limpiar el historial de conversación:**

Cuando el contexto se llena, inicie una nueva conversación con `/clear`.
```
/clear
```
Borra la conversación actual y comienza de nuevo. Use esto cuando desee cambiar de tema o cuando su conversación se vuelva demasiado larga. Es esencial para gestionar el contexto.


**Salir de Claude Code:**

```
/exit
```

Finaliza su sesión y regresa al prompt normal de la terminal. También puede presionar **Ctrl + C** dos veces.

## Paso 6: Atajos de Teclado

Estos atajos hacen que trabajar con Claude Code sea más rápido:

- **Shift+Tab** - Cambiar entre modo plan, edición o normal - Planifique primero para tareas complejas
- **Alt+Enter** (Windows/Linux) o **Option+Return** (Mac) - Agregar una nueva línea en su mensaje sin enviarlo
- **Ctrl+C** - Cancelar la operación actual o la respuesta de Claude
- **Ctrl+D** - Aprobar cambios en archivos cuando Claude solicite permiso
- **Esc** - Cerrar menús o cancelar la entrada actual

## Paso 7: Siempre Cree un Archivo CLAUDE.md

El archivo CLAUDE.md es el manual de instrucciones de su proyecto para Claude. Persiste a través de sesiones, por lo que Claude recuerda contexto importante sobre su proyecto.

**Cree el archivo:**

```
/init
```

Claude creará el archivo con un resumen de su proyecto. Este archivo permanece en la raíz de su proyecto y Claude lo lee automáticamente cada vez que inicia una nueva sesión.

Puede editar CLAUDE.md en la carpeta del proyecto en cualquier momento para agregar instrucciones específicas del proyecto, convenciones de codificación, o contexto importante como el propósito de los archivos, etc.

## Paso 8: Referirse a Archivos o Líneas de Código

Puede usar `@` para referirse a un archivo específico:

```
Explain the code in @Visualization/Matplotlib/Nested_Pie_Chart.ipynb
```

Claude leerá el notebook y explicará qué hace, cómo funciona, y qué logra el código. Esto efectivamente trae el archivo al contexto.

Si trabaja con Claude Code desde VS Code y tiene la extensión de Claude Code instalada, puede agregar el archivo al contexto simplemente abriéndolo. Verá en la parte inferior derecha de la ventana de comandos que dice `In Nested_Pie_Chart.ipynb`. Entonces Claude sabe que está hablando de este archivo.

Además, puede seleccionar unas pocas líneas de código y Claude mostrará **3 lines selected**. Puede pedirle a Claude que haga cambios rápidos a estas líneas o hacer preguntas. Por lo tanto, recomiendo encarecidamente usar Claude Code desde VS Code.


## Paso 9: Realice Acciones con Comandos de Linux

Claude puede realizar acciones ejecutando comandos de Linux de muchas formas.

- Instalar software
  ```
  Install the pandas library
  ```

- Iniciar control de versiones
  ```
  Start tracking changes using Git. My name is James Bond and my email is bond@earth.com
  ```
- Confirmar cambios
  ```
  Commit these changes.
  ```
- Encontrar y descargar datos
  ```
  Download the wine quality dataset from UCI. Put it in a new folder called wine.
  ```

- Ejecutar código
  ```
  Rewrite the nested pie chart code as a regular Python script.
  Run it and save the new code and plots in the same folder.
  ```

Podemos hacer esta pregunta vaga porque acabamos de pedirle que explique el código. Muchas cosas suceden después de esto. Claude instala software, soluciona errores, resuelve problemas de entornos - todo por su cuenta.



Esencialmente tiene un experto en comandos bash de Linux a su disposición. Mientras gestione los permisos y apruebe las acciones, puede ser muy productivo.

## Próximos Pasos

Ahora que conoce lo básico, pruebe esto por su cuenta:

- Pídale a Claude que explique un algoritmo de aprendizaje automático en una de las carpetas del proyecto
- Solicite modificaciones a un notebook existente (como cambiar colores de gráficos o agregar nuevas características)
- Cree un nuevo script de Python que use datos del proyecto
- Pídale a Claude que compare dos enfoques diferentes en el código base

## Solución de Problemas

- **Error "Command not found"** - Claude Code no está instalado o no está en su PATH. Ejecute `npm install -g @anthropic-ai/claude-code` para instalarlo.
- **Claude proporciona información desactualizada** - Limpie el contexto con `/clear` y pregunte nuevamente. Las conversaciones largas pueden llenar la memoria de Claude.
- **Los cambios en archivos no funcionan** - Asegúrese de tener permisos de escritura en su carpeta de proyecto. Claude solicitará aprobación antes de modificar archivos—presione Ctrl+D para aprobar.
- **El contexto se llena rápidamente** - Use `/context` para verificar el uso. Cuando esté casi lleno, use `/clear` para iniciar una conversación nueva con contexto limpio.

## Resumen del Flujo de Trabajo

Trabajar con Claude Code sigue este patrón:

- Inicie Claude en su carpeta de proyecto con `claude`
- Haga preguntas en lenguaje natural
- Claude lee archivos según sea necesario y responde
- Solicite cambios en el código—Claude pide permiso antes de modificar archivos
- Use `/clear` al cambiar de tema o cuando el contexto se llene
- Use `/exit` cuando termine

Creado por [Steven Ge](https://www.linkedin.com/in/steven-ge-ab016947/) el 14 de diciembre de 2025.
