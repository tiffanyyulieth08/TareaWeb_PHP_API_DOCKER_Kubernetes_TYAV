# Aplicación PHP con API de Clima + Docker + Kubernetes
# Autor: Tiffany Alfaro Valverde
- Descripción
* Esta es una aplicación web básica desarrollada en PHP que consume la API pública de Open-Meteo para mostrar información del clima actual. 

* Requisitos Previos
- Windows 10/11 
- Docker Desktop instalado y funcionando
- WSL2 habilitado
- Kubernetes habilitado en Docker Desktop 
- PowerShell actualizado

* Estructura del Proyecto

php-clima-k8s/
├── index.php                   # Aplicación PHP principal
├── Dockerfile                  # Configuración de la imagen Docker
├── k8s-deployment.yaml         # Manifiesto de Kubernetes
     
Instrucciones 
1. Clonar el Proyecto
# Crear carpeta del proyecto
mkdir C:\Tarea\ProyectoClima
cd C:\Tarea\ProyectoClima

# Copiar todos los archivos del proyecto en esta carpeta
2. Construir la Imagen Docker desde PowerShell, en la carpeta del proyecto.

# Construir la imagen Docker
docker build -t php-clima-api:v1 .

# Verificar que la imagen se creó correctamente
docker images | findstr "php-clima-api"

3. Probar Localmente
# Ejecutar contenedor de prueba
docker run -d -p 8080:80 --name php-clima-test php-clima-api:v1

# Acceder en el navegador: http://localhost:8080 

# Detener y eliminar contenedor de prueba
docker stop php-clima-test
docker rm php-clima-test

4. Desplegar en Kubernetes

# Aplicar el manifiesto de Kubernetes
kubectl apply -f k8s-deployment.yaml

# Verificar el estado del pod
kubectl get pods

# Verificar el servicio
kubectl get service php-clima-service

5. Acceder a la Aplicación
Acceda a la aplicación en el navegador:

# http://localhost:30080

Comandos útiles para verificar el estado:
# Ver todos los pods
kubectl get pods
# Ver detalles del pod específico
kubectl describe pod <nombre-pod>
# Ver servicios
kubectl get services
# Ver logs del pod
kubectl logs <nombre-pod>

* Estado esperado:
- Pod: Estado Running
- Service: Tipo NodePort con puerto 30080 accesible

# Uso de la Aplicación
- La aplicación muestra por defecto el clima mediante una API.
-  Se puede ingresar coordenadas personalizadas.
- Haga clic en "Consultar clima" para actualizar la información


# Solución de Problemas Comunes
Si Kubernetes no está funcionando:
- Verifique que Docker Desktop esté ejecutándose
- Confirme que Kubernetes esté habilitado en Docker Desktop Settings
- Si el puerto 30080 está en uso:
* Modifique el valor nodePort rango 30000-32767
- Vuelva a aplicar el manifiesto: kubectl apply -f k8s-deployment.yaml

Repositorio GitHub
# https://github.com/tiffanyyulieth08/TareaWeb_PHP_API_DOCKER_Kubernetes_TYAV.git

