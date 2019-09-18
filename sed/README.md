Solve the following questions
-----------------------------
<ol type="1">
  <li>A file named "interfaces" has network configuration settings</li>
  <pre>
  root@OpenStack:/etc/network# cat interfaces
  # This file describes the network interfaces available on your system
  # and how to activate them. For more information, see interfaces(5).    
    source /etc/network/interfaces.d/*

    # The loopback network interface
    auto lo
    iface lo inet loopback

    # The primary network interface
    auto ens160
    iface ens160 inet static
            address 10.0.0.111
            netmask 255.255.255.0
            network 10.0.0.0
            broadcast 10.0.0.255
            gateway 10.0.0.1
            # dns-* options are implemented by the resolvconf package, if installed
            dns-nameservers 10.10.0.111
            dns-search OpenStackDomainName
  <pre>
  <li>using sed command replace the ip 10.0.0.111 to 10.0.0.113 by keeping a backup file</li>
</ol>
