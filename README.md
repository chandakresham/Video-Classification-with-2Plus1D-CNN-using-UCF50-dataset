# Slide 1

Video CLASSIFICATION USING (2+1)D CNNBY Resham CHANDAKMtech. CSE (AI)202363004

# Slide 2

Index

Introduction
Convolutional Variants
2D CNN
Full 3D CNN
(2+1)D CNN 
Implementation
Conclusion
References

2

# Slide 3

Introduction

Video classification is a computer vision task that involves categorizing videos into predefined labels or classes based on their content. 
A Video consists of series of frames displayed in rapid succession to create the illusion of motion.
Key components of video:
Frame: Basic building block of video
Frame Rate: No. of frames displayed per second (fps)
Spatial Dimension: Frame/image size
Temporal Dimension: Time Dimension
The applications of video classification include activity recognition, face gesture recognition and video recommendation systems.

3

# Slide 4

Convolutional Variants

2D Convolution 
Processes individual frames, ignoring temporal dynamics.

3D Convolution 
Captures spatiotemporal information by convolving over the spatial and temporal dimensions.

4

Mixed Convolution (MC) 
Employs 3D convolutions in early layers and 2D convolutions in top layers to balance motion modeling and spatial reasoning.

(2+1)D Convolution 
Factorizes 3D convolution into separate 2D spatial and 1D temporal convolutions, enhancing accuracy and optimization.

# Slide 5

CNN Variants

5

2D CNN

Mixed CNN

Full 3D CNN

(2+1)D CNN

# Slide 6

2D CNN

2D CNN ignores temporal ordering and treats the total frames of the video analogously to channels.
Thus, we need to convert 4D tensor to 3D tensor.

	Input size of 4D tensor = (3 x L x H x W) 
	Input size of 3D tensor = (N x H x W) =N x d x d

                where,
                              L-> No. of frames
                              H x W -> Spatial dimensions of the frame 
  	              N -> No. of features
                              d -> Spatial width and height
Filter size is 3D, but it is convolved in 2D over the spatial dimensions of the preceding convolution layer.
So, no temporal modeling is performed in the convolutional layers and the global spatiotemporal pooling layer at the top simply fuses the information extracted independently from the L frames.

6

# Slide 7

3D CNN

3D CNN preserve temporal information and propagate it through the layers of the network.
Input size of 4D tensor = (3 x L x H x W) 
      Filter size of 4D tensor = (N x t x d x d)
        where, t ->Temporal dimension.

Given, Kernel Size = (3 x 3 x 3)

      Spatial dimension = (1 x H x W) = (1 x 3 x 3)
      Temporal dimension = (t x 1 x 1) = (3 x 1 x 1)

7

Weight matrix of 3D CNN= t x H x W x Input channel x Output Channel
                                             = (27 * channels**2)

Here, Input Channel = Output channel = channels

# Slide 8

(2+1)D CNN

The (2+1)D convolution allows for the decomposition of the spatial and temporal dimensions.
Shape of Spatial convolution = (1, d, d)  and  Shape of Temporal convolution = (t, 1, 1)
      Spatial Filter size = (Ni-1 x 1 x d x d) and Temporal Filter size = (Mi x t x 1 x 1)
      Here, i-1 and i -> Previous and Current layers resp.
                Ni-1 and Ni -> Input and output channels resp.
                Mi -> Intermediate channel dimension between the spatial and temporal convolutions


I have chosen Mi to make the parameters of (2+1)D CNN and 3D CNN equal.
Kernel size = (3,3,3)
      Weight matrix = (9 * channels**2) + (3 * channels**2)   

      This is much less than half as many as the full 3D convolution.

8

# Slide 9

(2+1)D CNN

Also, the spatiotemporal filters are factorized in (2+1)D CNN for the optimization, which reduces testing and training error. So, we can say (2+1)D CNN is much better than 3D CNN in case of performance.

9

# Slide 10

Implementation of VIDEO CLASSIFICATION USING (2+1)D CNN

Dataset: I have used UCF50 dataset in my implementation which contains 50 classes. UCF50 is an action recognition data set with 50 action categories, consisting of realistic videos taken from youtube. This data set is an extension of YouTube Action data set (UCF11) which has 11 action categories. 
I have considered 10 classes from the above dataset. They are Baseball Pitch, Basketball, Bench Press, Biking, Billiards, Breast Stroke, Clean and Jerk, Diving , Drumming and Fencing.
First, I have load the dataset. I have kept the maximum no. of frames to be extracted as 10 from each video.
X shape = (1381, 10, 64, 64, 3)
      Y shape = (1381,) 
I have splitted the dataset into 80% training, 10% validation and 10% testing datasets.

10

# Slide 11

Implementation of VIDEO CLASSIFICATION USING (2+1)D CNN

Model architecture:

11

# Slide 12

Implementation of VIDEO CLASSIFICATION USING (2+1)D CNN

Results:
1)   Plotting accuracy and loss

12

At 50 epochs,
Accuracy = 100%
Loss = 1.21%
Val Acc. = 92.75% Val Loss = 20.10%

Test Acc. = 96.40%
Test Loss = 11.30%

# Slide 13

Implementation of VIDEO CLASSIFICATION USING (2+1)D CNN

2)  Plotting confusion matrix

13

# Slide 14

Implementation of VIDEO CLASSIFICATION USING (2+1)D CNN

3) Calculating Precision and Recall for each class



       



4)  I have also saved the last 24 predicted videos captioned with predicted classes.

14

# Slide 15

Conclusion

In conclusion, we can say that (2+1)D CNN provide an efficient method of video classification which optimizes training and testing errors.
We can use this video classification in various tasks like human activity recognition, Real-time 3D pose classification, etc.

15

# Slide 16

References

Tran, Du, et al. "A closer look at spatiotemporal convolutions for action recognition." Proceedings of the IEEE conference on Computer Vision and Pattern Recognition. 2018.’
Video classification with a 3D convolutional neural network. (n.d.). TensorFlow. https://www.tensorflow.org/tutorials/video/video_classification

16

