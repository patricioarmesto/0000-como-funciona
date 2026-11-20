# ¿Cómo funciona Matching de Marketplace?

> Ejercicio 0562 de 1024 del curso ¿Cómo funciona...?
> Nivel: **Medio** | Track: **System Design / Patrones** | Fecha: **06 Oct 2037 — 13:00 ART** | Repo: `como-funciona/0562-patron-169-matching-de-marketplace`

## Aprende construyendo

En este ejercicio no leés sobre Matching de Marketplace. Lo construís en chiquito, corriendo en `localhost:3000`, y lo rompés a propósito para entender por qué está diseñado así.

Si terminás este ejercicio, entendés cómo funciona Matching de Marketplace por dentro, no solo cómo se usa.

## Qué vas a construir

Un prototipo funcional de Matching de Marketplace, con backend + frontend + infra, que puedas correr con un solo comando:

```bash
docker compose up
# Abrir http://localhost:3000
```

El prototipo incluye:

- **Frontend** en TypeScript + React + Vite + Tailwind, con la pantalla principal del producto
- **Backend** en Go, con la API y el flujo completo
- **Botón para romperlo** — simulación de tráfico, doble click, fallo o conflicto, para ver el caso difícil
- **Panel en vivo** — estado, métricas y resultado, para ver qué pasó

El caso que lo vende: el ejercicio está diseñado para que el caso difícil ocurra en tu máquina, no en teoría.

## Conceptos que ejercitás

- Diseño de API
- Flujo completo
- Decisiones de datos
- Escala
- Alcance

Cada concepto tiene un comentario didáctico en el código que explica **por qué** está hecho así, no solo **qué** hace.

## Qué resuelve Matching de Marketplace

Matching de Marketplace resuelve un problema de escala, de concurrencia o de datos que no se ve en un tutorial simple.

En este ejercicio, ese problema está aislado: un solo flujo, una sola decisión difícil, un prototipo que lo muestra.

## Flujo

1. Usuario hace la acción principal en el frontend
2. Frontend llama a la API en Go
3. API valida, aplica la decisión clave del ejercicio (idempotencia, cache, batch, dedup, etc.)
4. Se guarda en la base correcta para ese caso
5. Se publica evento si el track lo usa
6. Frontend muestra el resultado en vivo

> Flujo detallado, arquitectura y prompt completo para Claude en el repo `0562-patron-169-matching-de-marketplace`.
> Este archivo es la definición del ejercicio en formato Portfolio. El código completo vive en su repo.

## Arquitectura

```
Frontend React
   |
API (Go)
   |
Postgres + Redis + Kafka + ClickHouse / Qdrant según track
```

Ver `README.md` del repo `0562-patron-169-matching-de-marketplace` para el diagrama en texto completo de este ejercicio.

## Stack

Go + React + Postgres + Redis + Kafka + ClickHouse + Docker Compose

Solo tecnologías que están en `docker-compose.yml`. Sin tecnologías de más.

## Decisiones clave

- **Una decisión central** — la que hace que este ejercicio valga la pena
- **Fuente de verdad** — dónde vive el dato que no se puede perder
- **Cache vs base** — qué va en Redis y qué va en Postgres / ClickHouse
- **Qué queda fuera** — a propósito, para mantener el ejercicio legible

## Alcance y decisiones de diseño

Alcance: Ejercicio de System Design. Decisiones intencionales. Los patrones avanzados de producción están fuera de alcance a propósito para mantener el ejercicio legible. No son omisiones por desconocimiento.

## Qué NO implementamos

- Integración real con el producto original
- Transactional Outbox, DLT, Exactly-Once, monitoreo de producción, salvo que el ejercicio sea específicamente sobre ese patrón
- Escalado real multi-región

Si el ejercicio es sobre uno de esos patrones, ahí sí se implementa y se explica.

## Cómo probar

1. Correr `docker compose up` y abrir `localhost:3000`
2. Hacer la acción principal una vez, ver que funciona
3. Hacer la acción difícil: doble click, 100 requests en paralelo, o simular fallo, y ver que el sistema se comporta como se explica en el README
4. Revisar los comentarios didácticos en el código para entender el por qué

## ADRs

En el repo `0562-patron-169-matching-de-marketplace`:

- `docs/adr/0001-decision-principal.md`
- `docs/adr/0002-decision-de-datos.md`
- `docs/adr/0003-decision-de-flujo.md`
- `docs/adr/0004-que-queda-fuera.md`

Formato estándar de ADR en todos los ejercicios.

## Repo

- **Repo:** `como-funciona/0562-patron-169-matching-de-marketplace`
- **Índice general:** `../README.md`
- **Estado:** Por hacer
