# Verificar instalación de Java

## 🎯 Objetivo

Comprobar que el entorno dispone de **Java 17**, versión requerida para ejecutar la aplicación Spring Boot utilizada en el curso.

---

## 🧠 Contexto

Camunda 7 y Spring Boot necesitan una **JVM (Java Virtual Machine)** para ejecutar la aplicación.

En este curso utilizaremos:

```
Java 17
```

Antes de continuar es necesario verificar que Java está instalado correctamente en el entorno.

---

## 🔎 Verificar versión de Java

Abre una **terminal** en VS Code (menú **Terminal** → **New Terminal**, o atajo **Ctrl+ñ** / **Ctrl+`** según tu sistema). En la terminal ejecuta:

```bash
java -version
```

---

## 📌 Resultado esperado

El comando debería mostrar una salida similar a:

```text
openjdk version "17.x.x"
OpenJDK Runtime Environment
OpenJDK 64-Bit Server VM
```

Lo importante es que aparezca:

```
version "17"
```

---

## 🔎 Verificar el compilador Java

También es recomendable comprobar que el compilador está disponible.

Ejecutar:

```bash
javac -version
```

---

## 📌 Resultado esperado

```text
javac 17.x.x
```

---

## ⚠️ Si la versión no es correcta

Si la versión mostrada no es **Java 17**, será necesario instalar o configurar la versión adecuada antes de continuar con los siguientes laboratorios.

En entornos como **GitHub Codespaces** normalmente Java ya viene instalado correctamente.

---

## ✅ Comprobación final

Si los siguientes comandos funcionan correctamente:

```bash
java -version
javac -version
```

y muestran **Java 17**, el entorno está listo para continuar con el siguiente paso.
