# What is this

This is a [Docker Machine](https://docs.docker.com/machine/overview/) Driver for [Bhyve](http://bhyve.org/). It is
heavily inspired by the [xhyve driver](https://github.com/machine-drivers/docker-machine-driver-xhyve), the
[generic](https://github.com/docker/machine/tree/master/drivers/generic) driver and the
[VirtualBox](https://github.com/docker/machine/tree/master/drivers/virtualbox) driver.
See also [this issue](https://github.com/machine-drivers/docker-machine-driver-xhyve/issues/200).

# How To Use It

* Must have `sudo` installed and user running docker-machine must have password-less `sudo` access.
* Interface `bridge0` must exist and must have a member with a DHCP server on the same network
* Must know what IP the DHCP is going to give the machine with MAC address `00:A0:98:00:00:02`

```
docker-machine create --bhyve-ip-address 10.0.1.119
eval $(docker-machine env)
docker run --rm hello-world
```

### TODO

* Remove reliance on external files
* Remove reliance on external config
* Remove hard coded stuff
    * Paths
    * Files
    * Device names
    * MAC Address
    * `nmdm` Device
    * Docker port
    * `sudo` - may want to use `doas`
    * Avoid shelling out as much as possible

* Fetch ISO
* Log console
* Fix removing VM
* Fix state
* Implement unimplemented funcs
* Start vs. Create
* Stop
* Manage processes (grub-bhyve, bhyve, serial logger)
* Create vlan, attch vlan to bridge, attach machines to vlan