# Read Me

## An Inertial and Positioning Dataset for the walking activity

Guidelines for dataset usage

We publish a walking activity dataset including inertial and positioning information from 19 volunteers including reference distance measured using a trundle wheel.
Each track has data from the accelerometer and gyroscope embedded in the phones, location information from the Global Navigation Satellite System (GNSS), and the step count obtained by the device.

Example code can be found at [the following link](https://github.com/SaraCaramaschi/walking_dataset_for_6MWT/)

The data folder contains a metadata_tracks.csv file with attributes for each track. In addition, for every participant there is a folder (subject_X, X being a unique subject identifier) and for every track, a sub-folder (X_N, X being a unique subject identifier and N being the track identifier).

**Every track folder contains the following CSV files:**
Empty cells within a CSV file can be considered as missing data due to jittering or signal loss during data transmission or recording errors. 

| events.csv  |                                                                                  |
| :---------- | :------------------------------------------------------------------------------- |
| signalStart | time at which the test starts (but not walking!), always set as 0ms.             |
| testStart   | ms since signalStart when the GNSS signal reaches enough quality (15m accuracy). |
| testEnd     | ms since signalStart when data collection stops.                                 |

| positions.csv                     |                                                                                             |
| :-------------------------------- | :------------------------------------------------------------------------------------------ |
| ms                                | milliseconds from signalStart. Zero ms corresponds to the value of testStart in events.csv. |
| latitude, longitude, and altitude | geolocation coordinates.                                                                    |
| confInterval                      | confidence interval reported by the GNSS system heading.                                    |
| speed                       	    | sample-wise speed computed by the system. \[m/s]                                                   |
| heading 		            | value of heading for that timestamp.							  |


| orientation.csv    |                                |
| :----------------- | :----------------------------- |
| ms                 | milliseconds from signalStart. |
| alpha, beta, gamma | device orientation.            |

| steps.csv          |                                           |
| :----------------- | :---------------------------------------- |
| ms                 | milliseconds from signalStart.            |
| steps              | incremental number of steps taken.        |
| startDate, endDate | ms intervals when those steps were taken. |
|floorsUp| number of ascending floors (not to consider) |
|floorsDown|number of descending floors (not to consider)|
|distance| distance estimated by the smartphone (not to consider)|


| motion.csv                                                    |                                        |
| :------------------------------------------------------------ | :------------------------------------- |
| ms                                                            | milliseconds from signalStart.         |
| accelX, accelY, accelZ, accelWithGX, accelWithGY, accelWithGZ | acceleration without and with G force. \[m/s^2]  |
| rotRateAlpha, rotRateBeta, rotRateGamma                       | rotation rate.                         |
| interval                                                      | sampling frequency in ms.              |

| reference\_cont\_distance.csv | available if the reference distance is continuous       |
| :---------------------------- | :-------------------------------------------- |
| ms                            | milliseconds from signalStart                 |
| distance                      | continuous incremental value of distance \[m] |

**Columns and description of the metadata_tracks.csv files and attributes:**
Missing data for certain tracks (hasMotion: False or hasGNSS: False) is given by technical issues (subjects did not update smartphone app) or challenges to collect GNSS signal. 

| Column                      | Description                                                                                          |
| :-------------------------- | :--------------------------------------------------------------------------------------------------- |
| subject                     | unique subject ID.                                                                                   |
| testID                      | test ID.                                                                                             |
| testName                    | subjectID\_testID.                                                                                   |
| isPatient                   | boolean value True or False.                                                                         |
| distanceReference           | total distance walked \[m].                                                                          |
| hasMotion                   | boolean value True or False if during the walk IMU was collected.                                    |
| hasGNSS                     | boolean value True or False if during the walk GNSS signal was received.  
| device                      | brand, model and operating system of the smartphone.                                                 |
| distanceByApp               | distance measured by the Timed Walk App.                                                             |
| totSteps                    | total steps taken during the walk.                                                                   |
| path curvature              | 0,1, or 2 indicating a straight, gently curved (<6 90 deg curves) or curved path (>5 90 deg curves). |
| total\_gaps\_time\_inertial | total time in seconds where IMU was not received for more than 0.05 seconds.                         |
| total\_gaps\_time\_gnss     | total time in seconds where GNSS signal was not received for more than 6 seconds.                    |
| gt\_type                    | "final" or "continuous" according to which type of reference distance was collected.                 |
| country                     | country where the subject registered the track (UK or SE)                                            |
| gnss\_anonimized            | boolean True or False according to whether the geographical positions were anonymized.               |
| duration \[s]               | duration of the walk \[s].                                                                           |
| fs\_acc                     | average IMU sampling frequency.                                                                      |
| fs\_gnss                    | average GNSS signal sampling frequency.                                                              |
| fs\_steps                   | average step counting sampling frequency.                                                            |
| average\_walking\_speed     | total reference distance divided by the test duration.                                               |
| smartphone\_position        | Used smartphone position (Hand held).                                                                |
| smartphone app              | Used smartphone app (Timed Walk App or Malisa).                                                      |
