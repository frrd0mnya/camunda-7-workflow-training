# Verificar instalación de Maven

## 🎯 Objetivo

Comprobar que **Maven** está instalado y disponible en el entorno para poder compilar y ejecutar el proyecto.

---

## 🧠 Contexto

Durante el curso utilizaremos **Maven** para:

* gestionar dependencias
* compilar el proyecto
* ejecutar la aplicación Spring Boot
* empaquetar la aplicación

El archivo principal de configuración de Maven es:

```id="w9f5wr"
pom.xml
```

Este archivo define:

* dependencias del proyecto
* versión de Java
* plugins de compilación
* configuración de construcción

---

## 🔎 Verificar instalación de Maven

Abre una **terminal** en VS Code (menú **Terminal** → **New Terminal**). Desde esa terminal ejecuta:

```bash id="y5z6dd"
mvn -v
```

---

## 📌 Resultado esperado

El comando debería mostrar una salida similar a:

```text id="9llfyz"
Apache Maven 3.x.x
Maven home: /usr/share/maven
Java version: 17
Default locale: en_US
OS name: linux
```

Es importante comprobar que aparecen:

```id="p5m5v8"
Apache Maven 3
Java version: 17
```

---

## 🔎 Qué información muestra Maven

La salida del comando incluye información útil sobre el entorno:

| Información      | Significado                 |
| ---------------- | --------------------------- |
| Versión de Maven | herramienta de construcción |
| Java version     | JVM utilizada por Maven     |
| Maven home       | ubicación de Maven          |
| OS name          | sistema operativo           |

---

## ⚠️ Posibles problemas

Si el comando muestra:

```text id="w2v1lu"
command not found
```

significa que Maven no está instalado o no está en el **PATH** del sistema.

En entornos como **GitHub Codespaces** normalmente Maven ya viene instalado.

---

## ✅ Comprobación final

Si el comando:

```bash id="9hqddu"
mvn -v
```

muestra correctamente la versión de Maven y Java 17, el entorno está listo para continuar con el siguiente paso.
