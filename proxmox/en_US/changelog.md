---
layout: default
title: Proxmox changelog
lang: en_US
pluginId: proxmox
---

# 2020-08-25

- Update of the plugin icon to match the Jeedom standard
- Add an icon for each type of Proxmox resource for greater clarity
- During synchronization, the plugin will automatically activate and deactivate Jeedom devices corresponding to Proxmox resources depending on whether they exist or not in order to facilitate management and provide more clarity.
- Add an accordion menu in the devices page

# 2020-06-09

- Add support for Zstandard compression mode (zstd) in backup options, requires Proxmox 6.2

# 2020-03-30

- Move documentations
- Add "reset" command on VM

# 2020-02-12

- Add commands "Start all" and "Shutdown all" on the nodes
- Add commands "Shutdown the node" and "Reboot the node"
- Add commands "Suspend" and Resume" on VMs and LXCs

# 2019-11-23

- Added a specific health page listing an overview of all Proxmox resources

# 2019-11-16

- Added a field to enter a description (optional) when taking a snapshot. If you have scenarios using this command please check them.
- Add snapshot list command on VM and LXC
- Added a command giving the percentage of usage for memory, disk and swap on all devices
- remove vmid and node commands on all devices
- Fixed: status "paused" is correctly specified on a VM or a container on pause
- Fix: It is now possible to rename the device in Jeedom with a different name than the one in Proxmox

# 2019-11-12

- Added configuration information on VMs (agent, processors, memory, network)
- Added IPv4, IPv6 and MAC address information commands on VMs
- Adding the PVE version on the node configuration page
- Added commands giving the average load of the node
- Addition of a command giving swap usage
- Added a binary command indicating if updates are available on the node

# 2019-11-05

- Added more information on storage device
- Added a Backup command for VMs (check documentation for all options)

# 2019-10-28

- Fix an (non-blocking) error when starting and stopping the plugin
- Add translation for en_US

# 2019-10-26

- Added more information on nodes
- Added a Refresh command on nodes

# 2019-10-22

- Added support for linux containers (LXC)
- Added a command to take a snapshot on VM and LXC
- Added a Start, Shutdown and Stop immediately command on VM and LXC (see documentation)
- Added a Refresh command on VM and LXC
- Fixed problem connecting to Proxmox when the certificate is invalid

# 2019-10-21

First stable release

# Documentation

[See documentation]({{site.baseurl}}/{{page.pluginId}}/{{page.lang}})
