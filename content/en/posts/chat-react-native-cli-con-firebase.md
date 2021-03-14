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

Nos detendremos a a pensar nuestra mejor estructura para nuestra base de datos, a continuación se propone la siguiente:

```msc
Alice->Bob: Hello Bob, how are you?
Note right of Bob: Bob thinks
Bob-->Alice: I am good thanks!
```

```msc
Title: Here is a title
A->B: Normal line
B-->C: Dashed line
C->>D: Open arrow
D-->>A: Dashed open arrow
```