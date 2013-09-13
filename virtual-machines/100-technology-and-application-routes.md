## 100 epiproXX.dipr.partners.org configuration

Each **epiproXX** machine is configured identically and is used to host the following Rails applications (in order of application creation date).

The only exception to this is that **epipro01** runs cron jobs for Rails rake tasks (ex: such as the daily email rake task for Task Tracker).

### 101 Technology

```
Nginx                   1.4.2
Ruby Version Manager    1.21.8 (stable)
Ruby                    ruby 2.0.0p247 (2013-06-27 revision 41674) [x86_64-linux]
Passenger               4.0.17
```

### 102 Front End Servers to Back End Rails Applications

| F.E.Server    | Path            | Application       |   epipro01   |   epipro02   |   epipro03   |   epipro04   | tasktracker  |    slice     |
| ------------- | --------------- | ----------------- |:------------:|:------------:|:------------:|:------------:|:------------:|:------------:|
| sleepepi      | /sleepportal    | Sleep Portal      |      X       |      X       |      -       |      -       |      -       |      -       |
| sleepepi      | /rely           | Rely              |      X       |      X       |      -       |      -       |      -       |      -       |
| sleepepi      | /review         | CHAT Publications |      X       |      X       |      -       |      -       |      -       |      -       |
| -*            | /screen         | Screen            |      X       |      X       |      -       |      -       |      -       |      -       |
| sleepepi      | /slice          | Slice             |      X       |      X       |      -       |      -       |      -       |      -       |
| sleepepi      | /tasktracker    | Task Tracker      |      X       |      X       |      -       |      -       |      -       |      -       |
| sleepepi      | /training_grant | Training Grant    |      X       |      X       |      -       |      -       |      -       |      -       |
| sleepclinic   | /slice          | Clinical Slice    |      -       |      -       |      X       |      X       |      -       |      -       |
| tasktracker   | /               | Task Tracker Demo |      -       |      -       |      -       |      -       |      X       |      -       |
| slice         | /               | Slice Demo        |      -       |      -       |      -       |      -       |      -       |      X       |

\* The screen web application is not hosted through a front end server

### 109 epistaXX.dipr.partners.org Rails Applications

These servers are load balanced and run the **staging** environments for multiple Rails applications.

Each application is available under the `/edge/` root of **sleepepi.dipr.partners.org**.

#### Sleep Portal

Proxy Path: /edge/sleepportal

#### Task Tracker

Proxy Path: /edge/tasktracker

#### CHAT Publications

Proxy Path: /edge/review

#### Screen

Proxy Path: /edge/screen

#### Training Grant Manager

Proxy Path: /edge/training_grant

#### Slice

Proxy Path: /edge/slice


#### Front End Server Configuration

Both **sleepepi.dipr.partners.org**, and **sleepclinic.dipr.partners.org** are front end servers that act as routers to the **epiproXX** machines.

Specific nginx configuration for **sleepclinic.dipr.partners.org** can be found here: [500 Front End Server Configuration](https://github.com/sleepepi/sleepepi/blob/master/virtual-machines/500-front-end-server-configuration.md)


### First Step

[110 - Prerequisites](https://github.com/sleepepi/sleepepi/tree/master/virtual-machines/110-prerequisites.md)
