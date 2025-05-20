# Genre-Driven Storytelling from Images using PyTorch XPU backend
## Overview
This sample explores the generation of creative, genre-specific stories from images, specifically optimized for Intel hardware using the PyTorch XPU backend. 
The core of the sample lies in its ability to understand visual content through the VLM and then weave a story that adheres to the conventions and style of the selected genre. By utilizing the PyTorch XPU backend, this sample aims for efficient computation and accelerated story generation on Intel Arc GPUs and other compatible hardware.

## Contents

- [Sample Workflow](./Readme.md#sample-workflow)
- [Pre-requisites](./Readme.md#pre-requisites)
- [Sample structure](./Readme.md#sample-structure)
- [Run the `Genre-driven storytelling` Sample](./Readme.md#sample-structure)
   - [Using `uv`](./Readme.md#using-uv)
   - [AI PC from Intel](./Readme.md#ai-pc-from-intel)
   - [Intel® Tiber™ AI Cloud](./Readme.md#intel-tiber-ai-cloud)
- [Sample Execution](./Readme.md#sample-execution)

## Sample Workflow
It takes an image and a user-defined genre (e.g., fantasy, horror, romance, sci-fi) as input and leverages a Vision Language Model (VLM) to craft engaging narratives that are visually inspired and thematically aligned with the chosen genre.

<img width="800" alt="image" src="./assets/story-generation.png">

## Pre-requisites

| Optimized for                      | Description                                                                                                                                                                 |
| :----------------------------------| :---------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| OS                        | Windows 11 64-bit (22H2, 23H2) and newer or Ubuntu* 22.04 64-bit (with Linux kernel 6.6+) and newer                                                                                                                                                                                                              |
| Hardware                  | Intel® Core™ Ultra Processors, Intel Arc™ Graphics, or Intel Graphics, Intel® Data Center GPU Max Series                                                                                                                                                                                                         |
| Software                  | [Intel® GPU drivers from Intel® Arc™ & Iris® Xe Graphics for Windows](https://www.intel.com/content/www/us/en/download/785597/intel-arc-iris-xe-graphics-windows.html), [uv](https://docs.astral.sh/uv/)                                                                                                                                                                                       |
| Minimum RAM required      | 32 GB or more                                                                                                                                                                        |
| Optional                  | Monitor GPU Utilization using [Intel XPU Manager](https://github.com/intel/xpumanager)
                                                                                     
## Sample Structure

This Sample directory contains:
| Notebook                           | Description                                                                                            |
| :--------------------------------- | :----------------------------------------------------------------------------------------------------- |
| [Genre-driven-storytelling.ipynb](./Genre-driven-storytelling.ipynb) | Enables faster and affordable company logo generation using language and diffusion models with the help of automated prompt engineering  |


## Run the `Automated Logo Generation` Sample:

### Using `uv`:
The sample uses [uv](https://docs.astral.sh/uv/) for environment management. Steps to install `uv` can be found [here](https://docs.astral.sh/uv/getting-started/installation/).

1. Setup the environment
   - Initialize the environment
       ```bash
       uv init
       ```
       > Run `uv sync` if your face any dependency issues.
   
2. Launch Jupyter Notebook
   ```bash
   uv run jupyter lab
   ```

### AI PC from Intel
<div class="alert alert-block alert-info"> <b>NOTE:</b> You can run the step on both, <b>Windows and Ubuntu</b>. </div>

1. Open the [Genre driven storytelling](./Automated_Logo_Generation.ipynb) notebook file in the jupyter notebook, select the default kernel i.e. `Python(ipykernel)` and run the code cells one by one in the notebook.

### Intel Tiber AI Cloud
1. Open the [Genre driven storytelling](./Automated_Logo_Generation.ipynb) notebook file in the jupyter notebook, select the default kernel i.e. `Python(ipykernel)` and run the code cells one by one in the notebook.

## Sample Execution
GPU utilization would be observed as this sample is optimized to run on Intel XPUs.

<img alt="image" width=600 src="./assets/xpu-usage.png"/>

### Creative story generation using Vision-language models

<img alt="image" width=600 src="./assets/story-example.png"/>




