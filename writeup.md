# Final Project: Sensor Fusion and Object Tracking

This is the final project of the section "Sensor Fusion and Tracking" in [Udacity's Nanodegree Program "Self Driving Car Engineer"](https://www.udacity.com/course/self-driving-car-engineer-nanodegree--nd0013).


## 1. Tracking

The functions related to tracking have been implemented in [filter.py](student/filter.py).  The resulting RMSE is shown below.  Despite a relatively high initial error, it is gradually reduced to reach a mean below 0.35 m.

<img src="img/ID_S1_RMSE.png" width="800"/>


## 2. Track Management

The functions related to the track management have been implemented in [trackmanagement.py](student/trackmanagement.py).  The following table illustrates the succession of relevant events:

|# frame | Event | Explanation |
|---|---|---|
| 67 | Track 0 is created | / |
| 68 | Track 0 is tentative | Detected a second time |
| 71 | Track 0 is confirmed | Threshold score of 0.8 reached |
| 97 | Track 0 is removed | Thresholed of estimation error covariance reached |

The mean RMSE remains relatively high at 0.78 m due to a y-offset of the lidar detection as explained in the project instructions:

<img src="img/ID_S2_RMSE.png" width="800"/>


## 3. Data Association

## 4. Sensor Fusion

## 5. Evaluation and Conclusion

