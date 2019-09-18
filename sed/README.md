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
  </pre>
  using sed command replace the ip 10.0.0.111 to 10.0.0.113 by keeping a backup file
  
  <li>Assume that the following set of commands are executed in a linux terminal</li>
  <pre>
  mkdir infraclass
  touch infraclass/config
  INFRACLASS_REGION=Asia-e
  echo INFRACLASS_REGION=$INFRACLASS_REGION >> ~/infraclass/config
  INFRACLASS_PROJECT_ID=123#$56dfgttehiow
  echo INFRACLASS_PROJECT_ID=$INFRACLASS_PROJECT_ID >> ~/infraclass/config
  source infraclass/config
  echo $INFRACLASS_PROJECT_ID
  echo $INFRACLASS_PROJECT_ID
  </pre>
  What will be printed as an output of last 2 echo commands
  <li>Consider the following commands</li>
  <pre>
  blrk@rk-lpc:/rkdrive/sysadmin> ip route show
  default via 192.168.1.1 dev eth2  proto static  metric 100 
  10.0.0.0/24 dev virbr1  proto kernel  scope link  src 10.0.0.1 
  172.17.0.0/16 dev virbr3  proto kernel  scope link  src 172.17.0.1 
  192.168.0.0/16 dev eth2  proto kernel  scope link  src 192.168.1.101  metric 100 
  192.168.100.0/24 dev virbr0  proto kernel  scope link  src 192.168.100.1 
  192.168.123.0/24 dev virbr123  proto kernel  scope link  src 192.168.123.1 
  192.168.126.0/24 dev virbr126  proto kernel  scope link  src 192.168.126.1   
  </pre>
  What will be the output suppose we run the following command
  <pre>
  ip route show | sed -n '/src/p' | sed -e 's/  */ /g' | cut -d' ' -f9
  </pre>
</ol>
