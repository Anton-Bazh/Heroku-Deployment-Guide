# Manual detallado para subir y mantener una aplicación en Heroku

## Índice
1. [Preparación del proyecto](#1-preparación-del-proyecto)
    - 1.1. Crear el archivo `requirements.txt`
    - 1.2. Crear el archivo `Procfile`
    - 1.3. Configurar el archivo `.gitignore`
2. [Inicializar Git y conectar con Heroku](#2-inicializar-git-y-conectar-con-heroku)
    - 2.1. Inicializar un repositorio Git
    - 2.2. Crear una aplicación en Heroku
    - 2.3. Configurar el remoto de Heroku en Git
3. [Desplegar la aplicación en Heroku](#3-desplegar-la-aplicación-en-heroku)
4. [Actualizar la aplicación](#4-actualizar-la-aplicación)
5. [Notas adicionales](#5-notas-adicionales)

---

## 1. Preparación del proyecto

### 1.1. Crear el archivo `requirements.txt`
Este archivo lista las dependencias de tu aplicación. Para generarlo automáticamente, utiliza el siguiente comando en tu terminal:

```bash
pip freeze > requirements.txt
```

Esto generará un archivo `requirements.txt` con todas las bibliotecas instaladas en tu entorno virtual. Asegúrate de que contenga todas las dependencias necesarias para tu aplicación.

### 1.2. Crear el archivo `Procfile`
El `Procfile` le indica a Heroku cómo ejecutar tu aplicación. Este archivo debe:

- Estar en el directorio raíz del proyecto.
- Guardarse en formato UTF-8 con terminaciones de línea LF (Line Feed).
- No tener extensión (solo "Procfile").

Ejemplo de contenido:

```plaintext
web: gunicorn app:app
```

Aquí, `app:app` se refiere al archivo `app.py` y a la instancia de Flask llamada `app`.

### 1.3. Configurar el archivo `.gitignore`
Para evitar subir archivos innecesarios a Git, crea un archivo `.gitignore` con el siguiente contenido como base:

```plaintext
*.pyc
__pycache__/
env/
venv/
.DS_Store
```

Esto excluirá archivos temporales y carpetas de entornos virtuales.

---

## 2. Inicializar Git y conectar con Heroku

### 2.1. Inicializar un repositorio Git
Si no tienes un repositorio Git inicializado, hazlo con estos comandos:

```bash
git init
git add .
git commit -m "Initial commit"
```

### 2.2. Crear una aplicación en Heroku
Asegúrate de haber iniciado sesión en Heroku:

```bash
heroku login
```

Esto abrirá una ventana en tu navegador para que ingreses tus credenciales. Nota: Aunque Heroku ofrece un plan gratuito, necesitarás asociar una tarjeta de crédito a tu cuenta para habilitar ciertas funcionalidades.

Luego, crea una nueva aplicación en Heroku con este comando:

```bash
heroku create tu-nombre-app
```

Si no especificas un nombre, Heroku generará uno automáticamente.

### 2.3. Configurar el remoto de Heroku en Git
Conecta tu repositorio local con la aplicación de Heroku creada:

```bash
heroku git:remote -a tu-nombre-app
```

Verifica que Heroku esté configurado como remoto:

```bash
git remote -v
```

Esto debería mostrar algo similar a:

```plaintext
heroku  https://git.heroku.com/tu-nombre-app.git (fetch)
heroku  https://git.heroku.com/tu-nombre-app.git (push)
```

Si no aparece, vuelve a ejecutar el comando anterior.

---

## 3. Desplegar la aplicación en Heroku

Para desplegar tu aplicación, usa el siguiente comando:

```bash
git push heroku main
```

Nota: Si tu rama principal se llama `master` en lugar de `main`, utiliza:

```bash
git push heroku master
```

Heroku detectará automáticamente los cambios y desplegará tu aplicación. Una vez completado, Heroku mostrará la URL de tu aplicación (por ejemplo, `https://tu-nombre-app.herokuapp.com`).

Si Git solicita un nombre de usuario y contraseña, sigue estos pasos:

1. **Obtén tu token de API de Heroku**:

    ```bash
    heroku auth:token
    ```

    Esto devolverá un token que usarás como contraseña.

2. **Ingresa las credenciales**:
    - Nombre de usuario: Tu correo electrónico asociado a Heroku.
    - Contraseña: El token obtenido en el paso anterior.

---

## 4. Actualizar la aplicación

### 4.1. Realiza los cambios en tu código
Edita los archivos necesarios localmente. Si agregas nuevas dependencias, no olvides actualizarlas en `requirements.txt` con:

```bash
pip freeze > requirements.txt
```

### 4.2. Confirma los cambios en Git
Guarda tus actualizaciones en Git con estos comandos:

```bash
git add .
git commit -m "Descripción breve de los cambios"
```

### 4.3. Sube los cambios a Heroku
Envía tus actualizaciones con:

```bash
git push heroku main
```

Heroku reconstruirá y desplegará tu aplicación automáticamente.

---

## 5. Notas adicionales

- **Dominio personalizado**: Si configuras un dominio personalizado, asegúrate de actualizar los registros DNS en tu proveedor de dominios según las instrucciones de Heroku.
- **Logs de Heroku**: Si encuentras problemas, verifica los registros con:

    ```bash
    heroku logs --tail
    ```

- **Plan gratuito**: Aunque Heroku tiene un plan gratuito, este tiene límites de uso. Considera actualizar a un plan de pago si tu aplicación necesita más recursos.

---

Con esta guía, deberías poder desplegar y mantener tu aplicación en Heroku sin problemas. Si necesitas más detalles o encuentras algún inconveniente, no dudes en buscar soporte adicional.
