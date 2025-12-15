[Inicio](index.html)

# Escriba un Artículo de Investigación con Claude Code

Escriba artículos de investigación utilizando Claude Code como asistente para investigar, generar ideas, planificar, redactar y editar. Luego automatice este proceso creando un slash command de plantilla. Vea un [ejemplo de artículo](./example_paper.md) creado usando este flujo de trabajo.

## Conceptos Clave

- **Flujo de trabajo** - Investigación → Lluvia de ideas → Investigación enfocada → Esquema → Borrador → Revisión manual → Pulir con IA → Agregar resumen → Mejorar título → Verificar referencias → Corrección con IA
- **Asistente de IA** - El humano toma las decisiones clave mientras la IA hace el trabajo tedioso
- **Claude Code** - Sistema de IA agéntica que busca en la web, organiza la investigación y redacta contenido mediante solicitudes simples
- **slash command** - Un prompt personalizado y detallado que puede reutilizarse en Claude Code

## Lo Que Necesitará

- Haber completado [Claude Code in VS Code on Windows](./Claude_Code_in_VS_Code_Win) o [Claude Code in VS Code on Mac](./Claude_Code_in_VS_Code_Mac)
- 30-40 minutos

## Paso 1: Crear una Carpeta de Proyecto

Cree una carpeta para su artículo de investigación:

- Abra **File Explorer** (Windows) o **Finder** (Mac)
- Navegue a **Documentos**
- Cree una nueva carpeta llamada `test_claude`

Todo sobre este proyecto ocurre en esta carpeta.

## Paso 2: Iniciar VS Code
Para Windows:
- Haga clic en el **botón Inicio de Windows** (esquina inferior izquierda de su pantalla)
- Escriba `Visual Studio Code` o `VS Code` en el cuadro de búsqueda
- Haga clic en **Visual Studio Code** cuando aparezca en los resultados de búsqueda
- VS Code se abre con una pestaña de Bienvenida - puede cerrar esta pestaña
- Mire la esquina inferior izquierda de VS Code - verá un icono azul o verde
- Haga clic en este icono para abrir el menú de conexión remota
- Seleccione **Connect to WSL** del menú
- VS Code se recargará y se conectará a su instalación de Ubuntu
- La esquina inferior izquierda ahora debería mostrar **WSL: Ubuntu**

Para Mac:
- Abra **Finder** y vaya a **Aplicaciones**
- Encuentre **Visual Studio Code** y haga doble clic en él
- Si ve una advertencia "Visual Studio Code es una aplicación descargada de internet", haga clic en **Abrir**
- VS Code se abre con una pestaña de Bienvenida - puede cerrar esta pestaña

## Paso 3: Abrir la Carpeta en VS Code
Para Windows vía WSL:
- En VS Code (todavía conectado a WSL), haga clic en **File** en la barra de menú, luego en **Open Folder**
- Aparece un menú desplegable **Open Folder** en el centro superior
- Encuentre su carpeta escribiendo:
  ```
  /mnt/c/Users/YOUR_USERNAME/Documents/test_claude
  ```
  Reemplace `YOUR_USERNAME` con su nombre de usuario de Windows (por ejemplo, `John.Smith`)
- Haga clic en **OK**. VS Code se recarga con su carpeta `test_claude`


Para Mac:
- En VS Code, haga clic en **File** en la barra de menú, luego en **Open Folder**
- Navegue y seleccione la carpeta `test_claude`
- Haga clic en **Open** (Mac) o **OK** (Windows)
- Si se le pregunta "Do you trust the authors?", haga clic en **Yes, I trust the authors**

## Paso 4: Iniciar Claude Code

- Abra un terminal: haga clic en **Terminal** en el menú principal de VS Code, luego en **New Terminal**
- En el panel de terminal, escriba:
  ```
  claude
  ```
- Claude Code se inicia y está listo para ayudar con su artículo de investigación

## Paso 5: Investigación Inicial

Pídale a Claude que investigue su tema. Copie y pegue este prompt en Claude Code, reemplazando el tema con el suyo propio:

```
I'm writing a ~1,000 word research paper on AI adoption in the workplace.
Search for recent data (2023-2025) on:
- Productivity gains from AI tools
- Job displacement concerns and statistics
- Real-world case studies from companies

Requirements:
- Prioritize peer-reviewed research and credible industry reports
- Avoid anecdotes and opinion pieces
- List each source with a 1-3 sentence summary
- Group sources by topic

Save as general_research.md
```

