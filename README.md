# Taller Arquitectura de Software  
## Rediseño y Refactorización Arquitectónica  

**Corporación Universitaria del Huila – CORHUILA**  
**Asignatura:** Arquitectura de Software  
**Docente:** Luis Ángel Vargas Narváez  

### 👥 Integrantes
- Angie Valentina Flórez Vargas  
- Sebastián Puentes Gonzales  
- Sergio Alejandro Muñoz Cabrera  
- Miguel Ángel Rivera Lozano  

**Fecha:** 17 de febrero de 2026  
**Lugar:** Neiva, Huila  

---

# 📌 Introducción

El presente proyecto corresponde a las Fases 3 y 4 del proceso de análisis, rediseño y refactorización del sistema **“Espagueti de Encuestas”**, desarrollado como caso de estudio académico para la asignatura Arquitectura de Software.

En fases anteriores se identificaron múltiples deficiencias estructurales propias de una arquitectura monolítica con alto acoplamiento y baja separación de responsabilidades. A partir de dichos hallazgos, se planteó una propuesta formal de rediseño arquitectónico y la aplicación práctica de mejoras orientadas a elevar la calidad técnica del sistema.

Este documento describe las decisiones arquitectónicas adoptadas, los patrones implementados y el impacto técnico del proceso de refactorización.

---

# 🏗 Fase 3 – Rediseño Arquitectónico

## 🔍 Diagnóstico Inicial

El sistema original presentaba las siguientes problemáticas:

- Concentración de lógica de negocio y acceso a datos en un único controlador.
- Uso de SQL concatenado manualmente.
- Credenciales de base de datos hardcodeadas.
- Uso de estructuras genéricas (`Map`) en lugar de contratos tipados.
- Ausencia de separación clara entre capas.
- Bajo nivel de escalabilidad.

Estas condiciones comprometían la mantenibilidad, seguridad y evolución futura del sistema.

---

## 🧩 Propuesta de Nueva Arquitectura

Se planteó la descomposición del sistema en una arquitectura basada en microservicios, estructurada en:

- **API Gateway** → Punto único de entrada.
- **survey-service** → Gestión de encuestas.
- **voting-service** → Gestión de votos.
- Persistencia desacoplada mediante Spring Data JPA.
- Separación por capas: Controller → Service → Repository.

### 🎯 Objetivos del Rediseño

- Reducir el acoplamiento estructural.
- Permitir escalabilidad independiente.
- Mejorar mantenibilidad.
- Fortalecer seguridad.
- Preparar el sistema para CI/CD.

---

## 🏛 Patrones Arquitectónicos Aplicados

### 🔹 Repository Pattern (Spring Data JPA)
Elimina SQL manual y reduce riesgo de inyección SQL.

### 🔹 Arquitectura en Capas
Separa responsabilidades entre presentación, negocio y persistencia.

### 🔹 DTO Pattern + Bean Validation
Define contratos tipados y validaciones declarativas.

### 🔹 Global Exception Handler
Centraliza manejo de errores y estandariza respuestas HTTP.

### 🔹 Externalized Configuration
Elimina credenciales embebidas en código y permite configuración por entorno.

---

# 🛠 Fase 4 – Refactorización y Mejora de Calidad

## 🔧 Refactorización Backend (Spring Boot)

Mejoras implementadas:

- Eliminación de credenciales hardcodeadas.
- Migración de SQL manual a repositorios JPA.
- Implementación de DTOs con validación declarativa.
- Separación formal entre capas.
- Manejo global de excepciones.
- Preparación para arquitectura modular.

### ✅ Beneficios

- Mayor seguridad.
- Código más limpio.
- Mejor testabilidad.
- Escalabilidad estructural.
- Reducción de deuda técnica.

---

## 🌐 Mejora del Frontend (Angular)

Problemas identificados:

- URLs hardcodeadas.
- Uso directo de HttpClient sin capa de abstracción.
- Manipulación directa del DOM.
- Uso manual de `setInterval`.

### 🔄 Soluciones Propuestas

- Creación de servicios Angular centralizados.
- Uso de `environment.ts`.
- Implementación de programación reactiva con RxJS.
- Uso de data binding declarativo.

---

# 📊 Impacto Arquitectónico

La transición de una arquitectura monolítica a una arquitectura modular basada en microservicios genera mejoras en:

- Escalabilidad
- Mantenibilidad
- Seguridad
- Organización estructural
- Preparación para entornos empresariales

Adicionalmente, la documentación mediante ADR permite justificar técnicamente cada decisión arquitectónica adoptada.

---

# 📚 Architecture Decision Records (ADR)

## ADR-001 – Descomposición del Monolito en Microservicios

Se decidió dividir el sistema en bounded contexts independientes para reducir acoplamiento y permitir despliegue desacoplado.

## ADR-002 – Uso de Spring Data JPA

Se adoptó JPA como estrategia estándar de persistencia para eliminar SQL manual y mejorar seguridad y mantenibilidad.

---

# 🎓 Conclusión

Este proyecto permitió aplicar principios de arquitectura moderna en un contexto académico real, integrando análisis crítico, rediseño estructural y refactorización práctica.

El resultado es un sistema más robusto, modular y alineado con estándares profesionales de ingeniería de software.

Más allá de la mejora técnica, el proceso fortaleció competencias clave en:

- Evaluación arquitectónica
- Aplicación de patrones
- Documentación formal de decisiones
- Pensamiento estructural orientado a calidad

---
