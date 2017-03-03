# Minimal Stack

This stack is optimized for cost. And this is one stack to run all different sort of enviroments (dev, stage, prod, etc.)

1. Service Discovery | 24x7 |  Node? (what should be its name?)
   Type Nano
   
   Consul
   Housekeeper

   Why?
   This needs to be up and running always as other apps need it for discovery. Running 24x7

2. Tools Node
   Type Medium
   
   Nexus
   GoCD
   Docker Registry
   ToolsPortal

   Why?
   Global running tools.
   This node can be shutdown during non working hours and weekends.

3. Monitoring Node


   ELK
   GKC

   Why?
   This node can be shutdown during non working hours and weekends.   

4. Dev Node
   Type Medium?

   Apps (1...N)
   Databases (1..N)

   Why?
   This node can be shutdown during non working hours and weekends.

5. Stage Node
   Type Medium?

   Apps (1...N)
   Databases (1..N)

   Why?
   This node can be shutdown during non working hours and weekends.   

6. Prod Node
   Type Medium?

   Apps (1...N)
   Databases (1..N)

   Why?
   This node can be shutdown during non working hours and weekends.


Estimated Cost per Month
