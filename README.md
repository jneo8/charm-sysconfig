# Overview

This is a subordinate charm to deploy the cpufrequtils package and
configure a type of CPU reservation: isolcpus or CPU Affinity.

# Usage

Deploy sysconfig alongside your service,

    juju deploy sysconfig

Add the relations: 

    juju add-relation sysconfig os-cs-vnf

# Configuration

## Reservation

By default, the charm does not configure any CPU related reservation.
However, "isolcpus" or "affinity" can be configured on systemd hosts.

## cpu-range

In case of "isolcpus", it determines the pcpus that won't be used by the
host (ie. the same range is configured for QEMU usage).

In case of "affinity", it determines the pcpus that the host WILL use
(ie. a complementary range to the QEMU vcpu_pin_set).

If this value is left empty, charm behaves as if reservation=off.

## update-grub

By default, this value is set to "false". If enabled, charm will run
"update-grub" when changing /etc/default/grub (when
reservation=isolcpus).

## config-flags

If you need further options configured, this extra optons will be added
to the files:
 * `/etc/default/grub` (reservation=isolcpus)
 * `/etc/systemd/system.conf` (reservation=affinity)

It does nothing if reservation=off.

# Contact Information

- Charm bugs: https://bugs.launchpad.net/bootstack-ops
