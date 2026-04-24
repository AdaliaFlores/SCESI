# GIT

**Nombre:** Adalia Flores Escobar  
**Clase:** CLASE 1  

---

## ¿Qué es Git?
Git es un sistema de control de versiones distribuido que permite registrar y gestionar cambios en archivos a lo largo del tiempo.

Funciona como un sistema de "checkpoints", permitiendo volver a versiones anteriores del proyecto cuando sea necesario.

---

## Ventajas de Git
- Permite volver a versiones anteriores en caso de errores.
- Mantiene un historial completo de cambios.
- Facilita el trabajo colaborativo.
- Cada usuario tiene una copia completa del repositorio.

---

## Origen de Git
Git fue creado por Linus Torvalds en 2005.

Antes, el desarrollo del kernel de Linux se gestionaba mediante correos electrónicos. Luego se utilizó una herramienta llamada BitKeeper, pero debido a restricciones en su uso, se dejó de utilizar.

Como solución, Linus Torvalds desarrolló Git en pocas semanas, priorizando velocidad, seguridad y trabajo distribuido.

---

## Instalación en Linux

Verificar si Git está instalado:
```bash
git --version
```
---

# CLASE 2 - STATES Y COMMITS

---

## Estados de Git

Git maneja tres áreas principales:

### 1. DIRECTORIO DE TRABAJO (Working Directory)

Es donde estás trabajando directamente con tus archivos.

- Detecta cambios que haces en los archivos.

#### Estados dentro del directorio:

- **untracked**: Archivo nuevo que Git detecta pero aún no tiene versión previa.

- **modified**: Archivo que ya existe en Git pero ha sido modificado, eliminado o renombrado.

📌 **Nota:**  
Cualquier archivo que no esté en `.gitignore` entra automáticamente en estos estados.

---

### Ver estado de los archivos

```bash
git status
```

### Restaurar archivos

```bash
git restore nombreArchivo
```

⚠️ Elimina los cambios actuales (usar con cuidado).

### Archivo .gitignore

Crear archivo:

```bash
touch .gitignore
```

Editar:

```bash
nano .gitignore
```

**Función:** Indicar qué archivos o carpetas Git debe ignorar.

Ejemplo:
node_modules/
.env
*.log

---

### 2. STAGE AREA (Área de preparación)

Es donde seleccionas los archivos que quieres incluir en el próximo commit.

#### Agregar archivos al stage

```bash
git add nombreArchivo
```

#### Agregar todo:

```bash
git add .
```

#### Quitar archivos del stage

```bash
git restore --staged nombreArchivo
```

- Saca el archivo del área de preparación.
- Vuelve al estado `modified`.
- ❗ No elimina los cambios, solo los deselecciona.

---

### 3. REPOSITORIO LOCAL (Commits)

Aquí se guardan los cambios confirmados con un identificador único (ID).

#### Crear un commit

```bash
git commit -m "mensaje descriptivo"
```

Guarda todos los archivos del stage en el historial.

#### Volver al estado anterior (manteniendo cambios)

```bash
git reset --soft HEAD~1
```

Regresa el último commit al stage.

#### Modificar el último commit

```bash
git commit --amend -m "Nuevo mensaje"
```

Cambia el mensaje del último commit.

---

### Buenas prácticas en commits

#### ¿Cada cuánto hacer commits?

- Haz commits pequeños y frecuentes.
- Cada commit debe representar una tarea completa y significativa.

#### Cómo escribir buenos commits

✔ Usa verbos en imperativo:

- `add` → añadir
- `change` → modificar
- `fix` → corregir errores
- `remove` → eliminar

❌ Evita:

- Puntos finales (`.`)
- Puntos suspensivos (`...`)

Ejemplos:

```bash
git commit -m "Add new search feature"   ✔
git commit -m "Fix topbar bug"           ✔
git commit -m "Add new feature."         ✘
```

#### Longitud del mensaje

- Máximo recomendado: 50 caracteres
- Claro y conciso

#### Uso de prefijos en commits

Formato:

```bash
git commit -m "<tipo>: <descripción>"
```

Ejemplo:

```bash
git commit -m "feat: add search feature"
```

#### Prefijos más usados

| Prefijo | Uso |
|---------|-----|
| `feat:` | nueva funcionalidad |
| `fix:` | corrección de errores |
| `perf:` | mejora de rendimiento |
| `build:` | cambios en build o despliegue |
| `ci:` | integración continua |
| `docs:` | documentación |
| `refactor:` | refactorización |
| `style:` | formato (no afecta funcionalidad) |
| `test:` | pruebas |

Ejemplo:

```bash
git commit -m "docs: add fruits list to README"
```

#### Añadir más contexto al commit

Si necesitas explicar más:

```bash
git commit
```

Esto abre el editor. 

Ejemplo:
feat: add login system
Se implementa autenticación con JWT
y validación de credenciales

- Primera línea → título
- Siguientes líneas → descripción detallada

