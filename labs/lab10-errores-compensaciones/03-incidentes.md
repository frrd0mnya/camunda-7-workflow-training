# Incidentes en el motor de procesos

## 🎯 Objetivo

Explorar cómo Camunda detecta **incidentes** cuando un Job falla repetidamente y aprender a inspeccionar y resolver estos problemas desde Cockpit.

---

## 🧠 Contexto

En el ejercicio anterior se provocó un **fallo técnico** en una Service Task.

Cuando una tarea asíncrona falla, Camunda aplica el siguiente mecanismo:

```id="m3l1eh"
ejecutar Job
si falla → retries--
si retries > 0 → reintentar
si retries = 0 → crear incidente
```

Un **Incident** indica que el proceso no puede continuar hasta que el problema sea solucionado.

---

# Ejecutar el proceso con el fallo

Arrancar la aplicación:

```bash id="tvdfgt"
cd backend
mvn spring-boot:run
```

El proceso se iniciará y llegará a la tarea:

```
Validar solicitud
```

El `JavaDelegate` lanzará una excepción y el Job fallará.

Después de agotar los retries, el motor creará un **Incident**.

---

# Abrir Cockpit

Abrir el navegador:

```
http://localhost:8081/camunda
```

Entrar en **Cockpit**.

---

# Localizar el incidente

Ir a:

```
Processes
```

Seleccionar:

```
approval-process
```

Abrir una instancia activa.

El diagrama BPMN mostrará un indicador rojo en la tarea donde ocurrió el fallo.

Esto indica que existe un **Incident**.

---

# Explorar el incidente

Seleccionar la actividad con el error.

Cockpit mostrará información como:

```
Incident Type: failedJob
Configuration: jobId
Message: Fallo técnico en validación
```

Esto permite identificar el origen del problema.

---

# Ver los Jobs fallidos

Ir a la sección:

```
Jobs
```

Aquí se pueden observar:

```
Job ID
Retries
Exception Message
```

Los Jobs con `retries = 0` generan incidentes.

---

# Resolver el incidente

Para resolver el incidente se puede:

1. **corregir el error en el código**
2. volver a desplegar la aplicación
3. aumentar los retries del Job

En Cockpit seleccionar el Job y modificar:

```
Retries
```

Por ejemplo:

```
Retries = 1
```

Esto permitirá que el motor vuelva a intentar ejecutar la tarea.

---

# Modificar el código para eliminar el fallo

Abrir:

```
ValidarSolicitudDelegate.java
```

Eliminar la excepción:

```java
throw new RuntimeException("Fallo técnico en validación");
```

Reemplazar por:

```java
System.out.println("Validación completada correctamente");
```

---

# Reiniciar la aplicación

```bash id="nq2hdy"
cd backend
mvn spring-boot:run
```

El Job volverá a ejecutarse y el proceso continuará.

---

# Qué ocurre internamente

Cuando un Job falla definitivamente:

```
RuntimeException
       │
       ▼
Retries = 0
       │
       ▼
Camunda crea Incident
       │
       ▼
Proceso detenido
```

Cuando se corrige el problema:

```
Retries actualizados
       │
       ▼
Job reejecutado
       │
       ▼
Proceso continúa
```

---

# Comprobación

El ejercicio se considera completado cuando:

* el proceso genera un **Incident**
* el incidente aparece en **Cockpit**
* se corrige el error
* el proceso continúa después de reintentar el Job.
