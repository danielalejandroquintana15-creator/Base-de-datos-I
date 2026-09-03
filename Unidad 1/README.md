# Base-de-datos-I
Tareas y avances de la materia de Base de Datos I, grupo I4
# Ejercicios — Sistemas Gestores de Bases de Datos (SGBD)

---

## Ejercicio 1 — Identificación de componentes SGBD

### Contexto

Una empresa de logística maneja **envíos, clientes, rutas y conductores**. Los envíos se registran con fecha, origen, destino, peso y estado.

### a) Minimundo del sistema y entidades

El **minimundo** representa la parte de la realidad que será gestionada por el sistema de base de datos. En este caso, corresponde a las operaciones relacionadas con la gestión de envíos de una empresa de logística.

Las principales entidades son:

- **Cliente:** persona o empresa que solicita un envío.
- **Envío:** operación de transporte de una mercancía.
- **Ruta:** recorrido utilizado para realizar un envío.
- **Conductor:** persona encargada de conducir el vehículo que realiza el envío.

El envío contiene información como fecha, origen, destino, peso y estado.

### b) SGBD elegido

Se elegiría **PostgreSQL** como SGBD.

PostgreSQL es una buena opción porque es un sistema gestor de bases de datos relacional, robusto, escalable y adecuado para aplicaciones que manejan una cantidad considerable de información y múltiples usuarios simultáneamente.

| SGBD | Características |
|---|---|
| SQLite | Es ligero y sencillo, adecuado para aplicaciones pequeñas o locales. |
| MySQL | Es popular, fácil de utilizar y adecuado para aplicaciones web. |
| PostgreSQL | Es robusto, escalable y ofrece características avanzadas para sistemas complejos. |

Para una empresa de logística, **PostgreSQL** sería una buena elección debido a su capacidad para manejar múltiples usuarios, transacciones y grandes cantidades de datos.

### c) Actores del sistema

#### Administrador de la empresa

- Gestiona clientes.
- Gestiona conductores.
- Registra y modifica rutas.
- Consulta información de los envíos.

#### Operador logístico

- Registra nuevos envíos.
- Asigna rutas.
- Consulta el estado de los envíos.
- Actualiza información de los envíos.

#### Conductor

- Consulta los envíos asignados.
- Consulta la ruta correspondiente.
- Actualiza el estado del envío durante el recorrido.

### d) Esquema de tres niveles

```text
                    NIVEL EXTERNO
        ┌──────────────┬──────────────┐
        │              │              │
   Administrador    Operador      Conductor
        │              │              │
        └──────────────┼──────────────┘
                       │
                       ▼
                 NIVEL CONCEPTUAL
              ┌─────────────────────┐
              │   Base de Datos                        │
              │                                                  │
              │ CLIENTE                                    │
              │ ENVÍO                                       │
              │ RUTA                                         │
              │ CONDUCTOR                            │
              └─────────────────────┘
                       │
                       ▼
                  NIVEL INTERNO
              ┌─────────────────────┐
              │ Archivos                                    │
              │ Índices                                      │
              │ Páginas de datos                      │
              │ Almacenamiento                      │
              └─────────────────────┘
```

El **nivel externo** representa las diferentes vistas que tienen los usuarios.

El **nivel conceptual** representa la estructura lógica completa de la base de datos.

El **nivel interno** describe cómo se almacenan físicamente los datos.

---

## Ejercicio 2 — Archivos vs Base de Datos

### a) Problemas del uso de archivos planos

El uso de archivos de texto independientes para registrar los préstamos puede generar los siguientes problemas:

1. **Redundancia de información:** los mismos datos de estudiantes o libros pueden repetirse en diferentes archivos.
2. **Dificultad para realizar consultas:** buscar todos los préstamos de un estudiante requiere revisar varios archivos.
3. **Problemas de integridad:** puede ser difícil garantizar que los datos sean correctos y consistentes.
4. **Dificultad para controlar usuarios:** varios usuarios podrían modificar los archivos simultáneamente y generar conflictos.
5. **Mayor dificultad para realizar respaldos:** existen muchos archivos que deben respaldarse y administrarse.
6. **Escalabilidad limitada:** a medida que aumenta la cantidad de información, administrar los archivos se vuelve más complicado.

