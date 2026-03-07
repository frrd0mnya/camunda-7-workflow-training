# REST API de Camunda

## 🎯 Objetivo

Utilizar la **REST API de Camunda** para iniciar procesos y consultar información del motor desde herramientas externas.

---

## 🧠 Contexto

Además de la API Java, Camunda expone una **API REST completa** que permite interactuar con el motor desde:

* aplicaciones externas
* microservicios
* scripts
* herramientas como Postman o curl

La API REST está disponible cuando se utiliza:

```
camunda-bpm-spring-boot-starter-webapp
```

El endpoint base suele ser:

```
/engine-rest
```

---

# Verificar que la API REST está disponible

Arrancar la aplicación:

```bash
cd backend
mvn spring-boot:run
```

Abrir el navegador:

```
http://localhost:8081/engine-rest
```

Si la API está activa aparecerá una respuesta JSON o la documentación básica.

---

# Iniciar un proceso mediante REST

Enviar una petición HTTP POST al endpoint:

```
/engine-rest/process-definition/key/approval-process/start
```

Ejemplo usando **curl**:

```bash
curl -X POST \
http://localhost:8081/engine-rest/process-definition/key/approval-process/start \
-H "Content-Type: application/json" \
-d '{
  "variables": {
    "solicitante": { "value": "carlos", "type": "String" },
    "importe": { "value": 1500, "type": "Integer" },
    "tipoSolicitud": { "value": "compra", "type": "String" }
  }
}'
```

---

# Qué devuelve la API

La respuesta será similar a:

```
{
  "id": "aProcessInstanceId",
  "definitionId": "approval-process:3:12345",
  "businessKey": null,
  "caseInstanceId": null,
  "ended": false,
  "suspended": false
}
```

Esto indica que se ha creado una **nueva instancia del proceso**.

---

# Ver la instancia en Cockpit

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

En **Process Instances** debería aparecer la nueva instancia creada mediante REST.

---

# Consultar instancias activas

También es posible consultar las instancias activas del proceso.

Ejemplo:

```bash
curl http://localhost:8081/engine-rest/process-instance
```

La respuesta mostrará todas las instancias activas.

---

# Consultar variables del proceso

Para consultar las variables de una instancia:

```
/engine-rest/process-instance/{id}/variables
```

Ejemplo:

```bash
curl http://localhost:8081/engine-rest/process-instance/{processInstanceId}/variables
```

Esto devolverá las variables almacenadas en esa instancia.

---

# Qué permite la REST API

La API REST permite controlar el motor sin utilizar Java.

Ejemplos de operaciones posibles:

```
iniciar procesos
consultar instancias
leer variables
completar tareas
enviar mensajes
gestionar deployments
```

Esto facilita la integración con otros sistemas.

---

# Comprobación

El ejercicio se considera completado cuando:

* la API REST responde en `/engine-rest`
* se inicia un proceso mediante `curl`
* la instancia aparece en **Camunda Cockpit**.
