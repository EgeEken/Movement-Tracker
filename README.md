# Movement Tracker
Tracks the movement in a given video, placing a red dot on the most active object.

I will not be publishing this as a separate file, instead it will be added as a feature to my [ImageProcessing_Ege](https://github.com/EgeEken/ImageProcessing_Ege) library.

This repository will serve as a tutorial on which functions to use for this purpose and how to use them.


## Installing and importing the library

1-) Download and install [Git](https://git-scm.com/downloads)

2-) Run the following command in the command terminal
```bash
pip install "git+"https://github.com/EgeEken/ImageProcessing_Ege""
```

3-) Use `from ImageProcessing_Ege import imgpro` in a python script or runtime (`from ImageProcessing_Ege import imgpro as (prefix)` if you don't want to write the whole thing every time)

## Relevant Functions

### Reading video and saving it into a matrix

```py
from ImageProcessing_Ege import imgpro
filename = "video.mp4" # Alternatively, ("video"), the extension ".mp4" is added if needed.
vid = imgpro.ReadVideo(filename)
```


### Creating a contrast video, this is done by subtracting frame i-1 from every frame i

```py
contrast = imgpro.contrast_video(vid) # Alternatively, contrast_video("video.mp4")
imgpro.WriteVideo(filename + "_contrast", contrast)
```



### Creating a black and white contrast video, same system, but doesnt take hue changes into account

```py
normalized = imgpro.contrast_video_bnw(vid) # Alternatively, contrast_video_bnw("video.mp4")
imgpro.WriteVideo(filename + "_contrast_normalized", normalized)
```

### Creating a motion tracked video, this returns the same video but with a red dot with a white center placed on the tracked movement center

```py
tracker = imgpro.movement_tracker_cv2(vid)
imgpro.WriteVideo(filename + "_movement_tracker", tracker)
```

### Creating a motion tracked video, with a threshold to lower the impact camera shaking or noise has on the motion tracking, the higher threshold used, the more strict the program will be with what it considers "motion"

```py
threshold = 50
tracker = imgpro.movement_tracker_cv2_threshold(vid, threshold)
imgpro.WriteVideo(filename + "_movement_tracker_threshold_" + str(threshold), tracker)
```
