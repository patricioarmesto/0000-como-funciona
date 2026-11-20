---
status: accepted
---

# Un repositorio por ejercicio

Cada ejercicio vive en su propio repositorio autocontenido, con nombre `NNNN-slug`, en lugar de ser un directorio dentro de un monorepo. Se decidió así porque la unidad de aprendizaje es el ejercicio completo: se clona, se levanta con los mismos tres comandos y se explica sin depender de otro repo. Este repositorio `0000` existe solo como índice y guía.

**Considered Options**

- **Monorepo con un directorio por ejercicio.** Simplifica el CI centralizado, pero obliga a clonar los 1024 ejercicios para ver uno y rompe la promesa de que cada ejercicio es autocontenido.
- **Repo por ejercicio (elegido).** Repite configuración entre repos, pero mantiene el aislamiento, la independencia de clonado y un único punto de entrada para cada ejercicio.

**Consequences**

- Hay 1024 repositorios más el índice: el descubrimiento depende de este README y del calendario.
- Los tres comandos de arranque deben ser idénticos en todos los repositorios; cualquier excepción se documenta en el README del ejercicio.
- Un error de configuración se corrige en un repo y no se propaga automáticamente a los demás.
