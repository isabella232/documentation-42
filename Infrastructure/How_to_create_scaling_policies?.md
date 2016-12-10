To enable dynamic scalling of your resources, you need to add scaling policies to your Auto Scaling Groups.

Policies basically determine when you need to scale up your resources or scale down your resources. They use Cloud Watch Alarms to achieve this.

You can use policy modules (from https://github.com/stakater/blueprint-instance-pool-aws/tree/master/modules/asg-policy) to create your policies.

The main parameters for the policy module are 

1- adjustment_type -> ChangeInCapacity — Increase or decrease the current capacity of the group by the specified number of
                                         instances. A positive value increases the capacity and a negative adjustment value
                                         decreases the capacity.
                                         
                      ExactCapacity    — Change the current capacity of the group to the specified number of instances. Note
                                         that you must specify a positive value with this adjustment type.
                                         
                      PercentChangeInCapacity — Increment or decrement the current capacity of the group by the specified
                                             percentage. A positive value increases the capacity and a negative value decreases
                                             the capacity. If the resulting value is not an integer, Auto Scaling rounds it.
2- scaling_adjustment ->  The number/percentage instances by which to scale
3- cooldown           ->  Wait time in second before applying the scaling policy again
4- comparison_operator -> The comparison operator to use to decide if policy is to be applied or not e.g
                          GreaterThanOrEqualToThreshold
5- period              -> Number of seconds to be used as the base time measurement unit
6- evaluation_periods  -> After how many periods should the policy re-check if it should raise Alarm
7- metric_name         -> Metric whose value is used to check policy
8- threshold           -> Maximum value of choosen matric that can activate policy check
9- min_adjustment_magnitude -> minimum amount change to resources (available when adjustmentType is PercentChangeInCapacity)

References:
http://docs.aws.amazon.com/autoscaling/latest/userguide/as-scale-based-on-demand.html
