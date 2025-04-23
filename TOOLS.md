# 🛠 Herramientas útiles

## 🔁 Quicktype.io

Sirve para generar modelos Dart (u otros lenguajes) a partir de un JSON.

### ¿Cómo se usa?
1. Ir a [https://app.quicktype.io/](https://app.quicktype.io/)
2. Pegás un JSON que venga de una API.
3. Elegís el lenguaje: `Dart`.
4. Te genera una clase con `fromJson` y `toJson` automáticamente.
5. ¡Copiás y pegás en tu proyecto!

Esto lo usamos para crear el modelo `MovieFromMovieDB` a partir del JSON de TheMovieDB.

---

## 📬 Postman

Herramienta para probar APIs sin tener que armar todo el código.

### ¿Cómo lo uso?
1. Instalá Postman (es gratis).
2. Ponés la URL de la API (por ejemplo: `https://api.themoviedb.org/3/movie/now_playing?api_key=...`)
3. Hacés clic en “Send”.
4. Podés ver la respuesta JSON, copiarla y usarla en Quicktype, por ejemplo.

Postman es ideal para entender qué estructura devuelve la API antes de programar.
