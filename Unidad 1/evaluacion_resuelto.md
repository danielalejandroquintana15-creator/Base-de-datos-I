# Unidad I · Banco de Evaluación y Rúbrica

## Objetivo

Evaluar el dominio conceptual sobre los **sistemas de bases de datos**, su arquitectura, los actores involucrados y las ventajas del enfoque de bases de datos.

---

## Formato de evaluación

| Componente | Puntos |
|---|---:|
| Teoría corta (conceptos clave) | 30 |
| Análisis de caso | 30 |
| Preguntas de aplicación | 40 |
| **Total** | **100** |

---

# Banco de preguntas

## Parte A · Teoría

**Tipo:** Respuesta corta

### 1. Define base de datos y minimundo con tus palabras.

Explica qué es una base de datos y qué se entiende por **minimundo**, indicando la relación que existe entre ambos conceptos.

### 2. Diferencia entre dato, información y metadato.

Explica las diferencias entre estos tres conceptos e incluye un ejemplo para cada uno.

### 3. ¿Qué es un SGBD y por qué no basta solo con archivos planos?

Explica qué función cumple un **Sistema Gestor de Bases de Datos (SGBD)** y menciona algunas de las limitaciones que presentan los archivos planos.

### 4. Explica las 4 características del enfoque de BD.

Describe las cuatro características principales:

- **Catálogo o metadatos (autodescripción).**
- **Aislamiento entre programas y datos.**
- **Múltiples vistas.**
- **Compartición de datos y procesamiento multiusuario.**

### 5. ¿Qué significa independencia lógica y física de datos?

Explica la diferencia entre:

- **Independencia lógica de datos.**
- **Independencia física de datos.**

### 6. Diferencia DDL, DML y DCL con un ejemplo de comando para cada uno.

| Categoría | Finalidad | Ejemplo |
|---|---|---|
| DDL | Definir o modificar la estructura de la BD | `CREATE TABLE` |
| DML | Consultar y manipular los datos | `SELECT` |
| DCL | Controlar permisos y acceso | `GRANT` |

---

# Parte B · Caso guiado

## Caso

Una clínica gestiona información de **pacientes, médicos y citas** utilizando hojas de cálculo separadas.

### 1. Identifica 4 problemas del enfoque por archivos.

Menciona cuatro problemas que podrían presentarse al administrar la información mediante hojas de cálculo separadas.

- Redundancia de datos.
- Inconsistencia de información.
- Dificultad para compartir información.
- Problemas de seguridad.
- Problemas de concurrencia.
- Dificultad para realizar consultas complejas.

### 2. Propón cómo un SGBD reduce la redundancia e inconsistencia.

Explica cómo el uso de una base de datos centralizada y un SGBD puede ayudar a evitar que la misma información sea almacenada varias veces y mantener los datos consistentes.

### 3. Define dos vistas externas distintas.

#### Vista de recepción

Puede contener:

- Datos básicos del paciente.
- Información de contacto.
- Médico asignado.
- Fecha y hora de la cita.
- Estado de la cita.

#### Vista de dirección médica

Puede contener:

- Cantidad de pacientes atendidos.
- Médicos.
- Citas programadas.
- Citas atendidas.
- Información estadística.

### 4. Menciona 3 restricciones de acceso por rol.

| Rol | Restricción de acceso |
|---|---|
| Recepción | Puede registrar y consultar citas, pero no administrar usuarios. |
| Médico | Puede consultar información de sus pacientes, pero no administrar usuarios. |
| Dirección médica | Puede consultar reportes y estadísticas, pero no modificar directamente los datos de pacientes. |

---

# Parte C · Aplicación

## 1. Arquitectura ANSI/SPARC para el caso clínica

```text
                 USUARIOS
                    │
        ┌───────────┴───────────┐
        │                       │
   RECEPCIÓN             DIRECCIÓN MÉDICA
        │                       │
        ▼                       ▼
┌───────────────────────────────────────┐
│          NIVEL EXTERNO                │
│       Vistas de los usuarios          │
└──────────────────┬────────────────────┘
                   │
                   ▼
┌───────────────────────────────────────┐
│         NIVEL CONCEPTUAL              │
│                                       │
│ PACIENTE ─── CITA ─── MÉDICO          │
│                                       │
│ Esquema lógico de toda la clínica     │
└──────────────────┬────────────────────┘
                   │
                   ▼
┌───────────────────────────────────────┐
│          NIVEL INTERNO                │
│                                       │
│ Tablas, índices, archivos y           │
│ estructuras de almacenamiento         │
└───────────────────────────────────────┘
