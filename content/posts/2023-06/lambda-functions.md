---
title: "🚫 Why You Should Reconsider Using AWS Lambdas"
date: 2023-06-21
showToc: true
tags: ["lambda", "aws", "devops", "data-engineering"]
---


## 🧩 Complexity Overload

While AWS Lambdas offer great flexibility, they also introduce additional complexity to your application architecture. Implementing complex business logic and handling dependencies within small, isolated functions can be challenging and lead to code duplication. Managing a large number of Lambdas can become unwieldy, impacting development and maintenance efforts.

This can be mitigated by using the [serverless framework](https://www.serverless.com/framework/docs) but there are still other engineering challenges

### 🔌 Integration Challenges

Integrating AWS Lambdas with existing infrastructure or third-party services can present challenges. You may encounter compatibility issues, necessitating additional workarounds or modifications to make Lambdas seamlessly interact with other components of your application stack.

This is particular notable when trying to use lambdas to process data and using the `pandas` and `numpy` packages. When these are packaged within the `lambda` function alongside the `pyarrow` package, they can easily exceed the hard limit of  **250 MB** limit.

As such, you would either have to rewrite your lambda to avoid using these packages which has the potential to increase tech debt or alternatively use the managed AWS Lambda Layers.

Refer to the published layers [here](https://aws-sdk-pandas.readthedocs.io/en/stable/layers.html).

### ⚙️ Cold Start Performance

One of the limitations of AWS Lambdas is the cold start time, which can result in longer response times for infrequently invoked functions. If your application requires immediate and consistent response times, Lambdas may not be the optimal choice. Long cold start times can impact user experience and lead to dissatisfaction.


## Hard Limitations

There are hard limits associated with Lambda functions, these are:


| AWS Lambda Limits              | Limit                                              |
|-------------------------------|----------------------------------------------------|
| Execution Time                | Maximum of **900 seconds** (15 minutes) per function invocation. |
| Memory                        | Allocated up to **10,240 MB** (10 GB), with a minimum of 128 MB. |
| Deployment Package Size       | Limited to **250 MB** for direct upload.            |
| Environment Variables        | Up to **4 KB** of combined key-value data.          |
| Function Payload              | Input/output payload can be up to **6 MB** in size. |
| Concurrent Executions         | Initially set to **1,000** per region, but can be increased through AWS support. |
| Deployment Package Extraction | Extraction to `/tmp` directory limited to **512 MB** of storage space. |



## 💰 Cost Considerations

Though AWS Lambdas are cost-efficient for low-traffic or sporadic workloads, they may not be the most cost-effective solution for high-traffic or continuously running applications. Lambda costs are calculated based on execution time and resource usage, which can quickly escalate if your application has high usage patterns or requires frequent invocations.

Here is a [key example from Amazon Prime Video](https://www.primevideotech.com/video-streaming/scaling-up-the-prime-video-audio-video-monitoring-service-and-reducing-costs-by-90) which moved away from AWS Lambdas whereby moving towards a monolith application reduced costs by 90%.



## 🛠️ Use Cases and Alternatives

While Lambdas are a powerful tool, it's crucial to evaluate whether they align with your specific use case.
### Alternatives
- A step above using straight AWS lambda functions is to use Lambda container images which mitigates the hard limit of **250 MB** but will require publishing to AWS ECR or similar repo to store these images so that they can be run. As such, this will further push out the start times as these images will need to be pulled from the repositories.
- If your application has predictable and constant workloads, consider using traditional server models or container-based solutions like AWS EC2 or ECS.

These alternatives offer more control over resources and reduced latency.

## 💭 Final Thoughts

AWS Lambdas undoubtedly have their merits, but they are not a one-size-fits-all solution. Consider your application requirements, development team expertise, cost considerations, and integration complexities before deciding to go serverless with Lambdas. Evaluate the trade-offs and explore alternative options to ensure you select the best-fit architecture for your project.

Remember, every application is unique, and careful consideration of the pros and cons is essential when making architectural decisions.