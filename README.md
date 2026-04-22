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