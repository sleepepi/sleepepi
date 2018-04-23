# sleepepi proxy configuration and server setup

Documentation providing architecture overview of sleepepi

## Network Architecture

```
`-- sleepepi.partners.org
    `-- sleepepi.dipr.partners.org          1GB     CentOS release 5.10 (Final)
`-- tryslice.io, tryslice.com, tryslice.org, slice.partners.org
    `-- slice.dipr.partners.org             2GB     CentOS release 7.4  (Core)
        |-- epipro03.dipr.partners.org      2GB     CentOS release 7.3  (Core)
        |-- epipro04.dipr.partners.org      2GB     CentOS release 7.3  (Core)
        `-- epijob01.dipr.partners.org      2GB     CentOS release 7.4  (Core)
`-- sleepdata.org
    `-- sleepdata.dipr.partners.org         2GB     CentOS release 7.4  (Core)
        |-- epipro05.dipr.partners.org      2GB     CentOS release 7.3  (Core)
        |-- epipro06.dipr.partners.org      2GB     CentOS release 7.3  (Core)
        `-- epipro07.dipr.partners.org      2GB     CentOS release 7.3  (Core)
`-- sleepclinic.partners.org
    `-- sleepclinic.dipr.partners.org       1GB     CentOS release 6.9  (Final)
`-- tasktracker.partners.org
    `-- tasktracker.dipr.partners.org       1GB     CentOS release 6.9  (Final)
`-- traintracks.partners.org
    `-- traintracks.dipr.partners.org       2GB     CentOS release 7.3  (Core)
`-- myapnea.org, myapnea.net
    `-- myapnea.dipr.partners.org           2GB     CentOS release 7.4  (Core)
        |-- myapneapro01.dipr.partners.org  2GB     CentOS release 7.3  (Core)
        |-- myapneapro02.dipr.partners.org  2GB     CentOS release 7.3  (Core)
        `-- myapneapro03.dipr.partners.org  2GB     CentOS release 7.3  (Core)
`-- bostonsleep.org
    `-- bostonsleep.dipr.partners.org       2GB     CentOS release 7.4  (Core)
`-- patstrial.org
    `-- patstrial.dipr.partners.org         1GB     CentOS release 7.4  (Core)
`-- sleepinnovate.org
    `-- sleepinnovate.dipr.partners.org     2GB     CentOS release 7.3  (Core)
`-- staging.partners.org
    `-- staging.dipr.partners.org           2GB     CentOS release 7.4  (Core)
        `-- epista01.dipr.partners.org      2GB     CentOS release 7.3  (Core)
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
