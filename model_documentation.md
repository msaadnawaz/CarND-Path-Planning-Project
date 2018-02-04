# Documentation: Path Planning Project
The path planning project is divided into three sections:
  1. Prediction
  2. Behavior planning
  3. Trajectory generation
  
## Prediction:
The prediction model only searches if there is a car too close ahead (less than 30 meters) in ego car's path which may collide in near-future and if it decides to change lanes in case of a car too close ahead of the ego car, the model searches if there is a car in goal lane between the area of 10 meters behind the ego car and 30 meters ahead of ego car.

## Behavior Planning:
Based upon the prediction, the behavior planning model chooses to change to another lane or stay in the current lane.

The ego car stays in same same lane until there is another car ahead within the dangerous distance (30m), it then changes to the state where it prepares to enter a new lane. According to defined policy, the ego car can only go to center lane (lane 1) from left lane (lane 0) and right lane (lane 2), however from center lane, the car prepares to change to left lane first but in case of another car within the dangerous distance (10m behind to 30m ahead) it prepares to change to right lane instead.

During preparation to change to a given lane, the ego car searches if there is a car within the dangerous distance in goal lane, if the goal lane is clear then it changes the lane otherwise it stays in same lane (except changing from center lane as described in previous para) and slows down to avoid getting any closer to the car in front.

As a general policy, the ego car only changes lanes if its velocity is more than 35mph.

The state machine implementing the model is shown in the figure below:
![alt_text](State_machine.jpg?raw=true "State Machine")

## Trajectory Generation:
The trajectory generator takes previous 2 points forwarded to simulator as well as current location of car and also generates the intended future waypoints depending upon goal lane (current or different).

Here, the spline comes to advantage to create smooth path connecting previous path (forwarded to simulator) and the future waypoints. Similarly, the intermediate path steps at every time step (0.02 seconds) are also calculated using spline and then displayed in the simulator.
