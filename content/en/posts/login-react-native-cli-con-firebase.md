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