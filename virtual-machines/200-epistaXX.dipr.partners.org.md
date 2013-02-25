## 200 epistaXX.dipr.partners.org configuration

These servers are load balanced and run the **staging** environments for multiple Rails applications.

Each application is available under the `/edge/` root of **sleepepi.dipr.partners.org**.

### 201 Technology

```
Nginx                   1.2.6
Ruby Version Manager    rvm 1.18.14
Ruby                    ruby 1.9.3p327 (2012-11-10 revision 37606) [x86_64-linux]
Ruby (upcoming)         ruby 2.0.0p0 (2013-02-24 revision 39474) [x86_64-linux]
Passenger               3.0.19
```

### 202 Rails Applications

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

