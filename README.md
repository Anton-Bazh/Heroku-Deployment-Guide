# Manual Profesional para Subir y Actualizar una Aplicación en Heroku

## Índice

1. [Requisitos previos](#requisitos-previos)
2. [Subir una aplicación a Heroku](#subir-una-aplicación-a-heroku)
   - 2.1. Crear un archivo `requirements.txt`
   - 2.2. Crear un archivo `Procfile`
   - 2.3. Inicializar un repositorio Git
   - 2.4. Crear una aplicación en Heroku
   - 2.5. Configurar el repositorio con Heroku
   - 2.6. Realizar el despliegue
3. [Actualizar una aplicación en Heroku](#actualizar-una-aplicación-en-heroku)
   - 3.1. Realizar cambios en el proyecto
   - 3.2. Confirmar los cambios con Git
   - 3.3. Subir los cambios a Heroku
4. [Notas adicionales](#notas-adicionales)

---

## Requisitos previos

Antes de comenzar, asegúrate de cumplir con los siguientes requisitos:

- Tener una cuenta en [Heroku](https://www.heroku.com/).
- Tener instalado [Git](https://git-scm.com/) en tu sistema.
- Tener instalado [Python](https://www.python.org/downloads/) y `pip` en tu sistema.
- Una tarjeta de crédito registrada en Heroku (necesaria incluso para el plan gratuito).

---

## Subir una aplicación a Heroku

### 2.1. Crear un archivo `requirements.txt`

Este archivo especifica las dependencias necesarias para tu aplicación. Puedes generarlo automáticamente con el siguiente comando en tu terminal:

```bash
pip freeze > requirements.txt
```

Asegúrate de que todas las dependencias necesarias estén listadas correctamente en este archivo.

### 2.2. Crear un archivo `Procfile`

El `Procfile` le indica a Heroku cómo ejecutar tu aplicación. Crea un archivo llamado `Procfile` (sin extensión) en la raíz de tu proyecto. 

El contenido típico para una aplicación Flask es:

```
web: gunicorn app:app
```

- **Nota:** Asegúrate de guardar este archivo con codificación **UTF-8** y formato de salto de línea **LF**.

### 2.3. Inicializar un repositorio Git

Si aún no tienes un repositorio Git inicializado, hazlo con estos comandos en tu terminal:

```bash
git init
git add .
git commit -m "Initial commit"
```

### 2.4. Crear una aplicación en Heroku

Inicia sesión en Heroku con el siguiente comando:

```bash
heroku login
```

Esto abrirá una ventana en tu navegador para que inicies sesión. Luego, crea una nueva aplicación en Heroku con:

```bash
heroku create nombre-de-tu-app
```

- Si no especificas un nombre, Heroku generará uno automáticamente.

### 2.5. Configurar el repositorio con Heroku

Conecta tu repositorio local con la aplicación en Heroku creada previamente:

```bash
heroku git:remote -a nombre-de-tu-app
```

Verifica que Heroku esté configurado como remoto con:

```bash
git remote -v
```

Esto debería mostrar algo como:

```
heroku  https://git.heroku.com/nombre-de-tu-app.git (fetch)
heroku  https://git.heroku.com/nombre-de-tu-app.git (push)
```

### 2.6. Realizar el despliegue

Envía tu código a Heroku con el siguiente comando:

```bash
git push heroku main
```

- **Nota:** Si tu rama principal se llama `master`, reemplaza `main` por `master` en el comando anterior. Puedes verificar el nombre de tu rama con:

```bash
git branch
```

---

## Actualizar una aplicación en Heroku

### 3.1. Realizar cambios en el proyecto

Edita los archivos de tu proyecto localmente en tu computadora como lo harías normalmente. Si agregas nuevas dependencias, recuerda actualizarlas en el archivo `requirements.txt` con:

```bash
pip freeze > requirements.txt
```

### 3.2. Confirmar los cambios con Git

Guarda tus actualizaciones en Git ejecutando los siguientes comandos:

```bash
git add .
git commit -m "Descripción breve de los cambios"
```

### 3.3. Subir los cambios a Heroku

Envía tus actualizaciones a Heroku con este comando:

```bash
git push heroku main
```

Heroku detectará automáticamente los cambios, reconstruirá tu aplicación y la desplegará con las actualizaciones.

---

## Notas adicionales

- **Depuración:** Si encuentras errores durante el despliegue, consulta los registros de Heroku con:

  ```bash
  heroku logs --tail
  ```

- **SSL:** Para habilitar HTTPS en tu dominio personalizado, configura un certificado SSL desde el panel de Heroku.

- **Planes de Heroku:** Aunque el plan gratuito es suficiente para muchas aplicaciones, considera actualizar a un plan de pago si necesitas más recursos.

- **Cuidado con las dependencias:** Verifica regularmente que las versiones de tus dependencias sean compatibles entre sí.

