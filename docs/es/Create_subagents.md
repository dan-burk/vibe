[Inicio](index.html)

# Cree un Subagente en Claude Code

Usted desea comparar oportunidades de inversión, pero investigar múltiples empresas y evaluarlas toma horas. Piense en un subagente como contratar a un analista financiero que sabe exactamente cómo usar sus herramientas de investigación—usted le da nombres de empresas, y ellos recopilan informes, evalúan cada empresa según métricas clave, y recomiendan la mejor inversión. Una vez que aprenda a construir subagentes, podrá automatizar cualquier flujo de trabajo repetitivo de múltiples pasos en su trabajo. Este tutorial le muestra cómo construir ese analista.

## Conceptos Clave

- **Subagente** - Un trabajador de IA especializado con su propio objetivo, prompt de sistema, y herramientas que completa tareas de forma autónoma
- **Skill** - Una capacidad reutilizable (como generar informes de acciones) que los subagentes pueden invocar para lograr sus objetivos
- **System Prompt** - Instrucciones que definen qué hace el subagente, cómo evalúa empresas, y qué formato devuelve
- **Separación de Responsabilidades** - Los skills recopilan datos; los subagentes usan esos datos para tomar decisiones

## Lo Que Necesitará

- Haber completado [Claude Code en VS Code en Windows](./Claude_Code_in_VS_Code_Win.md) o [Claude Code en VS Code en Mac](./Claude_Code_in_VS_Code_Mac.md)
- El skill de informe de acciones ya instalado (en `.claude/skills/generate-stock-reports/`)
- VS Code u otro editor de texto
- 20-25 minutos

## Paso 1: Cree una Carpeta de Proyecto e Inicie Claude Code

**Windows (WSL):**
- Abra **Ubuntu** desde el menú Inicio
- Escriba estos comandos:
  ```bash
  cd /mnt/c/Users/YOUR_USERNAME/Documents
  mkdir stock_picker_test
  cd stock_picker_test
  ```
  Reemplace `YOUR_USERNAME` con su nombre de usuario de Windows
- Inicie Claude Code:
  ```
  claude
  ```

**Mac:**
- Abra **Terminal** (encuéntrelo en Aplicaciones > Utilidades)
- Escriba estos comandos:
  ```bash
  cd ~/Documents
  mkdir stock_picker_test
  cd stock_picker_test
  ```
- Inicie Claude Code:
  ```
  claude
  ```

Claude Code se inicia y muestra un mensaje de bienvenida.

## Paso 2: Verifique que Existe el Skill de Informe de Acciones

Antes de construir su subagente, confirme que el skill está disponible. Escriba:

```
List all available skills
```

Debería ver `generate-stock-reports` en la salida. Este skill investiga empresas y genera informes que cubren noticias de productos, actualizaciones de gestión, desempeño financiero, y perspectivas de analistas.

Si no lo ve, los archivos del skill deberían estar en `.claude/skills/generate-stock-reports/` (nivel de proyecto).

## Paso 3: Comprenda la Arquitectura de Subagente vs Skill

Así es como los subagentes y skills trabajan juntos:

| Componente | Propósito | Ejemplo |
|-----------|---------|---------|
| **Skill** | Recopila datos sin procesar sobre una empresa | "Genere informe para Apple: productos, finanzas, gestión, analistas" |
| **Subagente** | Usa datos del skill para lograr un objetivo | "Obtenga informes para Apple y Microsoft, evalúe ambos, recomiende en cuál invertir" |

**Diferencia clave:**
- **Skill = herramienta** que hace investigación
- **Subagente = tomador de decisiones** que usa la herramienta y aplica lógica

Su subagente selector de acciones:
1. Invocará el skill de informe de acciones para cada empresa (2+ veces)
2. Evaluará empresas según categorías (finanzas, crecimiento, gestión, sentimiento)
3. Comparará puntuaciones y recomendará la mejor inversión

## Paso 4: Cree el Subagente Selector de Acciones

Escriba este comando:

```
/agents
```

Verá la interfaz de agentes de Claude Code mostrando subagentes existentes (si los hay) y opciones para **Crear**, **Editar**, o **Eliminar** subagentes.

Ahora cree su subagente:
- Seleccione **Create new subagent**
- Seleccione **Project**
- Seleccione **Generate with Claude (recommended)**
- Pegue lo siguiente para las instrucciones:
  ```
  Create a markdown file for a new subagent called stock-picker:
  - It takes two or more stocks
  - Uses the generate-stock-reports skill to do research
  - Score cards are created based on the categories of data collected
  - A final recommendation is given.
  ```
