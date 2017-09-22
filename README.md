# RaspiClusterConfig
Automatic configuration of a Raspberry cluster using Ansible.
Used to manage my personal cluster of SBC with Ansible.

Cluster made of 7 machines :

* raspi000 : runs domoticz, and grafana
  * Connected to RfxCom 433 MHz receiver
  * Connected to a MySensors gateway
  * Grafana should be moved to raspi003
* raspi001 : runs rabbitmq (with MQTT protocol support)
* raspi002 : runs node red
* raspi003 : runs influxdb (should also run grafana as well)
* raspi004 : newly installed
* raspi005 : newly installed

* volumio : audio player
