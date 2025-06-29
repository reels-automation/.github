# Aprendiendo con personajes

Aprendiendo con personajes es un proyecto que tiene como objetivo la creación de videos de manera automática en formato Reels.

## Arquitectura

La aplicación tiene una arquitectura de microservicios, cada etapa del proceso de creación de un reel es un microservicio distinto. Los microservicios interactuan entre sí utilizando Kafka.
Como ejecutar
### Api Gateway

Es la api central del sistema, conecta el frontend con el resto de microservicios.

### Frontend

Es el frontend de la aplicación

### Prompt Generator

Envía un prompt a un modelo de lenguaje local para crear el guión del video en base a un tema.

### Tts Rvc

Convierte el texto generado por el microservicio "Prompt Generator" en un audio utilizando un modelo de voz y luego convirtiendo esa voz a la de un personaje.
Este repositorio es un Fork de [rvc-cli](https://github.com/blaisewf/rvc-cli)

### Subtitle Generator

Genera subtitulos en formato json en base a un audio generado por el microservicio "Tts Rvc".

### Video Creator

Genera un video en formato reel utilizando un gameplay de fondo, el audio generado por el microservicio "Tts Rvc" y los subtitulos generador por el microservicio "Subtitle Generator"

### Admin Api

Una api que accede a un Bucket privado de Minio para obtener los distitnos modelos de voz de los personajes, modelos de Vosk e imagenes para los videos. Permite sistematizar todos los assets para no guardarlos en una carpeta local.

## Tecnologías

### Backend y Microservicios

- **Python**: Lenguaje principal para los microservicios
- **FastAPI**: Framework web para la Api gateway.
- **PostgreSQL**: Base de datos para los usuarios
- **MongoDB**: Base de datos para los videos
- **Kafka**: Comunicación entre microservicios.
- **Minio**: Almacenamiento de assets como imágenes, videos, modelos de voz, etc.
- **Ollama**: Ejecución local de modelos de lenguaje.
- **Vosk**: Reconocimiento de voz para la generación de subtítulos.
- **RVC (Retrieval-based Voice Conversion)**: Generador de voz según modelo de personaje especifico.
- **Mercado Pago API**: Integración con la API para comprar Tokens para crear videos

### DevOps

- **Docker**: Contenerización de microservicios para facilitar despliegue y desarrollo. Docker compose para manejar varios contenedores a la vez
- **Github CI/CD**: Creación de imagenes cada vez que se hace push a main
- **Nginx**: Proxy reverso para acceder mediante el puerto 80 y 443
- **LetsEncrypt**: Permite obtener certificados SSL para el dominio
- **Duck Dns**: Permite asociar una subdominio a una IP dinamica

### Frontend

- **TypeScript**: Lenguaje principal del frontend
- **React**: Framework para el frontend
- **ShadCN**: Libreria para componentes de React
- **Tailwind CSS**: Framework para agregar estilos a los componentes visuales

## Como ejecutar

Para ejecutar la aplicación se deben levantar los siguientes docker compose

- [Docker compose Microservicios](https://github.com/reels-automation/aprendiendo-con-personajes-compose)
- [Docker compose Ollama](https://github.com/reels-automation/ollama-docker)
- [Docker compose Dependencias](https://github.com/reels-automation/reels-automation-docker-compose-new)

## Logros

Utilizando este proyecto logramos crear una cuenta de Instagram que sube estos reels de manera totalmente automática. La cuenta se puede visitar aca [@aprendiendo.con.personajes](https://www.instagram.com/aprendiendo.con.personajes/)
