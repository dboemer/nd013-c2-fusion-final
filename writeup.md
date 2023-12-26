# Final Project: Sensor Fusion and Object Tracking

This is the final project of the section "Sensor Fusion and Tracking" in [Udacity's Nanodegree Program "Self Driving Car Engineer"](https://www.udacity.com/course/self-driving-car-engineer-nanodegree--nd0013).


## 1. Summary

### 1.1. Write a short recap of the four tracking steps and what you implemented there (filter, track management, association, camera fusion). Which results did you achieve? Which part of the project was most difficult for you to complete, and why?

The four tracking steps, their implementation and the results are explained [below](#2-tracking) in sections 2.-5.  The main difficulty was getting familiar with the codebase, in particular, with the definition of specific variables/matrices, since the algorithms were already very well explained in the course and they could therefore be easily implemented.


### 1.2. Do you see any benefits in camera-lidar fusion compared to lidar-only tracking (in theory and in your concrete results)?

In theory, various sensors used for object detection come with distinct advantages and drawbacks. For instance:

1. 3D LiDAR: This sensor excels in providing highly accurate distance measurements for vehicles. It compensates for the loss of distance precision in camera measurements, which result from the 2D projection of the 3D world.

2. Camera: While lacking the depth accuracy of LiDAR, a camera stands out as the sole sensor capable of capturing rich textured and color-based information. This includes essential details such as speed signs, traffic lights, and more. LiDAR, in contrast, is usually unable to offer color and texture information.

In practice, the average RMSE was reduced after adding the additional camera measurements to the lidar measurements.


### 1.3. Which challenges will a sensor fusion system face in real-life scenarios? Did you see any of these challenges in the project?

A sensor fusion system encounters significant challenges in real-world scenarios, and this project identifies and addresses these challenges across various dimensions:

1. Visibility Discrepancies: Each sensor within the fusion system has a distinct field of view (FOV), leading to fluctuating track scores. Notably, the front camera sensor exhibits a narrower FOV compared to LiDAR. To address this, a method called "in_fov" is implemented to assess whether tracks updated by LiDAR measurements fall outside the FOV of the front camera, ensuring comprehensive coverage and minimizing tracking uncertainties.

2. Sensor Performance: Adverse environmental conditions, such as rain, heavy fog, and darkness, can severely impact the performance of LiDAR and camera sensors. To mitigate these effects, the project explores the incorporation of an additional sensor, such as radar, to enhance the system's capability in extreme weather conditions.

3. Algorithmic Complexity: The complexity of algorithms, particularly in data association, escalates with an increasing number of detected vehicles. To streamline the data association process and facilitate prompt tracking, the project adopts a gating method. This method effectively eliminates improbable associations between detected tracks and measurements, optimizing the overall efficiency of the system.

4. Process Noise: The variation in process noise across different scenarios, such as high acceleration during emergencies and low acceleration on highways, poses a challenge. Moreover, the system's parameterization for noise lacks robust support from real-world data, necessitating a more data-driven approach to enhance accuracy.


### 1.4. Can you think of ways to improve your tracking results in the future?

There are various avenues for enhancing the existing sensor fusion and tracking system:

1. Explore advanced data association algorithms, like Global Nearest Neighbor (GNN) or Joint Probabilistic Data Association (JPDA), to replace the simpler Single Nearest Neighbor (SNN) approach.

2. Substitute the existing camera detections in the tracking with more precise detections from Project 1, enhancing overall accuracy.

3. Enhance the Kalman filter by extending its capabilities to estimate the object's width, length, and height, moving beyond the reliance on unfiltered lidar detections as implemented in the current project.

4. Fine-tune various parameters, e.g. the system parameters by incorporating standard deviation values for lidar, derived from 3D object detection in the midterm project, into the system noise Q.


## 2. Tracking

The functions related to tracking have been implemented in [filter.py](student/filter.py).  The resulting RMSE is shown below.  Despite a relatively high initial error, it is gradually reduced to reach a mean below 0.35 m.

<img src="img/ID_S1_RMSE.png" width="800"/>


## 3. Track Management

The functions related to the track management have been implemented in [trackmanagement.py](student/trackmanagement.py).  The following table illustrates the succession of relevant events:

|# frame | Event | Explanation |
|---|---|---|
| 67 | Track 0 is created | / |
| 68 | Track 0 is tentative | Detected a second time |
| 71 | Track 0 is confirmed | Threshold score of 0.8 reached |
| 97 | Track 0 is removed | Thresholed of estimation error covariance reached |

The mean RMSE remains relatively high at 0.78 m due to a y-offset of the lidar detection as explained in the project instructions:

<img src="img/ID_S2_RMSE.png" width="800"/>


## 4. Data Association

The functions related to the data association have been implemented in [association.py](student/association.py).  The following figure illustrates that multiple vehicles are successfully tracked.

<img src="img/ID_S3_Tracking-View.png" width="800"/>


The RMSE plot below indicates that track 0 and 1 have been active for the entire duration, while track 10 only became active at about 10s.  This can be explained by vehicles 0 and 1 moving approximately at the same speed than the measuring vehicles, while vehicle 10 overtakes the latter.

<img src="img/ID_S3_RMSE.png" width="800"/>


## 5. Sensor Fusion

The functions related to the sensor fusion have been implemented in [measurements.py](student/measurements.py).  The figure below shows that the RMSE has on average been reduced with the help of the additional camera data.

<img src="img/ID_S4_RMSE.png" width="800"/>

This video illustrates the final results: [Link](img/video.mp4)
