# 📚 Guía Completa de Peticiones HTTP

## 🧠 Objetivo General

Comprender los métodos de petición HTTP, su propósito, cuándo y cómo se usan, además de los códigos de estado y buenas prácticas al trabajar con APIs RESTful.

---

## 🗂️ Índice

1. [¿Qué es HTTP?](#qué-es-http)
2. [Método GET](#método-get)
3. [Método POST](#método-post)
4. [Métodos PUT y PATCH](#métodos-put-y-patch)
5. [Método DELETE](#método-delete)
6. [Códigos de Estado HTTP](#códigos-de-estado-http)
7. [Headers y Autenticación](#headers-y-autenticación)
8. [Herramientas para Pruebas](#herramientas-para-pruebas)
9. [Buenas Prácticas y REST](#buenas-prácticas-y-rest)
10. [Proyecto Final](#proyecto-final)

## ¿Qué es HTTP?

HTTP (HyperText Transfer Protocol) es el protocolo que permite la comunicación entre clientes (navegadores o apps) y servidores web. Es un protocolo basado en texto plano.

### 🔄 Proceso general:

1. Cliente hace una petición HTTP (ej. desde un navegador o código).
2. El servidor procesa la petición y envía una respuesta.
3. El cliente recibe la respuesta (datos, errores, estado, etc).

### 🧱 Estructura de una petición

- Método (GET, POST, etc)
- URL
- Headers (cabeceras)
- Body (solo en métodos como POST o PUT)

### 📦 Estructura de una respuesta

- Código de estado (ej. 200 OK)
- Headers
- Cuerpo (datos en JSON, HTML, etc)

---

## Método GET

### 📌 ¿Qué hace?

Solicita datos desde el servidor.

### 📅 Cuándo usarlo

- Para obtener información sin modificar nada.
- Ej: ver usuarios, buscar productos, cargar perfiles.

### 🧪 Ejemplo

- Usando `.then`

```js
fetch("https://api.example.com/users")
  .then((response) => response.json())
  .then((data) => console.log(data));
```

- Usando `async/await`

```js
const getUsers = async () => {
  try {
    const response = await fetch("https://api.example.com/users");
    const data = await response.json();
    console.log(data);
  } catch (error) {
    console.error("Error:", error);
  }
};

getUsers();
```

### 🧠 ¿Por qué usar `async/await`?

| ✅ Ventaja              | 💡 Explicación                                                      |
| ----------------------- | ------------------------------------------------------------------- |
| Más legible             | El flujo de código se parece más al código síncrono tradicional     |
| Manejo de errores claro | Usas `try/catch`, como en código común                              |
| Escalable               | Más fácil de mantener en funciones grandes o con múltiples `await`s |
| Depuración más sencilla | Los errores se ven más claros en consola                            |

## ⚠️ Cuidados

- Siempre indicar el Content-Type.
- Validar los datos antes de enviarlos.

---

## Método POST

### 📌 ¿Qué hace?

Envía datos al servidor para crear un nuevo recurso.

### 📅 Cuándo usarlo

- Crear un usuario, enviar un comentario, registrar un producto.

🧪 Ejemplo

```js
fetch("https://api.example.com/users", {
  method: "POST",
  headers: {
    "Content-Type": "application/json",
  },
  body: JSON.stringify({
    name: "Juan",
    email: "juan@example.com",
  }),
});
```

### ⚠️ Cuidados

- Siempre indicar el Content-Type.
- Validar los datos antes de enviarlos.

---

## Métodos PUT y PATCH

### 📌 PUT

Reemplaza todo el recurso.

### 📌 PATCH

Modifica una parte del recurso.

### 📅 Cuándo usar

- Para editar un perfil, cambiar nombre, email, estado, etc.

### 🧪 Ejemplo PUT

```js
fetch("https://api.example.com/users/1", {
  method: "PUT",
  headers: {
    "Content-Type": "application/json",
  },
  body: JSON.stringify({
    name: "Pedro",
    email: "pedro@example.com",
  }),
});
```

### 🧪 Ejemplo PATCH

```js
fetch("https://api.example.com/users/1", {
  method: "PATCH",
  headers: {
    "Content-Type": "application/json",
  },
  body: JSON.stringify({ email: "nuevo@example.com" }),
});
```

---

## Método DELETE

### 📌 ¿Qué hace?

Elimina un recurso del servidor.

### 📅 Cuándo usarlo

Para eliminar usuarios, publicaciones, productos.

### 🧪 Ejemplo

```js
fetch("https://api.example.com/users/1", {
  method: "DELETE",
});
```

---

## 🧾 Headers y Autenticación

- `Content-Type:` tipo de datos (application/json)
- `Accept:` formato que acepta el cliente
- `Authorization:` autenticación (token, etc)

### 🔐 Autenticación con token.

```js
fetch("https://api.example.com/profile", {
  headers: {
    Authorization: "Bearer eyJhbGciOiJIUzI1NiIsInR5cCI6IkpXVCJ9...",
  },
});
```

---

## Herramientas para Pruebas

### 🧰 Recomendadas

- Postman: muy visual y fácil de usar.
- Insomnia: alternativa potente y ligera.
- DevTools (Red): para ver tráfico de red directamente.

### 🧪 Actividad sugerida

- Probar todos los métodos con una API de prueba o local.

---

## Buenas Prácticas y REST

### ✅ Buenas prácticas

- Usar el método correcto según la acción.
- No usar GET para enviar datos que cambian el servidor.
- Validar y sanitizar datos del usuario.
- Mostrar mensajes claros si ocurre un error.
- No exponer tokens ni datos sensibles en URLs.

### 🧭 RESTful API (principios)

- Usar rutas claras con sustantivos: /users, /products
- Evitar verbos en las rutas: ❌ /getUsers
- Métodos HTTP representan acciones: GET, POST, PUT, DELETE

## 🧪 Proyecto Final: CRUD de Usuarios

### 🎯 Objetivo

Crear una aplicación web básica en HTML y JavaScript que permita realizar operaciones **CRUD (Create, Read, Update, Delete)** sobre usuarios utilizando peticiones HTTP. Puedes usar una API local simulada como [JSON Server](https://github.com/typicode/json-server).

---

### 📁 Funcionalidades

#### 📄 GET – Mostrar lista de usuarios

- Obtener todos los usuarios desde la API.
- Renderizarlos en una tabla o lista.

#### ➕ POST – Agregar nuevo usuario

- Formulario para crear un nuevo usuario.
- Enviar datos a la API con método `POST`.

#### ✏️ PUT / PATCH – Editar información de usuario

- Permitir editar un usuario desde la lista.
- Usar `PUT` o `PATCH` para enviar la actualización.

#### 🗑️ DELETE – Eliminar usuario

- Botón para eliminar un usuario.
- Confirmar y hacer la petición `DELETE` a la API.

---

### 💡 Sugerencias adicionales

- Usa `fetch()` con `async/await` para mayor claridad.
- Muestr

