# Minimal Stack

This stack is optimized for cost. And this is one stack to run all different sort of enviroments (dev, stage, prod, etc.)

1. Service Discovery | 24x7 |  Node? (what should be its name?)
   
   * Consul
   * Housekeeper

   **Instance Type** Nano

   Why?

   This needs to be up and running always as other apps need it for discovery. Running 24x7

2. Tools Node
      
   * Nexus
   * GoCD
   * Docker Registry
   * ToolsPortal
   * Service Generator

   **Instance Type** Medium

   Why?

   Global running tools. This node can be shutdown during non working hours and weekends.

3. Monitoring Node

   * ELK
   * GKC

   **Instance Type** Medium

   Why?
   
   This node can be shutdown during non working hours and weekends.   

4. Dev Node

   * Apps (1...N)
   * Databases (1..N)

   **Instance Type** Medium

   Why?

   This node can be shutdown during non working hours and weekends.

5. Stage Node

   * Apps (1...N)
   * Databases (1..N)

   **Instance Type** Medium

   Why?

   This node can be shutdown during non working hours and weekends.   

6. Prod Node

   * Apps (1...N)
   * Databases (1..N)

   **Instance Type** Medium or Large

   Why?

   Running 24x7. As this is prod!

---


* S3 buckets to store backups of databases?
* S3 buckets to store images?


---

## Approximate Cost per Month
