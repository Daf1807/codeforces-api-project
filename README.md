# Codeforces Contest & User Data Analysis (2024)

Este proyecto consiste en la extracción, limpieza y análisis de datos de competencias y usuarios de la plataforma [Codeforces](https://codeforces.com/) utilizando su API oficial. Se realizó en el marco de un curso universitario de Data Science durante el segundo semestre de 2024.

## Objetivo

Analizar datos de competencias realizadas entre **julio y diciembre de 2024**, enfocándonos en los concursos que contienen los términos `"Hello"`, `"Round"` y `"Good Bye"` en sus títulos. Se busca:

- Comprender patrones de participación y desempeño de usuarios.
- Estudiar el tiempo de respuesta y dificultad de los problemas.
- Explorar la relación entre el nivel del usuario y sus resultados en competencias.

## Dataset

Los datos fueron recolectados a través de los siguientes endpoints de la [API de Codeforces](https://codeforces.com/apiHelp):

- `contest.list`: Lista de concursos disponibles.
- `contest.standings`: Detalles de cada concurso y sus problemas.
- `contest.status`: Envíos realizados por usuarios.
- `contest.ratingChanges`: Cambios de rating por concurso.
- `user.ratedList`: Información de usuarios participantes.

Cada concurso se almacenó en carpetas individuales, con archivos `.csv` que contienen la información extraída de los endpoints.

### Variables Derivadas

Se generaron variables para el análisis, como:

- `finished_n`: Indicador de si el usuario resolvió el problema n.
- `n_language`: Lenguaje de programación usado para el problema n.
- `relative_time_n`: Tiempo transcurrido desde el inicio del concurso hasta el envío del problema n.
- `time_to_answer_n`: Tiempo entre respuestas consecutivas.
- `rating_n`: Dificultad del problema n.
- `rating_achieved`: Suma del rating de los problemas resueltos por el usuario.

## Data Wrangling

- Conversión de timestamps.
- Manejo de campos anidados o faltantes.
- Normalización y creación de variables derivadas.
- Unificación de datasets por usuario y concurso.

## Visualizaciones

- Histograma del tiempo de envío (`submission times`).
- Densidad kernel del `maximum rating` por usuario.
- Boxplots: `Lenguaje de programación vs. tiempo de respuesta`.
- Binscatter: `Rating vs. tiempo de respuesta`.
- Regresión lineal: `Rating actual vs. rating alcanzado`.

Cada figura fue acompañada por una interpretación clara.

## Análisis Causal

- Se explora la relación entre el nivel previo de rating de los usuarios y su rendimiento en las competencias.
- Se aplicó una regresión lineal básica para evaluar esta relación.

## Autores

- Dafne Andrea Mamani Vila  
  *Estudiante de Economía – Universidad del Pacífico*
