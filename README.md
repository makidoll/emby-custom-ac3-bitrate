# Emby Custom AC3 (Dolby Digital) Bitrate

This is a hacky fix for this problem

https://emby.media/community/index.php?/topic/67030-adjust-bitrate-for-transcoded-audio-such-as-dolby-ac-3

My solution is to replace the **ffmpeg** binary with a wrapper that manipulates incoming arguments and then actually runs ffmpeg.

It looks for arguments **-c:a:? ac3** then replaces **-ab:a:? ??????** with **-ab:a:? 640000** or whatever you set **`EMBY_CUSTOM_AC3_BITRATE`** to.

## Using Docker Compose on Linux

-   Make a folder named **build** next to your **docker.compose.yml** file and place **Dockerfile** and **ffmpeg.go** into it.
-   Replace image: **emby/embyserver:latest** with **build: ./build** in your yml file
-   When running **docker-compose up -d**, it will automatically build and start
-   To force a build (for new Emby versions) run **docker-compose build** and **up -d**
-   If you'd like to change the bitrate, set environment variable **`EMBY_CUSTOM_AC3_BITRATE`** in your yml file. By default its **`640000`** which is **640 kbps**

## Not using Docker

### Getting the wrapper

-   You can build the wrapper yourself by downloading **ffmpeg.go** and running `go build -ldflags="-s -w" ffmpeg.go`
-   Alternatively you can download the binary compiled through GitHub actions by
    -   Clicking **Actions** above
    -   Clicking the latest top most
    -   Scroll down to **Artifacts**

### Setting up

Ignore .exe when working on Linux.

-   I'm not sure how Emby works without Docker, but you have to find the path to **ffmpeg.exe** used by Emby. I think you can set this yourself on Windows.
-   Rename **ffmpeg.exe** to **\_ffmpeg.exe**
-   Add an environment variable named **`EMBY_CUSTOM_FFMPEG_PATH`** which points to the **\_ffmpeg.exe** file (e.g. **C:\\Program Files\\ffmpeg\\bin\\\_ffmpeg.exe**)
-   Place the compiled/downloaded **ffmpeg.exe** file where the original used to be
-   Try running **ffmpeg.exe --help** and if it works, it's successfully wrapping around **\_ffmpeg.exe**
-   If you'd like to change the bitrate, set environment variable **`EMBY_CUSTOM_AC3_BITRATE`**. By default its **`640000`** which is **640 kbps**
