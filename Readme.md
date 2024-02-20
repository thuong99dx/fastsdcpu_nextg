# FastSD CPU :sparkles:

FastSD CPU is a faster version of Stable Diffusion on CPU. Based on [Latent Consistency Models](https://github.com/luosiallen/latent-consistency-model) and
[Adversarial Diffusion Distillation](https://nolowiz.com/fast-stable-diffusion-on-cpu-using-fastsd-cpu-and-openvino/).
The following interfaces are available :

- Desktop GUI (Qt)
- WebUI
- CLI (CommandLine Interface)

Using __OpenVINO(SD Turbo)__, it took __1.7 seconds__ to create a single 512x512 image on a __Core i7-12700__.

## Fast 1 step inference (SD/SDXL Turbo - Adversarial Diffusion Distillation,ADD)

Added support for ultra fast 1 step inference using [sdxl-turbo](https://huggingface.co/stabilityai/sdxl-turbo) model

:exclamation: These SD turbo models are intended for research purpose only.

Text to Image -  Implemented

Image to Image - Implemented

OpenVINO model - Implemented

### Inference Speed

Tested on Core i7-12700 to generate 512x512 image(1 step).

__SD Turbo__

| Diffusion Pipeline    | Latency       |
| --------------------- | ------------- |
| Pytorch               | 7.8s          |
| OpenVINO              | 5s            |
| OpenVINO + TAESD      | 1.7s          |

__SDXL Turbo__

| Diffusion Pipeline    | Latency       |
| --------------------- | ------------- |
| Pytorch               | 10s           |
| OpenVINO              | 5.6s          |
| OpenVINO + TAESDXL    | 2.5s          |

### OpenVINO SD Turbo models

We have converted SD/SDXL Turbo models to OpenVINO for fast inference on CPU. These models are intended for research purpose only. Also we converted TAESDXL MODEL to OpenVINO and

- *SD Turbo OpenVINO* - [rupeshs/sd-turbo-openvino](https://huggingface.co/rupeshs/sd-turbo-openvino)
- *SDXL Turbo OpenVINO int8* - [rupeshs/sdxl-turbo-openvino-int8](https://huggingface.co/rupeshs/sdxl-turbo-openvino-int8)
- *TAESDXL OpenVINO* - [rupeshs/taesdxl-openvino](https://huggingface.co/rupeshs/taesdxl-openvino)

You can directly use these models in FastSD CPU.

## Know issues

- TAESD will not work with OpenVINO image to image workflow

## Supported platforms

- Windows
- Linux
- Mac
- Raspberry PI 4

![FastSD CPU Desktop GUI Screenshot](https://raw.githubusercontent.com/rupeshs/fastsdcpu/main/docs/images/fastsdcpu-gui.jpg)

## Features

- Supports 256,512,768 image sizes
- Supports Windows and Linux
- Saves images and diffusion setting used to generate the image
- Settings to control,steps,guidance and seed
- Added safety checker setting
- Maximum inference steps increased to 25
- Added [OpenVINO](https://github.com/openvinotoolkit/openvino) support
- Added web UI
- Added CommandLine Interface(CLI)
- Fixed OpenVINO image reproducibility issue
- Fixed OpenVINO high RAM usage,thanks [deinferno](https://github.com/deinferno)
- Added multiple image generation support
- Application settings
- Added Tiny Auto Encoder for SD (TAESD) support, 1.4x speed boost (Fast,moderate quality)
- Safety checker disabled by default
- Added SDXL,SSD1B - 1B LCM models
- Added LCM-LoRA support, works well for fine-tuned Stable Diffusion model 1.5  or SDXL models
- Added negative prompt support in LCM-LoRA mode
- LCM-LoRA models can be configured using text configuration file
- Added support for custom models for OpenVINO (LCM-LoRA baked)
- OpenVINO models now supports negative prompt (Set guidance >1.0)
- Real-time inference support,generates images while you type (experimental)
- Fast 2,3 steps inference
- Lcm-Lora fused models for faster inference
- Supports integrated GPU(iGPU) using OpenVINO (export DEVICE=GPU)
- 5.7x speed using OpenVINO(steps: 2,tiny autoencoder)
- Image to Image support (Use Web UI)
- OpenVINO image to image support
- Fast 1 step inference (SDXL Turbo)
- Added SD Turbo support
- Added image to image support for Turbo models (Pytorch and OpenVINO)
- Added image variations support
- Added 2x upscaler (EDSR and Tiled SD upscale (experimental)),thanks [monstruosoft](https://github.com/monstruosoft) for SD upscale
- Works on Android + Termux + PRoot

## 2 Steps fast inference

FastSD CPU supports 2 to 3 steps fast inference using LCM-LoRA workflow. It works well with SD 1.5 models.

![2 Steps inference](https://raw.githubusercontent.com/rupeshs/fastsdcpu/main/docs/images/2steps-inference.jpg)

## OpenVINO support

Thanks [deinferno](https://github.com/deinferno) for the OpenVINO model contribution.
We can get 2x speed improvement when using OpenVINO.
Thanks [Disty0](https://github.com/Disty0) for the conversion script.

### Convert SD 1.5 models to OpenVINO LCM-LoRA fused models

We first creates LCM-LoRA baked in model,replaces the scheduler with LCM and then converts it into OpenVINO model. For more details check [LCM OpenVINO Converter](https://github.com/rupeshs/lcm-openvino-converter), you can use this tools to convert any StableDiffusion 1.5 fine tuned models to OpenVINO.

## Real-time text to image (EXPERIMENTAL)

Now we can generate near real-time text to images using FastSD CPU.

**CPU (OpenVINO)**

Near real-time inference on CPU using OpenVINO, run the `start-realtime.bat` batch file and open the link in brower (Resolution : 256x256,Latency : 2.3s on Intel Core i7)

**Colab (GPU)**

You can use the colab to generate real-time images (Resolution : 512x512,Latency : 500ms on Tesla T4)
[![Open in Colab](https://colab.research.google.com/assets/colab-badge.svg)](https://colab.research.google.com/drive/1slhhDhxPcb0Xk19nMuxWT9xG6VrmE4a5?usp=sharing)

Watch YouTube video :

[![IMAGE_ALT](https://img.youtube.com/vi/s2zSxBHkNE0/sddefault.jpg)](https://youtu.be/s2zSxBHkNE0)

## Models

Fast SD supports LCM models and LCM-LoRA models.

### LCM Models

Following LCM models are supported:

- *LCM_Dreamshaper_v7* - <https://huggingface.co/SimianLuo/LCM_Dreamshaper_v7> by [Simian Luo](https://github.com/luosiallen)
- *SSD-1B* -LCM distilled version of [segmind/SSD-1B](https://huggingface.co/segmind/SSD-1B)
- *StableDiffusion XL* -LCM distilled version of [stable-diffusion-xl-base-1.0](https://huggingface.co/stabilityai/stable-diffusion-xl-base-1.0)

### OpenVINO models

These are LCM-LoRA baked in models.

- [LCM-dreamshaper-v7-openvino](https://huggingface.co/rupeshs/LCM-dreamshaper-v7-openvino) by Rupesh
- [LCM_SoteMix](https://huggingface.co/Disty0/LCM_SoteMix) by Disty0

### LCM-LoRA models

- *lcm-lora-sdv1-5* - distilled consistency adapter for [runwayml/stable-diffusion-v1-5](https://huggingface.co/runwayml/stable-diffusion-v1-5)
- *lcm-lora-sdxl* - Distilled consistency adapter for [stable-diffusion-xl-base-1.0](https://huggingface.co/stabilityai/stable-diffusion-xl-base-1.0)
- *lcm-lora-ssd-1b* - Distilled consistency adapter for [segmind/SSD-1B](https://huggingface.co/segmind/SSD-1B)

:exclamation: Currently no support for OpenVINO LCM-LoRA models.

### How to add new LCM-LoRA models

To add new model follow the steps:
For example we will add `wavymulder/collage-diffusion`, you can give Stable diffusion 1.5 Or SDXL,SSD-1B fine tuned models.

1. Open `configs/stable-diffusion-models.txt` file in text editor.
2. Add the model ID `wavymulder/collage-diffusion`  or locally cloned path.

Updated file as shown below :

```Lykon/dreamshaper-8
Fictiverse/Stable_Diffusion_PaperCut_Model
stabilityai/stable-diffusion-xl-base-1.0
runwayml/stable-diffusion-v1-5
segmind/SSD-1B
stablediffusionapi/anything-v5
wavymulder/collage-diffusion
```

Similarly we can update `configs/lcm-lora-models.txt` file with lcm-lora ID.

### How to use LCM-LoRA models offline

Please follow the steps to run LCM-LoRA models offline :

- In the settings ensure that  "Use locally cached model" setting is ticked.
- Download the model for example `latent-consistency/lcm-lora-sdv1-5`
Run the following commands:

```
git lfs install
git clone https://huggingface.co/latent-consistency/lcm-lora-sdv1-5
```

Copy the cloned model folder path for example "D:\demo\lcm-lora-sdv1-5" and update the `configs/lcm-lora-models.txt` file as shown below :

```
D:\demo\lcm-lora-sdv1-5
latent-consistency/lcm-lora-sdxl
latent-consistency/lcm-lora-ssd-1b
```

- Open the app and select the newly added local folder in the combo box menu.
- That's all!

## FastSD CPU on Windows

:exclamation:**You must have a working Python installation.(Recommended : Python 3.10 or 3.11 )**

Clone/download this repo or download release.

### Installation

- Double click `install.bat`  (It will take some time to install,depending on your internet speed.)

### Run

You can run in desktop GUI mode or web UI mode.

#### Desktop GUI

- To start desktop GUI double click `start.bat`

#### Web UI

- To start web UI double click `start-webui.bat`

## FastSD CPU on Linux

Ensure that you have Python 3.8 or higher version installed.

- Clone/download this repo
- In the terminal, enter into fastsdcpu directory
- Run the following command

  `chmod +x install.sh`

  `./install.sh`

#### To start Desktop GUI

  `./start.sh`

#### To start Web UI

  `./start-webui.sh`

## FastSD CPU on Mac

![FastSD CPU running on Mac](https://raw.githubusercontent.com/rupeshs/fastsdcpu/main/docs/images/fastsdcpu-mac-gui.jpg)

### Installation

Ensure that you have Python 3.8 or higher version installed.

- Clone/download this repo
- In the terminal, enter into fastsdcpu directory
- Run the following command

  `chmod +x install-mac.sh`

  `./install-mac.sh`

#### To start Desktop GUI

  `./start.sh`

#### To start Web UI

  `./start-webui.sh`

Thanks [Autantpourmoi](https://github.com/Autantpourmoi) for Mac testing.

:exclamation:We don't support OpenVINO on Mac.

If you want to increase image generation speed on Mac(M1/M2 chip) try this:

`export DEVICE=mps` and start app `start.sh`

## Web UI screenshot

![FastSD CPU WebUI Screenshot](https://raw.githubusercontent.com/rupeshs/fastsdcpu/main/docs/images/fastcpu-webui.png)

## Google Colab

Due to the limitation of using CPU/OpenVINO inside colab, we are using GPU with colab.
[![Open in Colab](https://colab.research.google.com/assets/colab-badge.svg)](https://colab.research.google.com/drive/1SuAqskB-_gjWLYNRFENAkIXZ1aoyINqL?usp=sharing)

## CLI mode (Advanced users)

![FastSD CPU CLI Screenshot](https://raw.githubusercontent.com/rupeshs/fastsdcpu/main/docs/images/fastcpu-cli.png)

 Open the terminal and enter into fastsdcpu folder.
 Activate virtual environment using the command:

#### Windows users

 (Suppose FastSD CPU available in the directory "D:\fastsdcpu")
  `D:\fastsdcpu\env\Scripts\activate.bat`

#### Linux users

  `source env/bin/activate`

Start CLI  `src/app.py -h`

## Android (Termux + PRoot)

FastSD CPU running on Google Pixel 7 Pro.

![FastSD CPU Android Termux Screenshot](https://raw.githubusercontent.com/rupeshs/fastsdcpu/main/docs/images/fastsdcpu-android-termux-pixel7.png)

### 1. Prerequisites

First you have to [install Termux](https://wiki.termux.com/wiki/Installing_from_F-Droid) and [install PRoot](https://wiki.termux.com/wiki/PRoot). Then install and login to Ubuntu in PRoot.

### 2. Install FastSD CPU

Run the following command to install without Qt GUI.

 `proot-distro login ubuntu`

 `./install.sh --disable-gui`

 After the installation you can use WebUi.

  `./start-webui.sh`

  Note : If you get `libgl.so.1` import error run `apt-get install ffmpeg`.

  Thanks [patienx](https://github.com/patientx) for this guide  [Step by step guide to installing FASTSDCPU on ANDROID](https://github.com/rupeshs/fastsdcpu/discussions/123)

## Raspberry PI 4 support

Thanks WGNW_MGM for Raspberry PI 4 testing.FastSD CPU worked without problems.
System configuration - Raspberry Pi 4 with 4GB RAM, 8GB of SWAP memory.

### License

The fastsdcpu project is available as open source under the terms of the [MIT license](https://github.com/rupeshs/fastsdcpu/blob/main/LICENSE)

## Contributors

<a href="https://github.com/rupeshs/fastsdcpu/graphs/contributors">
  <img src="https://contrib.rocks/image?repo=rupeshs/fastsdcpu" />
</a>
