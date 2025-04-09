
## 🧊☁️ **Niveles de acceso en Azure Blob Storage**

Azure ofrece **tres niveles de acceso** para ayudarte a administrar el **ciclo de vida** de tus datos de forma **eficiente y económica**.

| Nivel de acceso | Frecuencia de acceso       | Tiempo recomendado de retención | Coste de almacenamiento | Coste de acceso | Ejemplos                                |
|------------------|-----------------------------|-----------------------------------|---------------------------|------------------|------------------------------------------|
| **Hot (Activo)**   | Alta                         | Cualquier duración                 | 🟡 Medio-alto             | 🟢 Bajo           | Imágenes de sitios web, archivos de uso frecuente. |
| **Cool (Frío)**    | Baja (datos inactivos pero accesibles) | ≥ 30 días                     | 🟢 Bajo                   | 🟡 Medio          | Facturas de clientes, registros recientes. |
| **Archive (Archivo)** | Muy baja o nula               | ≥ 180 días                        | 🟢🟢 Muy bajo              | 🔴 Alto (rehidratación) | Copias de seguridad, históricos, datos legales. |

---

## 🛠️ Consideraciones Técnicas

- 🔁 **Cambiar de nivel de acceso** se puede hacer **a nivel de blob** (individual) en cualquier momento, incluso después de subir los datos.
- 🧾 **Hot y Cool** también se pueden definir **a nivel de cuenta de almacenamiento**.
- 📦 **Archive** no puede usarse a nivel de cuenta, solo a nivel de blob.
- 🧩 Azure ofrece políticas de **ciclo de vida automático** para mover blobs entre niveles según reglas que tú definas (por ejemplo, mover a “cool” tras 30 días sin acceso).

---

## 🔁 ¿Cómo se decide el nivel de acceso?

**Criterios de decisión clave:**

- ¿Con qué frecuencia se accede al archivo?
- ¿Cuánto tiempo necesitas retenerlo?
- ¿Puedes aceptar una latencia más alta para ahorrar costos?

📌 Por ejemplo:
> Si tienes datos que serán consultados activamente durante la primera semana, pero luego raramente, podrías iniciar en **Hot** y luego pasar a **Cool** automáticamente.

---

## 🧠 Aplicación práctica para Tailwind Traders

| Escenario                                                   | Nivel sugerido     |
|-------------------------------------------------------------|---------------------|
| Imágenes del catálogo de productos en la web                | **Hot**             |
| Registros de transacciones que deben conservarse por ley    | **Archive**         |
| Informes financieros mensuales consultados ocasionalmente   | **Cool**            |
| Videos de formación interna vistos esporádicamente          | **Cool o Archive**  |