### b) Solución mediante un SGBD relacional

| Problema | Solución del SGBD |
|---|---|
| Redundancia | Organización de los datos mediante tablas relacionadas y normalización. |
| Consultas difíciles | Uso de SQL para realizar búsquedas y consultas. |
| Integridad | Claves primarias, claves foráneas y restricciones. |
| Acceso simultáneo | Control de concurrencia y transacciones. |
| Respaldos | Herramientas de backup y recuperación. |
| Crecimiento de datos | Administración eficiente de grandes cantidades de información. |

### c) Escenario donde podrían utilizarse archivos planos

Los archivos planos pueden ser válidos cuando se necesita almacenar una **cantidad pequeña de información**, existe un único usuario y no se requieren relaciones complejas ni consultas frecuentes.

Por ejemplo, un programa pequeño podría utilizar un archivo de texto para guardar una configuración o una lista temporal de datos.

---

## Ejercicio 3 — Metadatos y catálogo del sistema

La consulta utilizada es:

```sql
SELECT name, type, sql 
FROM sqlite_master;
```

### a) ¿Qué información devuelve?

La consulta muestra información sobre los objetos definidos dentro de una base de datos SQLite.

Entre la información que puede devolver se encuentran:

- **name:** nombre del objeto.
- **type:** tipo de objeto, como tabla, índice, vista o trigger.
- **sql:** sentencia SQL utilizada para crear el objeto.

Por ejemplo:

```text
name        | type   | sql
------------|--------|-------------------------
estudiante  | table  | CREATE TABLE estudiante...
idx_nombre  | index  | CREATE INDEX idx_nombre...
```

### b) ¿Por qué el catálogo del sistema es una base de datos?

El catálogo del sistema almacena información estructurada sobre los objetos que forman parte de la propia base de datos.

Por ejemplo, guarda información sobre:

- Tablas.
- Columnas.
- Índices.
- Vistas.
- Triggers.

Por esta razón, el catálogo puede considerarse una base de datos de **metadatos**, es decir, información acerca de los datos y de la estructura de la BD.

### c) Datos y metadatos

Los **datos** son la información que representa objetos o hechos del mundo real.

#### Ejemplos de datos

- CI: `1234567`
- Nombre: `Juan`
- Fecha de nacimiento: `2003-05-15`

Los **metadatos** describen la estructura y características de esos datos.

#### Ejemplos de metadatos

- Nombre de la tabla: `ESTUDIANTE`
- Nombre de una columna: `nombre`
- Tipo de dato de la columna: `VARCHAR(50)`

---

## Ejercicio 4 — Independencia de datos

La base de datos contiene:

```text
ESTUDIANTE(ci, nombre, apellido, fecha_nac)
```

Se decide agregar la columna `email` y cambiar `fecha_nac` por `edad`.

### a) Aplicaciones que podrían romperse

Podrían romperse las aplicaciones que dependen directamente de la estructura anterior de la tabla.

Por ejemplo:

- Aplicaciones que realizan consultas utilizando `fecha_nac`.
- Reportes que muestran la fecha de nacimiento.
- Programas que calculan la edad utilizando `fecha_nac`.
- Consultas SQL que esperan encontrar la columna `fecha_nac`.

Si la columna `fecha_nac` se elimina y se reemplaza por `edad`, las consultas que utilicen `fecha_nac` dejarán de funcionar.

### b) Independencia lógica y física

**Independencia lógica de datos:** es la capacidad de modificar la estructura lógica de la base de datos sin tener que modificar las aplicaciones o vistas que dependen de ella, siempre que sea posible mantener su funcionamiento.

**Ejemplo:** agregar una nueva columna a una tabla sin afectar las aplicaciones existentes.

