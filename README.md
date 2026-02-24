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

🧹 2.1 Refactorización del Backend

Se implementaron mejoras estructurales orientadas a:

Eliminación de credenciales embebidas en el código.

Sustitución de consultas SQL manuales por repositorios JPA.

Creación de clases DTO con validaciones declarativas.

Implementación de manejo global de excepciones.

Separación clara entre lógica de negocio y acceso a datos.

Estas acciones reducen riesgos de seguridad, mejoran la legibilidad del código y facilitan la escalabilidad futura.

🌐 2.2 Mejora del Frontend (Angular)

En el cliente Angular se identificaron prácticas que afectaban mantenibilidad y calidad, tales como:

Uso directo de HttpClient con URLs hardcodeadas.

Manipulación directa del DOM mediante document.getElementById.

Uso manual de setInterval en lugar de soluciones reactivas.

Como solución se propuso:

Creación de una capa de servicios centralizada.

Uso de environments para configuración por ambiente.

Implementación de programación reactiva con RxJS.

Uso de data binding declarativo en lugar de manipulación directa del DOM.

Estas mejoras fortalecen la coherencia arquitectónica entre frontend y backend.

🔍 3. Impacto Técnico del Rediseño

El paso de una arquitectura monolítica con acoplamiento elevado a una arquitectura basada en microservicios representa una evolución significativa en términos de:

Escalabilidad

Mantenibilidad

Seguridad

Claridad estructural

Preparación para despliegue en entornos modernos (CI/CD)

Además, la incorporación de decisiones arquitectónicas documentadas mediante ADR permite justificar técnicamente cada cambio, fortaleciendo el enfoque profesional del proyecto.

🎯 4. Finalidad Académica y Proyección

El desarrollo de las fases 3 y 4 consolida el proceso formativo al integrar:

Análisis crítico del software.

Aplicación práctica de patrones.

Documentación formal de decisiones arquitectónicas.

Propuesta de rediseño alineada con estándares empresariales.

Más allá de la refactorización técnica, el proyecto permitió comprender cómo las decisiones arquitectónicas influyen directamente en la calidad, sostenibilidad y evolución de un sistema de software.

Este trabajo no solo representa una mejora técnica del sistema analizado, sino también un ejercicio integral de pensamiento arquitectónico aplicado a un contexto real.