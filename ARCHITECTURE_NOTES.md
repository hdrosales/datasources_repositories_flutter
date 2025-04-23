# 🧠 Notas de Arquitectura - Flutter Clean Architecture

Este archivo contiene explicaciones clave sobre cómo y por qué se organizan las capas de *datasources* y *repositories* en este proyecto.

---

## 📚 Conceptos Clave

### 📦 Datasource
- Es la **fuente directa** de los datos.
- Puede ser una API, una base de datos local, Firebase, etc.
- Se encarga de obtener datos crudos y devolverlos procesados como entidades.

#### ✅ ¿Por qué usar una clase abstracta?
- Para definir **qué métodos** debe tener cualquier fuente de datos.
- Esto permite cambiar la fuente (ej: API → base local) sin romper el resto del código.

```dart
abstract class MoviesDatasource {
  Future<List<Movie>> getNowPlaying({int page = 1});
}
```

#### ✅ ¿Quién implementa esta clase?
- Una clase concreta como `MoviedbDatasource` que usa `dio` para hacer peticiones reales a la API.


### 🗂 Repository
- Es una **capa intermedia** entre la UI y el datasource.
- Se comunica con la UI (como un `Bloc`, `Provider`, etc.) usando las **entidades del dominio**, no modelos externos.
- Decide de qué datasource obtener los datos.

#### ✅ ¿Por qué también es abstracto?
- Define la interfaz que espera la UI o la capa de aplicación.
- Así, podemos cambiar la lógica interna (cambiar datasource, agregar cache, etc.) sin afectar quién lo usa.

```dart
abstract class MoviesRepository {
  Future<List<Movie>> getNowPlaying({int page = 1});
}
```

---

## 🔄 Flujo resumido

1. La **UI** llama al método `getNowPlaying()` del repositorio.
2. El **repositorio** usa un **datasource** para obtener los datos.
3. El **datasource** hace la petición a la API y usa un **mapper** para convertir los modelos externos a entidades del dominio.
4. Se devuelve una `List<Movie>` lista para usar en la app.

---

## 🧰 Mappers

### 🎯 ¿Por qué dos mappers?
- **Primer mapper**: JSON crudo → Modelo intermedio (`MovieFromMovieDB`)
- **Segundo mapper**: Modelo intermedio → Entidad del dominio (`Movie`)

Esto permite aislar cambios de la API externa sin que rompan toda la lógica interna de la app.

---

## ✅ Ventajas de esta arquitectura

- Separación clara de responsabilidades
- Testeable y escalable
- Fácil de mantener
- Permite múltiples orígenes de datos (APIs, local, etc.) sin modificar la UI

---

> 💡 Esta estructura está basada en los principios de Clean Architecture adaptados para apps Flutter.
