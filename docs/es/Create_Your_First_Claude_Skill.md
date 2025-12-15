[Inicio](index.html)

# Cree Su Primera Claude Skill

Ha estado escribiendo manualmente `/stock-report AAPL` para generar informes. ¿Qué pasaría si Claude pudiera decidir automáticamente cuándo crear un informe de acciones basándose en su conversación? Ese es el poder de las Skills: es como actualizar de un cambio de marchas manual a una transmisión automática que cambia cuando es necesario.

## Conceptos Clave

- **Skill** - Una capacidad invocada por el modelo almacenada en `.claude/skills/` que Claude activa automáticamente según el contexto
- **Invocada por el modelo** - Claude decide cuándo usar la Skill leyendo su descripción, sin que usted escriba un comando
- **SKILL.md** - El archivo principal que contiene el frontmatter YAML (metadatos) e instrucciones para Claude

## Lo Que Necesitará

- Tutorial completado: [Crear Comandos Slash Personalizados](./Reuse_Prompts_via_Slash_Commands.md)
- El comando slash `stock-report` de ese tutorial
- VS Code instalado
- 10-15 minutos

## Paso 1: Navegue a la Carpeta del Proyecto

**Windows (WSL):**
- Abra **Ubuntu** desde el menú Inicio
- Escriba:
  ```bash
  cd /mnt/c/Users/YOUR_USERNAME/Documents/test_claude
  ```
  Reemplace `YOUR_USERNAME` con su nombre de usuario de Windows

  Si la carpeta no existe, créela primero:
  ```bash
  mkdir -p /mnt/c/Users/YOUR_USERNAME/Documents/test_claude
  cd /mnt/c/Users/YOUR_USERNAME/Documents/test_claude
  ```

**Mac:**
- Abra **Terminal** (Aplicaciones > Utilidades)
- Escriba:
  ```bash
  cd ~/Documents/test_claude
  ```

  Si la carpeta no existe, créela primero:
  ```bash
  mkdir -p ~/Documents/test_claude
  cd ~/Documents/test_claude
  ```

## Paso 2: Inicie Claude Code

Escriba:
```
claude
```

Claude Code se inicia y muestra el mensaje de bienvenida.

## Paso 3: Active Auto-Aprobar para Ediciones

Presione `Ctrl+E` (Windows/Linux) o `Cmd+E` (Mac) para habilitar el modo de auto-aprobación para ediciones.

Esto permite que Claude cree y modifique archivos sin pedir permiso cada vez.

## Paso 4: Pídale a Claude que Convierta el Comando Slash

Escriba este prompt:
```
Convert my stock-report slash command to a Skill called generate-stock-reports.
The Skill should activate automatically when I ask about companies or stocks.
```

Claude analiza su comando slash existente y lo convierte en una Skill en `.claude/skills/stock-report/`.

**Lo que sucede:** Claude crea una nueva estructura de carpetas con `SKILL.md` que contiene el frontmatter YAML que le indica a Claude cuándo usar automáticamente esta Skill.

## Paso 5: Revise la Estructura de la Skill

Abra VS Code y vea el proyecto:
- Haga clic en **File > Open Folder**
- Seleccione `Documents/test_claude`
- En el explorador de archivos, navegue a `.claude/skills/stock-report/`
- Haga clic en `SKILL.md` para abrirlo

Note la estructura:
```yaml
---
name: stock-report
description: Generates reports on companies... Use when users ask about stocks, companies, or ticker symbols.
---

[Rest of the instructions]
```

El campo `description` es la clave: le dice a Claude exactamente cuándo activar esta Skill automáticamente.

## Paso 6: Pruebe la Skill (Sin Escribir un Comando)

En lugar de escribir `/stock-report AAPL`, simplemente haga una pregunta natural:
```
What's happening with Apple lately?
```

**La diferencia clave:** No escribió un comando. Claude lee su pregunta, reconoce que está preguntando sobre una empresa, verifica las descripciones de las Skills y decide automáticamente usar la Skill stock-report.

Observe cómo trabaja Claude: debería generar el mismo informe completo que vio antes.

## Paso 7: Compare los Dos Enfoques

**Comando Slash (Manual):**
```
/stock-report AAPL
```
- Usted le dice explícitamente a Claude qué hacer
- Siempre es igual
- Bueno para tareas repetitivas y predecibles

**Skill (Automática):**
```
Tell me about Tesla's recent developments
```
o
```
I'm thinking about investing in Microsoft
```
o
```
What's NVIDIA up to?
```
- Claude decide si usar la Skill
- Conversación más natural
- Bueno para flujos de trabajo complejos que Claude administra por usted

## Paso 8: Pruebe Casos Límite

Pruebe preguntas que NO deberían activar la Skill de informe de acciones:
```
How do I install Python?
```

Claude responde normalmente sin invocar la Skill.

Ahora pruebe una pregunta que SÍ debería activarla:
```
Compare Google and Meta
```

Claude debería usar la Skill dos veces: una para Google, una para Meta.

## Paso 9: Modifique la Descripción de la Skill (Opcional)

Hagamos que la Skill sea más selectiva. Pídale a Claude:
```
Update the stock-report Skill to only activate when I explicitly mention
"analyze" or "report" along with a company name.
```

Claude actualiza el campo `description` en `SKILL.md`. Pruebe la diferencia:
```
What's Apple doing?
```
(Puede que no active la Skill ahora)

```
Analyze Apple
```
(Debería activar la Skill)

## Próximos Pasos

Ahora que entiende las Skills, cree más para sus flujos de trabajo:

- **Research Skill** - Se activa automáticamente cuando hace preguntas que requieren investigación web
- **Code Review Skill** - Se activa cuando menciona errores, problemas o problemas de código
- **Meeting Notes Skill** - Se activa cuando pega transcripciones de reuniones o menciona resúmenes

El patrón: Defina cuándo Claude debería ayudar automáticamente, no solo atajos que usted activa manualmente.

## Solución de Problemas

- **La Skill no se activa:** Verifique el campo `description` en `SKILL.md`: debe incluir palabras clave relacionadas con su pregunta
- **La Skill se activa con demasiada frecuencia:** Haga la descripción más específica sobre cuándo usarla
- **No puede encontrar la carpeta de la Skill:** Las Skills están en `.claude/skills/` (carpeta oculta: habilite "Mostrar archivos ocultos" en su explorador de archivos)
- **Los cambios en SKILL.md no funcionan:** Las Skills se cargan automáticamente cuando se modifican: no es necesario reiniciar. Si aún no funciona, verifique el formato YAML

## Descripción General del Flujo de Trabajo

- **Los comandos slash** son atajos que usted escribe manualmente (como marcadores)
- **Las Skills** son capacidades que Claude descubre y usa automáticamente (como un asistente que conoce sus preferencias)
- **Las descripciones de Skills** actúan como instrucciones que le dicen a Claude: "Úsame cuando el usuario diga X"
- **Ambos pueden coexistir** - Use comandos slash para tareas rápidas y repetitivas; use Skills para flujos de trabajo complejos
- **Las Skills escalan mejor** - No necesita recordar nombres de comandos; Claude decide basándose en el contexto

---

Created by [Steven Ge](https://www.linkedin.com/in/steven-ge-ab016947/) on December 13, 2025.
