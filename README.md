# UsefulSnippets




## Nvidia
[Nvidia](./nvidia/README.md)


## Pytorch Snippets
[Pytorch](./pytorch/README.md)

## Bash

```bash
### 1. Find and remove empty files/directories
find ./ -type f -empty	
find ./ -type d -empty

find ./ -type f -size 0 -delete
find ./ -type d -empty -delete
```


## Jupyter
### 1. Autoreload
```bash
%load_ext autoreload
%autorelaod 2
%pylab inline
import sys
# sys.path.append('')
```

## FFMEG
### 1. vertically and horizonally stacking
https://stackoverflow.com/questions/11552565/vertically-or-horizontally-stack-mosaic-several-videos-using-ffmpeg
Only video:
```bash
ffmpeg -i input0 -i input1 -filter_complex vstack=inputs=2 output
ffmpeg -i input0 -i input1 -filter_complex hstack=inputs=2 output
```

## Python

```python
### 1. Find the closest face pose from a video compared to a given image wiht a face

from scipy.spatial import ConvexHull
def find_best_frame(source, driving, cpu=False):
    import face_alignment

    def normalize_kp(kp):
        kp = kp - kp.mean(axis=0, keepdims=True)
        area = ConvexHull(kp[:, :2]).volume
        area = np.sqrt(area)
        kp[:, :2] = kp[:, :2] / area
        return kp

    fa = face_alignment.FaceAlignment(face_alignment.LandmarksType._2D, flip_input=True,
                                      device='cpu' if cpu else 'cuda')
    kp_source = fa.get_landmarks(255 * source)[0]
    kp_source = normalize_kp(kp_source)
    norm  = float('inf')
    frame_num = 0
    for i, image in tqdm(enumerate(driving)):
        kp_driving = fa.get_landmarks(255 * image)[0]
        kp_driving = normalize_kp(kp_driving)
        new_norm = (np.abs(kp_source - kp_driving) ** 2).sum()
        if new_norm < norm:
            norm = new_norm
            frame_num = i
    return frame_num
```

```python
### 2. Readt rtsp stream

import cv2
import numpy as np
import os
os.environ["OPENCV_FFMPEG_CAPTURE_OPTIONS"] = "rtsp_transport;udp"
vcap = cv2.VideoCapture("rtsp://192.168.1.2:5554/camera", cv2.CAP_FFMPEG)
while(1):
ret, frame = vcap.read()
    if ret == False:
        print("Frame is empty")
        break;
    else:
        cv2.imshow('VIDEO', frame)
        cv2.waitKey(1)
```

### 2. Parameter expansion
```python
def func(arg1, arg2, arg3):
    print(arg1)
    print(arg2)
    print(arg3)

l = ['one', 'two', 'three']

func(*l)
# one
# two
# three

func(*['one', 'two', 'three'])
# one
# two
# three

t = ('one', 'two', 'three')

func(*t)
# one
# two
# three

func(*('one', 'two', 'three'))
# one
# two
# three

# When specifying a dictionary (dict) with ** as an argument, key will be expanded as an argument name and value as the value of the argument. Each element will be passed as keyword arguments.

def func(arg1, arg2, arg3):
    print(arg1)
    print(arg2)
    print(arg3)

d = {'arg1': 'one', 'arg2': 'two', 'arg3': 'three'}

func(**d)
# one
# two
# three

func(**{'arg1': 'one', 'arg2': 'two', 'arg3': 'three'})
# one
# two
# three

```


## Git

```
### Rebase // copy new commits from one branch to another 
(master) git rebase developement

```

