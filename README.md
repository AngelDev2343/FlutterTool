# 🛠️ FlutterTool

![Plataforma](https://img.shields.io/badge/plataforma-Windows-blue)
![Sin admin](https://img.shields.io/badge/UAC-no%20requerido-brightgreen)
![Java](https://img.shields.io/badge/Java-21%20OpenJDK-orange)
![Flutter](https://img.shields.io/badge/Flutter-stable-02569B?logo=flutter)
![Android SDK](https://img.shields.io/badge/Android%20SDK-36-green?logo=android)

**FlutterTool** es un script `.bat` para Windows que instala y configura automáticamente todo el entorno de desarrollo Flutter — incluyendo Java, Flutter SDK y Android SDK — **sin necesitar permisos de administrador (UAC)**.

Ideal para equipos de cómputo escolares, laboratorios o cualquier máquina donde no se tenga acceso a una cuenta administradora.

---

## 🚀 Instalación

> Nota: si intentaste instalar Flutter/Android Studio, elimina todo rastro de estos, incluyendo el PATH y ANDROID HOME de variables de entorno.

1. Abrir tu IDE de preferencia (Ej. VS Code)
2. Abre una nueva terminal
3. Copia y pega (en una sola linea) el siguiente comando:
   
   **powershell**
   ```
   irm https://raw.githubusercontent.com/AngelSPerez/flutter-instalacion/main/flutter-script.bat -OutFile setup.bat; Unblock-File setup.bat; .\setup.bat
   ```
5. Espera y listo, tendras Flutter instalado y funcionando con todo lo necesario para empezar.

## 📦 Instalación alternativa

1. Descarga el script de [AQUÍ](https://github.com/AngelDev2343/FlutterTool/releases/download/v1.0/FlutterTool.bat)
2. Ejecutar con doble clic
3. Esperar y listo, tendras Flutter instalado y funcionando con todo lo necesario para empezar.

---

## ✨ ¿Qué hace?

Con un solo doble clic, el script realiza los siguientes pasos de forma automática:

| Paso | Acción |
|------|--------|
| 1️⃣ | Descarga e instala **Java 21 OpenJDK** (Adoptium) en `%USERPROFILE%\Java` |
| 2️⃣ | Configura `JAVA_HOME` y actualiza el `PATH` de usuario |
| 3️⃣ | Descarga la versión **stable más reciente de Flutter** automáticamente |
| 4️⃣ | Agrega Flutter al `PATH` de usuario |
| 5️⃣ | Descarga e instala **Android SDK commandline-tools** |
| 6️⃣ | Configura `ANDROID_HOME`, `ANDROID_SDK_ROOT` y `PATH` Android |
| 7️⃣ | Instala componentes del SDK: `platform-tools`, `android-36`, `build-tools;28.0.3` |
| ✅ | Acepta licencias y ejecuta `flutter doctor` |

---

## 🔒 Sin permisos de administrador

Todo se instala dentro del perfil del usuario de Windows (`%USERPROFILE%`), por lo que **no se requiere UAC** ni cuenta de administrador en ningún momento.

```
%USERPROFILE%\
├── Java\
│   └── jdk-21\          ← Java 21 OpenJDK
├── flutter\             ← Flutter SDK
└── Android\
    └── Sdk\             ← Android SDK
        ├── cmdline-tools\
        ├── platform-tools\
        └── platforms\
```

---

## 🛡️ Manejo de errores

El script verifica la integridad de cada archivo ZIP antes de extraerlo. Si un archivo está corrupto o la descarga falló, lo elimina y muestra un mensaje claro antes de abortar, evitando instalaciones a medias.

Los casos cubiertos incluyen:

- ZIP de Java corrupto o descarga fallida
- ZIP de Flutter corrupto, descarga o extracción fallida
- ZIP del Android SDK corrupto o descarga fallida
- `sdkmanager` no responde

---

## 🔁 Reanudación inteligente

Si el script ya fue ejecutado anteriormente, detecta automáticamente qué componentes ya están instalados y los omite, evitando re-descargas innecesarias:

- Si `jdk-21\bin\java.exe` ya existe → omite Java
- Si `flutter` ya está en el `PATH` → omite Flutter
- Si `sdk.zip` ya existe y está íntegro → lo reutiliza

---

## 📋 Requisitos previos

- Windows 10 / 11 (64 bits)
- Conexión a Internet
- `curl.exe` disponible (incluido por defecto en Windows 10 desde 2018)
- `tar.exe` disponible (incluido por defecto en Windows 10 1803+)
- PowerShell (incluido en Windows)

> No se requiere ninguna instalación previa de Java, Flutter ni Android Studio.

---

## 📦 Componentes instalados

| Componente | Versión | Fuente |
|------------|---------|--------|
| Java OpenJDK | 21 (LTS) | [Adoptium](https://adoptium.net) |
| Flutter | Última stable | [flutter.dev](https://flutter.dev) |
| Android SDK cmdline-tools | 11076708 | Google |
| Android platform | android-36 | Google |
| Android build-tools | 28.0.3 | Google |
| Android platform-tools (adb) | Última | Google |

---

## ⚠️ Notas importantes

- Al finalizar, **reinicia la terminal** para que el `PATH` actualizado sea reconocido.
- Si `adb` no se detecta inmediatamente después de la instalación, es normal: reiniciar la terminal lo soluciona.
- El script limpia descargas temporales (`.zip`) una vez extraídas correctamente.
- Las variables de entorno se configuran a nivel de **usuario**, no de sistema, por lo que no afectan a otros usuarios de la máquina.

---
