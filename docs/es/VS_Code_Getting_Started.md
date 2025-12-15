[Inicio](index.html)

# Primeros Pasos con VS Code

Usted desea escribir código, pero Notepad o TextEdit se siente limitante. Necesita algo que le ayude a codificar más rápido, con resaltado de sintaxis, autocompletado y herramientas integradas. **VS Code es como un cuaderno inteligente para código**: entiende lo que está escribiendo y le ayuda en el camino. [Visual Studio Code](https://code.visualstudio.com) es gratuito, funciona en cualquier sistema operativo y es utilizado por millones de desarrolladores.

## Conceptos Clave

- **Editor** - El área principal donde escribe código
- **Explorer** - La barra lateral que muestra sus archivos y carpetas
- **Extensions** - Complementos que dan nuevas funciones a VS Code
- **Integrated Terminal** - Una línea de comandos integrada en VS Code

## Lo Que Necesitará

- Computadora con Windows, macOS o Linux
- Conexión a Internet
- ~500 MB de espacio en disco
- 20-25 minutos

## Paso 1: Descargue e Instale VS Code

- Vaya a [code.visualstudio.com](https://code.visualstudio.com)
- Haga clic en el botón **Download** (detecta su sistema operativo automáticamente)
- Ejecute el instalador:
   - **Windows:** Haga doble clic en el archivo `.exe`, haga clic en **Next** en las indicaciones
   - **Mac:** Abra el archivo `.dmg`, arrastre VS Code a **Applications**
   - **Linux:** Siga las instrucciones para su gestor de paquetes
- Inicie VS Code

Verá una pestaña de bienvenida con opciones para comenzar.

## Paso 2: Recorra la Interfaz

VS Code tiene cinco áreas principales:

- **Activity Bar** (borde izquierdo) - Iconos para Explorer, Search, Git, Extensions, etc.
- **Side Bar** - Muestra el contenido de la actividad seleccionada (archivos, resultados de búsqueda)
- **Editor** (centro) - Donde escribe código
- **Panel** (parte inferior) - Terminal, Problems, Output
- **Status Bar** (borde inferior) - Información sobre su archivo y proyecto

Haga clic en el icono **Explorer** (parte superior del Activity Bar) para ver el navegador de archivos.

## Paso 3: Abra una Carpeta y Explore

- Haga clic en **File** → **Open Folder**
- Navegue a cualquier carpeta existente en su computadora (por ejemplo, Documents)
- Haga clic en **Open** (o **Select Folder**)
- Si se le pregunta "Do you trust the authors?", haga clic en **Yes, I trust the authors**

La barra lateral Explorer ahora muestra los archivos de su carpeta:

- Haga clic en una carpeta para expandirla
- Haga clic en cualquier archivo para abrirlo en el editor
- Haga clic en el icono **Search** en el Activity Bar (lupa) para buscar en todos los archivos

## Paso 4: Cree un Archivo Markdown

- En Explorer, haga clic en el icono **New File** (página con +)
- Nómbrelo `README.md`
- Agregue este contenido:

```
# My Project

This is a **demo project** for learning VS Code.

## Features
- Easy to edit
- Markdown formatting
- Live preview

## Next Steps
1. Add more content
2. Try other file types
3. Explore extensions
```
- Haga clic en **File** → **Save** para guardar

Markdown es un formato de texto simple que usa símbolos como `#` para encabezados, `**` para negrita y `-` para listas. Es ampliamente utilizado para documentación y para comunicarse con LLMs como ChatGPT y Claude.

## Paso 5: Instale la Extensión Markdown Preview

- Haga clic en el icono **Extensions** en el Activity Bar (el icono de cuadrados)
- Escriba `Markdown Preview Enhanced` en el cuadro de búsqueda
- Encuentre **Markdown Preview Enhanced** en los resultados
- Haga clic en **Install**

## Paso 6: Previsualice Su Archivo Markdown

- Abra `README.md` si no está ya abierto
- Haga clic derecho en el editor y seleccione **Markdown Preview Enhanced: Open Preview to the Side**

Se abre un panel de vista previa que muestra su Markdown formateado: edite a la izquierda, vea los cambios a la derecha en tiempo real.

## Paso 7: Use el Terminal Integrado

- Haga clic en **Terminal** → **New Terminal**
- Pruebe estos comandos:

**Listar archivos:**
```
ls
```
(En Windows Command Prompt, use `dir`)

**Imprimir directorio de trabajo:**
```
pwd
```
(En Windows Command Prompt, use `cd`)

**Crear una nueva carpeta:**
```
mkdir notes
```

Revise Explorer: aparece la carpeta `notes`. El terminal se ejecuta en su carpeta de proyecto, por lo que los comandos afectan directamente su proyecto.

## Paso 8: Use Agentes de IA en VS Code (Opcional)

VS Code incluye [GitHub Copilot Chat](https://code.visualstudio.com/docs/copilot/chat/getting-started-chat), un asistente de IA que puede explicar, escribir y depurar código.

- Abra el archivo `README.md` (o cualquier otro archivo en su proyecto)
- Haga clic en **Chat** → **Open Chat** en la barra de título (o presione `Ctrl+Alt+I` en Windows/Linux, `Ctrl+Cmd+I` en Mac)
- Si se le solicita, inicie sesión con su cuenta de **GitHub** (hay un plan gratuito disponible)
- En el panel de chat que se abre, escriba: "Explain this file"
- Presione **Enter**

GitHub Copilot analizará su archivo y explicará qué hace. Puede pedirle que escriba código nuevo, corrija errores o responda preguntas como "How do I add more features?"

**Consejo:** Para [edición en línea](https://code.visualstudio.com/docs/copilot/copilot-chat), resalte código en cualquier archivo y presione `Ctrl+I` (Windows/Linux) o `Cmd+I` (Mac) para pedirle a Copilot que modifique, corrija o explique solo esa sección.

## Cómo Reabrir Su Proyecto

- Abra VS Code desde el menú Start (Windows), Spotlight (Mac) o Applications (Linux)
- Haga clic en **File** → **Open Recent** → seleccione su carpeta
- O haga clic en **File** → **Open Folder** y navegue hasta ella

## Solución de Problemas

- **La vista previa no se muestra:** Asegúrese de que la extensión Markdown Preview Enhanced esté instalada y tenga un archivo `.md` abierto
- **El terminal muestra el directorio incorrecto:** Haga clic en el icono de papelera en el panel del terminal, luego haga clic en **Terminal** → **New Terminal**
- **El menú Chat no es visible:** Es posible que GitHub Copilot Chat necesite instalarse: haga clic en el icono **Extensions**, busque "GitHub Copilot Chat" e instálelo
- **Las extensiones no funcionan:** Haga clic en **View** → **Command Palette**, escriba "reload window" y seleccione **Developer: Reload Window**

## El Flujo de Trabajo Completo

1. Abra una carpeta en VS Code
2. Cree/edite archivos
3. Use extensiones para previsualizar
4. Use el terminal para comandos
5. Use IA para entender y mejorar el código
6. Guarde y repita

## Próximos Pasos

- **Pruebe otros tipos de archivos:** Cree archivos `.html`, `.css`, `.js` o `.py` y vea el resaltado de sintaxis de VS Code
- **Explore las funciones de IA:** Pídale a la IA que escriba código, corrija errores o sugiera mejoras para sus proyectos
- **Instale más extensiones:** Pruebe "Prettier" para formato automático o "GitLens" para funciones de Git
- **Aprenda atajos:** Haga clic en **Help** → **Keyboard Shortcuts Reference** para acelerar su flujo de trabajo

---

Creado por [Steven Ge](https://www.linkedin.com/in/steven-ge-ab016947/) el 7 de diciembre de 2025.
