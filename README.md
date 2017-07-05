# Nagios NRPE WordPress check

Nagios NRPE plugin to check WordPress update

## Supervisor side

**Host mywebsite.cfg** :

```
define host {
   host_name            mywebsite
   alias                My Website
   use                  generic-host
   address              XXX.XXX.XXX.XXX
}

define service{
   host_name            mywebsite
   use                  generic-service
   service_description  Wordpress Updates
   check_command        check_nrpe!check_wp_mywebsite
}
```

## Client side

Copy check_wp to your Nagios plugins folder. For me, it's on /etc/nagios-plugins

make it executable

```
$ chmod +x /etc/nagios-plugins/check_wp
```

Now, edit your nrpe.cfg

```
$ vi /etc/nagios/nrpe.cfg
```

and add at the end of the file :

```
command[check_wp_mywebsite] = sudo /etc/nagios-plugins/check_wp /path/to/wordpress/installation
```

optionaly you can pass fake request url as parameter :

```
command[check_wp_mywebsite] = sudo /etc/nagios-plugins/check_wp /path/to/wordpress/installation "http://my.domain.com/"
```


## Todo
- Use argument for installation path of WordPress (soon)