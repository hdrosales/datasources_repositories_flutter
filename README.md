### README.md

# 🎬 Flutter Movie App - Clean Architecture Example

Este proyecto es un ejemplo de cómo estructurar una app Flutter consumiendo la API de TheMovieDB siguiendo los principios de **arquitectura limpia**.

---

## 🚀 Funcionalidad

- Consulta de películas en cartelera desde [TheMovieDB API](https://developers.themoviedb.org/3)
- Separación clara en capas: datasource, repository, entidad, presentación
- Uso de `dio` para peticiones HTTP
- Conversión del JSON externo a entidades del dominio

---

## 🧠 Arquitectura Limpia - Flujo de datos

| ETAPA | RESPONSABLE | DESCRIPCIÓN | EJEMPLO |
|-------|-------------|-------------|---------|
| **1. Petición HTTP** | `Datasource` | Hace la solicitud a la API externa | `dio.get('/movie/now_playing')` |
| **2. Datos JSON crudos** | - | Respuesta sin tipado (formato original de la API) | `Map<String, dynamic>` |
| **3. Modelo generado (mapper primario)** | `fromJson()` en `MovieFromMovieDB` | Transforma el JSON crudo a un modelo estructurado | `MovieFromMovieDB.fromJson(json)` |
| **4. Mapeo a entidad del dominio (mapper secundario)** | `Datasource` + `MovieMapper` | Convierte `MovieFromMovieDB` en la entidad de la app `Movie` | `MovieMapper.movieDBToEntity(movieDb)` |
| **5. Resultado final: Entidades** | `Datasource` retorna `List<Movie>` | Datos listos para usarse en la app | `[Movie, Movie, ...]` |
| **6. Repository (capa de dominio)** | `MoviesRepository` | Recibe las entidades procesadas | `getNowPlaying()` |
| **7. UI / UseCase** | `Widget`, Provider, Bloc, etc. | Consume el repositorio para mostrar datos | `await moviesRepository.getNowPlaying()` |

---

## 📂 Estructura del proyecto

```plaintext
/lib
├── domain
│   ├── entities/         → Movie.dart (entidad del dominio)
│   ├── datasources/      → MoviesDatasource.dart (abstracta)
│   └── repositories/     → MoviesRepository.dart (abstracta)
├── infrastructure
│   ├── datasources/      → MoviedbDatasource.dart (implementa el datasource)
│   ├── models/           → movie_from_moviedb.dart (modelo generado desde JSON)
│   └── mappers/          → movie_mapper.dart (convierte modelo externo → entidad)
```

---

## ✅ Beneficios de esta arquitectura

- Código modular y testable ✅
- Desacoplamiento entre la lógica y los datos externos ✅
- Escalable para nuevos orígenes de datos ✅
- Fácil de mantener y entender ✅

---

## ⚠️ Importante

Este proyecto **omite la clave de API** por seguridad. Asegurate de crear un archivo `.env` o similar para guardarla, o usar variables de entorno.

---

## 📜 Licencia

Este código está hecho con fines educativos y es de uso libre para mejorar tu aprendizaje en Flutter. ¡Forkealo, experimentá, y construí el tuyo!
