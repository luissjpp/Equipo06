# Equipo 06 — Esquema relacional del proyecto

**Dominio de negocio:**

**Integrantes:**
Rodríguez Prado Isaac
Contreras Luna David
Ochoa Murillo Santiago Daniel
Perez Juarez Luis Javier

**Enlace al diagrama E/R del jueves 17** (dbdiagram.io, Mermaid o archivo en el repositorio del proyecto):

---

## 1. Esquema relacional
PLAN(**id_plan**, nombre_plan UNIQUE, costo_mensual)

SOCIO(**num_socio**, nombre, fecha_nacimiento, correo, id_plan → PLAN)

TELEFONO_SOCIO(**num_socio** → SOCIO, **telefono**)

LOCKER(**num_locker**, ubicacion, num_socio? UNIQUE → SOCIO)

INSTRUCTOR(**num_empleado**, nombre, especialidad, num_supervisor? → INSTRUCTOR)

CLASE(**id_clase**, nombre, cupo_maximo, num_empleado → INSTRUCTOR)

SESION(**id_clase** → CLASE, **num_sesion**, fecha, hora_inicio, salon)

INSCRIPCION(**num_socio** → SOCIO, **id_clase** → CLASE, **fecha_inscripcion**, estatus)
<!-- Transformen su E/R completo con la notación de guias/notacion.md.
     Todas las tablas, todas las PK, todas las FK y el ? donde corresponda. -->

```

```


## 2. Relaciones N:M y cómo las resolvieron

| Relación en el E/R | Tabla intermedia | Llave primaria de la tabla intermedia | ¿Se puede repetir la misma pareja? ¿Por qué? |
|---|---|---|---|
| SOCIO – CLASE | INSCRIPCION | (num_socio, id_clase, fecha_inscripcion) | Sí, pero con distinta fecha un socio puede darse de baja de una clase y volver a inscribirse meses después, entonces la pareja socio-clase se repite

## 3. Relaciones 1:1, recursivas, débiles y multivaluados

| Caso | Dónde aparece en su E/R | Cómo lo resolvieron |
|---|---|---|
| Relación 1:1 | SOCIO – LOCKER | Pusimos la FK num_socio en LOCKER, con UNIQUE y admite NULL. Así un socio no puede tener dos lockers y los lockers libres quedan vacíos. |
| Relación recursiva | INSTRUCTOR – INSTRUCTOR | Una columna num_supervisor en la misma tabla INSTRUCTOR que apunta a num_empleado asi admite NULL por la coordinadora general, que no tiene supervisor. |
| Entidad débil | SESION | Su llave primaria es (id_clase, num_sesion). id_clase es FK a CLASE, porque una sesión no se identifica sin su clase. |
| Atributo multivaluado | Teléfonos del socio | Se hizo la tabla TELEFONO_SOCIO con llave (num_socio, telefono), una fila por cada teléfono. |

## 4. Llaves foráneas que admiten NULL

| Tabla.columna | Por qué puede quedar vacía |
|---|---|
| LOCKER.num_socio | Hay lockers libres que nadie ha rentado. |
| INSTRUCTOR.num_supervisor | La coordinadora general no tiene supervisor. |

## 5. Cambios respecto el E/R del jueves
