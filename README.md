# Sudoku-Grabber
This is a self project aimed at using Computer Vision to detect and solve sudokus from images. This was done by me during Summer 2020, with aim of understanding the application Machine Learning.

The structure of the project was as follows - 
1. First train a convolutional neural network on the MNIST dataset for handwritten digit recognition. This was done using Keras.
2. Segment the sudoku in images. This was a hard task and employed various functions in OpenCV. This is described in detail later
3. Solving the recognized sudoku. This was done by a backtracking algorithm written in Python.

## Training the Neural Network
The neural network was trained on the MNIST dataset. This is a pretty standard ML problem that almost all the beginners do. Reference was mainly taken from [here](https://machinelearningmastery.com/how-to-develop-a-convolutional-neural-network-from-scratch-for-mnist-handwritten-digit-classification/), although a lot of other resources on the net were used, and a bit of experimentation as well. 

## Segmenting the Sudoku in Images
The test image was <br> <img height="300" width="300" src="screenshots/sudoku.jpg"><br>
First, the Gaussian Blur was applied to smoothen the image. The image after this is given by <br><img height="300" width="300" src="screenshots/blur.png"><br>
The next step involved differentiating the light and dark parts of the image. This was done to recognise the numbers and the boundary lines of the sudoku as distinct from the background region. This was done by thresholding the image. <br><img height="300" width="300" src="screenshots/thresholded.png"><br>

To reduce the noise further in the image, it was eroded. What this basically did was replace the regions where there is very less "0" valued pixels into pixel values of "255".<br><img height="300" width="300" src="screenshots/eroded.png"><br>

Now, to recognise where the sudoku lies, the contours of the image were found which are basically the continuous curves joining the points with same pixel value. The result is shown on a fully black image with the white area representing where the image lied. <br> <img height="300" width="300" src="screenshots/mask.png"><br>

The corner points coordinates were found the image was cropped using the `getPerspectiveTransform` function in OpenCV.<br><img height="300" width="300" src="screenshots/cropped.png"><br>