**Independencia física de datos:** es la capacidad de modificar la forma en que los datos se almacenan físicamente sin modificar el esquema lógico ni las aplicaciones.

**Ejemplo:** cambiar la organización de los archivos, índices o estructuras de almacenamiento sin cambiar las tablas que utilizan los usuarios.

### c) Uso de vistas

Las vistas pueden ayudar a mantener la independencia lógica porque permiten presentar a las aplicaciones una estructura estable aunque la organización interna de las tablas cambie.

Por ejemplo:

```sql
SELECT ci, nombre, apellido, fecha_nac
FROM ESTUDIANTE;
```

Se puede crear una **vista** que mantenga esa estructura mientras internamente se realizan cambios en las tablas.

De esta manera, las aplicaciones pueden continuar utilizando la vista sin conocer todos los cambios realizados en la estructura interna de la base de datos.

---

## Ejercicio 5 — Arquitectura de SGBD

```text
Aplicación Web      App Móvil      Reporte Python
       │                │                │
       └────────────────┼────────────────┘
                        │
                        ▼
                 ┌─────────────┐
                 │     SGBD    │
                 │ Componente X│
                 └─────────────┘
                        │
                        ▼
                 Base de Datos
```

### a) ¿Qué es el Componente X?

El **Componente X es el Sistema Gestor de Bases de Datos (SGBD)**.

Es el software encargado de administrar la base de datos y actuar como intermediario entre las aplicaciones y los datos almacenados.

Entre sus funciones se encuentran:

- Permitir la creación y modificación de bases de datos.
- Ejecutar consultas SQL.
- Administrar el acceso de los usuarios.
- Mantener la integridad de los datos.
- Controlar las transacciones.
- Gestionar el almacenamiento y recuperación de información.
- Proporcionar mecanismos de seguridad y recuperación.

### b) Cinco funciones de un SGBD además de almacenar datos

1. **Control de acceso:** determina qué usuarios pueden acceder o modificar información.
2. **Gestión de transacciones:** garantiza que las operaciones se ejecuten correctamente.
3. **Control de concurrencia:** permite que varios usuarios trabajen simultáneamente.
4. **Seguridad:** protege la información frente a accesos no autorizados.
5. **Recuperación:** permite recuperar los datos después de fallos o errores.

También puede proporcionar funciones de respaldo, optimización de consultas, mantenimiento de índices e integridad referencial.

### c) Diferencia entre SGBD y sistema de archivos

Un **sistema de archivos (filesystem)** administra archivos y directorios dentro de un dispositivo de almacenamiento.

Un **SGBD** administra datos estructurados y proporciona mecanismos especializados para consultar, relacionar, proteger y mantener la integridad de esos datos.

| Característica | Sistema de archivos | SGBD |
|---|---|---|
| Organización | Archivos y carpetas | Tablas y relaciones |
| Consultas | Limitadas | SQL y consultas avanzadas |
| Integridad | Limitada | Restricciones y reglas |
| Concurrencia | Básica | Controlada mediante transacciones |
| Seguridad | Permisos de archivos | Usuarios, roles y permisos |
| Relaciones entre datos | No nativas | Sí |
| Recuperación | Depende del sistema | Mecanismos de recuperación y respaldo |

**Similitud:** ambos permiten almacenar, organizar, recuperar y administrar información en dispositivos de almacenamiento.
---

# Ejercicio 6 — Práctica SQLite

Para este ejercicio se analiza el script `01_intro_sqlite.py`, desarrollado en Python utilizando el módulo `sqlite3`.

### a) ¿En qué directorio se crea el archivo `.db`? ¿Qué pasa si lo eliminas y vuelves a ejecutar el script?

El archivo de la base de datos se crea en el directorio:

```text
/tmp/universidad_bd1.db
```

Esto se debe a que en el script se define:

```python
DB_PATH = "/tmp/universidad_bd1.db"
```

SQLite crea automáticamente el archivo `.db` cuando se establece la conexión mediante:

```python
conn = sqlite3.connect(DB_PATH)
```

