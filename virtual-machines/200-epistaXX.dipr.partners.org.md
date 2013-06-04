## 200 epistaXX.dipr.partners.org configuration

These servers are load balanced and run the **staging** environments for multiple Rails applications.

Each application is available under the `/edge/` root of **sleepepi.dipr.partners.org**.

### 201 Technology

```
Nginx                   1.4.1
Ruby Version Manager    rvm 1.20.13 (stable)
Ruby                    ruby 2.0.0p195 (2013-05-14 revision 40734) [x86_64-linux]
Passenger               4.0.5
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

