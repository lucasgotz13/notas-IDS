# Plan - Sistema de Gestión Psiquiátrica

## 📊 Diagrama ER

### Entidades Principales

#### `users`
| Campo | Tipo | Descripción |
|-------|------|-------------|
| id | PK | Identificador único |
| email | UNIQUE | Correo electrónico |
| password_hash | string | Hash de contraseña |
| role | enum | admin \| psychiatrist \| patient \| developer |

#### `people`
| Campo | Tipo | Descripción |
|-------|------|-------------|
| id | PK | Identificador único |
| user_id | FK → users.id (UNIQUE) | Relación 1:1 con usuario |
| first_name | string | Nombre |
| last_name | string | Apellido |
| dni | string | Documento de identidad |
| phone | string | Teléfono |
| address | string | Dirección |

#### `psychiatrists`
| Campo | Tipo | Descripción |
|-------|------|-------------|
| id | PK | Identificador único |
| person_id | FK → people.id (UNIQUE) | Relación 1:1 con persona |
| license_number | string | Número de matrícula |
| specialty | string | Especialidad |
| status | string | Estado del profesional |

#### `patients`
| Campo | Tipo | Descripción |
|-------|------|-------------|
| id | PK | Identificador único |
| person_id | FK → people.id (UNIQUE) | Relación 1:1 con persona |
| insurance_provider | string | Obra social/Prepaga |
| member_number | string | Número de afiliado |

#### `sessions`
| Campo | Tipo | Descripción |
|-------|------|-------------|
| id | PK | Identificador único |
| patient_id | FK → patients.id (INDEX) | Paciente |
| psychiatrist_id | FK → psychiatrists.id (INDEX) | Psiquiatra |
| session_date | datetime | Fecha de la sesión |
| duration_minutes | int | Duración en minutos |
| notes | text | Historia clínica (texto libre) |
| created_at | timestamp | Fecha de creación |
| updated_at | timestamp | Fecha de actualización |

---

## 📖 User Stories

### 👨‍⚕️ Psiquiatra

1. Quiero poder subir las historias clínicas de mis pacientes a la plataforma
2. Quiero poder ver las historias clínicas de mis pacientes en la página
3. Quiero poder ver una tabla con todas las historias clínicas que hice
   - En esta, quiero poder hacer click para ver esta historia clínica específica y hacer diferentes cosas como editarla o borrarla
   - Quiero también poder filtrar por diferentes cosas (fecha, discapacidad, copago, nombre, etc)
   - Quiero también poder ordenar por diferentes cosas (alfabéticamente, más/menos reciente, etc)
4. Quiero tener una tabla en relación a los honorarios. Quiero que diga por cada bimestre cuántas sesiones dí y en relación a esto cuánto debería cobrar por el bimestre
5. Quiero tener un apartado de "tickets" para poder pedir ayuda al área administrativa para temas administrativos ó de funcionamiento de la página
6. Quiero poder agregar mis consultorios

### 🧑 Paciente

1. Quiero poder ver mis datos
2. Quiero poder ver quién fue el psiquiatra de mi última sesión
3. Quiero poder solicitar un cambio de psiquiatra en caso de ser necesario
   - Quiero solicitar un psiquiatra de la zona que yo quiera

### 🏢 Administrativo

1. Quiero poder acceder a una tabla perteneciente a un psiquiatra y que contenga:
   - **Columnas:** nombre_paciente, fecha_sesion, honorario, condicion?
   - **Filas:** Sesiones hechas por el psiquiatra
2. A partir de esta tabla, quiero que se pueda generar un excel para descargar con un botón
3. Quiero poder crear, modificar y/o borrar los perfiles tanto de los pacientes como de los psiquiatras, pero que **no se borren las sesiones** al borrar alguno de estos

---

## 🔌 Endpoints API

> **Base URL:** `/api/v1`

### 🔐 Auth
> Better-Auth maneja esto, pero documentamos la interfaz

| Método | Endpoint | Descripción |
|--------|----------|-------------|
| POST | `/auth/sign-in` | Login |
| POST | `/auth/sign-up` | Registro |
| POST | `/auth/sign-out` | Logout |
| GET | `/auth/session` | Ver sesión actual |

### 👤 Users (Admin & Developer only)

| Método | Endpoint | Descripción | RBAC |
|--------|----------|-------------|------|
| GET | `/users` | Listar usuarios (paginado) | admin, developer |
| GET | `/users/:id` | Obtener usuario por ID | admin, developer, own user |
| POST | `/users` | Crear usuario | admin, developer |
| PATCH | `/users/:id` | Actualizar usuario | admin, developer, own user |
| DELETE | `/users/:id` | Eliminar usuario | admin, developer |
| PATCH | `/users/:id/role` | Cambiar rol de usuario | admin, developer |

**Query params para GET /users:**
- `?page=1&pageSize=20`
- `?role=psychiatrist`
- `?search=john@email.com`

