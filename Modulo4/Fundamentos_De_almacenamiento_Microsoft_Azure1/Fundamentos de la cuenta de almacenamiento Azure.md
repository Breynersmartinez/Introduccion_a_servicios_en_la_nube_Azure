
## ☁️ ¿Qué es Azure Storage?

Es un **servicio de almacenamiento en la nube** que permite guardar datos de todo tipo (archivos, blobs, colas, tablas, discos) con acceso seguro y alta disponibilidad.

> 📦 Ideal para: Sitios web, apps móviles, escritorios, máquinas virtuales (VMs), y más.

---

## 🔐 Cuenta de Azure Storage

Una **cuenta de almacenamiento** es el punto de entrada. Todo lo que guardes (blobs, archivos, colas, discos) estará dentro de esta cuenta.

| Característica                     | Detalle                                                                 |
|-----------------------------------|-------------------------------------------------------------------------|
| 🌐 Espacio de nombres único       | Accesible desde cualquier parte vía HTTP o HTTPS                       |
| 🔒 Seguridad integrada             | Cifrado en reposo y en tránsito, claves de acceso, roles RBAC          |
| 📈 Alta escalabilidad             | Capaz de manejar petabytes de datos                                    |
| 🟢 Alta disponibilidad             | Redundancia geográfica, copias automáticas                             |
| 💾 Durabilidad                    | Mecanismos para mantener integridad de datos frente a fallos           |

---

## 🧰 Tipos de almacenamiento en Azure Storage

| Tipo                         | Uso principal                                                               |
|------------------------------|------------------------------------------------------------------------------|
| **Blob Storage**             | Almacenamiento de objetos no estructurados (imágenes, vídeos, logs, etc.)   |
| **File Storage (Azure Files)** | Compartición de archivos mediante SMB, similar a un servidor de archivos     |
| **Queue Storage**            | Sistema de colas para mensajería entre componentes de aplicaciones           |
| **Table Storage**            | Almacenamiento NoSQL de datos estructurados                                 |
| **Disk Storage**             | Discos virtuales para máquinas virtuales (sólo se usan con VMs)              |

---

## ⚙️ ¿Cómo crear una cuenta de almacenamiento?

Puedes hacerlo por diferentes medios:

- 🖥️ **Portal de Azure** (interfaz visual)
- 💻 **Azure CLI** (`az storage account create ...`)
- 🧑‍💻 **Azure PowerShell** (`New-AzStorageAccount`)
- 📜 **Plantillas ARM o Bicep** para infraestructura como código

---

## 🧩 Ejemplo: Migración de archivos de Tailwind Traders

**Sally** quiere mover archivos al almacenamiento en la nube:

1. Crea una cuenta de almacenamiento (por ejemplo: `tailwindstorage`)
2. Dentro de la cuenta, crea un contenedor o recurso tipo **Azure File Share**
3. Carga archivos usando el portal, AzCopy, CLI o SDK
4. Accede a los archivos desde aplicaciones web, móviles o de escritorio usando una URL como:

```plaintext
https://tailwindstorage.blob.core.windows.net/documentos/informe2025.pdf
```

---

## 🛑 Importante

- **Azure Storage ≠ Azure Database Services**: Storage se usa para objetos y archivos. Las bases de datos (como SQL Database, Cosmos DB) son servicios separados y optimizados para consultas.
- **Azure Disk Storage** se usa **solo para VMs** — no se debe usar como almacenamiento general de archivos.

