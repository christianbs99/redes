# Práctica Vídeo

1. Instala FFmpeg.
2. Descarga el vídeo de Aules. Se trata de un .mp4 a 1080p.
3. Haz
   ```bash
   ffprobe -v error -show_streams fichero.mp4
   ```
   y localiza información que has estudiado
4. Remuxing: cambio de contenedor. De .mp4 a .mkv:
   ```bash
   ffmpeg -i original.mp4 -c:v copy -c:a copy salida.mkv
   ```

    Responde:
    - ¿Ha cambiado el tamaño de forma significativa?
    - ¿Ha habido carga de CPU?¿Ha tardado mucho?
  5. Cambio de códecs y comparación.
     Crea el fichero en H.264 con un bitrate de 2Mbps:
     ```bash
     ffmpeg -i original.mp4 -c:v libx264 -b:v 2M -c:a copy
     h264_2mbps.mp4
     ```
     - Reproduce ambos vídeos a la vez. Pon pausa en una escena con mucho movimiento.
     - ¿Cuál de los dos presenta más "artefactos" (cuadraditos)?
     - Si ambos tienen el mismo bitrate (2 Mbps), ¿pesan lo mismo los archivos finales?
  6. Simulación de streaming con diferentes tipos de fichero.
       1. Low (móvil):
     
          Resolución 240p
          
          Bitrate: 400k
       2. High (fibra):
          
          Resolución: 1080p
          
          Bitrate: 2Mbp
          
## Instalacion ffmpeg

- instalamos el ffmpeg

```bash
sudo apt update && sudo apt install ffmpeg -y
```

- Descargamos un video cualquiera yo he descargado uno de youtube en calidad 1080p

- Hacemos la comprobacion de ffprobe

```bash
ffprobe -v error -show_streams /home/chris/Descargas/naruto.mp4
```

- imagen del resultado

<img src="https://github.com/user-attachments/assets/161576ee-4e89-4004-a1c1-b151a88016d8" style="max-width: 1000px">

## Remuxing
- ahora debemos cambiar de mp4 a mkv para ello haremos lo siguiente
```bash 
ffmpeg -i /home/chris/Descargas/naruto.mp4 -c:v copy -c:a copy salida.mkv
```


1. ¿Ha cambiado el tamaño de forma significativa?

- No, el tamaño es similar ya que solo hemos cambiado el formato de video no los datos del propio video

2. ¿Ha habido carga de CPU?¿Ha tardado mucho?
- Muy poca, el comando ha terminado en menos de 5 segundos

## Cambio de códecs y comparación

- reducimo el peso del archivo 

```bash
ffmpeg -i /home/chris/Descargas/naruto.mp4 -c:v libx264 -b:v 2M -c:a copy h264_2mbps.mp4
```
- comparativa de las dos imagenes
1. original
<img width="885" height="444" alt="Image" src="https://github.com/user-attachments/assets/158054d2-8f99-458e-9c0f-fda8d2b84bdf">

2. 2bitrate
<img width="908" height="458" alt="Image" src="https://github.com/user-attachments/assets/0ab50a59-d0b2-4599-85ce-a05501097a62" />

- Podemos comprobar en el pelo rosa que la linea negra no esta tan definida como la original

- ¿Cuál de los dos presenta más "artefactos" (cuadraditos)?
   - El de 2 de bitrate ya que tiene mas pixeles borrosos 

- Si ambos tienen el mismo bitrate (2 Mbps), ¿pesan lo mismo los archivos finales?
   - Ambos pesaran similar, en mi caso como me he descargado un video el original tiene un bit rate de 0,56 Mbps respecto al que he creado a 2 Mbps entonces si que tengo una diferencia aprox de unos 20MB respecto al original, la formula utilizada en este caso ha sido ```Tamaño = Bitrate X Duración```

## Simulación de streaming con diferentes tipos de fichero.

1. Low (Móvil 240p): ffmpeg -i naruto.mp4 -vf "scale=-2:240" -c:v libx264 -b:v 400k -c:a copy low_movil.mp4
   
   ```bash
   #iniciamos el streaming
   ffmpeg -re -i low_movil.mp4 -c copy -f mpegts udp://127.0.0.1:1234
   ```
   
   <video src="https://github.com/user-attachments/assets/4bbc48ec-a62f-4fc7-9bc9-c1731550ad41" controls="controls" style="max-width: 1000px;">


2. High (Fibra 1080p): ffmpeg -i naruto.mp4 -vf scale=-1:1080 -b:v 2M high.mp4

   ```bash
   - ffmpeg -re -i high.mp4 -c copy -f mpegts udp://127.0.0.1:1234
   ```
   
   - abrimos el vlc y en medio -> abrir ubicacion en la red y ponemos ```udp://@:1234```
   
   <video src="https://github.com/user-attachments/assets/7d682a10-ce8c-465f-acd0-6e0c70e7399f" controls="controls" style="max-width: 1000px;">