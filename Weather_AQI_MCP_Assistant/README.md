# Weather-AQI MCP Assistant
## Overview
The `Weather-AQI MCP Assistant` is an interactive & asynchronous application architected for the real-time orchestration of environmental telemetry, specifically weather and Air Quality Index (AQI) data for a given location, ultimately generating actionable health and safety recommendations. Its distributed backend comprises three distinct Model Context Protocol (MCP) servers, implemented with **`FastMCP`** (a FastAPI-inspired Python framework), whose tools are invoked by MCP clients.

Weather and AQI Tools, utilizing external API Services are hosted on **Intel® Core™ Ultra Processors** followed by Data Analysis & Actionable safety precautions/recommendations are generated with the help of [Qwen2.5-3B-Instruct model](https://huggingface.co/Qwen/Qwen2.5-3B-Instruct) is loaded using the [**PyTorch XPU backend**](https://docs.pytorch.org/docs/stable/notes/get_start_xpu.html) to leverage Intel hardware acceleration.


## Table of Contents

- [Sample Workflow](#sample-workflow)
- [Pre-requisites](#pre-requisites)
- [Project Structure](#project-structure)
- [Weather & AQI Data Requirements](#weather--aqi-data-requirements)
- [Installing Prerequisites && Setting Up the Environment](#installing-prerequisites--setting-up-the-environment)
   - [For Windows](#for-windows)
   - [For Linux](#for-linux)
- [Running the Sample && execution output](#running-the-sample--execution-output)
- [Troubleshooting](#troubleshooting)
---

## Sample Workflow

This diagram illustrates how the WeatherAQI MCP Assistant operates end-to-end within an AI PC environment, combining MCP Compliant Servers, an MCP client, and external APIs.

- **User Input**: User provides a location (e.g California). The MCP client sends this to the AQI and Weather MCP servers.
- **AQI MCP Server**: Converts location to latitude/longitude (via [geocoding API](https://open-meteo.com/en/docs/geocoding-api)), then calls [OpenWeatherMap Air Pollution API](https://openweathermap.org/api/air-pollution)  for AQI data, returning it to the client.
- **Weather MCP Server**: Converts location to latitude/longitude (via [geocoding API](https://open-meteo.com/en/docs/geocoding-api)), then calls [Open-Meteo Weather Forecast API](https://open-meteo.com/en/docs#api_response) for weather data, returning it to the client.
- **LLM Inferencing MCP Server**: Receives both AQI and weather reports from the client, and the LLM (Qwen/Qwen2.5-3B-Instruct) generates personalized safety guidelines.
- **Final Result**: LLM output (safety advice, health risks, precautions) is sent back to the MCP client for user presentation.

![How it works](./assets/WeatherAQI_MCP_Assistant_Workflow.png)

---

## Pre-requisities

| Optimized for                      | Description                                                                                                                                                                 |
| :----------------------------------| :---------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| OS                        | Windows 11 64-bit (22H2, 23H2) and newer or Ubuntu* 22.04 64-bit (with Linux kernel 6.6+) and newer                                                                                                                                                                                                              |
| Hardware                  | Intel® Core™ Ultra Processors, Intel Arc™ Graphics, or Intel Graphics, Intel® Data Center GPU Max Series                                                                                                                                                                                                         |
| Software                  | [Intel® GPU drivers from Intel® Arc™ & Iris® Xe Graphics for Windows](https://www.intel.com/content/www/us/en/download/785597/intel-arc-iris-xe-graphics-windows.html), [uv](https://docs.astral.sh/uv/)                                                                                                                                                                                       |
| Minimum RAM required      | 32 GB or more                                                                                                                                                                        |
| External API Services                 | [geocoding API](https://open-meteo.com/en/docs/geocoding-api), [Open-Meteo Weather Forecast API](https://open-meteo.com/en/docs#api_response), [OpenWeatherMap Air Pollution API](https://openweathermap.org/api/air-pollution) |
| Optional                  | Monitor GPU Utilization using [Intel XPU Manager](https://github.com/intel/xpumanager) |

---


## Project Structure

    Weather-AQI MCP Assistant/                                             # Project Sample folder
    ├── assets/                                                            # Assets folder which contains the images and diagrams
    │   ├── Generating_safety_guidelines_using_Pytorch_XPU.png             # Output screenshot image 1
    │   ├── WeatherAQI_MCP_Assistant_Workflow.png                          # Workflow image
    │   └── safety_measures.png                                            # Output screenshot image 2
    ├── Readme.md                                                          # Readme file which contains all the details and instructions about the project sample
    ├── 1_weather_server.py                                                # python file that retrives weather information
    ├── 2_Air_Quality_Index_server.py                                      # python file that retrives Air Quality Index(AQI) information
    ├── 3_LLM_inference_server.py                                          # python file which gives safety guidelines based on weather and AQI reports
    ├── weather_AQI_MCP_Assistant.ipynb                                    # Notebook file to excute the project sample
    ├── pyproject.toml                                                     # Requirements for the project sample
    └── uv.lock                                                            # File which captures the packages installed for the project sample

---

## Run the `Weather_AQI_MCP_Assistant Sample`:
### Weather & AQI Data Requirements

This project uses two public APIs to provide real-time weather and air quality information:
  1. **Open-Meteo API**\
     Purpose:
      - Geocoding: Convert a city or place name into coordinates (latitude & longitude).
      - Weather Forecast: Get current weather data (temperature, wind speed, etc.)
      
     Usage:
      - No API key required! Open-Meteo is free for testing and development.
  2. **OpenWeatherMap API**\
     Purpose:
      - Provides Air Quality Index (AQI) and detailed pollutant data for any coordinates
     
     Usage:
      - OpenWeatherMap requires an API key for all AQI endpoints.
     
     To get API key:
      - Sign up [here](https://home.openweathermap.org/users/sign_in)
      - Log in and go to API keys in your account dashboard.
      - Copy your key.
     
     Add it to the project:
      - Add your AQI API Key in the .env file present in your project root:
      ```
      AQI_API_KEY=<aqi_key>
      ```
> **NOTE**: API activation could take 3-6 hours. Immediate usage might lead to errors (e.g."cod":401, "message": "Invalid API key).
---


### Installing Prerequisites && Setting Up the Environment

#### For Windows:
To install any software using commands, Open the Command Prompt as an administrator by right-clicking the terminal icon and selecting `Run as administrator`.
1. **GPU Drivers installation**\
   Download and install the Intel® Graphics Driver for Intel® Arc™ B-Series, A-Series, Intel® Iris® Xe Graphics, and Intel® Core™ Ultra Processors with Intel® Arc™ Graphics from [here](https://www.intel.com/content/www/us/en/download/785597/intel-arc-iris-xe-graphics-windows.html)\
   **IMPORTANT:** Reboot the system after the installation.

2. **Git for Windows**\
   Download and install Git from [here](https://git-scm.com/downloads/win)

3. **uv for Windows**\
   Steps to install `uv` in the Command Prompt are as follows. Please refer to the [documentation](https://docs.astral.sh/uv/getting-started/installation/) for more information.
   ```
   powershell -ExecutionPolicy ByPass -c "irm https://astral.sh/uv/install.ps1 | iex"
   ```
   **NOTE:** Close and reopen the Command Prompt to recognize uv.
   
#### For Linux:
To install any software using commands, Open a new terminal window by right-clicking the terminal and selecting `New Window`.
1. **GPU Drivers installation**\
   Download and install the GPU drivers from [here](https://dgpu-docs.intel.com/driver/client/overview.html)

2. **Dependencies on Linux**\
   Install Curl, Wget, Git using the following commands:
   - For Debian/Ubuntu-based systems:
   ```
   sudo apt update && sudo apt -y install curl wget git
   ```
   - For RHEL/CentOS-based systems:
   ```
   sudo dnf update && sudo dnf -y install curl wget git
   ```

3. **uv for Linux**\
   Steps to install uv are as follows. Please refer to the [documentation](https://docs.astral.sh/uv/getting-started/installation/) for more information.
   - If you want to use curl to download the script and execute it with sh:
   ```
   curl -LsSf https://astral.sh/uv/install.sh | sh
   ```
   - If you want to use wget to download the script and execute it with sh:
   ```
   wget -qO- https://astral.sh/uv/install.sh | sh
   ```
   **NOTE:** Close and reopen the Terminal to recognize uv.

---

### Run the Sample
   
1. In the Command Prompt/terminal, navigate to `WeatherAQI MCP Assistant` folder after cloning the sample:
   ```
   cd <path/to/Weather-AQI MCP Assistant/folder>
   ```
   
2. Log in to Hugging Face, generate a token, and download the required model:

   `huggingface-cli` lets you interact directly with the Hugging Face Hub from a terminal. Log in to [Huggingface](https://huggingface.co/) with your credentials. You need a [User Access Token](https://huggingface.co/docs/hub/security-tokens) from your [Settings page](https://huggingface.co/settings/tokens). The User Access Token is used to authenticate your identity to the Hub.\
   Once you have your token, run the following command in your terminal.
   ```
   uv run huggingface-cli login
   ```
   This command will prompt you for a token. Copy-paste yours and press Enter.
   ```
   uv run huggingface-cli download Qwen/Qwen2.5-3B-Instruct
   ```
   
3. Run all MCP servers locally:

   This sample has 3 MCP servers (runs on 3 different ports):
     - **Weather** (port no - 8000)
     - **AQI (Air Quality Index)** (port no - 8001)
     - **LLM (Large Language Model) Inference** (port no - 8002)
  
   To run them all, open **3 separate terminals**
  
   Terminal 1: Start the Weather MCP server
   ```
   uv run 1_weather_server.py
   ```
   Terminal 2: Start the AQI MCP server
   ```
   uv run 2_Air_Quality_Index_server.py
   ```
   Terminal 3: Start the LLM Inferencing MCP server
   ```
   uv run 3_LLM_inference_server.py
   ```
   
4. Launch Jupyter Lab and Run the notebook:
   
   Open the [Weather-AQI MCP Assistant](./Weather_AQI_MCP_Assistant.ipynb) notebook in the Jupyter Lab.
   - In the Jupyter Lab go to the kernel menu in the top-right corner of the notebook interface and choose default kernel i.e. `Python 3 (ipykernel)` from the available kernels list and run the code cells one by one in the notebook.
   ```
   uv run jupyter lab
   ```
---

## Sample Execution

### GPU Utilization
GPU utilization can be seen in the Task Manager while generating safety guidelines for the requested location which are processing on Intel XPUs.
   ![Generating_safety_guidelines_using_Pytorch_XPU](./assets/Generating_safety_guidelines_using_Pytorch_XPU.png)


### Sample Output
Based on the weather and AQI report in the requested location, the model generates safety guidelines.
   ![safety_measures](./assets/safety_measures.png)


---

## Troubleshooting

- **`uv` Dependency Issues:**
  Run `uv clean` before running `uv sync` command to clear out any remaining cache.
- **File Access Issues:** Restart the kernel and run the cells again.
- **API_KEY Issues:**
  - Invalid API Key Error
    1. OpenWeather API_KEY takes several hours to get activate. Make sure it is activated(you would be notified via Mail) before using it.
    2. Add your API_KEY in [.env file](./.env)
- **403 Forbidden Error with MCP Servers**
  You might encounter this error if you are behind a company proxy, make sure you add the appropriate proxy details, similar to the below lines, in the [Weather_AQI_MCP_Assistant.ipynb Notebook](./Weather_AQI_MCP_Assistant.ipynb)
   > os.environ['HTTP_PROXY'] = "http://proxy.example.com:port"
   > 
   > os.environ['HTTPS_PROXY'] = "http://proxy.example.com:port"
   > 
   > os.environ['NO_PROXY'] = "localhost,127.0.0.1"
---

