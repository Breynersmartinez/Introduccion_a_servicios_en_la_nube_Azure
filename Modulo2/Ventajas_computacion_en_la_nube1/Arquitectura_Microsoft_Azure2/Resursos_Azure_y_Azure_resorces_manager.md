

## 📁 Recursos y Grupos de Recursos

Una vez creada una suscripción en Azure, puedes comenzar a crear **recursos** y organizarlos en **grupos de recursos**. Estos conceptos son fundamentales para trabajar eficientemente en la nube.

### 🔹 ¿Qué es un Recurso?

Un **recurso de Azure** es un **elemento administrable** disponible a través de la plataforma. Ejemplos de recursos:

- Máquinas virtuales (VM)
- Cuentas de almacenamiento
- Aplicaciones Web
- Bases de datos (como SQL o Cosmos DB)
- Redes virtuales
- Azure Application Gateway

> Todo recurso creado en Azure debe estar asociado a un **grupo de recursos**.

---

### 🔸 ¿Qué es un Grupo de Recursos?

Un **grupo de recursos** es un **contenedor lógico** que organiza y administra recursos relacionados para una solución de Azure.

#### 🧰 Características clave:

- Todos los recursos deben pertenecer a un único grupo de recursos.
- Un recurso **solo puede estar en un grupo de recursos a la vez**.
- Algunos recursos pueden moverse entre grupos; otros tienen **limitaciones específicas**.
- Los grupos **no se pueden anidar**.
- Un grupo **debe existir** antes de crear recursos.

#### 🎯 ¿Por qué usar grupos de recursos?

- **Organización lógica** por tipo, ubicación, uso o ciclo de vida.
- Facilita la **administración de acceso** (mediante RBAC).
- Permite **eliminar un conjunto completo de recursos** fácilmente.
- Ideal para **entornos no productivos** (desarrollo, pruebas, experimentación).
- Mejora el orden y reduce el desorden en suscripciones con muchos recursos.

> 🧼 Ejemplo: Si estás probando una solución temporal, puedes agrupar todos sus recursos en un solo grupo. Al finalizar, simplemente eliminas el grupo y todo su contenido se borra.

---

## 🧠 Azure Resource Manager (ARM)

**Azure Resource Manager (ARM)** es el servicio de implementación y administración que permite interactuar con los recursos de Azure.

### 🛠️ ¿Qué hace ARM?

- Gestiona solicitudes enviadas desde:
  - Azure Portal
  - Azure PowerShell
  - Azure CLI
  - SDKs y APIs REST

- Autentica y autoriza cada solicitud.
- Envía la acción solicitada al servicio de Azure correspondiente.
- Garantiza una experiencia **coherente** entre herramientas.

### 🌟 Ventajas del uso de ARM

- Implementación mediante **plantillas declarativas (ARM templates)**.
- Gestión de todos los recursos de una solución **como un solo grupo**.
- Permite la **reimplementación coherente** a lo largo del ciclo de vida del desarrollo.
- Definición clara de **dependencias** y orden de despliegue.
- Aplicación de **control de acceso** nativo (RBAC).
- Uso de **etiquetas** para organizar y clasificar recursos.
- Monitoreo y facturación más clara gracias a las etiquetas.

> 💡 Las funcionalidades publicadas a través de las APIs estarán disponibles en el Portal de Azure **180 días después de su lanzamiento** inicial.


