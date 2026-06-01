# Bloque 1. Herramientas de seguridad

## 1. (2 puntos) Llama al profesor para que cree un usuario en una máquina Linux. Pondrá una contraseña con seis caracteres: una mayúscula, cuatro dígitos del 1 al 6 y una minúscula. Tienes que averiguar esa contraseña antes de que acabe la prueba. Sube una captura de pantalla con dicha contraseña.

Para este ejercicios usaremos dos herramientas, Jhon the Reaper para realizar un ataque usando el diccionario que generaremos con crunch

Primero que nada hacemos el volcado del hash en el un fichero, lo haremos con el siguiente comando

```bash
sudo grep -E 'examensad' /etc/shadow > ./hashes_examen_sad.txt
```

Y generamos el diccionario con el siguie te comando


```bash
crunch 6 6 abcdefghijklmnopqrstuvwxyz ABCDEFGHIJKLMNOPQRSTUVWXYZ 123456 -t ,%%%%@ -o diccionario_examen_sad.txt
```

Y ahora usamos la herramienta jhon para crakear la contraseña usando el diccionario

```bash
john --wordlist=diccionario_examen_sad.txt hashes_examen_sad.txt
```


![alt text](img/bloque1_ejercicio1_img1.png)

![alt text](img/bloque1_ejercicio1_img2.png)

# 2. (2 puntos) Instala una herramienta de integridad de datos en Linux y cambia la configuración para que envíe las alertas relacionadas con modificaciones o borrados de ficheros en el directorio /bin a la dirección raulpruebas21@gmail.com. Haz las capturas de pantalla necesarias para acreditar el cambio y haz que envíe alguna alerta para demostrar el funcionamiento.

![alt text](img/bloque1_ejercicio2_img1.png)


## 5. (2 puntos) Obten toda la información que puedas legalmente sobre un dominio de tu elección que no sea el del instituto (no uses técnicas de reconocimiento activo). Explica las operaciones realizadas y muestra las capturas con la información obtenida.

# Bloque II. Criptografía

## 2. Realiza las siguientes operaciones (4 puntos):

### a) Crea un par de claves y sube tu clave pública al servidor de claves de Ubuntu. Adjunta captura que demuestre que la clave se ha subido correctamente.

Generamos la clave con el siguiente comando:

```bash
gpg --gen-key
```

![alt text](img/bloque2_ejercicio2_img1.png)

Y las subiremos al servidor de claves de ubuntu de la siguiente forma

```
gpg --keyserver https://keyserver.ubuntu.com/ --send-keys "2DF092151F0DDC944C0A5ADF2EA5F1B825DDD18A"
```

![alt text](img/bloque2_ejercicio2_img2.png)

Al buscarla en el servidor de claves nos sale la nuestra, eso comprueba que esta subida

![alt text](img/bloque2_ejercicio2_img3.png)


![alt text](img/bloque2_ejercicio2_img4.png)

### b) Manda un correo a raulpruebas21@gmail.com adjuntando tu clave pública recién creada como texto ASCII.

Pasaremos la clave a formato ASCII con el siguiente comando

```
gpg --armor --output examen_sad.asc --export 2DF092151F0DDC944C0A5ADF2EA5F1B825DDD18A
```

![alt text](img/bloque2_ejercicio2_img5.png)

Podemos comprobar el contenido haciendo un cat

![alt text](img/bloque2_ejercicio2_img6.png)

Y ahora que ya lo tenemos la enviamos por correo

### c) Cifra un fichero de texto de forma simétrica con la clave “ThisIsMyLastChance” usando OpenSSL.

Lo primero que hacermos sera generar el fichero cifrado para el examen


![alt text](img/bloque2_ejercicio2_img7.png)

Y ahora lo cifraremos usando OPENSSL

Lo cifraremos usando el siguiente comando

```
openssl enc -aes-256-cbc -pbkdf2 -salt -in mensaje-cifrado-examen-sad.txt -out mensaje-cifrado-examen-sad.txt.enc -k "ThisIsMyLastChance"
```

## Bloque IV. Informática Forense

Sobre el volcado de memoria y el de disco de una máquina Windows que realizaste para la práctica, obten si es posible las siguientes informaciones usando Volatility, Autopsy, un editor del Registro u otras herramientas de tu elección:

1. Identifica los cinco últimos archivos abiertos por algún usuario. (0,5 puntos)

![alt text](img/bloque4_ejercicio1_img1.png)

2. Determina cual fue el último dispositivo USB externo conectado y la fecha de conexión (0,5 puntos)

