

## 🎯 **Objetivo de la lección**
Al finalizar esta lección, podrás:
- 📦 Describir y comparar **Azure Blob Storage**, **Azure Disk Storage** y **Azure File Storage**.
- 🎛️ Comprender los **niveles de acceso en Azure Blob Storage**.
- 💡 Aplicar el conocimiento a un escenario real de migración empresarial.

---

## 🧪 **Estudio de caso: Tailwind Traders**
**Situación**:
- La empresa tiene una variedad de archivos de marketing, ventas y soporte.
- Actualmente, estos archivos están alojados en **servidores web locales**.
- Están migrando a la nube para:
  - 🌍 Aprovechar la distribución geográfica.
  - ⚙️ Reducir infraestructura física.
  - 📈 Mejorar escalabilidad y acceso global.

---

## 📦 **Opciones de almacenamiento en Azure**

### 1. **Azure Blob Storage**
- 🔹 Ideal para **archivos no estructurados** como imágenes, documentos, videos.
- 🔹 Ofrece **varios niveles de acceso**:
  - **Hot (Activo)**: para archivos accedidos con frecuencia.
  - **Cool (Frío)**: para archivos que se usan ocasionalmente.
  - **Archive (Archivo)**: para archivos que rara vez se usan.
- 📍 **Recomendado para Tailwind**: ✅ Imágenes de productos, folletos PDF, hojas de datos.

### 2. **Azure File Storage**
- 🔹 Ofrece recursos compartidos de archivos a través de **SMB o NFS**.
- 🔹 Compatible con sistemas Windows, Linux y macOS.
- 🔹 Se accede como si fuera un disco compartido de red.
- 📍 **Recomendado para Tailwind**: ✅ Compartir archivos de soporte entre equipos internos.

### 3. **Azure Disk Storage**
- 🔹 Diseñado para discos duros virtuales (VHD) conectados a máquinas virtuales.
- 🔹 No es adecuado para compartir archivos directamente entre usuarios.
- 📍 **Recomendado para Tailwind**: ❌ No es la mejor opción para marketing o distribución de archivos.

---

## 🌐 **Recomendación para Tailwind Traders**

| Tipo de archivo       | Recomendación de Azure Storage | Nivel de acceso sugerido |
|------------------------|-------------------------------|---------------------------|
| Imágenes de productos  | Blob Storage                  | Hot                       |
| Folletos y hojas de datos | Blob Storage               | Hot / Cool                |
| Archivos de soporte    | File Storage                  | N/A                       |
| Registros antiguos     | Blob Storage                  | Archive                   |

---

## ✅ **Ventajas clave de migrar a Azure**

| Beneficio                             | Explicación                                                                 |
|--------------------------------------|------------------------------------------------------------------------------|
| 🌍 Acceso global                      | Se puede acceder a los archivos desde cualquier lugar con conexión a Internet |
| 🔐 Seguridad                          | Cifrado en reposo y en tránsito                                             |
| 💵 Costos optimizados                 | Diferentes niveles de acceso permiten ahorrar según el uso                 |
| ⚙️ Escalabilidad automática           | Azure maneja la infraestructura, sin necesidad de servidores físicos        |

