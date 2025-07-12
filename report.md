# Methodology Report: Player Re-Identification using YOLOv8 and Deep SORT

## 1. Approach and Methodology

This project focuses on tracking and re-identifying players in a sports video using deep learning and tracking algorithms. The system combines:

- **YOLOv8** for real-time object detection
- **Deep SORT** for maintaining consistent object identities across video frames

The goal was to develop a robust pipeline that could not only detect players but also consistently assign them unique identifiers, even in the presence of occlusion or brief exits from the camera frame.

### Workflow

1. **Detection**: Each video frame is processed using a custom-trained YOLOv8 model (`best.pt`) to detect players.
2. **Filtering**: Only the detections corresponding to class ID `2` (representing players) are retained.
3. **Tracking**: The bounding boxes and confidence scores are passed to the Deep SORT tracker, which assigns unique IDs and updates them across frames.
4. **Handling Occlusion**: The Deep SORT parameter `max_age` is set to 300 (equivalent to 10 seconds at 30 FPS), allowing for temporary disappearance of players without loss of identity.
5. **Visualization**: OpenCV is used to draw bounding boxes and ID labels on the video in real time.

## 2. Techniques and Outcomes

| Technique                          | Purpose                                             | Outcome                                                             |
|-----------------------------------|-----------------------------------------------------|----------------------------------------------------------------------|
| YOLOv8 (custom-trained)           | Detect players in each frame                        | Provided fast and accurate detection results                        |
| Deep SORT                         | Assign and maintain player identities               | Successfully tracked players across frames, even with partial occlusion |
| Adjusted `max_age` parameter      | Allow players to leave and re-enter the frame       | Maintained consistent IDs for players after brief disappearance     |
| OpenCV Visualization              | Real-time tracking feedback                         | Helped verify the effectiveness of detection and tracking visually  |
| Google Drive Model Hosting        | Handle large model file (>100MB)                    | Solved GitHub upload limitation by using an external download link  |

## 3. Challenges Encountered

- **Model Size Limitations**: The trained YOLOv8 model (`best.pt`) exceeded GitHub’s file size limits. This was resolved by uploading the model to Google Drive and including a link in the README file.
  
- **Identity Reassignment**: With default settings, Deep SORT frequently reassigned new IDs when players briefly exited the frame. This was addressed by increasing the `max_age` parameter, allowing for temporary occlusion.

- **Performance on Lower-End Systems**: Real-time tracking performance dropped when using high-resolution videos on machines without GPUs. This may require further optimization or hardware acceleration.

- **Class Filtering**: Ensuring that the correct class ID (2 for players) was being used required validation against the YOLOv8 training setup.

## 4. Future Improvements

While the core system works well for the basic tracking task, several enhancements can be considered:

- **Video Output Saving**: Add functionality to save the annotated video to disk for later analysis.
- **Exporting Logs**: Output tracking data (coordinates, IDs, timestamps) to CSV or JSON format for post-processing or analytics.
- **Multiple Object Tracking**: Extend tracking to include other relevant entities like referees or balls.
- **GPU Acceleration**: Enable GPU support for faster inference and improved performance on large videos.
- **Improved Tracking Algorithms**: Experiment with alternative trackers such as OC-SORT or ByteTrack, which may offer better results in crowded or dynamic environments.

## 5. Conclusion

This project successfully integrates YOLOv8 and Deep SORT into a pipeline for real-time player tracking and re-identification. By adjusting tracking parameters and handling model deployment issues, we created a system that performs reliably under common video challenges such as occlusion and frame exits. With additional features and refinements, the system can be further extended to support broader use cases in sports analytics or surveillance.
