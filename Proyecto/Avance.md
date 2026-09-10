# Clínica Odontológica "Sonríe Odontología Integral"

# 1. Descripción del problema o problemática

La clínica odontológica presenta dificultades en la organización y control de la información relacionada con la programación de citas y la atención de los pacientes. Actualmente, el registro de los datos puede realizarse de manera manual o mediante diferentes medios, lo que dificulta mantener la información centralizada y consultarla de forma rápida.

Uno de los principales problemas se encuentra en la gestión de las citas, debido a que es necesario controlar la fecha, hora, paciente, consultorio, motivo y estado de cada cita, además de identificar al usuario encargado de registrarla y al odontólogo responsable de atenderla.

Asimismo, existe la necesidad de registrar adecuadamente las atenciones realizadas, incluyendo los diagnósticos y tratamientos aplicados. La información de las diferentes consultas debe mantenerse relacionada con el historial clínico de cada paciente para facilitar el seguimiento de sus atenciones anteriores.

También se requiere organizar la información de los tratamientos y sus costos, así como registrar los pagos realizados por las atenciones y los métodos de pago utilizados. La falta de una estructura centralizada puede ocasionar pérdida o duplicidad de información, dificultades para consultar el historial de los pacientes y problemas en el seguimiento de las citas y atenciones odontológicas.

Por estas razones, se plantea el diseño de una base de datos que permita gestionar de manera organizada las citas, pacientes, consultorios y usuarios, además de registrar las atenciones odontológicas, diagnósticos, tratamientos e información relacionada con los pagos.

# 2. Preguntas y respuestas de la entrevista

### 1. ¿Cómo registran actualmente las citas de los pacientes?

Actualmente las citas las vamos anotando de forma manual, principalmente en una agenda y, en algunos casos, en el celular. Ahí vamos colocando la fecha, hora y nombre del paciente.

### 2. ¿Qué información solicitan cuando un paciente quiere sacar una cita?

Normalmente pedimos el nombre del paciente, número de teléfono, el motivo de la consulta y el día y hora que desea. Si es un paciente que ya conocemos, también revisamos sus datos anteriores.

### 3. ¿Quién se encarga de registrar las citas?

Generalmente la persona que está encargada de la atención en ese momento es quien anota la cita. Dependiendo del día, puede hacerlo la recepción o alguno de los doctores.

### 4. ¿Un paciente puede tener más de una cita?

Sí, claro. Un paciente puede venir varias veces, dependiendo del tratamiento que necesite. Por ejemplo, puede tener una cita para una revisión y después otras para continuar con su tratamiento.

### 5. ¿Cómo saben qué doctor atenderá al paciente?

Lo coordinamos de acuerdo con la disponibilidad del doctor y el tipo de atención que necesita el paciente. Normalmente lo anotamos junto con la cita para saber quién estará encargado.

### 6. ¿Cómo asignan el consultorio para cada cita?

Se revisa qué consultorio está disponible y se coordina con el doctor que atenderá. Esto normalmente lo tenemos presente en la agenda o lo comunicamos entre nosotros.

### 7. ¿Qué pasa cuando un paciente cancela o no se presenta?

Cuando cancela, simplemente anotamos que la cita fue cancelada y, si desea, se le busca otro horario. Si no se presenta, normalmente lo registramos en la agenda para tenerlo en cuenta.

### 8. ¿Qué información registran cuando se atiende a un paciente?

Anotamos los datos más importantes de la atención, como el motivo por el que vino, lo que se encontró durante la revisión, el diagnóstico y el tratamiento que se realizó o que se recomienda.

### 9. ¿Cómo registran actualmente los diagnósticos?

Los diagnósticos se anotan de manera manual en las fichas o registros del paciente. Dependiendo de la atención, se pueden registrar uno o varios diagnósticos.

### 10. ¿Un paciente puede recibir varios tratamientos durante una misma consulta?

Sí. En una misma consulta se puede realizar más de un procedimiento o tratamiento, dependiendo de lo que necesite el paciente.

### 11. ¿Cómo llevan el historial de los pacientes?

Tenemos los datos y antecedentes en registros físicos y fichas de los pacientes. Cuando vuelve una persona, buscamos su información para revisar lo que se le realizó anteriormente.

### 12. ¿Qué información guardan sobre los tratamientos?

Principalmente anotamos qué tratamiento se realizó, la cantidad o las veces que se realizó y algunas observaciones relacionadas con la atención.

### 13. ¿El costo de un tratamiento puede cambiar con el tiempo?

Sí, los precios pueden cambiar. Por eso es importante saber cuánto costaba el tratamiento en el momento en que se atendió al paciente y no solamente tener el precio actual.

### 14. ¿Cómo registran actualmente los pagos?

Los pagos se registran de manera manual. Normalmente anotamos cuánto pagó el paciente y lo relacionamos con la atención que recibió.

