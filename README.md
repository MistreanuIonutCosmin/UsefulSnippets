# UsefulSnippets




## Nvidia
[Nvidia](./nvidia/README.md)


## Pytorch Snippets
[Pytorch](./pytorch/README.md)

## Bash
[Bash](./bash/README.md)


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
ffmpeg -i LostInTranslation.mkv -codec copy LostInTranslation.mp4
ffmpeg -i video.mp4 img%04.png // split in frames with lossless convertion 

ffmpeg -i input.avi -vf scale=320:240 output.avi

ffmpeg -i Video.mp4 -filter_complex \
"[0:v]trim=start=0:end=20,setpts=PTS-STARTPTS[a]; \
 [0:v]trim=start=27:end=90,setpts=PTS-STARTPTS[b]; \
 [0:v]trim=start=95:end=169,setpts=PTS-STARTPTS[c]; \
 [a][b][c]concat=n=3[out1]" -map [out1] VideoTrimed.mp4
 
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
### Revion - a tracked state of project. Every revion has it's own sha-1 hash

### Rebase // copy new commits from one branch to another 
(master) git rebase developement

### Lightweight tag // a user friendly name pointer to a commit 
git tag awesome_tag_name

(master) git rebase developement

### Remotes 
There is nothing special about remotes. Same revisions, with their own unique hashes are stored in your local git repository when you fetch changes. References to remote branches are automatically created, based on name of remote branch, and prepended with the name of remote.
```

