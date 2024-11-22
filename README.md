# Extract Images from Video

This project extracts unique frames from a video file using perceptual hashing to detect and avoid saving duplicate frames. The extracted frames are saved as images in a specified output directory.

## Requirements

- Python 3.10 or higher
- OpenCV
- ImageHash
- Pillow

## Installation

To install the required packages, run the following commands:

```bash
pip install opencv-python
pip install imagehash
pip install pillow
```

### Usage
- Place your video file in the project directory and update the ```video_path``` variable in the ```main``` function with the path to your video file.
- Update the ```output_dir``` variable in the ```main``` function with the desired output directory for the extracted frames.
- Run the ```extract.ipynb``` notebook or convert it to a Python script and run it.

### Example
```python
def main():
    # Hardcoded paths
    video_path = "./Solution.mp4"  # Replace with the path to your video
    output_dir = "./output"  # Replace with your desired output folder

    # Create output directory if it doesn't exist
    os.makedirs(output_dir, exist_ok=True)

    print("\nProcessing video...\n")
    processor = FrameProcessor(video_path, output_dir)
    extracted_count = processor.extract_frames()

    if extracted_count > 0:
        print(f"\nExtraction complete. {extracted_count} unique frames saved to '{output_dir}'.")
    else:
        print("No unique frames were extracted.")

if __name__ == "__main__":
    main()
```

## Classes and Functions

### FrameProcessor
A class to process video frames and extract unique frames.

**__init__(self, video_path, output_dir)**
* Initializes the `FrameProcessor` with the video path and output directory.
* **Parameters:**
  * `video_path`: Path to the video file.
  * `output_dir`: Directory to save the extracted frames.

**get_frame_phash(self, frame)**
* Computes the perceptual hash of a grayscale frame.
* **Parameters:**
  * `frame`: The video frame to compute the hash for.
* **Returns:** The perceptual hash of the frame.

**save_if_unique(self, frame, frame_count)**
* Saves the frame if it is unique compared to previous frames.
* **Parameters:**
  * `frame`: The video frame to save.
  * `frame_count`: The current frame count.
* **Returns:** The updated frame count.

**extract_frames(self)**
* Processes the video to extract unique frames.
* **Returns:** The number of unique frames extracted.

**print_progress(percentage)**
* Prints a progress bar for frame extraction.
* **Parameters:**
  * `percentage`: The current progress percentage.

### Constants
**SIMILARITY_TOLERANCE**
* Threshold for duplicate detection. Frames with a perceptual hash difference less than or equal to this value are considered duplicates.