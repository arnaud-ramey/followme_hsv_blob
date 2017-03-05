# followme_hsv_blob

[![Build Status](https://travis-ci.org/arnaud-ramey/followme_hsv_blob.svg)](https://travis-ci.org/arnaud-ramey/followme_hsv_blob)

followme_hsv_blob is used to follow a moving goal, made of a colorful marker.
For instance, it can be a bright orange strip.
The goal is detected and recognized thanks to color thresholding in the HSV color space.

Example
=======

To launch the tracking of a HSV color blob by a Parrot Jumping Sumo robot:

```bash
$ roslaunch followme_hsv_blob blob_tracker_sumo.launch
```

Blob tracker node
=================

Node parameters
---------------

- `~hue_min, ~hue_max, ~saturation_min, ~saturation_max, ~value_min, ~value_max`
  [int, range: 0~255, default: 0,255, 0,255, 0,255]

  The parameters of the HSV filter.
  They can also be adjusted in real-time:
  the window showing the filter results has a slider for each of the parameters.

- `~min_blob_size`
  [int, pixels, default: 10 pixels]

  The minimal size of the biggest blob in the HSV filter to be considered valid.
  If the biggest blob is smaller than this size, it is considered as noise
  and not tracked.

- `~max_blob_size`
  [int, pixels, default: 200 pixels]

  The size of the biggest blob in the HSV filter that triggers the robot to stop.
  If the biggest blob is bigger than this size, the robot
  is considered to be close enough and won't move forward.

- `~max_v, ~max_w`
  [double, m/s, rad/s, default: 1 m/s, 1 rad/s]

  The maximum linear and angular speeds of the robot.

- `~x_deadzone,`
  [double, range: 0~1, default: .2=20%]

  The deadzone of the horizontal position of the biggest blob to be considered centered
  according to the robot direction.
  If the normalized x-coordinate in the image of the biggest blob is between
  `0.5-x_deadzone/2` and `0.5+x_deadzone/2`, it is considered centered.
  Otherwise the robot will turn inplace to center it.

Subscriptions
-------------

- `camera/image_raw`
  [sensor_msgs::Image]

  The RGB video stream coming from the robot.

Publications
------------

- `cmd_vel`
  [geometry_msgs::Twist, (m/s, rad/s)]

  The instantaneous speed order.
