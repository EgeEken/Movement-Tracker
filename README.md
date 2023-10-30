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
<details><summary>Results: (click here to open)</summary>
<video loop autoplay muted playsinline src="https://github.com/EgeEken/Movement-Tracker/assets/96302110/8337dc90-976b-49f5-85c9-d94cb1561980"> 
</video>
</details>

### Creating a contrast video, this is done by subtracting frame i-1 from every frame i

```py
contrast = imgpro.contrast_video(vid) # Alternatively, contrast_video("video.mp4")
imgpro.WriteVideo(filename + "_contrast", contrast)
```

<details><summary>Results: (click here to open)</summary>
<video loop autoplay muted playsinline src="https://github.com/EgeEken/Movement-Tracker/assets/96302110/b41d6d77-2d59-4e4f-a7d9-97ef5ba223aa"> 
</video>
</details>



### Creating a black and white contrast video, same system, but doesnt take hue changes into account

```py
normalized = imgpro.contrast_video_bnw(vid) # Alternatively, contrast_video_bnw("video.mp4")
imgpro.WriteVideo(filename + "_contrast_normalized", normalized)
```

<details><summary>Results: (click here to open)</summary>
<video loop autoplay muted playsinline src="https://github.com/EgeEken/Movement-Tracker/assets/96302110/92e81bb6-bb5a-4d47-b0c4-1b21bd5e3676"> 
</video>
</details>

### Creating a motion tracked video, this returns the same video but with a red dot with a white center placed on the tracked movement center

```py
tracker = imgpro.movement_tracker_cv2(vid)
imgpro.WriteVideo(filename + "_movement_tracker", tracker)
```

<details><summary>Results: (click here to open)</summary>
<video loop autoplay muted playsinline src="https://github.com/EgeEken/Movement-Tracker/assets/96302110/8dfca2d3-d0a2-4fe3-b1f5-cc5e4b586a25"> 
</video>
</details>

### Creating a motion tracked video, with a threshold to lower the impact camera shaking or noise has on the motion tracking, the higher threshold used, the more strict the program will be with what it considers "motion"

```py
threshold = 50
tracker = imgpro.movement_tracker_cv2_threshold(vid, threshold)
imgpro.WriteVideo(filename + "_movement_tracker_threshold_" + str(threshold), tracker)
```

<details><summary>Results: (click here to open)</summary>
<video loop autoplay muted playsinline src="https://github.com/EgeEken/Movement-Tracker/assets/96302110/ea338a14-da0d-456a-b8d3-940664cde33f"> 
</video>
</details>
