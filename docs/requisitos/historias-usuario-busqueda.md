# Historias de usuario de búsqueda

| Campo | Valor |
| --- | --- |
| Proyecto | Proyecto Simbiosis |
| Fecha | 28/10/2026 |
| Versión | 0.1 |
| Estado | Borrador |

## Fuentes comunes

- [Acta de UC-21 Buscar recetas](../captura/acta-acuerdos-uc-21-buscar-recetas.md), v1.1, Vigente.
- [Catálogo de requisitos](catalogo-requisitos.md), UR-08 y FR pertinentes.
- [Modelo de casos de uso](../modelos/modelo-casos-de-uso.md), UC-21.

## Épica de búsqueda

Como persona usuaria registrada, quiero buscar recetas por una palabra o frase, por los ingredientes que quiero usar y excluyendo los que no quiero, para encontrar con rapidez recetas que se ajusten a lo que busco.

**Estado:** descompuesta en US-01, US-02 y US-03. Conserva la necesidad conjunta.

## Justificación de la división

La épica se divide por capacidad de búsqueda y no por pantallas ni tareas: cada historia entrega una búsqueda completa con resultados y puede usarse sin las otras, incluida la exclusión de ingredientes, que funciona sin otros criterios. La combinación de criterios se comprueba en los criterios de aceptación, conforme al acta, y no es una historia aparte.

## US-01

**Título:** Buscar recetas por una palabra o frase

Como persona usuaria registrada, quiero buscar recetas por una palabra o frase, para encontrar una receta cuando recuerdo cómo se llama o de qué trata.

**Fuentes:** UR-08; UC-21; FR-085; acta, «Criterios de búsqueda» y «Búsqueda sin resultados».

### Criterios de aceptación

- **CA-01.** Dado que existen una receta publicada y validada titulada «Tarta de Santiago» y otra cuya descripción breve dice «Santiago y tarta de almendra», cuando la persona busca «tarta de santiago», entonces los resultados incluyen «Tarta de Santiago» y no incluyen la otra, porque la frase no aparece seguida y en el mismo orden.
- **CA-02.** Dado que ninguna receta publicada y validada contiene «tortila de patatas», cuando la persona busca esa frase, entonces el sistema indica que no hay resultados, conserva el texto buscado y propone «tortilla de patatas» como corrección, separada de los resultados, sin ejecutar otra búsqueda.
- **CA-03.** Dado que el campo de texto está vacío y no se ha indicado ningún otro criterio, cuando la persona solicita buscar, entonces el sistema pide indicar al menos un criterio y no ejecuta la búsqueda.

## US-02

**Título:** Buscar recetas por ingredientes incluidos

Como persona usuaria registrada, quiero buscar recetas que contengan los ingredientes que quiero usar, para decidir qué cocinar con lo que tengo.

**Fuentes:** UR-08; UC-21; FR-086; acta, «Criterios de búsqueda» y «Resultados y detalle».

### Criterios de aceptación

- **CA-01.** Dado que existen la receta R1 con harina, huevo y azúcar, y la receta R2 con harina y huevo, ambas publicadas y validadas, cuando la persona selecciona harina, huevo y azúcar, entonces los resultados incluyen R1 y no incluyen R2, porque debe contener todos los ingredientes seleccionados.
- **CA-02.** Dado que existen «Tarta de Santiago», con almendra, y «Tarta de queso», con queso, ambas publicadas y validadas, cuando la persona busca la frase «tarta» y selecciona almendra, entonces los resultados incluyen solo «Tarta de Santiago», porque cumple el texto y el ingrediente.
- **CA-03.** Dado que dos recetas publicadas y validadas con huevo se publicaron el 20/10/2026 y el 15/10/2026, y otra con huevo está pendiente de validación, cuando la persona selecciona huevo, entonces los resultados muestran primero la del 20/10 y después la del 15/10, con título, imagen, calificación promedio y descripción breve, y no muestran la pendiente.

