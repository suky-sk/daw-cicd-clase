# Práctica: CI/CD con GitHub Actions y GitHub Pages

## Objetivo

Aprender qué es la **Integración Continua (CI)** y el **Despliegue Continuo (CD)** de forma práctica:

1. **Parte 1 — Individual:** crearás tu propia página web personalizada, configurarás los workflows de CI/CD rellenando los huecos, y verás cómo se valida y despliega automáticamente.
2. **Parte 2 — Colaborativa:** contribuirás al mural de la clase haciendo un Pull Request a un repositorio central. Tu contribución se validará y fusionará **automáticamente** sin intervención.

### Conceptos clave

| Concepto | Qué es | Cuándo se ejecuta |
|----------|--------|--------------------|
| **CI** (Integración Continua) | Un workflow que **valida** tu código automáticamente | Cuando abres un **Pull Request** |
| **CD** (Despliegue Continuo) | Un workflow que **publica** la web automáticamente | Cuando se fusiona código en **main** |
| **Pull Request (PR)** | Petición para fusionar tus cambios en otra rama/repo | Lo creas tú manualmente |
| **Fork** | Copia de un repositorio ajeno en tu cuenta | Para contribuir a repos de otros |

### Buenas prácticas

Eliminar **TODOs** una vez están resueltos.

Trabajar en **ramas**.

---

## Parte 1: Tu página personal con CI/CD

### Paso 1: Crear tu repositorio

1. Accede al repositorio template del profesor:
   `https://github.com/gtraver-edu/daw-cicd-individual`
2. Haz clic en **"Use this template" → "Create a new repository"**.
3. Ponle un nombre: `cicd-tunombre` (por ejemplo, `cicd-ana`).
4. Selecciona **Public** y haz clic en **Create repository**.

### Paso 2: Clonar en tu equipo

```bash
git clone https://github.com/TU-USUARIO/cicd-tunombre.git
cd cicd-tunombre
```

### Paso 3: Crear una rama de trabajo

```bash
git checkout -b feature/mi-pagina
```

> **¿Por qué una rama?** En el mundo real nunca se trabaja directamente sobre `main`. Las ramas permiten hacer cambios sin afectar al código estable. Después, un Pull Request permite revisar los cambios antes de integrarlos.

### Paso 4: Personalizar tu página

#### 4a. Editar `index.html`

- Sustituye **todas** las apariciones de `TU_NOMBRE` por tu nombre real o alias.

#### 4b. Configurar el workflow de CI (`.github/workflows/ci.yml`)

Abre el archivo y completa los **TODOs** siguiendo las pistas:

| TODO | Pregunta | Pista |
|------|----------|-------|
| TODO 1 | ¿Qué evento activa el CI? | Se activa al abrir un Pull Request


#### 4c. Configurar el workflow de CD (`.github/workflows/cd.yml`)

Abre el archivo y completa los **TODOs**:

| TODO | Pregunta | Pista |
|------|----------|-------|
| TODO 1 | ¿Qué evento activa el CD? | Se activa al fusionar |
| TODO 2 | ¿Qué permiso necesita? | Necesario para crear la rama gh-pages. |
| TODO 3 | ¿Qué directorio publicar? | Los archivos están en la raíz. ¿Cómo se referencia el directorio actual en Linux? |

### Paso 5: Subir los cambios

```bash
git add .
git commit -m "Personalizar página y configurar CI/CD"
git push origin feature/mi-pagina
```

### Paso 6: Abrir un Pull Request

1. Ve a tu repositorio en GitHub.
2. Verás un aviso para crear un PR. Haz clic en **"Compare & pull request"**.
3. Título: `Personalizar mi página`
4. Rama base: `main` ← Rama comparada: `feature/mi-pagina`
5. Clic en **"Create pull request"**.

### Paso 7: Observar el CI en acción

