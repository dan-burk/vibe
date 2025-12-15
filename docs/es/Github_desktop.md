[Inicio](index.html)

# Comience con el Control de Versiones

Está trabajando en un proyecto y realiza cambios que rompen todo. No puede recordar qué cambió y desea poder volver a cuando funcionaba. El control de versiones es como puntos de guardado en un videojuego: cada vez que "confirma" su trabajo, crea un punto de restauración al que siempre puede volver. [GitHub](https://github.com) almacena sus puntos de guardado en la nube, por lo que su código está respaldado de forma segura y es accesible desde cualquier computadora.

## Conceptos Clave

- **Git** - Software de control de versiones que rastrea los cambios en sus archivos en su computadora
- **GitHub** - Sitio web que almacena su código en la nube, como Google Drive para código
- **GitHub Desktop** - Aplicación que hace que Git sea fácil de usar con botones en lugar de comandos
- **Repository (repo)** - Una carpeta de proyecto que rastrea todos sus cambios

## Lo Que Necesitará

- Computadora con Windows, macOS o Linux
- Conexión a Internet
- Dirección de correo electrónico para cuenta de GitHub
- 15-20 minutos

## Paso 1: Crear una Cuenta de GitHub

- Abra su navegador web
- Vaya a [github.com](https://github.com)
- Haga clic en **Sign up**
- Ingrese su correo electrónico, cree una contraseña y elija un nombre de usuario
- Complete los pasos de verificación

## Paso 2: Descargar GitHub Desktop

- Vaya a [desktop.github.com](https://desktop.github.com)
- Haga clic en el botón **Download**
- Abra el archivo descargado para instalar

**En Windows:**
- Haga doble clic en el archivo del instalador
- GitHub Desktop se instala y se abre automáticamente

**En Mac:**
- Abra el archivo `.zip` descargado
- Arrastre **GitHub Desktop** a su carpeta Applications
- Abra GitHub Desktop desde Applications

## Paso 3: Iniciar Sesión en GitHub Desktop

- Abra GitHub Desktop
- Haga clic en **Sign in to GitHub.com**
- Su navegador se abre—haga clic en **Authorize desktop**
- Vuelva a GitHub Desktop
- Haga clic en **Finish** para completar la configuración

## Paso 4: Crear Su Primer Repositorio

- En GitHub Desktop, haga clic en **Create a New Repository on your Hard Drive**
- Complete el formulario:
  - **Name:** `my-first-project` (o cualquier nombre que desee)
  - **Description:** `Learning version control` (opcional)
  - **Local Path:** Elija dónde guardarlo (la carpeta Documents está bien)
  - Marque **Initialize this repository with a README**
- Haga clic en **Create Repository**

## Paso 5: Abrir la Carpeta de Su Proyecto

- En GitHub Desktop, haga clic en **Repository** en la barra de menú
- Seleccione **Show in Finder** (Mac) o **Show in Explorer** (Windows)
- Verá una carpeta con el nombre de su proyecto
- Dentro hay un archivo llamado `README.md`

## Paso 6: Realizar Su Primer Cambio

- Abra `README.md` en cualquier editor de texto (Notepad, TextEdit o VS Code)
- Reemplace el contenido con:
  ```
  # My First Project

  I'm learning version control with GitHub Desktop.

  ## What I'm Building

  This is a practice project to learn how to:
  - Track changes to my code
  - Create save points (commits)
  - Back up my work to GitHub
  ```
- Haga clic en **File** → **Save**

## Paso 7: Crear Su Primer Commit (Punto de Guardado)

- Vuelva a GitHub Desktop
- Verá sus cambios resaltados en el lado derecho (verde = agregado, rojo = eliminado)
- En la parte inferior izquierda, escriba un mensaje de commit: `Updated README with project description`
- Haga clic en el botón azul **Commit to main**

## Paso 8: Enviar a GitHub (Respaldar en la Nube)

- Haga clic en el botón azul **Publish repository** en la parte superior
- Mantenga el nombre tal como está
- Desmarque "Keep this code private" si desea que otros lo vean (opcional)
- Haga clic en **Publish Repository**

Su código ahora está respaldado en línea en: `https://github.com/YOUR-USERNAME/my-first-project`

## Próximos Pasos

- Edite su archivo README nuevamente y confirme los cambios
- Cree un nuevo archivo en la carpeta de su proyecto y confírmelo
- Explore la pestaña **History** para ver cómo evoluciona su proyecto con el tiempo

## Solución de Problemas

- **No puede iniciar sesión en GitHub** - Verifique su conexión a Internet. Intente iniciar sesión primero en github.com para verificar que sus credenciales funcionen.
- **Los cambios no aparecen en GitHub Desktop** - Asegúrese de haber guardado sus archivos. Haga clic en **Repository** → **Refresh** o reinicie GitHub Desktop.
- **El envío falla con error "rejected"** - Alguien más envió cambios. Haga clic en **Fetch origin** primero, luego intente enviar nuevamente.

## Descripción General del Flujo de Trabajo

- Realice cambios en los archivos de su proyecto
- Revise los cambios en GitHub Desktop (verde = agregado, rojo = eliminado)
- Escriba un mensaje de commit descriptivo y haga clic en **Commit to main**
- Haga clic en **Push origin** para respaldar en GitHub
- Repita

---

Created by [Steven Ge](https://www.linkedin.com/in/steven-ge-ab016947/) on December 7, 2025.
