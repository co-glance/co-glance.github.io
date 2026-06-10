# Co-GLANCE: Uncertainty-Aware Active Perception for Heterogeneous Robot Teaming

### Project Page | Dataset | Demo Notebook

- **Project Page:** https://co-glance.github.io/
- **Dataset:** https://huggingface.co/datasets/co-glance/Co-GLANCE
- **Demo Notebook:** [notebooks/dataset_viewer.ipynb](notebooks/dataset_viewer.ipynb)

---

## TL;DR

Co-GLANCE is a real-world aerial-ground dataset and project page for studying person detection, occlusion reasoning, and multi-robot perception with heterogeneous robot teams.

The dataset provides:

- Over 4,000 synchronized RGB frames from aerial and ground viewpoints
- 2,071 annotated frame pairs across two outdoor collection events
- Ground-truth person bounding box annotations
- Raw sensor streams from heterogeneous robot platforms
- Raw ROS 2 bag files for evaluation beyond static image benchmarks

---

## Dataset Overview

Co-GLANCE is designed for evaluating perception systems in realistic outdoor conditions where viewpoint, occlusion, and platform capability matter. Unlike simulation-only or road-scene datasets, Co-GLANCE contains synchronized data from aerial and ground robots operating on semi-structured outdoor terrain.

The dataset supports research in:

- Aerial-ground collaborative perception
- Person detection and tracking
- Occlusion-aware perception
- Multi-robot active perception
- Evaluation of autonomy stacks using raw sensor streams

---

## Scenarios

The dataset contains two outdoor collection scenarios.

| Scenario | Description | Ground Hardware | Aerial Hardware | Runs |
| --- | --- | --- | --- | --- |
| Construction Scenario (2025-03-30) | A construction worker walks through a construction site while ground and aerial viewpoints record synchronized observations. | GoPro HERO 10 | Arducam HQ IMX477 | 4 |
| Camouflage Scenario (2025-04-14) | Two individuals wearing camouflage move through a visually occluded outdoor area. | Boston Dynamics Spot front-left and front-right cameras, stitched | GoPro HERO 10 | 3 |

---

## Data Categories

Each run is split into scene-type categories depending on the event.

| Category | Construction Scenario | Camouflage Scenario |
| --- | --- | --- |
| Clean | Exactly one person is clearly visible. | Both individuals are fully visible with no occlusion. |
| Filtered Out | No humans are present. These frames are excluded from primary detection analysis. | Not used. |
| Multiperson | More than one person is visible simultaneously. | Not used. |
| Partial Occlusion | Not used. | One or both individuals are partially hidden by environmental features. |
| Full Occlusion | Not used. | One or both individuals are completely obscured from view. |

---

## Frame Counts

The dataset contains **2,071 annotated frame pairs** in total.

### Construction Scenario (03-30)

| Run | Clean | Filtered Out | Multiperson | All |
| --- | ---: | ---: | ---: | ---: |
| 1 | 77 | 34 | 7 | 118 |
| 2 | 229 | 43 | 54 | 326 |
| 3 | 88 | 54 | 138 | 280 |
| 4 | 135 | 144 | 206 | 485 |
| **Total** | **529** | **275** | **405** | **1,209** |

### Camouflage Scenario (04-14)

| Run | Clean | Partial Occlusion | Full Occlusion | All |
| --- | ---: | ---: | ---: | ---: |
| 1 | 54 | 101 | 31 | 186 |
| 2 | 210 | 252 | 83 | 545 |
| 3 | 69 | 47 | 15 | 131 |
| **Total** | **333** | **400** | **129** | **862** |

---

## Dataset Structure

```text
dataset/
├── 03-30/                        # Construction Scenario
│   └── <run>/                    # 4 runs
│       ├── all/
│       ├── clean/
│       ├── filtered_out/
│       └── multiperson/
│           ├── aerial/
│           │   ├── rgb/          # PNG frames
│           │   ├── gt_bbox/      # Frames with bounding boxes rendered on image
│           │   ├── acceleration/ # JSON sensor stream
│           │   ├── attitude/     # JSON sensor stream
│           │   ├── gps_position/ # JSON RTK GPS stream
│           │   └── *.json        # Additional odometry data
│           └── ground/
│               └── <same structure>
└── 04-14/                        # Camouflage Scenario
    └── <run>/                    # 3 runs
        ├── all/
        ├── clean/
        ├── partial_occlusion/
        └── full_occlusion/
            ├── aerial/
            │   └── <same structure>
            └── ground/
                └── <same structure>
```

---

## Data Fields

Each aerial and ground platform folder contains synchronized data streams.

| Folder / File | Format | Description |
| --- | --- | --- |
| `rgb/` | PNG | Raw RGB frames from the platform camera |
| `gt_bbox/` | PNG | Corresponding frames with ground-truth bounding boxes rendered on the image |
| `acceleration/` | JSON | IMU linear acceleration stream |
| `attitude/` | JSON | Platform orientation / attitude stream |
| `gps_position/` | JSON | RTK GPS position stream |
| `*.json` | JSON | Additional odometry and platform state data |

---

## Demo Notebook

A lightweight dataset viewer notebook is included in this repository:

- [Open the local dataset viewer notebook](notebooks/dataset_viewer.ipynb)
- [View the notebook on Hugging Face](https://huggingface.co/datasets/co-glance/Co-GLANCE/blob/main/dataset_viewer.ipynb)

GitHub will render the local `.ipynb` when opened from the repository. Use the notebook to inspect dataset samples, visualize synchronized aerial-ground frames, and review annotations.

---

## Website

The project website is located in the `docs/` folder and is intended to be served with GitHub Pages:

```text
docs/
├── index.html
└── static/
    ├── css/
    ├── images/
    ├── js/
    └── videos/
notebooks/
└── dataset_viewer.ipynb
```

To publish with GitHub Pages, set:

- Source: `Deploy from a branch`
- Branch: `main`
- Folder: `/docs`

---

## Citation

Citation information will be added upon publication.

---

## License

The dataset is released under the Creative Commons Attribution 4.0 International License (CC BY 4.0).

