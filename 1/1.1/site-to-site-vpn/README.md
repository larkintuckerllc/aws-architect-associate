# Site-to-Site VPN

Site-to-Site VPN: By default, instances that you launch into an Amazon VPC can't communicate with your own (remote) network. You can enable access to your remote network from your VPC by creating an AWS Site-to-Site VPN (Site-to-Site VPN) connection, and configuring routing to pass traffic through the connection.

Although the term VPN connection is a general term, in this documentation, a VPN connection refers to the connection between your VPC and your own on-premises network. Site-to-Site VPN supports Internet Protocol security (IPsec) VPN connections.

Your Site-to-Site VPN connection is either an AWS Classic VPN or an AWS VPN.

Each Site-to-Site VPN connection has two tunnels, with each tunnel using a unique virtual private gateway public IP address.

You can use pre-shared keys, or certificates to authenticate your Site-to-Site VPN tunnel endpoints.

If you do not specify the IP address of your customer gateway device, we do not check the IP address.

If you do not configure IKE initiation from the AWS side for your VPN tunnel and the VPN connection experiences a period of idle time (usually 10 seconds, depending on your configuration), the tunnel might go down. To prevent this, you can use a network monitoring tool to generate keepalive pings, for example, by using IP SLA.

You can optionally enable acceleration for your Site-to-Site VPN connection. An accelerated Site-to-Site VPN connection (accelerated VPN connection) uses AWS Global Accelerator to route traffic from your on-premises network to an AWS edge location that is closest to your customer gateway device.

Route tables determine where network traffic from your VPC is directed. In your VPC route table, you must add a route for your remote network and specify the virtual private gateway as the target. This enables traffic from your VPC that's destined for your remote network to route via the virtual private gateway and over one of the VPN tunnels. You can enable route propagation for your route table to automatically propagate your network routes to the table for you.

Network traffic sent over the Site-to-Site VPN connection to the virtual private gateway is free but network traffic sent over the Site-to-Site VPN connection from the virtual private gateway to the endpoint is billed at the standard AWS data transfer rate.

If you have multiple AWS Site-to-Site VPN connections, you can provide secure communication between sites using the AWS VPN CloudHub. This enables your remote sites to communicate with each other, and not just with the VPC. The VPN CloudHub operates on a simple hub-and-spoke model that you can use with or without a VPC.

**note:** For redundancy, can setup multiple customer gateways to single Virtual Private Gateway.
