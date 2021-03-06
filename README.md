# review_labeled_video_and_extract

Python script allowing you to review a video labelled from a deep neural network (e.g., DeepLabCut) and created a new video with mislabeled frames that can be used to re-train and hopefully improve your model.

I often use DeepLabCut to train neural networks with the aim of tracking animals. The models are often very good most of the time but there are always mislabeled frames. These are often associated with relatively rare events that were not represented in the images used to train the network. 

The main goal of the script is to review your labeled video and create a new video of challenging rare events (possibly mislabeled frames). You can then use the "challenging" video to retrain your network and hopefully improve it.


## Instruction

1. Label some frames from videos using DeepLabCut.
1. First train your network using DeepLabCut as described on the DeepLabCut website.
2. Use your trained network to analyze and label a video. 
3. Use dlc_review_labeled_video to identify mislabeled frames and store them in a new video.
4. Add the new videos to your DeepLabCut project, extract some frames to be labeled from these new videos.
5. Label the new frames.
6. Retrain you network and hopefully get better results!

## Example case

I train a network with DeepLabCut. The object to track was a lever box (a lever for operant conditioning on wheels). After one iteration of training of 226500 iterations, and 90 % of the images in the training set, I got an error of 2.66 and 11.85 pixels for the train and validation set. 

The network had problems when the mouse or my hands was close to the lever. So I used review_labeled_video_and_extract to create a video containing only frames in which my hands or a mouse were close to the lever.

I retrain the network with 120 new frames from the videos of problematic frames and here were the results:
Results for 148000  training iterations: 90 1 train error: 2.95 pixels. Test error: 3.52  pixels.

The error on the test set seems to be lower on the second round. I then reviewed the labeled videos and they looked much better.


## Installation

You will need a python environment with openCV
```
 conda install -c conda-forge opencv=4.1.0
```
## Usage
To extract and save some frames.

Use "f", "b", "s" and "q" to move forward, backward, save frames and quit.

Do not close the window with our mouse. Use "q" to quit.
```
python ~/repo/review_labeled_video_and_extract/review_labeled_video_and_extract.py  mn5183-29072020-1513.arena_topDLC_resnet50_leverDetectorSep29shuffle1_226500_labeled.mp4 mn5183-29072020-1513.arena_top.avi selected_frames_mn5183-29072020-1513.arena_top.avi
```

