# Unidad II — Ejercicios Prácticos

> **Tema:** Mapeo Objeto-Relacional en SQL  
> **Caso de referencia:** Sistema de Biblioteca UAGRM  
> **Archivo de referencia:** `01_herencia_mapeo.sql`

---

# Ejercicio 1 — Identificación de clases y atributos

Para cada dominio se identifican las principales clases, sus atributos, tipos de datos, restricciones y claves primarias.

## a) Sistema de reservas de un hotel


┌──────────────────────────────────────┐
│                HOTEL                 │
├──────────────────────────────────────┤
│ + id_hotel: INTEGER <<PK>>           │
│ + nombre: VARCHAR(100) NOT NULL      │
│ + direccion: VARCHAR(200)            │
│ + ciudad: VARCHAR(100)               │
│ + categoria: INTEGER CHECK (1-5)     │
└──────────────────────────────────────┘

┌──────────────────────────────────────┐
│             HABITACION               │
├──────────────────────────────────────┤
│ + id_habitacion: INTEGER <<PK>>      │
│ + numero: INTEGER NOT NULL           │
│ + tipo: VARCHAR(30) NOT NULL         │
│ + capacidad: INTEGER NOT NULL        │
│ + precio: DECIMAL(10,2) NOT NULL     │
│ + id_hotel: INTEGER <<FK>>           │
└──────────────────────────────────────┘
┌──────────────────────────────────────┐
│               HUESPED                │
├──────────────────────────────────────┤
│ + ci: VARCHAR(15) <<PK>>             │
│ + nombre: VARCHAR(100) NOT NULL      │
│ + apellido: VARCHAR(100) NOT NULL    │
│ + telefono: VARCHAR(20)              │
│ + email: VARCHAR(100)                │
└──────────────────────────────────────┘
┌──────────────────────────────────────┐
│               RESERVA                │
├──────────────────────────────────────┤
│ + id_reserva: INTEGER <<PK>>         │
│ + fecha_inicio: DATE NOT NULL        │
│ + fecha_fin: DATE NOT NULL           │
│ + estado: VARCHAR(20) NOT NULL       │
│ + ci_huesped: VARCHAR(15) <<FK>>     │
│ + id_habitacion: INTEGER <<FK>>      │
└──────────────────────────────────────┘

