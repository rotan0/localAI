
**LocalAI** is the free, Open Source OpenAI alternative. LocalAI act as a drop-in replacement REST API that's compatible with OpenAI (Elevenlabs, Anthropic... ) API specifications for local AI inferencing. It allows you to run LLMs, generate images, audio (and not only) locally or on-prem with consumer grade hardware, supporting multiple model families. Does not require GPU. It is created and maintained by [Ettore Di Giacinto](https://github.com/mudler).


## 📚🆕 Local Stack Family

🆕 LocalAI is now part of a comprehensive suite of AI tools designed to work together:

<table>
  <tr>
    <td width="50%" valign="top">
      <a href="https://github.com/mudler/LocalAGI">
        <img src="https://raw.githubusercontent.com/mudler/LocalAGI/refs/heads/main/webui/react-ui/public/logo_2.png" width="300" alt="LocalAGI Logo">
      </a>
    </td>
    <td width="50%" valign="top">
      <h3><a href="https://github.com/mudler/LocalAGI">LocalAGI</a></h3>
      <p>A powerful Local AI agent management platform that serves as a drop-in replacement for OpenAI's Responses API, enhanced with advanced agentic capabilities.</p>
    </td>
  </tr>
  <tr>
    <td width="50%" valign="top">
      <a href="https://github.com/mudler/LocalRecall">
        <img src="https://raw.githubusercontent.com/mudler/LocalRecall/refs/heads/main/static/localrecall_horizontal.png" width="300" alt="LocalRecall Logo">
      </a>
    </td>
    <td width="50%" valign="top">
      <h3><a href="https://github.com/mudler/LocalRecall">LocalRecall</a></h3>
      <p>A REST-ful API and knowledge base management system that provides persistent memory and storage capabilities for AI agents.</p>
    </td>
  </tr>
</table>

## Screenshots


| Talk Interface | Generate Audio |
| --- | --- |
| ![Screenshot 2025-03-31 at 12-01-36 LocalAI - Talk](./docs/assets/images/screenshots/screenshot_tts.png) | ![Screenshot 2025-03-31 at 12-01-29 LocalAI - Generate audio with voice-en-us-ryan-low](./docs/assets/images/screenshots/screenshot_tts.png) |

| Models Overview | Generate Images |
| --- | --- |
| ![Screenshot 2025-03-31 at 12-01-20 LocalAI - Models](./docs/assets/images/screenshots/screenshot_gallery.png) | ![Screenshot 2025-03-31 at 12-31-41 LocalAI - Generate images with flux 1-dev](./docs/assets/images/screenshots/screenshot_image.png) |

| Chat Interface | Home |
| --- | --- |
| ![Screenshot 2025-03-31 at 11-57-44 LocalAI - Chat with localai-functioncall-qwen2 5-7b-v0 5](./docs/assets/images/screenshots/screenshot_chat.png) | ![Screenshot 2025-03-31 at 11-57-23 LocalAI API - c2a39e3 (c2a39e3639227cfd94ffffe9f5691239acc275a8)](./docs/assets/images/screenshots/screenshot_home.png) |

| Login | Swarm |
| --- | --- |
|![Screenshot 2025-03-31 at 12-09-59 ](./docs/assets/images/screenshots/screenshot_login.png) | ![Screenshot 2025-03-31 at 12-10-39 LocalAI - P2P dashboard](./docs/assets/images/screenshots/screenshot_p2p.png) |

## 💻 Quickstart

Run the installer script:

```bash
# Basic installation
curl https://localai.io/install.sh | sh
```

For more installation options, see [Installer Options](https://localai.io/docs/advanced/installer/).

### macOS Download:

<a href="https://github.com/mudler/LocalAI/releases/latest/download/LocalAI.dmg">
  <img src="https://img.shields.io/badge/Download-macOS-blue?style=for-the-badge&logo=apple&logoColor=white" alt="Download LocalAI for macOS"/>
</a>

Or run with docker:

> **💡 Docker Run vs Docker Start**
> 
> - `docker run` creates and starts a new container. If a container with the same name already exists, this command will fail.
> - `docker start` starts an existing container that was previously created with `docker run`.
> 
> If you've already run LocalAI before and want to start it again, use: `docker start -i local-ai`

### CPU only image:

```bash
docker run -ti --name local-ai -p 8080:8080 localai/localai:latest
```

### NVIDIA GPU Images:

```bash
# CUDA 12.0
docker run -ti --name local-ai -p 8080:8080 --gpus all localai/localai:latest-gpu-nvidia-cuda-12

# CUDA 11.7
docker run -ti --name local-ai -p 8080:8080 --gpus all localai/localai:latest-gpu-nvidia-cuda-11

# NVIDIA Jetson (L4T) ARM64
docker run -ti --name local-ai -p 8080:8080 --gpus all localai/localai:latest-nvidia-l4t-arm64
```

### AMD GPU Images (ROCm):

```bash
docker run -ti --name local-ai -p 8080:8080 --device=/dev/kfd --device=/dev/dri --group-add=video localai/localai:latest-gpu-hipblas
```

### Intel GPU Images (oneAPI):

```bash
docker run -ti --name local-ai -p 8080:8080 --device=/dev/dri/card1 --device=/dev/dri/renderD128 localai/localai:latest-gpu-intel
```

### Vulkan GPU Images:

```bash
docker run -ti --name local-ai -p 8080:8080 localai/localai:latest-gpu-vulkan
```

### AIO Images (pre-downloaded models):

```bash
# CPU version
docker run -ti --name local-ai -p 8080:8080 localai/localai:latest-aio-cpu

# NVIDIA CUDA 12 version
docker run -ti --name local-ai -p 8080:8080 --gpus all localai/localai:latest-aio-gpu-nvidia-cuda-12

# NVIDIA CUDA 11 version
docker run -ti --name local-ai -p 8080:8080 --gpus all localai/localai:latest-aio-gpu-nvidia-cuda-11

# Intel GPU version
docker run -ti --name local-ai -p 8080:8080 localai/localai:latest-aio-gpu-intel

# AMD GPU version
docker run -ti --name local-ai -p 8080:8080 --device=/dev/kfd --device=/dev/dri --group-add=video localai/localai:latest-aio-gpu-hipblas
```

For more information about the AIO images and pre-downloaded models, see [Container Documentation](https://localai.io/basics/container/).

To load models:

```bash
# From the model gallery (see available models with `local-ai models list`, in the WebUI from the model tab, or visiting https://models.localai.io)
local-ai run llama-3.2-1b-instruct:q4_k_m
# Start LocalAI with the phi-2 model directly from huggingface
local-ai run huggingface://TheBloke/phi-2-GGUF/phi-2.Q8_0.gguf
# Install and run a model from the Ollama OCI registry
local-ai run ollama://gemma:2b
# Run a model from a configuration file
local-ai run https://gist.githubusercontent.com/.../phi-2.yaml
# Install and run a model from a standard OCI registry (e.g., Docker Hub)
local-ai run oci://localai/phi-2:latest
```


