# What is this

This is a [Docker Machine](https://docs.docker.com/machine/overview/) Driver for [Bhyve](http://bhyve.org/). It is
heavily inspired by the [xhyve driver](https://github.com/machine-drivers/docker-machine-driver-xhyve), the
[generic](https://github.com/docker/machine/tree/master/drivers/generic) driver and the
[VirtualBox](https://github.com/docker/machine/tree/master/drivers/virtualbox) driver.
See also [this issue](https://github.com/machine-drivers/docker-machine-driver-xhyve/issues/200).

# How To Use It

## One time setup

* Install required packages:
  * `sudo`
  * `grub2-bhyve`
  * `dnsmasq`

* User running docker-machine must have password-less `sudo` access.

* Add user to wheel group

* Add these lines to /etc/devfs.rules:

```
[system=10]
add path 'nmdm*' mode 0660
```

* Set `devfs_system_ruleset="system"` in `/etc/rc.conf` and run `service devfs restart`

* Add `ng_ether`, `nmdm` and `vmm` to `kld_list` in `/etc/rc.conf`, `kldload ng_ether`, `kldload vmm`, `kldload nmdm`.

## Build

```
make
```

## Setup

```
export MACHINE_DRIVER=bhyve
export PATH=${PATH}:${PWD}
```

## Normal usage

```
docker-machine kill default || :
docker-machine rm -y default || :

docker-machine create
eval $(docker-machine env)
docker run --rm hello-world
```


### TODO

* Remove reliance on external files
* Remove reliance on external config
* Remove hard coded stuff
    * Docker port
    * `sudo` - may want to use `doas`
* Avoid shelling out as much as possible
* Manage processes (grub-bhyve, bhyve, serial logger)
* Networking
    * Create VLAN
    * Attach VLAN to bridge
