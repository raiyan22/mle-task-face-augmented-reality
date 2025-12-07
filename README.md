## task 1: 2D to 3D model generation

A simple program to convert 2D images into 3D `.glb` models using OpenAI's Shap-E. It runs locally. It's set up to force CPU usage on Macs to avoid the common "MPS float64" crashes that happen with PyTorch on Apple Silicon (M1).

![Python](https://img.shields.io/badge/Python-3.8+-blue.svg)
![License](https://img.shields.io/badge/License-MIT-green.svg)

# project structure
```
gen-three-d-model/
├── gen_3d.py          
├── requirements.txt   
├── README.md          
└── input/             # source images here
```

### after cloning repo create and activate virtual environment
```
python3 -m venv venv
source venv/bin/activate
```
on Windows use: ```venv\Scripts\activate```

### install dependencies
```pip3 install -r requirements.txt```

<img width="1544" height="1079" alt="Screenshot 2025-12-07 at 10 59 42 AM" src="https://github.com/user-attachments/assets/bc5797d1-802c-4c03-b1b2-1324192de3d9" />

### basic run
```python3 gen_3d.py --input input/hat.jpeg```


| Flag / Option       | Description                                              | Required | Default / Example            |
|---------------------|----------------------------------------------------------|----------|------------------------------|
| `--input` / `-i`   | Path to the image you want to convert.                   | Yes      |                              |
| `--output` / `-o`  | Output file path, e.g., `output/model.glb`             |          | `output/model.glb`           |
| `--steps` / `-s`   | Number of diffusion steps. Lower is faster; higher yields better detail. |          | `64`                         |

### example
```python3 gen_3d.py -i input/hat.jpeg -s 8```

```python3 gen_3d.py -i input/hat.jpeg -steps 64```

Here -s 8 denotes the diffusion steps. the value 64 gives moderately good looking 3d model while taking a good period of time.  

First Run: The first time it will be downloading about 2GB of models from OpenAI. It might take around 25 to 30 mins (to download the models) for the first time to run as it runs on CPU by default on Mac. This is normal and may take around 7 minutes per image for subsequent runs.

for Mac users: I've disabled GPU acceleration (MPS) in the script because Shap-E uses 64-bit floats that Apple's Metal shaders don't support yet. It runs on CPU. I also tried to test the TripoSR architecture due to its state-of-the-art performance but unfortunately it was not working as expected yet.

After generating a .glb file, it can viewed at [meshy.ai](https://www.meshy.ai/3d-tools/online-viewer/glb) or in macOS via spacebar in finder:

<img width="1903" height="1079" alt="Screenshot 2025-12-07 at 11 20 54 AM" src="https://github.com/user-attachments/assets/92c582fd-1698-4390-9548-bf6ca179ab13" />


## task 2: AR hat demo

This project is a lightweight browser-based face-tracking AR demo built with **MindAR** and **A-Frame**. It overlays a 3D model (cowboy hat) on the user’s face and allows real-time adjustments via keyboard controls.

![Python](https://img.shields.io/badge/Python-3.8+-blue.svg)
![License](https://img.shields.io/badge/License-MIT-green.svg)

# Features
- Real-time face tracking with MindAR.
- Load and display a GLB 3D hat model on the head of a user using webcam.
  
Keyboard controls for adjusting:
  - Position (`Arrow Keys`, `W/S` for depth)
  - Rotation (`Q/E` tilt, `A/D` yaw)
  - Scale (`+/-`)
  - Presets (`R` reset, `T` custom fit)

### required files for this demo:
```
project-root/
├─ index.html 
└─ cowboy_hat.glb    # input .glb file
```

We ensure `cowboy_hat.glb` is in the same directory as `index.html`

### prerequisites
- VS Code with **Live Server** extension installed.
- Modern browser (Chrome, Edge) with camera support.
- Camera access is to be allowed in the browser.

### running the Demo
1. Right-click `index.html` → **“Open with Live Server”** in VS Code.
3. The will launch in the default browser (Live Server serves via `http://127.0.0.1:5500`).
4. Click **Start Camera** to initialize face tracking.

### Keyboard Controls
| Key(s)            | Action                          |
|-------------------|---------------------------------|
| `Arrow Keys`      | Move X/Y                        |
| `W` / `S`         | Move Z (depth)                  |
| `Q` / `E`         | Tilt (X rotation)               |
| `A` / `D`         | Yaw (Y rotation)                |
| `+` / `-`         | Scale up / down                 |
| `R`               | Reset to default preset         |
| `T`               | Apply custom preset             |

The improvement ideas for both the tasks are written in separate improvements.md file 
