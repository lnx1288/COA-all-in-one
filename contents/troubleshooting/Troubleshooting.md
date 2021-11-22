## Troubleshooting Openstack

In the past, the COA requirements included a Troubleshooting section 
detailing the key aspects you needed to master. That is not the case 
any more (at least at the time of this writing) but I have included 
some troubleshooting content here for completeness.

Troubleshooting Openstack is far from a trivial task. Overall, you
should get at least be familiar with the following topics in order 
to start acquiring troubleshooting experience:

  * Configuration files for Openstack and related services
  * Openstack component interactions and key workflows (e.g., instance
creation process)
  * Log files for Openstack services and other relevant log files (e.g., 
`kern.log` in Linux for system-level messages)
  * Openstack services monitoring/management
  * Network troubleshooting (e.g., instance connectivity not working)

The sections below mostly benefit from the [Openstack Operations Guide](https://docs.openstack.org/operations-guide/),
although some additional resources have been included for completeness. 
A comprehensive troubleshooting guide from Red Hat can be found [here](https://access.redhat.com/documentation/en-us/red_hat_openstack_platform/16.2/html/logging_monitoring_and_troubleshooting_guide/index). Note that this is
for RED HAT OPENSTACK PLATFORM 16.2. You may need to find the most recent 
version at the time you're reading this.  


### Configuration files

  * [Common OpenStack Configuration Files and Services](https://docs.oracle.com/cd/E65465_01/html/E57770/app-configfiles.html)

Typically, configuration files for Openstack can be found in 
`/etc/<service>/`, e.g., `/etc/neutron/neutron.conf`. However, since 
some services may require/depend on other non-Openstack services/tools,
you may need to be familiar with those config files as well (e.g.,
`/etc/rsyncd.conf`, `rsync` config file, `rsync` is used/required by 
Swift).

### Logging

  * [Openstack logging](https://docs.openstack.org/operations-guide/ops-logging.html)

### Monitoring

  * [Openstack monitoring](https://docs.openstack.org/operations-guide/ops-monitoring.html)

When monitoring Openstack services, it is quite useful to be familiar
with `systemd` and with the `systemctl` command. A useful resource for
this can be found [here](https://wiki.debian.org/systemd).

### Network troubleshooting

  * [Openstack network troubleshooting](https://docs.openstack.org/operations-guide/ops-network-troubleshooting.html)