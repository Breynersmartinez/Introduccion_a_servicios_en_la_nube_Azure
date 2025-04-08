

---

# 📘 Estudio de Caso: Estructura Organizativa de Recursos en Azure

Como parte de la investigación para los operadores de **Tailwind**, es fundamental conocer la **estructura organizativa de los recursos en Azure**. Esta estructura se compone de **cuatro niveles jerárquicos**, de arriba hacia abajo:

1. Grupos de administración  
2. Suscripciones  
3. Grupos de recursos  
4. Recursos  

A continuación, se describe cada nivel desde la base hacia la cima:

---

## 🔹 Recursos

Los **recursos** son instancias de servicios que se crean en Azure. Algunos ejemplos incluyen:

- Máquinas virtuales (VM)
- Almacenamiento
- Bases de datos (por ejemplo, bases de datos SQL)

---

## 🔸 Grupos de recursos

Los **grupos de recursos** son contenedores lógicos que permiten organizar y administrar recursos relacionados. Dentro de un grupo de recursos se pueden implementar servicios como:

- Aplicaciones web
- Bases de datos
- Cuentas de almacenamiento

Estos grupos facilitan el manejo conjunto de los recursos.

---

## 🟠 Suscripciones

Una **suscripción** agrupa tanto a las cuentas de usuario como a los recursos que estas han creado. Las suscripciones son útiles para:

- Establecer **límites** o **cuotas** sobre los recursos disponibles
- Gestionar **costos**
- Organizar recursos por **usuarios**, **equipos** o **proyectos**

---

## 🟣 Grupos de administración

Los **grupos de administración** permiten organizar varias suscripciones y aplicar configuraciones a gran escala. Estos grupos son útiles para:

- Gestionar el **acceso**
- Aplicar **políticas**
- Asegurar el **cumplimiento** normativo

> Todas las suscripciones dentro de un grupo de administración **heredan automáticamente** las condiciones establecidas en dicho grupo.

---

## 🧠 Nota Final

Cada uno de estos cuatro niveles será examinado en detalle durante el desarrollo del curso. Comprender esta jerarquía es clave para una administración efectiva y escalable de los recursos en Azure.

