# Compensaciones

## 🎯 Objetivo

Añadir un mecanismo de **compensación** al proceso para revertir una operación cuando ocurre un problema en una etapa posterior.

---

## 🧠 Contexto

En muchos procesos de negocio existen operaciones que deben **deshacerse** si algo falla más adelante.

Ejemplos reales:

```
reservar producto
cobrar pago
confirmar pedido
```

Si el pago falla después de reservar el producto, el sistema debe **cancelar la reserva**.

Este patrón se llama:

```
Compensación
```

En BPMN las compensaciones permiten **ejecutar una acción inversa** para deshacer una operación anterior.

---

# Abrir el modelo BPMN

Abrir el archivo:

```
model/approval-process.bpmn
```

Editar el modelo con **Camunda Modeler**.

---

# Añadir una tarea compensable

Seleccionar la tarea:

```
Validar solicitud
```

Esta tarea representará una operación que puede necesitar ser revertida.

Añadir una nueva tarea llamada:

```
Registrar solicitud
```

Esta tarea simulará que la solicitud ha sido registrada en un sistema externo.

---

# Añadir la actividad de compensación

Añadir una nueva **Service Task** que represente la compensación.

Nombre:

```
Cancelar registro
```

Esta tarea representará la acción inversa.

---

# Marcar la tarea como compensable

Seleccionar la tarea:

```
Registrar solicitud
```

En el panel de propiedades activar:

```
Is For Compensation
```

Esto indica que la tarea puede ejecutarse como compensación.

---

# Añadir un Boundary Compensation Event

Añadir un **Boundary Event** a la tarea:

```
Registrar solicitud
```

Cambiar el tipo del evento a:

```
Compensation Event
```

Conectar este evento con la tarea:

```
Cancelar registro
```

---

# Flujo del proceso

El modelo debería representar un comportamiento similar a:

```
Registrar solicitud
       │
       ▼
Aprobar solicitud
       │
       ▼
Error en proceso
       │
       ▼
Compensación
       │
       ▼
Cancelar registro
```

---

# Guardar el modelo

Guardar el archivo:

```
model/approval-process.bpmn
```

Copiar el modelo al backend:

```bash
cp model/approval-process.bpmn backend/src/main/resources/processes/
```

---

# Implementar la lógica de compensación

Crear el archivo:

```
backend/src/main/java/com/example/workflow/delegate/CancelarRegistroDelegate.java
```

---

# Código del delegate

```java
package com.example.workflow.delegate;

import org.camunda.bpm.engine.delegate.DelegateExecution;
import org.camunda.bpm.engine.delegate.JavaDelegate;
import org.springframework.stereotype.Component;

@Component
public class CancelarRegistroDelegate implements JavaDelegate {

    @Override
    public void execute(DelegateExecution execution) {

        System.out.println("Ejecutando compensación: cancelando registro");

    }
}
```

---

# Configurar el delegate en el modelo

En la tarea:

```
Cancelar registro
```

Configurar:

```
Delegate Expression
```

Valor:

```
${cancelarRegistroDelegate}
```

---

# Ejecutar el proceso

Arrancar la aplicación:

```bash
cd backend
mvn spring-boot:run
```

Ejecutar el proceso hasta el punto en el que se dispare la compensación.

En la consola debería aparecer:

```
Ejecutando compensación: cancelando registro
```

---

# Qué ocurre internamente

Cuando el proceso dispara una compensación:

```
Actividad ejecutada
        │
        ▼
Evento de compensación
        │
        ▼
Camunda busca actividad compensatoria
        │
        ▼
Se ejecuta la tarea de compensación
```

Esto permite deshacer operaciones anteriores.

---

# Comprobación

El ejercicio se considera completado cuando:

* el proceso contiene un **Compensation Event**
* existe una tarea de compensación
* el delegate `CancelarRegistroDelegate` se ejecuta cuando se activa la compensación.
