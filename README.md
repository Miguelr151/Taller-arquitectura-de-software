Taller Arquitectura de Software – Rediseño y Refactorización

Corporación Universitaria del Huila – CORHUILA
Asignatura: Arquitectura de Software
Docente: Luis Ángel Vargas Narváez

Integrantes:
Angie Valentina Flórez Vargas
Sebastián Puentes Gonzales
Sergio Alejandro Muñoz Cabrera
Miguel Ángel Rivera Lozano

Fecha: 17 de febrero de 2026
Lugar: Neiva, Huila

📚 1. Fase 3 – Propuesta de Rediseño Arquitectónico

En esta fase se desarrolló una propuesta formal de rediseño arquitectónico para el sistema Espagueti de Encuestas, tomando como base los hallazgos identificados en el análisis estructural previo. El objetivo principal fue transformar una arquitectura monolítica con múltiples anti-patrones en una arquitectura más modular, escalable y alineada con principios modernos de diseño de software.

El rediseño parte de la identificación de responsabilidades mal distribuidas, acoplamientos excesivos y problemas de seguridad derivados del manejo manual de SQL y credenciales embebidas en el código fuente. A partir de este diagnóstico, se estructuró una nueva arquitectura basada en microservicios, separación por capas y adopción de patrones consolidados del ecosistema Spring Boot.

📐 1.1 Principales Decisiones Arquitectónicas

Se propuso la descomposición del sistema en los siguientes componentes:

API Gateway como punto único de entrada.

survey-service para la gestión de encuestas.

voting-service para la gestión de votos.

Separación clara entre capas: Controller → Service → Repository.

Uso de Spring Data JPA como estrategia estándar de persistencia.

Esta reorganización permite reducir el acoplamiento, mejorar la mantenibilidad y facilitar despliegues independientes.

🧩 1.2 Aplicación de Patrones de Diseño

En esta fase se documentaron y justificaron patrones de diseño aplicados como parte del rediseño:

Repository Pattern (Spring Data JPA)
Sustituye SQL concatenado manual, reduciendo riesgo de inyección SQL.

Arquitectura en Capas (Layered Architecture)
Separa responsabilidades técnicas y de negocio.

DTO Pattern + Bean Validation
Define contratos tipados y elimina uso de estructuras genéricas como Map.

Global Exception Handler (@RestControllerAdvice)
Centraliza el manejo de errores y estandariza respuestas HTTP.

Externalized Configuration
Elimina credenciales hardcodeadas y permite configuración por ambiente.

Estas decisiones fortalecen la calidad estructural del sistema y alinean el proyecto con estándares profesionales.

🛠 2. Fase 4 – Refactorización y Mejora de Calidad

La fase 4 se enfocó en la aplicación práctica de mejoras identificadas, aplicando principios de Clean Code y buenas prácticas de ingeniería de software.

🧹 2.1 Refactorización del BackendPerfecto 👌 ahora sí vamos a subirle el nivel.
Te lo voy a reescribir con un tono **más profesional, más técnico, más estructurado y con mayor profundidad arquitectónica**, para que no se vea “simple”, sino como un documento serio de arquitectura.

Puedes copiarlo y pegarlo directamente en tu README o en el Word.

---

# Taller Arquitectura de Software – Rediseño y Refactorización Arquitectónica

**Corporación Universitaria del Huila – CORHUILA**
**Asignatura:** Arquitectura de Software
**Docente:** Luis Ángel Vargas Narváez

**Integrantes:**
Angie Valentina Flórez Vargas
Sebastián Puentes Gonzales
Sergio Alejandro Muñoz Cabrera
Miguel Ángel Rivera Lozano

**Fecha:** 17 de febrero de 2026
**Lugar:** Neiva, Huila

---

# 📌 Introducción General

El presente trabajo corresponde a las fases 3 y 4 del proyecto académico desarrollado sobre el sistema **Espagueti de Encuestas**, cuyo propósito fue analizar, rediseñar y refactorizar una solución inicialmente construida bajo un enfoque monolítico con deficiencias estructurales.

A partir del análisis realizado en fases anteriores, se evidenciaron múltiples problemas arquitectónicos tales como acoplamiento excesivo, violaciones al principio de responsabilidad única, exposición a riesgos de seguridad (SQL Injection), credenciales embebidas en el código fuente y ausencia de separación clara entre capas.

En respuesta a estos hallazgos, se planteó un rediseño arquitectónico fundamentado en principios de arquitectura moderna, patrones de diseño consolidados y buenas prácticas de ingeniería de software.

---

# 🏗 Fase 3 – Rediseño Arquitectónico

## 1. Diagnóstico Arquitectónico

El sistema original presentaba características típicas de una arquitectura monolítica con las siguientes problemáticas:

