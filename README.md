# Práctica Calificada 3 - Simulación de Selección Natural
### Curso Tópicos en Ciencias de la Computación
### Estudiantes: 
- Ibrahim Imanol Jordi Arquiñigo Jacinto
- Ian Joaquin Sanchez Alva
- Eduardo Jose Rivas Siesquen
- Daniel Orlando Luis Lázaro

## Introducción

La presente práctica calificada tiene como objetivo implementar un sistema de simulación de selección natural inspirado en el video “Simulating Natural Selection” del youtuber Primer. La simulación modelará criaturas simples (blobs) que deben buscar alimento diariamente, sobrevivir o morir según sus recursos y potencialmente desarrollar nuevas características, como mayor velocidad. A partir de los requerimientos proporcionados, este informe describe el diseño general del sistema, su arquitectura, el comportamiento esperado de los blobs, la estructura del gestor de la simulación, el diseño de la interfaz gráfica y evidencias de la implementación.

## Descripción del Problema

El problema consiste en construir un entorno artificial en el que criaturas elementales compiten por alimento en un mapa rectangular, enfrentando presión selectiva derivada de recursos limitados. Cada blob inicia desde un punto de origen, se desplaza por el mapa, consume energía, busca comida y finalmente regresa. Según su desempeño, puede sobrevivir, morir o presentar una mutación que le otorgue una ventaja competitiva. La simulación se organiza en “días”, durante los cuales ocurre el ciclo completo de exploración, alimentación, retorno y evaluación. Además, se requiere una interfaz gráfica que permita visualizar la dinámica poblacional, las rutas de los blobs, las mutaciones y los cambios de velocidad de la simulación. Aunque los blobs son objetos y no agentes autónomos, deben tener un comportamiento lo suficientemente rico como para producir selección natural emergente.

## Diseño General del Sistema

El sistema propuesto se compone de varios elementos que interactúan de manera controlada por un agente central. A continuación se describen los componentes principales y su relación conceptual.

### Componentes Principales

- Blob: Objeto que representa una criatura con atributos como posición, energía, velocidad y características variables. Puede desplazarse, buscar comida, consumir energía, morir o desarrollar nuevas características.
- Food (Comida): Entidad simple distribuida en el mapa al inicio de cada día, que puede ser consumida por un blob.
- BlobManager: Agente encargado de actualizar los blobs, controlar la población máxima, generar comida, manejar el ciclo diario y proveer información a la GUI. Es equivalente a un “host agent”.
- Mapa: Espacio bidimensional donde los blobs se desplazan. Es rectangular y define posiciones iniciales aleatorias.
- GUI: Interfaz que muestra las posiciones y estados de los blobs en tiempo real, permitiendo ajustar la velocidad de la simulación.

### Flujo de Simulación por Día

1. Generación de comida en el mapa.
2. Inicialización de blobs en su punto de origen.
3. Los blobs salen a buscar alimento.
4. Consumición de energía durante desplazamiento.
5. Consumo de comida y aumento de energía.
6. Regreso al punto de origen.
7. Evaluación de supervivencia o muerte.
8. Aplicación de mutaciones en blobs sobrevivientes.
9. Preparación del siguiente día.

### Consideraciones sobre Selección Natural

El sistema implementa un mecanismo de selección natural basado en limitación de recursos. Como los blobs deben competir por una cantidad reducida de comida, aquellos con características más ventajosas (como mayor velocidad o menor consumo energético) tienen más probabilidad de sobrevivir y transmitir esa característica en generaciones posteriores o mantenerla como ventaja persistente. Las mutaciones introducen variabilidad, permitiendo que algunos blobs obtengan ventajas inesperadas que pueden volverse dominantes si el entorno lo favorece. Este modelo reproduce de manera simplificada los principios de presión selectiva, variación heredable y supervivencia diferencial.
