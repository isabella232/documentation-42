Cost
====
One of the key thing we have been trying to achieve is to have minimal cost to run the whole infrastructure!

## ELB - Elastic Loadbalancers
Initially we had ELB's in front of every ASG and that was resulting in quite extra bucks every month; and now we have replaced them with soft loadbalancers.

## EBS - Elastic BlockStorage
Initially we attached 3 EBS per instance; and now we have made it optional and it has resulted in cost reduction as well.

## Schedule Start & Stop of Instances
For economic reason, the non-prod instances should be running only during a specified time window. And it should happen automatically. And this results in quite a lot of cost saving as well.

## Network Traffic?
