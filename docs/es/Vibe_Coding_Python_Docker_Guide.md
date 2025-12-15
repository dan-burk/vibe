[Inicio](index.html)

# Vibe Coding en Python con Claude Code y Docker

Ha escrito código Python escribiendo cada línea usted mismo. Pero ¿qué pasaría si pudiera describir lo que desea en inglés sencillo y ver cómo aparece el código? Vibe coding es como tener una conversación con su computadora: usted describe el resultado, Claude Code lo construye, usted prueba y refina. No es magia; es una nueva forma de trabajar donde usted guía la visión y la IA maneja la implementación. Este tutorial le muestra cómo analizar el conjunto de datos clásico de flores Iris usando nada más que solicitudes en lenguaje natural.

## Conceptos Clave

- **[Vibe Coding](https://www.ibm.com/think/topics/vibe-coding)** - Programar describiendo lo que desea en lenguaje natural, luego iterar basándose en resultados en lugar de escribir código línea por línea
- **[Claude Code](https://code.claude.com/)** - Asistente de codificación IA que escribe, depura y refactoriza código basándose en sus solicitudes en lenguaje natural
- **[Iris Dataset](https://scikit-learn.org/stable/datasets/toy_dataset.html#iris-dataset)** - Conjunto de datos clásico que contiene mediciones de 150 flores iris de tres especies
- **Refinamiento iterativo** - El patrón central de vibe coding: describir → probar → refinar → confirmar versiones funcionales

## Lo Que Necesitará

- Haber completado [Python Coding in VS Code via Docker](./Python_Coding_Docker_Guide)
- Haber completado [Using GitHub Desktop with Claude Code](./GitHub_Desktop_Claude_Code_Workflow)
- 20-25 minutos

## Paso 1: Crear Nuevo Repositorio en GitHub

- Abra GitHub Desktop
- Haga clic en **File > New Repository**
- Complete los detalles:
  - **Name:** `iris-analysis`
  - **Description:** `Iris data analysis built with vibe coding`
  - **Local Path:** Elija una ubicación (ej., Documents o carpeta de trabajo)
  - Marque **Initialize this repository with a README**
- Haga clic en **Create Repository**
- Haga clic en **Publish repository** en la parte superior
- Desmarque **Keep this code private** si desea que sea público (opcional)
- Haga clic en **Publish Repository**

Ahora tiene un repositorio Git local y una copia de seguridad en GitHub.

## Paso 2: Copiar Configuración de Docker

Necesita la carpeta `.devcontainer` del proyecto vibe para configurar su entorno Docker.

- Abra File Explorer (Windows) o Finder (Mac)
- Navegue a su carpeta del proyecto vibe (ej., `Documents/vibe`)
- Busque la carpeta `.devcontainer`
- Copie la carpeta completa (contiene `Dockerfile` y `devcontainer.json`)
- Navegue a su nueva carpeta `iris-analysis`
- Pegue la carpeta `.devcontainer` allí

Su carpeta `iris-analysis` ahora debe contener:
- `.devcontainer/` (carpeta que acaba de copiar)
- `README.md` (creado por GitHub Desktop)
- `.git/` (carpeta oculta para control de versiones)

## Paso 3: Abrir Proyecto en Container

- Abra VS Code
- Haga clic en **File > Open Folder**
- Navegue a la carpeta `iris-analysis`
- Haga clic en **Select Folder**
- Aparece una notificación en la parte inferior derecha: **Folder contains a Dev Container configuration file**
- Haga clic en **Reopen in Container**
- Si no ve la notificación, haga clic en el ícono verde en la esquina inferior izquierda y seleccione **Reopen in Container**
- VS Code construye el container de Docker (toma 3-5 minutos la primera vez)
- Observe la notificación de progreso mostrando los pasos de construcción
- Cuando se complete, el ícono verde muestra **Dev Container: Python in Docker**

## Paso 4: Iniciar Claude Code

- En VS Code, haga clic en **Terminal > New Terminal**
- Ahora está dentro del container de Docker
- Escriba este comando para iniciar Claude Code:

```bash
claude
```

- Se abre una ventana del navegador para autenticación
- Haga clic en **Continue with Google** o **Continue with Email**
- Inicie sesión con su cuenta de Claude (o cree una)
- Después de que la autenticación sea exitosa, regrese al terminal de VS Code
- Verá el mensaje de bienvenida de Claude

Claude Code ahora está ejecutándose y listo para sus solicitudes.

## Paso 5: Primer Vibe - Cargar los Datos

Ahora comienza la diversión. En lugar de buscar documentación, simplemente describa lo que desea.

- En el terminal de Claude Code, escriba:

```
Load the iris dataset from scikit-learn. Convert it to a pandas dataframe with proper column names. Add the species names as a column (not just numbers). Show me the first 10 rows. Save the code to a file called iris_exploration.py
```

- Presione Enter
- Observe cómo Claude:
  - Escribe código Python para cargar los datos
  - Crea un script con las importaciones apropiadas
  - Ejecuta el código para mostrarle los resultados
- Revise la salida que muestra las mediciones de flores y nombres de especies

¡Acaba de usar vibe coding! Sin buscar documentación, sin ensayo y error—solo describa y pruebe.

Solicite a Claude que confirme usando Git. O hágalo usted mismo desde GitHub Desktop.
```
Commit these changes.
```
## Paso 6: Segundo Vibe - Estadísticas Resumidas

Antes de crear visualizaciones, comprenda qué contienen los datos.

- En el terminal de Claude Code, escriba:

```
Show me summary statistics for the iris data grouped by species. I want to see the mean, min, and max for each measurement (sepal length, sepal width, petal length, petal width) for each of the three species. Add this to iris_exploration.py
```

- Presione Enter
- Claude actualiza el script y muestra las estadísticas
- Note cómo diferentes especies tienen diferentes rangos de mediciones
- Setosa tiene pétalos mucho más pequeños que Virginica

Esta exploración le ayuda a comprender patrones en los datos.

Solicite a Claude que confirme usando Git. O hágalo usted mismo desde GitHub Desktop.

## Paso 7: Tercer Vibe - Crear un Histograma

Es hora de visualizar los datos.

- En el terminal de Claude Code, escriba:

```
Create a histogram showing the distribution of petal lengths for all flowers. Use 20 bins. Add a title and axis labels. Save the plot as petal_length_histogram.png. Add this code to iris_exploration.py
```

- Presione Enter
- Claude crea el código de visualización
- Un archivo PNG aparece en su carpeta del proyecto
- Abra `petal_length_histogram.png` para ver el gráfico
- Note los dos picos—esto muestra que las especies tienen diferentes longitudes de pétalos

## Paso 8: Cuarto Vibe - Gráfico de Dispersión

Los gráficos de dispersión muestran relaciones entre dos variables.

- En el terminal de Claude Code, escriba:

```
Create a scatter plot with petal length on the x-axis and petal width on the y-axis. Color each point by species using different colors. Add a legend showing which color is which species. Save as petal_scatter.png. Add this to iris_exploration.py
```

- Presione Enter
- Claude crea el gráfico de dispersión
- Abra `petal_scatter.png` para ver el resultado
- Note cómo las tres especies forman grupos distintos
- Setosa (pétalos pequeños) está claramente separada de las demás

Esto es vibe coding en acción: describa la visualización, pruébela, itere.

## Paso 9: Quinto Vibe - Gráfico de Cajas

Los gráficos de cajas son excelentes para comparar distribuciones entre grupos.

- En el terminal de Claude Code, escriba:

```
Create a box plot comparing petal lengths across the three species. Put species on the x-axis and petal length on the y-axis. Use different colors for each species. Add a title. Save as species_boxplot.png. Add this to iris_exploration.py
```

- Presione Enter
- Claude añade el código del gráfico de cajas
- Abra `species_boxplot.png` para ver la comparación
- Las cajas muestran la mediana y los cuartiles para cada especie
- Puede ver claramente que Virginica tiene los pétalos más largos

## Paso 10: Revisar y Confirmar

Antes de confirmar, revise lo que Claude construyó.

- En VS Code Explorer, haga clic en `iris_exploration.py` para abrirlo
- Revise el código—note las importaciones, carga de datos y secciones de gráficos
- No necesita entender cada línea, pero obtenga una idea de la estructura
- Verifique que todos los archivos PNG fueron creados: `petal_length_histogram.png`, `petal_scatter.png`, `species_boxplot.png`
- Abra GitHub Desktop
- Verá todos los archivos nuevos listados (el script Python y las imágenes PNG)
- En el campo **Summary** en la parte inferior izquierda, escriba:

```
Iris data analysis with histograms, scatter plots, and box plots
```

- Haga clic en **Commit to main**
- Haga clic en **Push origin** para respaldar en GitHub

¡Ha guardado su primer análisis funcional!

## Paso 11: Iterar y Mejorar

Vibe coding brilla cuando usted itera. Intente añadir funciones describiéndolas:

**Ejemplos de solicitudes a Claude:**

- "Add a correlation matrix heatmap showing relationships between all four measurements"
- "Create a violin plot comparing sepal width across species"
- "Calculate and display the correlation coefficient between petal length and width"
- "Add statistical test results comparing species (ANOVA or t-test)"
- "Create a pair plot showing all variable relationships colored by species"

Después de cada función exitosa:
- Pruébela ejecutando el script
- Si funciona, confirme con GitHub Desktop
- Si falla, diga a Claude el error y solicite que lo corrija
- Cuando esté corregido, confirme la versión funcional


**Principios clave:**

- **Describa resultados, no implementación** - Diga "show correlation heatmap" no "use seaborn.heatmap() with df.corr()"
- **Itere rápidamente** - Probar → refinar → probar → refinar
- **Confirme versiones funcionales** - Guarde cada éxito antes de probar nuevas funciones
- **Acepte los fallos** - Si el código de Claude falla, simplemente describa el error y solicite que lo corrija
- **Mantenga el control** - Usted decide las funciones, prioridades y cuándo es suficientemente bueno

Cada vez, siga el patrón: describir → probar → iterar → confirmar.

## Próximos Pasos

- **Pruebe diferentes conjuntos de datos** - Solicite a Claude que use el conjunto de datos wine, digits, o cargue un archivo CSV
- **Explore más visualizaciones** - Pruebe heatmaps, pair plots, o violin plots
- **Aprenda preguntando** - Cuando Claude escriba código, pregunte "explain what this line does" para aprender Python
- **Aplique a sus propios datos** - Use vibe coding para analizar sus datos de investigación o trabajo
- **Lea sobre vibe coding** - Visite [la guía de IBM](https://www.ibm.com/think/topics/vibe-coding) para aprender más sobre este estilo de codificación

## Solución de Problemas

- **El gráfico no se muestra** - El código guarda los gráficos como archivos PNG. Busque en su carpeta del proyecto y abra el archivo de imagen directamente en VS Code.
- **Errores de importación** - El container de Docker debe tener pandas, matplotlib, y scikit-learn preinstalados. Si no, solicite a Claude que los instale con pip.
- **Claude comete errores** - ¡Normal! Copie el mensaje de error, péguelo a Claude y diga "fix this error." Vibe coding incluye iteración y depuración.
- **No puede hacer push a GitHub** - Asegúrese de haber iniciado sesión en GitHub Desktop y publicado el repositorio (Paso 1). Verifique su conexión a internet.
- **El container no inicia** - Asegúrese de que Docker Desktop esté ejecutándose (indicador de estado verde). Intente hacer clic en el ícono verde en VS Code y seleccionar **Rebuild Container**.

## Resumen del Flujo de Trabajo

Este tutorial combinó varias tecnologías en un flujo de trabajo:

- **GitHub Desktop** - Control de versiones con interfaz visual (crear repositorios, confirmar, hacer push)
- **Docker container** - Entorno Python aislado con todas las dependencias preinstaladas
- **VS Code** - Editor de código que se conecta al container de Docker
- **Claude Code** - Asistente IA que escribe código Python desde sus descripciones
- **scikit-learn** - Proporciona el conjunto de datos Iris y herramientas de machine learning
- **pandas** - Manipulación y análisis de datos
- **matplotlib** - Creación de visualizaciones

La magia no es una sola herramienta—es cómo vibe coding le permite describir lo que desea e iterar rápidamente. Pasó de un proyecto vacío a un análisis de datos completo con múltiples visualizaciones en 20 minutos sin escribir una sola línea de código manualmente.


---

Creado por [Steven Ge](https://www.linkedin.com/in/steven-ge-ab016947/) el 11 de diciembre de 2025.
