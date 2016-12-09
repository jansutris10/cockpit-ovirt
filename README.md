# Project moved

**This project has been moved to oVirt gerrit: [https://gerrit.ovirt.org/#/q/project:cockpit-ovirt](https://gerrit.ovirt.org/#/q/project:cockpit-ovirt).**

This repository is no more used for development.

This project became base for ongoing development around Cockpit and Virtual Machines, some of the interesting follow-ups:

* **[cockpit-ovirt](https://gerrit.ovirt.org/#/q/project:cockpit-ovirt)** - View of oVirt host absed on VDSM. Among the others, part of the oVirt NextGen Node.
* **Machines** in upstream [Cockpit](http://www.cockpit-project.org) based on Libvirt, added by [4434 PR](https://github.com/cockpit-project/cockpit/pull/4434) followed by multiple other patches
* **External Providers** for 'machines' plugin in Cockpit to allow integration of upstream code with other providers, like VDSM, ManageIQ or other.

# Cockpit-oVirt plugin
[![Build Status](https://travis-ci.org/mareklibra/cockpit-ovirt.svg?branch=master)](https://travis-ci.org/mareklibra/cockpit-ovirt)

Virtual Machine Management plugin for Cockpit based on oVirt (VDSM).

Features in recent release:

* list of VMs running on a host
* single VM detail
* VM monitoring (statistics and usage charts)
* basic VM operations
* edit of vdsm.conf
* plugin's components are embeddable to other tools/dashboard, like VM detail

* With optional Engine login available
    * list of VMs administered by the oVirt Engine in a cluster
    * VM details


The plugin requires Virtual Desktop Server Manager [VDSM](http://www.ovirt.org/Installing_VDSM_from_rpm), part of the oVirt project.

With **optional** [oVirt Engine](http://www.ovirt.org/Quick_Start_Guide) installed, the plugin allows basic monitoring/management of VMs administered by the engine beyond the scope of the single host running the cockpit.

### About Cockpit
[Cockpit](http://cockpit-project.org/) is easy-to-use sysadmin tool with web-based UI.

### About oVirt
[oVirt](http://www.ovirt.org/Home) manages Virtual Machines (VMs) in a datacenter/cluster.
Scales easily from tens to tens of thousands VMs running on multiple KVM hypervisor hosts.

The oVirt deals with
* VM definition, monitoring and tuning
* (automatic|manual) migration
* storage or network management
* SLA
* security
* easy to use web UI
* and more (see [website](http://www.ovirt.org/Home))


## How to Install
### Prerequisites
* Install [VDSM](http://www.ovirt.org/Installing_VDSM_from_rpm)
    * recently only **master** oVirt release is supported
    * Centos 7 (minimal):
        * have FQDN, DNS, DHCP set and working
        * yum install http://resources.ovirt.org/pub/yum-repo/ovirt-release-master.rpm
        * yum install vdsm

* Optional: Install [oVirt Engine](http://www.ovirt.org/Quick_Start_Guide)
    * recently only **master** oVirt release is supported
    * Centos 7 (minimal):
        * have FQDN, DNS, DHCP set and working
        * yum install http://resources.ovirt.org/pub/yum-repo/ovirt-release-master.rpm
        * yum install ovirt-engine
        * engine-setup
        * add host from previous step to the engine
        * more at http://www.ovirt.org/documentation/quickstart/quickstart-guide/ 

* Install [Cockpit](http://cockpit-project.org/running.html)
    * yum install cockpit
    * make sure cockpit is started/enabled:
        * systemctl enable cockpit.socket
        * systemctl start cockpit

### Install From Sources
#### Build
For build you will need [Node.js](https://nodejs.org/) v4 (LTS). If your OS repositories don't contain
required version you can always use Node Version Manager [nvm](https://github.com/creationix/nvm) to
install and manage multiple Node.js versions side by side.

Run `npm i` to install dependencies.

Use `npm t` to run tests and lint the code.

Use `npm run build` to create production build.

The last command will generate `/dist` directory containing all files that are needed to be copied to your
cockpit installation.

Developer's note: you can use `npm run dev` to start a background build service that will incrementally
recompile the code on the fly and update the contents of `/dist` directory. Symbolically linking the `/dist`
directory into proper place (see below) one can achieve automatic code updates in running cockpit instance.

#### Deploy Plugin
* after build, copy contents of `/dist` to /root/.local/share/cockpit/ovirt/

* **Alternative:**
    * copy contents of `/dist` to /usr/share/cockpit/ovirt/
    * change VDSM variable in ovirt.js to new location of vdsm/vdsm shell script

* Troubleshooting tips:
    * Installation instructions stated above should lead to successful setup on Centos 7. If not, following tips might help:
        * If VDSM is properly configured, following command should return without any error:

            \# /root/.local/share/cockpit/ovirt/vdsm/vdsm getAllVmStats

    * As the plugin is in early development state, **PLEASE let author know about all issues you encounter during installation/use**, it will help in making the product better.

### Install From RPM
RPM is recently built for Fedora 23 and Centos 7 and stored within oVirt's ovirt-master-snapshot-static repo.

* Please meet **Prerequisites**
* enable repo
    * yum install http://resources.ovirt.org/pub/yum-repo/ovirt-release-master.rpm 
* install RPM
    * yum install cockpit
    * yum install cockpit-ovirt

### Verify
* Follow:
    * https://YOUR_HOST:9090/ovirt/ovirt
    * or https://YOUR_HOST:9090/ovirt/ovirt#/ping

## TODO:
Please note, the plugin is in early development state.

See the issue tracker for list of planed changes.

## More Info
* About [oVirt](http://www.ovirt.org/Home)
* oVirt [Quick Start Guide](http://www.ovirt.org/Quick_Start_Guide)
* About [Cockpit](http://cockpit-project.org/)

