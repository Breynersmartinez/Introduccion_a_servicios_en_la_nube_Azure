

# ☁️ Guía de Estructura Organizativa y Suscripciones en Azure

A medida que los operadores de **Tailwind** comienzan a utilizar Azure, es fundamental comprender cómo están organizados los recursos y cómo funcionan las suscripciones. Esta guía proporciona una descripción detallada de los conceptos clave.

---

## 📦 ¿Qué es un Recurso de Azure?

Un **recurso de Azure** es cualquier elemento administrable disponible en la plataforma. Ejemplos de recursos incluyen:

- Máquinas virtuales (VM)
- Cuentas de almacenamiento
- Aplicaciones web
- Bases de datos
- Redes virtuales

El uso de Azure **requiere una suscripción**, ya que esta proporciona acceso autenticado y autorizado a los productos y servicios de Azure.

---

## 🧾 Suscripciones de Azure

Una **suscripción de Azure** es:

- Una **unidad lógica** que agrupa servicios de Azure.
- Asociada a una **cuenta de Azure**, la cual se representa como una identidad en **Azure Active Directory (Azure AD)** o un directorio de confianza.

### 🔑 Funciones principales de una suscripción

- Aprovisionamiento de recursos
- Control de acceso
- Administración de costos y facturación
- Separación de entornos (producción, pruebas, desarrollo)

### 📊 Tipos de límites de suscripción

1. **Límite de facturación**
   - Determina cómo se organiza la facturación.
   - Permite generar facturas independientes por suscripción.
   - Útil para segmentar costos por equipo, proyecto o departamento.

2. **Límite de control de acceso**
   - Permite aplicar políticas distintas según el departamento o proyecto.
   - Controla qué usuarios tienen acceso a qué recursos, a través de políticas de suscripción.

> Es posible crear múltiples suscripciones para reflejar la estructura organizativa o para separar entornos y mejorar el cumplimiento normativo.

---

## 💳 Facturación en Azure

- Los **costos** se agregan a nivel de suscripción.
- Puedes usar **perfiles de facturación** para generar múltiples facturas con distintos métodos de pago dentro de una misma cuenta.
- Las **secciones de facturación** organizan los cargos por equipo, departamento o proyecto.

> Ejemplo: Una organización puede tener una factura unificada y múltiples secciones para distinguir entre producción, desarrollo y pruebas.

---

## 🛡️ Límites Técnicos de Suscripción

Cada suscripción está sujeta a **limitaciones técnicas**, por ejemplo:

- Máximo de **10 circuitos de Azure ExpressRoute** por suscripción.

> En caso de necesitar más recursos, se pueden crear suscripciones adicionales.

---

## 🏢 Grupos de Administración en Azure

Los **grupos de administración** permiten gestionar múltiples suscripciones bajo una jerarquía lógica.

### ⚙️ Funciones de los grupos de administración:

- Aplicación de políticas de gobernanza (seguridad, región, cumplimiento)
- Gestión centralizada de acceso (RBAC)
- Estandarización de configuraciones

### 📐 Características clave:

- Cada grupo puede tener **varios hijos**, pero **solo un padre**.
- Se admiten **hasta 10.000 grupos de administración** por directorio.
- La jerarquía puede tener hasta **6 niveles de profundidad** (sin incluir raíz ni suscripción).
- Todas las suscripciones y grupos se encuentran dentro de una **única jerarquía por directorio**.

### 🎯 Ejemplo práctico:

- Crear un grupo llamado **Producción** que limite la creación de VMs a una región específica.
- Todas las suscripciones dentro de ese grupo **heredan automáticamente** esa política.
- Asignar roles (RBAC) a nivel de grupo para simplificar la administración del acceso.

---

## 🧭 Diseño Recomendado de Jerarquía

Puedes diseñar una jerarquía flexible para:

- Separar recursos por equipos, departamentos o entornos.
- Aplicar políticas consistentes a gran escala.
- Controlar el acceso de forma centralizada.

> Este diseño favorece la gobernanza y la seguridad organizacional a gran escala.

---

## 📝 Conclusión

Comprender las suscripciones y la estructura organizativa en Azure es esencial para:

- Gestionar recursos eficientemente.
- Controlar costos y facturación.
- Asegurar el cumplimiento normativo y la seguridad.

¡Exploraremos cada uno de estos aspectos con más detalle a lo largo del curso!

