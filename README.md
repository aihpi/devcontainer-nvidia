<div style="background-color: #ffffff; color: #000000; padding: 10px;">
<img src="images\img\logo_aisc_bmftr.jpg">
<h1> CUDA DevContainer Template
</div>


---

This repository provides a reproducible VS Code DevContainer that can access NVIDIA GPUs immediately after build time—nvidia-smi works without additional manual steps, even when you run inside Kubernetes (for example via devpod or Rancher Desktop).

## Features

- **.devcontainer/devcontainer.json**: Uses an `nvidia/cuda:12.1.0-devel-ubuntu22.04` image and passes `--gpus=all` to Docker.
- **.devcontainer/install-dev-tools.sh**: Installs CUDA 12.1, cuDNN 8.9.7, and the exact nvidia-utils / libnvidia-compute 570.133.20 packages that match the host driver.
- **docs/gpu-setup.md**: Detailed information how to fix different NVML "driver / library mismatch" errors.
- **docs/devpod-setup.md**: Setting up Devpod with the correct provider options.
- **notebooks/gpu-test.ipynb**: Minimal Jupyter notebook that verifies PyTorch GPU visibility.


## Setup and Installation
### 🚀 Quick Start (Devpod)
1.	**Configure Devpod**  
If you haven’t done so, follow **docs/devpod-setup.md** to add the _aihpi_ provider with GPU support.
2. **Create a new workspace**  
   - In the Devpod UI click **Workspaces** → **Create** → **Git Repo**
   - Enter the following Workspace Source: `https://github.com/aihpi/devcontainer-nvidia.git`
3. **Pick the provider**  
Select **aihpi** as the provider (the GPU-enabled provider you created in step 1).
4. **Set the Devcontainer Path**  
`.devcontainer/devcontainer.json`
5. **Create the workspace**  
   - Click Create Workspace and wait for the image to build.
   - The build installs CUDA 12.1, cuDNN 8.9.7, and NVIDIA user-space libraries matching driver **570.133.20**.
6. **Verify GPU access**  
Open a terminal inside the new VS Code window and run:
`nvidia-smi`

You should see the GPU table (no NVML mismatch).
If you don’t see a GPU, check that:  
- The node has nvidia.com/gpu resources.
-	The provider is configured with --gpus=all.
-	The user-space library versions match the host driver (see docs/gpu-setup.md).


## References

- [NVIDIA-Enabled Devcontainer](https://github.com/felixboelter/devcontainer-nvidia-base/)
- [DevPod](https://devpod.sh/)

## Author
- [Felix Boelter](https://www.linkedin.com/in/felixboelter/)

## License
MIT

---

## Acknowledgements
<img src="00_aisc/img/logo_bmftr_de.png" alt="drawing" style="width:170px;"/>

The [AI Service Centre Berlin Brandenburg](http://hpi.de/kisz) is funded by the [Federal Ministry of Research, Technology and Space](https://www.bmbf.de/) under the funding code 01IS22092.
