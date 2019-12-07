# Essential DeepRacer Analytics

## tl;dr

* Submit every single model you create to the race, even if you think a model isn’t good enough.
* If it manages to complete a lap, submit it again to see if the lap time becomes better.
* If it didn’t manage to complete a lap, submit it again to see if it will manage to complete a lap.
* Keep a log with every submission you make to the race. Model name, date and time, lap time. That info will be useful whenever you have the time to read the rest of this short document.
* Remember that you can submit as many models as you wish to the race. You can even submit the same model more than once. The only limitation is that you have to wait 30 minutes before making a new submission to the race.

_(*) Essential analytics means, literally essential.
If you would like to use advanced analytics, please look for the exceptional resources shared on ... ._
 
When submitting a model to the race:

> Tip: When submitting a model to the race, keep a record with the following information:
* Model name
* Submission date and time
* Average lap time
* Also, by clicking on “Evaluation logs”, keep the information of the “Last Event Time” for future reference.

*Keeping the above information, makes it very easy to access the logs of a particular model and submission at any time. Otherwise, it becomes difficult and time consuming to find out which log file corresponds to which submission you've made to the race.*

## Evaluation logs:
Clicking the “Evaluation logs” link, takes you to a page where only one file appears. The current logs. Click the file to open and you see the following page.
Scrolling the file, you will see a lot of information (below, the default hyperparameters appear) but you are mostly interested on the 5 episodes that begin after several lines of entries.
Note: No need to use the “CloudWatch Logs Insights”
 
The default layout of the logs is easy to read, but if you would like to copy a part of the logs, it’s easier to change the layout by clicking on the top and selecting “Text”:

Whenever submitting a model to the race, the car always runs 5 laps. Each of those laps is an episode (Episode 0, 1, 2, 3, 4). The submission is successful if the car manages to complete at least 1 lap out of the 5. If it completes more than 1 laps, then the best lap time is used.
Each new episode in the logs starts with the line “agent: Starting evaluation phase” followed by several (or even hundreds) of “SIM_TRACE_LOG:” lines.


Each “SIM_TRACE_LOG:” line has 16 variables (separated by commas) which are as follows:

var | Meaning | example
---|---|---
1 | episode | 0, 1, 2, 3 or 4. Every time the car starts a new lap, a new episode starts.
2 | step | Starts at 0 and increments by 1 every 1/15 of a second. i.e. there are 15 steps on the log file for every second of the race.
3 | x-coordinate | The x-coordinate of the car
4 | y-coordinate | The y-coordinate of the car
5 | heading | The heading of the car in radians. 
6 | steering_angle | The steering angle in radians
7 | speed | The maximum speed of the car in meters per second (m/s)
8 | action_taken | The action number that the model takes, according to the numbering used in the action space
9 | reward | The reward that the model gets at each step
10 | job_completed | TRUE or FALSE. It’s FALSE and only becomes TRUE, when the episode has been completed
11 | all_wheels_on_track | TRUE or FALSE. The episode runs while this is TRUE. When it becomes FALSE, after a few steps, the episode ends.
12 | progress | Completion percentage of the track in %
13 | closest_waypoint_index | These are numbers across the track, starting from 1 and up to a max number which is usaually between 150 and 180
14 | track_length | The length of the track in meters
15 | time.time() | Time in a format like this: 1569740907.5428395
16 | *new variable* | Recently added variable with the values: in_progress, off_track, crashed, lap_complete

## The Variables in more detail

5. This is the heading of the car in radians. To convert to degrees, we should multiply by 57,29587795  
(360 degress = 2π radians => 1 radian = 360/2π degress => 1 radian = 360/2\*3,14159 => 1 radian = 57,2958)

On a X-Y coordinate, when the car is heading right, the heading is 0o. Heading up is 90o. Heading left is 180o
Negative values: When the car is heading right is 0o. Heading down is -90o and heading left is -180o
So, heading right, might be 180o or -180o depending on its previous position

### 14. track_length
This variable shows the length of the track in meters. Take into consideration though, that the training track is usually longer than the corresponding reacing track.

### 15. time.time()
This variable is used to calculate the time and the format is: 1569740907.5428395  
A simpler, though only approximate way to estimate the time, is to divide the number of steps with 15, as there are 15 steps every second.

### 16. *new variable* representing "status"
This variable was added at the end of November 2019 and it gets the following values:
* in_progress
* off_track
* crashed
* lap_complete