Claude busca en la web y organiza los hallazgos en un archivo llamado `general_research.md`. Esto puede tomar uno o dos minutos. Cuando complete, solicite un resumen:

```
Give me a brief summary.
```

Revise el resumen de Claude para obtener una vista rápida del panorama de investigación.

## Paso 6: Leer las Fuentes
Lea el documento de investigación y haga clic en las fuentes originales para verificar la información:

1. Haga clic en `general_research.md` en el panel Explorer a la izquierda
2. Previsualice el documento formateado: haga clic derecho en la pestaña `general_research.md` y seleccione **Open Preview**
3. Haga clic en los enlaces de las fuentes para leer los artículos y estudios originales

## Paso 7: Lluvia de Ideas Sobre Su Enfoque

Pídale a Claude que ayude con la lluvia de ideas:

```
Based on this research, suggest 3-4 angles I could take for this paper.
```

Revise los enfoques y elija el que más le interese.

## Paso 8: Investigación Enfocada

Ahora que tiene su enfoque, pídale a Claude investigación dirigida:

```
I want to focus on [your chosen angle]. Search for more specific data
and examples that support this perspective. Save as focused_research.md
```

Claude encuentra información específica.

## Paso 9: Crear Su Plan

Pídale a Claude que cree un esquema basado en su enfoque elegido:

```
Give me 3 options for a brief outline for my paper based on the focused
research and my chosen angle. Use bullet points for the narrative flow.
Save as outlines.md
```

Revise el esquema y pídale a Claude que lo ajuste según sea necesario (por ejemplo, "Make section 2 focus more on case studies" o "Add a section on limitations").

## Paso 10: Redactar el Artículo

Seleccione su esquema y pídale a Claude que escriba el borrador completo:

```
I like outline #2 [your chosen option].

Write a ~1,000 word research paper based on the outline and research.

Structure:
- Introduction: Hook, context, thesis statement
- Body: 2-3 sections with arguments, statistics, and examples
- Conclusion: Summary and implications

Style:
- Clear, concise sentences (15-20 words average)
- Active voice, analytical tone
- Statistics woven into prose (no bullet lists)
- Smooth transitions between paragraphs

Citations:
- Use numbered references [1], [2], etc. after claims
- Include 5-15 references
- Add a References section at the end

Save as paper.md
```

Claude escribe el borrador.

## Paso 11: Revisar Manualmente

Abra `paper.md` en su editor de texto. Lea cuidadosamente y haga sus propias revisiones:
- Agregue su voz personal y perspectivas
- Ajuste los argumentos para que coincidan con su pensamiento
- Corrija cualquier redacción incómoda
- Asegúrese de que las citas sean precisas

Guarde sus cambios en el editor.

## Paso 12: Pulir con IA

Pídale a Claude que mejore secciones específicas:

```
Make the introduction more engaging with a compelling hook.
```

## Paso 13: Agregar un Resumen

Pídale a Claude que agregue un resumen ejecutivo breve al principio:

```
Add an abstract at the beginning of the paper. Write 2-3 short sentences
that summarize the paper.
```

Claude agregará el resumen. Revise y edite para asegurarse de que capture con precisión la esencia de su artículo.

## Paso 14: Mejorar el Título

Pídale a Claude que le dé algunas opciones para el título:

```
Give me a few options for the title. Make it more appealing.
```

Seleccione un título. Agregue su toque personal:

```
I like option #2 [your choice]. Edit the file.
```

## Paso 15: Verificar Referencias (Opcional)
Pídale a Claude que verifique que sus citas sean consistentes y completas:
```
Check all references in my paper:
- Verify each citation number [1], [2], etc. has a matching reference
- Verify each reference in the list is actually cited in the paper
- Check that author names and titles are consistent
- Verify the cited data and examples appear in the source
```

Nota: Claude solo puede verificar fuentes de acceso público. Para artículos con acceso de pago, verifique manualmente que sus citas coincidan con lo que leyó.

## Paso 16: Corrección con IA

Pídale a Claude que haga una corrección final:

```
Do a final proofread of the paper:
- Fix any spelling and grammar errors
- Ensure consistent formatting throughout
- Check flow and transition
```

Revise los cambios de Claude.

