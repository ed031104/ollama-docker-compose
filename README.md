# Ollama con Docker Compose

Este repositorio contiene una configuración mínima de Docker Compose para ejecutar [Ollama](https://ollama.com/) en un contenedor.

## Cómo funciona

El archivo [docker-compose.yml](docker-compose.yml) levanta un único servicio:

- `ollama`: usa la imagen oficial `ollama/ollama`.
- Expone el puerto `11434`, que es el puerto por defecto de la API de Ollama.
- Monta el volumen `ollama_data` en `/root/.ollama` para conservar modelos y configuración entre reinicios.
- Reinicia automáticamente con `unless-stopped`.

También hay un bloque comentado para usar GPU con NVIDIA. Si tu máquina tiene GPU compatible, puedes descomentarlo y asegurarte de tener instalado NVIDIA Container Toolkit en el host.

## Requisitos

- Docker
- Docker Compose

## Ejecutar el proyecto

1. Inicia el servicio:

   ```bash
   docker compose up -d
   ```

2. Verifica que el contenedor esté corriendo:

   ```bash
   docker compose ps
   ```

3. Revisa los logs si lo necesitas:

   ```bash
   docker compose logs -f
   ```

## Probar Ollama

Una vez levantado el contenedor, la API queda disponible en:

```text
http://localhost:11434
```

Puedes descargar y ejecutar un modelo con:

```bash
docker compose exec ollama ollama pull llama3.2
docker compose exec ollama ollama run llama3.2
```

## Detener y limpiar

Para detener el servicio:

```bash
docker compose down
```

Si quieres borrar también los datos persistidos del volumen:

```bash
docker compose down -v
```

## Notas

- El volumen `ollama_data` conserva los modelos descargados.
- Si activas GPU, asegúrate de descomentar solo una versión válida del bloque de servicios en el compose y de tener soporte NVIDIA correctamente configurado.