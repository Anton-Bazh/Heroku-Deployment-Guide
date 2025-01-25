Este manual te guía paso a paso para desplegar y actualizar una aplicación en Heroku utilizando un dominio personalizado. Incluye detalles claros y ejemplos prácticos.

---

## **Índice**

1. [Requisitos previos](#requisitos-previos)
2. [Configuración inicial del proyecto](#configuracion-inicial-del-proyecto)
3. [Despliegue en Heroku](#despliegue-en-heroku)
4. [Vincular un dominio personalizado](#vincular-un-dominio-personalizado)
5. [Actualizar la aplicación](#actualizar-la-aplicacion)
6. [Solución de problemas comunes](#solucion-de-problemas-comunes)

---

## **1. Requisitos previos**

Antes de comenzar, asegúrate de tener:

- Una cuenta activa en [Heroku](https://heroku.com/).
- Heroku CLI instalado. [Instrucciones de instalación](https://devcenter.heroku.com/articles/heroku-cli).
- Git instalado y configurado.
- Un proyecto configurado localmente (por ejemplo, una aplicación Flask o Node.js).
- Un dominio personalizado si deseas usarlo.

---

## **2. Configuración inicial del proyecto**

### 2.1. Crear un archivo `requirements.txt`

Lista todas las dependencias necesarias para tu aplicación en este archivo. Ejemplo para Flask:

```
Flask==3.1.0
Gunicorn==23.0.0
```

Guarda este archivo en la raíz de tu proyecto.

### 2.2. Crear un archivo `Procfile`

Este archivo indica a Heroku cómo ejecutar tu aplicación. Crea un archivo llamado `Procfile` (sin extensión) en la raíz de tu proyecto con este contenido:

```
web: gunicorn app:app
```

- `app:app` se refiere a tu archivo principal (`app.py`) y la instancia de Flask (`app`).

---

## **3. Despliegue en Heroku**

### 3.1. Inicializar Git y hacer el primer commit

```bash
git init
git add .
git commit -m "Initial commit for Heroku deployment"
```

### 3.2. Crear una aplicación en Heroku

```bash
heroku create <nombre-de-tu-app>
```

Si no especificas un nombre, Heroku generará uno automáticamente.

### 3.3. Conectar el repositorio local a Heroku

```bash
heroku git:remote -a <nombre-de-tu-app>
```

### 3.4. Subir el proyecto a Heroku

```bash
git push heroku main
```

> Nota: Si tu rama principal no se llama `main`, reemplaza `main` con el nombre correcto (por ejemplo, `master`).

### 3.5. Verifica el despliegue

Accede al dominio proporcionado por Heroku:

```
https://<nombre-de-tu-app>.herokuapp.com
```

---

## **4. Vincular un dominio personalizado**

### 4.1. Añadir el dominio a Heroku

```bash
heroku domains:add www.tudominio.com
```

### 4.2. Configurar los registros DNS

1. Accede al panel de administración de tu dominio.
2. Configura los registros DNS:
   - **Tipo A**:
     - `@` → `75.2.60.5`
     - `@` → `99.83.190.102`
   - **CNAME**:
     - `www` → `www.tudominio.com`

### 4.3. Verificar SSL

Heroku configura automáticamente un certificado SSL para dominios personalizados.

```bash
heroku certs:auto:enable
```

---

## **5. Actualizar la aplicación**

### 5.1. Realizar cambios en el código

Edita los archivos localmente y guarda los cambios.

### 5.2. Subir los cambios a Heroku

```bash
git add .
git commit -m "Descripción de los cambios"
git push heroku main
```

Heroku reconstruirá y desplegará automáticamente tu aplicación.

---

## **6. Solución de problemas comunes**

### Problema: El dominio personalizado muestra un candado rojo

- Asegúrate de haber configurado los registros DNS correctamente.
- Verifica que SSL esté habilitado con:

```bash
heroku certs:auto
```

### Problema: No puedo subir cambios

- Verifica que Heroku esté configurado como remoto:

```bash
git remote -v
```

- Si no aparece, conéctalo de nuevo:

```bash
heroku git:remote -a <nombre-de-tu-app>
```

---

## **Recursos adicionales**

- [Documentación oficial de Heroku](https://devcenter.heroku.com/)
- [Configuración de dominios en Heroku](https://devcenter.heroku.com/articles/custom-domains)
- [Uso de Git con Heroku](https://devcenter.heroku.com/articles/git)

---

Con este manual, deberías tener todo lo necesario para desplegar y gestionar aplicaciones en Heroku con éxito. ¡Buena suerte!
