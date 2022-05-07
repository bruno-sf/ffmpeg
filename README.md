# ffmpeg

An Alpine based docker image multiarch with ffmpeg version 4.4.built with gcc 10.3.1 (Alpine 10.3.1_git20211027).
Link:https://hub.docker.com/repository/docker/brunoferreira/ffmpeg


Why ``ffmpeg``?
-----------------------
Based on https://github.com/bruno-sf/conversor-webm-mp4

![ffmpeg](https://raw.githubusercontent.com/linuxserver/docker-templates/master/linuxserver.io/img/ffmpeg.png)


### Prerequisites

- Docker 🐋

### Usage

Just use it like executing ffmpeg locally.

Basic Transcode:
```
docker run --rm -it \
  -v $(pwd):/conversor \
  brunoferreira/ffmpeg \
  -i /config/input.mkv \
  -c:v libx264 \
  -b:v 4M \
  -vf scale=1280:720 \
  -c:a copy \
  /config/output.mkv
```

Bulk compress .mp4 files in the current directory:
```
 docker run --rm -it -v ${PWD}:/conversor ffmpeg find /conversor -maxdepth 1 -type f -name "*.mp4" -exec ffmpeg -i {} -f mp4 -vcodec libx264 -preset fast -profile:v main -acodec aac -b:v 256k -bufsize 256k {}.mp4 -hide_banner \;
```

### Tips :thought_balloon:
Use it with alias, for example:
```
alias @vid_conv_mp4_to_mp4_bulk_compress='docker run -it -v ${PWD}:/conversor ffmpeg find /conversor -maxdepth 1 -type f -name "*.mp4" -exec ffmpeg -i {} -f mp4 -vcodec libx264 -preset fast -profile:v main -acodec aac -b:v 256k -bufsize 256k {}.mp4 -hide_banner \;'
```

## License

This project is licensed under the MIT License - see the [LICENSE.md](LICENSE.md) file for details.