3. Últimos cinco archivos eliminados, incluyendo nombre, ruta y fecha de eliminación (0,5 puntos)

![alt text](img/bloque4_ejercicio3_img1.png)

4. Conexiones de red activas y direcciones IP involucradas. (0,5 puntos)

![alt text](img/bloque4_ejercicio4_img1.png)

![alt text](img/bloque4_ejercio4_img2.png)

5. Nombre del último usuario logueado. (1 punto)

![alt text](img/bloque4_ejercicio5_img1.png)

6. Listado de programas que se arrancan en el inicio del sistema. (1 punto)

![alt text](img/bloque4_ejercicio6_img1.png)

7. Procesos ocultos o inyectados en otros procesos (0,5 puntos)

![alt text](img/bloque4_ejercicio7_img1.png)

8. Pruebas de ejecución reciente de PowerShell (0,5 puntos)

![alt text](img/bloque4_ejercicio8_img1.png)

Sobre el volcado de memoria y el de disco de una máquina Linux que realizaste para la práctica, obten si es posible las siguientes informaciones:

9. Conexiones SSH entrantes. (0,5 puntos)

10. Archivos de imagen cuya ubicación está en Europa. (0,5 puntos)

![alt text](img/bloque4_ejercicio10_img1.png)

11. Archivos ejecutados por el usuario root. (0,5 puntos)

![alt text](img/bloque4_ejercicio11_img1.png)

12. Servicios activos y en ejecución. (0,5 puntos)

![alt text](img/bloque4_ejercicio16_img1.png)

13. Muestra los usuarios del sistema y su historial de comandos (1 punto)

![alt text](img/bloque4_ejercicio13_img1.png)

14. Detecta si hay comandos que se ejecuten automáticamente en el inicio de la sesión. (0,5 puntos)

Hay dos lados uno para cada usuario /home/usuario/.bashrc o .zshrc o .profile tambien

![alt text](img/bloque4_ejercicio14_img1.png)

Y la gloval que es /etc/profile o profile.d

![alt text](img/bloque4_ejercicio14_img2.png)


15. Muestra los últimos ficheros de configuración de sistema que han sido modificados. (0,5 puntos)

![alt text](img/bloque4_ejercicio15_img1.png)

16. Dí qué módulos del kernel estaban cargados en el momento de la captura (1 punto)
    
![alt text](img/bloque4_ejercicio16_img1.png)

Todas las operaciones deben estar documentadas con las capturas de pantalla necesarias demostrando que la información obtenida es veraz.

En dichas capturas debe quedar de manifiesto que es la máquina del alumno y la fecha y hora de la misma.


# Bloque V. Cortafuegos

## 1. (1 punto) Explica en qué situación debes usar la acción MASQUERADE en nftables y escribe un ejemplo del comando en el que se emplea habitualmente.

Debes usar la acción masquerade cuando necesitas configurar un enmascaramiento de red (Source NAT o SNAT) para que los equipos de tu red local puedan acceder a Internet, pero la dirección IP pública de tu interfaz de salida es dinámica (por ejemplo, asignada por DHCP).

A diferencia del SNAT normal (donde especificas una dirección IP de salida fija), masquerade lee automáticamente la dirección IP que tiene asignada la interfaz de salida en el momento de enviar el paquete. Si tu proveedor de Internet cambia tu IP pública, masquerade se adapta automáticamente sin que se rompa la conexión. Si tuvieras una IP pública estática, es mejor usar snat.

Habitualmente, esta regla se aplica en una tabla de tipo nat y dentro de una cadena tipo postrouting (justo antes de que el paquete abandone el equipo).
La forma más sencilla de implementarlo es la siguiente:

```bash
nft add rule ip nat postrouting oifname "eth0" masquerade
```

## 2. (3 puntos) Escribe los comandos necesarios para poner un cortafuegos de nodo nftables en un servidor con política DROP por defecto y permitir las siguientes operaciones:
	
### Obtención de configuración IP por DHCP

```bash
sudo nft add rule ip filtro output udp sport 68 udp dport 67 accept
sudo nft add rule ip filtro input udp sport 67 udp dport 68 accept
```

### Actualización de paquetería Debian desde las 7 a las 10 de la mañana

```bash
sudo nft add rule ip filtro output udp dport 53 hour "07:00"-"10:00" accept
sudo nft add rule ip filtro output tcp dport 53 hour "07:00"-"10:00" accept
sudo nft add rule ip filtro output tcp dport { 80, 443 } hour "07:00"-"10:00" accept
```

