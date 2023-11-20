# home-monitoring-stack

for now it is just a dockerized version of https://github.com/ar51an/unbound-exporter setup to work with unbound in OPNSense

## Random Infos
most of the config for the unbound-exporter can be set in the advance tab in the webgui:
![image](https://github.com/roastpiece/home-monitoring-stack/assets/64126646/52c9dd0e-0966-432f-8ab9-2a1582667aff)

additionally on the opnsense box the listening interface for the remote-control needs to be set to be reachable from the docker host:
  
`/usr/local/etc/unbound.opnsense.d/unbound-exporter.conf`
```
remote-control:
control-interface: 192.168.1.11
```

for collecting the logs i configured a syslog listener in promtail and use the OPNSense syslog-ng service to forward the logs:
![image](https://github.com/roastpiece/home-monitoring-stack/assets/64126646/e64558d3-5fe7-41e5-a424-4caeb1a66543)

in the unbound-exporter i made the blockfile optional and have disabled it for now in this setup.
In the future i think i will collect this metric from the logs:  
`Informational	unbound	[38399:6] info: dnsbl_module: blocklist loaded. length is 1168543`

## Deployment
Setup OPNSense like above.  
Then deploy the stack:  
`docker stack deploy -c ./docker-compose.yml monitoring-stack`

🤷
