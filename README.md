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

## Endpoints

- GET /clientes - Todos los clientes
- GET /clientes/:id - Cliente por ID
- POST /clientes - Crear cliente
- PUT /clientes/:id - Actualizar cliente
- DELETE /clientes/:id - Eliminar cliente
- GET /servicios - Todos los servicios
- GET /servicios/:id - Servicio por ID
- POST /servicios - Crear servicio
- PUT /servicios/:id - Actualizar servicio
- DELETE /servicios/:id - Eliminar servicio
- GET /citas - Todas las citas
- GET /citas/:id - Cita por ID
- POST /citas - Crear cita
- PUT /citas/:id - Actualizar cita
- DELETE /citas/:id - Eliminar cita
- GET /pagos - Todos los pagos
- GET /pagos/:id - Pago por ID
- POST /pagos - Registrar pago
- PUT /pagos/:id - Actualizar pago
- DELETE /pagos/:id - Eliminar pago
