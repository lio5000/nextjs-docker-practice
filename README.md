Contenerización de Aplicación Next.js con Docker

Este repositorio contiene una aplicación Next.js contenerizada utilizando Docker mediante una estrategia de Multi-Stage Build, lo que garantiza un entorno de desarrollo e implementación aislado, portable, ligero y consistente.

🛠️ Requisitos Previos
Node.js (v20+)
Docker Desktop ejecutándose en el sistema
🚀 Instrucciones de Uso

1. Construir la imagen de Docker

Para construir la imagen optimizada utilizando la configuración del Dockerfile, ejecuta el siguiente comando en la raíz del proyecto:

bash
docker build -t mi-app-nextjs . 2. Ejecutar el contenedor

Inicia el contenedor mapeando el puerto 3000 de tu máquina local con el puerto 3000 del contenedor:

bash
docker run -p 3000:3000 mi-app-nextjs

Accede a la aplicación desde cualquier navegador ingresando a:

👉 http://localhost:3000

📦 Arquitectura del Dockerfile (Multi-Stage Build)

El archivo Dockerfile utiliza 3 etapas estructuradas para optimizar el tamaño de la imagen final y mejorar la seguridad:

deps (Etapa de Dependencias): Utiliza la imagen base node:20-alpine para instalar únicamente las dependencias de producción y desarrollo definidas en el package-lock.json mediante npm ci.
builder (Etapa de Compilación): Copia el código fuente del proyecto y ejecuta el proceso de compilación npm run build para generar los archivos compilados en modo standalone.
runner (Etapa de Producción): Crea una imagen limpia en entorno de producción (NODE_ENV=production), configura un usuario del sistema sin privilegios root (nextjs) por buenas prácticas de seguridad y ejecuta el servidor ligero mediante node server.js.
