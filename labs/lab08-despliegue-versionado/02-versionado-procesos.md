# Versionado de procesos

## 🎯 Objetivo

Comprender cómo **Camunda gestiona automáticamente las versiones de un proceso** cuando se despliega un modelo BPMN actualizado.

---

## 🧠 Contexto

En Camunda cada vez que se despliega un proceso con el mismo **Process Definition Key**, el motor crea automáticamente **una nueva versión del proceso**.

Por ejemplo:

```
Process Key: approval-process
```

Versiones posibles:

```
approval-process:1
approval-process:2
approval-process:3
```

Las instancias nuevas siempre utilizarán **la última versión desplegada**.

Las instancias antiguas continúan ejecutándose con **la versión con la que fueron creadas**.

Esto permite actualizar procesos sin interrumpir instancias ya en ejecución.

---

# Ver la versión actual del proceso

Abrir **Camunda Cockpit**:

```
http://localhost:8081/camunda
```

Ir a:

```
Processes
```

Seleccionar:

```
approval-process
```

En la pantalla del proceso se mostrará el número de versión actual.

Ejemplo:

```
Version 1
```

---

# Modificar el modelo BPMN

Abrir el archivo:

```
model/approval-process.bpmn
```

Modificar el modelo para generar una nueva versión.

Por ejemplo:

Cambiar el nombre de la tarea:

```
Aprobar solicitud
```

por

```
Revisar y aprobar solicitud
```

Guardar el archivo.

---

# Desplegar la nueva versión

Copiar el modelo actualizado al backend:

```bash
cp model/approval-process.bpmn backend/src/main/resources/processes/
```

Reiniciar la aplicación.

```bash
cd backend
mvn spring-boot:run
```

Durante el arranque Camunda detectará que el proceso ya existe y creará **una nueva versión**.

---

# Verificar la nueva versión en Cockpit

Abrir:

```
http://localhost:8081/camunda
```

Ir a:

```
Processes
```

Seleccionar:

```
approval-process
```

Ahora debería aparecer:

```
Version 2
```

---

# Ver todas las versiones

En la pantalla del proceso existe un selector de versiones.

Aquí se pueden ver:

```
Version 1
Version 2
```

Cada versión corresponde a un despliegue distinto.

---

# Probar el comportamiento

Iniciar una nueva instancia del proceso.

Esta instancia utilizará automáticamente:

```
Version 2
```

Las instancias que ya estaban ejecutándose seguirán utilizando:

```
Version 1
```

---

# Qué ocurre internamente

Cuando se despliega un proceso actualizado:

```
Nuevo BPMN desplegado
        │
        ▼
Camunda detecta mismo Process Key
        │
        ▼
Incrementa número de versión
        │
        ▼
Nuevas instancias usan la versión más reciente
```

---

# Comprobación

El ejercicio se considera completado cuando:

* el proceso muestra **más de una versión en Cockpit**
* el motor asigna automáticamente un número de versión
* nuevas instancias utilizan la última versión desplegada.
