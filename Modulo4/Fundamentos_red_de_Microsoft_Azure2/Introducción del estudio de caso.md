

## 🧭 **Objetivo de la lección**
Al completar esta lección, serás capaz de:
- 🕸️ Describir los principales recursos de red en Azure.
- 🔐 Explicar cuándo usar **Azure Virtual Network**, **VPN Gateway** y **ExpressRoute**.
- 🏗️ Aplicar estos conceptos en un caso de migración empresarial real.

---

## 🧪 **Estudio de caso: Tailwind Traders**
**Situación actual**:
- Tailwind ha migrado algunas aplicaciones a la nube y está diseñando otras.
- Sus **servidores de datos principales** están en Silicon Valley.
- Tienen **sucursales distribuidas** geográficamente.
- Quieren trasladar más recursos (como el sitio web) a la nube.
- Requieren acceso **seguro y eficiente** desde las sucursales a los datos privados.

---

## 🌐 **Opciones de red en Azure**

### 1. 🧠 **Azure Virtual Network (VNet)**
- Es el **fundamento** de la red en Azure, similar a una red local.
- Permite:
  - Conectar máquinas virtuales.
  - Definir subredes, direcciones IP, y grupos de seguridad.
  - Usar control de tráfico con **NSGs (Network Security Groups)** y **rutas personalizadas**.
- 📍 **Recomendado para Tailwind**: ✔️ Crear redes aisladas para distintas apps y ambientes (desarrollo, pruebas, producción).

---

### 2. 🔒 **Azure VPN Gateway**
- Proporciona una **conexión cifrada entre la red local y Azure** a través de Internet.
- Usa protocolos estándar como **IPSec/IKE**.
- Tipos:
  - **Site-to-Site (S2S)**: conecta sucursales con Azure.
  - **Point-to-Site (P2S)**: conecta usuarios individuales desde sus dispositivos.
- 📍 **Recomendado para Tailwind**: ✔️ Conectar sucursales y empleados remotos con los datos de Silicon Valley.

---

### 3. ⚡ **Azure ExpressRoute**
- Ofrece una **conexión privada y dedicada** entre la red local y Azure (no usa Internet).
- Ideal para:
  - Altas velocidades (hasta 100 Gbps).
  - Bajísima latencia.
  - Alta seguridad y confiabilidad.
- 📍 **Recomendado para Tailwind**: ✔️ Si necesitan una conexión de nivel empresarial entre el centro de datos en Silicon Valley y Azure.

---

## 🧩 **Resumen de uso para Tailwind Traders**

| Recurso de red         | ¿Para qué sirve? | ¿Tailwind lo necesita? | Ventaja principal                  |
|------------------------|------------------|-------------------------|------------------------------------|
| **Virtual Network**     | Crear redes privadas en la nube | ✅ Sí                      | Control de red similar al local    |
| **VPN Gateway**         | Conexión segura entre sucursales y Azure | ✅ Sí                      | Ahorro de costes usando Internet   |
| **ExpressRoute**        | Conexión privada de alto rendimiento | 🔄 Opcional (si hay presupuesto) | Máxima velocidad y seguridad       |

---

## 🎯 **Recomendación estratégica**
1. Crear una **Virtual Network principal en Azure**, con subredes para:
   - Aplicaciones web.
   - Bases de datos.
   - Servicios internos.
2. Implementar una **VPN Gateway Site-to-Site** para conectar las sucursales con Azure.
3. Si se requiere alto rendimiento o confidencialidad total, considerar **ExpressRoute** para enlazar el centro de datos de Silicon Valley directamente a Azure.

