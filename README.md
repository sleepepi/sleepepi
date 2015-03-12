# sleepepi proxy configuration and server setup

Documentation providing architecture overview of sleepepi

## Network Architecture

```
`-- sleepepi.partners.org
    `-- sleepepi.dipr.partners.org          1GB     CentOS release 5.10 (Final)
        |-- epista01.dipr.partners.org      1GB     CentOS release 6.5  (Final)
        |-- epipro01.dipr.partners.org      2GB     CentOS release 5.10 (Final)
        `-- epipro02.dipr.partners.org      2GB     CentOS release 5.10 (Final)
`-- tryslice.io, tryslice.com, tryslice.org, slice.partners.org
    `-- slice.dipr.partners.org             1GB     CentOS release 6.5  (Final)
        |-- epipro03.dipr.partners.org      1GB     CentOS release 6.5  (Final)
        `-- epipro04.dipr.partners.org      1GB     CentOS release 6.5  (Final)
`-- sleepdata.org
    `-- sleepdata.dipr.partners.org         1GB     CentOS release 6.5  (Final)
        |-- epipro05.dipr.partners.org      1GB     CentOS release 6.5  (Final)
        |-- epipro06.dipr.partners.org      1GB     CentOS release 6.5  (Final)
        `-- epipro07.dipr.partners.org      1GB     CentOS release 6.5  (Final)
`-- sleepclinic.partners.org
    `-- sleepclinic.dipr.partners.org       1GB     CentOS release 6.5  (Final)
`-- tasktracker.partners.org
    `-- tasktracker.dipr.partners.org       1GB     CentOS release 6.5  (Final)
`-- myapnea.org, myapnea.net
    `-- myapnea.dipr.partners.org           1GB     CentOS release 6.5  (Final)
        |-- myapneapro01.dipr.partners.org  1GB     CentOS release 6.6  (Final)
        |-- myapneapro02.dipr.partners.org  1GB     CentOS release 6.6  (Final)
        `-- myapneapro03.dipr.partners.org  1GB     CentOS release 6.6  (Final)
```

## Servers

Front End Servers

- [sleepepi.dipr.partners.org](https://github.com/sleepepi/sleepepi/tree/master/virtual-machines/000-sleepepi.dipr.partners.org.md)
- [sleepclinic.dipr.partners.org](https://github.com/sleepepi/sleepepi/tree/master/virtual-machines/100-technology-and-application-routes.md)

Back End Production Servers

- [epiproXX.dipr.partners.org](https://github.com/sleepepi/sleepepi/tree/master/virtual-machines/100-technology-and-application-routes.md)

Back End Staging Servers

- [epistaXX.dipr.partners.org](https://github.com/sleepepi/sleepepi/blob/master/virtual-machines/100-technology-and-application-routes.md)

Demo Servers

- [tasktracker.dipr.partners.org](https://github.com/sleepepi/sleepepi/blob/master/virtual-machines/100-technology-and-application-routes.md)
- [slice.dipr.partners.org](https://github.com/sleepepi/sleepepi/blob/master/virtual-machines/100-technology-and-application-routes.md)
