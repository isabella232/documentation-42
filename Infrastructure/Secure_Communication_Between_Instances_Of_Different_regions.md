# Secure communication between private resources in different regions

If you have a scenario where you have some resources in private subnet of one region e.g your webapp with load balancer attached and you have some other resources in another region e.g database or your EFS.

You have to enable public access to your database since cross-region VPC peering is not available which helps you access resources in a different VPC privately. Making these resources public puts you at a lot of risk. So how do you restrict access of your EFS or database?

The only solution is to add IP based restrictions. For this you allow your webapp to access internet via NAT gateway. You then assign an elastic IP to that NAT gateway. So now all the calls that you make to internet from your webapp will use this attached elastic IP and there you go. Bingo! Even if you have multiple resources/web apps running. As long as they are attached to the same NAT gateway. They will have the same IP address.

So in case of stakater, All the resources that you created in let's say private sub-net of dev environment, will use the NAT gateway to access internet and will thus have the same IP. You can get this IP address from the outputs of network module with name `nat_public_ip`
