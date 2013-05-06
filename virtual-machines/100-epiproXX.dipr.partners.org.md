## 100 epiproXX.dipr.partners.org configuration

Each **epiproXX** machine is configured identically and is used to host the following Rails applications (in order of application creation date).

The only exception to this is that **epipro01** runs cron jobs for Rails rake tasks (ex: such as the daily email rake task for Task Tracker).

### 101 Technology

```
Nginx                   1.4.0
Ruby Version Manager    1.18.21 (stable)
Ruby                    ruby 2.0.0p0 (2013-02-24 revision 39474) [x86_64-linux]
Passenger               4.0.1
```

### 102 Rails Applications

#### Sleep Portal

Proxy Path: /hybrid


#### Task Tracker

Proxy Path: /tasktracker


#### CHAT Publications

Proxy Path: /review


#### Screen

Proxy Path: /screen


#### Slice

Proxy Path: /slice


#### Training Grant Manager

Proxy Path: /training_grant


### First Step

[110 - Prerequisites](https://github.com/sleepepi/sleepepi/tree/master/virtual-machines/110-prerequisites.md)
