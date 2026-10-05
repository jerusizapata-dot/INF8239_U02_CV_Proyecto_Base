\# Model Card - Fashion-MNIST CNN



\## Modelo y versión



Proyecto INF-8239 U02.LAB07. Se comparan un baseline Dense y una CNN sobre la misma partición de Fashion-MNIST.



\- Dense baseline: Flatten + Dense(64, ReLU) + salida de 10 clases.

\- CNN: dos bloques Conv2D + MaxPooling2D, GlobalAveragePooling2D, Dropout(0.25) y salida de 10 clases.

\- Modelo CNN: `models/best\_cnn.keras`.

\- Semilla: 42.



\## Uso previsto



Clasificación experimental de imágenes de Fashion-MNIST con finalidad académica y de evaluación reproducible de modelos de visión computacional.



\## Usos fuera de alcance



No utilizar este modelo para imágenes reales fuera de Fashion-MNIST ni para decisiones de alto impacto. El rendimiento observado no garantiza generalización a otros dominios.



\## Dataset y particiones



Se utilizó Fashion-MNIST.



\- Entrenamiento: 54,000 imágenes.

\- Validación: 6,000 imágenes.

\- Prueba: 10,000 imágenes.

\- El conjunto de prueba contiene 1,000 imágenes por clase.



\## Preprocesamiento



Las imágenes de 28x28 píxeles se convierten a `float32` y se normalizan dividiendo entre 255. Se agrega un canal para obtener la forma `(n, 28, 28, 1)`.



La misma partición y el mismo preprocesamiento se utilizaron para comparar ambos modelos.



\## Métricas globales y por clase



\### F1 macro



| Modelo | F1 macro |

|---|---:|

| Dense baseline | 0.8637 |

| CNN | 0.7900 |



El modelo Dense obtuvo un F1 macro superior al CNN por aproximadamente 0.0736 puntos.



\### CNN por clase



| Clase | Precision | Recall | F1 |

|---:|---:|---:|---:|

| 0 | 0.645 | 0.806 | 0.717 |

| 1 | 0.990 | 0.931 | 0.960 |

| 2 | 0.705 | 0.653 | 0.678 |

| 3 | 0.754 | 0.844 | 0.796 |

| 4 | 0.660 | 0.667 | 0.664 |

| 5 | 0.950 | 0.883 | 0.916 |

| 6 | 0.508 | 0.370 | 0.428 |

| 7 | 0.854 | 0.953 | 0.901 |

| 8 | 0.917 | 0.937 | 0.927 |

| 9 | 0.934 | 0.896 | 0.915 |



La clase 6 fue la más difícil para el CNN, con F1 de 0.428 y recall de 0.370.



Sus principales confusiones fueron:



\- Clase 0: 273 ejemplos.

\- Clase 4: 134 ejemplos.

\- Clase 2: 125 ejemplos.



\## Comparación de costo



\- Hardware: CPU en Windows; no se utilizó GPU.

\- Parámetros Dense: 50,890.

\- Parámetros CNN: 19,466.

\- Tiempo de entrenamiento Dense: 9.75 s.

\- Tiempo de entrenamiento CNN: 79.01 s.

\- Inferencia Dense: 0.0569 ms por imagen.

\- Inferencia CNN: 0.1212 ms por imagen.



La CNN utiliza aproximadamente 62% menos parámetros que el baseline Dense, pero en esta ejecución tuvo mayor costo de entrenamiento e inferencia y obtuvo menor F1 macro.



\## Limitaciones y riesgos



El resultado corresponde exclusivamente al benchmark Fashion-MNIST y a la partición utilizada.



La clase 6 presenta dificultades importantes y se confunde principalmente con las clases 0, 4 y 2.



No se debe asumir que la CNN tendrá mejor rendimiento en otros datasets.



\## Supervisión y monitoreo



Antes de utilizar el modelo en otro dominio se debe verificar nuevamente el rendimiento con datos representativos, revisar métricas por clase y analizar errores.



Se recomienda mantener seguimiento de F1 macro, métricas por clase, matriz de confusión, costo computacional y cambios en la distribución de los datos.



\## Resultado principal



En esta ejecución, el baseline Dense obtuvo mejor F1 macro que la CNN: 0.8637 frente a 0.7900.



\## Evidencia predictiva



La CNN alcanzó F1 macro de 0.7900. La clase 6 fue la más difícil, con F1 de 0.428 y recall de 0.370.



\## Clase más difícil



La clase 6, debido a su bajo recall y F1. Sus principales confusiones fueron las clases 0, 4 y 2.



\## Costo comparado



La CNN utilizó menos parámetros, pero requirió más tiempo de entrenamiento y presentó mayor tiempo de inferencia por imagen.



\## ¿La mejora justifica el costo?



No en esta ejecución. La CNN no produjo una mejora predictiva frente al baseline Dense y además presentó mayor costo temporal.



\## Limitación del benchmark



Fashion-MNIST es un benchmark controlado de imágenes pequeñas y no representa necesariamente imágenes reales de otros dominios.



\## Decisión antes de usar otro dominio



No trasladar directamente el modelo. Primero se debe validar con datos representativos del nuevo dominio, comparar nuevamente contra un baseline y revisar el rendimiento por clase y los errores.