**Relaciones**
HUESPED (1) ─────────── (N) RESERVA
HABITACION (1) ──────── (N) RESERVA
HOTEL (1) ───────────── (N) HABITACION
## b) Plataforma de streaming de música
┌──────────────────────────────────────┐
│               USUARIO                │
├──────────────────────────────────────┤
│ + id_usuario: INTEGER <<PK>>         │
│ + nombre: VARCHAR(100) NOT NULL      │
│ + email: VARCHAR(100) UNIQUE         │
│ + fecha_registro: DATE               │
└──────────────────────────────────────┘
┌──────────────────────────────────────┐
│               CANCION                │
├──────────────────────────────────────┤
│ + id_cancion: INTEGER <<PK>>         │
│ + titulo: VARCHAR(200) NOT NULL      │
│ + duracion: INTEGER NOT NULL         │
│ + genero: VARCHAR(50)                │
│ + anio: INTEGER                      │
│ + id_artista: INTEGER <<FK>>         │
└──────────────────────────────────────┘
┌──────────────────────────────────────┐
│               ARTISTA                │
├──────────────────────────────────────┤
│ + id_artista: INTEGER <<PK>>         │
│ + nombre: VARCHAR(150) NOT NULL      │
│ + pais: VARCHAR(50)                  │
└──────────────────────────────────────┘
┌──────────────────────────────────────┐
│             REPRODUCCION             │
├──────────────────────────────────────┤
│ + id_reproduccion: INTEGER <<PK>>    │
│ + fecha_hora: DATETIME NOT NULL      │
│ + id_usuario: INTEGER <<FK>>         │
│ + id_cancion: INTEGER <<FK>>         │
└──────────────────────────────────────┘
**Relaciones**
ARTISTA (1) ────────── (N) CANCION
USUARIO (1) ────────── (N) REPRODUCCION
CANCION (1) ─────────── (N) REPRODUCCION
## c) Sistema de gestión de una aerolínea
┌──────────────────────────────────────┐
│                VUELO                 │
├──────────────────────────────────────┤
│ + id_vuelo: INTEGER <<PK>>           │
│ + numero: VARCHAR(20) UNIQUE         │
│ + origen: VARCHAR(100) NOT NULL      │
│ + destino: VARCHAR(100) NOT NULL    │
│ + fecha_hora: DATETIME NOT NULL      │
└──────────────────────────────────────┘
┌──────────────────────────────────────┐
│              PASAJERO                │
├──────────────────────────────────────┤
│ + ci: VARCHAR(15) <<PK>>             │
│ + nombre: VARCHAR(100) NOT NULL      │
│ + apellido: VARCHAR(100) NOT NULL    │
│ + telefono: VARCHAR(20)              │
│ + email: VARCHAR(100)                │
└──────────────────────────────────────┘
┌──────────────────────────────────────┐
│               ASIENTO                │
├──────────────────────────────────────┤
│ + id_asiento: INTEGER <<PK>>         │
│ + numero: VARCHAR(10) NOT NULL       │
│ + clase: VARCHAR(30) NOT NULL        │
│ + estado: VARCHAR(20) NOT NULL       │
│ + id_vuelo: INTEGER <<FK>>           │
└──────────────────────────────────────┘
┌──────────────────────────────────────┐
│               RESERVA                │
├──────────────────────────────────────┤
│ + id_reserva: INTEGER <<PK>>         │
│ + fecha: DATE NOT NULL               │
│ + estado: VARCHAR(20) NOT NULL       │
│ + ci_pasajero: VARCHAR(15) <<FK>>    │
│ + id_vuelo: INTEGER <<FK>>           │
│ + id_asiento: INTEGER <<FK>>         │
└──────────────────────────────────────┘
**Relaciones**
VUELO (1) ──────────── (N) ASIENTO
VUELO (1) ──────────── (N) RESERVA
PASAJERO (1) ───────── (N) RESERVA
# Ejercicio 2 — Tipos de atributos
| Atributo                | Contexto   | Clasificación | Justificación                                            |
| ----------------------- | ---------- | ------------- | -------------------------------------------------------- |
| `nombre_completo`       | PERSONA    | Compuesto     | Puede dividirse en nombre y apellido.                    |
| `edad`                  | PERSONA    | Derivado      | Se obtiene a partir de la fecha de nacimiento.           |
| `dirección`             | CLIENTE    | Compuesto     | Está formada por calle, ciudad y código postal.          |
| `teléfonos`             | EMPLEADO   | Multivaluado  | Un empleado puede tener varios teléfonos.                |
| `precio_con_iva`        | PRODUCTO   | Derivado      | Se calcula a partir del precio base y el IVA.            |
| `calificacion_promedio` | ESTUDIANTE | Derivado      | Se obtiene calculando el promedio de sus calificaciones. |
| `nombre`                | PRODUCTO   | Simple        | Representa un único valor.                               |
| `coordenadas_gps`       | SUCURSAL   | Compuesto     | Está formada por latitud y longitud.                     |

# Ejercicio 3 — Cardinalidades
##a) PAÍS — CAPITAL

Cardinalidad: 1:1

Un país tiene una capital y una capital pertenece a un país.

PAÍS (1) ───────── (1) CAPITAL
##b) MÉDICO — PACIENTE

Cardinalidad: N:M

Un médico puede atender a muchos pacientes y un paciente puede ser atendido por varios médicos.

MÉDICO (N) ───────── (M) PACIENTE

En un modelo relacional se necesitaría una tabla intermedia, por ejemplo ATENCION.

##c) AUTOR — LIBRO

Cardinalidad: N:M

Un autor puede escribir varios libros y un libro puede tener varios autores.

AUTOR (N) ───────── (M) LIBRO

Se puede resolver mediante:

AUTOR ───< LIBRO_AUTOR >─── LIBRO
##d) EMPLEADO — PROYECTO

Cardinalidad: N:M

Un empleado puede participar en varios proyectos y un proyecto puede tener varios empleados.

EMPLEADO (N) ───────── (M) PROYECTO

Se requiere una tabla intermedia:

EMPLEADO ───< EMPLEADO_PROYECTO >─── PROYECTO
##e) ESTUDIANTE — CARRERA

Cardinalidad: N:1

Varios estudiantes pueden pertenecer a una misma carrera, mientras que cada estudiante pertenece a una carrera.

CARRERA (1) ───────── (N) ESTUDIANTE
##f) VUELO — ASIENTO

Cardinalidad: 1:N

