Comparación de LDA y QDA sobre el Wine Dataset
Proyecto de investigación e implementación que compara el Análisis Discriminante Lineal
(LDA) y el Análisis Discriminante Cuadrático (QDA) sobre el conjunto de datos Wine
(UCI Machine Learning Repository), utilizado sin ningún tratamiento o limpieza previa.

Contenido del repositorio

├── LDA_vs_QDA_Wine.ipynb   # Cuaderno de Google Colab con el análisis completo y comentado
├── Informe_LDA_QDA.pdf     # Informe técnico (fundamentos teóricos de LDA y QDA)
├── README.md               # Este archivo
└── data/                   # (opcional) copia local del dataset — ver sección "Obtener el dataset"
Obtener el dataset
El conjunto de datos Wine se utiliza sin tratamiento previo y se carga directamente desde
scikit-learn, por lo que no es necesario descargar ningún archivo para ejecutar el
notebook:

from sklearn.datasets import load_wine
wine = load_wine()
Este es exactamente el mismo dataset publicado en el UCI Machine Learning Repository
(https://archive.ics.uci.edu/dataset/109/wine).
Si se desea trabajar con el archivo CSV de forma local, puede generarse a partir del mismo
objeto con:

import pandas as pd
df = pd.DataFrame(wine.data, columns=wine.feature_names)
df["target"] = wine.target
df["target_name"] = df["target"].map(dict(enumerate(wine.target_names)))
df.to_csv("data/wine.csv", index=False)
Cómo ejecutar el proyecto
Abrir LDA_vs_QDA_Wine.ipynb en Google Colab
(Archivo → Subir cuaderno, o directamente desde GitHub con
Archivo → Abrir cuaderno → GitHub pegando la URL de este repositorio).

Ejecutar las celdas en orden (Entorno de ejecución → Ejecutar todas). No requiere
instalar dependencias adicionales: todas las librerías (scikit-learn, pandas, numpy,
matplotlib, seaborn) están preinstaladas en Colab.

El cuaderno recorre, en orden, las siguientes secciones: descripción del dataset,
exploración de datos, visualización, preparación de datos, implementación de LDA,
implementación de QDA, comparación de modelos, fronteras de decisión y conclusiones.

Resumen de hallazgos principales
El Wine Dataset contiene 178 observaciones, 13 variables predictoras numéricas y 3
clases (cultivares de uva), sin valores faltantes.

Con las 13 variables, LDA alcanza un accuracy de ≈ 0.98 y QDA alcanza un
accuracy de 1.0 sobre el conjunto de prueba (30 %, división estratificada).

Al reducir el problema a dos variables (flavanoids y proline) para visualizar las
fronteras de decisión, la diferencia entre ambos modelos se hace más evidente: LDA obtiene
≈ 0.91 de exactitud con una frontera lineal, mientras que QDA obtiene ≈ 0.96 con una
frontera cuadrática que se ajusta mejor a la forma real de cada clase.

La diferencia de desempeño se explica por el supuesto de homocedasticidad (igualdad de
matrices de covarianza entre clases) que asume LDA y que QDA relaja: en este dataset, las
clases presentan estructuras de covarianza ligeramente distintas, lo que favorece a QDA.

Dado el tamaño moderado del dataset, se recomienda validar estos resultados con
k-fold cross-validation antes de generalizar las conclusiones.

La validación cruzada con 5 folds confirma que QDA (accuracy ≈ 0.974) supera
consistentemente a LDA (accuracy ≈ 0.967), respaldando los resultados obtenidos.
