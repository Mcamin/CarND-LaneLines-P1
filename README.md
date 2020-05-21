# ** Project 1: Finding Lane Lines on the Road** 
[![Udacity - Self-Driving Car NanoDegree](https://s3.amazonaws.com/udacity-sdc/github/shield-carnd.svg)](http://www.udacity.com/drive)

<img src="examples/laneLines_thirdPass.jpg" width="480" alt="Combined Image" />

Overview
---

Identifying lanes of the road is very common task that human driver performs. This is important to keep the vehicle in the constraints of the lane. This is also very critical task for an autonomous vehicle to perform. And very simple Lane Detection pipeline is possible with simple Computer Vision techniques. 
This project is an implementation of a simple pipeline that can be used for simple lane detection using Python and OpenCV.


Instructions
---

## If you have already installed the [CarND Term1 Starter Kit](https://github.com/udacity/CarND-Term1-Starter-Kit/blob/master/README.md) you should be good to go!   If not, you should install the starter kit to get started on this project. ##

**Step 1:** Set up the [CarND Term1 Starter Kit](https://github.com/udacity/CarND-Term1-Starter-Kit/blob/master/README.md) if you haven't already.

**Step 2:** Open the code in a Jupyter Notebook

You will complete the project code in a Jupyter notebook.  If you are unfamiliar with Jupyter Notebooks, check out [Udacity's free course on Anaconda and Jupyter Notebooks](https://classroom.udacity.com/courses/ud1111) to get started.

Jupyter is an Ipython notebook where you can run blocks of code and see results interactively.  All the code for this project is contained in a Jupyter notebook. To start Jupyter in your browser, use terminal to navigate to your project directory and then run the following command at the terminal prompt (be sure you've activated your Python 3 carnd-term1 environment as described in the [CarND Term1 Starter Kit](https://github.com/udacity/CarND-Term1-Starter-Kit/blob/master/README.md) installation instructions!):

`> jupyter notebook`

A browser window will appear showing the contents of the current directory.  Click on the file called "P1.ipynb".  Another browser window will appear displaying the notebook.  Follow the instructions in the notebook to complete the project.  

**Step 3:** Complete the project and submit both the Ipython notebook and the project writeup

# Reflection 


## Pipeline
#### 1. Convert original image to grayscale.
#### 2. Apply Gaussian Blur with the chosen kernel.
#### 3. Apply canny Edge Detector (adjust the thresholds — trial and error) to obtain edges.
#### 4. Define the Region of Interest. This helps in weeding out unwanted edges detected by canny edge detector.
#### 5. Apply an image mask according to chosen set of region of interest coordinates.
#### 6. Retrieve Hough lines within a region of interest according to given set of hyperparameters.
#### 7. Fuse image containing those Hough lines with the original image

#### the draw_lines() function was modified in order to draw a single line on the left and right lanes:

* #### All obtained Hough lines were separated into two heaps denoting left and right lanes according to their slope ('m' in y = mx + b equation). As vertical axis increases from top to down, negative slopes go to the left heap, positive - to the right.
* #### Average slopes and intercepts (m's and b's in y=mx+b) within each heap. It yields data for 2 linear functions at maximum (one for left and one right lane).
* #### Compute coordinates of intersection with the button and the upper edges of the region of interest according to obtained functions.
* #### Draw those averaged lines across the full extent of the region of interest.


## Shortcomings
* #### Hough Lines based on straight lines do not work well for curved road/lane.
* ####Getting the right hyper parameters involve many trial-and-error. Also Region of Interest assumes that camera stays at same location and lanes are flat. So there is “guess” work or hard coding involved in deciding polygon vertices.
* #### There are many roads without lane markings where this approach won't work.
##Future Improvements
* #### Instead of using lines , it would be better to use higher degree curve that will be useful on curved road.
* #### Averaging lanes only is not be very good approach even when we used information from previous frames. may be weight average or some form of priority value might be a better approach.