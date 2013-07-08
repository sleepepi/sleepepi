## 100 epiproXX.dipr.partners.org configuration

Each **epiproXX** machine is configured identically and is used to host the following Rails applications (in order of application creation date).

The only exception to this is that **epipro01** runs cron jobs for Rails rake tasks (ex: such as the daily email rake task for Task Tracker).

### 101 Technology

```
Nginx                   1.4.1
Ruby Version Manager    1.21.7 (stable)
Ruby                    ruby 2.0.0p247 (2013-06-27 revision 41674) [x86_64-linux]
Passenger               4.0.7
```

### 102 epiproXX.dipr.partners.org Rails Applications

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


### 103 tasktracker.dipr.partners.org Rails Applications

This server hosts the Task Tracker Demo site available at https://tasktracker.partners.org.

#### Task Tracker

Proxy Path (root): /


### 104 slice.dipr.partners.org Rails Applications

This server hosts the Slice Demo site available at https://slice.partners.org.

#### Slice

Proxy Path (root): /


### 109 epistaXX.dipr.partners.org Rails Applications

These servers are load balanced and run the **staging** environments for multiple Rails applications.

Each application is available under the `/edge/` root of **sleepepi.dipr.partners.org**.

#### Sleep Portal

Proxy Path: /edge/hybrid

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





### First Step

[110 - Prerequisites](https://github.com/sleepepi/sleepepi/tree/master/virtual-machines/110-prerequisites.md)
