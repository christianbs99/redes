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