- En el PR verás un **círculo amarillo** (ejecutándose).
- Cuando termine:
  - **Check verde** ✅ → todo correcto, puedes fusionar.
  - **X roja** ❌ → hay un error. Ve a la pestaña **Actions**, lee el log, corrige y haz push. El CI se re-ejecuta automáticamente.

### Paso 8: Fusionar el Pull Request

1. Haz clic en **"Merge pull request"** → **"Confirm merge"**.
2. Opcionalmente, elimina la rama.

### Paso 9: Observar el CD en acción

- Al fusionar se dispara el workflow de CD (push a `main`).
- Ve a **Actions** y comprueba que el job `deploy` termina con check verde.
- Se habrá creado automáticamente una rama `gh-pages`.

### Paso 10: Activar GitHub Pages

1. Ve a **Settings → Pages**.
2. En *Source*, selecciona **Deploy from a branch**.
3. Elige la rama **`gh-pages`**, carpeta `/ (root)`. Clic en **Save**.
4. Espera 1-2 minutos.
5. Accede a tu URL: `https://TU-USUARIO.github.io/cicd-tunombre/`

**¡Comprueba que ves tu página con tu nombre!**

> 📝 **Anota tu URL de GitHub Pages**, la necesitarás en la Parte 2.

---

## Parte 2: Contribuir al mural de la clase

Ahora vas a añadir tu página al mural colectivo de la clase. Tu contribución será validada y fusionada **automáticamente** por el workflow del repositorio central.

**Entregables**

1. **Respuestas a las preguntas:** Un documento con las respuestas a la **Pregunta 1** (Paso 7) y a la **Pregunta 2** (Paso 8).
2. **Verificación web:** Tu página personal debe estar listada y visible correctamente en el mural de la clase.

### Paso 1: Hacer fork del repositorio de clase

1. Accede al repositorio central del profesor:
   `https://github.com/gtraver-edu/daw-cicd-clase`
2. Haz clic en **"Fork"** (esquina superior derecha).
3. Crea el fork en tu cuenta (deja el nombre por defecto).

### Paso 2: Clonar tu fork

```bash
git clone https://github.com/TU-USUARIO/daw-cicd-clase.git
cd daw-cicd-clase
```

### Paso 3: Crear una rama

```bash
git checkout -b feature/mi-contribucion
```

### Paso 4: Crear tu archivo de contribución

1. **Copia** el archivo de ejemplo:
   ```bash
   cp alumnos/ejemplo.html alumnos/tu-nombre.html
   ```
   Sustituye `tu-nombre` por tu nombre y apellido (sin espacios ni acentos, en minúsculas).
   Ejemplo: `alumnos/ana-garcia.html`

2. **Edita** tu archivo `alumnos/tu-nombre.html` con tus datos:

   ```html
   <div class="alumno-card">
       <h3>Ana García</h3>
       <iframe src="https://ana-garcia.github.io/cicd-ana/"
               title="Página de Ana García"></iframe>
       <a href="https://ana-garcia.github.io/cicd-ana/" target="_blank">
           Abrir página ↗
       </a>
   </div>
   ```

   - Cambia el nombre en `<h3>`.
   - Cambia la URL del `iframe` y del `<a>` por **tu URL de GitHub Pages** de la Parte 1.

3. **Importante:**
   - NO modifiques `ejemplo.html`.
   - NO modifiques `index.html`, `style.css`, ni ningún otro archivo.
   - Solo crea tu propio archivo dentro de `alumnos/`.

### Paso 5: Subir y crear Pull Request

```bash
git add alumnos/tu-nombre.html
git commit -m "Añadir contribución de Tu Nombre"
git push origin feature/mi-contribucion
```

Ve a tu fork en GitHub. Verás un aviso sugiriendo crear un Pull Request. Haz clic en **"Compare & pull request"**.

> **Nota:** Si no ves el aviso, haz clic en **"Contribute" → "Open pull request"**.

