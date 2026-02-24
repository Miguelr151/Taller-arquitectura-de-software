# ADR-001: Descomposición del Monolito en Arquitectura de Microservicios

## 📌 Contexto

El sistema “Espagueti de Encuestas” fue originalmente desarrollado bajo una arquitectura monolítica tradicional, donde un único módulo concentraba:

- Lógica de presentación (controllers)
- Lógica de negocio
- Acceso a datos
- Validaciones
- Configuración de infraestructura

Esta concentración de responsabilidades generó múltiples problemas estructurales:

- Violación del principio de responsabilidad única (SRP).
- Alto acoplamiento entre componentes.
- Dificultad para escalar funcionalidades específicas.
- Riesgo elevado ante cambios evolutivos.
- Imposibilidad de despliegue independiente por dominio funcional.
- Baja capacidad de adaptación a entornos distribuidos modernos.

Aunque el sistema cumplía funcionalmente su propósito, su diseño interno comprometía su mantenibilidad y sostenibilidad a mediano y largo plazo.

Ante este escenario, se evaluó la necesidad de adoptar una arquitectura más modular y orientada a dominios.

---

## ✅ Decisión

Se decidió descomponer el monolito en una arquitectura basada en microservicios, estructurada por bounded contexts claramente definidos:

- **survey-service** → Responsable exclusivamente de la gestión de encuestas.
- **voting-service** → Responsable de la gestión de votos.
- **API Gateway** → Punto único de entrada para clientes externos, encargado de enrutamiento y centralización de acceso.

Cada microservicio mantiene:

- Su propia capa de presentación.
- Su lógica de negocio independiente.
- Su capa de persistencia desacoplada.

La comunicación entre servicios se establece mediante APIs REST bien definidas.

Esta decisión busca alinear la arquitectura con principios de:

- Separación de dominios
- Bajo acoplamiento
- Alta cohesión
- Escalabilidad independiente

---

## 📊 Consecuencias

### 🔹 Positivas

- Escalabilidad independiente por servicio.
- Despliegue desacoplado sin afectar otros dominios.
- Reducción del impacto de fallos (aislamiento parcial).
- Mejor organización del código por contexto de negocio.
- Facilita integración futura con infraestructura CI/CD.
- Mayor alineación con arquitecturas empresariales modernas.

### 🔹 Negativas

- Incremento en la complejidad operativa.
- Necesidad de gestionar comunicación entre servicios.
- Mayor esfuerzo inicial de configuración.
- Posibles desafíos de consistencia de datos.
- Requiere monitoreo y observabilidad distribuida.

---

## 🔄 Alternativas Consideradas

### 1️⃣ Mantener Monolito Modular

Se evaluó mantener el sistema como monolito reorganizado internamente por módulos.

**Razón de descarte:**

- No permite escalabilidad independiente.
- Continúa limitando despliegues desacoplados.
- No resuelve completamente la concentración de responsabilidades.

### 2️⃣ Arquitectura Hexagonal dentro del Monolito

Se consideró aplicar arquitectura hexagonal (Ports & Adapters) sin dividir el sistema.

**Razón de descarte:**

- Mantiene el despliegue como una única unidad.
- No cumple el objetivo de independencia operacional.
- No permite escalado selectivo por dominio funcional.

---

## 🎯 Justificación Arquitectónica

La decisión de migrar hacia microservicios prioriza:

- Escalabilidad horizontal
- Independencia de dominios
- Mantenibilidad a largo plazo
- Preparación para entornos distribuidos
- Adaptabilidad ante crecimiento funcional

Aunque introduce mayor complejidad operativa, los beneficios estructurales y estratégicos superan los costos iniciales.