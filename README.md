# Wyoming Faster Whisper for Large v3 model with official faster whisper on CUDA

[Wyoming protocol](https://github.com/rhasspy/wyoming) server for the [faster-whisper](https://github.com/guillaumekln/faster-whisper/) speech to text system.

## Home Assistant Add-on

[![Show add-on](https://my.home-assistant.io/badges/supervisor_addon.svg)](https://my.home-assistant.io/redirect/supervisor_addon/?addon=core_whisper)

[Source](https://github.com/home-assistant/addons/tree/master/whisper)

## Local Install

Clone the repository and set up Python virtual environment:

``` sh
git clone https://github.com/rhasspy/wyoming-faster-whisper.git
cd wyoming-faster-whisper
script/setup
```

Download model to data dir
```sh
git clone https://huggingface.co/Systran/faster-whisper-large-v3
```

Run a server anyone can connect to:
```sh
/usr/bin/python3 -m wyoming_faster_whisper --uri 'tcp://0.0.0.0:10300' --data-dir /ai/models/whisper --model large-v3 --beam-size 1 --language ru --download-dir /ai/models/whisper --compute-type float16 --device cuda --initial-prompt "promt"

```

## Docker Image

``` sh
docker run -it -p 10300:10300 -v /path/to/local/data:/data rhasspy/wyoming-whisper \
    --model tiny-int8 --language en
```

[Source](https://github.com/rhasspy/wyoming-addons/tree/master/whisper)
