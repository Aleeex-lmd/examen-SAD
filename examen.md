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

## 1. Realiza las siguientes operaciones:

### a) Crea una autoridad certificadora. Configura dicha autoridad de forma que para que una CSR sea válida deba aportarse la dirección postal del solicitante y deba coincidir el pais. La provincia por defecto debe ser Sevilla y la localidad por defecto Dos Hermanas. El nombre de la organización debe ser IESGN. La contraseña debe tener un mínimo de 8 caracteres.

![alt text](img/bloque2_ejercicio1_img1.png)

![alt text](img/bloque2_ejercicio1_img0.png)

![alt text](img/bloque2_ejercicio1_img2.png)

![alt text](img/bloque2_ejercicio1_img3.png)

![alt text](img/bloque2_ejercicio1_img4.png)

![alt text](img/bloque2_ejercicio1_img5.png)

![alt text](img/bloque2_ejercicio1_img6.png)

b) Genera una CSR para un servidor HTTPS que deberás montar con Apache

![alt text](img/bloque2_ejercicio1_img7.png)

![alt text](img/bloque2_ejercicio1_img8.png)

c) Configura el servidor Apache adecuadamente con la información proporcionada por la autoridad certificadora como respuesta a la CSR.

![alt text](img/bloque2_ejercicio1_img9.png)

![alt text](img/bloque2_ejercicio1_img10.png)

![alt text](img/bloque2_ejercicio1_img11.png)

![alt text](img/bloque2_ejercicio1_img12.png)

![alt text](img/bloque2_ejercicio1_img13.png)

Documenta el proceso completo, demostrando que el servidor es accesible por HTTPS en el puerto 443 con su certificado recién firmado por la CA (Debes mostrar la fecha de creación del certificado). 

(6 puntos)


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

openssl enc -d -aes-256-cbc -pbkdf2 -salt -in mensaje-cifrado-examen-sad.txt.enc -k "ThisIsMyLastChance"

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

![alt text](img/bloque4_ejercicio12_img1.png)

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

Se usa masquerade en nftble cuando la ip publica que se usa para conectarse a internet es una ip dinámica, es decir que esta puede cambiar por lo que habria que cambiar la red cada vez que la ip cambia, lo que hacemos es que en vez de poner una direccion publica ponemos masquerade que buesca la ip publica actual y usa esa


```bash
nft add rule ip nat postrouting oifname "eth0" masquerade
```

## 2. (3 puntos) Escribe los comandos necesarios para poner un cortafuegos de nodo nftables en un servidor con política DROP por defecto y permitir las siguientes operaciones:

![alt text](img/bloque5_ejercicio2_img1.png)

### Obtención de configuración IP por DHCP

![alt text](img/bloque5_ejercicio2_img2.png)

![alt text](img/bloque5_ejercicio2_img3.png)

![alt text](img/bloque5_ejercicio2_img4.png)


### Actualización de paquetería Debian desde las 12 a las 13 de la mañana

![alt text](img/bloque5_ejercicio2_img5.png)

![alt text](img/bloque5_ejercicio2_img6.png)

![alt text](img/bloque5_ejercicio2_img7.png)


### Acceso desde el exterior al servidor Apache instalado en el propio servidor, evitando ataques de Denegación de Servicio

![alt text](img/bloque5_ejercicio2_img8.png)

![alt text](img/bloque5_ejercicio2_img9.png)


### Acceso desde la máquina con MAC 52:54:00:50:36:89 al servicio de MariaDB instalado en el propio servidor

![alt text](img/bloque5_ejercicio2_img10.png)

![alt text](img/bloque5_ejercicio2_img11.png)

![alt text](img/bloque5_ejercicio2_img12.png)

### Navegación web a todas las páginas excepto a las alojadas en 59.1.22.3

![alt text](img/bloque5_ejercicio2_img13.png)

![alt text](img/bloque5_ejercicio2_img14.png)

![alt text](img/bloque5_ejercicio2_img15.png)

![alt text](img/bloque5_ejercicio2_img16.png)

### Comunicación por ping hacia y desde las máquinas de la 192.168.122.1 a la 192.168.122.100

![alt text](img/bloque5_ejercicio2_img17.png)

![alt text](img/bloque5_ejercicio2_img18.png)

![alt text](img/bloque5_ejercicio2_img19.png)

![alt text](img/bloque5_ejercicio2_img20.png)

![alt text](img/bloque5_ejercicio2_img21.png)

## 3. Supon que dispones del siguiente escenario con las direcciones indicadas en la tabla que se encuentra a continuación:

Todas las direcciones son /28

(6 puntos) Añade las reglas mínimas necesarias para que funcionen correctamente las operaciones de la a) a la d) y solo esas. Debes cumplir también las siguientes condiciones empleando los módulos que necesites:

    • Las conexiones funcionarán exclusivamente hasta la hora del recreo.
    • No se permitirán más de tres peticiones por segundo a los servidores web y cinco a los de bases de datos.
    • Solo los clientes pueden empezar conexiones.
    • No se permitirá tráfico que atraviese el router por interfaces distintas de las marcadas por las rutas establecidas.

	Las operaciones permitidas serán las siguientes:


