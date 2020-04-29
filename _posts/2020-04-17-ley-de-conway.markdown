---
layout: post
title:  "La ley de Conway"
date:   2019-11-24 15:22:26 -0300
category: Arquitectura
author: Matías Reyes
---

# La Ley de Conway

La **Ley de Conway**, el enunciado de Melvin Conway en 1967, dice:

  > Las organizaciones ... están abocadas a producir diseños que son copias de las estructuras de comunicación de dichas organizaciones.

Dicho de otra manera, las arquitecturas de sistemas reflejan la estructura organizacional. Esta observación ha sido comprobada en estudios posteriores, sin embargo la causa del también denominado "efecto espejo" tiene muchas aristas, desde un diseño intencional, como es el caso del "Domain Driven Design", hasta algo más práctico como es que los presupuestos de las áreas financian sistemas para sus usuarios. Por esto, aún cuando el diseño del sistema sea independiente de la organización, su implementación se asemeja a su estructura.

La realidad es que también las organizaciones que se han ido moldeando a las arquitecturas impuestas por sus sistemas. En algunos casos esto es intencional, como es la implementación de SAP como estandarizador de los procesos de la industria, pero en otros casos no lo es.

## Sistemas de datos

En todos los sistemas existen "cuellos de botella" que restringen su velocidad total. En el caso de la persistencia de datos (o bases de datos), este suele ser el disco duro, que para sus operaciones involucra el movimiento del disco y del cabezal hasta el punto donde se encuentra el sector donde está el dato (HDD); y muchas veces para encontrar el dato se requieren varias búsquedas y lecturas, las que pueden ser optimizadas utilizando índices que indican donde se encuentran los datos. En el caso de la escritura el costo es mayor porque requiere una la búsqueda, escritura y luego se deben actualizar (reordenar y reescribir) todas las referencias o índices.

La restricción de velocidad de disco ha dado origen a muchas estrategias para su optimización. Si a esto se le añaden las estrategias para construir bases de datos distribuidas dadas las restricciones de velocidad y fiabilidad de las redes, obtenemos cientos de combinaciones que se ven reflejadas en la gran diversidad de motores de bases de datos existentes, cada una con ventajas y desventajas que dependen del uso de los datos. Esto es lo que origina la separación entre las bases de datos que tienen objetivos transaccionales (optimizadas para la actualización de registros) y las bases de datos analíticas (optimizadas para las agregaciones de datos o Buisiness Intelligence).

Todo lo anterior ha llevado a que los eventos que ocurren en las operaciones de una empresa sean registrados en bases de datos transaccionales, generalmente [relacionales](https://es.wikipedia.org/wiki/Base_de_datos_relacional) y para el análsis se empleen procesos de Extracción, Transformación y Carga (ETL) que mueven los datos a bases de datos para el análisis (comunmente denominados Data Warehouse).

Que el Data Warehouse sea un artefacto separado del sistema transaccional ha generado funciones empresariales distintas: Equipos técnicos separados para cada especialidad, equipos de BI, y equipos operativos. A su vez, los sistemas construidos son muchas veces analíticos u operativos (en gran medida gracias a las herramientas de BI). ¿Hubiéramos hecho esta separación si no hubieran restricciones técnicas? ¿qué pasaría si las funciones operativas tuvieran todas las capacidades analíticas?.

Las empresas con arquitecturas de datos maduras han logrado unir esos dos mundos, es así como cuando pides un automovil en Uber, se te asigna un tiempo de viaje y un precio estimado, o cuando decides hacer marketing por Facebook, puedes apuntar a un público objetivo muy preciso.

Lo anterior se logra con un conjunto de técnicas y herramientas que permiten que los datos fluyan a otras aplicaciones y bases de datos, almacenándolos y presentándolos distintas maneras. Esto requiere infraestructura, coordinación entre equipos, capacidades técnicas, conocimiento del negocio y tiempo, por lo que se debe implementar una estrategia de largo plazo, pero por mientras, hay que unir los proyectos operativos con los analíticos; de ahí puede nacer el requerimiento y la innovación.
