<div align="center">
  <h1 align="center">
    📊 Análisis de Sentimiento de la Película "Gladiator 2"
  </h1>
  <p align="center">
    <strong>Un proyecto NLP de extremo a extremo para extraer y clasificar la opinión pública sobre la película <em>Gladiator 2</em>, utilizando un corpus sintético y modelos de Machine Learning.</strong>
  </p>
</div>

<p align="center">
  <img src="https://img.shields.io/badge/Python-3776AB?style=for-the-badge&logo=python&logoColor=white" alt="Python">
  <img src="https://img.shields.io/badge/spaCy-09A3D5?style=for-the-badge&logo=spacy&logoColor=white" alt="spaCy">
  <img src="https://img.shields.io/badge/scikit--learn-F7931E?style=for-the-badge&logo=scikit-learn&logoColor=white" alt="scikit-learn">
  <img src="https://img.shields.io/badge/NLTK-3776AB?style=for-the-badge" alt="NLTK">
  <img src="https://img.shields.io/badge/Matplotlib-010101?style=for-the-badge&logo=matplotlib&logoColor=white" alt="Matplotlib">
</p>

---

## 📜 Descripción del Proyecto

Este proyecto presenta un sistema completo de **extracción de información y análisis de sentimientos** enfocado en el sector audiovisual, tomando como caso de estudio la película **Gladiator 2**.

El objetivo es analizar un conjunto de reseñas para identificar y clasificar las opiniones del público en relación con los siguientes aspectos clave:

-   🗣️ **Opinión general** sobre la película.
-   ✍️ **Opinión sobre el guion** y la trama.
-   🎭 **Opinión sobre los actores** y sus interpretaciones.
-   🎬 **Opinión sobre la producción** (dirección, efectos, música, etc.).

A partir de las reseñas, se extraen entidades relevantes que se clasifican automáticamente según el sentimiento asociado (Positivo, Negativo o Neutro).

---

## ⚙️ Metodología y Pipeline

El proyecto se ha desarrollado siguiendo un pipeline de NLP bien definido:

### 1. Creación del Corpus (Datos Sintéticos)

Debido a las restricciones de las APIs de plataformas como *IMDB* o *FilmAffinity*, el corpus se ha generado de forma sintética mediante **Prompt Engineering**.

> **Prompt utilizado para generar datos de análisis:**
> ```
> “Actúa como un crítico especialista en cine. Accede a la página IMDB y analiza las reseñas asociadas a la película Gladiator II. Ahora ofréceme, en formato tabla, 40 reseñas inventadas por ti que reflejen de manera fiel el sentimiento de las reseñas analizadas.”
> ```

Se utilizó una técnica similar para el corpus de entrenamiento, pidiendo además la clasificación del sentimiento (POS, NEG, NEU) para agilizar el etiquetado de los datos.

### 2. Preprocesamiento de Datos

Los datos se han limpiado para eliminar ruido, aplicando las siguientes técnicas:
-   Eliminación de emails, nombres de usuario y emoticonos.
-   Conversión a minúsculas.
-   Tokenización de palabras con `word_tokenize` de **NLTK**.
-   **No se han eliminado stopwords**, ya que son cruciales para el análisis de sentimiento.

### 3. Extracción de Entidades (NER)

Para la extracción de las entidades relevantes, se utilizó el modelo `es_core_news_lg` de **spaCy**, personalizado con un `EntityRuler` a partir de un diccionario definido a medida.

> [!NOTE]
> **Definición del Diccionario de Entidades**
> El diccionario se ha elaborado basándose en el marco semántico del mundo cinematográfico y la frecuencia léxica de los términos en el corpus.
>
> -   **Entidad: Gladiator II**
>     -   **Variantes:** `secuela`, `continuación`, `película`
>     -   **Tipo Semántico:** PELÍCULA | **Etiqueta:** `GENERAL`
>
> -   **Entidad: Paul Mescal, Pedro Pascal, Denzel Washington**
>     -   **Tipo Semántico:** PERSONA | **Etiqueta:** `ACTOR`
>
> -   **Entidad: Producción**
>     -   **Variantes:** `Ridley Scott`, `dirección`, `producción`, `visual`, `escenas`, `efectos especiales`, `coreografías`, `música`, `batallas`
>     -   **Tipo Semántico:** OBJETO FÍLMICO | **Etiqueta:** `PRODUCCIÓN`
>
> -   **Entidad: Guion**
>     -   **Variantes:** `trama`, `historia`, `narrativa`, `guión`, `personajes`, `desarrollo`
>     -   **Tipo Semántico:** OBJETO ESCRITO | **Etiqueta:** `GUION`

### 4. Entrenamiento del Modelo de Sentimiento

Para la clasificación de sentimientos, se evaluaron varios modelos de la librería **Scikit-learn**:
-   Regresión Logística (`LogisticRegression`)
-   Naive Bayes (`MultinomialNB`)
-   Support Vector Classifier (`SVC`)
-   Linear Support Vector Classifier (`LinearSVC`)
-   Árboles de Decisión (`DecisionTreeClassifier`)

El modelo **SVC** fue finalmente seleccionado para el procesamiento final.

### 5. Análisis y Visualización de Resultados

Los textos extraídos para cada etiqueta se procesaron con el modelo SVC entrenado. Los resultados se graficaron utilizando la librería **Matplotlib** para su posterior análisis e interpretación.

---

## 👥 Perfiles Profesionales Requeridos

Un proyecto de estas características requiere un equipo multidisciplinar:
-   **Experto en PLN:** Para reconocer patrones, definir marcos semánticos y crear diccionarios de extracción.
-   **Anotadores de Datos:** Para desarrollar corpus de entrenamiento rigurosos y exactos.
-   **Científico de Datos:** Para el modelado, escalamiento, estandarización y evaluación de los modelos.
-   **Analista de Datos:** Para la correcta interpretación de los resultados y la generación de insights.

