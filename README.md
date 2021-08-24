# Emby Custom AC3 (Dolby Digital) Bitrate

This is a hacky fix for this problem

https://emby.media/community/index.php?/topic/67030-adjust-bitrate-for-transcoded-audio-such-as-dolby-ac-3

## Using Docker Compose on Linux

-   Make a folder named **build** next to your **docker.compose.yml** file and place **Dockerfile** and **ffmpeg.go** into it.
-   Replace image: **emby/embyserver:latest** with **build: ./build** in your yml file
-   When running **docker-compose up -d**, it will automatically build and start
-   To force a build (for new Emby versions) run **docker-compose build** and **up -d**
