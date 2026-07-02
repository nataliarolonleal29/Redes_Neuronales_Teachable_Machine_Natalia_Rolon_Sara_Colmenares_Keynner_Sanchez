# Actividad Práctica — Redes Neuronales y Clasificación con Teachable Machine

***Autores*** :
- Natalia Rolon Leal
- Sara Lucia Colmenares Bonilla
- Keynner Sanchez 

# Descripción del problema

En entornos educativos es común que se requiera identificar rápidamente determinados objetos utilizados por los estudiantes. Realizar esta tarea manualmente puede ser repetitivo y propenso a errores. Por ello, este proyecto propone desarrollar un modelo de Inteligencia Artificial capaz de reconocer diferentes objetos escolares utilizando la cámara web y una red neuronal entrenada con Teachable Machine.

El sistema busca automatizar el reconocimiento visual de objetos mediante técnicas de aprendizaje automático, permitiendo clasificar cada imagen en una categoría específica.

---

# Objetivo

Diseñar, entrenar y evaluar un modelo de clasificación de imágenes utilizando Teachable Machine, comprendiendo el funcionamiento de una red neuronal y su capacidad para identificar patrones visuales mediante el análisis de píxeles.

---

# Clases utilizadas

El modelo fue entrenado para reconocer tres clases:

* Atenta
* Distraída
* Cansada

Cada una de estas clasificaciones, tienen unas subclasificaciones

* Atenta: Mira al frente, ojos abiertos, Buena postura
* Distraída: Mira a otro lado, usa el celular, aburrida
* Cansada: Cabeza inclinada, ojos entrecerrdos, ojos cerrados

Estas tres clasificaciones fueron seleccionadas porque representan diferentes estados de animo, que indican si una persona relamente esta prestando atención y conciente de su entorno. Ademas, se optó por otras tres subclasificaciones por cada clase general (atenta, distraida, cansada), para que el programa tuviera mas ejemplos de las diferentes señales que podria sugerir si la persona esta atenta y conciente.

---

# Dataset utilizado

El dataset fue construido por el equipo mediante fotografías tomadas con la cámara del computador.

Se procuró capturar imágenes con diferentes condiciones para mejorar la capacidad de generalización del modelo.

### Características del dataset

* Diferentes posiciones de los objetos.
* Distintas distancias respecto a la cámara.
* Cambios de iluminación.
* Fondos variados.
* Diferentes orientaciones.

### Cantidad de imágenes

Por cada clase se tomo entre 90-100

---

# Entrenamiento del modelo

El modelo fue desarrollado utilizando **Google Teachable Machine**, una plataforma que permite entrenar modelos de aprendizaje automático mediante redes neuronales convolucionales sin necesidad de programar el entrenamiento desde cero.

Durante el entrenamiento, el modelo aprendió a identificar patrones característicos de cada clase a partir de las imágenes proporcionadas.

Posteriormente se realizaron múltiples pruebas utilizando la cámara web para verificar el comportamiento del sistema en tiempo real.

---

# Análisis de la Red Neuronal: ¿Qué "ve" realmente la IA?

Al entrenar nuestro modelo en Teachable Machine con imágenes clasificadas en diferentes estados (como `Mira al frente - Atenta`, `Usa el celular - Distraída`, `Cabeza inclinada - Cansada` u `Ojos cerrados - Dormida`), es fundamental aclarar que la inteligencia artificial **no "ve" personas, rostros ni expresiones** en la forma en que lo hace un ser humano. La IA no posee un entendimiento conceptual de lo que significa "estar distraído" o "estar cansado". En su lugar, el modelo procesa la información de manera puramente matemática y algorítmica.

A continuación, se detalla cómo funciona internamente la red neuronal de nuestro proyecto:

### 1. La Materia Prima: Píxeles, Números y Colores
Cada imagen capturada por la cámara web o subida a la plataforma es descompuesta en una matriz bidimensional o tridimensional de **píxeles**. Para la computadora, cada píxel es simplemente un **número** (o un conjunto de tres números en el espacio de color RGB: Red, Green, Blue) que representa la intensidad de la luz y el **color** en un punto específico del espacio. 
* Por ejemplo, la clase `Usa el celular - Distraída` no es interpretada como una persona con un teléfono, sino como una configuración específica de números y contrastes concentrados en una zona determinada de la matriz de entrada.

### 2. Extracción y Reconocimiento de Patrones
A medida que la información numérica avanza por las capas de la red, el algoritmo identifica **relaciones matemáticas** y correlaciones espaciales entre los píxeles. La red neuronal aprende a detectar **patrones** visuales abstractos sin entender su significado real:
* **Bordes y líneas:** El contraste entre el contorno de la silueta y el fondo.
* **Formas complejas:** La geometría de los ojos (abiertos vs. entrecerrados o cerrados) o la inclinación del eje de la cabeza en píxeles.

### 3. El Proceso de Computación: Forward Pass y Pesos Neuronales
Cuando el modelo recibe una imagen para evaluar, se ejecuta un proceso llamado **Forward Pass** (paso hacia adelante). En esta etapa, los valores numéricos de los píxeles de entrada se multiplican por los **pesos neuronales** (parámetros numéricos que determinan la importancia o relevancia de cada característica visual) a lo largo de las capas de la red. 
* Durante el entrenamiento, estos pesos se ajustaron de manera que si el *Forward Pass* detecta combinaciones de píxeles que coinciden con los patrones de la clase `Aburrida - Distraída` (como una mano apoyada en la cara), los pesos asociados a esa etiqueta se activarán con mayor fuerza.

### 4. Clasificación y Probabilidades
El objetivo final de toda esta estructura algebraica es la **clasificación**. Al llegar a la capa de salida, la red neuronal aplica una función matemática (comúnmente *Softmax*) para transformar las señales numéricas finales en una distribución de **probabilidades**. 

El modelo no afirma conceptualmente *"la alumna está dormida"*, sino que calcula una salida probabilística:

$$\text{Resultado} = \begin{cases} P(\text{Atenta}) = 0.05 \\ P(\text{Distraída}) = 0.10 \\ P(\text{Cansada}) = 0.15 \\ P(\text{Dormida}) = 0.70 \end{cases}$$

La clase que obtenga el mayor porcentaje numérico será la predicción final que se renderiza en la interfaz.

---
> **Conclusión:** La IA de nuestro proyecto "ve" una inmensa matriz de números que representan colores, y a través de operaciones algebraicas en el *Forward Pass*, filtra y asocia esos números con los pesos optimizados en el entrenamiento para predecir, probabilísticamente, la etiqueta correspondiente.
