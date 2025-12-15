[Inicio](index.html)

# Cree un Claude Skill para Investigación Médica

Mantenerse al día con la investigación médica significa navegar a través de densos artículos científicos llenos de jerga. Un Claude Skill es como tener un asistente de investigación que lee cientos de artículos y los explica en un lenguaje claro - en lugar de pasar horas buscando en PubMed y decodificando lenguaje técnico, usted hace una pregunta simple y obtiene un resumen claro basado en la ciencia más reciente.

En este tutorial, creará un Claude Skill que busca literatura médica revisada por pares. Primero creamos un script de Python para consultar PubMed. ¿La mejor parte? ¡Puede pedirle a Claude que haga todo el trabajo! ¡Claude tiene un Skill que crea Skills!

## Conceptos Clave

- **Claude Skill** - Una herramienta especializada que extiende las capacidades de Claude Code con instrucciones personalizadas, código y documentación almacenados en `.claude/skills/`
- **PubMed** - Base de datos gratuita de más de 35 millones de artículos de investigación biomédica mantenida por la Biblioteca Nacional de Medicina de EE.UU.
- **Biopython** - Biblioteca de Python que proporciona herramientas para consultar la base de datos de PubMed programáticamente
- **Modo auto-edit** - Función activada con Shift+Tab que permite a Claude realizar múltiples cambios en archivos sin pedir permiso cada vez

## Lo Que Necesitará

- Haber completado [Claude Code en VS Code en Windows](./Claude_Code_in_VS_Code_Win.md) o [Claude Code en VS Code en Mac](./Claude_Code_in_VS_Code_Mac.md)
- Conexión a Internet para búsquedas en PubMed
- 15-20 minutos

## Paso 1: Navegue a la Carpeta del Proyecto

Si completó el [tutorial de slash commands](./Reuse_Prompts_via_Slash_Commands.md), la carpeta `test_claude` ya existe. Estos comandos funcionan de cualquier manera.

**Windows (WSL):**
- Abra **Ubuntu** desde el menú Inicio
- Escriba estos comandos:
  ```bash
  cd /mnt/c/Users/YOUR_USERNAME/Documents
  mkdir -p test_claude
  cd test_claude
  ```
  Reemplace `YOUR_USERNAME` con su nombre de usuario de Windows

**Mac:**
- Abra **Terminal** (encuéntrelo en Aplicaciones > Utilidades)
- Escriba estos comandos:
  ```bash
  cd ~/Documents
  mkdir -p test_claude
  cd test_claude
  ```

La bandera `-p` crea la carpeta si no existe, o simplemente no hace nada si ya existe.

## Paso 2: Inicie Claude Code

Escriba este comando:
```bash
claude
```

Claude Code se inicia y muestra un mensaje de bienvenida.

## Paso 3: Active el Modo Auto-Edit

Presione **Shift+Tab** para activar el modo auto-edit. Verá un mensaje de confirmación.

El modo auto-edit permite a Claude crear y modificar múltiples archivos sin pedir permiso cada vez. Esto es esencial para construir skills que implican crear muchos archivos.

## Paso 4: Cree el Script de Búsqueda en PubMed

Copie y pegue este prompt:

```
Write a Python script called pubmed_search.py that:
- Takes a search query as command line argument
- Retrieves up to 10 recent papers
- Returns PMID, title, authors, journal, year, abstract preview, and URL
```
Claude crea el script. Instala el paquete Biopython requerido, que incluye un módulo entrez para interactuar con PubMed. Revise la salida para ver la estructura del script.

## Paso 5: Pruebe el Script

Pídale a Claude que lo pruebe:

```
Test the script with the query "immunotherapy breast cancer"
```

Claude ejecuta el script y muestra 10 artículos recientes sobre inmunoterapia para el cáncer de mama. Verá títulos, autores, resúmenes y enlaces de PubMed.

**Nota:** La búsqueda encuentra miles de artículos pero recupera solo los 10 más recientes para una revisión rápida.

## Paso 6: Cree el Skill de Investigación Médica

Ahora empaquetaremos todo en un skill reutilizable. Copie y pegue:

```
Create a Claude Skill called "medical-research" that:
- Takes on a medical question
- Designs queries to retrieve PubMed abstracts
- Creates plain-language summaries accessible to non-scientists
- Includes the pubmed_search.py script inside the skill folder
```

Claude crea la estructura completa del skill:
- `.claude/skills/medical-research/pubmed_search.py` - El script de búsqueda
- `.claude/skills/medical-research/SKILL.md` - Instrucciones para Claude sobre cómo usar el skill
- `.claude/skills/medical-research/README.md` - Documentación para el usuario
- `.claude/skills/medical-research/EXAMPLES.md` - Ejemplos de salidas

Esto toma 2-3 minutos ya que Claude escribe documentación completa.

## Paso 7: Pruebe el Skill

Haga una pregunta de investigación en lenguaje claro:

