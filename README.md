# ADAS Video ML Model Binary Store

## Overview

For use with [https://github.com/t4g/ml-adas-pilot] platform:

A modular CLI application that processes dashcam video (file or RTSP stream) and outputs an MP4 with ADAS-style overlays including lane detection, road damage detection, pedestrian detection with collision-risk highlighting, and forward motion estimation.

_or your own YOLOv8 project_

___

Due to large complexity of training models, included here are a few pretrained models to get you started.

 ```text
  ┌─────────┬───────────┬──────────────┬────────────┬───────────────┐    
  │  Class  │ Box mAP50 │ Box mAP50-95 │ Mask mAP50 │ Mask mAP50-95 │
  ├─────────┼───────────┼──────────────┼────────────┼───────────────┤    
  │ all     │ 0.438     │ 0.206        │ 0.389      │ 0.169         │    
  ├─────────┼───────────┼──────────────┼────────────┼───────────────┤    
  │ crack   │ 0.195     │ 0.074        │ 0.153      │ 0.044         │    
  ├─────────┼───────────┼──────────────┼────────────┼───────────────┤
  │ pothole │ 0.681     │ 0.338        │ 0.626      │ 0.294         │    
  └─────────┴───────────┴──────────────┴────────────┴───────────────┘    
  ```
  
  Pothole detection is strong (68% mAP50). Crack detection is lower due  
  to the more fragmented nature of cracks, but still functional.

  The model is at:
  ```runs/segment/runs/damage_seg/train_v2/weights/best.pt```

  Use it with the pipeline:

  ```bash
  python -m adas_pipeline --input video.mp4 --output out.mp4 \
      --damage-model runs/segment/runs/damage_seg/train_v2/weights/best.pt
  ```

## Results

Leading model: [segment/runs/damage_seg/train_v2]

![segment/runs/damage_seg/train_v2/val_batch2_labels.png](Example)

![segment/runs/damage_seg/train_v2/results.png](Overview)

![segment/runs/damage_seg/train_v2/MaskPR_curve.png](Seg P-R)

![segment/runs/damage_seg/train_v2/BoxPR_curve.png](Bounding Box P-R)

## Authors

Author: [@t4g] (Kyle Younge)