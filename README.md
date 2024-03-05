# create a virtual private gateway # attach this gateway with vpc
# create a customer gateway
  1. routing is static
  2. ip address= ip address of ec2 instance for which we want to establish the connection(other region)
  3. click on create customer gateway

# create site to site vpn connection
  * click on vpn connection
  * name
  * choose virtual private gateway
  * customer gateway
  * routing static
  * ststic ip prifixes = cidr of other side subnet

# click on create vpn connection

# download the configuration file

# Go to route table in vpnside 
  * add the route propogation

# login to instance on other side
  * Commands for Installation of Openswan
    i. Change to root user: 
                $ sudo su
    ii. Install openswan:
                $ yum install openswan -y
    iii. In /etc/ipsec.conf uncomment following line if not already 
          uncommented:
                 include /etc/ipsec.d/*.conf
    iv. Update /etc/sysctl.conf to have following
 net.ipv4.ip_forward = 1
 net.ipv4.conf.all.accept_redirects = 0
 net.ipv4.conf.all.send_redirects = 0
    v. Restart network service:
                 $ service network restart

    #  Command for /etc/ipsec.d/aws-vpn.conf
conn Tunnel1
        authby=secret
        auto=start
        left=%defaultroute
        leftid=Customer end Gateway VPN public IP
        right=AWS Virtual private gateway ID- public IP
        type=tunnel
        ikelifetime=8h
        keylife=1h
        phase2alg=aes128-sha1;modp1024
        ike=aes128-sha1;modp1024
        keyingtries=%forever
        keyexchange=ike
        leftsubnet=Customer end VPN CIDR
        rightsubnet=AWS end VPN CIDR
        dpddelay=10
        dpdtimeout=30
        dpdaction=restart_by_peer

3. Contents for  /etc/ipsec.d/aws-vpn.secrets
customer_public_ip aws_vgw_public_ip: PSK "shared secret"

4. Commands to enable/start ipsec service
           $ chkconfig ipsec on
           $ service ipsec start
           $ service ipsec status
