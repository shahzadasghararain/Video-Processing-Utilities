**Video Processing Utilities**
This repository contains Python scripts for processing video files. The provided utilities include converting .ts files to .mp4 format, creating video previews, and generating thumbnails. These scripts leverage ffmpeg and moviepy libraries for media processing.

**Features**
Convert .ts files to .mp4 format.
Create previews from video files.
Generate thumbnails from video frames.
Batch processing of videos in specified directories.
Requirements
Python 3.6 or higher
ffmpeg installed and available in the system's PATH
ffmpeg-python library
moviepy library
Pillow library
**Installation**
**Install Python 3.6+:** Ensure you have Python 3.6 or higher installed on your system. You can download it from the official Python website.

**Install ffmpeg**: Download and install ffmpeg from the official website and make sure it is available in your system's PATH.

**Install the required Python libraries:**

bash
Copy code
pip install ffmpeg-python moviepy Pillow
Usage
**Clone the repository:**

bash
Copy code
git clone https://github.com/yourusername/video-processing-utilities.git
cd video-processing-utilities
Prepare your directories:

Create necessary directories such as previews and thumbnails in the same directory as the scripts.
Place your video files in the specified input directories.
Run the scripts:

For converting .ts files to .mp4:

bash
Copy code
python app3.py
The script will process all .ts files in the previews directory and save the converted .mp4 files in the converted_previews directory.

For creating previews and thumbnails:

bash
Copy code
python app2.py
This script will create previews and thumbnails for video files in the specified input directory.

For creating previews only:

bash
Copy code
python app.py
This script will create previews for video files in the specified input directory.

Script Details
app3.py
This script converts .ts files to .mp4 format using ffmpeg.

python
Copy code
import os
import ffmpeg

def convert_ts_to_mp4(input_path, output_path):
    try:
        ffmpeg.input(input_path).output(output_path, vcodec='libx264', acodec='aac').run(overwrite_output=True)
        print(f"Converted {input_path} to {output_path}")
    except Exception as e:
        print(f"Failed to convert {input_path}: {e}")

def convert_previews(preview_folder, output_folder):
    os.makedirs(output_folder, exist_ok=True)
    
    for filename in os.listdir(preview_folder):
        if filename.endswith(".ts"):
            input_path = os.path.join(preview_folder, filename)
            output_filename = os.path.splitext(filename)[0] + ".mp4"
            output_path = os.path.join(output_folder, output_filename)
            
            convert_ts_to_mp4(input_path, output_path)

current_directory = os.path.dirname(os.path.abspath(__file__))
preview_folder = os.path.join(current_directory, "previews")
output_folder = os.path.join(current_directory, "converted_previews")

convert_previews(preview_folder, output_folder)
app2.py
This script creates video previews and thumbnails using moviepy and Pillow.

python
Copy code
import os
from moviepy.editor import VideoFileClip
from PIL import Image

def create_preview(video_path, output_path, preview_duration=10):
    video = VideoFileClip(video_path)
    preview_end_time = min(preview_duration, video.duration)
    preview_clip = video.subclip(0, preview_end_time)
    preview_clip.write_videofile(output_path, codec="libx264", audio_codec="aac")

def create_thumbnail(video_path, output_path, size=(600, 400), thumbnail_time=10):
    video = VideoFileClip(video_path)
    thumbnail_time = min(thumbnail_time, video.duration)
    frame = video.get_frame(thumbnail_time)
    image = Image.fromarray(frame)
    image = image.resize(size, Image.ANTIALIAS)
    image.save(output_path)

def process_videos(input_folder, preview_folder, thumbnail_folder, preview_duration=24, thumbnail_time=24):
    os.makedirs(preview_folder, exist_ok=True)
    os.makedirs(thumbnail_folder, exist_ok=True)
    
    for filename in os.listdir(input_folder):
        if filename.endswith((".mp4", ".avi", ".mov", ".mkv", ".ts")):
            input_path = os.path.join(input_folder, filename)
            preview_output_path = os.path.join(preview_folder, f"preview_{filename}")
            thumbnail_output_path = os.path.join(thumbnail_folder, f"thumbnail_{os.path.splitext(filename)[0]}.jpg")
            
            try:
                create_preview(input_path, preview_output_path, preview_duration)
                print(f"Preview created for {filename}")
                
                create_thumbnail(input_path, thumbnail_output_path, size=(600, 400), thumbnail_time=thumbnail_time)
                print(f"Thumbnail created for {filename}")
            except Exception as e:
                print(f"Failed to process {filename}: {e}")

