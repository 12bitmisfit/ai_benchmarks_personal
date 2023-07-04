## Prompt:
Make a python script that uses opencv to iterate over a video file and save every frame in a folder with the same name as the video file's name.


## Model: Redmond Hermes 4 bit GPTQ
### Inference Speed 1x P40: 1.48 Tokens/second
### Ram Usage: 9516MiB
## output code:
```Python
import cv2
# Open the input video file
cap = cv2.VideoCapture('input_video.mp4')
# Get the width and height of the video
width = int(cap.get(3))
height = int(cap.get(4))
# Define the output directory for saving the extracted frames
output_directory = 'frames'
try:
    # Create the output directory if it doesn't exist yet
    os.makedirs(output_directory)
except FileExistsError:
    pass
# Iterate over each frame in the video
frame_number = 0
while True:
    ret, frame = cap.read()

    # Break out of the loop if there are no more frames left in the video
    if not ret:
        break

    # Save the current frame to disk
    filename = f'{output_directory}/frame_{str(frame_number).zfill(5)}.jpg'
    cv2.imwrite(filename, frame)

    # Increment the frame counter
    frame_number += 1

# Release the video capture object
cap.release()
print("Frames have been saved successfully.")
```

## Model: WizardCoder 4 bit GPTQ
### Inference Speed 1x P40: 5.54 Tokens/second
### Ram Usage: 9200MiB
## output code:
```Python
import cv2 
from os import path 

# Path where all videos are stored  
videos_path = "C:/Users/username/Videos"  

for root, dirs, files in sorted(os.walk(videos_path)):  
    # Iterate over each video 
    for file in files: 
        if not file.endswith('.mp4'):
            continue
        print("Processing Video:",file)

        try: 
            vidcap = cv2.VideoCapture(root + '/' + file)

            success,image = vidcap.read()

            while success: 
                imgname=str(frameCount)+".jpg"
                cv2.imwrite("./"+vidName+"/"+imgname, image)     # Save frame as JPEG file     

                success,image = vidcap.read()

                frameCount += 1

        except Exception as e: 
            print('Error processing:',e,'Skipping this video')

        finally: 
            vidcap.release()    # Release resources after use 

print("All Videos Processed")  
'''

## Model: WizardCoder 4 bit GPTQ
### Inference Speed 1x P40: 10.82 Tokens/second
### Ram Usage: 9500MiB
## output code:
```Python
import cv2
import os

def main():
    video_path = 'video.mp4'
    video_name = os.path.splitext(os.path.basename(video_path))[0]
    video_frames_path = os.path.join(os.path.dirname(video_path), video_name)
    if not os.path.exists(video_frames_path):
        os.makedirs(video_frames_path)
    cap = cv2.VideoCapture(video_path)
    while(cap.isOpened()):
        ret, frame = cap.read()
        if ret == True:
            cv2.imwrite(os.path.join(video_frames_path, '{:04d}.jpg'.format(cap.get(cv2.CAP_PROP_POS_FRAMES))), frame)
        else:
            break
    cap.release()
    cv2.destroyAllWindows()

if __name__ == '__main__':
    main()
'''

## Model: ChatGPT 3.5 Turbo 0613
### Inference Speed: Unable to measure easily, but very quick. Probably 25+ tokens/second
## output code:
```Python
import cv2
import os

def save_frames(video_path, output_dir):
    # Create output directory if it doesn't exist
    os.makedirs(output_dir, exist_ok=True)

    # Open the video file
    video = cv2.VideoCapture(video_path)

    # Get the base name of the video file
    video_name = os.path.basename(video_path)

    # Remove file extension from video name
    video_name = os.path.splitext(video_name)[0]

    # Initialize frame counter
    frame_count = 0

    while True:
        # Read the next frame
        ret, frame = video.read()

        # Break the loop if no more frames are available
        if not ret:
            break

        # Save the frame as an image file
        frame_path = os.path.join(output_dir, f"{video_name}_{frame_count:06d}.jpg")
        cv2.imwrite(frame_path, frame)

        # Increment frame counter
        frame_count += 1

    # Release the video file
    video.release()

    print(f"Saved {frame_count} frames in '{output_dir}'")

# Example usage
video_path = "path/to/video.mp4"
output_dir = "path/to/output/folder"

save_frames(video_path, output_dir)
```

## Model: ChatGPT 4 0613
### Inference Speed: Unable to measure easily, but quite reasonable, probably around 10 tokens/second
## output code:
```Python
import cv2
import os

# Specify your video file's path here
video_file = "/path/to/your/video.mp4"

# Get the video file's base name (e.g. "video.mp4")
base_name = os.path.basename(video_file)

# Get the name without the extension (e.g. "video")
name_without_ext = os.path.splitext(base_name)[0]

# Make a directory with the same name as the video file
if not os.path.exists(name_without_ext):
    os.makedirs(name_without_ext)

# Open the video file
cap = cv2.VideoCapture(video_file)

# Initialize frame count
frame_count = 0

while True:
    # Read the next frame
    ret, frame = cap.read()

    # If the frame was read correctly ret is True
    if not ret:
        break

    # Save the frame as an image file
    img_file = os.path.join(name_without_ext, f"frame_{frame_count}.png")
    cv2.imwrite(img_file, frame)

    frame_count += 1

# Release the video file
cap.release()

print(f"Saved {frame_count} frames to folder {name_without_ext}")
```
