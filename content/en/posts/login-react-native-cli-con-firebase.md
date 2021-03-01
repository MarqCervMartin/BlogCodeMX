+++
author = "Martín Márquez"
authorEmoji = "🤠"
categories = ["mobile", "react"]
date = 2021-02-28T04:00:00Z
description = "¿Cómo crear un login paso a paso con la ayuda de Firebase?, react native sin duda nos ayudara para nuestras aplicaciones móviles en Andriod/IOS."
enableToc = true
enableTocContent = false
hideToc = false
image = ""
pinned = true
series = []
tags = ["javascript", "react"]
title = "Login react native cli con Firebase"

+++
Hola coders, hoy realizaremos un login súper sencillo y práctico con firebase, en sus marcas listos fuera!

## Crear un proyecto de React Native.

Lo primero claro es seleccionar un lugar en donde nuestro proyecto se guardara, luego claro abrir nuestra poderosa terminal y escribir :

{{< tabs Windows MacOS Ubuntu >}}
{{< tab >}}

### Windows

```bash
npx react-native init factura
```

⚠️Según la documentación oficial: https://reactnative.dev/docs/environment-setup es recomendable instalarlo mediante npx y no directamente con reac-native ya que puede ocasionar problemas, en está ocasión le llamare factura a mi proyecto.

{{< /tab >}}
{{< tab >}}

### MacOS

```bash
npx react-native init factura
```

{{< /tab >}}
{{< tab >}}

### Ubuntu

```bash
npx react-native init factura
```

{{< /tab >}}
{{< /tabs >}}

### Componentes

Para nuestro Login necesitaremos crear una carpeta llamada components o componentes, en donde crearemos los siguientes archivos además de arrastrar nuestro App.js:

![](/uploads/blogreacfirebase-1.png)

Ahora bien deberemos cambiar nuestra ruta de App.js en nuestro index.js al importar nuestro componente principal App debemos cambiarla por nuestra nueva ruta:

``` javascript
import App from './components/App';
```

### Firebase

Una vez creado los archivos instalaremos firebase, pero antes debemos de crear un proyecto en https://firebase.google.com/

 1. Ir a Firebase y clickear Comenzar.

    ![](/uploads/blogreacfirebase-2.png)
 2. Añadir un proyecto.

    ![](/uploads/blogreacfirebase-3.png)
 3. Darle un nombre al proyecto.

    ![](/uploads/blogreacfirebase-4.png)
 4. Puedes o no añadir Google Analytics, en este caso lo habilitaré.

    ![](/uploads/blogreacfirebase-5.png)
 5. Seleccionar la ubicación.

    ![](/uploads/blogreacfirebase-6.png)
 6. En información General dar click en icono de configuración y en Configuración del proyecto.

    ![](/uploads/blogreacfirebase-7.png)
 7. En la última sección, la sección de Aplicaciones dar click en el tercer icono para Web.

    ![](/uploads/blogreacfirebase-8.png)
 8. Seleccionar un apodo en este caso Facturas.

    ![](/uploads/blogreacfirebase-9.png)
 9. Listo ahora deberemos copiar el siguiente código que firabase te otorga.

    ![](/uploads/blogreacfirebase-10.png)
10. Seleccionamos ir a la consola, y en la parte de Authentication damos click en Empezar.

    ![](/uploads/blogreacfirebase-11.png)
11. Nos desplegara los métodos de autenticación, es decir la forma en como podemos logearnos, con Facebook, Google, GitHub, pero por ahora daremos click en Email/Password.

    ![](/uploads/blogreacfirebase-12.png)
12. Le daremos Habilitar y Guardar.

    ![](/uploads/blogreacfirebase-13.png)
13. Por último nos dirigimos a registrar una app de Android, click en configuración del proyecto y añadir aplicación.

    ![](/uploads/blogreacfirebase-7.png)
14. Nos preguntara acerca de nuestro paquete, esto lo podemos ver en el Manifest en android/app/src/main/AndroidManifest.xml, normalmente cuando creaste un proyecto con react-native init \[Nombre\] tú paquete es com.\[Nombre\].

    ![](/uploads/blogreacfirebase-14.png)

    Agregamos un apodo, y para generar nuestro SHA-1 según la documentación en [https://rnfirebase.io/](https://rnfirebase.io/ "https://rnfirebase.io/") nos servira para autenticar mediante celular, ejecutamos en nuestra terminal

```bash
cd android && ./gradlew signingReport
```

Copiamos la cadena SHA-1 y le damos en registrar aplicación.

Finalmente vamos a descargar el archivo google.services.json

![](/uploads/blogreacfirebase-15.png)

### Yarn Firebase

En la terminal nos posicionamos a nuestro directorio del proyecto y deberemos añadir el paquete react-native-firebase/app y auth

```bash
yarn add @react-native-firebase/app @react-native-firebase/auth
```

### Android setup

Antes de correr nuestra aplicación deberemos pegar el archivo google-services.json en la ruta android/app dentro de la carpeta app.

![](/uploads/blogreacfirebase-16.png)

Seguiremos con la documentación de [https://rnfirebase.io/](https://rnfirebase.io/ "https://rnfirebase.io/") ya que unicamente hay que añadir los servicios de Google. Nos vamos al siguiente archivo y añadimos en el la línea de classpath: /android/build.gradle

```bash
buildscript {
  dependencies {
    // ... other dependencies
    classpath 'com.google.gms:google-services:4.3.3'
    // Añadir classpath --- /\
  }
}
```

Luego al archivo /android/app/build.gradle

```bash
apply plugin: 'com.android.application'
apply plugin: 'com.google.gms.google-services' // <- Añadir solo esta línea
```

### Ejecutar

Ahora bien deberemos iniciar metro con el siguiente comando:
```bash
yarn start
```
Y luego ejecutar en otra pestaña:
```bash
yarn android
```

Si todo funciono, se iniciara la aplicación!