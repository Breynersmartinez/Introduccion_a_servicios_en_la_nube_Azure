# 🏗️ Fundamentos Arquitectónicos de Azure

## 📌 Estudio de Caso: Tailwind Traders

### 🏢 Contexto Actual
- **Infraestructura local**: Hardware físico en datacenter propio
- **Desafíos**:
  - Altos costos de mantenimiento
  - Escalabilidad limitada
  - Implementaciones lentas

### ☁️ Beneficios de Migrar a Azure
| Área | Beneficio | Ejemplo Tailwind Traders |
|------|----------|--------------------------|
| **Disponibilidad** | SLA garantizado | Sitio web sin downtime |
| **Escalabilidad** | Ajuste automático | Más VMs en temporadas altas |
| **Costos** | Modelo pay-as-you-go | Pago solo por tráfico real |
| **Implementación** | Configuración rápida | Nuevos entornos en minutos |
| **Híbrido** | Integración on-premise | Apps parcialmente en nube |

## 💡 Conceptos Clave de Nube

### 1. Modelos de Servicio
| Tipo | Responsabilidad | Ejemplo Azure |
|------|----------------|---------------|
| **IaaS** | Hardware virtualizado | Azure VMs |
| **PaaS** | Entorno de desarrollo | Azure App Service |
| **SaaS** | Software completo | Office 365 |

### 2. Ventajas Clave
- **Alta disponibilidad**: 99.9% - 99.99% SLA
- **Escalabilidad**:
  - Vertical (+CPU/RAM)
  - Horizontal (+instancias)
- **Elasticidad**: Autoescalado automático
- **Geodistribución**: 60+ regiones globales
- **DR/Backup**: Réplicas automáticas

### 3. Modelos Financieros
|  | CapEx (On-premise) | OpEx (Nube) |
|---|--------------------|-------------|
| **Inversión** | Alta inicial | Pay-as-you-go |
| **Mantenimiento** | Costo adicional | Incluido |
| **Flexibilidad** | Limitada | Escalado bajo demanda |

## 🛠️ Soluciones para Tailwind Traders

### 🌐 Sitio Web
- **Azure App Service** (PaaS)
  - Escalado automático
  - Parches automáticos
  - Integración continua

### 🖥️ Aplicaciones Híbridas
- **Azure Arc**: Gestión unificada
- **Azure Stack**: Nube privada local

### 💾 Base de Datos
- **Azure SQL Database**
  - Réplicas geográficas
  - Tuning automático

## 📊 Comparativa Costos
```bash
# On-premise vs Cloud
├── On-premise
│   ├── Servidores: $50,000 (CapEx)
│   ├── Mantenimiento: $15,000/año
└── Azure
    ├── App Service: $120/mes (OpEx)
    ├── SQL DB: $300/mes
    └── Ahorro estimado: 40-60%