#### Ver historial de commits

Para verlo de manera resumida:

```bash
git log --online
```
#### Tamaño maximo que puedes subir a Github

Lo maximo que puedes subir es 100 MB

---

# CLASE 3 - GITHUB Y SSH

---

## ¿Qué es GitHub?

GitHub es una plataforma en la nube y red social para desarrolladores que permite alojar, gestionar y colaborar en proyectos de software utilizando Git.

---

## Git vs GitHub

| | Git | GitHub |
|---|---|---|
| **Qué es** | Sistema de control de versiones local | Plataforma en la nube |
| **Función** | Crea los "puntos de guardado" (commits) | Almacena y comparte esos commits |
| **Dónde vive** | En tu computadora | En internet |

> GitHub **usa** Git, pero no son lo mismo. Git puede existir sin GitHub, pero GitHub no existiría sin Git.

---

## SSH vs HTTPS

### HTTPS

Al clonar y usar un repositorio con HTTPS, GitHub te pedirá autenticarte **cada vez** que hagas un `push` o `pull`, incluyendo el uso de tokens de acceso personal. Esto puede volverse tedioso en el día a día.

### SSH

Con SSH configuras un par de claves criptográficas en tu máquina. Le entregas tu **clave pública** a GitHub, y desde ese momento tu computadora se autentica automáticamente sin necesidad de ingresar credenciales.

> 💡 **Recomendación:** Usa siempre SSH para trabajar con GitHub de forma más cómoda y segura.

---

## Configuración SSH

Ejecuta los siguientes comandos desde tu terminal (Linux/Mac) o Git Bash (Windows):

### 1. Generar el par de claves SSH

```bash
ssh-keygen -t ed25519 -C "tu-correo@email.com"
```

- `-t ed25519` → tipo de algoritmo de cifrado (el más moderno y seguro)
- `-C` → comentario para identificar la clave (usa el correo asociado a GitHub)

Cuando te pregunte dónde guardar la clave, presiona **Enter** para usar la ubicación por defecto (`~/.ssh/id_ed25519`).

### 2. Copiar la clave pública

```bash
cat ~/.ssh/id_ed25519.pub
```

Copia todo el contenido que aparece. Luego ve a **GitHub → Settings → SSH and GPG keys → New SSH key** y pégala.

### 3. Verificar la conexión

```bash
ssh -T git@github.com
```

Si todo salió bien, verás un mensaje como:
Hi TuUsuario! You've successfully authenticated...

---

## Crear un repositorio en GitHub

1. Ve a tu sección de repositorios: `https://github.com/TuUsuario?tab=repositories`
2. Haz clic en **"New"**
3. Escribe el nombre del repositorio y, opcionalmente, una descripción
4. Haz clic en **"Create repository"**

---

## Conectar un repositorio local con GitHub

> ⚠️ **Requisito previo:** ya debes haber ejecutado `git init` y tener al menos un commit (`git add . + git commit -m "Initial commit"`).

### 1. Vincular el repositorio remoto

```bash
git remote add origin git@github.com:TuUsuario/TuRepo.git
```

- `remote` → URL que apunta a tu repositorio en GitHub
- `origin` → apodo (alias) que Git le da por defecto a esa URL. Puedes cambiarlo, pero `origin` es la convención universal

### 2. Renombrar la rama principal a `main`

```bash
git branch -M main
```

Cambia el nombre de la rama por defecto de `master` a `main` (estándar actual de GitHub).

### 3. Subir los commits a GitHub

```bash
git push -u origin main
```

- `-u` → establece `origin main` como destino por defecto, así en el futuro solo necesitas escribir `git push`

---

## Clonar un repositorio de GitHub

```bash
git clone git@github.com:TuUsuario/TuRepo.git
```

### Si lo clonaste por error con HTTPS

Usa este comando para cambiar la URL remota a SSH y evitar autenticarte en cada operación:

```bash
git remote set-url origin git@github.com:TuUsuario/TuRepo.git
```

> 💡 Este mismo comando sirve también si quieres **cambiar el repositorio remoto** al que está conectado tu proyecto.

### Ver a qué repositorio remoto estás conectado

```bash
git remote -v
```

---

## Subir y bajar cambios

### Subir cambios → `git push`

```bash
git push origin <rama>
```

| Parte | Significado |
|---|---|
| `git push` | "Empuja" tus commits hacia el servidor |
| `origin` | El servidor remoto (GitHub) |
| `<rama>` | La rama que quieres subir (ej: `main`) |

### Bajar cambios → `git pull`

```bash
git pull origin <rama>
```

| Parte | Significado |
|---|---|
| `git pull` | "Trae" los commits del servidor a tu máquina |
| `origin` | El servidor remoto (GitHub) |
| `<rama>` | La rama de la que quieres traer cambios |

> 💡 `git pull` es equivalente a hacer `git fetch` + `git merge` en un solo paso.

---
