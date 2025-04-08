

## 🆚 Azure Container Instances (ACI) vs Azure Kubernetes Service (AKS)

| Característica | **Azure Container Instances (ACI)** | **Azure Kubernetes Service (AKS)** |
|----------------|-------------------------------------|-------------------------------------|
| 🧠 **Gestión** | Totalmente administrado, sin necesidad de infraestructura | Tú gestionas el clúster (aunque Azure ayuda con la administración base) |
| ⚙️ **Orquestación** | No tiene orquestador integrado | Kubernetes completo como orquestador |
| 🚀 **Facilidad de uso** | Súper fácil y rápido de desplegar | Más complejo, requiere conocimientos de Kubernetes |
| 📈 **Escalabilidad** | Escala manual o con lógica básica (cron, eventos) | Escalado automático avanzado (basado en carga, pods, nodos) |
| 💵 **Costo** | Ideal para cargas pequeñas o intermitentes | Económico para cargas grandes o persistentes |
| 🧩 **Integraciones** | Menos personalizable, pero rápido para tareas específicas | Muy flexible y extensible para microservicios complejos |
| 🧪 **Casos de uso** | Tareas por lotes, procesamiento rápido, pruebas, APIs simples | Microservicios, apps distribuidas, backends de producción |

---

## ✅ ¿Cuándo usar **Azure Container Instances (ACI)**?

ACI es perfecto si necesitas:

- Desplegar **contenedores rápidamente** sin configurar infraestructura.
- Ejecutar **tareas aisladas**, scripts, APIs livianas o procesamiento por lotes.
- Probar contenedores sin tener que montar todo un clúster.
- Automatizar procesos puntuales (por ejemplo, transformar archivos cuando se cargan en Blob Storage).
- Ahorrar dinero en cargas **no permanentes** (pagas por segundo de ejecución).

---

## 🛠️ ¿Cómo se gestiona un contenedor con **ACI**?

### 1. **Subes tu contenedor a un registro**
Puedes usar [Azure Container Registry](https://azure.microsoft.com/products/container-registry/) o Docker Hub.

### 2. **Creas una instancia de contenedor**
Desde el portal, la CLI o ARM:

```bash
az container create \
  --resource-group mi-grupo \
  --name mi-contenedor \
  --image mi-registro.azurecr.io/mi-imagen:latest \
  --cpu 1 \
  --memory 1 \
  --ip-address public
```

### 3. **Supervisión y control**
- **`az container show`**: Ver el estado.
- **`az container logs`**: Ver registros del contenedor.
- **Azure Monitor**: Para métricas y alertas.

---

## 💡 Extra: Orquestación con ACI + Kubernetes (Virtual Kubelet)

Aunque ACI **no tiene orquestación avanzada nativa**, se puede usar **como un nodo virtual dentro de un clúster AKS**, lo que combina lo mejor de ambos mundos:

- AKS maneja la lógica y distribución.
- ACI ejecuta tareas bajo demanda, sin afectar el clúster base.

---

## 🧠 Conclusión rápida

| Si necesitas... | Usa... |
|-----------------|--------|
| Ejecutar contenedores **rápido y sin complicaciones** | ✅ **ACI** |
| Gestionar muchos contenedores o apps distribuidas | ✅ **AKS** |
| Ejecutar tareas por lotes, pruebas o scripts simples | ✅ **ACI** |
| Orquestar, escalar y automatizar microservicios complejos | ✅ **AKS** |

