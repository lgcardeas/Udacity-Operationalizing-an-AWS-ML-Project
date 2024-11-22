## Configuration 
	SageMaker Endpoint Autoscaling:
		-	Target Metric: 3 invocations per instance
		-	Min Instances: 1
		-	Max Instances: 5
	Lambda Provisioned Concurrency:
		-	Concurrency: 5 pre-warmed Lambda instances

### Why This Setup Works
	Proactive Scaling with Lower Target Metric: 
		-	By setting the target metric to 3 invocations per instance, the SageMaker endpoint will now scale up faster as traffic increases. This ensures sufficient capacity to handle traffic spikes without waiting for a high invocation count.
	Efficient Lambda Responsiveness:
		-	Keeping 5 provisioned Lambda instances ensures steady and low-latency handling of up to 5 concurrent requests.
		-	Any traffic beyond 5 requests will trigger Lambda’s on-demand scaling, where new Lambda instances are spun up (introducing possible cold starts).

### Expected Behavior
	- At low traffic:
	- The SageMaker endpoint will remain at 1 instance, capable of handling up to 3 invocations per second.
	- All requests from the 5 pre-warmed Lambda instances will be processed with minimal delay.
	- At moderate traffic:
	- When invocations exceed 3 per instance, the endpoint will scale up additional instances to handle the load efficiently (up to the configured max instances).
	-	The 5 pre-warmed Lambdas will continue to serve traffic seamlessly.
	-	At high traffic:
	-	If traffic exceeds 5 concurrent requests, Lambda will spin up new instances on-demand, introducing possible cold starts for additional requests.
	-	The SageMaker endpoint will scale to its maximum configured instance count, ensuring it can handle sustained high traffic.

### Key Advantages
	- Improved Responsiveness: Lowering the target metric to 3 invocations per instance ensures the endpoint scales early to handle surges in traffic.
	- Cost Efficiency: Maintaining 5 provisioned Lambda instances ensures consistent performance for steady traffic while avoiding over-provisioning.
	- Balanced Traffic Handling: The configuration aligns Lambda’s concurrency with the endpoint’s scaling behavior, ensuring a smooth response to traffic variations.