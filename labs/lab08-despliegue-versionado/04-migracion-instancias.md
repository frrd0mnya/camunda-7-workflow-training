# Migración de instancias de proceso

## 🎯 Objetivo

Migrar una instancia de proceso que está ejecutándose en una **versión antigua** hacia una **versión más reciente del proceso**.

---

## 🧠 Contexto

Cuando se despliega una nueva versión de un proceso:

```
approval-process:1
approval-process:2
approval-process:3
```

Las instancias ya iniciadas continúan ejecutándose en la versión con la que fueron creadas.

Sin embargo, Camunda permite **migrar manualmente una instancia** hacia una nueva versión del proceso.

Esto se utiliza cuando:

* se corrigen errores en el proceso
* se añade nueva lógica
* se desea continuar una instancia con la definición más reciente

---

# Ver las instancias activas

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

Abrir la versión más reciente del proceso.

---

# Localizar una instancia antigua

Ir a:

```
Process Instances
```

Buscar una instancia que esté ejecutándose en una versión anterior.

Por ejemplo:

```
Version 1
```

Abrir la instancia.

---

# Abrir la herramienta de migración

En la pantalla de la instancia seleccionar:

```
Migrate Process Instance
```

Esto abrirá el asistente de migración.

---

# Seleccionar la versión destino

Elegir la nueva versión del proceso.

Por ejemplo:

```
approval-process:3
```

Camunda mostrará un mapa de las actividades del proceso antiguo con las del proceso nuevo.

---

# Verificar el mapeo de actividades

El asistente mostrará cómo se corresponden las tareas entre versiones.

Por ejemplo:

```
Validar solicitud  →  Validar solicitud
Aprobar solicitud  →  Revisión final de la solicitud
```

Si las actividades tienen el mismo **id BPMN**, la migración se puede realizar automáticamente.

---

# Ejecutar la migración

Confirmar la operación.

Camunda actualizará la instancia para que utilice la nueva definición del proceso.

---

# Verificar el resultado

Volver a la vista de la instancia.

Ahora debería aparecer:

```
Process Definition Version = 3
```

La instancia continuará ejecutándose en la nueva versión.

---

# Qué ocurre internamente

Durante la migración:

```
Instancia del proceso
        │
        ▼
referencia a Process Definition
        │
        ▼
se actualiza a nueva versión
        │
        ▼
la instancia continúa en el nuevo modelo
```

El estado del proceso se mantiene, pero la definición BPMN utilizada cambia.

---

# Limitaciones de la migración

La migración solo es posible cuando:

* las actividades existen en ambas versiones
* los identificadores BPMN coinciden
* el estado del proceso es compatible

Si el proceso cambia demasiado, la migración puede no ser posible.

---

# Comprobación

El ejercicio se considera completado cuando:

* se localiza una instancia en una versión antigua
* se ejecuta la herramienta de migración
* la instancia pasa a utilizar la nueva versión del proceso.