## US-03

**Título:** Excluir ingredientes de la búsqueda

Como persona usuaria registrada, quiero excluir los ingredientes que no quiero, para obtener solo recetas que no los contengan.

**Fuentes:** UR-08; UC-21; FR-087; acta, «Criterios de búsqueda» y «Búsqueda sin resultados».

### Criterios de aceptación

## Dudas pendientes

Ninguna.

- **CA-01.** Dado que existen R1 con huevo y leche, R2 con huevo y almendra, y R3 con harina y azúcar, todas publicadas y validadas, cuando la persona excluye leche y almendra sin indicar otros criterios, entonces los resultados incluyen solo R3, porque R1 y R2 contienen alguno de los ingredientes excluidos.
- **CA-02.** Dado que la persona ha seleccionado huevo para incluirlo, cuando lo selecciona también para excluirlo y solicita buscar, entonces el sistema señala el conflicto y no ejecuta la búsqueda hasta que lo corrija.
- **CA-03.** Dado que ninguna receta publicada y validada contiene bacalao y no contiene sal, y el sistema dispone de «merluza» como alternativa, cuando la persona incluye bacalao y excluye sal, entonces el sistema indica que no hay resultados y propone la alternativa «merluza» manteniendo la exclusión de sal, sin proponer retirar la exclusión.

## Revisión INVEST

La revisión abarca US-01, US-02 y US-03. «Aplicado» indica si se ha realizado la comprobación. «Cumple» indica si todas las historias cumplen el criterio. Si alguna no lo cumple, indicar «No» e identificar la historia y el motivo en la justificación. Si no se ha realizado la comprobación o faltan datos, indicar «Pendiente» en «Cumple».

| Criterio | Pregunta de revisión | Aplicado | Cumple | Justificación |
| --- | --- | --- | --- | --- |
| Independiente | ¿Puede implementarse cada historia y ofrecer un resultado útil sin implementar antes las otras historias del conjunto? Puede compartir infraestructura con ellas. | Sí | Sí | Cada historia ofrece una búsqueda útil por sí sola, y US-03 funciona sin otros criterios. Comparten la infraestructura de búsqueda, pero no hace falta implementar una para usar otra. Solo US-02 CA-02 combina texto e ingrediente y se comprueba cuando existen US-01 y US-02; los demás criterios no dependen de otra historia. |
| Negociable | ¿Cada historia explica qué necesita la persona y deja margen para discutir los detalles de la solución, respetando los acuerdos confirmados? | Sí | Sí | US-01, US-02 y US-03 expresan la necesidad sin fijar pantallas, controles ni algoritmos; solo recogen los acuerdos del acta. |
| Valiosa | ¿La parte «para…» de cada historia explica el beneficio que obtiene la persona al usar esa capacidad? | Sí | Sí | Cada «para…» indica un beneficio concreto: encontrar una receta por su nombre o tema (US-01), decidir qué cocinar con lo que se tiene (US-02) y obtener solo recetas sin los ingredientes no deseados (US-03). |
| Estimable | ¿Están claros el alcance y los datos necesarios para estimar el trabajo de cada historia? | Sí | Sí | El acta define los criterios, los resultados, las sugerencias y los errores de cada historia, así que el alcance y los datos necesarios están acotados. |
| Pequeña | ¿Se centra cada historia en una única capacidad de alcance manejable? | Sí | Sí | Cada historia se centra en un criterio de búsqueda y deja fuera los filtros adicionales, las recomendaciones y los favoritos. |
| Comprobable | ¿Los criterios de aceptación de cada historia describen acciones y resultados observables que permiten distinguir un comportamiento correcto de uno incorrecto? | Sí | Sí | Los nueve criterios usan datos concretos, una acción y un resultado observable, como las recetas que aparecen o no, el mensaje de conflicto y las sugerencias. |

