
---
## 🧠✨ COSAS QUE DEBERÍAS SABER DEL PDF (según yo, tu bestie digital)

### 🧱 MODELO OSI aka la biblia de las redes

Son 7 capas que explican cómo se comunican los dispositivos.  
Imaginátelo como una lasaña tecnológica, cada capa hace algo distinto:

1. **Física**: cables, señales eléctricas, cosas que hacen _bzzzt_ ⚡
    
2. **Enlace de datos**: conecta compus en red local, tipo el chismoso del barrio 🧃
    
3. **Red**: ruta pa' que los datos viajen (hello IPs 🚗💨)
    
4. **Transporte**: asegura que los datos lleguen bien (acá vive TCP/UDP 👀)
    
5. **Sesión**: mantiene las sesiones abiertas y cerradas (como los vínculos tóxicos 😮‍💨)
    
6. **Presentación**: traduce datos al lenguaje que entienden las apps 📄➡️💻
    
7. **Aplicación**: lo que vos usás (Google, WhatsApp, Twitch, etc) 📲
    

---

### 📦 TCP vs UDP (el dilema existencial)

- **TCP** = confiable, lento, ordenado → sirve para cosas importantes: emails, páginas web, bancas online.  
    ➤ Usa _handshake_, confirma cada paquetito. Es como la mamá que se asegura que comiste. 🥹
    
- **UDP** = rápido, caótico, cero confirmaciones → ideal para juegos, llamadas, streaming.  
    ➤ Si se pierde un paquete, se perdió. Es la amiga que grita “YA LLEGUÉ” sin saber si abriste la puerta 💀
    

---

### 📡 PROTOCOLOS CLAVE

- **DNS**: convierte nombres como “google.com” en direcciones IP 😮‍💨📞
    
- **DHCP**: te da una IP automática cuando te conectás. No lo tenés? APIPA te da una de emergencia tipo 169.254.x.x 😭
    
- **FTP**: subir/bajar archivos (old school vibes 💾)
    
- **HTTP/HTTPS**: ver webs, con o sin cifrado 🔓🔐
    
- **SSH**: acceso remoto seguro (tipo hacker real 💻🕶️)
    
- **TELNET**: igual que SSH pero inseguro, cancelado 🚫
    
- **QUIC**: el nuevo cool kid, reemplazo de TCP en HTTP/3, rápido y cifrado ✨
    

---

### 🔐 ATAQUES & DRAMA

- **Spoofing**, **DDoS**, **ARP**, **SYN flood**...  
    Básicamente hay mil formas de hacerte daño en la red si no estás alerta 🙃  
    Solución: _firewall bien configurado + no usar routers del año 2001_
    

---

### 🌍 TRÁFICO EN LA RED

Los datos viajan con diferentes _vibes_:

- Constante → como sensores IoT.
    
- En ráfagas → backups o series en Netflix.
    
- Tiempo real → videollamadas, gaming 🎮📞
    

---

### ⚠️ DHCP ANTI-DRAMA TIP:

Activa _DHCP Snooping_ pa’ bloquear servidores falsos. Literal es como un portero que no deja pasar al que no fue invitado 💅🔐

---

## TL;DR de tu angelito de datos 😇

Tenés que entender:

- Cómo viajan los datos (modelo OSI)
    
- Qué hace cada protocolo
    
- Cuándo usar TCP o UDP
    
- Cómo protegerte de ataques
    
- Qué significa que te den una IP automáticamente
    


## 🧠 FLASHCARDS EXPRESS 💥

---

**Q:** ¿Cuántas capas tiene el modelo OSI y para qué sirve?  
**A:** 7 capas. Es la receta secreta de cómo se comunican los dispositivos en red. Una lasaña digital. 🍝🌐

---

**Q:** ¿Cuál es la diferencia entre TCP y UDP?  
**A:** TCP = confiable pero lento 😌  
UDP = rápido pero caótico 💨💀

---

**Q:** ¿Qué hace el DNS?  
**A:** Traduce "google.com" a números que las compus entienden. Básicamente un traductor de vibes. 🌍➡️💻

---

**Q:** ¿Qué es y para qué sirve DHCP?  
**A:** Te da una IP automáticamente cuando te conectás. Es como entrar a una fiesta y que te den tu mesa sin preguntar 🪪🎉

---

**Q:** ¿Qué hace DHCP Snooping?  
**A:** Bloquea servidores DHCP truchos. Es el portero de la red que no deja pasar al tóxico. 🚫🧍‍♂️

---

**Q:** ¿Qué patrón de tráfico usan juegos online y videollamadas?  
**A:** Tiempo real: súper rápido, tolerancia 0 al lag. Si se pierde algo, _seguimos igual_ 😭🎮📞

---

# SOLEMNE 1 PRUEBA

OK BFF VAMOS CON TODO 💻🔥 esta solemne está jugosita y con vibes de “me quiero lanzar por la ventana del laboratorio de redes” 😭 pero tranqui, que ya me puse el gorro de sysadmin ✨ y voy a desmenuzarla como si fuera drama en TikTok. TE VOY A SALVAR DE ESTA 💅