current_directory = os.path.dirname(os.path.abspath(__file__))
input_folder = current_directory
preview_folder = os.path.join(current_directory, "previews")
thumbnail_folder = os.path.join(current_directory, "thumbnails")

process_videos(input_folder, preview_folder, thumbnail_folder)
app.py
This script creates video previews using moviepy.

python
Copy code
import os
from moviepy.editor import VideoFileClip

def create_preview(video_path, output_path, preview_duration=10):
    video = VideoFileClip(video_path)
    preview_end_time = min(preview_duration, video.duration)
    preview_clip = video.subclip(0, preview_end_time)
    preview_clip.write_videofile(output_path, codec="libx264", audio_codec="aac")

def process_videos(input_folder, output_folder, preview_duration=10):
    os.makedirs(output_folder, exist_ok=True)
    
    for filename in os.listdir(input_folder):
        if filename.endswith((".mp4", ".avi", ".mov", ".ts")):
            input_path = os.path.join(input_folder, filename)
            output_path = os.path.join(output_folder, f"preview_{filename}")
            
            try:
                create_preview(input_path, output_path, preview_duration)
                print(f"Preview created for {filename}")
            except Exception as e:
                print(f"Failed to create preview for {filename}: {e}")

current_directory = os.path.dirname(os.path.abspath(__file__))
input_folder = current_directory
output_folder = os.path.join(current_directory, "previews")

process_videos(input_folder, output_folder)
Contributing
If you would like to contribute to this project, please fork the repository and submit a pull request. We welcome bug reports, feature requests, and other contributions.

License
This project is licensed under the MIT License. See the LICENSE file for details.

Acknowledgements
This project uses the ffmpeg, ffmpeg-python, moviepy, and Pillow libraries for media processing.

Feel free to customize the repository URL, add any additional sections as necessary, and include a link to the LICENSE file if you decide to add one.

Description (optional)
ChatGPT
Video Processing Utilities
This repository contains Python scripts for processing video files. The provided utilities include converting .ts files to .mp4 format, creating video previews, and generating thumbnails. These scripts leverage ffmpeg and moviepy libraries for media processing.

Features
Convert .ts files to .mp4 format.
Create previews from video files.
Generate thumbnails from video frames.
Batch processing of videos in specified directories.
Requirements
Python 3.6 or higher
ffmpeg installed and available in the system's PATH
ffmpeg-python library
moviepy library
Pillow library
Installation
Install Python 3.6+: Ensure you have Python 3.6 or higher installed on your system. You can download it from the official Python website.

Install ffmpeg: Download and install ffmpeg from the official website and make sure it is available in your system's PATH.

Install the required Python libraries:

bash
Copy code
pip install ffmpeg-python moviepy Pillow
Usage
Clone the repository:

bash
Copy code
git clone https://github.com/yourusername/video-processing-utilities.git
cd video-processing-utilities
Prepare your directories:

Create necessary directories such as previews and thumbnails in the same directory as the scripts.
Place your video files in the specified input directories.
Run the scripts:

For converting .ts files to .mp4:

bash
Copy code
python app3.py
The script will process all .ts files in the previews directory and save the converted .mp4 files in the converted_previews directory.

For creating previews and thumbnails:

bash
Copy code
python app2.py
This script will create previews and thumbnails for video files in the specified input directory.

For creating previews only:

bash
Copy code
python app.py
This script will create previews for video files in the specified input directory.

Script Details
app3.py
This script converts .ts files to .mp4 format using ffmpeg.

python
Copy code
import os
import ffmpeg

def convert_ts_to_mp4(input_path, output_path):
    try:
        ffmpeg.input(input_path).output(output_path, vcodec='libx264', acodec='aac').run(overwrite_output=True)
        print(f"Converted {input_path} to {output_path}")
    except Exception as e:
        print(f"Failed to convert {input_path}: {e}")

