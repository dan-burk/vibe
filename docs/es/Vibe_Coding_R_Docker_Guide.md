[Inicio](index.html)

# Vibe Coding en R con Claude Code y Docker

Vibe coding es como tener una conversación con su computadora: usted describe el resultado deseado, Claude Code lo construye, usted prueba y refina. No es magia; es una nueva forma de trabajar donde usted guía la visión y la IA maneja la implementación. Este tutorial le muestra cómo construir un panel de estadísticas de la NBA usando únicamente solicitudes en lenguaje natural.

## Conceptos Clave

- **[Claude Code](https://code.claude.com/)** - Asistente de codificación con IA que escribe, depura y refactoriza código basándose en sus solicitudes en lenguaje natural
- **[hoopR](https://hoopr.sportsdataverse.org/)** - Paquete de R que proporciona acceso fácil a estadísticas de jugadores de la NBA y datos de partidos
- **Refinamiento iterativo** - El patrón central de vibe coding: describir → probar → refinar → confirmar versiones funcionales

## Lo Que Necesitará

- Haber completado [R Coding in VS Code via Docker](./R_Coding_Docker_Guide)
- Haber completado [Using GitHub Desktop with Claude Code](./GitHub_Desktop_Claude_Code_Workflow)
- Docker Desktop instalado e iniciado
- 25-30 minutos

## Paso 1: Crear un Nuevo Repositorio en GitHub

- Abra GitHub Desktop
- Haga clic en **File > New Repository**
- Complete los detalles:
  - **Name:** `nba-dashboard`
  - **Description:** `NBA stats dashboard built with vibe coding`
  - **Local Path:** Elija una ubicación (por ejemplo, Documents o carpeta de trabajo)
  - Marque **Initialize this repository with a README**
- Haga clic en **Create Repository**
- Haga clic en **Publish repository** en la parte superior
- Desmarque **Keep this code private** si desea que sea público (opcional)
- Haga clic en **Publish Repository**

Ahora tiene un repositorio Git local y una copia de seguridad en GitHub.

## Paso 2: Copiar la Configuración de Docker

- Vaya a https://github.com/gexijin/vibe
  - **Nota para usuarios de ARM64 (Apple Silicon Macs):** Use https://github.com/gexijin/vibe/tree/ARM64 en su lugar
- Haga clic en **Code** y Download Zip
- Abra File Explorer (Windows) o Finder (Mac)
- Descomprima el archivo en la carpeta Download
- Navegue a su carpeta del proyecto vibe (por ejemplo, `Documents/vibe`)
- Encuentre la carpeta `.devcontainer`
- Copie la carpeta completa (contiene `Dockerfile` y `devcontainer.json`)
- Navegue a su nueva carpeta `nba-dashboard`
- Pegue la carpeta `.devcontainer` allí

Su carpeta `nba-dashboard` ahora debería contener:
- `.devcontainer/` (carpeta que acaba de copiar)
- `README.md` (creado por GitHub Desktop)
- `.git/` (carpeta oculta para control de versiones)

## Paso 3: Abrir el Proyecto en el Contenedor

- Inicie la aplicación **Docker Desktop** desde Windows o Mac. Déjela ejecutándose en segundo plano
- Abra VS Code
- Haga clic en **File > Open Folder**
- Navegue a la carpeta `nba-dashboard`
- Haga clic en **Select Folder** (Windows) o **Open** (Mac)
- Aparece una notificación en la esquina inferior derecha: **Folder contains a Dev Container configuration file**
- Haga clic en **Reopen in Container**
- Si no ve la notificación, haga clic en el ícono verde en la esquina inferior izquierda y seleccione **Reopen in Container**
- VS Code construye el contenedor Docker (toma de 3 a 5 minutos la primera vez)
- Observe la notificación de progreso que muestra los pasos de construcción
- Cuando se complete, el ícono verde muestra **Dev Container: R in Docker**

## Paso 4: Iniciar Claude Code

- En VS Code, haga clic en **Terminal > New Terminal**
- Ahora está dentro del contenedor Docker
- Escriba este comando para iniciar Claude Code:

```bash
claude
```

- Se abre una ventana del navegador para autenticación
- Haga clic en **Continue with Google** o **Continue with Email**
- Inicie sesión con su cuenta de Claude (o cree una)
- Después de que la autenticación tenga éxito, regrese al terminal de VS Code
- Verá el mensaje de bienvenida de Claude

Claude Code ahora está ejecutándose y listo para sus solicitudes.

## Paso 5: Primer Vibe - Obtener Datos de la NBA

Ahora comienza la parte divertida. En lugar de buscar documentación, simplemente describa lo que desea.

- En el terminal de Claude Code, escriba:

```
Install the hoopR package and load current NBA player statistics. Show me the top 10 players by total points scored this season. Display it as a nice table.
```

- Presione Enter
- Observe cómo Claude:
  - Instala el paquete hoopR
  - Escribe código R para cargar datos
  - Crea un script para mostrar los mejores anotadores
  - Ejecuta el código
- Revise la salida que muestra nombres de jugadores, equipos y puntos

¡Acaba de usar vibe coding! Sin buscar documentación, sin prueba y error, solo describir y probar.

**Guarde su progreso:** Pida a Claude que confirme usando Git, o hágalo usted mismo desde GitHub Desktop:
```
Commit these changes.
```

## Paso 6: Segundo Vibe - Explorar los Datos

Antes de construir un panel, comprenda qué datos tiene.

- En el terminal de Claude Code, escriba:

```
Show me what columns are available in this NBA data. Then create a summary showing: number of players, number of teams, average points per player, and who has the most assists and rebounds.
```

- Presione Enter
- Claude explora el conjunto de datos y le muestra estadísticas interesantes
- Observe la salida para ver las columnas disponibles como: player_name, team, points, assists, rebounds, field_goal_percentage, etc.

Esta exploración le ayuda a decidir qué poner en su panel.

**Guarde su progreso:** Pida a Claude que confirme, o use GitHub Desktop.

## Paso 7: Tercer Vibe - Crear una Aplicación Shiny Básica

Es hora de construir el panel interactivo.

- En el terminal de Claude Code, escriba:

```
Create a Shiny app in a file called app.R that shows an interactive table of NBA player stats. Include columns for player name, team, points, assists, and rebounds. Add a slider to filter players by minimum points scored (from 0 to 1000). Make it look clean and professional.
```

- Presione Enter
- Claude crea `app.R` con una aplicación Shiny completa
- Espere a que Claude termine de escribir el archivo

## Paso 8: Ejecutar la Aplicación Shiny

Pruebe su panel para ver si funciona.

- Mire en la parte superior derecha del editor de VS Code (donde está abierto `app.R`)
- Encuentre el botón **▶** con una flecha desplegable
- Haga clic en el desplegable y seleccione **Run Shiny App**
- La aplicación se inicia y aparece una notificación: **Open in Browser**
- Haga clic en **Open in Browser**
- El panel de la NBA se abre en su navegador web
- Intente mover el control deslizante de puntos: la tabla se filtra en tiempo real
- Desplácese por los datos de jugadores
- Confirme los cambios si la aplicación funciona

Si algo no funciona, copie cualquier mensaje de error y péguelo a Claude para que lo corrija.

## Paso 9: Cuarto Vibe - Agregar Visualización

Las tablas son útiles, pero las visualizaciones cuentan mejores historias.

- De vuelta en el terminal de Claude Code, escriba:

```
Add a bar chart below the table showing the top 15 players by points. Use different colors for each player. Also add a scatter plot showing the relationship between points and assists for all filtered players.
```

- Presione Enter
- Claude actualiza `app.R` con código de visualización
- Haga clic en **Run Shiny App** nuevamente para recargar la aplicación
- Actualice su navegador
- Ahora ve un gráfico de barras colorido y un diagrama de dispersión
- Mueva el control deslizante: todas las visualizaciones se actualizan juntas

Esto es vibe coding en acción: describir la funcionalidad, probarla, iterar.

## Paso 10: Quinto Vibe - Agregar Filtro de Equipo

Haga el panel más interactivo con selección de equipo.

- En el terminal de Claude Code, escriba:

```
Add a dropdown menu to filter players by team. Put it at the top. When I select a team, show only players from that team. Include an "All Teams" option to show everyone.
```

- Presione Enter
- Claude agrega el filtro de equipo
- Actualice su navegador
- Pruebe el menú desplegable: seleccione diferentes equipos como Lakers, Warriors, Celtics
- Observe cómo la tabla y los gráficos se actualizan para cada equipo

Está construyendo un panel profesional mediante una conversación.

## Paso 11: Revisar y Confirmar

Antes de confirmar, revise lo que Claude construyó.

- En el Explorador de VS Code, haga clic en `app.R` para abrirlo
- Revise el código: observe el diseño de la interfaz, la lógica del servidor y el código de gráficos
- No necesita entender cada línea, pero obtenga una idea de la estructura
- Abra GitHub Desktop
- Verá `app.R` listado como un archivo nuevo
- El panel derecho muestra todo el código en verde (adiciones nuevas)
- En el campo **Summary** en la parte inferior izquierda, escriba:

```
Create NBA dashboard with team filter and visualizations
```

- Haga clic en **Commit to main**
- Haga clic en **Push origin** para respaldar en GitHub

¡Ha guardado su primera versión funcional!

## Paso 12: Iterar y Mejorar

Vibe coding brilla cuando itera. Intente agregar funcionalidades describiéndolas:

**Ejemplos de solicitudes a Claude:**

- "Add a player search box so I can type a player's name and jump to them"
- "Show the team logos next to team names in the dropdown"
- "Add a line chart showing points per game trend for the selected team"
- "Make the bar chart sortable by clicking column headers"
- "Add tooltips to the scatter plot showing player names when I hover"

Después de cada funcionalidad exitosa:
- Pruébela en el navegador
- Si funciona, confírmela con GitHub Desktop
- Si falla, dígale a Claude el error y pida que lo corrija
- Cuando esté corregido, confirme la versión funcional


**Principios clave:**

- **Describa resultados, no implementación** - Diga "mostrar mejores anotadores" no "usar arrange() y head()"
- **Itere rápidamente** - Probar → refinar → probar → refinar
- **Confirme versiones funcionales** - Guarde cada éxito antes de intentar nuevas funcionalidades
- **Acepte los fallos** - Si el código de Claude falla, simplemente describa el error y pida que lo corrija
- **Mantenga el control** - Usted decide funcionalidades, prioridades y cuándo es suficientemente bueno

Cada vez, siga el patrón: describir → probar → iterar → confirmar.

## Próximos Pasos

- **Aplíquelo a su dominio** - Use vibe coding para sus propios datos (investigación, negocios, pasatiempos)
- **Pruebe otros paquetes** - Pida a Claude que use `nflfastR` para fútbol americano o `worldfootballR` para fútbol
- **Aprenda preguntando** - Cuando Claude escriba código, pregunte "explica qué hace esta función" para aprender R
- **Comparta su panel** - Despliegue en [shinyapps.io](https://www.shinyapps.io/) (pregunte a Claude cómo)
- **Lea sobre vibe coding** - Visite [la guía de IBM](https://www.ibm.com/think/topics/vibe-coding) para aprender más sobre este estilo de codificación

## Solución de Problemas

- **La instalación de hoopR falla** - Verifique su conexión a internet; el paquete descarga datos de la web. Intente ejecutar `install.packages("hoopR")` en un terminal de R para ver mensajes de error detallados.
- **La aplicación Shiny no se inicia** - Verifique que la extensión Shiny esté instalada (busque "Posit.shiny" en Extensiones de VS Code). Revise el terminal para mensajes de error y péguelos a Claude.
- **No se muestran datos** - El paquete hoopR obtiene datos en vivo; si la temporada de la NBA no ha comenzado, puede haber datos limitados. Pida a Claude que use datos de muestra o una temporada anterior.
- **Claude comete errores** - ¡Normal! Copie el mensaje de error, péguelo a Claude y diga "corrige este error". Vibe coding incluye iteración y depuración.
- **No puedo hacer push a GitHub** - Asegúrese de haber iniciado sesión en GitHub Desktop y publicado el repositorio (Paso 1). Verifique su conexión a internet.

## Descripción General del Flujo de Trabajo

Este tutorial combinó varias tecnologías en un flujo de trabajo:

- **GitHub Desktop** - Control de versiones con interfaz visual (crear repositorios, confirmar, hacer push)
- **Contenedor Docker** - Entorno R aislado con todas las dependencias preinstaladas
- **VS Code** - Editor de código que se conecta al contenedor Docker
- **Claude Code** - Asistente de IA que escribe código R y Shiny a partir de sus descripciones
- **Paquete hoopR** - Fuente de datos de la NBA con API simple
- **Framework Shiny** - Aplicaciones web interactivas en R

La magia no es ninguna herramienta individual, es cómo vibe coding le permite describir lo que desea e iterar rápidamente. Pasó de un proyecto vacío a un panel de deportes funcional en menos de 30 minutos sin escribir una sola línea de código manualmente.

## Flujo de Trabajo Diario

Después de esta configuración inicial, su rutina diaria de vibe coding se convierte en:

1. **Iniciar Docker Desktop** - Lance la aplicación, espere el estado verde
2. **Abrir VS Code** - Abra su proyecto, reabra en contenedor si es necesario
3. **Iniciar Claude Code** - Escriba `claude` en el terminal
4. **Describa su objetivo** - "Agregar una funcionalidad que..." o "Corregir el error donde..."
5. **Probar los cambios** - Ejecute su aplicación, verifique si funciona
6. **Iterar o confirmar** - Si falla, describa la corrección; si funciona, confirme con GitHub Desktop
7. **Hacer push regularmente** - Haga clic en **Push origin** para respaldar en GitHub

Cuanto más practique, mejor será describiendo lo que desea. Vibe coding es una habilidad: aprende qué tipos de descripciones funcionan mejor y cómo dividir grandes ideas en piezas probables.

---

Creado por [Steven Ge](https://www.linkedin.com/in/steven-ge-ab016947/) el 7 de diciembre de 2025.
