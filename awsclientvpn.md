1. Before we touch the vpn client we must generate certificates and upload them to the aws certificate manager. This can be done with a variety of tools and methods.

2. On the left panel under "Virtual Private Network (VPN)", click on "Client VPN Endpoints"
3. Provide a Name Tag, Description, Client IPv4 CIDR block, server certificate Amazon Resource Name, and authentication options. We will use mutual authentication since we are using a certificate based validation.
4. You can enable client connections in order to 
