# create a virtual private gateway # attach this gateway with vpc
# create a customer gateway
  1. routing is static
  2. ip address= ip address of ec2 instance for which we want to establish the connection(other region)
  3. click on create customer gateway

# create site to site vpn connection
  # click on vpn connection
  # name
  # choose virtual private gateway
  # customer gateway
  # routing static
  # ststic ip prifixes = cidr of other side subnet

# click on create vpn connection

