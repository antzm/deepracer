# Creating a DeepRacer Model

1. Log in to the AWS Console
2. Search for DeepRacer and select it
3. Create the DeepRacer resources (only needed during the very first time you are using DeepRacer).
4. Go to Garage and build our model  

In this section, we are going to select the configuration of the car that we will use to build our model.  

We have the option to select a car with:

* One camera
	* Classic DeepRacer configuration
* Stereo Camera
	* Advanced configuration with two cameras that provides distance information which is useful to calculate the distance from objects and thus, helps to avoid collision with vatious objects on the track, or even other DeepRacer cars that raace on the same track.

And then, we are going to select the action space of our car.

This means that we are going to select:

The car's maximum speed and the speed granularity
* The maximum speed can be set from 0.1 m/s to 4 m/s, in steps of 0.1 m/s
* While the speed granularity can be either 1, 2 or 3

The car's maximum steering angle and the steering granularity
* The maximum steering angle can be set from 0 degrees to 30 degress, in steps of 1 degree
* While the steering granularity can be either 1, 3, 5 or 7

Thus, the action space will have a total number of actions based on the speed granularity and the steering granularity that we have selected:

Total number of actions in the action space = 
= speed granularity * steering granularity

Each action in the action space will have a unique number. In the logs, we can see that number and so we are able understand the exact acion that the our model chose at every step of a race.

Example 1:  

Example 2:  

Example 3:  

5. Create your first model 
