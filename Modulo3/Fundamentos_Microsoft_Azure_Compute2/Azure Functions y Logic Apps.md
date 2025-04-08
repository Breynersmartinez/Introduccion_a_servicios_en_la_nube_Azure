

### 🆚 **Azure Functions vs Azure Logic Apps**

| Característica                         | **Azure Functions**                                                | **Azure Logic Apps**                                               |
|--------------------------------------|--------------------------------------------------------------------|--------------------------------------------------------------------|
| **Modelo de ejecución**              | Ejecuta **código personalizado**                                    | Ejecuta **flujos de trabajo visuales**                             |
| **Código requerido**                 | Sí, en lenguajes como C#, JavaScript, Python, etc.                 | No necesariamente, se usa un diseñador visual                      |
| **Desencadenadores**                 | REST API, temporizadores, colas, eventos, etc.                     | Eventos, programación, webhooks, servicios externos                |
| **Cobro**                            | Solo cuando se ejecuta la función (por consumo de CPU)             | Por ejecución de acciones y conectores                             |
| **Duración típica de ejecución**     | Rápida (segundos o menos), aunque permite funciones duraderas      | Puede durar más, diseñado para flujos de negocio complejos         |
| **Escenarios ideales**              | Lógica personalizada basada en eventos, procesamiento rápido       | Integraciones empresariales, automatización sin código             |
| **Escalado automático**              | Sí                                                                 | Sí                                                                 |
| **Persistencia de estado**           | No por defecto, pero se puede con "Durable Functions"              | Sí, cada ejecución persiste como una instancia                     |
| **Desarrollo**                       | Con IDE como Visual Studio o VS Code                               | Diseñador visual en Azure Portal o Visual Studio                   |
| **Usuarios ideales**                 | Desarrolladores                                                     | Analistas de negocios o desarrolladores que integran servicios     |
| **Conectores disponibles**           | Personalizables vía código                                          | +200 conectores predefinidos (Office 365, SharePoint, SQL, etc.)  |

---

### 💡 Ejemplo práctico (como el del curso):

**Escenario:** Tailwind Traders quiere automatizar tareas cuando recibe un ticket de soporte.

| Parte del flujo | Azure Logic Apps                                   | Azure Functions                                |
|-----------------|----------------------------------------------------|------------------------------------------------|
| Detectar ticket | Conector a Zendesk en Logic Apps                   | No aplica                                      |
| Analizar mensaje| Llamada a Azure Cognitive Services (integrado)     | Podrías hacerlo con código, pero más complejo  |
| Crear en SharePoint | Conector directo en Logic Apps               | Necesitas SDK o REST API manual                |
| Enviar email     | Conector de correo predefinido                   | Requiere código SMTP o uso de otro servicio    |

Resultado: para automatización empresarial **sin código**, Logic Apps es ideal. Para lógica compleja o personalizada, **Functions** es mejor.