Sin embargo, en este script existe una particularidad. Antes de conectarse a la base de datos, el programa verifica si el archivo existe y lo elimina:

```python
if os.path.exists(DB_PATH):
    os.remove(DB_PATH)
```

Por lo tanto, **cada vez que se ejecuta el programa se elimina la base de datos anterior y se crea una nueva**.

Después de eliminarla, el programa vuelve a ejecutar las instrucciones `CREATE TABLE` e `INSERT`, creando nuevamente las tablas y cargando los datos iniciales.

En resumen:

```text
Ejecución del programa
        ↓
¿Existe universidad_bd1.db?
        ↓
      Sí
        ↓
Se elimina la BD anterior
        ↓
Se crea una nueva BD
        ↓
Se crean las tablas
        ↓
Se insertan nuevamente los datos
```

### b) Agregar la tabla CARRERA e insertar 3 carreras

En el script proporcionado, **esta parte ya está implementada**.

La tabla `CARRERA` se crea mediante:

```sql
CREATE TABLE IF NOT EXISTS CARRERA (
    id_carrera INTEGER PRIMARY KEY AUTOINCREMENT,
    nombre VARCHAR(100) NOT NULL UNIQUE,
    duracion_anios INTEGER DEFAULT 5
)
```

También se insertan tres carreras:

```python
conn.executemany(
    "INSERT OR IGNORE INTO CARRERA (nombre, duracion_anios) VALUES (?, ?)",
    [
        ("Ingeniería en Sistemas", 5),
        ("Ingeniería en Telecomunicaciones", 5),
        ("Licenciatura en Informática", 4),
    ]
)
```

Por lo tanto, las tres carreras son:

| ID | Carrera | Duración |
|---:|---|---:|
| 1 | Ingeniería en Sistemas | 5 años |
| 2 | Ingeniería en Telecomunicaciones | 5 años |
| 3 | Licenciatura en Informática | 4 años |

Además, la tabla `ESTUDIANTE` ya tiene una relación con `CARRERA` mediante:

```sql
id_carrera INTEGER,
FOREIGN KEY (id_carrera) REFERENCES CARRERA(id_carrera)
```

Esto permite determinar a qué carrera pertenece cada estudiante.

### c) Consulta SQL para listar estudiantes de una carrera específica usando JOIN

Para listar los estudiantes inscritos en una carrera específica se puede utilizar la siguiente consulta:

```sql
SELECT 
    e.ci,
    e.nombre,
    e.apellido,
    c.nombre AS carrera
FROM ESTUDIANTE e
JOIN CARRERA c 
    ON e.id_carrera = c.id_carrera
WHERE c.nombre = 'Ingeniería en Sistemas'
ORDER BY e.apellido, e.nombre;
```

La consulta relaciona las tablas `ESTUDIANTE` y `CARRERA` mediante el campo `id_carrera`.

Por ejemplo, para consultar los estudiantes de **Ingeniería en Sistemas**, se utiliza:

```sql
WHERE c.nombre = 'Ingeniería en Sistemas'
```

---

# Ejercicio 7 — Desafío integrador

## Sistema elegido: Gestión de turnos de un consultorio médico

### 1. Minimundo

El sistema permitirá gestionar los turnos de un consultorio médico y organizar la atención de los pacientes.

El consultorio registra información de los pacientes que solicitan atención médica.

Los médicos poseen diferentes especialidades y atienden en determinados horarios.

Cada paciente puede solicitar uno o varios turnos con un médico.

Cada turno registra la fecha, hora y estado de la atención.

El sistema también permitirá consultar el historial de turnos de los pacientes.

De esta manera, la información estará organizada y será posible controlar los turnos disponibles, atendidos, cancelados y pendientes.

### 2. Entidades y atributos principales

#### PACIENTE

- `id_paciente`
- `ci`
- `nombre`
- `apellido`
- `fecha_nacimiento`
- `telefono`
- `email`

#### MÉDICO

- `id_medico`
- `ci`
- `nombre`
- `apellido`
- `telefono`
- `id_especialidad`

