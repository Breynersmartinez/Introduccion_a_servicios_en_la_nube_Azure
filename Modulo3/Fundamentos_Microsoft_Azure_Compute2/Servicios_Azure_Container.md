
## 🐳 **Contenedores: Lo esencial**

Un **contenedor** es una unidad ligera, autónoma y ejecutable de software que incluye todo lo necesario para que una aplicación se ejecute:

- Código
- Dependencias
- Variables de entorno
- Configuraciones

### ⚙️ Diferencias clave entre contenedores y máquinas virtuales

| Característica            | Máquinas Virtuales 🖥️         | Contenedores 🐳              |
|--------------------------|------------------------------|-----------------------------|
| Sistema operativo        | Incluyen uno completo        | Comparten el del host       |
| Tamaño                   | GB                           | MB                          |
| Tiempo de inicio         | Minutos                      | Segundos                    |
| Aislamiento              | Alto                         | Medio-alto                  |
| Recursos necesarios      | Elevados                     | Livianos                    |
| Escalabilidad            | Menos ágil                   | Súper rápida                |

---

## 🧩 ¿Por qué usar contenedores?

✅ **Ligereza**  
✅ **Portabilidad**: se ejecutan igual en desarrollo y producción  
✅ **Escalado veloz**  
✅ **Automatización fácil (CI/CD)**  
✅ **Menor consumo de recursos que las VMs**  
✅ **Ideal para microservicios**

---

## 🛠️ Azure y los contenedores

Azure ofrece **varios servicios para trabajar con contenedores**, dependiendo de tu nivel de control, complejidad y escalabilidad:

### 1. **Azure Container Instances (ACI)**
- Para tareas simples o aisladas.
- Ideal para ejecutar contenedores sin orquestación.
- Ejemplo: procesamiento por lotes, scripts periódicos, apps pequeñas.

### 2. **Azure Kubernetes Service (AKS)**
- Plataforma completa de orquestación de contenedores.
- Ideal para microservicios, aplicaciones distribuidas y escalado automático.

### 3. **Azure App Service for Containers**
- Despliega contenedores en entornos totalmente administrados.
- Útil para aplicaciones web rápidas sin preocuparte por la infraestructura.

---

## 🧪 Contenedor con Docker: ejemplo básico

### Dockerfile

```Dockerfile
# Imagen base
FROM node:18

# Establecer directorio de trabajo
WORKDIR /app

# Copiar archivos y dependencias
COPY package*.json ./
RUN npm install
COPY . .

# Puerto y comando
EXPOSE 3000
CMD ["node", "app.js"]
```

### Comandos para construir y correr

```bash
docker build -t mi-app .
docker run -p 3000:3000 mi-app
```

---

## 🔐 Seguridad en contenedores

- Usa imágenes oficiales o verificadas.
- Escanea imágenes en Azure Container Registry.
- Mantén separados los secretos (usa Azure Key Vault).
- Aplica control de acceso y redes privadas (VNETs en AKS).

---

## 🎯 Cuándo usar contenedores

| Escenario | ¿Contenedores? |
|-----------|----------------|
| Migrar apps monolíticas | ❌ Mejor usar VMs o App Service |
| Microservicios | ✅ Ideal |
| Escalado rápido | ✅ Sí |
| Portabilidad entre entornos | ✅ Muy útil |
| Despliegue rápido sin infraestructura | ✅ Azure Container Instances o App Service |

---

## 📦 Conclusión

Los **contenedores (con Docker y servicios de Azure)** te permiten ejecutar aplicaciones de forma ligera, escalable y portable, sin necesidad de administrar sistemas operativos completos como en las VMs. Son una excelente elección cuando necesitas desplegar múltiples instancias de una app en un mismo host y responder a la demanda en tiempo real.

