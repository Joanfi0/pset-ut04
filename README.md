# pset-ut04

# Grafos no dirigidos — Guía de trabajo

Este documento resume el estado de los ejercicios 8 al 12 del Problem Set UT04 y las tareas de programación pendientes. No contiene implementaciones Java.

## Estado general

| Ejercicio | Trabajo realizado | Pendiente de código |
|---|---|---|
| 8 — Prim | Modelo del grafo, lista de adyacencias, representación gráfica, ejecución manual, pseudocódigo, prueba con cuatro zonas, casos de prueba y contenido del póster. | No exige implementación Java en este PDF. |
| 9 — Kruskal | Representación gráfica y ejecución paso a paso. | No exige implementación Java. |
| 10 — Búsqueda en amplitud | Recorrido desde E, árbol abarcador, pseudocódigo y precondiciones. | Parte 3: implementar BFS con las estructuras existentes. |
| 11 — Puntos de articulación | Grafo, identificación de ciudades críticas, explicación, precondiciones y pseudocódigo. | Parte 3: implementar el método de puntos de articulación. |
| 12 — Número de Bacon | Casos de prueba descritos. | Implementar el método, cargar archivos, ejecutar consultas y guardar resultados. |

Las resoluciones están desarrolladas en el chat. Este README funciona como guía de continuidad; no sustituye esas resoluciones ni incluye un póster diagramado listo para imprimir.

## Ejercicio 10 — Parte 3: búsqueda en amplitud

### Trabajo pendiente

- Revisar la interfaz y las estructuras de grafos ya implementadas en el proyecto del curso.
- Implementar BFS utilizando una cola y un registro de vértices visitados.
- Marcar cada vértice cuando ingresa en la cola, evitando incorporarlo más de una vez.
- Adaptar la firma y el resultado del método a la interfaz existente.
- Comprobar el recorrido sobre el grafo del ejercicio, comenzando desde E.

### Resultado de referencia

Procesando los vecinos en orden alfabético:

- Recorrido: **E, D, F, G, B, C, H, A**.
- Aristas del árbol: **E–D, E–F, E–G, D–B, D–C, F–H, B–A**.
- Niveles: **{E}; {D, F, G}; {B, C, H}; {A}**.

Los pesos no intervienen en BFS. Otro orden de vecinos puede producir otro recorrido y otro árbol válidos, conservando los niveles.

### Verificación

- Cada vértice alcanzable se visita una sola vez.
- Se respeta el orden por niveles.
- Se controla que el origen pertenezca al grafo.
- Si el grafo es desconectado, una búsqueda desde un único origen solo alcanza su componente.

## Ejercicio 11 — Parte 3: puntos de articulación

### Trabajo pendiente

Implementar el método solicitado por la consigna:

`<V, E> List<V> puntosDeArticulacion(IGraph<V, E> grafo)`

El método debe devolver los puntos de articulación de un grafo no dirigido conexo, utilizando las operaciones disponibles en el proyecto.

### Criterios del algoritmo

- Realizar una búsqueda en profundidad (DFS).
- Registrar el padre, el orden de descubrimiento y el valor `low` de cada vértice.
- Para un vértice que no es raíz, comprobar si algún hijo cumple `low[hijo] >= descubrimiento[vertice]`.
- Para la raíz, comprobar si tiene más de un hijo en el árbol DFS.
- Evitar duplicados en el resultado.

### Resultado de referencia

**Nairobi y Mekele** son los puntos de articulación:

- Al eliminar Nairobi, Cairo queda aislada.
- Al eliminar Mekele, Praia queda aislada.

### Verificación

- Red del ejercicio: devolver Nairobi y Mekele, sin duplicados.
- Cadena de tres vértices: devolver solo el vértice central.
- Triángulo: no devolver puntos de articulación.
- Un único vértice: no devolver puntos de articulación.
- Raíz DFS con un solo hijo: no marcarla únicamente por tener varios vecinos.

