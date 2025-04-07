# ☁️ Modelos de Servicio en la Nube: IaaS, PaaS y SaaS

## 📌 Modelos de Responsabilidad Compartida

| Modelo          | Control del Usuario | Responsabilidad del Proveedor | Ejemplo Azure                  |
|-----------------|---------------------|-------------------------------|--------------------------------|
| **On-Premise**  | Hardware → Aplicación | Ninguna                       | Datacenter físico              |
| **IaaS**        | SO → Aplicación      | Hardware/Virtualización       | Azure Virtual Machines         |
| **PaaS**        | Solo Aplicación      | Hasta runtime                 | Azure App Service              |
| **SaaS**        | Uso                  | Todo el stack                 | Microsoft 365                  |

## 🔍 Profundizando en Cada Modelo

### 1. **IaaS (Infraestructura como Servicio)**
- **Qué proporciona Azure**: 
  - Virtualización (Hipervisor)
  - Servidores físicos
  - Redes y almacenamiento básico

- **Qué gestionas tú**:
  - Sistemas operativos
  - Middleware
  - Aplicaciones
  - Datos

- **Caso de uso ideal**:
  - Migración lift-and-shift
  - Entornos altamente personalizados

### 2. **PaaS (Plataforma como Servicio)**
- **Qué proporciona Azure**:
  - Entorno de ejecución
  - Herramientas de desarrollo
  - Servicios gestionados (DB, autenticación)

- **Qué gestionas tú**:
  - Código de aplicación
  - Configuraciones
  - Datos

- **Beneficios clave**:
  - ✔️ Actualizaciones automáticas
  - ✔️ Escalado integrado
  - ✔️ Menor overhead de gestión

### 3. **SaaS (Software como Servicio)**
- **Qué proporciona Azure**:
  - Aplicación completa
  - Infraestructura subyacente
  - Mantenimiento continuo

- **Qué gestionas tú**:
  - Configuración básica
  - Usuarios y permisos

- **Ejemplo avanzado**:
  - Azure Cognitive Services (IA como servicio)

## 📊 Evolución de Responsabilidades
```mermaid
graph LR
    A[On-Premise] -->|Menos control| B(IaaS)
    B --> C(PaaS)
    C -->|Máxima delegación| D(SaaS)