### Acceso desde el exterior al servidor Apache instalado en el propio servidor, evitando ataques de Denegación de Servicio

```bash
# Lo que haremos el limitar el limite de conexiones a 10 por minuto, esto hara que sea imposible hacer un ataque de denegacion de servicios ya que cuando la misma ip haga la undecima conexion en menos de 10 minutos se dropea
nft add rule ip filtro input tcp dport 80 ct state new meter tcp-conn-limit-80 { ip saddr timeout 10m limit rate over 10/minute } drop
nft add rule ip filtro input tcp dport 80 accept
nft add rule ip filtro input tcp dport 443 ct state new meter tcp-conn-limit-443 { ip saddr timeout 10m limit rate over 10/minute } drop
nft add rule ip filtro input tcp dport 443 accept
```

### Acceso desde la máquina con MAC 00:11:22:33:44:55:66 al servicio de MariaDB instalado en el propio servidor

```bash
nft add rule ip filtro input ether saddr 00:11:22:33:44:55 tcp dport 3306 accept
```

### Navegación web a todas las páginas excepto a las alojadas en 59.1.22.3

```bash
# Primero ponemos el bloqueo de esa ip por ambos pueros y luego permitimos el acceso a todas, si lo hiciesemos al reves permitiria el acceso a todas y la otra red la ignoraría
nft add rule ip filtro output ip daddr 59.1.22.3 tcp dport { 80, 443 } drop
nft add rule ip filtro output tcp dport { 80, 443 } accept
```

### Comunicación por ping hacia y desde las máquinas de la 192.168.1.10 a la 192.168.1.100

```bash
# Permitimos que nuestra maquina pueda hacer ping a las otras máquinas
nft add rule ip filtro output ip daddr 192.168.1.10-192.168.1.100 icmp type echo-request accept
nft add rule ip filtro input ip saddr 192.168.1.10-192.168.1.100 icmp type echo-reply accept

# Y despues permitims que nos hagan ping
nft add rule ip filtro input ip saddr 192.168.1.10-192.168.1.100 icmp type echo-request accept
nft add rule ip filtro output ip daddr 192.168.1.10-192.168.1.100 icmp type echo-reply accept
```

## 3. Supon que dispones del siguiente escenario con las direcciones indicadas en la tabla que se encuentra a continuación:

Todas las direcciones son /28

(6 puntos) Añade las reglas mínimas necesarias para que funcionen correctamente las operaciones de la a) a la d) y solo esas. Debes cumplir también las siguientes condiciones empleando los módulos que necesites:

    • Las conexiones funcionarán exclusivamente hasta la hora del recreo.
    • No se permitirán más de tres peticiones por segundo a los servidores web y cinco a los de bases de datos.
    • Solo los clientes pueden empezar conexiones.
    • No se permitirá tráfico que atraviese el router por interfaces distintas de las marcadas por las rutas establecidas.

	Las operaciones permitidas serán las siguientes:

### a) Acceso desde Garfield a la web de Shenzi

```bash
# R2 parte privada
nft add rule ip filtro input ip saddr 192.168.1.3 ip daddr 192.168.1.1 tcp dport { 80, 443 } hour "11:00"-"12:00" ct state new limit rate 3/second accept
nft add rule ip filtro output ct state established,related accept

# R2 parte publica
nft add rule ip filtro forward ip saddr 11.1.1.2 ip daddr 15.5.5.2 tcp dport { 80, 443 } hour "11:00"-"12:00" ct state new limit rate 3/second accept
nft add rule ip filtro forward ct state established,related accept

# R1 
nft add rule ip filtro forward ip saddr 11.1.1.2 ip daddr 15.5.5.2 tcp dport { 80, 443 } hour "11:00"-"12:00" ct state new limit rate 3/second accept
nft add rule ip filtro forward ct state established,related accept

# R4
nft add rule ip filtro forward ip saddr 11.1.1.2 ip daddr 15.5.5.2 tcp dport { 80, 443 } hour "11:00"-"12:00" ct state new limit rate 3/second accept
nft add rule ip filtro forward ct state established,related accept

# R6 parte pública
nft add rule ip filtro forward ip saddr 11.1.1.2 ip daddr 15.5.5.2 tcp dport { 80, 443 } hour "11:00"-"12:00" ct state new limit rate 3/second accept
nft add rule ip filtro forward ct state established,related accept

# R6 parte privada
nft add rule ip filtro forward ip saddr 192.168.1.1 ip daddr 192.168.1.3 tcp dport { 80, 443 } hour "11:00"-"12:00" ct state new limit rate 3/second accept
nft add rule ip filtro forward ct state established,related accept
```

