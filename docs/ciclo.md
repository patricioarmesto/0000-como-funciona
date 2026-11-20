# El ciclo de 4 semanas

El curso avanza en bloques de cuatro semanas. Cada bloque se llama **ciclo** y tiene una estructura fija: tres semanas de ejercicio, una semana de comunidad. Con 1024 ejercicios semanales, el calendario completo contiene 256 ciclos.

La estructura no es decorativa. Está diseñada para que cada ejercicio tenga un momento de cierre antes de pasar al siguiente.

## Semana 1: Inicial

Se presenta la marca y se recorta el problema. El objetivo es entender qué hace el sistema y qué parte del mismo vale la pena reconstruir.

En esta semana se definen:

- Los actores y los flujos principales.
- El modelo de datos mínimo en Postgres.
- El servicio Go que expone el flujo y la interfaz React que lo consume.
- Los comandos para levantar todo con Docker Compose.

Alcance y decisiones de diseño: en Inicial se busca que el sistema funcione de punta a punta. No se agrega caché, colas ni almacenamiento analítico solo porque el stack los incluya. Si una decisión no está justificada por el problema, se deja para otra semana o no se incluye.

El resultado observable es simple: se abre `localhost:3000`, se ejecuta el flujo principal y se entiende qué pasó con los datos.

## Semana 2: Medio

Aparecen los requisitos no funcionales. La pregunta deja de ser «¿funciona?» y pasa a ser «¿qué pasa cuando crece?».

Se trabajan aquí:

- Medición de latencia y volumen con datos representativos.
- Separación entre escritura y lectura.
- Caché en Redis y estrategias de invalidación.
- Eventos en Kafka para desacoplar servicios que antes se llamaban de forma síncrona.
- Particionamiento inicial y límites de tablas en Postgres.

Las decisiones de esta semana son las que más se benefician de un ADR: hay alternativas reales y cada elección tiene un costo. Se registra qué se eligió, qué se descartó y por qué.

## Semana 3: Avanzado

Se lleva el diseño al límite. El objetivo no es agregar componentes, sino entender qué se rompe primero.

Se abren explícitamente:

- Fallas parciales y degradación graciosa.
- Consistencia eventual y estrategias de compensación.
- Volúmenes altos y agregaciones en ClickHouse.
- Búsqueda vectorial en Qdrant cuando el problema la requiere.
- Límites operativos: qué se observa, qué se alerta y qué no se puede recuperar.

Alcance y decisiones de diseño: en Avanzado se documentan los límites con la misma importancia que las soluciones. Un ejercicio que no puede decir dónde se rompe no está terminado.

## Semana 4: Comunidad

No hay marca nueva. La semana se usa para cerrar el ciclo anterior en conjunto.

Qué se hace:

- Comparar los tres ejercicios del ciclo y buscar patrones repetidos.
- Revisar los ADRs escritos y corregir los que quedaron ambiguos.
- Discutir decisiones que se tomaron por intuición y nunca se documentaron.
- Analizar qué partes del stack se usaron de más y cuáles faltaron.
- Ajustar los comentarios didácticos para que expliquen mejor el porqué.

## Por qué existe la semana de Comunidad

Si los ejercicios se encadenaran sin pausa, el curso acumularía deuda didáctica: decisiones sin explicar, ADRs desactualizados y soluciones que funcionan pero nadie puede defender. La semana de Comunidad existe para impedirlo.

Cumple cuatro funciones concretas:

1. **Cierre.** Cada ciclo termina con una revisión, no con un `git push`.
2. **Contraste.** Ver tres problemas distintos seguidos permite reconocer qué es específico de una marca y qué es un patrón de System Design.
3. **Corrección.** Los ADRs se escriben en el momento, pero se entienden mejor una semana después. Ese es el momento de arreglarlos.
4. **Continuidad.** Lo que se aprende en la revisión se aplica al ciclo siguiente. El curso se mejora a sí mismo en lugar de repetirse.

## Estructura resumida

| Semana | Nivel | Pregunta central | Entregable principal |
| --- | --- | --- | --- |
| 1 | Inicial | ¿Qué hace el sistema? | Flujo principal funcionando. |
| 2 | Medio | ¿Qué pasa cuando crece? | Decisiones de escala con ADRs. |
| 3 | Avanzado | ¿Dónde se rompe? | Límites documentados. |
| 4 | Comunidad | ¿Qué aprendimos? | ADRs revisados y criterio compartido. |
