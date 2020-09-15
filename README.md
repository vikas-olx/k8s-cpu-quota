# CPU Quota in Kubernetes

CPU quota is evaluated in fixed periods, for example, 100ms.
It means- 
	* if you request for 1 cpu, then you are guaranteed 100ms of CPU time every 100ms.
	* If you request for 2 cpu, you are guaranteed 200ms of CPU time every 100ms.
	* If you request for 5 cpu, you are guaranteed 500ms of CPU time every 100ms.
Further, CPU is allocated in slots of time period (say 10ms). It means that once you get a CPU, you are guaranteed to get 10ms of CPU time before being interrupted and CPU allocated to a different task.
So, if you request 1 CPU, every 100ms, you can get any of these:
	* 10 un-interrupted slots of 10ms on a single CPU
	*  7 slots on one CPU and 3 slots on another CPU
	* 1 slot on 10 CPUs
	* Any other combination as long as sum is 100ms
If you request 700m CPU,  you can get any of these:
	* 7 slots on a single CPU
	* 2 slots on one CPU and 5 on other
	* 1 slot on 7 CPUs
	* Any other combination as long as sum of 70ms
If you request 3 CPU,  you can get any of these:
	* 10 un-interrupted slots on 3 CPUs
	* 5, 10, 7, 2, 6 slots on 5 CPUs
	* 1 slot on 30 CPUs
	* Any other combination as long as sum of 300ms