### 15. ¿Qué métodos de pago reciben?

Recibimos principalmente efectivo, tarjeta, QR y transferencia, dependiendo de la disponibilidad y de lo que prefiera el paciente.

### 16. ¿Permiten realizar pagos parciales?

Actualmente, por lo general, se trata de completar el pago correspondiente a la atención. Si se presenta algún caso diferente, se coordina directamente con el paciente.

### 17. ¿Quiénes necesitan consultar la información de los pacientes?

Principalmente los doctores y la persona encargada de la atención o administración, porque necesitan consultar las citas, los datos del paciente y la información de las atenciones anteriores.

### 18. ¿Qué información sería importante poder consultar rápidamente?

Sería útil poder buscar rápidamente los datos del paciente, sus próximas citas, las consultas anteriores, los diagnósticos y tratamientos que recibió, además de los pagos realizados.

### 19. ¿Qué problemas tienen actualmente al trabajar de esta manera?

El principal problema es que la información está distribuida entre agendas, fichas y anotaciones. A veces cuesta encontrar rápidamente los datos de un paciente o saber qué se hizo en una consulta anterior. También puede ser difícil llevar un control ordenado de las citas y los pagos.

### 20. ¿Qué espera obtener con un sistema para la clínica?

Esperamos poder tener toda la información más organizada en un solo lugar, poder consultar los datos de los pacientes y sus historiales con mayor facilidad, controlar mejor las citas y tener un registro más ordenado de las consultas, tratamientos y pagos.


# 3. Diseño de la solución

### Entidades y atributos

**ROL:** ID_ROL, NOMBRE_ROL

**USUARIO:** ID_USUARIO, NOMBRE, APELLIDO, NOMBRE_USUARIO, CLAVE, ESTADO_CLAVE

**PACIENTE:** ID_PACIENTE, CI/NIT, NOMBRE, APELLIDO, TELEFONO, EMAIL

**HISTORIAL_CLINICO:** ID_HISTORIAL, FECHA_APERTURA, OBSERVACIONES

**CONSULTORIO:** ID_CONSULTORIO, NOMBRE, DESCRIPCION, ESTADO

**CITA:** ID_CITA, FECHA, HORA, MOTIVO, ESTADO

**CONSULTA:** ID_CONSULTA, FECHA, HORA, DIAGNOSTICO_GENERAL

**DIAGNOSTICO:** ID_DIAGNOSTICO, NOMBRE, DESCRIPCION

**CONSULTA_DIAGNOSTICO:** OBSERVACIONES

**TRATAMIENTO:** ID_TRATAMIENTO, NOMBRE, DESCRIPCION, COSTO

**CONSULTA_TRATAMIENTO:**  CANTIDAD, COSTO_UNITARIO, SUBTOTAL, OBSERVACION

**METODO_PAGO:** ID_METODO_PAGO, NOMBRE, DESCRIPCION, ESTADO

**PAGO:** ID_PAGO, FECHA_PAGO, MONTO, ESTADO, OBSERVACION




# 4. Uniones o cardinalidades

ROL -> USUARIO (1,N)

PACIENTE -> HISTORIAL_CLINICO (1,1)

PACIENTE -> CITA (1,N)

USUARIO -> CITA (1,N) [AGENDA]

USUARIO -> CITA (1,N) [ATIENDE]

CONSULTORIO -> CITA (1,N)

CITA -> CONSULTA (1,0..1)

HISTORIAL_CLINICO -> CONSULTA (1,N)

CONSULTA -> DIAGNOSTICO (N,N)

CONSULTA -> CONSULTA_DIAGNOSTICO (1,N)

DIAGNOSTICO -> CONSULTA_DIAGNOSTICO (1,N)

CONSULTA -> TRATAMIENTO (N,N)

CONSULTA -> CONSULTA_TRATAMIENTO (1,N)

TRATAMIENTO -> CONSULTA_TRATAMIENTO (1,N)

CONSULTA -> PAGO (1,0..1)

METODO_PAGO -> PAGO (1,N)

# Relaciones N:N

La relación entre **CONSULTA y DIAGNOSTICO** es de muchos a muchos y se resuelve mediante **CONSULTA_DIAGNOSTICO**.

La relación entre **CONSULTA y TRATAMIENTO** es de muchos a muchos y se resuelve mediante **CONSULTA_TRATAMIENTO**.

# Atributos calculados

El **SUBTOTAL** de CONSULTA_TRATAMIENTO se obtiene mediante:

**SUBTOTAL = CANTIDAD × COSTO_APLICADO**

El **TOTAL de una consulta** se obtiene mediante la suma de los subtotales de los tratamientos asociados a dicha consulta:

**TOTAL = SUMA(SUBTOTAL)**

Estos valores pueden calcularse mediante consultas SQL y no necesariamente necesitan almacenarse físicamente en la base de datos.

* ![Diagrama Entidad-Relación](../diagrama.png)