Un vuelo tiene varios asientos y cada asiento pertenece a un vuelo.

VUELO (1) ───────── (N) ASIENTO
##g) FACTURA — PRODUCTO

Cardinalidad: N:M

Una factura puede contener varios productos y un producto puede aparecer en muchas facturas.

FACTURA (N) ───────── (M) PRODUCTO

Se resuelve mediante una tabla intermedia:

FACTURA ───< DETALLE_FACTURA >─── PRODUCTO
##h) PERSONA — DNI/CI

Cardinalidad: 1:1

Una persona posee un DNI/CI y un DNI/CI identifica a una sola persona.

PERSONA (1) ───────── (1) DNI/CI
#Ejercicio 4 — Herencia
##a) Sistema universitario

La clase PERSONA es la superclase y existen tres subclases:

                         PERSONA
                            △
             ┌──────────────┼──────────────┐
             │              │              │
             │              │              │
       ESTUDIANTE        DOCENTE     PERSONAL_ADMINISTRATIVO
             │              │              │
             ├─ carrera    ├─ categoría   ├─ cargo
             └─ año_ingreso└─ departamento└─ salario

┌──────────────────────────────┐
│            PERSONA           │
├──────────────────────────────┤
│ + ci: VARCHAR <<PK>>         │
│ + nombre: VARCHAR            │
│ + apellido: VARCHAR          │
│ + fecha_nac: DATE            │
└──────────────────────────────┘

┌──────────────────────────────┐
│          ESTUDIANTE          │
├──────────────────────────────┤
│ + ci: VARCHAR <<PK,FK>>      │
│ + carrera: VARCHAR           │
│ + año_ingreso: INTEGER       │
└──────────────────────────────┘

┌──────────────────────────────┐
│            DOCENTE           │
├──────────────────────────────┤
│ + ci: VARCHAR <<PK,FK>>      │
│ + categoria: VARCHAR         │
│ + departamento: VARCHAR      │
└──────────────────────────────┘

┌──────────────────────────────┐
│     PERSONAL_ADMINISTRATIVO  │
├──────────────────────────────┤
│ + ci: VARCHAR <<PK,FK>>      │
│ + cargo: VARCHAR             │
│ + salario: DECIMAL(10,2)     │
└──────────────────────────────┘
**Opción 1 — Tabla única**

Todas las clases se almacenan en una sola tabla.

PERSONA
├── ci
├── nombre
├── apellido
├── fecha_nac
├── tipo
├── carrera
├── año_ingreso
├── categoria
├── departamento
├── cargo
└── salario

Ejemplo:

CREATE TABLE PERSONA (
    ci VARCHAR(15) PRIMARY KEY,
    nombre VARCHAR(100) NOT NULL,
    apellido VARCHAR(100) NOT NULL,
    fecha_nac DATE,
    tipo VARCHAR(30) NOT NULL,
    carrera VARCHAR(100),
    año_ingreso INTEGER,
    categoria VARCHAR(50),
    departamento VARCHAR(100),
    cargo VARCHAR(100),
    salario DECIMAL(10,2)
);
**Ventaja**

Es sencilla de consultar porque toda la información está en una sola tabla.

**Desventaja**

Puede generar muchos valores NULL y desperdicio de espacio.

**Opción 2 — Tabla por hoja**

Se crea una tabla para la clase padre y una tabla para cada subclase.

PERSONA
├── ci
├── nombre
├── apellido
└── fecha_nac

ESTUDIANTE
├── ci
├── carrera
└── año_ingreso

DOCENTE
├── ci
├── categoria
└── departamento

PERSONAL_ADMINISTRATIVO
├── ci
├── cargo
└── salario

Ejemplo:

CREATE TABLE PERSONA (
    ci VARCHAR(15) PRIMARY KEY,
    nombre VARCHAR(100) NOT NULL,
    apellido VARCHAR(100) NOT NULL,
    fecha_nac DATE
);

CREATE TABLE ESTUDIANTE (
    ci VARCHAR(15) PRIMARY KEY,
    carrera VARCHAR(100) NOT NULL,
    año_ingreso INTEGER,
    FOREIGN KEY (ci) REFERENCES PERSONA(ci)
);

CREATE TABLE DOCENTE (
    ci VARCHAR(15) PRIMARY KEY,
    categoria VARCHAR(50) NOT NULL,
    departamento VARCHAR(100),
    FOREIGN KEY (ci) REFERENCES PERSONA(ci)
);

