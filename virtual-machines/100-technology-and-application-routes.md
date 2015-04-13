## 100 epiproXX.dipr.partners.org configuration

Each **epiproXX** machine is configured identically and is used to host the following Rails applications (in order of application creation date).

The only exception to this is that **epipro01** runs cron jobs for Rails rake tasks (ex: such as the daily email rake task for Task Tracker).

### 101 Technology

```
Nginx                   1.4.4
Ruby Version Manager    1.25.14 (stable)
Ruby                    ruby 2.1.0p0 (2013-12-25 revision 44422) [x86_64-linux]
Passenger               4.0.33
```

### 102 Front End Servers to Back End Rails Applications

| F.E.Server    | Path            | Application       |   epipro01   |   epipro02   |   epipro03   |   epipro04   |   epipro05   |   epipro06   |   epipro07   | tasktracker  |
| ------------- | --------------- | ----------------- |:------------:|:------------:|:------------:|:------------:|:------------:|:------------:|:------------:|:------------:|
| sleepepi      | /randomization  | Randomization     |      X       |      X       |      -       |      -       |      -       |      -       |      -       |      -       |
| sleepepi      | /review         | CHAT Publications |      X       |      X       |      -       |      -       |      -       |      -       |      -       |      -       |
| sleepepi      | /tasktracker    | Task Tracker      |      X       |      X       |      -       |      -       |      -       |      -       |      -       |      -       |
| sleepepi      | /traintracks    | Train Tracks      |      X       |      X       |      -       |      -       |      -       |      -       |      -       |      -       |
| sleepclinic   | /               | Try Slice         |      -       |      -       |      X       |      X       |      -       |      -       |      -       |      -       |
| slice         | /               | Try Slice         |      -       |      -       |      X       |      X       |      -       |      -       |      -       |      -       |
| sleepdata     | /               | sleepdata.org     |      -       |      -       |      -       |      -       |      X       |      X       |      X       |      -       |
| tasktracker   | /               | Task Tracker Demo |      -       |      -       |      -       |      -       |      -       |      -       |      -       |      X       |


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
