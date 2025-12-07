## task 1: 2D to 3D model generation

A simple program to convert 2D images into 3D `.glb` models using OpenAI's Shap-E. It runs locally. It's set up to force CPU usage on Macs to avoid the common "MPS float64" crashes that happen with PyTorch on Apple Silicon (M1).

![Python](https://img.shields.io/badge/Python-3.8+-blue.svg)
![License](https://img.shields.io/badge/License-MIT-green.svg)

# project structure
gen-three-d-model/
├── gen_3d.py          
├── requirements.txt   
├── README.md          
└── input/             # source images here

# after cloning repo create and activate virtual environment
python3 -m venv venv
source venv/bin/activate
# on Windows use: venv\Scripts\activate

# install dependencies
pip install -r requirements.txt

# basic run
python3 gen_3d.py --input "input/hat.jpeg" --output "output/hat.glb"

Flag	            Default	        Description
--input / -i	Required	        Path to the image you want to convert.
--output / -o	output/model.glb	Where to save the file.
--steps / -s	64	                Number of diffusion steps. Lower is faster. Higher is slower but better detail.

# example
python3 gen_3d.py -i input/image.png -s 8 


First Run: The first time it will be downloading about 2GB of models from OpenAI. It might take around 25 to 30 mins (to download the models) for the first time to run as it runs on CPU by default on Mac. This is normal and may take around 4 minutes per image for subsequent runs.

Mac Users: I've disabled GPU acceleration (MPS) in the script because Shap-E uses 64-bit floats that Apple's Metal shaders don't support yet. It runs on CPU

After generating a .glb file, it can viewed at [meshy.ai](https://www.meshy.ai/3d-tools/online-viewer/glb) or in macOS via spacebar in finder


## task 2: AR hat demo

This project is a lightweight browser-based face-tracking AR demo built with **MindAR** and **A-Frame**. It overlays a 3D model (cowboy hat) on the user’s face and allows real-time adjustments via keyboard controls.

## Features
- Real-time face tracking with MindAR.
- Load and display a GLB 3D model.
  
Keyboard controls for adjusting:
  - Position (`Arrow Keys`, `W/S` for depth)
  - Rotation (`Q/E` tilt, `A/D` yaw)
  - Scale (`+/-`)
  - Presets (`R` reset, `T` custom fit)

## required files for this demo:
project-root/
├─ index.html 
└─ cowboy_hat.glb    # input .glb file

We ensure `cowboy_hat.glb` is in the same directory as `index.html`

### prerequisites
- VS Code with **Live Server** extension installed.
- Modern browser (Chrome, Edge) with camera support.
- Camera access is to be allowed in the browser.

### Running the Demo
1. Right-click `index.html` → **“Open with Live Server”**.
3. The demo will launch in the default browser (Live Server serves via `http://127.0.0.1:5500` or similar).
4. Click **Start Camera** to initialize face tracking.

### Keyboard Controls
| Key(s)            | Action                           |
|------------------|----------------------------------|
| `Arrow Keys`      | Move X/Y                        |
| `W` / `S`         | Move Z (depth)                  |
| `Q` / `E`         | Tilt (X rotation)               |
| `A` / `D`         | Yaw (Y rotation)                |
| `+` / `-`         | Scale up / down                 |
| `R`               | Reset to default preset         |
| `T`               | Apply custom preset             |

