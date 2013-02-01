munin-plugins
=============

Two Munin plugins I wrote to monitor XEN virtual machines.

The only ones I found are written as shell scripts and apart from spawning a lot
of unnecessary processes (grep|awk and the like) the network plugin fails when a
domU has more than one network interface. So I rewrote them in Perl.

* xen\_cpu\_percent makes a stacked-area graph for CPU usage. It produces the
  same results as the original shell script, although I think it should actually
  account for number of physical CPUs. It has no configuration parameters.

* xen\_traffic\_all graphs network bandwidth usage for all domUs. Graphs will be
  named <domain><number> to allow for more than one interface per domU. My
  standard vserver has one external and one management interface so I need them
  separate. If you would like the bandwidths to simply be added, like for setups
  that use different intefaces for IPv4 and IPv6, you can set *env.summing* in
  Munin's configuration (e.g. /etc/munin/plugin-conf.d/munin-node) to 1.