* Concentración de lógica de negocio, acceso a datos y validaciones en un único controlador.
* Uso de consultas SQL concatenadas manualmente.
* Ausencia de contratos tipados para entrada y salida de datos.
* Configuración de base de datos embebida en el código.
* Dependencia directa entre componentes sin una capa de abstracción.

Este escenario generaba un sistema funcional pero frágil, difícil de mantener y con alta probabilidad de degradación ante futuras ampliaciones.

---

## 2. Propuesta de Nueva Arquitectura

Se propuso la migración hacia una arquitectura basada en microservicios, estructurada bajo los siguientes componentes:

* **API Gateway** como punto central de entrada y enrutamiento.
* **survey-service**, responsable exclusivamente de la gestión de encuestas.
* **voting-service**, encargado de la gestión de votos.
* Persistencia desacoplada mediante repositorios JPA.
* Separación formal por capas: Controller → Service → Repository.

Esta propuesta busca:

* Reducir el acoplamiento estructural.
* Permitir escalabilidad independiente por dominio.
* Mejorar la mantenibilidad del sistema.
* Facilitar despliegues desacoplados.
* Preparar el sistema para integración futura con infraestructura CI/CD.

---

## 3. Aplicación de Patrones de Diseño

El rediseño se fundamenta en la adopción explícita de patrones arquitectónicos y de diseño:

### 🔹 Repository Pattern (Spring Data JPA)

Se reemplaza la construcción manual de SQL por repositorios basados en JPA, delegando la gestión de persistencia al framework.
Esto elimina riesgos de inyección SQL y reduce código repetitivo.

### 🔹 Arquitectura en Capas (Layered Architecture)

Se establece una clara separación entre:

* Capa de presentación (Controllers)
* Capa de negocio (Services)
* Capa de acceso a datos (Repositories)

Lo anterior mejora la cohesión interna y reduce dependencias transversales.

### 🔹 DTO Pattern + Bean Validation

Se sustituyen estructuras genéricas por objetos tipados que definen contratos explícitos de entrada y salida, incorporando validaciones declarativas mediante anotaciones.

Esto fortalece la robustez del sistema y mejora la claridad del modelo de datos.

### 🔹 Global Exception Handling

Se centraliza el manejo de excepciones mediante `@RestControllerAdvice`, garantizando respuestas HTTP consistentes y mejorando la observabilidad del sistema.

### 🔹 Externalized Configuration

Las credenciales y configuraciones sensibles son externalizadas mediante variables de entorno y archivos de configuración, alineándose con prácticas DevOps modernas.

---

# 🛠 Fase 4 – Refactorización y Mejora de Calidad

La fase 4 consistió en la aplicación concreta de principios de Clean Code y refactorización estructural tanto en backend como en frontend.

---

## 🔧 4.1 Refactorización del Backend (Spring Boot)

Las mejoras implementadas incluyen:

* Eliminación de credenciales hardcodeadas.
* Migración de SQL manual a repositorios JPA.
* Implementación de DTOs con validación declarativa.
* Separación formal entre lógica de negocio y acceso a datos.
* Manejo global de excepciones.
* Preparación para despliegue modular.

Estas acciones mejoran:

* Seguridad del sistema.
* Legibilidad y claridad del código.
* Testabilidad de componentes.
* Evolución futura del proyecto.

---

## 🌐 4.2 Mejora del Frontend (Angular)

En el cliente Angular se identificaron prácticas que comprometían la mantenibilidad:

* Uso directo de HttpClient sin capa de abstracción.
* URLs hardcodeadas.
* Manipulación imperativa del DOM.
* Uso manual de temporizadores con `setInterval`.

Como parte del rediseño, se propuso:

* Creación de servicios Angular centralizados.
* Uso de `environment.ts` para configuración por entorno.
* Implementación de programación reactiva con RxJS.
* Sustitución de manipulación directa del DOM por data binding declarativo.

Estas mejoras alinean el frontend con principios de arquitectura reactiva y reducen riesgos de memory leaks y dependencias implícitas.

---

# 📊 Impacto Arquitectónico del Rediseño

El paso de una arquitectura monolítica a una arquitectura modular basada en microservicios representa una mejora significativa en términos de:

* Escalabilidad horizontal
* Desacoplamiento estructural
* Robustez ante cambios
* Seguridad de datos
* Preparación para entornos empresariales

Adicionalmente, la documentación formal mediante ADR (Architecture Decision Records) permite justificar técnicamente cada decisión adoptada, aportando trazabilidad y madurez al proceso de diseño.

---

# 🎓 Proyección Académica y Profesional

Este proyecto trasciende la simple corrección de errores técnicos. Representa un ejercicio integral de pensamiento arquitectónico aplicado a un sistema real, donde se integran:

* Análisis crítico
* Diseño basado en patrones
* Evaluación de riesgos
* Documentación formal de decisiones
* Refactorización estratégica

El resultado no solo es un sistema técnicamente mejorado, sino también una consolidación de competencias profesionales en arquitectura de software, orientadas a contextos empresariales reales.