**Exportar a Word:** En VS Code, haga clic derecho en la pestaña `paper.md` y seleccione **Open Preview**. Haga clic dentro del panel de vista previa, luego haga clic en **Edit > Select All** y **Edit > Copy**. Pegue en Microsoft Word—el formato se conservará.

## Paso 17: Crear un Slash Command para Futuros Artículos

Guarde este flujo de trabajo como un slash command reutilizable para su próximo artículo de investigación:

```
Create a slash command called /research-paper that guides me through
this entire workflow. Save it so I can use it for future research papers on various topics.
```

Claude creará un slash command personalizado en su carpeta `.claude/commands/`. Es un archivo Markdown que contiene un prompt. Puede comenzar su próximo artículo de investigación simplemente escribiendo `/research-paper [your topic]`!

## Paso 18: Obtener Retroalimentación

Los LLM no tienen memoria. Para cada respuesta, tenemos que enviar todas nuestras conversaciones anteriores en la sesión de chat para contexto. A medida que la interacción se hace más larga, debemos ser conscientes de la longitud del contexto. Si no está relacionado, o podemos proporcionar un contexto más limpio, nos beneficiaremos de un nuevo comienzo.

Limpie la memoria de Claude para obtener retroalimentación sobre su artículo. Escriba:

```
/clear
```

Esto elimina todo el historial de conversación, por lo que Claude leerá su artículo con ojos frescos. Ahora solicite retroalimentación:

```
Read paper.md and give me honest feedback.
```

Claude criticará su artículo sin estar influenciado por haberlo escrito. Haga las revisiones finales basándose en la retroalimentación.


## El Flujo de Trabajo Completo

1. **Crear Carpeta** - Configure su carpeta de proyecto en Documentos
2. **Abrir en VS Code** - Abra la carpeta en VS Code
3. **Iniciar Claude Code** - Lance Claude Code desde el terminal
4. **Investigar** - Claude busca información general sobre su tema
5. **Leer Fuentes** - Revise la investigación en su editor de texto
6. **Lluvia de Ideas** - Elija su enfoque/perspectiva
7. **Investigación Enfocada** - Claude encuentra datos específicos para su enfoque elegido
8. **Planificar** - Claude crea opciones de esquema basadas en su perspectiva
9. **Redactar** - Claude escribe el artículo completo con referencias
10. **Revisar Manualmente** - Usted agrega su voz y hace cambios
11. **Pulir con IA** - Claude mejora secciones específicas
12. **Agregar Resumen** - Claude crea un resumen ejecutivo
13. **Mejorar Título** - Claude sugiere opciones de título, usted personaliza
14. **Verificar Referencias** - (Opcional) Claude verifica todas las citas
15. **Corrección con IA** - Claude corrige errores y mejora el flujo
16. **Crear Slash Command** - Guarde el flujo de trabajo para futuros artículos
17. **Obtener Retroalimentación Fresca** - Limpie la memoria para una crítica imparcial

## Próximos Pasos

Ahora que tiene el slash command `/research-paper`, intente escribir más artículos:

- **Tecnología:** `/research-paper "Impact of social media on teen mental health"`
- **Negocios:** `/research-paper "Remote work productivity"`
- **Ciencia:** `/research-paper "CRISPR gene editing ethics"`
- **Formato:** Pídale a Claude `Give me the paper in LaTeX format`

¡El slash command lo guiará a través de todo el flujo de trabajo automáticamente! No olvide limpiar la memoria cuando esté cambiando de temas.

## Solución de Problemas

- **Los resultados de búsqueda de Claude parecen desactualizados:** Especifique "search for 2024-2025 data on [topic]"
- **El borrador es muy largo/corto:** Dígale a Claude: "Make this approximately 1,000 words"
- **No puede encontrar archivos:** En el terminal, escriba `ls` para listar todos los archivos en la carpeta actual

## Lo Que Puede Pedirle a Claude

- `search for more recent statistics on [topic]` - Encontrar datos más recientes
- `summarize the key arguments in this paper` - Obtener una vista general
- `make the conclusion more persuasive` - Mejorar secciones específicas
- `cite all sources in APA format` - Formatear referencias

¡Claude maneja la investigación y redacción a través de lenguaje natural—no hay comandos que memorizar!

---

Creado por [Steven Ge](https://www.linkedin.com/in/steven-ge-ab016947/) el 9 de diciembre de 2025.
