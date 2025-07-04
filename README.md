# 🌐 Tutorial: Cómo usar `json-server` en Ubuntu y Windows

`json-server` te permite crear una **API REST falsa** usando solo un archivo JSON. Es perfecto para probar o desarrollar aplicaciones frontend sin necesidad de un backend real.

---

## ⚙️ Requisitos previos

Antes de comenzar, asegúrate de tener instalado:

- **Node.js** y **npm**  
  Verifica con:

```bash
node -v
npm -v
```

## 🐧 Instalación en Ubuntu (Linux)

### 1. Instalar Node.js y npm

```bash
sudo apt update
sudo apt install nodejs npm -y
```

Opcional: para versiones más recientes, puedes instalar desde NodeSource.

### 2. Instalar json-server globalmente

```
npm install -g json-server
```

### 3. Crear y editar archivo db.json

```bash
mkdir api-fake
cd api-fake
nano db.json
```

- Contenido de ejemplo

```json
{
  "usuarios": [
    { "id": 1, "nombre": "Juan", "email": "juan@mail.com" },
    { "id": 2, "nombre": "Ana", "email": "ana@mail.com" }
  ]
}
```

### 4. Ejecutar el servidor

```bash
cd C:\fake-api
json-server --watch db.json --port 3000
```

Abre `http://localhost:3000/productos` en tu navegador.

### 🧪 Prueba rápida
Puedes hacer peticiones desde navegador, Postman o JavaScript:

```js
fetch("http://localhost:3000/productos")
  .then((res) => res.json())
  .then((data) => console.log(data));
```

---

## 🧠 Tips útiles

* Cambiar puerto:
```js
json-server --watch db.json --port 4000
```

* Filtros y ordenamientos:
```js
/usuarios?_page=1&_limit=2
/productos?_sort=precio&_order=desc
```

* Rutas personalizadas (usando routes.json):
```json
{
  "/api/*": "/$1"
}
```