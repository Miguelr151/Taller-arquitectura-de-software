# ADR-002: Adopción de Spring Data JPA como Estrategia de Persistencia

## 📌 Contexto

En la arquitectura original del sistema Espagueti de Encuestas, el acceso a datos se realizaba mediante consultas SQL construidas manualmente y concatenadas directamente dentro del controlador.

Esta práctica generaba múltiples problemas estructurales y de seguridad:

- Alto riesgo de SQL Injection.
- Violación del principio de responsabilidad única (SRP).
- Duplicación de lógica de acceso a datos.
- Bajo nivel de abstracción frente al modelo de dominio.
- Dificultad para pruebas unitarias y mantenimiento evolutivo.

Además, la lógica de persistencia estaba acoplada directamente a la capa de presentación, impidiendo una separación clara entre dominio y acceso a datos.

Se hizo necesario adoptar una estrategia de persistencia más robusta y alineada con el ecosistema Spring.

---

## ✅ Decisión

Se adopta **Spring Data JPA** como capa de persistencia oficial para los microservicios propuestos (survey-service y voting-service), utilizando el patrón Repository y delegando la gestión de entidades al proveedor JPA configurado.

La implementación incluye:

- Definición de entidades anotadas con `@Entity`.
- Creación de interfaces que extienden `JpaRepository`.
- Uso de consultas derivadas por convención.
- Integración con el contenedor de inversión de control de Spring.

Esta decisión desacopla la lógica de negocio del acceso a datos y estandariza la persistencia bajo un enfoque ORM.

---

## 📊 Consecuencias

### 🔹 Positivas

- Mitigación de vulnerabilidades frente a SQL Injection.
- Reducción significativa de código repetitivo.
- Mayor coherencia con Spring Boot.
- Mejora en la testabilidad mediante inyección de dependencias.
- Abstracción del modelo relacional hacia objetos.
- Facilita migraciones futuras de base de datos.
- Soporte para paginación y consultas dinámicas.

### 🔹 Negativas

- Curva de aprendizaje asociada al ORM.
- Posible sobrecarga en consultas altamente específicas.
- Dependencia del proveedor JPA.
- Necesidad de comprender el ciclo de vida de las entidades.

---

## 🔄 Alternativas Consideradas

### 1️⃣ JdbcTemplate

**Razón de descarte:**

- Requiere definición manual de consultas.
- Mayor exposición a errores humanos.
- No ofrece un modelo de dominio explícito.
- Mayor esfuerzo de mantenimiento.

### 2️⃣ MyBatis

**Razón de descarte:**

- No es estándar dentro del ecosistema actual del proyecto.
- Introduce dependencia adicional.
- Aumenta complejidad sin aportar beneficios significativos frente a JPA.
- El rediseño busca alinearse con prácticas predominantes en Spring Boot.

---

## 🎯 Justificación Arquitectónica

La adopción de Spring Data JPA responde a:

- Separación de responsabilidades
- Reducción de acoplamiento
- Estandarización tecnológica
- Seguridad por diseño
- Escalabilidad estructural

Esta decisión prepara el sistema para evolucionar hacia una arquitectura profesional y sostenible.