CREATE TABLE PERSONAL_ADMINISTRATIVO (
    ci VARCHAR(15) PRIMARY KEY,
    cargo VARCHAR(100) NOT NULL,
    salario DECIMAL(10,2),
    FOREIGN KEY (ci) REFERENCES PERSONA(ci)
);
**Opción 3 — Tabla por clase concreta**

Cada subclase contiene también los atributos heredados de PERSONA.

ESTUDIANTE
├── ci
├── nombre
├── apellido
├── fecha_nac
├── carrera
└── año_ingreso

DOCENTE
├── ci
├── nombre
├── apellido
├── fecha_nac
├── categoria
└── departamento

PERSONAL_ADMINISTRATIVO
├── ci
├── nombre
├── apellido
├── fecha_nac
├── cargo
└── salario
**¿Cuál opción elegiría?**

Para este sistema elegiría la Opción 2 — Tabla por hoja, porque permite mantener los atributos comunes de PERSONA en una sola tabla y los atributos específicos de cada tipo en sus respectivas tablas.

Además, evita la gran cantidad de valores NULL de la tabla única y evita repetir los atributos generales en cada tabla concreta.

#b) Sistema bancario

La clase CUENTA es la superclase.

                         CUENTA
                            △
                 ┌──────────┴──────────┐
                 │                     │
          CUENTA_AHORRO          CUENTA_CORRIENTE
                 │                     │
                 ├─ tasa_interes       ├─ sobregiro_permitido
                 └─ saldo_minimo       └─ cargos_mensuales
CUENTA
┌────────────────────────────────┐
│             CUENTA             │
├────────────────────────────────┤
│ + nro_cuenta: VARCHAR <<PK>>   │
│ + saldo: DECIMAL(12,2)         │
│ + fecha_apertura: DATE         │
└────────────────────────────────┘
CUENTA_AHORRO
┌────────────────────────────────┐
│         CUENTA_AHORRO          │
├────────────────────────────────┤
│ + nro_cuenta: VARCHAR <<PK>>   │
│ + tasa_interes: DECIMAL(5,2)   │
│ + saldo_minimo: DECIMAL(12,2)  │
└────────────────────────────────┘
CUENTA_CORRIENTE
┌────────────────────────────────┐
│       CUENTA_CORRIENTE         │
├────────────────────────────────┤
│ + nro_cuenta: VARCHAR <<PK>>   │
│ + sobregiro_permitido: DECIMAL │
│ + cargos_mensuales: DECIMAL    │
└────────────────────────────────┘

#Ejercicio 5 — Composición vs Agregación
**Relación	Tipo	Justificación**
PEDIDO — ÍTEM_PEDIDO	Composición ◆	Un ítem pertenece a un pedido y no tiene sentido sin él.
EMPRESA — EMPLEADO	Agregación ◇	Un empleado puede existir independientemente de una empresa.
FACTURA — LÍNEA_FACTURA	Composición ◆	Una línea de factura depende de la factura.
DEPARTAMENTO — DOCENTE	Agregación ◇	Un docente puede cambiar de departamento o existir fuera de uno específico.
EDIFICIO — PISO	Composición ◆	Los pisos forman parte del edificio.
CURSO — ESTUDIANTE	Agregación ◇	Un estudiante existe independientemente del curso.
EXPEDIENTE_MÉDICO — DIAGNÓSTICO	Composición ◆	El diagnóstico registrado forma parte del expediente médico.
Representación
PEDIDO ◆──── ÍTEM_PEDIDO

EMPRESA ◇──── EMPLEADO

FACTURA ◆──── LÍNEA_FACTURA

DEPARTAMENTO ◇──── DOCENTE

EDIFICIO ◆──── PISO

CURSO ◇──── ESTUDIANTE

EXPEDIENTE_MÉDICO ◆──── DIAGNÓSTICO
##Ejercicio 6 — Diagrama completo: Sistema de Veterinaria
Diagrama general
                         MASCOTA
                            △
             ┌──────────────┼──────────────┐
             │              │              │
           PERRO           GATO            AVE
                            │
                          REPTIL

DUEÑO (N) ◇────────── (M) MASCOTA

MASCOTA (1) ──────── (N) CONSULTA
VETERINARIO (1) ──── (N) CONSULTA

CONSULTA (1) ◆────── (0..1) RECETA
RECETA (1) ───────── (N) MEDICAMENTO