---

## 🧠 Pregunta 1 (20 pts)

🔥**Contexto:** estás en una LAN donde **NO SE PUEDE USAR TCP** por el firewall. Todo pasa por una **VLAN45**, y los chiquillos tienen que inscribir sus ramos de manera presencial desde computadores conectados por switch de capa 3.  
SO… toca hacer MAGIA con **protocolos que no usan TCP**. Cada funcionalidad necesita uno distinto + IPs + MACs + una forma en que TODO podría irse alv. Te hago el resumen paso a paso con ideas para cada punto:

---

### 💌 1. El server informa a TODOS el estado de los cursos

**Protocolo:** **UDP + Broadcast** o incluso **Multicast**  
**Cliente:** Escucha un puerto específico, p.ej. 5000.  
**Server:** Envía periódicamente info a `10.203.65.127` (broadcast con máscara /27).  
**MAC random válida:** `12:34:56:78:90:1A`  
**Fail possible:** Algún host con firewall que bloquee UDP broadcast = no recibe nada. 🙃

---

### ✋ 2. El alumno solicita inscribir ramo

**Protocolo:** **ICMP con payload custom** (como si fueras hacker del 2005 👾)  
**Cliente:** Manda echo request con ID del ramo al server.  
**Server:** Responde echo reply con estado.  
**IP usada:** alumno podría ser `10.203.65.101`, MAC: `12:34:56:78:90:65`  
**Fail:** Algún router que filtre ICMP y corte todo. Llorando. 😔

---

### ✅ 3. Confirmar la inscripción

**Protocolo:** **SNMP** (aunque medio cursed pa esto, pero sirve xD)  
**Cliente:** envía una solicitud tipo SET con info del ramo.  
**Server:** responde con un GET-RESPONSE de confirmación.  
**Fail:** SNMP mal configurado sin comunidad correcta = nada funciona.

---

### 📣 4. El server notifica a los alumnos online quiénes son sus compañeros

**Protocolo:** **Multicast usando UDP**  
**Server:** envía a grupo multicast tipo `224.0.0.1` la lista de inscritos x curso.  
**Clientes:** todos los que estén online escuchan y actualizan.  
**Fail:** Si algún alumno no se une al grupo multicast… se lo pierde lol.

---

### ❌ 5. Alumno elimina ramo

**Protocolo:** **TFTP (sobre UDP)**  
**Cliente:** manda archivo .txt con su ID y el ramo a borrar.  
**Server:** borra y responde ACK.  
**Fail:** Si el archivo se pierde (UDP es NO confiable), el server no hace nada.

---

### 📥 6. Descargar el programa del curso

**Protocolo:** **FTP en modo pasivo sobre UDP usando algún túnel tipo UDP-encapsulado**  
**Cliente:** hace request al server, y recibe el programa como archivo.  
**Fail:** Si el archivo es muy grande y hay pérdida de paquetes, te llega incompleto o corrupto 🤡

---

## 🛰️ Pregunta 2 (20 pts)

### "La descarga va lento y a veces ni avanza" = WELCOME TO TCP: THE SOAP OPERA™ 😩📉

Posibles causas:

1. **Congestión de red**: el TCP entra en modo “ay no, voy a esperar” (congestion control, cwnd bajísimo).
    
2. **Retransmisiones por pérdidas**: si hay pérdida de paquetes, el TCP se pone nervioso y empieza a repetir todo.
    
3. **Ventana de recepción del cliente llena**: el servidor espera a que el cliente diga “ok ya leí, mándame más”.
    
4. **Algún nodo intermedio con bufferbloat**: se acumulan paquetes y se atrasan por siglos.
    
5. **Limitación del ancho de banda o shaping**: te están haciendo throttling sin avisarte 😭
    
6. **Problemas con slow start o fast recovery**: TCP parte de a poco, y si hay pérdida, vuelve casi a cero.
    

💀💀💀 resumen: TCP es una relación tóxica que no supera sus traumas y cada packet que se pierde es una red flag más 🚩

---

## 🌐 Pregunta 3 (20 pts)

El usuario no puede entrar a `https://www.lala.cl` y tú eres EL SYSADMIN 🕵️‍♀️  
Posibles causas:

1. **DNS no resuelve el dominio**: el cliente no puede traducir el nombre a IP 😵
    
2. **Certificado HTTPS inválido/no confiable**: el navegador bloquea la conexión.
    
3. **Restricción en el firewall (filtro por contenido o IP)**: el tráfico hacia ese dominio está bloqueado.
    
4. **Problemas con la red local/DHCP**: IP mal asignada, gateway incorrecto, o DNS que no responde.
    

BONUS DRAMA:

- El sitio está caído 🙃
    
- El cliente tiene la hora mal configurada y no puede validar SSL ⏰💀
    
- Proxy interceptando tráfico HTTPS y rompiendo todo