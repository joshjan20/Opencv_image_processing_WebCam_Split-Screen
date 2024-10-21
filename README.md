```markdown
# Webcam Video Split-Screen with OpenCV

This Python project captures video from your webcam using OpenCV and creates a split-screen effect. The video feed is resized and rotated, then displayed in four quadrants of the window, creating a mirrored and rotated display of the webcam feed.

## Features

- **Real-Time Video Capture**: Captures video from your default webcam using OpenCV.
- **Resizing and Rotating**: The captured video frame is resized to 50% of its original size, and some parts of the frame are rotated by 180 degrees.
- **Quadrant Display**: The output is a 2x2 grid where each quadrant displays either the original resized frame or a rotated version of it.

## Requirements

- Python 3.x
- OpenCV
- NumPy

You can install the required packages using `pip`:

```bash
pip install opencv-python numpy
```

## How to Run

1. Clone this repository or download the script.
2. Ensure your webcam is connected or available for capture.
3. Run the script using Python:

```bash
python main.py
```

4. To quit the program, press the **'q'** key.

## Code Breakdown

### Video Capture and Processing

```python
import numpy as np
import cv2

cap = cv2.VideoCapture(0)

while True:
    ret, frame = cap.read()
    width = int(cap.get(3))
    height = int(cap.get(4))

    image = np.zeros(frame.shape, np.uint8)
    smaller_frame = cv2.resize(frame, (0, 0), fx=0.5, fy=0.5)
    image[:height//2, :width//2] = cv2.rotate(smaller_frame, cv2.ROTATE_180)
    image[height//2:, :width//2] = smaller_frame
    image[:height//2, width//2:] = cv2.rotate(smaller_frame, cv2.ROTATE_180)
    image[height//2:, width//2:] = smaller_frame

    cv2.imshow('frame', image)

    if cv2.waitKey(1) == ord('q'):
        break

cap.release()
cv2.destroyAllWindows()
```

### Explanation

1. **Webcam Capture**: 
   - The script starts by accessing the default webcam using `cv2.VideoCapture(0)`. It captures each frame in a loop.
   
2. **Frame Processing**:
   - Each frame is resized to 50% of its original size using `cv2.resize()`.
   - The smaller frame is placed into four quadrants of a new image. In two quadrants, the smaller frame is rotated by 180 degrees using `cv2.rotate()`.

3. **Display Output**:
   - The processed image is displayed in real-time using `cv2.imshow()`. The window is continuously updated with new frames.
   
4. **Exit the Program**:
   - Press the **'q'** key to exit the video capture and close the window.

## Example Output

- The output window shows the real-time video feed divided into four quadrants:
  - Top-left and top-right quadrants display the frame rotated 180 degrees.
  - Bottom-left and bottom-right quadrants display the original frame, resized.

## License

This project is licensed under the MIT License - see the [LICENSE](LICENSE) file for details.
```
