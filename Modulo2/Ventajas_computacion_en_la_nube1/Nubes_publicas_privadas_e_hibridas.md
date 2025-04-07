# ☁️ Modelos de Implementación en la Nube

## 📌 Tipos de Implementación

| Modelo       | Propiedad           | Ubicación                | Ventajas                                  | Desventajas                |
|--------------|---------------------|--------------------------|------------------------------------------|----------------------------|
| **Pública**  | Proveedor cloud     | Centros datos proveedor  | Costos bajos, escalabilidad ilimitada    | Menor control de seguridad |
| **Privada**  | Organización        | On-premise o hospedada   | Máximo control, seguridad personalizada  | Altos costos iniciales     |
| **Híbrida**  | Combinación         | Ambos entornos           | Flexibilidad, migración gradual          | Complejidad de gestión     |

## 🔍 Profundizando en Cada Modelo

### 1. **Nube Pública** (Ej: Azure, AWS)
- **Características**:
  - Recursos compartidos multi-tenant
  - Pago por uso (OPEX)
  - Ejemplo: Azure Virtual Machines

- **Caso ideal**:
  > Startups que necesitan escalar rápido sin inversión inicial

### 2. **Nube Privada** (Ej: Azure Stack)
- **Implementaciones**:
  - **On-premise**: Hyper-V + System Center
  - **Hospedada**: Dedicated hosts en Azure

- **Caso ideal**:
  > Bancos con datos sensibles que requieren compliance estricto

### 3. **Nube Híbrida** (Ej: Azure Arc)
- **Conectividad clave**:
  - ExpressRoute (conexión dedicada)
  - VPN Site-to-Site

- **Caso Tailwind Traders**:
  ```mermaid
  graph LR
    A[ERP On-premise] -->|Azure Arc| B(Azure SQL DB)
    B --> C[Power BI en nube pública]