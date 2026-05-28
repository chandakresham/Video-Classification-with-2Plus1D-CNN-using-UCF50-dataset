<!-- Slide number: 1 -->
# Video CLASSIFICATION USING (2+1)D CNN 
### BY 
### Resham CHANDAK 
### Mtech. CSE (AI) 
### 202363004

### Notes:

# Index
1. Introduction
2. Convolutional Variants
3. 2D CNN
4. Full 3D CNN
5. (2+1)D CNN
6. Implementation
7. Conclusion
8. References

### Notes:

# Introduction
Video classification is a computer vision task that involves categorizing videos into predefined labels or classes based on their content.
A Video consists of series of frames displayed in rapid succession to create the illusion of motion.
Key components of video:
Frame: Basic building block of video
Frame Rate: No. of frames displayed per second (fps)
Spatial Dimension: Frame/image size
Temporal Dimension: Time Dimension
The applications of video classification include activity recognition, face gesture recognition and video recommendation systems.

### Notes:

# Convolutional Variants
3D Convolution
Captures spatiotemporal information by convolving over the spatial and temporal dimensions.
2D Convolution
Processes individual frames, ignoring temporal dynamics.
Mixed Convolution (MC)
Employs 3D convolutions in early layers and 2D convolutions in top layers to balance motion modeling and spatial reasoning.
(2+1)D Convolution
Factorizes 3D convolution into separate 2D spatial and 1D temporal convolutions, enhancing accuracy and optimization.

# CNN Variants

![](images/slide5_img1.jpg)
2D CNN
Mixed CNN
Full 3D CNN
(2+1)D CNN


# 2D CNN
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


# 3D CNN

![](images/slide7_img2.jpg)
3D CNN preserve temporal information and propagate it through the layers of the network.
Input size of 4D tensor = (3 x L x H x W)
      Filter size of 4D tensor = (N x t x d x d)
        where, t ->Temporal dimension.

Given, Kernel Size = (3 x 3 x 3)

      Spatial dimension = (1 x H x W) = (1 x 3 x 3)
      Temporal dimension = (t x 1 x 1) = (3 x 1 x 1)

Weight matrix of 3D CNN= t x H x W x Input channel x Output Channel
                                             = (27 * channels**2)

Here, Input Channel = Output channel = channels


# (2+1)D CNN
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

![](images/slide8_img3.jpg)


# (2+1)D CNN
Also, the spatiotemporal filters are factorized in (2+1)D CNN for the optimization, which reduces testing and training error. So, we can say (2+1)D CNN is much better than 3D CNN in case of performance.

![](images/slide9_img4.jpg)


# Implementation of VIDEO CLASSIFICATION USING (2+1)D CNN
Dataset: I have used UCF50 dataset in my implementation which contains 50 classes. UCF50 is an action recognition data set with 50 action categories, consisting of realistic videos taken from youtube. This data set is an extension of YouTube Action data set (UCF11) which has 11 action categories.
I have considered 10 classes from the above dataset. They are Baseball Pitch, Basketball, Bench Press, Biking, Billiards, Breast Stroke, Clean and Jerk, Diving , Drumming and Fencing.
First, I have load the dataset. I have kept the maximum no. of frames to be extracted as 10 from each video.
X shape = (1381, 10, 64, 64, 3)
      Y shape = (1381,)
I have splitted the dataset into 80% training, 10% validation and 10% testing datasets.


# Implementation of VIDEO CLASSIFICATION USING (2+1)D CNN
Model architecture:

![](images/slide11_img5.jpg)


# Implementation of VIDEO CLASSIFICATION USING (2+1)D CNN
Results:
1)   Plotting accuracy and loss

![](images/slides12_img6.jpg)
At 50 epochs,
Accuracy = 100%
Loss = 1.21%
Val Acc. = 92.75% Val Loss = 20.10%
Test Acc. = 96.40%
Test Loss = 11.30%


# Implementation of VIDEO CLASSIFICATION USING (2+1)D CNN
2)  Plotting confusion matrix

![](images/slide13_img7.jpg)

# Implementation of VIDEO CLASSIFICATION USING (2+1)D CNN
3) Calculating Precision and Recall for each class

4)  I have also saved the last 24 predicted videos captioned with predicted classes.

![](images/slide14_img8.jpg)

![](images/slide14_img9.jpg)


# Conclusion
In conclusion, we can say that (2+1)D CNN provide an efficient method of video classification which optimizes training and testing errors.
We can use this video classification in various tasks like human activity recognition, Real-time 3D pose classification, etc.

# References
Tran, Du, et al. "A closer look at spatiotemporal convolutions for action recognition." Proceedings of the IEEE conference on Computer Vision and Pattern Recognition. 2018.’
Video classification with a 3D convolutional neural network. (n.d.). TensorFlow. https://www.tensorflow.org/tutorials/video/video_classification