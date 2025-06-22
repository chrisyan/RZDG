# RZDG
Code and dataset of paper IEEE IV 2025 "Framework and Multi-modal Dataset for Roadwork Zone Detection and Geo-localization"

The **RZDG (Roadwork Zone Detection and Geo-localization)** dataset is a multi-modal dataset designed to support research in roadwork zone perception, detection, tracking and geo-localization. It contains both **real-world (RZDG-real)** and **simulated (RZDG-sim)** data, structured in the [KITTI format](http://www.cvlibs.net/datasets/kitti/), and supports tasks such as:

- Image semantic segmentation  
- 3D object detection and tracking 
- Geo-localization of roadwork zones  

## Dataset Structure

### RZDG-Sim (Simulated)
- **Objects**: 419 road beacons, 254 barriers  
- **Scenarios**: 203 distinct roadwork zone scenarios across 8 simulated towns  
- **Frames**: 8591  

### RZDG-Real (Real-World)
- **Objects**: 3643 road beacons, 8837 barriers  
- **Scenarios**: 28 distinct roadwork zone scenarios 
- **Frames**: 1357

The overall structure of the dataset is as follows:
```text
RWDG_dataset
├── ImageSets
├── kitti_gt_database
├── testing
│   ├── calib
│   ├── image_0
│   └── lidar
└── training
    ├── calib
    ├── image_0
    ├── label_0
    └── lidar
```


## Detection & Tracking Pipeline

We adopt **[MMDetection3D](https://github.com/open-mmlab/mmdetection3d)** for 3D object detection and **[AB3DMOT](https://github.com/xinshuoweng/AB3DMOT)** for 3D object tracking.

To adapt these tools to the RZDG dataset, we provide **custom modifications** in the form of patch files located in the `patches/` directory.


| File                          | Target Repository | Description |
|------------------------------|-------------------|-------------|
| `patches/mmdetection3d.patch` | MMDetection3D      | Modifications to support RZDG dataset format, object classes, and evaluation setup |
| `patches/AB3DMOT.patch`       | AB3DMOT            | Tracker changes to handle geo-localization and RZDG-specific object cues |

Use following commands to apply patches to the Original Repositories
```bash
cd path/to/mmdetection3d
git apply ../patches/mmdetection3d.patch

cd path/to/AB3DMOT
git apply ../patches/AB3DMOT.patch
```

## Acknowledgment

This project is built upon the excellent open-source frameworks [MMDetection3D](https://github.com/open-mmlab/mmdetection3d) and [AB3DMOT](https://github.com/xinshuoweng/AB3DMOT). We sincerely thank the developers and maintainers of these repositories for their contributions to the research community.