## Ejercicio 12 — Número de Bacon

### Punto 1: implementar numBacon

- Recibir el nombre de un actor.
- Calcular la cantidad mínima de vínculos hasta `Kevin_Bacon` mediante BFS.
- Devolver 0 para Kevin Bacon y 1 para un actor conectado directamente con él.
- Definir cómo informar un actor inexistente y un actor sin conexión. La consigna no fija un valor para esos casos.

### Punto 2: programa principal

- Cargar los vértices desde `actores.csv`.
- Cargar las aristas desde `en_películas.csv`.
- Representar las relaciones como no dirigidas y conservar el nombre de la película como etiqueta de la arista.
- Invocar `numBacon` para los actores solicitados e imprimir los resultados.

### Punto 3: ejecución y resultados

Consultar estos actores:

1. `John_Goodman`
2. `Tom_Cruise`
3. `Jason_Statham`
4. `Lukas_Haas`
5. `Djimon_Hounsou`

Registrar los resultados en la entrega y en `salida.txt`, adjuntándolo al código completo.

Los valores deben obtenerse del grafo cargado desde los archivos del curso. No se pueden deducir del PDF ni sustituir por datos de otras fuentes.

### Punto 4: aplicar los casos de prueba

Los casos ya fueron descritos en el chat. Falta verificar la implementación con ellos:

- Kevin Bacon: resultado 0.
- Relación directa: resultado 1.
- Cadena con dos o tres vínculos: resultado 2 o 3.
- Rutas de distinta longitud: elegir la de menos vínculos.
- Rutas mínimas empatadas: devolver la misma distancia mínima.
- Ciclos: terminar sin repetir visitas indefinidamente.
- Actor aislado o en otra componente: informar que no hay conexión.
- Actor inexistente: informar la situación según el contrato elegido.
- Relaciones cargadas en sentido inverso: mantener el comportamiento no dirigido.
- Consultas sucesivas: no reutilizar incorrectamente el estado de visitados.
- Carga de datos: comprobar actores repetidos, relaciones repetidas y extremos inexistentes.

## Material necesario para continuar

- Proyecto Java del curso e interfaces de grafos.
- Clases y estructuras ya implementadas.
- Archivos `actores.csv` y `en_películas.csv`.
- Formato real de esos archivos y convenciones de errores del proyecto.

Estos materiales no se proporcionaron en el chat; solo se revisó el PDF de la consigna. Las firmas no indicadas por el PDF deben verificarse en el proyecto antes de programar.

## Lista de pendientes

- [ ] Implementar y verificar BFS del ejercicio 10.
- [ ] Implementar y verificar puntos de articulación del ejercicio 11.
- [ ] Implementar `numBacon` del ejercicio 12.
- [ ] Implementar la carga de actores y películas.
- [ ] Ejecutar las cinco consultas solicitadas.
- [ ] Crear `salida.txt` con los resultados reales.
- [ ] Aplicar los casos de prueba del ejercicio 12.
- [ ] Preparar los archivos de entrega según la consigna del curso.

## Referencias rápidas de las resoluciones manuales

| Ejercicio | Resultado |
|---|---|
| 8 — Prim | 5 caminos; costo mínimo 8 km. Una solución: 1–4, 4–6, 1–2, 2–3, 3–5. |
| 8 — Prueba con cuatro zonas | 3 caminos; costo mínimo 4 km. |
| 9 — Kruskal | 5 caminos; costo mínimo 8 km. Solución: 1–4, 2–3, 4–6, 3–4, 3–5. |
| 10 — BFS desde E | E, D, F, G, B, C, H, A, usando vecinos en orden alfabético. |
| 11 — Articulaciones | Nairobi y Mekele. |

**Atención:** la distancia entre las zonas 1 y 2 es 2 km en el ejercicio 8 y 3 km en el ejercicio 9.
