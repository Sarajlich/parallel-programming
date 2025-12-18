# Muhamed-Sarajlic-Parallel-Programming-Assignments


![](squeue.png)

![](topcompute.png)
script executed using sbatch 4 times, each job requested 4cpus

![](topoverload.png)
Without Slurm: 
stress executed in 3 terminals, 
resuling in system slowdown and cpu oversubscription. 

![](TOPTERMINAL.png)
With Slurm: 
stress exectued via batch, slurm handled resource alloc correctly