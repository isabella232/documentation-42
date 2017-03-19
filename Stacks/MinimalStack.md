# Minimal Stack

This stack is optimized for cost. And this is one stack to run all different sort of enviroments (dev, stage, prod, etc.) No clustering support.

0. Bastion Host

   **Instance Type** Nano	

   Always running! Best practices based approach to access the other nodes in the network.

1. Service Discovery | 24x7 | SDH | Node? (what should be its name?)
   
   * ETCD? _DO WE NEED IT? THERE WONT BE ANY CLUSTERING IN THIS CASE?_
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
   
   This node can be shutdown during non working hours and weekends. One node for all environments to optimize cost. Logs from different nodes will be tagged to differentiate between environments.

4. Dev Node

   * Apps (1...N)
   * Backing Services (databases, mq's) (1..N)

   **Instance Type** Medium

   Why?

   This node can be shutdown during non working hours and weekends.

5. Stage Node

   * Apps (1...N)
   * Backing Services (databases, mq's) (1..N)

   **Instance Type** Medium

   Why?

   This node can be shutdown during non working hours and weekends.   

6. Prod Node

   * Apps (1...N)
   * Backing Services (databases, mq's) (1..N)

   **Instance Type** Medium or Large

   Why?

   Running 24x7. As this is prod!

---

## Considerations

* Network topology? Ideally should be best practices based and databases should be run in a private persistence subnet. This might result in higher cost?
* 	

---


* S3 buckets to store backups of databases?
* S3 buckets to store images?
* S3 bucket to host maintenance site?

---

## Approximate Cost per Month

### Running Always

| Node          | Runtime       | Cost  |
| ------------- |:-------------:| -----:|
| SDH           | always        |    $0 |
| Tools         | always        |    $0 |
| Monitoring    | always        |    $0 |
| DEV           | always        |    $0 |
| Stage         | always        |    $0 |
| Prod          | always        |    $0 |

### Not Running Always


| Node          | Runtime       | Cost  |
| ------------- |:-------------:| -----:|
| SDH           | always        |    $0 |
| Tools         | always        |    $0 |
| Monitoring    | always        |    $0 |
| DEV           | always        |    $0 |
| Stage         | always        |    $0 |
| Prod          | always        |    $0 |

