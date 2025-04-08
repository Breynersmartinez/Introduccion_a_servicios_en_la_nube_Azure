

## 🌍 Regiones, Zonas de Disponibilidad y Pares de Regiones

### 📌 ¿Qué es una Región?

Una **región de Azure** es una ubicación geográfica que contiene al menos uno (o varios) centros de datos. Cada vez que creas un recurso en Azure (como una base de datos o máquina virtual), este se implementa en una región específica del mundo.

- Azure **no expone directamente** los centros de datos físicos, sino que los organiza en regiones.
- Ejemplos de regiones: `West US`, `Canada Central`, `West Europe`, `East Australia`, `Japan West`.
- Algunas regiones son **especializadas**, como las del gobierno de EE. UU. o China, que tienen restricciones legales y de acceso específicas.

> 🗺️ Azure tiene **más regiones globales** que cualquier otro proveedor de nube, lo que permite acercar las aplicaciones a los usuarios y cumplir requisitos de residencia de datos.

---

### 🏛️ Geografías

Una **geografía** de Azure es un área del mundo que agrupa varias regiones para garantizar el cumplimiento de requisitos legales y de residencia de datos (como "EE. UU.", "Europa", "Asia").

---

### 🧱 ¿Qué son las Zonas de Disponibilidad?

Una **zona de disponibilidad** es un conjunto de uno o más centros de datos independientes **dentro de una misma región**, con alimentación, refrigeración y red propios.

- Sirven como **límite de aislamiento** ante fallos.
- Están conectadas entre sí mediante **fibra óptica privada de alta velocidad**.
- **No todas las regiones** cuentan con zonas de disponibilidad.

#### 🔹 Beneficios:

- Alta disponibilidad y tolerancia a fallos.
- Puedes replicar recursos críticos entre zonas.
- Las zonas permiten mantener la operación incluso si una zona falla.

#### 📦 Tipos de servicios según disponibilidad:

1. **Servicios zonales**: Se asignan a una zona específica (VM, discos administrados, IPs).
2. **Servicios con redundancia zonal**: Se replican automáticamente entre zonas (Almacenamiento ZRS, SQL Database).

> ⚠️ Usar varias zonas puede generar **costos adicionales por replicación y transferencia**.

---

### 🔁 ¿Qué son los Pares de Regiones?

Un **par de regiones** es un conjunto de dos regiones dentro de una misma geografía, separadas por al menos **300 millas (480 km)**, diseñadas para aumentar la redundancia ante desastres a gran escala.

- Permiten replicar recursos entre regiones para mayor disponibilidad.
- Ejemplo: `West US` está emparejada con `East US`.

#### 🛡️ Ventajas clave:

- Actualizaciones planificadas se hacen en **una región a la vez**, reduciendo interrupciones.
- En caso de desastre, se prioriza el restablecimiento de **al menos una región del par**.
- **Algunos servicios**, como el almacenamiento geo-redundante, usan automáticamente estos pares.

> 📌 Salvo en casos especiales (como Brasil SCIF), los datos siempre **permanecen dentro de la misma geografía** que su región emparejada, cumpliendo requisitos legales y fiscales.