MASCOTA (1) ──────── (N) VACUNA
Clase MASCOTA
┌──────────────────────────────────┐
│              MASCOTA             │
├──────────────────────────────────┤
│ + id_mascota: INTEGER <<PK>>     │
│ + nombre: VARCHAR(100) NOT NULL  │
│ + fecha_nac: DATE                │
│ + sexo: VARCHAR(10)              │
│ + peso: DECIMAL(6,2)             │
└──────────────────────────────────┘
Clase PERRO
┌──────────────────────────────────┐
│               PERRO              │
├──────────────────────────────────┤
│ + id_mascota: INTEGER <<PK,FK>>  │
│ + raza: VARCHAR(50)              │
│ + tamaño: VARCHAR(30)            │
└──────────────────────────────────┘
Clase GATO
┌──────────────────────────────────┐
│                GATO              │
├──────────────────────────────────┤
│ + id_mascota: INTEGER <<PK,FK>>  │
│ + raza: VARCHAR(50)              │
└──────────────────────────────────┘
Clase AVE
┌──────────────────────────────────┐
│                 AVE              │
├──────────────────────────────────┤
│ + id_mascota: INTEGER <<PK,FK>>  │
│ + especie: VARCHAR(50)           │
│ + envergadura: DECIMAL(6,2)      │
└──────────────────────────────────┘
Clase REPTIL
┌──────────────────────────────────┐
│               REPTIL             │
├──────────────────────────────────┤
│ + id_mascota: INTEGER <<PK,FK>>  │
│ + especie: VARCHAR(50)           │
│ + venenoso: INTEGER              │
└──────────────────────────────────┘
Clase DUEÑO
┌──────────────────────────────────┐
│                DUEÑO             │
├──────────────────────────────────┤
│ + ci: VARCHAR(15) <<PK>>         │
│ + nombre: VARCHAR(100) NOT NULL  │
│ + telefono: VARCHAR(20)          │
│ + direccion: VARCHAR(200)        │
└──────────────────────────────────┘
Clase VETERINARIO
┌──────────────────────────────────┐
│            VETERINARIO           │
├──────────────────────────────────┤
│ + id_veterinario: INTEGER <<PK>> │
│ + nombre: VARCHAR(100) NOT NULL  │
│ + especialidad: VARCHAR(100)     │
│ + telefono: VARCHAR(20)          │
└──────────────────────────────────┘
Clase CONSULTA
┌──────────────────────────────────┐
│             CONSULTA             │
├──────────────────────────────────┤
│ + id_consulta: INTEGER <<PK>>    │
│ + fecha: DATETIME NOT NULL       │
│ + motivo: VARCHAR(300)           │
│ + diagnostico: VARCHAR(500)      │
│ + id_mascota: INTEGER <<FK>>     │
│ + id_veterinario: INTEGER <<FK>> │
└──────────────────────────────────┘
Clase RECETA
┌──────────────────────────────────┐
│              RECETA              │
├──────────────────────────────────┤
│ + id_receta: INTEGER <<PK>>      │
│ + fecha: DATE NOT NULL           │
│ + indicaciones: VARCHAR(500)     │
│ + id_consulta: INTEGER <<FK>>    │
└──────────────────────────────────┘
Clase MEDICAMENTO
┌──────────────────────────────────┐
│           MEDICAMENTO            │
├──────────────────────────────────┤
│ + id_medicamento: INTEGER <<PK>>│
│ + nombre: VARCHAR(100) NOT NULL  │
│ + presentacion: VARCHAR(100)     │
│ + dosis: VARCHAR(50)             │
└──────────────────────────────────┘
Clase VACUNA
┌──────────────────────────────────┐
│              VACUNA              │
├──────────────────────────────────┤
│ + id_vacuna: INTEGER <<PK>>      │
│ + nombre: VARCHAR(100) NOT NULL  │
│ + fecha_aplicacion: DATE         │
│ + proxima_dosis: DATE            │
│ + id_mascota: INTEGER <<FK>>     │
└──────────────────────────────────┘
**Relaciones principales**
DUEÑO (N) ◇──────── (M) MASCOTA

MASCOTA (1) ──────── (N) CONSULTA

VETERINARIO (1) ──── (N) CONSULTA

CONSULTA (1) ◆────── (0..1) RECETA

RECETA (N) ───────── (M) MEDICAMENTO

