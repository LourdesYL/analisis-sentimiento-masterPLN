# Análisis de sentimiento en español con BETO

Proyecto académico de clasificación de reseñas hoteleras en español en tres categorías: negativas, neutras y positivas. Incluye ajuste de un modelo BETO, evaluación cuantitativa y análisis lingüístico de aciertos y errores mediante LIME.

Este cuaderno forma parte del trabajo final de la asignatura Análisis de Sentimiento del Máster en Procesamiento del Lenguaje Natural realizado en la Universidad de La Rioja (2024-2026). Este repositorio conserva el cuaderno y sus resultados originales e incorpora una revisión posterior de sus limitaciones.

## Objetivo

Explorar el rendimiento de un transformador preentrenado en español para clasificar opiniones y analizar las dificultades que presentan las reseñas neutras, las valoraciones mixtas y otros casos ambiguos.

## Datos

Se utiliza la versión completa del corpus **Andalusian Hotels’ Reviews**, con 18.172 reseñas.

- Positivas: 13.227.
- Negativas: 2.671.
- Neutras: 2.274.

Fuente: [Andalusian Hotels’ Reviews en Kaggle](https://www.kaggle.com/datasets/chizhikchi/andalusian-hotels-reviews-unbalanced).

El corpus no se incluye en este repositorio. Sus condiciones de acceso y uso deben consultarse en la fuente original.

## Procedimiento

1. Unión del título y el cuerpo de cada reseña.
2. División estratificada en entrenamiento (80 %), validación (10 %) y prueba (10 %).
3. Tokenización con una longitud máxima de 128 tokens.
4. Ajuste del modelo `dccuchile/bert-base-spanish-wwm-uncased`.
5. Exploración de configuraciones de entrenamiento.
6. Evaluación global y por clase.
7. Análisis de ejemplos con pérdidas altas y explicaciones locales mediante LIME.

## Resultados originales

La siguiente tabla corresponde a la evaluación en prueba del modelo inicial, ajustado durante cinco épocas. El conjunto de prueba contiene 1.818 reseñas.

| Métrica | Resultado |
|---|---:|
| Accuracy | 0,9312 |
| Macro-F1 | 0,8693 |
| F1 — Negativas | 0,91 |
| F1 — Neutras | 0,73 |
| F1 — Positivas | 0,97 |

Son resultados guardados en el cuaderno original, no recalculados para esta publicación. No deben confundirse con los resultados de los experimentos posteriores.

La diferencia entre el F1 de la clase neutra y el de las otras clases motiva el análisis cualitativo. El macro-F1 complementa la accuracy al dar el mismo peso a cada clase en un corpus desequilibrado.

## Análisis lingüístico

El cuaderno explora dificultades como:

- Reseñas que combinan elogios y críticas.
- Fronteras ambiguas entre neutralidad y valoración positiva moderada.
- Posibles discrepancias entre las etiquetas originales y la interpretación del texto.
- Presencia de reseñas en otros idiomas.
- Influencia local de palabras y expresiones en las predicciones.

Las discrepancias con las etiquetas se consideran hipótesis que requieren revisión, no errores de anotación demostrados. Las explicaciones de LIME son aproximaciones locales al comportamiento del modelo.

## Limitaciones y revisión posterior

El cuaderno se conserva como registro del trabajo académico. En una revisión posterior se han identificado aspectos que afectan a la interpretación y a la reproducción de los experimentos:

- Los experimentos posteriores parten de un modelo ya ajustado durante cinco épocas. Por tanto, el experimento de tres épocas añade tres más; no demuestra que tres épocas totales sean equivalentes a cinco.
- La tabla comparativa final del cuaderno mezcla métricas de distintos experimentos y conjuntos. Para esta presentación se utilizan únicamente las cifras identificadas en la sección de resultados anterior.
- La descripción de la selección del mejor modelo no coincide plenamente con la configuración mostrada.
- Existen dependencias de archivos y modelos guardados en Google Drive, además de una variable utilizada sin definición visible.
- Algunas interpretaciones lingüísticas y de LIME necesitan formularse con mayor cautela.
- Es necesario comprobar el efecto del truncamiento antes de interpretar la ausencia de determinadas expresiones en las explicaciones.

Estas limitaciones se documentan sin repetir los entrenamientos originales.
[Consultar la revisión crítica y las posibles correcciones](revision_critica.md).

## Consultar el cuaderno

[Abrir el cuaderno con código, explicaciones y resultados](analisis_sentimiento_transformers.ipynb).

El archivo puede consultarse en GitHub sin ejecutarlo. Su ejecución completa requiere datos, modelos y un entorno que no se distribuyen con este repositorio. No se ha verificado su ejecución desde cero para esta publicación.

El cuaderno contiene también conclusiones de un proyecto académico más amplio, con enfoques basados en lexicones, regresión logística y redes recurrentes. Sus implementaciones no están incluidas aquí.

## Tecnologías utilizadas

Python · pandas · NumPy · scikit-learn · PyTorch · Hugging Face Transformers · Datasets · Matplotlib · LIME · Google Colab

## Autoría y contexto académico

**Lourdes Yagüe Lobo**

Trabajo académico desarrollado a partir de los procedimientos y cuadernos docentes de la asignatura. El proyecto final de la asignatura pedía la comparación de 4 modelos para la tarea de análisis de sentimientos: (1) Lexicon, (2) ML Tradicional, (3) Deep Learning y, finalmente (4) Transformers. Este cuaderno corresponde al 4º caso. El propio cuaderno identifica el uso de una tarea previa como base para los experimentos con transformadores.

El corpus, el modelo preentrenado y las bibliotecas utilizadas corresponden a sus respectivos autores.
