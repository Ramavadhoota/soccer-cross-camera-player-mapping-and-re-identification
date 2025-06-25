# soccer-cross-camera-player-mapping-and-re-identification
This repository consists of all the out put and trained model of yolov11 and the codes

Cross-Camera Player Mapping (Broadcast ↔ Tacticam)

Player Re-Identification from a Different Match (Match B)
— powered by YOLOv11 + CLIP embeddings, generating SoccerNet-style frame visualizations.

# ⚽ Player Re-Identification and Cross-Camera Mapping in Football Videos

This project provides a modular deep learning pipeline for:

1. 🎥 **Cross-Camera Player Mapping**: Match the same players from different camera angles (e.g., broadcast and tacticam views).
2. 🔁 **Re-identification**: Track and re-identify players who reappear after leaving the frame or appear in a different match.

The visual output mimics **SoccerNet-style annotated frames** showing matched players across views with consistent IDs.

---

## 🧠 Core Features

- ✅ **Player Detection** using fine-tuned YOLOv11 (`best.pt`)
- ✅ **Deep Visual Embedding** using [OpenAI CLIP](https://github.com/openai/CLIP)
- ✅ **Cosine Similarity Matching** for cross-view and cross-match ID consistency
- ✅ **SoccerNet-style comparison image generation**
- ✅ **Modular, easy-to-extend design** (e.g., add DeepSORT, homography, grid view)

---

## 📂 Folder Structure

.
├── Player_Reid_Clip.ipynb # Colab-ready notebook (core code)
├── best.pt # Your YOLOv11 model (player + ball detection)
├── videos/
│ ├── broadcasting.mp4 # Match A - broadcast view
│ ├── tacticam.mp4 # Match A - alternate view
│ └── 15sec_input_720p.mp4 # Match B - re-ID scenario
├── matchA_mapping/ # Output: mapped players across camera angles
├── matchB_reid/ # Output: re-identified players across matches
├── README.md # This file


---

## 🚀 How to Run (Colab Recommended)

1. Clone this repository or upload code to your Colab workspace.
2. Upload your three video files and YOLOv11 model to Google Drive.
3. Update the following paths in the script:

``python
model_path = "/content/drive/MyDrive/best.pt"
broadcast_path = "/content/drive/MyDrive/broadcasting.mp4"
tacticam_path = "/content/drive/MyDrive/tacticam.mp4"
matchB_path = "/content/drive/MyDrive/15sec_input_720p.mp4"

Run the full pipeline by executing the notebook cells.

Check the output folders (matchA_mapping, matchB_reid) for comparison images.

🛠️ Requirements
Install required packages (automatically included in the script):
pip install git+https://github.com/openai/CLIP.git
pip install ftfy regex tqdm opencv-python-headless ultralytics matplotlib scikit-learn


📊 Output Examples
Each player ID match will be saved as:

matchA_mapping/player_1_clipmatch.png

matchB_reid/player_3_clipmatch.png

These images contain bounding boxes and labels for the same player across views or matches.

📌 Model Notes
YOLOv11 best.pt model should be fine-tuned on football-specific data with labels: ['player', 'ball'].

CLIP (ViT-B/32) is used for feature extraction of player crops to ensure semantic consistency across different views.

🔄 To Do / Extensions
 Add DeepSORT for temporal track consistency

 Visualize multi-frame 2×2 grid like full SoccerNet examples

 Add homography to align field positions across cameras

🧑‍💻 Author
Sushant Hegde – LinkedIn | GitHub
Built using PyTorch, OpenAI CLIP, and YOLOv11 by Ultralytics.