MASCOTA (1) ──────── (N) VACUNA

**Composición**: CONSULTA ◆── RECETA, porque la receta pertenece a una consulta específica.

**Agregación**: DUEÑO ◇── MASCOTA, porque el dueño y la mascota pueden existir independientemente
##Ejercicio 7 — Mapeo ORM
Diagrama de clases
FACULTAD (1) ──────── (N) CARRERA (1) ──────── (N) MATERIA
                           │
                           │
                           └──── (N) ESTUDIANTE
                                      │
                                      │
                                      N
                                      │
                                      M
                                   MATERIA

                         INSCRIPCION
                    ┌──────────────────┐
                    │ gestion          │
                    │ nota             │
                    └──────────────────┘

La relación N:M entre ESTUDIANTE y MATERIA se transforma en una tabla intermedia denominada INSCRIPCION.

Tabla FACULTAD
CREATE TABLE FACULTAD (
    id_facultad INTEGER PRIMARY KEY,
    nombre VARCHAR(100) NOT NULL UNIQUE,
    CHECK (length(nombre) >= 3),
    CHECK (nombre <> '')
);
Estructura
Campo	Tipo	Restricción
id_facultad	INTEGER	PK
nombre	VARCHAR(100)	NOT NULL, UNIQUE
Tabla CARRERA
CREATE TABLE CARRERA (
    id_carrera INTEGER PRIMARY KEY,
    nombre VARCHAR(100) NOT NULL UNIQUE,
    id_facultad INTEGER NOT NULL,
    duracion_anios INTEGER NOT NULL,
    FOREIGN KEY (id_facultad) REFERENCES FACULTAD(id_facultad),
    CHECK (duracion_anios BETWEEN 3 AND 7),
    CHECK (length(nombre) >= 3)
);
Estructura
Campo	Tipo	Restricción
id_carrera	INTEGER	PK
nombre	VARCHAR(100)	NOT NULL, UNIQUE
id_facultad	INTEGER	FK
duracion_anios	INTEGER	CHECK 3–7
Tabla ESTUDIANTE
CREATE TABLE ESTUDIANTE (
    ci VARCHAR(15) PRIMARY KEY,
    nombre VARCHAR(100) NOT NULL,
    apellido VARCHAR(100) NOT NULL,
    id_carrera INTEGER NOT NULL,
    anio_ingreso INTEGER NOT NULL,
    FOREIGN KEY (id_carrera) REFERENCES CARRERA(id_carrera),
    CHECK (length(nombre) >= 2),
    CHECK (anio_ingreso >= 2000)
);
Estructura
Campo	Tipo	Restricción
ci	VARCHAR(15)	PK
nombre	VARCHAR(100)	NOT NULL
apellido	VARCHAR(100)	NOT NULL
id_carrera	INTEGER	FK
anio_ingreso	INTEGER	CHECK
Tabla MATERIA
CREATE TABLE MATERIA (
    id_materia INTEGER PRIMARY KEY,
    nombre VARCHAR(100) NOT NULL,
    id_carrera INTEGER NOT NULL,
    creditos INTEGER NOT NULL,
    FOREIGN KEY (id_carrera) REFERENCES CARRERA(id_carrera),
    CHECK (creditos BETWEEN 1 AND 10),
    CHECK (length(nombre) >= 3)
);
Estructura
Campo	Tipo	Restricción
id_materia	INTEGER	PK
nombre	VARCHAR(100)	NOT NULL
id_carrera	INTEGER	FK
creditos	INTEGER	CHECK 1–10
Tabla INSCRIPCION

Esta tabla resuelve la relación N:M entre ESTUDIANTE y MATERIA.

CREATE TABLE INSCRIPCION (
    ci_estudiante VARCHAR(15) NOT NULL,
    id_materia INTEGER NOT NULL,
    gestion INTEGER NOT NULL,
    nota DECIMAL(5,2),
    PRIMARY KEY (ci_estudiante, id_materia, gestion),
    FOREIGN KEY (ci_estudiante) REFERENCES ESTUDIANTE(ci),
    FOREIGN KEY (id_materia) REFERENCES MATERIA(id_materia),
    CHECK (gestion >= 2000),
    CHECK (nota IS NULL OR nota BETWEEN 0 AND 100)
);
Estructura
Campo	Tipo	Restricción
ci_estudiante	VARCHAR(15)	PK, FK
id_materia	INTEGER	PK, FK
gestion	INTEGER	PK, CHECK
nota	DECIMAL(5,2)	CHECK 0–100
Esquema relacional final
FACULTAD
---------
id_facultad PK
nombre
│
│ 1:N
▼
CARRERA
-------
id_carrera PK
nombre
id_facultad FK
duracion_anios
│
├────────────── 1:N ──────────────► MATERIA
│
└────────────── 1:N ──────────────► ESTUDIANTE
                                      │
                                      │
                                      │
                                      ▼
                                INSCRIPCION
                                      ▲
                                      │
                                      │
                                   MATERIA