- Presione **Enter** en **[Continue]** para usar **All tools**
- Seleccione **Sonnet** para el modelo
- Presione **Enter** para elegir un color al azar

## Paso 5: Revise lo que Construyó (Punto de Reflexión)

Para abrir el archivo en VS Code, haga clic en **File > Open File...** y navegue a `.claude/agents/stock-picker.md`.

O puede pedirle a Claude:
```
Show me the stock-picker subagent file.
```
Claude mostrará el archivo del subagente ubicado en `.claude/agents/stock-picker.md`. Verá:

Hay un **YAML frontmatter** en la parte superior:
```
---
name: stock-picker
description: Compares multiple companies for investment decisions...
skills: generate-stock-reports
---
```

Este frontmatter (la sección entre marcadores `---`) le dice a Claude Code cuándo activar este subagente y qué skills puede usar.

Hay un **System prompt** debajo del frontmatter con su metodología de puntuación.

**Confirme estos elementos clave:**
- El subagente tiene acceso al skill `generate-stock-reports`
- El system prompt explica el desglose de puntuación
- El objetivo del subagente es claro: comparar empresas y recomendar una

Puede editar el archivo directamente o pedirle a Claude que lo actualice.

## Paso 6: Pruebe el Subagente

Ahora pruebe su subagente con una comparación real. Escriba:

```
Which is a better investment: Apple or Google?
```

El subagente se activará automáticamente según su descripción.

## Paso 7: Observe Cómo Trabaja el Subagente

Mientras el subagente se ejecuta, verá que:
1. **Invoca el skill dos veces** - Llama al skill generate-stock-reports una vez para Apple, luego para Google
2. **Recopila datos** - Cada llamada al skill busca en la web y genera un informe de empresa
3. **Evalúa empresas** - Aplica la ponderación 40/30/20/10 entre categorías
4. **Genera salida** - Crea tabla de comparación y recomendación

Esto puede tomar 2-3 minutos ya que involucra investigación web.

## Paso 8: Revise la Salida

El subagente devuelve un análisis detallado que incluye:
- **Informes individuales de empresas** - Actualizaciones de productos, métricas financieras, cambios de gestión, sentimiento de analistas para cada acción
- **Cuadro comparativo de puntuaciones** - Puntuaciones numéricas entre categorías (Salud Financiera, Potencial de Crecimiento, Calidad de Gestión, Sentimiento de Mercado)
- **Recomendación final** - En qué acción invertir y por qué

El subagente puede mostrar esto en el terminal o generar un archivo markdown con el informe completo. Puede editar el archivo del subagente para personalizar las ponderaciones de puntuación o el formato de salida.

## Próximos Pasos

Ahora que tiene un subagente selector de acciones funcional, pruebe estas extensiones:

- **Compare 3+ acciones**: "Compare AAPL, MSFT, and GOOGL" para ver cómo el subagente maneja más opciones
- **Ajuste ponderaciones de puntuación**: Edite el archivo del subagente para cambiar el desglose 40/30/20/10 (ej., haga que el crecimiento sea 40% si prefiere acciones de crecimiento)
- **Cree otros subagentes**: Construya un subagente "code-reviewer", subagente "bug-hunter", o subagente "document-writer" para diferentes tareas

## Solución de Problemas

- **Subagente no se activa**: Asegúrese de que su solicitud mencione comparar empresas o decisiones de inversión. Intente: "Use the stock-picker subagent to compare..."
- **Skill no encontrado**: Verifique que `.claude/skills/generate-stock-reports/SKILL.md` existe. Reinicie Claude Code si acaba de agregarlo.
- **Puntuaciones incompletas**: Pida al subagente que "continue" o "explain the scores for each category in more detail"
- **Error al crear subagente**: Verifique que la carpeta `.claude/agents/` existe. Claude Code debería crearla automáticamente.

## Resumen del Flujo de Trabajo

- **Los subagentes automatizan flujos de trabajo de múltiples pasos** - Orquestan skills, aplican lógica, y entregan decisiones
- **Los skills son herramientas reutilizables** - Un skill puede ser usado por múltiples subagentes para diferentes objetivos
- **Los system prompts definen el comportamiento** - Instrucciones claras y criterios de puntuación hacen que los subagentes sean confiables
- **Los subagentes mantienen el enfoque** - Cada subagente tiene un propósito único y claro (selección de acciones, revisión de código, etc.)
- **La composición escala** - Construya una biblioteca de skills y subagentes que trabajen juntos

---

Creado por [Steven Ge](https://www.linkedin.com/in/steven-ge-ab016947/) el 14 de diciembre de 2025.
