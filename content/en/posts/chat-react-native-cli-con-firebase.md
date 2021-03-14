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

### Registrar usuarios en Realtime

En el archivo src/navigation/AuthProvider.js registraremos y por el momento actualizaremos el estado del usuario, donde 1 significa conectado y 0 desconectado.

```javascript
import React, { createContext, useState } from 'react';
import auth from '@react-native-firebase/auth';
import database from '@react-native-firebase/database';

export const AuthProvider = ({ children }) => {
    const [user, setUser] = useState(null);
  
    return (
      <AuthContext.Provider
        value={{
          user,
          setUser,
          login: async (email, password) => {
            try {
              let {user} = await auth().signInWithEmailAndPassword(
                email,
                password,
              );
              await database()
                .ref('usuarios/' + user.uid)
                .update({state: 1});
              console.log('Usuario loggeado');
            } catch (e) {
              console.log(e);
            }
          },
          register: async (email, password) => {
            try {
              let {user} = await auth().createUserWithEmailAndPassword(
                email,
                password,
              );
              //setUser(user)
              console.log(user);
              const usuario = {
                uid: user.uid,
                email: user.email,
                state: 1,
              };
              await database()
                .ref('usuarios/' + user.uid)
                .set(usuario);
              console.log('Usuario guardado');
            } catch (e) {
              console.log(e);
            }
          },
          logout: async () => {
            try {
              await database()
                .ref('usuarios/' + user.uid)
                .update({state: 0});
              await auth().signOut();
            } catch (e) {
              console.error(e);
            }
          }
        }}
      >
        {children}
      </AuthContext.Provider>
    );
  };

export const AuthContext = createContext({});
```

Hecho esto ya podemos registrar usuarios, el siguiente paso es listar nuestros usuarios online y poder enviarles mensajes. En nuestra HomeScreen agregamos.

```javascript
const user = auth().currentUser;
  const [arrayOnline, setArrayOnline] = useState([]);
  const [objOnline, setObjonline] = useState({});

  useEffect(() => {
    //listar usuarios online, nodo estado firebase
    database()
      .ref(`usuarios`)
      .orderByChild('state')
      .limitToLast(50)
      .on('child_added', (snap) => {
        if (snap.val().state === true) {
          if (user.uid !== snap.key) {
            //delete objOnline[key];
            setObjonline((prevState) => {
              const key = snap.key;
              const val = snap.val();

              return { ...prevState, [key]: val };
            });
          }
        }
      });

    database()
      .ref(`usuarios`)
      .on('child_changed', (snap) => {
        //console.log(snap.val());
        if (snap.val().state === true) {
          if (user.uid !== snap.key) {
            setObjonline((prevState) => {
              const key = snap.key;
              const val = snap.val();

              return { ...prevState, [key]: val };
            });
          }
        } else {
          setObjonline((prevState) => {
            const key = snap.key;
            delete prevState[key];
            return { ...prevState };
          });
        }
      });
      
  }, []);

  useEffect(() => {
    const newArray = Object.values(objOnline);
    setArrayOnline(newArray);
    console.log(arrayOnline)
  }, [objOnline]);
```

Ahora bien ya podemos listar y seleccionar nuestro usuario, ahora vamos a enviar mensajes mediante GiftedChat