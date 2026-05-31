# Sistema de Lavado de Autos - Backend SQLite

## Informacion del Proyecto

| Campo        | Detalle                                 |
|--------------|-----------------------------------------|
| Materia      | Aplicaciones con Base de Datos          |
| Profesor     | Jesus Alejandro Flores Hernandez        |
| Alumno       | Alejandro del Jesus Diaz Lopez          |
| Matricula    | 191087                                  |
| Carrera      | Ingenieria en Sistemas Computacionales  |
| Rol          | Desarrollador Backend                   |
| Fecha        | Mayo 2026                               |

## Descripcion

API REST para administrar un negocio de lavado de autos.
Construida con Node.js + Express + Better-SQLite3 usando modulos ES6 y patron DAO.

## Como ejecutar el proyecto

1. Clonar el repositorio: git clone https://github.com/alex1999aj70/lavado-sqlite.git
2. Instalar dependencias: npm install
3. Crear archivo .env con: PORT=3000, DB_NAME=lavado.db, HOST=localhost
4. Crear la base de datos: npm run seed
5. Iniciar el servidor: npm run dev

El servidor arranca en http://localhost:3000

## Estructura del proyecto

    lavado-sqlite/
    ├── server.js
    ├── controller.db.js
    ├── package.json
    ├── .env
    ├── .gitignore
    ├── README.md
    └── src/
        ├── seed.js
        ├── models/
        │   ├── model.cliente.js
        │   ├── model.servicio.js
        │   ├── model.cita.js
        │   └── model.pago.js
        └── routes/
            └── routes.js

## Base de datos

La base de datos es SQLite y se guarda en el archivo lavado.db.

### Sentencias SQL

```sql
CREATE TABLE IF NOT EXISTS ROL (
  idRol INTEGER PRIMARY KEY AUTOINCREMENT,
  nombre_rol TEXT NOT NULL
);

CREATE TABLE IF NOT EXISTS USUARIO (
  idUsuario INTEGER PRIMARY KEY AUTOINCREMENT,
  nombre_usuario TEXT NOT NULL,
  contrasena TEXT NOT NULL,
  idRol INTEGER NOT NULL,
  FOREIGN KEY (idRol) REFERENCES ROL(idRol)
);

CREATE TABLE IF NOT EXISTS CLIENTE (
  idCliente INTEGER PRIMARY KEY AUTOINCREMENT,
  nombre TEXT NOT NULL,
  telefono TEXT NOT NULL,
  direccion TEXT
);

CREATE TABLE IF NOT EXISTS CATEGORIA_SERVICIO (
  idCategoria INTEGER PRIMARY KEY AUTOINCREMENT,
  nombre_categoria TEXT NOT NULL
);

CREATE TABLE IF NOT EXISTS SERVICIO (
  idServicio INTEGER PRIMARY KEY AUTOINCREMENT,
  nombre_servicio TEXT NOT NULL,
  descripcion TEXT,
  precio_base REAL NOT NULL,
  idCategoria INTEGER NOT NULL,
  FOREIGN KEY (idCategoria) REFERENCES CATEGORIA_SERVICIO(idCategoria)
);

CREATE TABLE IF NOT EXISTS CITA (
  idCita INTEGER PRIMARY KEY AUTOINCREMENT,
  fecha_hora TEXT NOT NULL,
  estado TEXT DEFAULT 'Pendiente',
  idCliente INTEGER NOT NULL,
  idUsuario INTEGER NOT NULL,
  FOREIGN KEY (idCliente) REFERENCES CLIENTE(idCliente),
  FOREIGN KEY (idUsuario) REFERENCES USUARIO(idUsuario)
);

CREATE TABLE IF NOT EXISTS DETALLE_CITA (
  idCita INTEGER NOT NULL,
  idServicio INTEGER NOT NULL,
  cantidad INTEGER DEFAULT 1,
  precio_aplicado REAL NOT NULL,
  PRIMARY KEY (idCita, idServicio),
  FOREIGN KEY (idCita) REFERENCES CITA(idCita),
  FOREIGN KEY (idServicio) REFERENCES SERVICIO(idServicio)
);

CREATE TABLE IF NOT EXISTS PAGO (
  idPago INTEGER PRIMARY KEY AUTOINCREMENT,
  fecha_pago TEXT NOT NULL,
  monto_total REAL NOT NULL,
  metodo_pago TEXT NOT NULL,
  idCita INTEGER NOT NULL,
  FOREIGN KEY (idCita) REFERENCES CITA(idCita)
);
```

### Datos de ejemplo

El script npm run seed inserta:
- 3 roles: Administrador, Empleado, Cajero
- 4 usuarios
- 5 clientes
- 4 categorias de servicio
- 7 servicios
- 5 citas
- 5 detalles de cita
- 2 pagos

## Endpoints

Base URL: http://localhost:3000

| Metodo | Endpoint        | Descripcion            |
|--------|-----------------|------------------------|
| GET    | /clientes       | Todos los clientes     |
| GET    | /clientes/:id   | Cliente por ID         |
| POST   | /clientes       | Crear cliente          |
| PUT    | /clientes/:id   | Actualizar cliente     |
| DELETE | /clientes/:id   | Eliminar cliente       |
| GET    | /servicios      | Todos los servicios    |
| GET    | /servicios/:id  | Servicio por ID        |
| POST   | /servicios      | Crear servicio         |
| PUT    | /servicios/:id  | Actualizar servicio    |
| DELETE | /servicios/:id  | Eliminar servicio      |
| GET    | /citas          | Todas las citas        |
| GET    | /citas/:id      | Cita por ID            |
| POST   | /citas          | Crear cita             |
| PUT    | /citas/:id      | Actualizar cita        |
| DELETE | /citas/:id      | Eliminar cita          |
| GET    | /pagos          | Todos los pagos        |
| GET    | /pagos/:id      | Pago por ID            |
| POST   | /pagos          | Registrar pago         |
| PUT    | /pagos/:id      | Actualizar pago        |
| DELETE | /pagos/:id      | Eliminar pago          |