### b) Acceso desde Garfield a RinTinTin por SSH

```bash
# R2 parte privada 
nft add rule ip filtro input ip saddr 192.168.1.3 ip daddr 192.168.1.1 tcp dport 22 hour "11:00"-"12:00" ct state new accept
nft add rule ip filtro forward ct state established,related accept

# R2 parte publica
nft add rule ip filtro forward ip saddr 11.1.1.2 ip daddr 16.6.6.1 tcp dport 22 hour "11:00"-"12:00" ct state new accept
nft add rule ip filtro forward ct state established,related accept

#R1
nft add rule ip filtro forward ip saddr 11.1.1.2 ip daddr 16.6.6.1 tcp dport 22 hour "11:00"-"12:00" ct state new accept
nft add rule ip filtro forward ct state established,related accept

# R4
nft add rule ip filtro forward ip saddr 11.1.1.2 ip daddr 16.6.6.1 tcp dport 22 hour "11:00"-"12:00" ct state new accept
nft add rule ip filtro forward ct state established,related accept

# R6
nft add rule ip filtro forward ip saddr 11.1.1.2 ip daddr 16.6.6.1 tcp dport 22 hour "11:00"-"12:00" ct state new accept
nft add rule ip filtro forward ct state established,related accept

# R5 parte pública
nft add rule ip filtro forward ip saddr 11.1.1.2 ip daddr 16.6.6.1 tcp dport 22 hour "11:00"-"12:00" ct state new accept
nft add rule ip filtro forward ct state established,related accept

# R5 parte privada
nft add rule ip filtro forward ip saddr 192.168.1.1 ip daddr 192.168.1.3 tcp dport 22 hour "11:00"-"12:00" ct state new accept
nft add rule ip filtro forward ct state established,related accept
```

### c) Acceso desde Simba hasta el servidor web de Milu

```bash
# R4 parte privada
nft add rule ip filtro input ip saddr 192.168.1.3 ip daddr 192.168.1.1 tcp dport { 80, 443 } hour "11:00"-"12:00" ct state new limit rate 3/second accept
nft add rule ip filtro output ct state established,related accept

# R4 parte publica 
nft add rule ip filtro forward ip saddr 15.5.5.1 ip daddr 16.6.6.1 tcp dport { 80, 443 } hour "11:00"-"12:00" ct state new limit rate 3/second accept
nft add rule ip filtro forward ct state established,related accept

# R6
nft add rule ip filtro forward ip saddr 15.5.5.1 ip daddr 16.6.6.1 tcp dport { 80, 443 } hour "11:00"-"12:00" ct state new limit rate 3/second accept
nft add rule ip filtro forward ct state established,related accept

# R5 parte publica
nft add rule ip filtro forward ip saddr 15.5.5.1 ip daddr 16.6.6.1 tcp dport { 80, 443 } hour "11:00"-"12:00" ct state new limit rate 3/second accept
nft add rule ip filtro forward ct state established,related accept

#R5 parte privada
nft add rule ip filtro forward ip saddr 192.168.1.1 ip daddr 192.168.1.2 tcp dport { 80, 443 } hour "11:00"-"12:00" ct state new limit rate 3/second accept
nft add rule ip filtro forward ct state established,related accept
```

### d) Acceso desde Alex al servidor de bases de datos de Rocinante

```bash
# R4 privada
nft add rule ip filtro input ip saddr 192.168.1.2 ip daddr 192.168.1.1 tcp dport 5432 hour "11:00"-"12:00" ct state new limit rate 5/second accept
nft add rule ip filtro output ct state established,related accept

# R4 publica
nft add rule ip filtro forward ip saddr 12.2.2.2 ip daddr 12.2.2.1 tcp dport 5432 hour "11:00"-"12:00" ct state new limit rate 5/second accept
nft add rule ip filtro forward ct state established,related accept

# R1 publica
nft add rule ip filtro forward ip saddr 12.2.2.2 ip daddr 12.2.2.1 tcp dport 5432 hour "11:00"-"12:00" ct state new limit rate 5/second accept
nft add rule ip filtro forward ct state established,related accept

# R1 privada
nft add rule ip filtro forward ip saddr 192.168.1.1 ip daddr 192.168.1.2 tcp dport 5432 hour "11:00"-"12:00" ct state new limit rate 5/second accept
nft add rule ip filtro forward ct state established,related accept
```
