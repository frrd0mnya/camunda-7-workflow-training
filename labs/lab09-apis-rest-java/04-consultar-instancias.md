# Consultar instancias de proceso

## 🎯 Objetivo

Consultar las **instancias de proceso activas** utilizando la API REST de Camunda.

---

## 🧠 Contexto

Cuando un proceso BPMN se ejecuta, Camunda crea una **Process Instance**.

Cada instancia representa una ejecución concreta del proceso.

Estas instancias pueden consultarse mediante:

```
RuntimeService (API Java)
REST API
Cockpit
```

En este ejercicio se utilizará la **REST API** para consultar instancias activas.

---

# Listar instancias activas

Arrancar la aplicación:

```bash
cd backend
mvn spring-boot:run
```

Consultar las instancias activas usando **curl**:

```bash
curl http://localhost:8081/engine-rest/process-instance
```

---

# Respuesta de la API

La API devolverá un JSON con las instancias activas.

Ejemplo:

```json
[
  {
    "id": "c2c1c9f1-8e9b-11ee-9c7b-0242ac120002",
    "definitionId": "approval-process:3:4f3e8a21-8e9b-11ee-9c7b-0242ac120002",
    "businessKey": null,
    "caseInstanceId": null,
    "ended": false,
    "suspended": false,
    "tenantId": null
  }
]
```

Cada objeto representa una instancia del proceso.

---

# Filtrar por proceso

Para consultar únicamente instancias del proceso:

```
approval-process
```

Utilizar el parámetro:

```
processDefinitionKey
```

Ejemplo:

```bash
curl "http://localhost:8081/engine-rest/process-instance?processDefinitionKey=approval-process"
```

---

# Ver variables de una instancia

Copiar el **id de la instancia** devuelto por la API.

Consultar sus variables:

```bash
curl http://localhost:8081/engine-rest/process-instance/{id}/variables
```

Ejemplo:

```bash
curl http://localhost:8081/engine-rest/process-instance/123456/variables
```

Respuesta:

```json
{
  "solicitante": {
    "type": "String",
    "value": "maria"
  },
  "importe": {
    "type": "Integer",
    "value": 3000
  },
  "tipoSolicitud": {
    "type": "String",
    "value": "compra"
  }
}
```

---

# Ver instancias en Cockpit

Abrir:

```
http://localhost:8081/camunda
```

Ir a:

```
Processes → approval-process
```

En la sección:

```
Process Instances
```

Se pueden visualizar las mismas instancias que devuelve la API.

---

# Qué ocurre internamente

Cuando se consulta el endpoint:

```
/engine-rest/process-instance
```

Camunda ejecuta internamente una consulta equivalente a:

```
RuntimeService.createProcessInstanceQuery()
```

Esto permite recuperar el estado actual de las instancias activas.

---

# Comprobación

El ejercicio se considera completado cuando:

* se consulta la API `/process-instance`
* se obtiene un listado de instancias activas
* se pueden consultar las variables de una instancia concreta.
