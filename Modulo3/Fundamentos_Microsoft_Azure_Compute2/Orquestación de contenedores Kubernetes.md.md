

## ☸️ ¿Qué es Kubernetes?

**Kubernetes** (K8s) es una plataforma de **orquestación de contenedores** de código abierto que automatiza el despliegue, escalado, mantenimiento y operación de contenedores.

> Piensa en Kubernetes como el "cerebro" que organiza cómo, cuándo y dónde deben ejecutarse tus contenedores.

---

## 🎯 ¿Por qué usar Kubernetes?

Kubernetes ayuda a resolver problemas comunes al manejar aplicaciones modernas distribuidas en contenedores:

✅ **Alta disponibilidad (HA)**  
✅ **Escalabilidad automática**  
✅ **Balanceo de carga**  
✅ **Autorreparación (autohealing)**  
✅ **Despliegues sin interrupciones (rolling updates)**  
✅ **Gestión declarativa (infraestructura como código)**  
✅ **Aislamiento y seguridad entre servicios**

---

## 🔧 Componentes Clave de Kubernetes

| Componente | Descripción |
|------------|-------------|
| **Pod** | Unidad más pequeña de ejecución (1+ contenedores que comparten red y almacenamiento). |
| **Node** | Máquina (física o virtual) donde se ejecutan los Pods. |
| **Cluster** | Conjunto de nodos gestionados por Kubernetes. |
| **Deployment** | Define cómo se crean y administran múltiples réplicas de Pods. |
| **Service** | Expone los Pods como un servicio estable con una IP fija. |
| **ConfigMap / Secret** | Almacenan configuraciones y datos sensibles (como contraseñas o claves). |
| **Ingress** | Gestiona el acceso externo (URLs, HTTPS, etc.) a los servicios. |

---

## 🛠️ ¿Qué es AKS (Azure Kubernetes Service)?

**AKS** es el servicio de Kubernetes administrado por Azure. Con AKS:

- Microsoft administra el plano de control (Kubernetes Master).
- Tú administras los **nodos de trabajo**, aplicaciones y configuraciones.
- Se integra fácilmente con servicios como Azure DevOps, Container Registry (ACR), Azure Monitor, etc.

---

## 🚀 ¿Qué puedes hacer con AKS?

### 📦 Desplegar microservicios
Cada microservicio (por ejemplo, pagos, carrito, productos) se ejecuta en su propio contenedor y se orquesta mediante Kubernetes.

### 🔄 Escalado automático
AKS puede aumentar o reducir el número de réplicas de tus Pods según la carga de CPU/memoria.

### 💥 Autoreparación
Si un contenedor falla, Kubernetes lo reemplaza automáticamente.

### 🚧 Despliegues controlados
Puedes hacer **rolling updates** sin tiempos de inactividad, o **rollback** si algo sale mal.

### 🔐 Seguridad
Configura secretos, RBAC, integración con Azure Active Directory y políticas de red.

---

## 🧪 Ejemplo simple: Desplegar una app en AKS

```yaml
# deployment.yaml
apiVersion: apps/v1
kind: Deployment
metadata:
  name: mi-app
spec:
  replicas: 3
  selector:
    matchLabels:
      app: mi-app
  template:
    metadata:
      labels:
        app: mi-app
    spec:
      containers:
      - name: mi-app
        image: mi-registro.azurecr.io/mi-app:1.0
        ports:
        - containerPort: 80
```

```yaml
# service.yaml
apiVersion: v1
kind: Service
metadata:
  name: mi-app-service
spec:
  type: LoadBalancer
  selector:
    app: mi-app
  ports:
  - protocol: TCP
    port: 80
    targetPort: 80
```

---

## 📈 ¿Cuándo usar Kubernetes (AKS)?

| Necesidad | ¿Es buena idea usar AKS? |
|-----------|---------------------------|
| App monolítica | ❌ No es ideal |
| Microservicios | ✅ Sí |
| Escalado bajo demanda | ✅ Sí |
| Contenedores pequeños y aislados | ⚠️ Mejor con Azure Container Instances |
| Automatización y CI/CD | ✅ Muy compatible |
| Recursos limitados / no expertos en K8s | ⚠️ Puede ser complejo |

---

## 🧠 Conclusión

Usar **Kubernetes (AKS)** te da una plataforma poderosa y flexible para orquestar tus contenedores y escalar tus aplicaciones según demanda. Es ideal para arquitecturas modernas de microservicios y despliegues cloud-native.

