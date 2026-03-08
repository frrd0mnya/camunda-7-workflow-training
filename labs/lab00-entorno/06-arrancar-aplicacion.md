# Arrancar la aplicación

## 🎯 Objetivo

Ejecutar la aplicación **Spring Boot** para verificar que el backend se inicia correctamente.

---

## 🧠 Contexto

La aplicación backend contiene:

* el motor de procesos **Camunda**
* la aplicación **Spring Boot**
* la configuración del proyecto

Al arrancar la aplicación se iniciará:

* servidor web
* motor Camunda
* base de datos embebida

---

## 📍 Ir al directorio del backend

Abre una **terminal** en VS Code (menú **Terminal** → **New Terminal**). Desde la **raíz del repositorio** (donde están README, **labs** y **backend**), ejecuta:

```bash
cd backend
```

---

## ▶️ Ejecutar la aplicación

Ejecutar el siguiente comando:

```bash
mvn spring-boot:run
```

---

## 📦 Qué ocurre al arrancar

Durante el arranque se inicializan varios componentes:

* Spring Boot Application
* Camunda Process Engine
* Base de datos H2
* Servidor web embebido

En la terminal aparecerán mensajes de inicio del sistema.

---

## 📌 Puerto de ejecución

La aplicación se ejecutará en el puerto:

```
8080
```

---

## 🔎 Verificar que la aplicación está funcionando

Abre un **navegador** y en la barra de direcciones escribe:

```
http://localhost:8080
```

Si la aplicación está en ejecución el servidor responderá a las peticiones.

---

## ⚠️ Detener la aplicación

Para detener la aplicación desde la terminal presionar:

```
CTRL + C
```

---

## ✅ Comprobación

El paso se considera completado cuando:

* el comando `mvn spring-boot:run` inicia la aplicación sin errores
* el servidor arranca correctamente
* la terminal muestra que la aplicación está escuchando en el puerto **8080**.