```
Can I lose weight via keto diet?
```

Claude automáticamente:
- Reconoce esto como una pregunta de investigación médica
- Activa el skill medical-research
- Busca en PubMed artículos relevantes
- Analiza los hallazgos
- Explica la investigación en lenguaje claro cubriendo efectividad, mecanismos y consideraciones

La respuesta incluye secciones como "How It Works," "Research Findings," "Important Considerations," y "The Bottom Line."

## Paso 8: Pruebe Otra Pregunta

Intente otro tema de investigación:

```
Does vaccine cause autism?
```

La respuesta explica el consenso científico, el origen del mito y las consecuencias en el mundo real.

## Paso 9: Explore los Archivos del Skill (Opcional)

Abra VS Code para ver la estructura del skill:

**Windows:**
- Abra **Explorador de Archivos**, navegue a `C:\Users\YOUR_USERNAME\Documents\test_claude`
- Haga clic derecho en la carpeta y seleccione **Open with Code**

**Mac:**
- Abra **Finder**, navegue a `Documents/test_claude`
- Haga clic derecho en la carpeta y seleccione **Open with Visual Studio Code**
- O simplemente escriba ``` code . ``` desde Terminal

En VS Code:
- Expanda `.claude/skills/medical-research/` en el explorador de archivos
- Abra `SKILL.md` para ver instrucciones detalladas para Claude
- Abra `README.md` para ver documentación del usuario
- Abra `pubmed_search.py` para ver el código Python

**Nota:** El skill es completamente autocontenido - todo el código y documentación viven en una carpeta.

## Paso 10: Instalación de Skills desde el Repositorio de Anthropic

Anthropic mantiene un repositorio de skills preconstruidos que puede instalar y usar instantáneamente.

- Para instalar un skill del repositorio, simplemente pídale a Claude:

  ```
  Install the document skill from Anthropic's repository
  ```
- Pruebe este skill:
  ```
  Create a PowerPoint presentation on Claude Skills.
  ```


El **document skill** le ayuda a leer y escribir archivos en PDF, Word, PowerPoint y Excel. Claude clonará el skill en su carpeta `.claude/skills/`.

**Otros skills disponibles del repositorio de Anthropic:**
- Explore el catálogo completo en [github.com/anthropics/claude-skills](https://github.com/anthropics/skills)
- Pregunte a Claude "What skills are available in the Anthropic repository?" para ver la lista actual

## Próximos Pasos

- **PDF:** Copie algunos archivos PDF en una subcarpeta en esta carpeta del proyecto y pida resúmenes.
- **Otros skills públicos:** Pruebe skills disponibles de Anthropic.
- **Comparta skills:** ¡Los skills son solo carpetas comprimidas!
- **Cree otros skills:** Cualquier cosa que le interese. Por ejemplo, puede poner sus propios archivos de datos en una carpeta de skill.

## Solución de Problemas

- **Biopython no instalado:** Claude instalará automáticamente Biopython cuando cree el script. Si ve errores de importación al probar, pídale a Claude que instale Biopython manualmente con `pip install biopython`
- **Script no encontrado:** Verifique que el modo auto-edit estaba activado (Shift+Tab) - Claude necesita permiso para crear archivos
- **El skill no se activa:** El skill debería funcionar inmediatamente después de la creación - intente hacer la pregunta de nuevo o verifique que SKILL.md tiene el `name: medical-research` correcto en el encabezado

## Descripción General del Flujo de Trabajo

- **Claude Skills** son más poderosos que los slash commands - combinan código, documentación e instrucciones personalizadas
- **Modo auto-edit** (Shift+Tab) agiliza la creación evitando solicitudes repetidas de permisos
- **Empaquetado autocontenido** - Los scripts viven dentro de las carpetas de skills, haciéndolos portátiles y compartibles
- **Activación automática** - Los skills se activan basándose en patrones de preguntas (preguntas de investigación activan medical-research)
- **Interfaz de lenguaje natural** - Haga preguntas naturales sin conocer los detalles técnicos

## Skills vs Slash Commands

| Característica | Skills | Slash Commands |
|---------|--------|----------------|
| **Qué contiene** | Prompts, código, datos y documentación | Solo prompts |
| **Activación** | Se cargan automáticamente cuando son relevantes | Se activan manualmente con `/command` |
| **Caso de uso** | Flujos de trabajo complejos que requieren ejecución de código | Plantillas de prompts rápidos y flujos de trabajo |
| **Ubicación de archivo** | `.claude/skills/skill-name/` | `.claude/commands/` |
| **Estructura** | Múltiples archivos (SKILL.md, README.md, archivos de código) | Un solo archivo `.md` por comando |

**Conclusión Clave:** Los Slash Commands solo inyectan prompts desde la interfaz de usuario. Es útil, pero limitado.

---

Creado por [Steven Ge](https://www.linkedin.com/in/steven-ge-ab016947/) el 13 de diciembre de 2025.
