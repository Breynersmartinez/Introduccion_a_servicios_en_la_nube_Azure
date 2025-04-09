

## 💽 ¿Qué es Azure Disk Storage?

**Azure Disk Storage** proporciona discos duros virtuales (VHDs) que pueden conectarse a **máquinas virtuales (VMs)** en Azure. Es un almacenamiento **persistente** y de alto rendimiento que permite manejar datos como si estuvieras usando discos físicos en un entorno local.

---

## 🧰 Características clave

| Característica               | Detalle                                                                 |
|------------------------------|-------------------------------------------------------------------------|
| 🔗 Conectado a VMs           | Se adjunta a una VM como disco del sistema operativo o de datos         |
| 📂 Persistente                | Los datos se mantienen incluso si la VM se detiene o reinicia          |
| 💡 Fácil de escalar          | Agrega más discos según las necesidades de almacenamiento               |
| 📊 Altamente disponible       | SLA empresarial con replicación automática                              |
| 🔐 Seguro                     | Encriptación automática en reposo con claves gestionadas por Azure      |

---

## ⚙️ Tipos de discos disponibles

| Tipo de disco         | Descripción                                                                                     | Uso recomendado                                        |
|------------------------|-------------------------------------------------------------------------------------------------|--------------------------------------------------------|
| 🟢 **HDD estándar**     | Discos económicos con rendimiento moderado                                                     | Copias de seguridad, datos menos usados                |
| 🟡 **SSD estándar**     | Mejores IOPS y latencia que HDD, a bajo costo                                                  | Cargas de trabajo con baja IOPS y latencia moderada    |
| 🔵 **SSD premium**      | Alto rendimiento, baja latencia, ideal para producción                                         | Bases de datos, aplicaciones críticas                  |
| 🔴 **SSD ultra**        | Ultra rápido, ideal para cargas de trabajo exigentes y sensibles al rendimiento                | SAP HANA, bases de datos de misión crítica             |

---

## 🔁 Uso típico de discos en una VM

- **Disco del sistema operativo (OS)**: contiene el sistema operativo de la VM.
- **Discos de datos**: para almacenar archivos, bases de datos u otros datos.
- **Disco temporal**: almacenamiento local efímero que se borra al reiniciar la VM.

> 🎯 Cada disco puede tener diferentes niveles de rendimiento y estar optimizado según el tipo de carga de trabajo.

---

## 📉 Tasa de fallos

Azure ofrece una **tasa de fallos anualizada (AFR) de 0%**, una de las más bajas del sector, gracias a su redundancia y replicación integrada.

---

## 📐 Tamaños y rendimiento

Cada tipo de disco tiene diferentes opciones de tamaño que impactan directamente en:

- ✅ **Capacidad (GB o TB)**
- 🚀 **IOPS (operaciones de entrada/salida por segundo)**
- ⚡ **Throughput (MB/s)**

> Puedes consultar [la documentación oficial de Microsoft](https://learn.microsoft.com/es-es/azure/virtual-machines/disks-types) para una tabla detallada de rendimiento por tipo de disco.

---

## 🌍 Escenarios de uso

| Escenario                                              | Tipo de disco recomendado         |
|--------------------------------------------------------|-----------------------------------|
| Almacenamiento de archivos o copias de seguridad       | HDD estándar                      |
| Aplicaciones web o sistemas ERP pequeños               | SSD estándar                      |
| SQL Server, Oracle, aplicaciones críticas              | SSD premium                       |
| SAP HANA, análisis en tiempo real, alto rendimiento    | SSD ultra                         |