def convert_previews(preview_folder, output_folder):
    os.makedirs(output_folder, exist_ok=True)
    
    for filename in os.listdir(preview_folder):
        if filename.endswith(".ts"):
            input_path = os.path.join(preview_folder, filename)
            output_filename = os.path.splitext(filename)[0] + ".mp4"
            output_path = os.path.join(output_folder, output_filename)
            
            convert_ts_to_mp4(input_path, output_path)

current_directory = os.path.dirname(os.path.abspath(__file__))
preview_folder = os.path.join(current_directory, "previews")
output_folder = os.path.join(current_directory, "converted_previews")

convert_previews(preview_folder, output_folder)
app2.py
This script creates video previews and thumbnails using moviepy and Pillow.

python
Copy code
import os
from moviepy.editor import VideoFileClip
from PIL import Image

def create_preview(video_path, output_path, preview_duration=10):
    video = VideoFileClip(video_path)
    preview_end_time = min(preview_duration, video.duration)
    preview_clip = video.subclip(0, preview_end_time)
    preview_clip.write_videofile(output_path, codec="libx264", audio_codec="aac")

def create_thumbnail(video_path, output_path, size=(600, 400), thumbnail_time=10):
    video = VideoFileClip(video_path)
    thumbnail_time = min(thumbnail_time, video.duration)
    frame = video.get_frame(thumbnail_time)
    image = Image.fromarray(frame)
    image = image.resize(size, Image.ANTIALIAS)
    image.save(output_path)

def process_videos(input_folder, preview_folder, thumbnail_folder, preview_duration=24, thumbnail_time=24):
    os.makedirs(preview_folder, exist_ok=True)
    os.makedirs(thumbnail_folder, exist_ok=True)
    
    for filename in os.listdir(input_folder):
        if filename.endswith((".mp4", ".avi", ".mov", ".mkv", ".ts")):
            input_path = os.path.join(input_folder, filename)
            preview_output_path = os.path.join(preview_folder, f"preview_{filename}")
            thumbnail_output_path = os.path.join(thumbnail_folder, f"thumbnail_{os.path.splitext(filename)[0]}.jpg")
            
            try:
                create_preview(input_path, preview_output_path, preview_duration)
                print(f"Preview created for {filename}")
                
                create_thumbnail(input_path, thumbnail_output_path, size=(600, 400), thumbnail_time=thumbnail_time)
                print(f"Thumbnail created for {filename}")
            except Exception as e:
                print(f"Failed to process {filename}: {e}")

current_directory = os.path.dirname(os.path.abspath(__file__))
input_folder = current_directory
preview_folder = os.path.join(current_directory, "previews")
thumbnail_folder = os.path.join(current_directory, "thumbnails")

process_videos(input_folder, preview_folder, thumbnail_folder)
app.py
This script creates video previews using moviepy.

python
Copy code
import os
from moviepy.editor import VideoFileClip

def create_preview(video_path, output_path, preview_duration=10):
    video = VideoFileClip(video_path)
    preview_end_time = min(preview_duration, video.duration)
    preview_clip = video.subclip(0, preview_end_time)
    preview_clip.write_videofile(output_path, codec="libx264", audio_codec="aac")

def process_videos(input_folder, output_folder, preview_duration=10):
    os.makedirs(output_folder, exist_ok=True)
    
    for filename in os.listdir(input_folder):
        if filename.endswith((".mp4", ".avi", ".mov", ".ts")):
            input_path = os.path.join(input_folder, filename)
            output_path = os.path.join(output_folder, f"preview_{filename}")
            
            try:
                create_preview(input_path, output_path, preview_duration)
                print(f"Preview created for {filename}")
            except Exception as e:
                print(f"Failed to create preview for {filename}: {e}")

current_directory = os.path.dirname(os.path.abspath(__file__))
input_folder = current_directory
output_folder = os.path.join(current_directory, "previews")

process_videos(input_folder, output_folder)
Contributing
If you would like to contribute to this project, please fork the repository and submit a pull request. We welcome bug reports, feature requests, and other contributions.

License
This project is licensed under the MIT License. See the LICENSE file for details.

Acknowledgements
This project uses the ffmpeg, ffmpeg-python, moviepy, and Pillow libraries for media processing.
Shahzad Asghar (Shahzad.cdcu@gmail.com)
