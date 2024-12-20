# OpenPose_DanceComparing

This repository provides a comprehensive set of tools to analyze, process, and visualize joint angle differences between two videos (e.g., student vs. teacher movements). The project leverages keypoint extraction, dynamic time warping, and skeleton visualization to highlight areas of significant movement differences. This README.md is made by chatGPT. 😊

models, bin, tables and output, check from: https://drive.google.com/drive/folders/1PSy92vllcudy35nP8EFolWO0oyZj5Ktp?usp=sharing

## Environment

- Python 3.8.5
- Opencv-python >=4.5
- NumPy >=1.20
- Matplotlib >=3.3
- OpenPose (Python API, manually compiled)
- scikit-learn >=0.24
- fastdtw >=0.3.4

## Features

1. **Keypoint Extraction**:
   - Extracts keypoints from videos using OpenPose.
   - Handles missing frames by applying interpolation for smoother results.

2. **Angle Difference Calculation**:
   - Computes joint angle differences between two sets of keypoints.
   - Supports frame alignment using truncation or interpolation.

3. **Dynamic Time Warping (DTW)**:
   - Measures the similarity between two temporal sequences of joint angles.
   - Provides insights into movement synchronization.

4. **Heatmap Visualization**:
   - Generates heatmaps to visualize angle differences across frames and joints.

5. **Skeleton Visualization**:
   - Draws skeletons on video frames.
   - Highlights joints with significant angle differences.

6. **High-Difference Joint Detection**:
   - Identifies joints with significant movement differences using a customizable threshold.

## Workflow

### Step 1: Preprocess Videos
Using the script `000_preprocess_videos.py`, resample student and teacher videos to ensure the same frame count, FPS, and resolution.

### Step 2: Extract Keypoints
The script `001_save_keypoints_and_offset.py` extracts keypoints from the videos and computes joint angle differences.

### Step 3: Analyze Angle Differences
With `002_angle_diff_analysis.py`, analyze the computed angle differences by:
- Clustering frames based on movement patterns.
- Detecting frames with high average angle differences.
- Saving high-difference joint information.

### Step 4: Visualize Heatmaps
Use `003_heatmap_angle.py` to generate heatmaps of angle differences for intuitive visualization of movement discrepancies.

### Step 5: Create Highlighted Video
Finally, with `004_visualize_diff.py`, create a video overlaying skeletons on student and teacher videos, highlighting joints with significant angle differences.

## Installation

1. Clone this repository:
   ```bash
   git clone https://github.com/chika19qian/OpenPose_DanceComparing.git
   cd MyOpenPose
   ```

2. **Install dependencies**:
   ```bash
   pip install -r requirements.txt
   ```
   **Note**: The `requirements.txt` file has not been fully tested, and some dependencies may need manual installation or adjustment.

3. **Set up OpenPose**:
   OpenPose is required for keypoint extraction, but it cannot be installed via pip. You need to compile OpenPose manually and ensure the `pyopenpose` library is accessible in your environment. Place the compiled `pyopenpose` files in the `OpenPose_DanceComparing/` directory.

   - Refer to the [OpenPose documentation](https://github.com/CMU-Perceptual-Computing-Lab/openpose) for compilation instructions.
   - Make sure to include the `pyopenpose` library in your Python environment.

4. Create a `models` directory and download the OpenPose models:
   ```bash
   mkdir models
   # Add OpenPose model files here
   ```

## Usage

### Preprocess Videos
```bash
python 000_preprocess_videos.py
```
Ensure that the student and teacher videos are in the `examples/` directory.

### Extract Keypoints
```bash
python 001_save_keypoints_and_offset.py
```
The keypoints and angle differences will be saved in the `table/` directory.

### Analyze and Visualize
Run each script step-by-step:

1. **Analyze Angle Differences**:
   ```bash
   python 002_angle_diff_analysis.py
   ```
   Outputs include:
   - **Frame-wise average angle differences**: `output/lip_frame_average_difference.png`
   - **Joint-wise average angle differences**: `output/lip_joint_average_difference.png`
   - **Clustering of frames**: `output/lip_frame_clustering.png`
   - **DTW results**: Printed DTW distance for angle synchronization analysis.

2. **Generate Heatmaps**:
   ```bash
   python 003_heatmap_angle.py
   ```

3. **Create Highlighted Video**:
   ```bash
   python 004_visualize_diff.py
   ```

The output will be saved in the `output/` directory.

## Directory Structure

```
.
├── bin/                   # OpenPose compiled binaries and pyopenpose
├── examples/              # Original student and teacher videos
├── models/                # OpenPose model files
├── myenv/                 # Optional virtual environment directory
├── output/                # Generated visualizations and videos
├── table/                 # Keypoints and angle difference data
├── videos/                # Processed videos
├── .gitignore
├── 000_preprocess_videos.py
├── 001_save_keypoints_and_offset.py
├── 002_angle_diff_analysis.py
├── 003_heatmap_angle.py
├── 004_visualize_diff.py
├── pyopenpose.cp38-win_amd64.pyd  # OpenPose Python library
├── requirements.txt
└── README.md
```



## Example Output

- **Frame-Wise Average Angle Differences**:
  ![Frame Average]![1angle_heatmap_csv](https://github.com/user-attachments/assets/80399006-6e87-46c9-929c-12af44efbd99)


- **Joint-Wise Average Angle Differences**:
  ![Joint Average]![1joint_average_difference](https://github.com/user-attachments/assets/7aa935fe-7801-401b-b6de-0bb7b8aa0ea3)

- **Clustering Visualization**:
  ![Clustering]![1frame_clustering](https://github.com/user-attachments/assets/52f94cac-00f7-434b-a931-8deb96cfbf56)

- **Heatmap**:
  ![Heatmap Example]![1angle_heatmap_csv](https://github.com/user-attachments/assets/d68c9bef-4112-42e1-9d18-da0adc3d6239)

- **Skeleton Visualization**:
  ![Skeleton Video]

## Contribution

Contributions are welcome! Feel free to submit issues or pull requests for improvements.


