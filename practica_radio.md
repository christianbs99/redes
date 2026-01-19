# Práctica Radio

1. Monta un Ubuntu 24 como servidor de streaming
    - Red: adaptador puente (configura como fija la IP que te dé el DHCP)
    - Comprueba que funciona el sonido
    - Instala Icecast2

2. Monta otro Ubuntu 24 como DJ
    - Red: adaptador puente
    - Comprueba que funciona el sonido
    - Instala Mixxx
    - Crea una radio con tu nombre (/christian)

3. Comprueba en la máquina anfitrión que escuchas tus ficheros. Hazlo desde
el navegador y desde VLC.

4. Escucha la radio de otro compañero.

# Resolucion del ejercicio

### 1. Montar el ubuntu como servidor 

- Fijar ip desde la interfaz grafica
- Comprobacion de que reproduce sonido

```bash
sudo apt install alsa-utils -y #para instalar gestionar el sonido
speaker-test -t sine -f 440 #hacer pureba de sonido para comprobar que funciona
```
- Instalar icecast2

```bash
sudo apt install icecast2 -y #instalacion de icecast2
```
### 2. Montar el ubuntu cliente

- Comprobacion de que se reproduce el sonido 

```bash
sudo apt install alsa-utils -y #para instalar gestionar el sonido
speaker-test -t sine -f 440 #hacer pureba de sonido para comprobar que funciona
```
- instalamos mixxx

```bash 
sudo apt install mixxx
```
- abriremos el mixxx y seleccionamos el directorio donde tenemos nuestra musica

- En opciones -> preferencias->emision en vivo y hacemos una nueva conexion y en conexion al servidor añadimos lo siguiente

```bash
- servidor: 192.168.1.174 #(ip del servidor icecast2) 
- montar: /cbs
- puerto: 8000
- identificacion: source (por defecto en el icecast2)
- contraseña: #(por defecto en el icecast2 lo podemos ver en el archivo de configuracion /etc/icecast2/icecast.xml)
```
- En el apartado hardware de sonido debemos seleccionar la salida del dispositivo de sonido en mi caso es front 

- Una vez añadimos esta configuracion lo aplicamos y nos vamos a la pista que queremos reproducir

- Le damos al boton "on air" y hacemos la comprobacion

### 3. Comprobacion

- En el navegador ponemos la siguiente url 
```bash
http://192.168.1.174:8000/cbs #ip servidor icecast2-> puerto por el que escucha-> punto de montaje
```
- Servidor de Streaming
<video src="https://github.com/user-attachments/assets/4d2cfc6e-f307-433f-939c-e0fa8e049b9b" controls="controls" style="max-width: 300px;">
  Tu navegador no soporta el vídeo.
</video>