#### ESPECIALIDAD

- `id_especialidad`
- `nombre`
- `descripcion`

#### TURNO

- `id_turno`
- `fecha`
- `hora`
- `estado`
- `motivo`
- `id_paciente`
- `id_medico`

#### CONSULTORIO

- `id_consultorio`
- `numero`
- `ubicacion`
- `piso`
- `estado`

### 3. Relaciones principales

Las relaciones entre las entidades serían:

```text
ESPECIALIDAD
     │
     │ 1:N
     ▼
   MÉDICO
     │
     │ 1:N
     ▼
   TURNO
     ▲
     │ N:1
     │
 PACIENTE

CONSULTORIO
     │
     │ 1:N
     ▼
   TURNO
```

Un médico pertenece a una especialidad y una especialidad puede tener varios médicos.

Un paciente puede tener varios turnos.

Un médico puede atender varios turnos.

Un consultorio puede ser utilizado para diferentes turnos.

### 4. Actores del sistema y sus roles

#### Administrador

- Registrar y modificar médicos.
- Registrar especialidades.
- Registrar consultorios.
- Gestionar usuarios.
- Consultar información general del sistema.

#### Recepcionista

- Registrar pacientes.
- Crear turnos.
- Modificar turnos.
- Cancelar turnos.
- Consultar disponibilidad de médicos.

#### Médico

- Consultar sus turnos.
- Consultar información de los pacientes.
- Registrar información relacionada con la atención.
- Consultar el historial de turnos del paciente.

#### Paciente

- Solicitar un turno.
- Consultar sus turnos.
- Consultar la fecha y hora de su cita.
- Cancelar un turno según las reglas del consultorio.

### 5. Consultas que debería poder responder el sistema

1. **¿Qué pacientes tienen turnos programados para una determinada fecha?**

2. **¿Qué turnos tiene asignados un médico en una fecha específica?**

3. **¿Qué médicos están disponibles para una determinada especialidad?**

4. **¿Cuántos turnos fueron atendidos, cancelados y pendientes durante un período?**

5. **¿Cuál es el historial de turnos de un paciente determinado?**

### 6. Resumen del modelo conceptual

```text
┌─────────────────┐
│  ESPECIALIDAD   │
├─────────────────┤
│ id_especialidad │
│ nombre          │
│ descripcion     │
└────────┬────────┘
         │
         │ 1:N
         ▼
┌─────────────────┐
│     MÉDICO      │
├─────────────────┤
│ id_medico       │
│ ci              │
│ nombre          │
│ apellido        │
│ id_especialidad │
└────────┬────────┘
         │
         │ 1:N
         ▼
┌─────────────────┐       ┌─────────────────┐
│      TURNO      │       │    PACIENTE     │
├─────────────────┤       ├─────────────────┤
│ id_turno        │◄──────│ id_paciente     │
│ fecha           │  N:1  │ ci              │
│ hora            │       │ nombre          │
│ estado          │       │ apellido        │
│ id_paciente     │       │ telefono        │
│ id_medico       │       └─────────────────┘
│ id_consultorio  │
└────────┬────────┘
         │
         │ N:1
         ▼
┌─────────────────┐
│  CONSULTORIO    │
├─────────────────┤
│ id_consultorio  │
│ numero          │
│ ubicacion       │
│ piso            │
│ estado          │
└─────────────────┘
```

---

# Conclusión

Los ejercicios permiten comprender los principales conceptos relacionados con los Sistemas Gestores de Bases de Datos. Se analizaron los componentes de un SGBD, las diferencias entre archivos planos y bases de datos, los metadatos, la independencia de datos y la arquitectura de un SGBD.

También se realizó una práctica utilizando **Python y SQLite**, donde se creó una base de datos universitaria con tablas relacionadas mediante claves foráneas. Finalmente, se diseñó conceptualmente una base de datos para la gestión de turnos de un consultorio médico, identificando sus entidades, atributos, relaciones, actores y consultas principales.