La relación entre estudiantes y materias queda:

ESTUDIANTE (N) ──── (M) MATERIA
          \           /
           \         /
          INSCRIPCION 
##Ejercicio 8 — ER → Diagrama de Clases
Esquema ER original
[EMPLEADO] ─── (trabaja_en) ─── [DEPARTAMENTO]
    │                                  │
(supervisa)                     (ubicado_en)
    │                                  │
[EMPLEADO]                       [CIUDAD]
Conversión a UML
EMPLEADO
┌──────────────────────────────────┐
│             EMPLEADO             │
├──────────────────────────────────┤
│ + id_empleado: INTEGER <<PK>>    │
│ + nombre: VARCHAR(100) NOT NULL  │
│ + apellido: VARCHAR(100)         │
│ + cargo: VARCHAR(100)            │
│ + id_departamento: INTEGER <<FK>>│
│ + id_supervisor: INTEGER <<FK>>  │
└──────────────────────────────────┘
DEPARTAMENTO
┌──────────────────────────────────┐
│           DEPARTAMENTO           │
├──────────────────────────────────┤
│ + id_departamento: INTEGER <<PK>>│
│ + nombre: VARCHAR(100) NOT NULL  │
│ + id_ciudad: INTEGER <<FK>>      │
└──────────────────────────────────┘
CIUDAD
┌──────────────────────────────────┐
│              CIUDAD              │
├──────────────────────────────────┤
│ + id_ciudad: INTEGER <<PK>>      │
│ + nombre: VARCHAR(100) NOT NULL  │
│ + departamento: VARCHAR(100)     │
└──────────────────────────────────┘
Relaciones UML
                         ┌──────────────┐
                         │ DEPARTAMENTO │
                         └──────┬───────┘
                                │
                              (N:1)
                                │
                                ▼
                         ┌──────────────┐
                         │    CIUDAD    │
                         └──────────────┘


┌──────────────┐
│   EMPLEADO   │
└──────┬───────┘
       │
       │ N:1
       ▼
┌──────────────┐
│ DEPARTAMENTO │
└──────────────┘


       ┌──────────────────────────┐
       │       EMPLEADO           │
       └───────────┬──────────────┘
                   │
                 1:N
             supervisa
                   │
                   ▼
       ┌──────────────────────────┐
       │       EMPLEADO           │
       └──────────────────────────┘
Modelo completo
                     ┌──────────────┐
                     │    CIUDAD    │
                     └──────▲───────┘
                            │
                           1:N
                            │
                     ┌──────┴───────┐
                     │ DEPARTAMENTO │
                     └──────▲───────┘
                            │
                           1:N
                            │
                     ┌──────┴───────┐
                     │   EMPLEADO   │
                     └──────┬───────┘
                            │
                          1:N
                        supervisa
                            │
                            ▼
                     ┌──────────────┐
                     │   EMPLEADO   │
                     └──────────────┘
##Diferencias entre ER y UML
| Aspecto            | Modelo ER                          | UML                                                |
| ------------------ | ---------------------------------- | -------------------------------------------------- |
| Elemento principal | Entidades                          | Clases                                             |
| Propiedades        | Atributos                          | Atributos                                          |
| Relaciones         | Relaciones                         | Asociaciones                                       |
| Cardinalidad       | 1:1, 1:N, N:M                      | Multiplicidades como 1, 0..1, 1..*, *              |
| Herencia           | No es el elemento principal        | Se representa directamente mediante generalización |
| Composición        | No se representa de la misma forma | Se representa con diamante lleno `◆`               |
| Agregación         | No se representa igual             | Se representa con diamante vacío `◇`               |
| Métodos            | Generalmente no se incluyen        | Las clases pueden incluir operaciones/métodos      |
| Identificación     | PK en entidades                    | Se puede indicar mediante `<<PK>>`                 |
