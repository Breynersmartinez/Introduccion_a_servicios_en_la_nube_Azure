# ⚡ Computación sin Servidor (Serverless) en Azure

## 📌 Definición Clave
> "Sin servidor no significa *sin servidores*, sino **sin gestión de servidores** por parte del desarrollador."

## 🔍 ¿Cómo Funciona?
- **Modelo basado en eventos**: Ejecución por triggers (HTTP, colas, BD, etc.)
- **Escalado automático**: De 0 a miles de instancias en segundos
- **Pago por uso**: Solo se cobra el tiempo de ejecución real (por milisegundo)

## 🆚 Comparativa: PaaS vs Serverless
| Característica       | PaaS                  | Serverless             |
|----------------------|-----------------------|------------------------|
| **Escalado**         | Manual/Auto           | Automático instantáneo |
| **Coste**            | Por recurso asignado  | Por ejecución real     |
| **Tiempo de inicio** | Minutos-segundos      | Milisegundos           |
| **Estado**           | Mantiene estado       | Sin estado (stateless) |
| **Ejemplo Azure**    | Azure App Service     | Azure Functions        |

## 💡 Beneficios para Tailwind Traders
1. **Productividad**:
   - Equipos enfocados en código (no en infraestructura)
   - Implementaciones más rápidas (ej: procesar pedidos en e-commerce)

2. **Optimización de costos**:
   - Cero costo cuando no hay tráfico
   - Ideal para cargas intermitentes (ej: procesar imágenes al subirlas)

3. **Escalabilidad nativa**:
   - Picos de tráfico manejados automáticamente (ej: Black Friday)

## 🛠️ Servicios Serverless en Azure
- **Azure Functions**: Ejecución de código basada en eventos
  ```csharp
  // Ejemplo: Función que procesa uploads a Blob Storage
  public static void Run(
      [BlobTrigger("uploads/{name}")] Stream myBlob, 
      string name, 
      ILogger log)
  {
      log.LogInformation($"Nuevo archivo: {name}");
      // Lógica de procesamiento...
  }
