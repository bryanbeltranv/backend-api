# backend-api

API Gateway para sistema de comentarios

## Descripción

Backend API construido con Node.js y Express que funciona como gateway para un sistema de comentarios.

## Requisitos

- Node.js 18 o superior
- Docker (opcional)

## Instalación y ejecución local

```bash
npm install
npm start
```

La API estará disponible en `http://localhost:8080`

## Docker

### Construir imagen localmente

```bash
docker build -t backend-api .
```

### Ejecutar contenedor

```bash
docker run -p 8080:8080 backend-api
```

## Despliegue automático a DockerHub

Este repositorio incluye un workflow de GitHub Actions que automáticamente construye y publica la imagen Docker a DockerHub.

### Configuración de Secrets

Para que el workflow funcione, necesitas configurar los siguientes secrets en GitHub:

1. Ve a tu repositorio en GitHub
2. Navega a **Settings** → **Secrets and variables** → **Actions**
3. Agrega los siguientes secrets:

   - `DOCKERHUB_USERNAME`: Tu nombre de usuario de DockerHub
   - `DOCKERHUB_TOKEN`: Un token de acceso de DockerHub (recomendado) o tu contraseña

### Cómo crear un token de DockerHub

1. Inicia sesión en [DockerHub](https://hub.docker.com)
2. Ve a **Account Settings** → **Security**
3. Click en **New Access Token**
4. Dale un nombre descriptivo (ej: "github-actions")
5. Copia el token generado y úsalo como `DOCKERHUB_TOKEN`

### Triggers del workflow

El workflow se ejecuta automáticamente cuando:

- Se hace push a las ramas `main` o `master`
- Se crea un tag con formato `v*` (ej: `v1.0.0`)
- Se ejecuta manualmente desde la pestaña Actions

### Tags de imagen generados

- `latest`: Para commits en la rama principal
- `<branch-name>`: Tag con el nombre de la rama
- `v1.0.0`, `v1.0`, `v1`: Para tags semánticos
- `<branch>-<sha>`: Tag con el SHA del commit

### Ejemplo de uso de la imagen

```bash
docker pull <tu-usuario-dockerhub>/backend-api:latest
docker run -p 8080:8080 <tu-usuario-dockerhub>/backend-api:latest
```
