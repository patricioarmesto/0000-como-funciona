# Stack fijo

Todos los ejercicios usan el mismo stack. La decisión permite que una persona que aprendió a correr el ejercicio 0001 pueda correr el 0873 sin leer documentación nueva.

| Componente | Rol | Cuándo se usa |
| --- | --- | --- |
| Go | Servicios y workers | Default para HTTP, workers, tareas periódicas y comandos. |
| React + Vite + Tailwind | Interfaz | Toda UI que necesite mostrar o cargar datos del ejercicio. |
| Postgres | Write model | Datos que requieren transacciones, integridad referencial y consultas estructuradas. |
| Redis | Caché y estado volátil | Lecturas frecuentes, sesiones, rate limiting y colas simples. |
| Kafka | Eventos | Historial durable de cambios, replay y comunicación entre servicios. |
| ClickHouse | Analítica | Agregaciones, reportes y consultas sobre grandes volúmenes de eventos. |
| Qdrant | Vectores | Búsqueda semántica, recomendaciones y RAG. |
| Docker Compose | Entorno local | Levantar y apagar el ejercicio completo con un comando. |

## Por qué Go donde se pueda

Go es el lenguaje por defecto porque resuelve tres necesidades del formato:

- **Arranque predecible.** Un binario compilado arranca rápido y no depende de un runtime que haya que instalar en el host.
- **Concurrencia explícita.** Los problemas de System Design suelen tratar con muchas operaciones simultáneas; en Go eso se modela con goroutines y canales sin framework adicional.
- **Superficie chica.** Hay menos magia detrás de la escena. El código del ejercicio se puede leer de arriba abajo y explicar en voz alta.

«Donde se pueda» es una condición real, no un eslogan. Si el ejercicio requiere entrenar un modelo, procesar lenguaje natural o usar una librería de IA que solo existe en Python, se usa Python para esa pieza. Lo que no se hace es escribir la API HTTP, los workers de negocio o las migraciones en Python por costumbre.

## Python solo para IA

Python queda reservado para:

- Generación y consulta de embeddings.
- Inferencia con modelos locales o remotos.
- Evaluación de prompts y pipelines de RAG.
- Notebooks de análisis que acompañen al ejercicio.

Incluso en esos casos, el servicio Go sigue siendo el dueño del flujo: expone la API, valida entradas, aplica reglas de negocio y persiste en Postgres. Python es una dependencia del servicio, no un servicio paralelo con su propio modelo de datos.

Alcance y decisiones de diseño: esta restricción existe para que el ejercicio siga siendo comparable entre pares. Si cada repo eligiera lenguaje según preferencia personal, el curso enseñaría herramientas distintas en lugar de decisiones de diseño.

## Cuándo NO usar un componente

El stack fijo no implica usarlo completo. Cada ejercicio incluye solo lo que su problema pide:

| Componente | Señal de que todavía no corresponde |
| --- | --- |
| Redis | No hay lecturas repetidas ni estado volátil que administrar. |
| Kafka | No hay dos consumidores interesados en el mismo cambio. |
| ClickHouse | El volumen y las agregaciones se resuelven en Postgres. |
| Qdrant | No hay búsqueda por similitud ni recuperación semántica. |
| Python | No hay ningún paso de IA en el flujo. |

Agregar un componente sin una señal clara es una decisión de diseño que hay que justificar en un ADR, igual que agregarlo con una señal clara.

## Convenciones comunes

- Puertos predecibles: `3000` para la interfaz, el resto documentado en el README del ejercicio.
- Un `docker-compose.yml` por repo, sin archivos alternativos por entorno.
- Las migraciones de Postgres corren al arrancar el compose.
- Los servicios Go leen configuración desde variables de entorno con valores por defecto razonables.
- Los datos de ejemplo se generan dentro del propio ejercicio; no se depende de servicios externos.

## Decisiones registradas

Las decisiones estructurales están en los ADRs de este repositorio:

- [0001: Un repo por ejercicio](./adr/0001-un-repo-por-ejercicio.md)
- [0002: Ciclo de 4 semanas](./adr/0002-ciclo-4-semanas.md)
- [0003: 1024 ejercicios](./adr/0003-1024-ejercicios.md)