### 🧑 People (Datos personales)

| Método | Endpoint | Descripción | RBAC |
|--------|----------|-------------|------|
| GET | `/people` | Listar personas | admin, developer |
| GET | `/people/:id` | Obtener persona | admin, developer, linked user |
| POST | `/people` | Crear persona (registro inicial) | admin, developer |
| PATCH | `/people/:id` | Actualizar datos personales | admin, developer, linked user |
| GET | `/people/me` | Obtener mi perfil | any authenticated |

### 🩺 Psychiatrists

| Método | Endpoint | Descripción | RBAC |
|--------|----------|-------------|------|
| GET | `/psychiatrists` | Listar psiquiatras | any authenticated |
| GET | `/psychiatrists/:id` | Obtener psiquiatra | any authenticated |
| POST | `/psychiatrists` | Crear perfil de psiquiatra | admin, developer |
| PATCH | `/psychiatrists/:id` | Actualizar psiquiatra | admin, developer, own profile |
| DELETE | `/psychiatrists/:id` | Eliminar psiquiatra | admin, developer |
| GET | `/psychiatrists/:id/sessions` | Sesiones del psiquiatra | admin, developer, own profile |
| GET | `/psychiatrists/:id/patients` | Pacientes asignados | admin, developer, own profile |

### 🏥 Patients

| Método | Endpoint | Descripción | RBAC |
|--------|----------|-------------|------|
| GET | `/patients` | Listar pacientes | admin, developer, psychiatrist |
| GET | `/patients/:id` | Obtener paciente | admin, developer, psychiatrist assigned |
| POST | `/patients` | Crear paciente | admin, developer, psychiatrist |
| PATCH | `/patients/:id` | Actualizar paciente | admin, developer, psychiatrist assigned |
| DELETE | `/patients/:id` | Eliminar paciente | admin, developer |
| GET | `/patients/:id/sessions` | Historial de sesiones | admin, developer, psychiatrist assigned, own patient |
| GET | `/patients/:id/psychiatrist` | Psiquiatra asignado | admin, developer, psychiatrist assigned, own patient |

### 📋 Sessions (Sesiones médicas + Historia clínica)

| Método | Endpoint | Descripción | RBAC |
|--------|----------|-------------|------|
| GET | `/sessions` | Listar sesiones | admin, developer, psychiatrist (own), patient (own) |
| GET | `/sessions/:id` | Obtener sesión | admin, developer, psychiatrist (own), patient (own) |
| POST | `/sessions` | Crear sesión | admin, developer, psychiatrist |
| PATCH | `/sessions/:id` | Actualizar sesión | admin, developer, psychiatrist (own) |
| DELETE | `/sessions/:id` | Eliminar sesión | admin, developer, psychiatrist (own) |
| GET | `/sessions/:id/notes` | Obtener historia clínica | admin, developer, psychiatrist (own), patient (own) |
| PATCH | `/sessions/:id/notes` | Editar historia clínica | admin, developer, psychiatrist (own) |

**Filtros para GET /sessions:**
- `?patientId=xyz`
- `?psychiatristId=abc`
- `?from=2024-01-01&to=2024-12-31`
- `?page=1&pageSize=20`

---

## 🔒 Matriz de Permisos (RBAC)

| Recurso | Admin | Developer | Psychiatrist | Patient |
|---------|-------|-----------|--------------|---------|
| Users | CRUD | CRUD | Read (own) | Read (own) |
| People | CRUD | CRUD | CRUD (own) | CRUD (own) |
| Psychiatrists | CRUD | CRUD | Read (all), Update (own) | Read |
| Patients | CRUD | CRUD | CRUD (assigned) | Read (own) |
| Sessions | CRUD | CRUD | CRUD (own), Read (assigned patients) | Read (own) |

---

## 🎯 Decisiones de Diseño Clave

### ✅ Resource-oriented
- `/patients/:id/sessions` (sesiones de un paciente)
- `/psychiatrists/:id/patients` (pacientes de un psiquiatra)
- **NO:** `/getPatientSessions` o `/createSessionForPatient`

### ✅ Versionado desde el día 1
- Todo bajo `/api/v1/` para poder evolucionar sin romper

### ✅ Paginación obligatoria
- Todos los listados tienen `page` y `pageSize`
- Máximo 100 items por request

### ✅ Métodos HTTP semánticos
| Método | Uso | Características |
|--------|-----|-----------------|
| GET | Leer | Idempotent, safe |
| POST | Crear | - |
| PATCH | Actualizar parcial | - |
| DELETE | Eliminar | - |

### ✅ Errores consistentes
```json
{
  "error": "NotFound",
  "message": "Patient with id 123 not found",
  "details": { "id": 123 },
  "timestamp": "2024-01-15T10:30:00Z",
  "path": "/api/v1/patients/123"
}
```
