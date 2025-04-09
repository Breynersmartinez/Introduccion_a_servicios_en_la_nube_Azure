
## 📂 ¿Qué es Azure Files?

**Azure Files** proporciona **recursos compartidos de archivos totalmente gestionados** accesibles desde cualquier parte del mundo, mediante **SMB (Server Message Block)** o **NFS (en vista previa)**.

> ✅ Permite compartir archivos como en una red corporativa, pero con la elasticidad y redundancia de Azure.

---

## 🛠️ Características principales

| Función                             | Descripción                                                                 |
|-------------------------------------|-----------------------------------------------------------------------------|
| 📡 Accesible desde la nube y local | Montable en Windows, Linux, macOS, tanto en la nube como on-premises       |
| 📁 Compatibilidad SMB/NFS          | Usa protocolos estándar como SMB 3.0 y NFS (vista previa)                   |
| 🌍 Acceso global vía URL            | Cada archivo puede tener un URI accesible desde cualquier parte            |
| 🔐 Cifrado                         | Cifrado en reposo + cifrado en tránsito con SMB                            |
| 📌 Control de acceso temporal      | Uso de SAS (Shared Access Signature) para acceso seguro y limitado         |

---

## 🔄 Casos de uso comunes

| Caso de uso                                          | Beneficio principal                                                                 |
|------------------------------------------------------|--------------------------------------------------------------------------------------|
| 🛠️ Migración de apps locales                        | Mismo comportamiento de red: se puede montar como letra de unidad (`Z:\`, por ejemplo) |
| 🧾 Configuración compartida entre VMs               | Centralización de archivos de configuración accesibles desde varias VMs            |
| 👥 Herramientas compartidas entre desarrolladores   | Asegura versiones consistentes de herramientas y utilidades                        |
| 🧪 Registro y procesamiento diferido                | Guarda registros o métricas para análisis posterior                                |
| 🌐 Compartir archivos entre sedes                  | Ideal para entornos distribuidos con presencia geográfica múltiple                 |

---

## 🔒 Seguridad

| Seguridad en reposo     | Seguridad en tránsito      | Acceso controlado                                |
|-------------------------|----------------------------|--------------------------------------------------|
| Cifrado automático      | SMB 3.0 con cifrado activo | SAS Tokens (firma de acceso compartido)          |
| Integración con Azure AD| TLS para NFS (en vista previa) | Políticas de acceso granular y expiración de tokens |

---

## 🌐 Acceso desde cualquier parte del mundo

Cada archivo tiene un URI del tipo:

```
https://<storage-account-name>.file.core.windows.net/<share-name>/<file-path>
```

Y puede llevar **un token SAS** como este:

```
https://tailwindstorage.file.core.windows.net/tools/devutils.exe?<token_sas>
```

Este enlace puede:

- 🔐 Limitarse a cierto rango horario
- 🔑 Permitir solo lectura/escritura
- ⌛ Expirar automáticamente

---

## 🚀 ¿Cómo se monta un Azure File Share?

- **En Windows**:

```powershell
net use Z: \\tailwindstorage.file.core.windows.net\archivos /user:Azure\<storage-key> <storage-key>
```

- **En Linux**:

```bash
sudo mount -t cifs //tailwindstorage.file.core.windows.net/archivos /mnt/archivos -o vers=3.0,username=storage_account,password=storage_key,dir_mode=0777,file_mode=0777
```

---

## 🧩 Azure Files vs Azure Blob Storage

| Característica            | Azure Files                     | Azure Blob Storage               |
|---------------------------|----------------------------------|----------------------------------|
| Estilo de acceso          | Montable (SMB/NFS)               | Acceso mediante API HTTP/SDK     |
| Uso típico                | Recursos compartidos de red      | Datos no estructurados (logs, vídeos) |
| Estructura                | Carpeta y archivo                | Contenedor y blob                |
| Montaje en VMs            | Sí                               | No (a menos que uses BlobFuse)   |

