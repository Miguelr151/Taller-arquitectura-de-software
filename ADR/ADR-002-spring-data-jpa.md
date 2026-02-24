ADR-002: Adopción de Spring Data JPA como Estrategia de Persistencia
📌 Contexto

En la arquitectura original del sistema Espagueti de Encuestas, el acceso a datos se realizaba mediante consultas SQL construidas manualmente y concatenadas directamente dentro del controlador. Esta práctica generaba múltiples problemas estructurales y de seguridad:

Alto riesgo de SQL Injection.

Violación del principio de responsabilidad única (SRP).

Duplicación de lógica de acceso a datos.

Bajo nivel de abstracción frente al modelo de dominio.

Dificultad para pruebas unitarias y mantenimiento evolutivo.

Adicionalmente, la lógica de persistencia estaba acoplada directamente a la capa de presentación, lo que impedía una separación clara entre dominio y acceso a datos.

Frente a este escenario, se hizo necesario adoptar una estrategia de persistencia más robusta, alineada con estándares modernos del ecosistema Spring.

✅ Decisión

Se adopta Spring Data JPA como capa de persistencia oficial para los microservicios propuestos (survey-service y voting-service), utilizando el patrón Repository y delegando la gestión de entidades al proveedor JPA configurado.

La implementación incluye:

Definición de entidades anotadas con @Entity.

Creación de interfaces que extienden JpaRepository.

Uso de consultas derivadas por convención.

Integración con el contenedor de inversión de control de Spring.

Esta decisión permite desacoplar completamente la lógica de negocio del acceso a datos y estandarizar la persistencia bajo un enfoque ORM (Object-Relational Mapping).

📊 Consecuencias
🔹 Positivas

Mitigación de vulnerabilidades frente a SQL Injection mediante prepared statements gestionados internamente.

Reducción significativa de código repetitivo (boilerplate).

Mayor coherencia con el ecosistema Spring Boot.

Mejora en la testabilidad mediante inyección de dependencias.

Abstracción del modelo relacional hacia un modelo orientado a objetos.

Facilita migraciones futuras de base de datos.

Soporte nativo para paginación, ordenamiento y consultas dinámicas.

🔹 Negativas

Curva de aprendizaje inicial asociada al uso de JPA y ORM.

Posible sobrecarga de rendimiento en consultas altamente específicas.

Dependencia del proveedor JPA configurado.

Necesidad de comprender correctamente el ciclo de vida de las entidades.

🔄 Alternativas Consideradas
1️⃣ JdbcTemplate

Se evaluó el uso de JdbcTemplate como alternativa más ligera.

Razón de descarte:

Continúa requiriendo definición manual de consultas.

Mayor exposición a errores humanos.

No ofrece un modelo de dominio explícito.

Mayor esfuerzo de mantenimiento a largo plazo.

2️⃣ MyBatis

Se consideró MyBatis como solución intermedia entre SQL manual y ORM completo.

Razón de descarte:

No es la solución estándar dentro del ecosistema actual del proyecto.

Introduce una dependencia adicional.

Aumenta complejidad sin aportar beneficios significativos frente a JPA para este caso académico.

El objetivo del rediseño es alinearse con prácticas predominantes en Spring Boot.

🎯 Justificación Arquitectónica

La adopción de Spring Data JPA responde a los siguientes principios arquitectónicos:

Separación de responsabilidades

Reducción de acoplamiento

Estandarización tecnológica

Seguridad por diseño

Escalabilidad estructural

Esta decisión no solo resuelve problemas técnicos detectados en la fase de análisis, sino que prepara el sistema para evolucionar hacia una arquitectura más profesional y sostenible.