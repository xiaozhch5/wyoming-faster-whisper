# Wyoming Faster Whisper for Large v3 model with official faster whisper on CUDA

[Wyoming protocol](https://github.com/rhasspy/wyoming) server for the [faster-whisper](https://github.com/guillaumekln/faster-whisper/) speech to text system.

##  Pre-requisites :
NVIDIA GPU, driver , cuda  installed

## Home Assistant Add-on

[![Show add-on](https://my.home-assistant.io/badges/supervisor_addon.svg)](https://my.home-assistant.io/redirect/supervisor_addon/?addon=core_whisper)

[Source](https://github.com/home-assistant/addons/tree/master/whisper)

## Local Install

Set up Python virtual environment:

Virtual Python env (Only for Conda using)
``` sh
conda create -n fwf python=3.10
conda activate fwf
```
Clone the repository 

``` sh
git clone https://github.com/neowisard/wyoming-faster-whisper.git
cd wyoming-faster-whisper
pip install -r requirements.txt
```

Download large model to data (/ai/models/whisper) dir

```sh
git clone https://huggingface.co/Systran/faster-whisper-large-v3
mv fwhisper-large-v3 large-v3
```
or quantized to INT8 (smaller and faster Largev3)
```sh
git clone https://huggingface.co/neowisard/fwhisper-large-v3-int8
mv fwhisper-large-v3-int8 large-v3i
```

Run a server anyone can connect to:
Full precision
```sh
python3 -m wyoming_faster_whisper --uri 'tcp://0.0.0.0:10300' --data-dir /ai/models/whisper --model large-v3 --beam-size 1 --language ru --download-dir /ai/models/whisper --compute-type float16 --device cuda --initial-prompt "promt"
```
Quantized INT8

```sh
python3 -m wyoming_faster_whisper --uri 'tcp://0.0.0.0:10300' --data-dir /ai/models/whisper --model large-v3i --beam-size 1 --language ru --download-dir /ai/models/whisper --compute-type int8_float32 --device cuda
```


[Source](https://github.com/rhasspy/wyoming-addons/tree/master/whisper)
