# Revisión crítica del proyecto

Esta revisión acompaña al cuaderno académico original. Aquí pretendo identificar limitaciones del procedimiento y de la interpretación de los resultados, y proponer posibles correcciones.

Las propuestas descritas aquí no se han implementado ni evaluado, ya que he preferido conservar el código y las salidas de los experimentos originales, tal cual los presenté en el trabajo final de la asignatura.

## 1. Punto de partida de los experimentos

Los experimentos posteriores cargan un modelo que ya había sido ajustado durante cinco épocas sobre el conjunto de entrenamiento, en ejercicios previos de la asignatura.

Por tanto, el experimento descrito como de tres épocas incorpora tres épocas adicionales: ocho épocas acumuladas. No permite concluir que entrenar tres épocas desde el modelo preentrenado sea equivalente a entrenar cinco.

**Posible corrección:** iniciar todas las configuraciones desde el mismo modelo preentrenado y registrar tanto las épocas adicionales como las acumuladas.

## 2. Correspondencia entre métricas y experimentos

La tabla final del cuaderno combina cifras procedentes de distintas evaluaciones:

- La accuracy de 0,9307 corresponde a validación del experimento 1.
- El macro-F1 de 0,8693 corresponde a prueba del modelo inicial de cinco épocas.
- La evaluación en prueba del experimento 1 muestra una accuracy de 0,9301.
- El recall de la clase neutra aparece como 0,86 en las conclusiones, mientras que los informes mostrados indican aproximadamente 0,71–0,72.

**Posible corrección:** construir las tablas a partir de registros que identifiquen el modelo, su configuración y el conjunto evaluado. El README utiliza únicamente los resultados de prueba del modelo inicial de cinco épocas.

## 3. Selección del mejor modelo

La explicación del cuaderno indica que se utiliza el mejor modelo al finalizar el entrenamiento. Sin embargo, la configuración mostrada no incluye los argumentos necesarios para respaldar esa selección automática, como `load_best_model_at_end` y `metric_for_best_model`.

**Posible corrección:** configurar explícitamente la evaluación durante el entrenamiento, la selección por macro-F1 de validación y la recuperación del checkpoint correspondiente.

## 4. Ejecución y dependencias

El cuaderno depende de archivos CSV y modelos almacenados en rutas personales de Google Drive. Además, utiliza la variable `df_test_sorted` sin una definición visible.

Las salidas guardadas permiten consultar el trabajo, pero no garantizan que el archivo pueda ejecutarse de principio a fin en un entorno nuevo.

**Posible corrección:** completar las variables necesarias, utilizar rutas configurables y documentar las dependencias y sus versiones. Después, verificar la ejecución en una sesión limpia.

## 5. Interpretación de las etiquetas

Una discrepancia entre una predicción y la etiqueta original no demuestra un error de anotación. Tampoco lo demuestra el desacuerdo de la autora con esa etiqueta.

Una opinión positiva moderada puede seguir siendo positiva. Una reseña con elogios y críticas no tiene por qué ser neutra: depende de la definición de las categorías y del criterio de anotación.

**Posible corrección:** consultar cómo se construyeron las etiquetas, definir criterios explícitos y revisar una muestra con más de una persona. Mantener separadas las etiquetas originales y las propuestas de revisión.

## 6. Interpretación de LIME

LIME aproxima localmente el comportamiento del clasificador mediante perturbaciones del texto. Sus resultados no demuestran que BERT razone de la forma descrita en algunos comentarios del cuaderno.

Una contribución negativa para una clase tampoco identifica por sí sola hacia qué otra clase se desplaza la predicción.

**Posible corrección:** formular las interpretaciones como hipótesis locales, fijar la semilla y comprobar la estabilidad de las explicaciones con distintas muestras de perturbaciones.

## 7. Truncamiento de las reseñas

La tokenización limita las entradas a 128 tokens. En reseñas largas, parte del contenido queda fuera de la entrada del modelo.

Antes de interpretar por qué una crítica no parece influir en la predicción, es necesario comprobar si el modelo recibió ese fragmento.

**Posible corrección:** medir qué proporción de reseñas se trunca y revisar los tokens recibidos en los ejemplos analizados.

## 8. Entrenamiento, validación y prueba

Una de las propuestas del cuaderno plantea añadir ejemplos a validación para que el modelo aprenda. Sin embargo, el ajuste de sus pesos se realiza con los datos de entrenamiento.

**Posible corrección:** incorporar nuevos ejemplos de aprendizaje al conjunto de entrenamiento; utilizar validación para seleccionar configuraciones y reservar prueba para la evaluación final.

## Alcance de esta publicación

La pretensión de este repositorio no es otra que mostrar un trabajo académico ya realizado, así como una revisión posterior de sus limitaciones. No presenta una reproducción nueva de los experimentos ni resultados de las mejoras propuestas.
