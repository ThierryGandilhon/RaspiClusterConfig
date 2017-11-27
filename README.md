# RaspiClusterConfig

Automatic configuration of a Raspberry cluster using Ansible.
Used to manage my personal cluster of SBC with Ansible.

Cluster made of 7 machines :

* `raspi000` : runs domoticz, and grafana
  * Connected to RfxCom 433 MHz receiver
  * Connected to a MySensors gateway
  * Grafana should be moved to raspi003
* `raspi001` : runs rabbitmq (with MQTT protocol support)
* `raspi002` : runs node red
* `raspi003` : runs influxdb (should also run grafana as well)
* `raspi004` : newly installed
* `raspi005` : newly installed

* `volumio` : audio player

## Tips and tricks to be reminded

### Running commands on multiple machines

To run a command on multiple machines the syntax is:

```bash
ansible group -m module -a arguments
```

So

```bash
ansible all -m ping
```

executes the `ping` module on the machines of group named `all`.

To run in parallel, use the `-f` option to fork multiple executions:

```bash
ansible all -m ping -f 10
```

By default the module is `command`. So

```bash
ansible all -a "date"
```

executes the `date` command on each machine of the `all` group.

To see hosts uptime:

```bash
ansible all -a uptime
```

To become `root`, use the `--become` option. Here are some exmaples of packets management.

```bash
ansible all -m apt -a "upgrade=no update_cache=yes" --become --forks=10
ansible all -m apt -a "upgrade=dist update_cache=yes" --become --forks=10
ansible all -m apt -a "upgrade=dist update_cache=yes autoremove=yes" --become --forks=10
ansible all -m apt -a "name=nfs-kernel-server state=absent purge=yes autoremove=yes" --become --forks=10
```

### Gather information on hosts

To gather info on multiple hosts (very talkative):

```bash
ansible all -m setup
```