- Base repository: `gtraver-edu/daw-cicd-clase` → rama `main`
- Head repository: `TU-USUARIO/daw-cicd-clase` → rama `feature/mi-contribucion`
- Título: `Contribución de Tu Nombre`
- Clic en **"Create pull request"**.

### Paso 6: Ver la magia del CI/CD automático

Observa lo que ocurre en tu PR **sin que nadie haga nada**:

1. **El workflow se ejecuta** → valida que:
   - Solo has tocado archivos en `alumnos/`.
   - Tu archivo contiene la estructura correcta (`alumno-card`, `iframe`).
   - No quedan placeholders sin rellenar (`TU-USUARIO`, `TU_NOMBRE`).
2. **Si pasa** → el PR se **fusiona automáticamente** (squash merge).
3. **Inmediatamente después** → genera la galería y **despliega** en GitHub Pages.

> Si falla (X roja), lee el log en Actions, corrige tu archivo, haz commit y push. El workflow se re-ejecutará.

### Paso 7: Comprobar el mural de clase

Accede a la URL del mural: `https://gtraver-edu.github.io/daw-cicd-clase/`

Verás las tarjetas de todos los compañeros que ya han contribuido. Cada tarjeta muestra un iframe con la página personalizada de cada uno.

**Pregunta 1:** ¿Qué archivo y qué líneas de código han provocado que tu contribución se despliegue automáticamente en el mural de clase al fusionarse el PR?

### Paso 8: Personalizar el color de fondo

Una vez tu contribución esté visible en el mural de clase, puedes cambiar el color de fondo de tu página individual:

1. En tu repositorio individual, edita `style.css`.
2. Busca la línea `background-color: #e0f7fa;` en el `body`.
3. Cámbiala por un color diferente. Elige uno en [htmlcolorcodes.com](https://htmlcolorcodes.com/es/).
4. Haz commit, push, y crea un nuevo PR en tu repo individual.
5. Fusiona el PR y espera a que se despliegue.
6. Comprueba que el iframe de tu tarjeta en el mural de clase ahora muestra tu nuevo color.

**Pregunta 2:** ¿Qué archivo y qué líneas de código de tu repositorio individual han hecho que este cambio de color se despliegue automáticamente tras fusionar el PR?

### Paso 9: Provocar un fallo de validación

Aprende qué pasa cuando la validación falla:

1. En tu fork del repositorio de clase, crea una nueva rama:
   ```bash
   git checkout -b feature/prueba-fallo
   ```
2. Revisa el workflow e intenta modificar un archivo para que falle la validación.
3. Abre un Pull Request con estos cambios.
4. Observa cómo el workflow **rechaza** tu PR con un mensaje de error.
5. Lee el log en la pestaña Actions para entender qué validación ha fallado.

> **Reflexión:** ¿Por qué es útil que el workflow rechace automáticamente cambios no permitidos?

## Referencia rápida de comandos Git

| Comando | Qué hace |
|---------|----------|
| `git clone <url>` | Descarga un repositorio |
| `git checkout -b <rama>` | Crea una rama nueva y se mueve a ella |
| `git branch` | Muestra en qué rama estás |
| `git add .` | Prepara todos los cambios para commit |
| `git add <archivo>` | Prepara un archivo concreto |
| `git commit -m "mensaje"` | Guarda los cambios con un mensaje |
| `git push origin <rama>` | Sube la rama al repositorio remoto |
| `git pull origin main` | Descarga los últimos cambios de main |

---

## Preguntas de reflexión

Cuando termines, piensa en estas preguntas (no es necesario entregarlas, pero son útiles para afianzar conceptos):

1. ¿Qué diferencia hay entre CI y CD? ¿Cuándo se ejecuta cada uno?
2. ¿Por qué trabajamos en ramas en vez de hacer push directo a `main`?
3. ¿Qué pasaría si dos personas modificaran el mismo archivo y ambas intentaran hacer un merge a `main`?
