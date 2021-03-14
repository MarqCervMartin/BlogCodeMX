+++
author = "Martín Márquez"
authorEmoji = "🤠"
categories = ["workshop"]
date = 2021-03-12T02:00:00Z
description = "Un chat full, completo con backend firebase."
enableToc = true
enableTocContent = false
hideToc = true
image = ""
pinned = true
series = []
tags = ["reac-native", "firebase", "javascript"]
title = "Chat react native cli con Firebase"

+++
## Chat con Firebase

¿Te has preguntado como funcionan las grandes aplicaciones de mensajería?, en está guía averiguaremos pequeños detalles que haran que nuestra app soporte multiples mensajes. Aprendiendo a implementar un chat que soporte salas, chat uno a uno, usuarios online y ordenamientos.

### Agradecimientos

Mariana - Frontend React Developer

Roberto - Senior React Developer

Aman Mittal - [Chat app with React](https://heartbeat.fritz.ai/chat-app-with-react-native-part-1-build-reusable-ui-form-elements-using-react-native-paper-75d82e2ca94f)

### Requerimientos

1. Editor de código
2. NodeJS
3. SDK Android
4. React Native

### Crear proyeco

```bash
npx react-native init ChatFirebase
```

### Conectar Firebase

Necesitaremos habilitar firebase para autenticarse y generar el google-services.json, para ello podemos ver el siguien [post ](https://blog.codemx.org/en/posts/login-react-native-cli-con-firebase/#firebase)

### Estructura de Firebase

Nos detendremos a a pensar nuestra mejor estructura para nuestra base de datos, en esta ocasión con Realtime Database a continuación se propone la siguiente:

### Dependencias

Después de crear nuestro proyecto, instalaremos las siguientes dependencias de Firebase:

```bash
yarn add @react-native-firebase/app @react-native-firebase/auth @react-native-firebase/database
```

Seguidamente instalaremos todo lo necesario para funcionar:

```bash
yarn add @react-navigation/native @react-navigation/stack react-native-reanimated react-native-gesture-handler react-native-screens react-native-safe-area-context @react-native-community/masked-view react-native-paper react-native-vector-icons
```

### Estructura de la Aplicación

Gracias a algunos componentes y nuestra navegación, podremos, tener una interfaz de prueba. En el siguiente [repositorio](https://github.com/MarqCervMartin/ChatFirebase/tree/meetup) en la rama meetup podremos importar la carpeta src.