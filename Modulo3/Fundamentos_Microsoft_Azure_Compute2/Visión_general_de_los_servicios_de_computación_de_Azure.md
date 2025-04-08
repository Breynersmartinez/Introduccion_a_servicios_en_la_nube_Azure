

## 🔍 Resumen de los principales servicios de Azure Compute

| Servicio                          | Tipo       | ¿Qué hace?                                                                 | ¿Cuándo usarlo? |
|----------------------------------|------------|----------------------------------------------------------------------------|------------------|
| **Azure Virtual Machines**       | IaaS       | Máquinas virtuales personalizables. Control total del SO y software.       | Cuando necesitas control total sobre el entorno o ejecutar software personalizado. |
| **Virtual Machine Scale Sets**   | IaaS       | Grupo de VMs idénticas con autoescalado y balanceo de carga.               | Cuando necesitas alta disponibilidad y escalar apps rápidamente. |
| **Azure Container Instances (ACI)** | PaaS    | Ejecuta contenedores de forma rápida sin gestionar infraestructuras.       | Para cargas puntuales o pruebas, o despliegues rápidos. |
| **Azure Kubernetes Service (AKS)** | PaaS    | Orquestación completa de contenedores a escala con Kubernetes.             | Para microservicios distribuidos o apps que requieren escalado avanzado. |
| **Azure App Service**            | PaaS       | Plataforma totalmente gestionada para apps web, móviles y APIs.            | Cuando quieres enfocarte en el código y no en la infraestructura. |
| **Azure Functions**              | Serverless | Ejecuta pequeñas funciones en respuesta a eventos sin preocuparte del servidor. | Para automatizaciones, tareas de backend o arquitectura basada en eventos. |

---

## 🧠 Conceptos clave que aprendiste

- **Azure Compute** = servicio de **recursos informáticos bajo demanda**.
- **Paga solo por lo que usas**, ideal para presupuestos ajustados.
- Compatible con **varios sistemas operativos y servicios empresariales** (Linux, Windows, SAP, etc.).
- Puedes usarlo tanto para **pruebas, desarrollo** como para entornos de **producción a gran escala**.

---

## 🎯 Aplicación práctica para Tailwind Traders

| Necesidad de Tailwind Traders                         | Solución de Azure recomendada                         |
|--------------------------------------------------------|-------------------------------------------------------|
| Sitio web no soporta demanda durante picos             | Azure Virtual Machine Scale Set o AKS                |
| Necesitan subir nuevas versiones de la app rápido      | Azure App Service o Azure Container Instances         |
| Automatizar tareas breves (como enviar correos o logs) | Azure Functions (arquitectura sin servidor)           |
| Pruebas de nuevas funciones con contenedores           | Azure Container Instances (ACI)                       |
| Despliegue de microservicios                           | Azure Kubernetes Service (AKS)                        |

---

## 💡 Recomendación general

Empieza eligiendo **la solución más sencilla posible** para tu necesidad actual. Luego, si tu carga crece o se vuelve más compleja, puedes migrar a servicios más avanzados como AKS o Scale Sets.

