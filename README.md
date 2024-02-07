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
pip install -r requirements.txt
```

Download large model to data dir
```sh
git clone https://huggingface.co/Systran/faster-whisper-large-v3
```
or quantized to INT8 (smaller and faster Largev3)
```sh
git clone https://huggingface.co/neowisard/fwhisper-large-v3-int8
rm folder fwhisper-large-v3-int8 to large-v3i
```

Run a server anyone can connect to:
Full precision
```sh
/usr/bin/python3 -m wyoming_faster_whisper --uri 'tcp://0.0.0.0:10300' --data-dir /ai/models/whisper --model large-v3 --beam-size 1 --language ru --download-dir /ai/models/whisper --compute-type float16 --device cuda --initial-prompt "promt"
```
Quantized INT8

```sh
python3 -m wyoming_faster_whisper --uri 'tcp://0.0.0.0:10300' --data-dir /ai/models/whisper --model large-v3i --beam-size 1 --language ru --download-dir /ai/models/whisper --compute-type int8_float32 --device cuda
```


## Docker Image

``` sh
docker run -it -p 10300:10300 -v /path/to/local/data:/data rhasspy/wyoming-whisper \
    --model tiny-int8 --language en
```

[Source](https://github.com/rhasspy/wyoming-addons/tree/master/whisper)
