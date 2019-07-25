# Cost-Optimized Compute

## COST-OPTIMIZED EC2 SERVICES

- **Choose the correct instance size for your workload**, categories of instances:
  - General Purpose
  - Compute Optimized
  - Memory Optimized
  - Accelerated Computing
  - Storage Optimized
- **Save costs through the use of reserved instances:** Using reserved computing capacity in AWS can save as much as 75 percent off using the default on-demand pricing model. three different types of reserved instances:

  - **Standard RIs**: These RIs are best suited for steady-state usage. These types offer the largest potential discount over on-demand computing instances.
  - **Convertible RIs**: These RIs enable you to change the attributes of the RIs. Your changes must be of equal or lesser cost value to the initial reservation. The potential discount with these types is lower, reaching approximately 55 percent off on-demand pricing.
  - **Scheduled RIs:** These RIs are launched within a certain time window.
    > Note
    > A common misconception is that an RI is a contract on an instance. Instead, it is merely instance capacity. For example, if you run 100 EC2 instances, but many come and go at any given time, and you purchase 20 RIs, those RIs are applied to the capacity, evaluated every hour. So every hour the billing system indicates you have 20 RIs to apply, and it looks for capacity to apply the contract pricing to. It is not bound to an instance.

- **Consider the use of the spot market for EC2 instances:** This approach enables you to bid on EC2 compute capacity. Most of the time spot pricing is substantially cheaper than on-demand and many times cheaper than RIs. The price is based on supply and demand at the AZ level. Savings can be as much as 90 percent off other alternatives.

- **Monitor, track, and analyze service usage:** You can use CloudWatch and Trusted Advisor to ensure you are right-sizing your EC2 computing power and balancing it against costs.

- **Analyze costs with tools in your billing dashboard and the Cost Explorer online tool:** You can set billing alarms, budgets, and other such valuable monitoring tools within the billing dashboard. You can also use powerful cost estimators when needed. Online you can find the Simple Monthly Cost Estimator that can help you with architecting decisions around costs.

## COST-OPTIMIZED LAMBDA SERVICES

- You can choose the amount of memory available for functions you are to run; this assignment ranges from 128 MB to 3 GB.

- Based on memory selection, Lambda allocates a proportional amount of CPU and other resources.

- Billing is based on gigabytes per seconds consumed; this means that a 256 MB function invocation that runs for 100 ms will cost twice as much as a 128 MB function that runs for 100 ms.

- For billing purposes, function duration is rounded to the **nearest 100 ms.**

### two primary metrics

- Allocated Memory Utilization
  - Watching this metric, you can decrease memory allocation on functions that are overprovisioned and watch for increasing memory use that may indicate functions becoming underallocated.
- Billed Duration Utilization
  - In this case it may make sense to decrease the memory setting of this function so that the runtime is closer to 100 ms with significantly lower costs
  - rewrite the function to perform more work per invocation, for example, processing multiple items from a queue instead of one—to increase Billed Duration Utilization
  - increasing the memory setting can result in lower costs and better performance. Consider a 1 GB function that runs in 110 ms. This will be billed as 200 ms. Increasing the memory setting slightly may allow the function to execute under 100 ms, which will decrease the billing duration by 50 percent and result in lower costs
