# Final Project: Sensor Fusion and Object Tracking

This is the final project of the section "Sensor Fusion and Tracking" in [Udacity's Nanodegree Program "Self Driving Car Engineer"](https://www.udacity.com/course/self-driving-car-engineer-nanodegree--nd0013).


## 1. Summary

### 1.1. Write a short recap of the four tracking steps and what you implemented there (filter, track management, association, camera fusion). Which results did you achieve? Which part of the project was most difficult for you to complete, and why?

The four tracking steps, their implementatino and the results are explained [below](#2.-tracking) in section 2.-5.


### 1.2. Do you see any benefits in camera-lidar fusion compared to lidar-only tracking (in theory and in your concrete results)?


### 1.3. Which challenges will a sensor fusion system face in real-life scenarios? Did you see any of these challenges in the project?


### 1.4. Can you think of ways to improve your tracking results in the future?



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
